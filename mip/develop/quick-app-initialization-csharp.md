---
title: Guide de démarrage rapide - initialisation pour Microsoft Information Protection (MIP) SDK C# clients
description: Un guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour une Protection de plus d’informations de Microsoft (MIP) SDK C# les applications clientes.
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: b7f2b25027502fbdd9dd7bd877b8893c1940628a
ms.sourcegitcommit: ca2df73f8bba6bf0f58eea5bee15e356705276d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56589983"
---
# <a name="quickstart-client-application-initialization-c"></a>Démarrage rapide : Initialisation de l’application cliente (C#)

Ce démarrage rapide est vous montrent comment implémenter le modèle de l’initialisation du client, utilisé par le wrapper .NET du SDK MIP lors de l’exécution.

> [!NOTE]
> Les étapes décrites dans ce démarrage rapide sont requis pour toute application cliente qui utilise le wrapper MIP .NET fichier ou stratégie d’API. L’API de Protection n’est pas encore disponible. Bien que ce guide de démarrage rapide illustre l’utilisation des API de fichier, ce même modèle s’applique aux clients utilisant les API de stratégie et de protection. Les guides de démarrage rapide futurs doivent être consultés dans l’ordre, car chacun s’appuie sur le précédent, celui-ci étant le premier.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas déjà fait, veillez à :

- Exécuter la procédure fournie dans [Installation et configuration du kit SDK Microsoft Information Protection (MIP)](setup-configure-mip.md). Ce guide de démarrage rapide « initialisation d’une application cliente » s’appuie sur une installation et une configuration correctes du kit SDK.
- Si vous le souhaitez :
  - Passez en revue [Objets de profil et moteur](concept-profile-engine-cpp.md). Les objets de profil et moteur sont des concepts universels, requis par les clients qui utilisent les API MIP de fichier/stratégie/protection. 
  - Passez en revue les [concepts d’authentification](concept-authentication-cpp.md) pour savoir comment l’authentification et le consentement sont implémentés par le kit SDK et l’application cliente.

## <a name="create-a-visual-studio-solution-and-project"></a>Créer une solution et un projet Visual Studio

Tout d’abord, nous créons et configurons la solution et le projet Visual Studio initiaux, sur lesquels les autres guides de démarrage rapide s’appuieront.

1. Ouvrez Visual Studio 2017, sélectionnez le menu **Fichier**, **Nouveau**, **Projet**. Dans la boîte de dialogue **Nouveau projet** :
   - Dans le volet gauche, sous **installé**, **Visual C#** , sélectionnez **Windows Desktop**.
   - Dans le volet central, sélectionnez **application Console (.NET Framework)**
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

3. Répétez les étapes ci-dessus pour ajouter le package de l’API de fichier du SDK MIP, mais ajouter « Microsoft.IdentityModel.Clients.ActiveDirectory » à l’application.

## <a name="implement-an-authentication-delegate"></a>Implémenter un délégué d’authentification

Le kit SDK MIP implémente l’authentification en utilisant l’extensibilité de classe, qui fournit un mécanisme pour partager le travail d’authentification avec l’application cliente. Le client doit acquérir un jeton d’accès OAuth2 approprié et le fournir au kit SDK MIP au moment de l’exécution.

Créez maintenant une implémentation pour un délégué d’authentification, en étendant le Kit de développement logiciel `Microsoft.InformationProtection.IAuthDelegate` interface et la substitution et l’implémentation de la `IAuthDelegate.AcquireToken()` fonction virtuelle. Le délégué de l’authentification est instancié et utilisé ultérieurement par le `FileProfile` et `FileEngine` objets.

1. Cliquez sur le nom de projet dans Visual Studio, sélectionnez **ajouter** puis **classe**.
2. Entrez « AuthDelegateImplementation » dans le **nom** champ. Cliquez sur **Ajouter**.
3. Ajouter à l’aide des instructions pour la bibliothèque d’authentification Active Directory (ADAL) et la bibliothèque MIP :

     ```csharp
     using Microsoft.InformationProtection;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     ```

4. Définissez `AuthDelegateImplementation` hériter `Microsoft.InformationProtection.IAuthDelegate` et implémenter une variable privée de `Microsoft.InformationProtection.ApplicationInfo` et un constructeur qui accepte le même type.

     ```csharp
     public class AuthDelegateImplementation : IAuthDelegate
     {
        private ApplicationInfo _appInfo;
        private string redirectUri = "mip-sdk-app://authorize";
        public AuthDelegateImplementation(ApplicationInfo appInfo)
        {
            _appInfo = appInfo;
        }
     }
     ```

Le `ApplicationInfo` objet contient deux propriétés. Le `_appInfo.ApplicationId` sera utilisé dans le `AuthDelegateImplementation` classe pour fournir l’ID de client à la bibliothèque d’authentification.

