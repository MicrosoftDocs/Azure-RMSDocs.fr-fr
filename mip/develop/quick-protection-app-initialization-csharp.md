---
title: 'Démarrage rapide : Initialisation d’une application cliente - API Protection (C#)'
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes C# du SDK Microsoft Information Protection (MIP) - API Protection (C#).
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: mbaldwin
ms.openlocfilehash: bfa1866618e65f1f9f215cb70fd76254623777d0
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865176"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>Démarrage rapide : Initialisation d’une application cliente pour les API Protection (C#)

Ce guide de démarrage rapide montre comment implémenter le modèle d’initialisation de client utilisé par le wrapper .NET du SDK MIP au moment de l’exécution.

> [!NOTE]
> Les étapes décrites dans ce guide de démarrage rapide sont requises pour toute application cliente qui utilise l’API Protection du wrapper .NET de MIP. Ces démarrages rapides doivent être effectués en série après l’initialisation de l’application et l’implémentation des classes de délégué d’authentification et de délégué de consentement.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas déjà fait, veillez à :

- Exécuter la procédure fournie dans [Installation et configuration du kit SDK Microsoft Information Protection (MIP)](setup-configure-mip.md). Ce démarrage rapide « Configuration du moteur et du profil de protection » s’appuie sur l’installation et la configuration appropriées du kit SDK.
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

3. Répétez les étapes ci-dessus pour ajouter le package de l’API Protection du SDK MIP, mais cette fois, ajoutez « Microsoft.IdentityModel.Clients.ActiveDirectory » à l’application.

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>Implémenter un délégué d’authentification et un délégué de consentement

Si ce n’est déjà fait, suivez les étapes indiquées dans [Initialisation d’application de l’API de fichier](quick-app-initialization-csharp.md) pour l’implémentation du délégué d’authentification et de consentement.

## <a name="initialize-the-mip-sdk-managed-wrapper"></a>Initialiser le wrapper managé du SDK MIP

1. À partir de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Supprimez l’implémentation générée de `main()`.

3. Le wrapper managé inclut une classe statique, `Microsoft.InformationProtection.MIP`, qui est utilisée pour l’initialisation, la création d’un `MipContext`, le chargement des profils et la libération des ressources. Pour initialiser le wrapper pour les opérations d’API de fichier, appelez `MIP.Initialize()`, en passant `MipComponent.Protection` qui charge les bibliothèques nécessaires aux opérations de protection.

4. Dans la section `Main()` du fichier *Program.cs*, ajoutez ce qui suit, en remplaçant **\<application-id\>** par l’ID de l’inscription d’application Azure AD que nous avons créée.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
    class Program
    {
        private const string clientId = "<application-id>";
        private const string appName = "<friendly-name>";

        static void Main(string[] args)
        {
            //Initialize Wrapper for Protection API operations
            MIP.Initialize(MipComponent.Protection);
        }
    }
}
```

## <a name="construct-a-protection-profile-and-engine"></a>Construire un moteur et un profil de protection

Comme nous l’avons mentionné précédemment, des objets de profil et de moteur sont nécessaires pour les clients du SDK utilisant des API MIP. Terminez la phase de codage de ce guide de démarrage rapide en ajoutant le code qui charge les DLL natives et qui instancie ensuite les objets de profil et de moteur.

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.InformationProtection;
using Microsoft.InformationProtection.Exceptions;
using Microsoft.InformationProtection.Protection;

namespace mip_sdk_dotnet_quickstart
{
     class Program
     {
          private const string clientId = "<application-id>";
          private const string appName = "<friendly-name>";

          static void Main(string[] args)
          {
               // Initialize Wrapper for Protection API operations.
               MIP.Initialize(MipComponent.Protection);

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

               // Initialize and instantiate the ProtectionProfile.
               // Create the ProtectionProfileSettings object.
               // Initialize protection profile settings to create/use local state.
               var profileSettings = new ProtectionProfileSettings(mipContext,
                                        CacheStorageType.OnDiskEncrypted,                                        
                                        new ConsentDelegateImplementation());

               // Load the Profile async and wait for the result.
               var protectionProfile = Task.Run(async () => await MIP.LoadProtectionProfileAsync(profileSettings)).Result;

               // Create a ProtectionEngineSettings object, then use that to add an engine to the profile.
               var engineSettings = new ProtectionEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
               engineSettings.Identity = new Identity("user1@tenant.com");
               var protectionEngine = Task.Run(async () => await protectionProfile.AddEngineAsync(engineSettings)).Result;

               // Application Shutdown
               // handler = null; // This will be used in later quick starts.
               protectionEngine = null;
               protectionProfile = null;
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


4. À présent, effectuez une build finale de l’application et corrigez les erreurs éventuelles. Votre code doit s’exécuter correctement.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre code d’initialisation est terminé, vous êtes prêt pour le guide de démarrage rapide suivant, où vous découvrirez les API Protection MIP.

> [!div class="nextstepaction"]
> [Répertorier les modèles de protection](quick-protection-list-templates-csharp.md)
