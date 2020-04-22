---
title: Démarrage rapide – Définir et obtenir une étiquette de sensibilité sur un fichier à l’aide du kit SDK MIP C#
description: Guide de démarrage rapide illustrant comment utiliser le wrapper .NET du SDK Microsoft Information Protection (MIP) pour définir et obtenir une étiquette de sensibilité sur un fichier.
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: c081d20ba3cfffdc1db06ade5d918230f3b9eff8
ms.sourcegitcommit: a3f901e479abbe056f8936a96b7253f0826d1415
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "75554988"
---
# <a name="quickstart-set-and-get-a-sensitivity-label-c"></a>Démarrage rapide : Définir et obtenir une étiquette de sensibilité (C#)

Ce guide de démarrage rapide vous montre comment utiliser plus d’API de fichier MIP. En utilisant l’une des étiquettes de sensibilité que vous avez listées dans le précédent guide de démarrage rapide, vous utilisez un gestionnaire de fichiers pour définir/obtenir l’étiquette sur un fichier. La classe de gestionnaire de fichiers expose différentes opérations pour définir/obtenir des étiquettes, ou une protection, pour les types de fichiers pris en charge.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Répertorier les étiquettes de sensibilité (C#)](quick-file-list-labels-csharp.md) pour créer une solution Visual Studio de démarrage qui liste les étiquettes de sensibilité d’une organisation. Ce guide de démarrage rapide « Définir et obtenir une étiquette de sensibilité » s’appuie sur le guide précédent.
- Éventuellement : passez en revue les concepts liés aux [gestionnaires de fichiers dans le kit SDK MIP](concept-handler-file-cpp.md).

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Ajouter une logique pour définir et obtenir une étiquette de sensibilité

Ajoutez une logique pour définir et obtenir une étiquette de sensibilité sur un fichier à l’aide de l’objet de moteur de fichier. 

1. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet. 

2. Vers la fin du corps `Main()`, au-dessous de `Console.ReadKey()` et au-dessus de `}` (où vous vous êtes arrêté dans le guide de démarrage rapide précédent), insérez le code suivant :

   ```csharp
     //Set paths and label ID
     string inputFilePath = "<input-file-path>";
     string actualFilePath = inputFilePath;
     string labelId = "<label-id>";
     string outputFilePath = "<output-file-path>";
     string actualOutputFilePath = outputFilePath;

     //Create a file handler for that file
     //Note: the 2nd inputFilePath is used to provide a human-readable content identifier for admin auditing. 
     var handler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(inputFilePath, actualFilePath, true)).Result;

     //Set Labeling Options
     LabelingOptions labelingOptions = new LabelingOptions()
     {
          AssignmentMethod = AssignmentMethod.Standard
     };

     // Set a label on input file
     handler.SetLabel(engine.GetLabelById(labelId), labelingOptions, new ProtectionSettings());

     // Commit changes, save as outputFilePath
     var result = Task.Run(async () => await handler.CommitAsync(outputFilePath)).Result;

     // Create a new handler to read the labeled file metadata
     var handlerModified = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(outputFilePath, actualOutputFilePath, true)).Result;

     // Get the label from output file
     var contentLabel = handlerModified.Label;
     Console.WriteLine(string.Format("Getting the label committed to file: {0}", outputFilePath));
     Console.WriteLine(string.Format("File Label: {0} \r\nIsProtected: {1}", contentLabel.Label.Name, contentLabel.IsProtectionAppliedFromLabel.ToString()));
     Console.WriteLine("Press a key to continue.");
     Console.ReadKey();
   ```

3. Vers la fin de `Main()`, identifiez le bloc d’arrêt d’application créé lors du premier démarrage rapide et supprimez les marques de commentaire de la ligne du gestionnaire :

   ```csharp
   // Application Shutdown
   handler = null;
   fileEngine = null;
   fileProfile = null;
   mipContext = null;
   ```

4. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<input-file-path\> | Le chemin complet vers un fichier d’entrée de test, par exemple : `c:\\Test\\Test.docx`. |
   | \<label-id\> | Un ID d’étiquette de sensibilité, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `f42a3342-8706-4288-bd31-ebb85995028z`. |
   | \<output-file-path\> | Le chemin complet vers le fichier de sortie, qui sera une copie étiquetée du fichier d’entrée, par exemple : `c:\\Test\\Test_labeled.docx`. |

## <a name="build-and-test-the-application"></a>Générer et tester l'application

Générez et testez votre application cliente. 

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application *peut* demander une authentification via ADAL chaque fois que le SDK appelle la méthode `AcquireToken()`. Si les informations d’identification ont déjà été mises en cache, vous n’êtes pas invité à vous connecter et à voir la liste des étiquettes, suivie des informations sur l’étiquette appliquée et le fichier modifié.

  ```console   
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.

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
