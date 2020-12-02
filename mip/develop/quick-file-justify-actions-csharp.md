---
title: Guide pratique pour rétrograder/supprimer une étiquette qui nécessite une justification (C#)
description: Cet article explique comment supprimer une étiquette qui nécessite une justification ou la faire passer à une version antérieure.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 666b0c7fdbc483f638f76def37ec3082c9eb7377
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316515"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>API de fichier du SDK Microsoft Information Protection - Justification d’action pour abaisser une étiquette de confidentialité dans un fichier (C#)

Ce guide de démarrage rapide traite de la gestion d’une opération de rétrogradation d’étiquette quand la stratégie d’étiquette nécessite une justification. Ici, nous allons utiliser l’interface `IFileHandler` pour changer les étiquettes d’un fichier. Pour plus d’informations, consultez la [référence d’API](/dotnet/api/?term=microsoft.informationprotection).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Définir/obtenir les étiquettes de confidentialité (C#)](quick-file-set-get-label-csharp.md) pour créer une solution Visual Studio de démarrage, en vue de lister les étiquettes de confidentialité d’une organisation, et de définir et lire les étiquettes de confidentialité d’un fichier. Le guide de démarrage rapide « Guide pratique pour rétrograder/supprimer une étiquette qui nécessite une justification (C#) » s’appuie sur le précédent.
- Éventuellement : Passez en revue les [concepts relatifs aux gestionnaires de fichiers](concept-handler-file-cpp.md) dans le SDK MIP.

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>Ajouter une logique en vue de définir une étiquette de niveau inférieur pour un fichier protégé

Ajoutez une logique pour définir une étiquette de confidentialité dans un fichier en utilisant l’objet Gestionnaire de fichiers.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Définir/obtenir des étiquettes de confidentialité (C#).

2. À l’aide de l’Explorateur de solutions, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Remplacez la valeur `<label-id>` du guide de démarrage rapide précédent par une étiquette de confidentialité qui nécessite une justification pour abaisser son niveau. Dans ce guide de démarrage rapide, nous allons commencer par définir cette étiquette, puis nous allons tenter d’abaisser son niveau à l’aide des extraits de code fournis dans les étapes suivantes.

4. Vers la fin du corps de `Main()`, sous `Console.ReadKey()` et au-dessus du bloc d’arrêt de l’application (où nous nous sommes arrêtés dans le guide de démarrage rapide précédent), insérez le code suivant.

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

5. Vers la fin de Main(), identifiez le bloc d’arrêt d’application créé dans le guide de démarrage rapide précédent et ajoutez les lignes du gestionnaire ci-dessous pour libérer les ressources.

    ````csharp
    downgradeHandler = null;
    commitHandler = null;
    ````

6. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<downgraded-labled-output\> | Chemin du fichier de sortie dans lequel vous souhaitez enregistrer le fichier modifié. |
   | \<new-label-id\> | ID de modèle, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `bb7ed207-046a-4caf-9826-647cff56b990`. Vérifiez que son niveau de confidentialité est inférieur à celui de l’étiquette du fichier protégé précédemment. |

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

Notez qu’une approche similaire s’applique aussi à l’opération `DeleteLabel()` si l’étiquette qui est supprimée d’un fichier nécessite une justification selon la stratégie d’étiquette. La fonction `DeleteLabel()` lance une exception `JustificationRequiredException` et l’indicateur `IsDowngradeJustified` doit avoir la valeur true dans la gestion des exceptions avant de supprimer une étiquette.