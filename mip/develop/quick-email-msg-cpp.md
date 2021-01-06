---
title: API de fichier - Traiter les fichiers e-mail .msg (C++)
description: Cet article vous aide à comprendre comment utiliser l’API de fichier SDK MIP pour traiter les fichiers .msg (C++).
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/08/2020
ms.author: mbaldwin
ms.openlocfilehash: 111b928538dd6222da55cb2ee5664549e272f785
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865312"
---
# <a name="file-api---process-email-msg-files-c"></a>API de fichier - Traiter les fichiers e-mail .msg (C++)

L’API de fichier prend en charge les opérations de protection appliquées aux fichiers .msg de la même manière que pour tous les autres types de fichiers. Toutefois, le SDK exige que l’application active l’indicateur de fonctionnalité MSG. Ici, nous verrons comment définir cet indicateur.

Comme nous l’avons vu précédemment, l’instanciation de `mip::FileEngine` nécessite un objet de paramètre : `mip::FileEngineSettings`. FileEngineSettings peut être utilisé pour passer les paramètres personnalisés que l’application doit définir pour une instance en particulier. La propriété `CustomSettings` de `mip::FileEngineSettings` permet de définir l’indicateur pour `enable_msg_file_type` en vue d’activer le traitement des fichiers .msg.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation de l’API de fichier (C++)](quick-app-initialization-cpp.md) pour créer une solution Visual Studio de démarrage. Le guide de démarrage rapide « Traitement des fichiers .msg (C++) » s’appuie sur le précédent.
- Consultez [Démarrage rapide : Lister les étiquettes de confidentialité (C++)](quick-file-list-labels-cpp.md).
- Consultez [Démarrage rapide : Définir/Obtenir des étiquettes de confidentialité (C++)](quick-file-set-get-label-cpp.md).
- Passez en revue les concepts relatifs au [SDK MIP des fichiers e-mail](concept-email.md).
- Éventuellement : Passez en revue les concepts relatifs au [SDK MIP des moteurs de fichiers](concept-profile-engine-file-engine-cpp.md).
- Éventuellement : passez en revue les concepts liés aux [gestionnaires de fichiers dans le kit SDK MIP](concept-handler-file-cpp.md).

## <a name="prerequisite-implementation-steps"></a>Étapes d’implémentation prérequises

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application cliente (C++) ».

