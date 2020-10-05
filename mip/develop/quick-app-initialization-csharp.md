---
title: Démarrage rapide – Initialisation pour les clients C# du SDK Microsoft Information Protection (MIP)
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes C# du SDK Microsoft Information Protection (MIP).
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 09/15/2020
ms.author: tommos
ms.custom: has-adal-ref
ms.openlocfilehash: 406068f5770f489c66963fc34a462ec7e205765b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108959"
---
# <a name="quickstart-client-application-initialization-c"></a>Démarrage rapide : Initialisation d’une application cliente (C#)

Ce guide de démarrage rapide montre comment implémenter le modèle d’initialisation de client utilisé par le wrapper .NET du SDK MIP au moment de l’exécution.

> [!NOTE]
> Les étapes décrites dans ce guide de démarrage rapide sont requises pour toute application cliente qui utilise les API de fichier ou de stratégie du wrapper .NET du MIP. L’API de protection n’est pas encore disponible. Bien que ce guide de démarrage rapide illustre l’utilisation des API de fichier, ce même modèle s’applique aux clients utilisant les API de stratégie et de protection. Les guides de démarrage rapide futurs doivent être consultés dans l’ordre, car chacun s’appuie sur le précédent, celui-ci étant le premier.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas déjà fait, veillez à :

- Exécuter la procédure fournie dans [Installation et configuration du kit SDK Microsoft Information Protection (MIP)](setup-configure-mip.md). Ce guide de démarrage rapide « initialisation d’une application cliente » s’appuie sur une installation et une configuration correctes du kit SDK.
- Éventuellement :
  - Passez en revue [Objets de profil et moteur](concept-profile-engine-cpp.md). Les objets de profil et moteur sont des concepts universels, requis par les clients qui utilisent les API MIP de fichier/stratégie/protection.
  - Passez en revue les [concepts d’authentification](concept-authentication-cpp.md) pour savoir comment l’authentification et le consentement sont implémentés par le kit SDK et l’application cliente.

## <a name="create-a-visual-studio-solution-and-project"></a>Créer une solution et un projet Visual Studio

Tout d’abord, nous créons et configurons la solution et le projet Visual Studio initiaux, sur lesquels les autres guides de démarrage rapide s’appuieront.

