---
title: Supprimer une étiquette qui nécessite une justification ou la faire passer à une version antérieure (C++)
description: Cet article explique comment supprimer une étiquette qui nécessite une justification ou la faire passer à une version antérieure.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/14/2020
ms.author: v-anikep
ms.openlocfilehash: 96bd94398c2a5c0bbe2cd87c12ec8e6a0af7e18b
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135672"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API de fichier du SDK Microsoft Information Protection - Justification d’action pour abaisser le niveau d’une étiquette de confidentialité dans un fichier (C++)

Ce guide de démarrage rapide traite du passage à une version antérieure d’une étiquette lorsque la stratégie d’étiquette nécessite une justification. Ici, nous utiliserons la classe `mip::FileHandler` pour modifier les étiquettes d’un fichier. Pour plus d’informations, consultez la [référence d’API](./reference/mip-sdk-reference.md).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Définir/Obtenir les étiquettes de confidentialité (C++)](quick-file-set-get-label-cpp.md) pour créer une solution Visual Studio de démarrage, en vue de lister les étiquettes de confidentialité d’une organisation, et de définir et lire les étiquettes de confidentialité d’un fichier. Le guide de démarrage rapide « Supprimer une étiquette qui nécessite une justification ou la faire passer à une version antérieure (C++) » s’appuie sur le précédent.
- Éventuellement : Passez en revue les [concepts relatifs aux gestionnaires de fichiers](concept-handler-file-cpp.md) dans le SDK MIP.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Ajouter une logique en vue de définir une étiquette de niveau inférieur pour un fichier protégé

Ajoutez une logique pour définir une étiquette de confidentialité dans un fichier à l’aide de l’objet `mip::FileHandler`.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent [Démarrage rapide : Définir/Obtenir des étiquettes de confidentialité (C++)](quick-file-set-get-label-cpp.md).

2. À l’aide de l’Explorateur de solutions, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Ajoutez les directives #include et using suivantes, sous les directives existantes correspondantes, en haut du fichier :

    ```cpp

        #include "mip/file/file_error.h"

        using mip::JustificationRequiredError;
        using std::cin;

    ```

4. Remplacez la valeur `<label-id>` du guide de démarrage rapide précédent par une étiquette de confidentialité qui nécessite une justification pour abaisser son niveau. Dans ce guide de démarrage rapide, nous allons commencer par définir cette étiquette, puis nous allons tenter d’abaisser son niveau à l’aide des extraits de code fournis dans les étapes suivantes.

5. Vers la fin du corps de `main()`, sous `system("pause");` et au-dessus du bloc de fermeture (où vous vous êtes arrêté dans le guide de démarrage rapide précédent), insérez le code suivant :

```cpp

// Downgrade label
// Set paths and lower label ID
// Set a new label on input file.

string lowerlabelId = "<lower-label-id>";
cout << "\nApplying new Label ID " << lowerlabelId << " to " << filePathOut << endl;
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);

// Try to apply a label with lower sensitivity.
try
{
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const mip::JustificationRequiredError& e)
{
    // Request justification from user.
    cout<<"Please provide justification for downgrading a label: "<<endl;
    string justification;
    cin >> justification;

    // Set Justification provided flag
    bool isDowngradeJustified = true;
    mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
    labelingOptions.SetDowngradeJustification(isDowngradeJustified,justification);

    //Set new label.
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}

// Commit changes, save as a different output file
string lowerFilePathOut = "<lower-output-file-path>";
try
{
    cout << "Committing changes" << endl;
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    handler->CommitAsync(lowerFilePathOut, commitPromise);
    if (commitFuture.get()) {
        cout << "\nLabel committed to file: " << lowerFilePathOut << endl;
    }
    else {
        cout << "Failed to label: " + lowerFilePathOut << endl;
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
string lowerActualFilePath = "<lower-content-identifier>";
try
{
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();
    engine->CreateFileHandlerAsync(
        lowerFilePathOut,
        lowerActualFilePath,
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

// Get the lowered label from output file
try
{
    cout << "\nGetting the label committed to file: " << lowerFilePathOut << endl;
    auto lowerLabel = handler->GetLabel();
    cout << "Name: " + lowerLabel->GetLabel()->GetName() << endl;
    cout << "Id: " + lowerLabel->GetLabel()->GetId() << endl;
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}
system("pause");

```

6. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<lower-label-id\> | ID d’étiquette, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `bb7ed207-046a-4caf-9826-647cff56b990`. Vérifiez que son niveau de confidentialité est inférieur à celui de l’étiquette du fichier protégé précédemment. |
   | \<lower-output-file-path\> | Chemin du fichier de sortie dans lequel vous souhaitez enregistrer le fichier modifié. |
   | \<lower-content-identifier\> | Un identificateur explicite du contenu. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Comme vous l’avez fait précédemment dans le guide de démarrage rapide « Définir/Obtenir des étiquettes de confidentialité (C++) », exécutez votre script PowerShell pour obtenir le jeton à chaque fois, en utilisant les valeurs fournies pour $authority et $resourceUrl.

  ```console
    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://syncservice.o365syncservice.com/
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID f55c2dea-db0f-47cd-8520-a52e1590fb6z to c:\Test\Test.docx
    Committing changes

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/common
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Label committed to file: c:\Test\Test.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Highly Confidential
    Id: f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying new Label ID f42a3342-8706-4288-bd31-ebb85995028z to c:\Test\Test_labeled.docx
    Please provide justification for downgrading a label:
    Need for sharing with wider audience.
    Committing changes

    Label committed to file: c:\Test\Test_downgraded.docx
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_downgraded.docx
    Name: General
    Id: f42a3342-8706-4288-bd31-ebb85995028z
    Press any key to continue . . .
   ```

Notez que si l’étiquette qui est supprimée d’un fichier nécessite une justification selon la stratégie d’étiquette, vous devez suivre une approche similaire pour l’opération `DeleteLabel()`. La fonction La fonction `DeleteLabel()` lève une exception `mip::JustificationRequiredError`. Pour que l’étiquette soit supprimée correctement, l’indicateur `isDowngradeJustified` doit avoir la valeur true pour la gestion des exceptions.
