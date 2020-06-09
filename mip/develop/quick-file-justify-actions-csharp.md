---
title: Comment faire pour rétrograder/supprimer une étiquette qui a besoin d’une justification (C#)
description: Cet article vous aidera à comprendre le scénario de mise à niveau ou de suppression d’une étiquette nécessitant une justification.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: cdf128d5d01db0362fac1b76c1e0d81a15e55432
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548341"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API du fichier du kit de développement logiciel (SDK) Microsoft Information Protection : justification de l’action pour réduire une étiquette de sensibilité sur un fichier (C#)

Ce guide de démarrage rapide traite de la gestion d’une étiquette de rétrogradation lorsque la stratégie de l’étiquette requiert une justification. Ici, nous allons utiliser `IFileHandler` l’interface pour modifier les étiquettes d’un fichier. Pour plus d’informations, consultez [référence des API](/dotnet/api/?term=microsoft.informationprotection).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Guide de [démarrage rapide : définir/obtenir des étiquettes de sensibilité (C#)](quick-file-set-get-label-csharp.md) en premier, qui génère une solution de démarrage Visual Studio, pour répertorier les étiquettes de sensibilité d’une organisation, pour définir et lire des étiquettes de sensibilité à partir d’un fichier. Ce guide de démarrage rapide « comment faire pour rétrograder/supprimer une étiquette qui a besoin d’une justification C# » s’appuie sur le précédent.
- Si vous le souhaitez, examinez les [concepts des gestionnaires de fichiers](concept-handler-file-cpp.md) dans les concepts du kit de développement logiciel MIP.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Ajouter une logique pour définir une étiquette inférieure sur un fichier protégé

Ajoutez une logique pour définir une étiquette de sensibilité sur un fichier à l’aide de l’objet de gestionnaire de fichiers.

1. Ouvrez la solution Visual Studio que vous avez créée dans le précédent «démarrage rapide : définir/recevoir des étiquettes de sensibilité (C#).

2. À l’aide de Explorateur de solutions, ouvrez le fichier. cs dans votre projet qui contient l’implémentation de la `Main()` méthode. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Mettez à jour la `<label-id>` valeur du Guide de démarrage rapide précédent sur une étiquette de sensibilité qui nécessite une justification de la diminution. Au cours de ce démarrage rapide, nous allons commencer par définir cette étiquette, puis essayer de la réduire à l’aide d’extraits de code dans d’autres étapes.

4. À la fin du `Main()` corps, au-dessous `Console.ReadKey()` et au-dessus du bloc d’arrêt de l’application (là où vous vous étiez arrêté dans le démarrage rapide précédent), insérez le code suivant.

    ```csharp
    //Set paths and label ID
    string lowerInput = actualOutputFilePath;
    string lowerActualInput = lowerInput;
    string newLabelId = "<new-label-id>";
    string lowerOutput = "<downgraded-labled-output>";
    string lowerActualOutput = lowerOutput;

    //Create a file handler for that file
    var downgradeHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerInput, lowerActualInput, true)).Result;

    //Set Labeling Options
    LabelingOptions options = new LabelingOptions()
    {
        AssignmentMethod = AssignmentMethod.Standard
    };

    try
    {
        //Try to set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    catch (Microsoft.InformationProtection.Exceptions.JustificationRequiredException)
    {
        //Request justification from user
        Console.Write("Please provide justification for downgrading a label: ");
        string justification = Console.ReadLine();

        options.IsDowngradeJustified = true;
        options.JustificationMessage = justification;

        //Set new label
        downgradeHandler.SetLabel(fileEngine.GetLabelById(newLabelId), options, new ProtectionSettings());
    }

    // Commit changes, save as outputFilePath
    var downgradedResult = Task.Run(async () => await downgradeHandler.CommitAsync(lowerActualOutput)).Result;

    // Create a new handler to read the labeled file metadata
    var commitHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(lowerOutput, lowerActualOutput, true)).Result;

    // Get the label from output file
    var newContentLabel = commitHandler.Label;
    Console.WriteLine(string.Format("Getting the new label committed to file: {0}", lowerOutput));
    Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", newContentLabel.Label.Name, newContentLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();

    ```

5. Vers la fin de main (), recherchez le bloc d’arrêt de l’application créé dans le démarrage rapide précédent et ajoutez les lignes du gestionnaire ci-dessous pour libérer les ressources.

    ````csharp
    downgradeHandler = null;
    commitHandler = null;

    ````

6. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | Chemin du fichier de sortie dans lequel vous souhaitez enregistrer le fichier modifié. |
   | \<new-label-id\> | Un ID de modèle, copié à partir de la sortie de console dans le démarrage rapide précédent, par exemple : `bb7ed207-046a-4caf-9826-647cff56b990` . Assurez-vous qu’il a une sensibilité inférieure à celle de l’étiquette du fichier précédemment protégé. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application *peut* demander une authentification via ADAL chaque fois que le SDK appelle la méthode `AcquireToken()`. Si les informations d’identification ont déjà été mises en cache, vous n’êtes pas invité à vous connecter et à voir la liste des étiquettes, suivie des informations sur l’étiquette appliquée et le fichier modifié.

  ```console
    Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
    Public : 73254501-3d5b-4426-979a-657881dfcb1e
    General : da480625-e536-430a-9a9e-028d16a29c59
    Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
    Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
    Press a key to continue.

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Confidential
    IsProtected: True
    Press any key to continue . . .

    Please provide justification for downgrading a label: Lower label approved.
    Getting the new label committed to file: c:\Test\Test_downgraded.docx
    File Label: General
    IsProtected: False
    Press a key to continue.
   ```

Notez qu’une approche similaire s’applique également à `DeleteLabel()` l’opération, au cas où l’étiquette supprimée d’un fichier nécessite une justification selon la stratégie par étiquette.`DeleteLabel()` la fonction lève une `JustificationRequiredException` exception et `IsDowngradeJustified` l’indicateur doit avoir la valeur true dans la gestion des exceptions avant de pouvoir supprimer une étiquette.