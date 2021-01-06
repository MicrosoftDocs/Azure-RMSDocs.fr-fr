---
title: Démarrage rapide - Définir et obtenir une étiquette de sensibilité sur un fichier à l’aide du kit SDK MIP C++
description: Guide de démarrage rapide illustrant comment utiliser le kit SDK C++ Microsoft Information Protection pour définir et obtenir une étiquette de sensibilité sur un fichier.
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 41c91ed1453b0819be727d333e15987ee9b3da3a
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865159"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Démarrage rapide : Définir et obtenir une étiquette de sensibilité (C++)

Ce guide de démarrage rapide vous montre comment utiliser plus d’API de fichier MIP. En utilisant l’une des étiquettes de sensibilité que vous avez listées dans le précédent guide de démarrage rapide, vous utilisez un gestionnaire de fichiers pour définir/obtenir l’étiquette sur un fichier. La classe de gestionnaire de fichiers expose différentes opérations pour définir/obtenir des étiquettes, ou une protection, pour les types de fichiers pris en charge.

## <a name="prerequisites"></a>Configuration requise

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Commencez par suivre le guide [Démarrage rapide : Répertorier les étiquettes de sensibilité (C++)](quick-file-list-labels-cpp.md), qui génère une solution Visual Studio de démarrage afin de lister les étiquettes de sensibilité d’une organisation. Ce guide de démarrage rapide « Définir et obtenir une étiquette de sensibilité » s’appuie sur le guide précédent.
- Si vous le souhaitez : passez en revue les concepts liés aux [gestionnaires de fichiers dans le kit SDK MIP](concept-handler-file-cpp.md).

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>Implémenter une classe d’observateur pour superviser l’objet de gestionnaire de fichiers

Comme avec l’observateur que vous avez implémenté (pour le profil et le moteur de fichier) dans Démarrage rapide – Initialisation de l’application, vous implémentez maintenant une classe d’observateur pour un objet de gestionnaire de fichier.

Créez une implémentation de base pour un observateur de gestionnaire de fichier, en étendant la classe `mip::FileHandler::Observer` du SDK. L’observateur est instancié et utilisé plus tard pour suivre les opérations du Gestionnaire de fichiers.

1. Ouvrez la solution Visual Studio sur laquelle vous avez travaillé dans l’article précédent « Démarrage rapide : Répertorier les étiquettes de sensibilité (C++) ».

2. Ajoutez une nouvelle classe dans votre projet, ce qui génère les fichiers header/.h et implementation/.cpp pour vous :

   - Dans l’**Explorateur de solutions**, recliquez avec le bouton droit sur le nœud du projet, sélectionnez **Ajouter**, puis sélectionnez **Classe**.
   - Dans la boîte de dialogue **Ajouter une classe** :
     - Dans le champ **Nom de la classe**, entrez « filehandler_observer ». Notez que les champs **Fichier .h** et **Fichier .cpp** sont remplis automatiquement en fonction du nom que vous entrez.
     - Une fois terminé, cliquez sur le bouton **OK**.

3. Après avoir généré les fichiers .cpp et .h pour la classe, ces deux fichiers sont ouverts dans les onglets du groupe d’éditeurs. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe d’observateur :

   - Mettez à jour « filehandler_observer.h » en sélectionnant/supprimant la classe `filehandler_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <memory>
     #include "mip/file/file_engine.h"
     #include "mip/file/file_handler.h"

     class FileHandlerObserver final : public mip::FileHandler::Observer {
     public:
        FileHandlerObserver() { }
        // Observer implementation
        void OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) override;
        void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
        void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) override;
        void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;       
     };
     ```

   - Mettez à jour « filehandler_observer.h » en sélectionnant/supprimant l’implémentation de classe `filehandler_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     void FileHandlerObserver::OnCreateFileHandlerSuccess(const std::shared_ptr<mip::FileHandler>& fileHandler, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_value(fileHandler);
     }

     void FileHandlerObserver::OnCreateFileHandlerFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<std::shared_ptr<mip::FileHandler>>>(context);
        promise->set_exception(error);
     }

     void FileHandlerObserver::OnCommitSuccess(bool committed, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_value(committed);
     }

     void FileHandlerObserver::OnCommitFailure(const std::exception_ptr & error, const std::shared_ptr<void>& context) {
        auto promise = std::static_pointer_cast<std::promise<bool>>(context);
        promise->set_exception(error);
     }
     ```

