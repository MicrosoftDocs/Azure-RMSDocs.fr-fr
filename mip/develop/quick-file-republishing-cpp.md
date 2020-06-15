---
title: Procédure de republication du scénario C++
description: Cet article vous aidera à comprendre le scénario de réutilisation du gestionnaire de protection pour les scénarios de republication.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 602cc8c56d260e8399fa62367d585baae1976157
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548256"
---
# <a name="file-api-re-publishing-quickstart-c"></a>Démarrage rapide de la republication de l’API de fichier (C++)

## <a name="overview"></a>Vue d’ensemble

Pour obtenir une vue d’ensemble de ce scénario et l’endroit où il peut être utilisé, reportez-vous à [republication dans MIP SDK](concept-republishing-cpp.md).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Guide de [démarrage rapide : définir/obtenir des étiquettes de sensibilité (C++)](quick-file-set-get-label-cpp.md) tout d’abord, qui génère une solution de démarrage Visual Studio, pour répertorier les étiquettes de sensibilité d’une organisation, pour définir et lire des étiquettes de sensibilité à partir d’un fichier. Ce guide de démarrage rapide « comment faire pour rétrograder/supprimer une étiquette nécessitant une justification C++ » s’appuie sur le précédent.
- Éventuellement : consultez les [gestionnaires de fichiers](concept-handler-file-cpp.md) dans les concepts du kit de développement logiciel MIP.
- Éventuellement : passez en revue les [gestionnaires de protection](concept-handler-protection-cpp.md) dans les concepts du kit de développement logiciel MIP.

## <a name="add-logic-to-filehandler-observer-class"></a>Ajouter une logique à la classe FileHandler observer

Pour pouvoir utiliser le déchiffrement d’un fichier protégé à l’aide de `GetDecryptedTemporaryFileAsync()` la méthode exposée par `mip::FileHandler` , les rappels de la méthode Async pour la réussite et l’échec doivent être définis comme indiqué ci-dessous.

1. Ouvrez la solution Visual Studio que vous avez créée dans le précédent «démarrage rapide : définir/recevoir des étiquettes de sensibilité (C++).

2. À l’aide de Explorateur de solutions, ouvrez le `filehandler_observer.h` fichier de dans votre projet. Vers la fin de la définition de FileHandler, avant d' `};` Ajouter les lignes ci-dessous pour la déclaration de méthode.

    ```cpp
        void OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) override;
        void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
    ```

3. À l’aide de Explorateur de solutions, ouvrez le `filehandler_observer.cpp` fichier dans votre projet. Vers la fin du fichier, ajoutez les lignes ci-dessous pour les définitions de méthode.

    ```cpp

        void FileHandlerObserver::OnGetDecryptedTemporaryFileSuccess(const std::string& decryptedFilePath, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_value(decryptedFilePath);
        }

        void FileHandlerObserver::OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::string>>(context);
        promise->set_exception(error);
        }
    ```

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Ajouter une logique pour modifier et republier un fichier protégé

1. À l’aide de Explorateur de solutions, ouvrez le fichier. cpp de votre projet qui contient l’implémentation de la `main()` méthode. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Vers la fin du corps principal (), sous System (« pause »); et supérieur retournent 0 ; (là où vous vous êtes arrêté dans le démarrage rapide précédent), insérez le code suivant :

    ```cpp

        //Originally protected file's path.
        std::string protectedFilePath = "<protected-file-path>";

        // Create file handler for the file
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(protectedFilePath, protectedFilePath, true, std::make_shared<FileHandlerObserver>(), handlerPromise);
        auto protectedFileHandler = handlerFuture.get();

        // retieve and store protection handler from file
        auto protectionHandler = protectedFileHandler->GetProtection();

        //Check if the user has the 'Edit' right to the file and if so decrypt the file.
        if (protectionHandler->AccessCheck("Edit")) {

            // Decrypt file to temp path using the same file handler
            auto tempPromise = std::make_shared<std::promise<string>>();
            auto tempFuture = tempPromise->get_future();
            protectedFileHandler->GetDecryptedTemporaryFileAsync(tempPromise);
            auto tempPath = tempFuture.get();

            /// Write code here to perform further operations for edit ///

            /// Follow steps below for re-protecting the edited file ///

            // Create a new file handler using the temporary file path.
            auto reprotectPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
            auto reprotectFuture = reprotectPromise->get_future();
            engine->CreateFileHandlerAsync(tempPath, tempPath, true, std::make_shared<FileHandlerObserver>(), reprotectPromise);
            auto republishHandler = reprotectFuture.get();

            // Set protection using the ProtectionHandler from the original consumption operation.
            republishHandler->SetProtection(protectionHandler);
            std::string reprotectedFilePath = "<protected-file-path>";

            // Commit changes
            auto republishPromise = std::make_shared<std::promise<bool>>();
            auto republishFuture = republishPromise->get_future();
            republishHandler->CommitAsync(reprotectedFilePath, republishPromise);

            // Validate republishing
            cout << "Protected File: " + protectedFilePath<<endl;
            cout << "Protected Label ID: " + protectedFileHandler->GetLabel()->GetLabel()->GetId() << endl;
            cout << "Protection Owner: " + protectedFileHandler->GetProtection()->GetOwner() << endl<<endl;

            cout << "Republished File: " + reprotectedFilePath<<endl;
            cout << "Republished Label ID: " + republishHandler->GetLabel()->GetLabel()->GetId() << endl;
            cout << "Republished Owner: " + republishHandler->GetProtection()->GetOwner() << endl;

        }
    ```

3. Vers la fin de main () Rechercher le bloc d’arrêt de l’application créé dans le démarrage rapide précédent et ajouter les lignes du gestionnaire ci-dessous pour libérer les ressources.

    ````csharp
        protectedFileHandler = nullptr;
        protectionHandler = nullptr;

    ````

4. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<protected-file-path\> | Fichier protégé du démarrage rapide précédent. |
   | \<reprotected-file-path\> | Chemin d’accès du fichier de sortie pour le fichier modifié à republier. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Comme vous l’avez fait précédemment dans le démarrage rapide « définir/obtenir une étiquette de sensibilité », exécutez votre script PowerShell pour obtenir le jeton à chaque fois, à l’aide des valeurs fournies pour $authority et $resourceUrl.

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Sensitivity labels for your organization:
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to C:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: C:\Test\Test_labeled.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: C:\Test\Test_labeled.docx
    Name: Confidential
    Id: 074e457c-5848-4542-9a6f-34a182080e7z
    Press any key to continue . . .
    Protected File: C:\Test\Test_labeled.docx
    Protected Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Protection Owner: user1@tenant.onmicrosoft.com

    Republished File: c:\Test\Test_republished.docx
    Republished Label ID: 074e457c-5848-4542-9a6f-34a182080e7z
    Republished Owner: user1@tenant.onmicrosoft.com

    Press any key to close this window . . .

   ```
   