5. Ajouter le `public string AcquireToken()` (méthode). Cette méthode doit accepter `Microsoft.InformationProtection.Identity` et deux chaînes : autorité et ressources. Ces variables de chaîne seront passés à la bibliothèque d’authentification dans par l’API et ne doit pas être manipulés. Modification peut entraîner un échec d’authentification.

     ```csharp
     public string AcquireToken(Identity identity, string authority, string resource)
     {
          AuthenticationContext authContext = new AuthenticationContext(authority);
          var result = authContext.AcquireTokenAsync(resource, _appInfo.ApplicationId, new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, null), UserIdentifier.AnyUser).Result;
          return result.AccessToken;
     }
     ```

## <a name="implement-a-consent-delegate"></a>Implémenter un délégué de consentement

Créez maintenant une implémentation pour un délégué de consentement, en étendant le Kit de développement logiciel `Microsoft.InformationProtection.IConsentDelegate` interface et la substitution et l’implémentation de `GetUserConsent()`. Le délégué de consentement est instancié et utilisé plus tard par les objets de profil de fichier et de moteur de fichier. Le délégué de consentement est fourni avec l’adresse du service de l’utilisateur doit donner son consentement à l’utilisation dans le `url` paramètre. Le délégué doit fournissent généralement des flux qui permet à l’utilisateur à accepter ou refuser pour donner son consentement pour l’accès au service. Pour coder en dur ce démarrage rapide `Consent.Accept`.

1. À l’aide de la même fonctionnalité « Ajouter une classe » de Visual Studio que nous avons utilisée précédemment, ajoutez une autre classe dans votre projet. Cette fois, entrez « ConsentDelegateImplementation » dans le **nom de la classe** champ. 

2. Mettre à jour maintenant **ConsentDelegateImpl.cs** pour implémenter votre nouvelle classe de délégué de consentement. Ajouter à l’aide de l’instruction pour `Microsoft.InformationProtection` et définissez la classe d’héritage `IConsentDelegate`.

     ```csharp
     class ConsentDelegateImplementation : IConsentDelegate
     {
          public Consent GetUserConsent(string url)
          {
               return Consent.Accept;
          }
     }
     ```

3. Si vous le souhaitez, essayez de générer la solution pour vous assurer qu’il est compilé sans erreur.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Initialiser le Wrapper managé du SDK MIP

1. À partir de **l’Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la `Main()` (méthode). Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Supprimez l’implémentation générée de `main()`. 

3. Le wrapper managé inclut une classe statique, `Microsoft.InformationProtection.MIP` utilisé pour l’initialisation, le chargement des profils et la libération des ressources. Pour initialiser le wrapper pour les opérations d’API de fichier, appelez MIP. Initialize, en transmettant `MipComponent.File` pour charger les bibliothèques nécessaires pour les opérations de fichier. 

4. Dans `Main()` dans *Program.cs* ajoutez ce qui suit, en remplaçant **\<id d’application\>** avec l’ID de l’inscription d’Application AD Azure créé précédemment.

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
            //Initialize Wrapper for File API operations 
            MIP.Initialize(MipComponent.File);
        }
    }
}
```

## <a name="construct-a-file-profile-and-engine"></a>Construire un profil de fichier et un moteur

Comme mentionné, les objets de profil et le moteur sont requis pour les clients du Kit de développement logiciel à l’aide de MIP APIs. Terminez la partie de codage de ce démarrage rapide, en ajoutant du code pour charger les DLL natives puis instancier les objets de profil et le moteur.

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
               //Initialize Wrapper for File API operations
               MIP.Initialize(MipComponent.File);

               //Create ApplicationInfo, setting the clientID from Azure AD App Registration as the ApplicationId
               ApplicationInfo appInfo = new ApplicationInfo()
               {
                    ApplicationId = clientId,
                    ApplicationName = appName,
                    ApplicationVersion = "1.0.0"
               };

               //Instatiate the AuthDelegateImpl object, passing in AppInfo. 
               AuthDelegateImplementation authDelegate = new AuthDelegateImplementation(appInfo);

               //Initialize and instantiate the File Profile
               //Create the FileProfileSettings object
               var profileSettings = new FileProfileSettings("mip_data", false, authDelegate, new ConsentDelegateImplementation(), appInfo, LogLevel.Trace);

               //Load the Profile async and wait for the result
               var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

               //Create a FileEngineSettings object, then use that to add an engine to the profile
               var engineSettings = new FileEngineSettings("user1@tenant.com", "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;
          }
     }
}
``` 

3. Remplacez les valeurs d’espace réservé dans le code source que vous avez collée, en utilisant les valeurs suivantes :

   | Espace réservé | Value | Exemple |
   |:----------- |:----- |:--------|
   | \<application-id\> | L’ID d’application Azure AD affecté à l’application inscrite dans « Installation et configuration du kit SDK MIP » (2 instances).  | 0edbblll-8773-44de-b87c-b8c6276d41eb |
   | \<friendly-name\> | Un nom convivial défini par l’utilisateur pour votre application. | AppInitialization |


4. À présent, effectuez une build finale de l’application et corrigez les erreurs éventuelles. Votre code doit être généré avec succès.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre code d’initialisation est terminé, vous êtes prêt pour le guide de démarrage rapide suivant, où vous découvrirez les API de fichier MIP.

> [!div class="nextstepaction"]
> [Répertorier les étiquettes de sensibilité](quick-file-list-labels-csharp.md)