4. Si vous le souhaitez, utilisez la touche F6 (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Ajouter une logique pour définir et obtenir une étiquette de sensibilité

Ajoutez une logique pour définir et obtenir une étiquette de sensibilité sur un fichier à l’aide de l’objet de moteur de fichier. 

1. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet. 

2. Ajoutez les directives `#include` et `using` suivantes, sous les directives existantes correspondantes, en haut du fichier :

   ```cpp
   #include "filehandler_observer.h" 
   #include "mip/file/file_handler.h" 

   using mip::FileHandler;
   ```
3. Vers la fin du corps `main()`, au-dessous de `system("pause");` et au-dessus de `return 0;` (où vous vous êtes arrêté dans le guide de démarrage rapide précédent), insérez le code suivant :

   ```cpp
   // Set up async FileHandler for input file operations
   string inputFilePath = "<input-file-path>";
   string actualFilePath = "<content-identifier>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             inputFilePath,
             actualFilePath,                       
             true, 
             std::make_shared<FileHandlerObserver>(), 
             handlerPromise);
        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid input file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Set a label on input file
   try
   {
        string labelId = "<label-id>";
        cout << "\nApplying Label ID " << labelId << " to " << filePathIn << endl;
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
        handler->SetLabel(engine->GetLabelById(labelId), labelingOptions, new ProtectionSettings());
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1; 
   }

   // Commit changes, save as a different/output file
   string filePathOut = "<output-file-path>";
   try
   {
        cout << "Committing changes" << endl;
        auto commitPromise = std::make_shared<std::promise<bool>>();
        auto commitFuture = commitPromise->get_future();
        handler->CommitAsync(filePathOut, commitPromise);
        if (commitFuture.get()) {
            cout << "\nLabel committed to file: " << filePathOut << endl;
        }
        else {
            cout << "Failed to label: " + filePathOut << endl;
            return 1;
        }
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");

   // Set up async FileHandler for output file operations
   actualFilePath = "<content-identifier>";
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathOut,
             actualFilePath,
             true,
             std::make_shared<FileHandlerObserver>(),
             handlerPromise);

        handler = handlerFuture.get();
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }

   // Get the label from output file
   try
   {
        cout << "\nGetting the label committed to file: " << filePathOut << endl;
        auto label = handler->GetLabel();
        cout << "Name: " + label->GetLabel()->GetName() << endl;
        cout << "Id: " + label->GetLabel()->GetId() << endl;
   }
   catch (const std::exception& e)
   {
        cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
        system("pause");
        return 1;
   }
   system("pause");
   ```

4. Vers la fin de `main()`, identifiez le bloc d’arrêt d’application créé lors du premier démarrage rapide et supprimez les marques de commentaire de la ligne du gestionnaire :

   ```cpp
   // Application shutdown. Null out profile and engine, call ReleaseAllResources();
   // Application may crash at shutdown if resources aren't properly released.
   profile = nullptr;
   engine = nullptr;
   handler = nullptr;
   mipContext = nullptr;
   ```

5. Remplacez les valeurs d’espace réservé que vous venez de coller dans le code source par des constantes de chaîne :

   | Espace réservé | valeur |
   |:----------- |:----- |
   | \<input-file-path\> | Le chemin complet vers un fichier d’entrée de test, par exemple : `"c:\\Test\\Test.docx"`. |
   | \<content-identifier\> | Un identificateur explicite du contenu. Exemple : <ul><li>pour un fichier, utilisez l’identificateur chemin\nomfichier : `"c:\Test\Test.docx"`</li><li>pour un e-mail, utilisez l’identificateur objet:expéditeur : `"RE: Audit design:user1@contoso.com"`</li></ul> |
   | \<label-id\> | Un ID d’étiquette de sensibilité, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `"f42a3342-8706-4288-bd31-ebb85995028z"`. |
   | \<output-file-path\> | Le chemin complet vers le fichier de sortie, qui sera une copie étiquetée du fichier d’entrée, par exemple : `"c:\\Test\\Test_labeled.docx"`. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente. 

1. Utilisez la touche F6 (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Comme vous l’avez fait précédemment dans le guide de démarrage rapide « Lister les étiquettes de sensibilité », exécutez votre script PowerShell pour obtenir le jeton chaque fois, en utilisant les valeurs fournies pour $authority et $resourceUrl. 

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:

   Sensitivity labels for your organization:
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
   Press any key to continue . . .

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

Vous pouvez vérifier l’application de l’étiquette, en ouvrant le fichier de sortie et en inspectant visuellement les paramètres de protection des informations du document.

> [!NOTE]
> Si vous étiquetez un document Office, mais que ne vous êtes pas connecté à l’aide d’un compte issu du locataire Azure Active Directory (AD) où le jeton d’accès a été obtenu (et les étiquettes de sensibilité sont configurées), vous pouvez être invité à vous connecter avant de pouvoir ouvrir le document étiqueté. 



