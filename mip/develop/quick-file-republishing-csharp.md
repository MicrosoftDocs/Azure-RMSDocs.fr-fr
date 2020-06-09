---
title: 'Procédure de republication du scénario C #'
description: Cet article vous aidera à comprendre le scénario de réutilisation du gestionnaire de protection pour les scénarios de republication.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: d82424c03fe8c2e050bbd4095706fa675de5ed6e
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548205"
---
# <a name="microsoft-information-protection-sdk---file-api-re-publishing-quickstart-c"></a>Kit de développement logiciel (SDK) Microsoft Information Protection-démarrage rapide de la publication d’API de fichier (C#)

## <a name="overview"></a>Vue d’ensemble

Pour obtenir une vue d’ensemble de ce scénario et l’endroit où il peut être utilisé, reportez-vous à [republication dans MIP SDK](concept-republishing-cpp.md).

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Guide de [démarrage rapide : définir/obtenir des étiquettes de sensibilité (C#)](quick-file-set-get-label-csharp.md) en premier, qui génère une solution de démarrage Visual Studio, pour répertorier les étiquettes de sensibilité d’une organisation, pour définir et lire des étiquettes de sensibilité à partir d’un fichier. Ce guide de démarrage rapide « procédure de republication d’un fichier protégé-C# » s’appuie sur le précédent.
- Éventuellement : consultez les [gestionnaires de fichiers](concept-handler-file-cpp.md) dans les concepts du kit de développement logiciel MIP.
- Éventuellement : passez en revue les [gestionnaires de protection](concept-handler-protection-cpp.md) dans les concepts du kit de développement logiciel MIP.

## <a name="add-logic-to-edit-and-republish-a-protected-file"></a>Ajouter une logique pour modifier et republier un fichier protégé

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « démarrage rapide : définir/recevoir des étiquettes de sensibilité (C#) ».

2. À l’aide de Explorateur de solutions, ouvrez le fichier. cs dans votre projet qui contient l’implémentation de la `Main()` méthode. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. À la fin du `Main()` corps, au-dessous `Console.ReadKey()` et au-dessus du bloc d’arrêt de l’application (là où vous vous étiez arrêté dans le démarrage rapide précédent), insérez le code suivant.

    ```csharp

        string protectedFilePath = "<protected-file-path>" // Originally protected file's path from previous quickstart.

            //Create a fileHandler for consumption for the Protected File.
            var protectedFileHandler = Task.Run(async () => await fileEngine.CreateFileHandlerAsync(protectedFilePath,// inputFilePath
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

                /// Write code here to perform further operations for edit ///

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
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", protectedLabel.Label.Id, protectedFileHandler.Protection.Owner, protectedLabel.IsProtectionAppliedFromLabel.ToString()));
                var reprotectedLabel = republishHandler.Label;
                Console.WriteLine(string.Format("Reprotected file: {0}", reprotectedFilePath));
                Console.WriteLine(string.Format("File LabelID: {0} \r\nProtectionOwner: {1} \r\nIsProtected: {2}", reprotectedLabel.Label.Id, republishHandler.Protection.Owner, reprotectedLabel.IsProtectionAppliedFromLabel.ToString()));
                Console.WriteLine("Press a key to continue.");
                Console.ReadKey();

            }

    ```

4. Vers la fin de main () Rechercher le bloc d’arrêt de l’application créé dans le démarrage rapide précédent et ajouter les lignes du gestionnaire ci-dessous pour libérer les ressources.

    ````csharp
        protectedFileHandler = null;
        protectionHandler = null;

    ````

5. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<protected-file-path\> | Fichier protégé du démarrage rapide précédent. |
   | \<reprotected-file-path\> | Chemin d’accès du fichier de sortie pour le fichier modifié à republier. |

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