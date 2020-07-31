---
title: API de fichier - Traiter les fichiers e-mail .msg (C#)
description: Cet article vous explique comment utiliser l’API de fichier SDK MIP pour traiter les fichiers .msg.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 9dca0317e80f1b09331132988aad69bb5f259697
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135689"
---
# <a name="file-api---process-email-msg-files-c"></a>API de fichier - Traiter les fichiers e-mail .msg (C#)

L’API de fichier prend en charge les opérations de protection appliquées aux fichiers .msg de la même manière que pour tous les autres types de fichiers. Toutefois, le SDK exige que l’application active l’indicateur de fonctionnalité MSG. Ici, nous verrons comment définir cet indicateur.

Comme nous l’avons vu précédemment, l’instanciation de `IFileEngine` nécessite un objet de paramètre : `FileEngineSettings`. FileEngineSettings peut être utilisé pour passer les paramètres personnalisés que l’application doit définir pour une instance en particulier. La propriété `CustomSettings` de `FileEngineSettings` permet de définir l’indicateur pour `enable_msg_file_type` en vue d’activer le traitement des fichiers .msg.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation de l’API de fichier (C#)](quick-app-initialization-csharp.md) pour créer une solution Visual Studio de démarrage. Le guide de démarrage rapide « Traitement des fichiers .msg (C#) » s’appuie sur le précédent.
- Passez en revue les concepts relatifs au [SDK MIP des fichiers e-mail](concept-email.md).
- Éventuellement : Passez en revue les concepts relatifs au [SDK MIP des moteurs de fichiers](concept-profile-engine-file-engine-cpp.md).
- Éventuellement : passez en revue les concepts liés aux [gestionnaires de fichiers dans le kit SDK MIP](concept-handler-file-cpp.md).

## <a name="set-enable_msg_file_type-and-use-file-api-for-protecting-msg-file"></a>Définir enable_msg_file_type et utiliser l’API de fichier pour protéger le fichier .msg

Pour poursuivre ce guide de démarrage rapide concernant l’initialisation de l’application API de fichier, modifiez le code de construction du moteur de fichiers pour définir `enable_msg_file_type flag`, puis utilisez le moteur de fichiers pour protéger un fichier .msg.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application API de fichier (C#) ».

2. À l’aide de l’Explorateur de solutions, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Supprimez l’implémentation de la fonction `Main()` du guide de démarrage rapide précédent. Dans le corps de `Main()`, insérez le code suivant. Dans le bloc de code ci-dessous, l’indicateur `enable_msg_file_type` est défini lors de la création du moteur de fichiers. Les fichiers .msg peuvent alors être traités par les objets `IFileHandler` créés à l’aide du moteur de fichiers.

    ```csharp
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

        MipContext mipContext = MIP.CreateMipContext(appInfo,"mip_data",LogLevel.Trace,null,null);

        // Initialize and instantiate the File Profile.
        // Create the FileProfileSettings object.
        // Initialize file profile settings to create/use local state.
        var profileSettings = new FileProfileSettings(mipContext, 
                                    CacheStorageType.OnDiskEncrypted, 
                                    new ConsentDelegateImplementation());

        // Load the Profile async and wait for the result.
        var fileProfile = Task.Run(async () => await MIP.LoadFileProfileAsync(profileSettings)).Result;

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var customSettings = new List<KeyValuePair<string, string>>();
        customSettings.Add(new KeyValuePair<string, string>("enable_msg_file_type", "true"));

        // Create a FileEngineSettings object, then use that to add an engine to the profile.
        var engineSettings = new FileEngineSettings("user1@tenant.com", authDelegate, "", "en-US");
        engineSettings.Identity = new Identity("user1@tenant.com");
        //set custom settings for the engine
        engineSettings.CustomSettings = customSettings;

        //Add fileEngine to profile
        var fileEngine = Task.Run(async () => await fileProfile.AddEngineAsync(engineSettings)).Result;

        //Set file paths
        string inputFilePath = "<input-file-path>"; //.msg file to be protected
        string actualFilePath = inputFilePath;
        string outputFilePath = "<output-file-path>"; //protected .msg file
        string actualOutputFilePath = outputFilePath;

        //Create a file handler for original file
        var fileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, 
                                                                    actualFilePath, 
                                                                    true)).Result;

        // List templates available to the user and use one of them to protect the mail file.

            /// Listing of protection templates has to be performed by creating protection engine as described in protection quick start

        string templateId = "<template-id>"; //protection template retrieved using protection engine

        // Construct a protection descriptor on input file and use the same to set protection to the file
        ProtectionDescriptor descriptor = new ProtectionDescriptor(templateId);
        fileHandler.SetProtection(descriptor, new ProtectionSettings());

        // Commit changes, save as outputFilePath
        var result = Task.Run(async () => await fileHandler.CommitAsync(outputFilePath)).Result;

        // Create a new handler to read the protected file metadata
        var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, 
                                                                        actualOutputFilePath, 
                                                                        true)).Result;

        Console.WriteLine(string.Format("Original file: {0}", inputFilePath));
        Console.WriteLine(string.Format("Protected file: {0}", outputFilePath));
        Console.WriteLine(string.Format("TemplateID applied to file: {0} \r\nProtectionOwner: {1}", 
            handlerModified.Protection.ProtectionDescriptor.TemplateId,handlerModified.Protection.Owner));
        Console.WriteLine("Press a key to continue.");
        Console.ReadKey();

        // Application Shutdown
        fileHandler = null;
        handlerModified = null;
        fileEngine = null;
        fileProfile = null;
        mipContext = null;
    }

    ```

    Pour plus d’informations sur les opérations de fichiers, consultez les [concepts relatifs au gestionnaire de fichiers](concept-handler-file-cpp.md).

4. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<input-file-path\> | Le chemin complet d’un fichier de message d’entrée de test, par exemple : `c:\\Test\\message.msg`. |
   | \<output-file-path\> | Le chemin complet vers le fichier de sortie, qui sera une copie étiquetée du fichier d’entrée, par exemple : `c:\\Test\\message_protected.msg`. |
   | \<template-id\> | Le templateId récupéré à l’aide du moteur de protection, par exemple : `667466bf-a01b-4b0a-8bbf-a79a3d96f720`. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Utilisez la touche **F6** (Générer la solution) pour générer votre application cliente. Si vous n’obtenez pas d’erreur de génération, utilisez **F5** (Démarrer le débogage) pour exécuter votre application.

```Console
    Original file: C:\Test.msg
    Protected file: C:\Test_protected.msg
    TemplateID applied to file: 667466bf-a01b-4b0a-8bbf-a79a3d96f720
    ProtectionOwner: user1@tenant.com
    Press a key to continue.
```

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C#

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| NetworkException: Le service RMS a détecté une entrée incorrecte dans la requête. Code d’erreur RMS : Microsoft.RightsManagement.Exceptions.BadInputException | * Parameters are invalid if both TemplateID and Policy are null., CorrelationId=f265b189-ebf6-4b30-a191-41539cdff215, CorrelationId.Description=FileHandler, HttpRequest.Id=04990d53-cf12-4969-9c80-06e365b312f2;d5fb4794-ac84-4445-abc6-647e41df62b2, HttpRequest.SanitizedUrl=https://api.aadrm.com/my/v2/publishinglicenses, HttpResponse.StatusCode=400, NetworkError.Category=FailureResponseCode* | Si votre projet a été généré sans problème, mais que vous voyez une sortie similaire sur la gauche, il est probable que votre templateID ne soit pas valide. Revenez au bloc de code pour corriger l’ID du modèle de protection, puis regénérez et retestez le projet. |
| TemplateNotFoundException | *Unrecognized template ID., CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b* | Si votre projet a été généré sans problème, mais que vous voyez une sortie similaire sur la gauche, il est probable que votre templateID ne soit pas valide. Revenez au bloc de code pour corriger l’ID du modèle de protection, puis regénérez et retestez le projet. |