1. Ouvrez Visual Studio 2017, sélectionnez le menu **Fichier**, **Nouveau**, **Projet**. Dans la boîte de dialogue **Nouveau projet** :
   - Dans le volet gauche, sous **Installé**, **Visual C#** , sélectionnez **Windows Desktop**.
   - Dans le volet central, sélectionnez **Application console (.NET Framework)**
   - Dans le volet inférieur, mettez à jour les champs **Nom**, **Emplacement** et **Nom de la solution** contenante du projet en conséquence.
   - Lorsque vous avez terminé, cliquez sur le bouton **OK** dans le coin inférieur droit.

     [![Création d’une solution dans Visual Studio](media/quick-app-initialization-csharp/create-vs-solution.png)](media/quick-app-initialization-csharp/create-vs-solution.png#lightbox)

2. Ajoutez le package Nuget pour l’API de fichier du kit SDK MIP dans votre projet :
   - Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet (directement sous le nœud supérieur/de solution), puis sélectionnez **Gérer les packages NuGet...**  :
   - Lorsque l’onglet **Gestionnaire de Package NuGet** s’ouvre dans la zone des onglets du groupe d’éditeurs :
     - Sélectionnez **Parcourir**.
     - Dans la zone de recherche, entrez « Microsoft.InformationProtection ».
     - Sélectionnez le package « Microsoft.InformationProtection.File ».
     - Cliquez sur « Installer », puis cliquez sur « OK » lorsque la boîte de dialogue de confirmation **Aperçu des modifications** apparaît.

3. Répétez les étapes ci-dessus pour ajouter le package de l’API de fichier SDK MIP, en ajoutant cette fois « Microsoft.Identity.Client » à l’application.

## <a name="implement-an-authentication-delegate"></a>Implémenter un délégué d’authentification

Le kit SDK MIP implémente l’authentification en utilisant l’extensibilité de classe, qui fournit un mécanisme pour partager le travail d’authentification avec l’application cliente. Le client doit acquérir un jeton d’accès OAuth2 approprié et le fournir au kit SDK MIP au moment de l’exécution.

Maintenant, créez une implémentation pour un délégué d’authentification, en étendant l’interface `Microsoft.InformationProtection.IAuthDelegate` du SDK et en remplaçant/implémentant la fonction virtuelle `IAuthDelegate.AcquireToken()`. Le délégué de l’authentification est instancié et utilisé plus tard par les objets `FileProfile` et `FileEngine`.

1. Cliquez avec le bouton droit sur le nom du projet dans Visual Studio, sélectionnez **Ajouter**, puis sélectionnez **Classe**.
2. Entrez « AuthDelegateImplementation » dans le champ **Nom**. Cliquez sur **Ajouter**.
3. Ajoutez les instructions using de la Bibliothèque d’authentification Microsoft (ADAL) et de la bibliothèque MIP :

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.Identity.Client;
     ```

4. Définissez `AuthDelegateImplementation` pour hériter `Microsoft.InformationProtection.IAuthDelegate` et implémenter une variable privée de `Microsoft.InformationProtection.ApplicationInfo` ainsi qu’un constructeur qui accepte le même type.

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
    {
        private ApplicationInfo _appInfo;
        // Microsoft Authentication Library IPublicClientApplication
        private IPublicClientApplication _app;
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }

    }
     ```

    L’objet `ApplicationInfo` contient trois propriétés. `_appInfo.ApplicationId` sera utilisé dans la classe `AuthDelegateImplementation` pour fournir l’ID client à la bibliothèque d’authentification. `ApplicationName` et `ApplicationVersion` figureront dans les rapports d’analyse Azure Information Protection.

5. Ajoutez la méthode `public string AcquireToken()`. Cette méthode doit accepter `Microsoft.InformationProtection.Identity` ainsi que trois chaînes : l’URL authority, l’URI resource et les revendications, si nécessaire. Ces variables de chaîne seront passées à la bibliothèque d’authentification par l’API et ne doivent pas être modifiées. Entrez le GUID issu du Portail Azure de votre locataire. Si vous modifiez d’autres chaînes que le GUID du locataire, l’authentification risque d’échouer.

     ```csharp
    public string AcquireToken(Identity identity, string authority, string resource, string claims)
    {
        var authorityUri = new Uri(authority);
        authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

        _app = PublicClientApplicationBuilder.Create(_appInfo.ApplicationId).WithAuthority(authority).WithDefaultRedirectUri().Build();
        var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

        // Append .default to the resource passed in to AcquireToken().
        string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
        var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                   .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

        return result.AccessToken;
    }

     ```

## <a name="implement-a-consent-delegate"></a>Implémenter un délégué de consentement

Maintenant, créez une implémentation pour un délégué de consentement, en étendant l’interface `Microsoft.InformationProtection.IConsentDelegate` du SDK et en remplaçant/implémentant `GetUserConsent()`. Le délégué de consentement est instancié et utilisé plus tard par les objets de profil de fichier et de moteur de fichier. Le délégué de consentement est fourni avec l’adresse du service dont l’utilisation doit être consentie par l’utilisateur dans le paramètre `url`. Le délégué doit généralement fournir un flux qui permette à l’utilisateur de donner ou refuser son consentement pour l’accès au service. Dans le cadre de ce guide de démarrage rapide, vous devez coder `Consent.Accept` en dur.

1. À l’aide de la même fonctionnalité « Ajouter une classe » de Visual Studio que nous avons utilisée précédemment, ajoutez une autre classe dans votre projet. Cette fois, entrez « ConsentDelegateImplementation » dans le champ **Nom de la classe**.

2. Maintenant, mettez à jour **ConsentDelegateImpl.cs** pour implémenter votre nouvelle classe de délégué de consentement. Ajoutez l’instruction using pour `Microsoft.InformationProtection` et définissez la classe afin qu’elle hérite `IConsentDelegate`.

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. Si vous le souhaitez, essayez de générer la solution pour vous assurer qu’elle se compile sans erreur.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Initialiser le wrapper managé du SDK MIP

1. À partir de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Supprimez l’implémentation générée de `main()`.

3. Le wrapper managé inclut une classe statique, `Microsoft.InformationProtection.MIP`, qui est utilisée pour l’initialisation, la création d’un `MipContext`, le chargement des profils et la libération des ressources. Pour initialiser le wrapper pour les opérations d’API de fichier, appelez `MIP.Initialize()`, en passant `MipComponent.File` qui charge les bibliothèques nécessaires aux opérations de fichier.

4. Dans la section `Main()` du fichier *Program.cs*, ajoutez ce qui suit, en remplaçant **\<application-id\>** par l’ID de l’inscription d’application Azure AD que nous avons créée.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.File;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for File API operations
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>Construire un moteur et un profil de fichier

Comme nous l’avons mentionné précédemment, des objets de profil et de moteur sont nécessaires pour les clients du SDK utilisant des API MIP. Terminez la phase de codage de ce guide de démarrage rapide en ajoutant le code qui charge les DLL natives et qui instancie ensuite les objets de profil et de moteur.


   ```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.File;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for File API operations.
               MIP.Initialize(MipComponent.File);

               // Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId.
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               // Instantiate the AuthDelegateImpl object, passing in AppInfo.
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               MipContext mipContext = MIP.CreateMipContext(appInfo,
                                        "mip_data",
                                        LogLevel.Trace,
                                        null,
                                        null);

               // Initialize and instantiate the File Profile.
               // Create the FileProfileSettings object.
               // Initialize file profile settings to create/use local state.
               var profileSettings = new FileProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               // Create a FileEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               fileEngine = null;
               fileProfile = null;
               mipContext = null;
          }
     }
}
```

3. Remplacez les valeurs d’espace réservé que vous aviez collées dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur | Exemple |
   |:----------- |:----- |:--------|
   | \<application-id\> | L’ID d’application Azure AD affecté à l’application inscrite dans « Installation et configuration du kit SDK MIP » (2 instances).  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | Un nom convivial défini par l’utilisateur pour votre application. | AppInitialization |
   | \<Tenant-GUID\> | ID de votre locataire Azure AD | ID de locataire |


4. À présent, effectuez une build finale de l’application et corrigez les erreurs éventuelles. Votre code doit s’exécuter correctement.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre code d’initialisation est terminé, vous êtes prêt pour le guide de démarrage rapide suivant, où vous découvrirez les API de fichier MIP.

> [!div class="nextstepaction"]
> [Lister les étiquettes de confidentialité](quick-file-list-labels-csharp.md)