2. Créez un script PowerShell pour générer des jetons d’accès, comme expliqué dans le guide de démarrage rapide [Lister les étiquettes de confidentialité (C++)](quick-file-list-labels-cpp.md#create-a-powershell-script-to-generate-access-tokens).

3. Implémentez la classe Observer pour superviser `mip::FileHandler`, comme expliqué dans le guide de démarrage rapide [Définir/Obtenir des étiquettes de confidentialité (C++)](quick-file-set-get-label-cpp.md#implement-an-observer-class-to-monitor-the-file-handler-object).

## <a name="set-enable_msg_file_type-and-use-file-api-to-protect-msg-file"></a>Définir enable_msg_file_type et utiliser l’API de fichier pour protéger le fichier .msg

Ajoutez le code de construction du moteur de fichiers ci-dessous pour définir `enable_msg_file_type flag` et utiliser le moteur de fichiers pour protéger un fichier .msg.

1. À l’aide de l’*Explorateur de solutions*, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Ajoutez les directives #include et using suivantes, sous les directives existantes correspondantes, en haut du fichier :

    ```cpp
    #include "filehandler_observer.h" 
    #include "mip/file/file_handler.h" 
    #include <iostream>
    #include "mip/protection/protection_descriptor_builder.h"
    #include "mip/protection_descriptor.h"
    using mip::FileHandler;
    using mip::ProtectionDescriptor;
    using mip::ProtectionDescriptorBuilder;
    using mip::ProtectionSettings;
    using std::endl;
    ```

3. Supprimez l’implémentation de la fonction `main()` du guide de démarrage rapide précédent. Dans le corps de `main()`, insérez le code suivant. Dans le bloc de code ci-dessous, l’indicateur `enable_msg_file_type` est défini lors de la création du moteur de fichiers. Les fichiers .msg peuvent alors être traités par les objets `mip::FileHandler` créés à l’aide du moteur de fichiers.

```cpp
int main()
{
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo { "<application-id>",                    // ApplicationInfo object (App ID, name, version)
                              "<application-name>", 
                              "1.0" 
    };

    auto mipContext = mip::MipContext::Create(appInfo,
                                                "file_sample",
                                                mip::LogLevel::Trace,
                                                false,
                                                nullptr /*loggerDelegateOverride*/,
                                                nullptr /*telemetryOverride*/);

    auto profileObserver = make_shared<ProfileObserver>();                      // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>");  // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>();              // Consent delegate object

    // Construct/initialize profile object
    FileProfile::Settings profileSettings(mipContext,mip::CacheStorageType::OnDisk,authDelegateImpl,
        consentDelegateImpl,profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
        std::cout << "An exception occurred. Are the Settings and ApplicationInfo objects populated correctly?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    auto profile = profileFuture.get();

    // Construct/initialize engine object
    FileEngine::Settings engineSettings(
                            mip::Identity("<engine-account>"),      // Engine identity (account used for authentication)
                            "<engine-state>",                       // User-defined engine state
                            "en-US");                               // Locale (default = en-US)

    //Set enamble_msg_file_type flag as true
    std::vector<std::pair<string, string>> customSettings;
    customSettings.emplace_back(mip::GetCustomSettingEnableMsgFileType(), "true");
    engineSettings.SetCustomSettings(customSettings);

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<FileEngine> engine;

    try
    {
        engine = engineFuture.get();
    }
    catch (const std::exception& e)
    {
        cout << "An exception occurred... is the access token incorrect/expired?\n\n"<< e.what() << "'\n";
        system("pause");
        return 1;
    }

    //Set file paths
    string inputFilePath = "<input-file-path>"; //.msg file to be protected
    string actualFilePath = inputFilePath;
    string outputFilePath = "<output-file-path>"; //protected .msg file
    string actualOutputFilePath = outputFilePath;

    //Create a file handler for original file
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();

    engine->CreateFileHandlerAsync(inputFilePath,
                                    actualFilePath,
                                    true,
                                    std::make_shared<FileHandlerObserver>(),
                                    handlerPromise);

    auto fileHandler = handlerFuture.get();

    //List templates available to the user and use one of them to protect the mail file.

    ///Listing of protection templates must be performed by creating protection engine as described in protection quick start

    string templateId = "<template-id>"; //protection template retrieved using protection engine

    //Create a protection descriptor using templateID and use it to set protection to the file
    auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
    const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();
    fileHandler->SetProtection(descriptor, ProtectionSettings());

    // Commit changes, save as outputFilePath
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    fileHandler->CommitAsync(outputFilePath, commitPromise);
    if (commitFuture.get()) {
        cout << "\n Protection applied to file: " << outputFilePath << endl;
    }
    else {
        cout << "Failed to protect: " + outputFilePath << endl;
        return 1;
    }

    // Create a new handler to read the protected file metadata
    auto protectedHandlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto protectedHandlerFuture = protectedHandlerPromise->get_future();
    engine->CreateFileHandlerAsync(outputFilePath, 
                                   actualOutputFilePath, 
                                   true, 
                                   std::make_shared<FileHandlerObserver>(), 
                                   protectedHandlerPromise);

    auto protectedFileHandler = protectedHandlerFuture.get();

    cout << "Original file: " << inputFilePath << endl;
    cout << "Protected file: " << outputFilePath << endl;
    cout << "TemplateID applied to protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetTemplateId() 
            << endl;
    cout << "Protection Owner of protected file : " 
            << protectedFileHandler->GetProtection()->GetProtectionDescriptor()->GetOwner() 
            << endl;

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    protectedFileHandler = nullptr;
    fileHandler = nullptr;
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
}
```

Pour plus d’informations sur les opérations de fichiers, consultez les [concepts relatifs au gestionnaire de fichiers](concept-handler-file-cpp.md).

4. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<application-id\> | L’ID d’application inscrit auprès du locataire Azure AD, par exemple : `0edbblll-8773-44de-b87c-b8c6276d41eb`. |
   | \<engine-account\> | Le compte utilisé pour l’identité du moteur, par exemple : `user@tenant.onmicrosoft.com`. |
   | \<engine-state\> | État de l’application défini par l’utilisateur, par exemple : `My engine state`. |
   | \<input-file-path\> | Le chemin complet d’un fichier de message d’entrée de test, par exemple : `c:\\Test\\message.msg`. |
   | \<output-file-path\> | Le chemin complet vers le fichier de sortie, qui sera une copie étiquetée du fichier d’entrée, par exemple : `c:\\Test\\message_protected.msg`. |
   | \<template-id\> | Le templateId récupéré à l’aide du moteur de protection, par exemple : `667466bf-a01b-4b0a-8bbf-a79a3d96f720`. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Utilisez la touche **F6** (Générer la solution) pour générer votre application cliente. Si vous n’obtenez pas d’erreur de génération, utilisez **F5** (Démarrer le débogage) pour exécuter votre application.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C#

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| TemplateNotFoundException | Unrecognized template ID., CorrelationId=abb2ef59-ad09-4aa0-b731-f59a92711dad, CorrelationId.Description=FileHandler, HttpRequest.Id=8c688752-ccd2-4dca-ace3-b67b44176689;78538a57-a9fd-4717-8924-33581a04598b| Si votre projet a été généré sans problème, mais que vous voyez une sortie similaire sur la gauche, il est probable que votre templateID ne soit pas valide. Revenez au bloc de code pour corriger l’ID du modèle de protection, puis regénérez et retestez le projet. |