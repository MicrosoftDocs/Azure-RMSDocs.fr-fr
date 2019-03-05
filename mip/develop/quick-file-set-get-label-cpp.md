---
title: Démarrage rapide - Définir et obtenir une étiquette de sensibilité sur un fichier à l’aide du kit SDK MIP C++
description: Guide de démarrage rapide illustrant comment utiliser le kit SDK C++ Microsoft Information Protection pour définir et obtenir une étiquette de sensibilité sur un fichier.
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 50fe4bce04b28440609c558297d8a3e39087e557
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332835"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Démarrage rapide : Définir et obtenir une étiquette de sensibilité (C++)

Ce guide de démarrage rapide vous montre comment utiliser plus d’API de fichier MIP. En utilisant l’une des étiquettes de sensibilité que vous avez listées dans le précédent guide de démarrage rapide, vous utilisez un gestionnaire de fichiers pour définir/obtenir l’étiquette sur un fichier. La classe de gestionnaire de fichiers expose différentes opérations pour définir/obtenir des étiquettes, ou une protection, pour les types de fichiers pris en charge.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Complète [Guide de démarrage rapide : Répertorier les étiquettes de sensibilité (C++)](quick-file-list-labels-cpp.md) first, qui génère un solution Visual Studio, starter pour répertorier les étiquettes de sensibilité d’une organisation. Ce guide de démarrage rapide « Définir et obtenir une étiquette de sensibilité » s’appuie sur le guide précédent.
- Si vous le souhaitez : Révision [gestionnaires de fichiers dans le SDK MIP](concept-handler-file-cpp.md) concepts.

## <a name="implement-an-observer-class-to-monitor-the-file-handler-object"></a>Implémenter une classe d’observateur pour superviser l’objet de gestionnaire de fichiers

Comme avec l’observateur que vous avez implémenté (pour le profil et le moteur de fichier) dans Démarrage rapide – Initialisation de l’application, vous implémentez maintenant une classe d’observateur pour un objet de gestionnaire de fichier.

Créer une implémentation de base pour un observateur de gestionnaire de fichier, en étendant le Kit de développement logiciel `mip::FileHandler::Observer` classe. L’observateur est instancié et utilisé plus tard pour suivre les opérations du Gestionnaire de fichiers.

1. Ouvrez la solution Visual Studio que vous avez travaillé dans le précédent « Guide de démarrage rapide : Répertorier les étiquettes de sensibilité (C++) « article.

2. Ajoutez une nouvelle classe dans votre projet, ce qui génère les fichiers header/.h et implementation/.cpp pour vous :

   - Dans le **l’Explorateur de solutions**, cliquez à nouveau sur le nœud du projet, sélectionnez **ajouter**, puis sélectionnez **classe**.
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
   string filePathIn = "<input-file-path>";
   string contentIdentifier = "<content-identifier>";
   std::shared_ptr<FileHandler> handler;
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathIn, 
             contentIdentifier,
             mip::ContentState::REST, 
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
        mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
        handler->SetLabel(labelId, labelingOptions);
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
   contentIdentifier = "<content-identifier>";
   try
   {
        auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
        auto handlerFuture = handlerPromise->get_future();
        engine->CreateFileHandlerAsync(
             filePathOut, 
             contentIdentifier,
             mip::ContentState::REST,
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

4. Remplacez les valeurs d’espace réservé dans le code source que vous venez de coller dans comme suit, à l’aide de constantes de chaîne :

   | Espace réservé | Value |
   |:----------- |:----- |
   | \<input-file-path\> | Le chemin complet vers un fichier d’entrée de test, par exemple : `"c:\\Test\\Test.docx"`. |
   | \<content-identifier\> | Un identificateur contrôlable de visu pour le contenu. Exemple : <ul><li>pour un fichier, tenez compte des Chemin\Nomfichier : `"c:\Test\Test.docx"`</li><li>un courrier électronique, pour prendre en compte : l’expéditeur de l’objet : `"RE: Audit design:user1@contoso.com"`</li></ul> |
   | \<label-id\> | Un ID d’étiquette de sensibilité, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `"f42a3342-8706-4288-bd31-ebb85995028z"`. |
   | \<output-file-path\> | Le chemin complet vers le fichier de sortie, qui sera une copie étiquetée du fichier d’entrée, par exemple : `"c:\\Test\\Test_labeled.docx"`. |

## <a name="build-and-test-the-application"></a>Générer et tester l'application

Générez et testez votre application cliente. 

1. Utilisez la touche F6 (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute avec succès, l’application demande un jeton d’accès, chaque fois que le Kit de développement logiciel appelle votre `AcquireOAuth2Token()` (méthode). Comme vous l’avez fait précédemment dans la « Liste des étiquettes de sensibilité » démarrage rapide, exécutez votre script PowerShell pour acquérir le jeton chaque fois, en utilisant les valeurs fournies pour $authority et $resourceUrl. 

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
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

   Applying Label ID 074e457c-5848-4542-9a6f-34a182080e7z to c:\Test\Test.docx
   Committing changes

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Label committed to file: c:\Test\Test_labeled.docx
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Getting the label committed to file: c:\Test\Test_labeled.docx
   Name: Confidential
   Id: 074e457c-5848-4542-9a6f-34a182080e7z
   Press any key to continue . . .
   ```

Vous pouvez vérifier l’application de l’étiquette, en ouvrant le fichier de sortie et en inspectant visuellement les paramètres de protection des informations du document.

> [!NOTE]
> Si vous étiquetez un document Office, mais que ne vous êtes pas connecté à l’aide d’un compte issu du locataire Azure Active Directory (AD) où le jeton d’accès a été obtenu (et les étiquettes de sensibilité sont configurées), vous pouvez être invité à vous connecter avant de pouvoir ouvrir le document étiqueté. 



