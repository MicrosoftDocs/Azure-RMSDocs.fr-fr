---
title: Guide pratique de republication de scénario C#
description: Cet article aide à comprendre le scénario de réutilisation du gestionnaire de protection dans les scénarios de republication.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: c72d284363c1ca988692d18b7007a88c88d808b5
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91421134"
---
# <a name="microsoft-information-protection-sdk---file-api-republishing-quickstart-c"></a>Kit SDK Microsoft Information Protection – Guide de démarrage rapide de la republication de l’API de fichier (C#)

## <a name="overview"></a>Vue d’ensemble

Pour une vue d’ensemble de ce scénario et de son contexte d’utilisation, consultez [Republication dans le kit SDK MIP](concept-republishing.md).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Définition/récupération des étiquettes de confidentialité (C#)](quick-file-set-get-label-csharp.md) pour créer une solution Visual Studio de démarrage, en vue de lister les étiquettes de confidentialité d’une organisation, et de définir et lire celles d’un fichier. Ce guide de démarrage rapide « Guide pratique de republication d’un fichier protégé – C# » s’appuie sur le précédent.
- Éventuellement : passez en revue les [Gestionnaires de fichiers](concept-handler-file-cpp.md) dans les concepts du kit SDK MIP.
- Éventuellement : passez en revue les [Gestionnaires de protection](concept-handler-protection-cpp.md) dans les concepts du kit SDK MIP.

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Ajout d’une logique pour modifier et republier un fichier protégé

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Définition/récupération des étiquettes de confidentialité (C#) ».

2. À l’aide de l’Explorateur de solutions, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Vers la fin du corps de `Main()`, sous `Console.ReadKey()` et au-dessus du bloc d’arrêt de l’application (où nous nous sommes arrêtés dans le guide de démarrage rapide précédent), insérez le code suivant :

```csharp
string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

//Create a fileHandler for consumption for the Protected File.
var protectedFileHandler = Task.Run(async () => 
                            await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
                                                                    protectedFilePath,// actualFilePath
                                                                    false, //isAuditDiscoveryEnabled
                                                                    null)).Result; // fileExecutionState

// Store protection handler from file
var protectionHandler = protectedFileHandler.Protection;

//Check if the user has the 'Edit' right to the file
if (protectionHandler.AccessCheck("Edit"))
{
    // Decrypt file to temp path
    var tempPath = Task.Run(async () => await protectedFileHandler.GetDecryptedTemporaryFileAsync()).Result;

    /*
        Your own application code to edit the decrypted file belongs here. 
    */

    /// Follow steps below for re-protecting the edited file. ///
    // Create a new file handler using the temporary file path.
    var republishHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(tempPath, tempPath, false)).Result;

    // Set protection using the ProtectionHandler from the original consumption operation.
    republishHandler.SetProtection(protectionHandler);

    // New file path to save the edited file
    string reprotectedFilePath = "<reprotected-file-path>" // New file path for saving reprotected file.

    // Write changes
    var reprotectedResult = Task.Run(async () => await republishHandler.CommitAsync(reprotectedFilePath)).Result;

    var protectedLabel = protectedFileHandler.Label;
    Console.WriteLine(string.Format("Originally protected file: {0}", protectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        protectedLabel.Label.Id, 
                        protectedFileHandler.Protection.Owner, 
                        protectedLabel.IsProtectionAppliedFromLabel.ToString()));
    var reprotectedLabel = republishHandler.Label;
    Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
    Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", 
                        reprotectedLabel.Label.Id, 
                        republishHandler.Protection.Owner, 
                        reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
    Console.WriteLine("Press a key to continue.");
    Console.ReadKey();
}
```

4. Vers la fin de Main(), identifiez le bloc d’arrêt d’application créé dans le guide de démarrage rapide précédent et ajoutez les lignes du gestionnaire ci-dessous pour libérer les ressources :

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;
    ````

5. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<protected-file-path\> | Fichier protégé issu du guide de démarrage rapide précédent. |
   | \<reprotected-file-path\> | Chemin du fichier de sortie pour la republication du fichier modifié. |

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

    Getting the label committed to file: C:\Test\Test_protected.docx
    File Label: Confidential
    IsProtected: True
    Press a key to continue.
    Originally protected file: C:\Test\Test_protected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Reprotected file: C:\Test\Test_reprotected.docx
    File LabelID: 569af77e-61ea-4deb-b7e6-79dc73653959
    ProtectionOwner: User1@Contoso.OnMicrosoft.com
    IsProtected: True
    Press a key to continue.
   ```