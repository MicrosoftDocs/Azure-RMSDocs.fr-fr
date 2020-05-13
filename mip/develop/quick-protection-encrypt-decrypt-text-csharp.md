---
title: 'Démarrage rapide : chiffrer/déchiffrer du texte à l’aide de l’API Protection du SDK MIP C#'
description: Ce démarrage rapide vous montre comment utiliser le wrapper Microsoft Information Protection SDK .NET pour chiffrer et déchiffrer le texte ad hoc à l’aide d’un modèle de protection.
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: 85c3575aad9315155b2fbfaad991e586435edb37
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2020
ms.locfileid: "82972150"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>Démarrage rapide : Chiffrer/déchiffrer le texte à l’aide du SDK MIP (C#)

Ce guide de démarrage rapide vous montre comment utiliser plus d’API Protection MIP. À l’aide de l’un des modèles de protection que vous avez indiqués dans le démarrage rapide précédent, vous utilisez un gestionnaire de protection pour chiffrer le texte ad hoc. La classe du gestionnaire de protection expose différentes opérations pour l’application et la suppression de la protection.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Commencez par répertorier les modèles de protection (C#)](quick-protection-list-templates-csharp.md), ce qui génère une solution de démarrage Visual Studio, afin de répertorier les modèles de protection disponibles pour un utilisateur authentifié. Ce guide de démarrage rapide « Chiffrer/déchiffrer le texte » s’appuie sur le précédent.
- Éventuellement : Passez en revue les concepts [Gestionnaires de protection dans le kit SDK MIP](concept-handler-protection-cpp.md).

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>Ajouter une logique pour définir et obtenir une étiquette de sensibilité

Ajoutez une logique pour chiffrer le texte ad hoc à l’aide de l’objet de moteur de protection.

1. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Vers la fin du corps `Main()`, où vous vous êtes arrêté dans le guide de démarrage rapide précédent, insérez le code suivant :

   ```csharp
   //Set text to encrypt and template ID
   string inputText = "<Sample-text>";
   string templateId = "<template-id>";
   //Create a template based publishing descriptor
   ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(templateId);

   //Create publishing settings using protection descriptor
   PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor);

   //Generate Protection Handler for publishing
   var publishingHandler = Task.Run(async() => await protectionEngine.CreateProtectionHandlerForPublishingAsync(publishingSettings)).Result;

   //Encrypt text using Publishing handler
   long bufferSize = publishingHandler.GetProtectedContentLength(inputText.Length, true);
   byte[] inputTextBuffer = Encoding.ASCII.GetBytes(inputText);
   byte[] encryptedTextBuffer = new byte[bufferSize];
   publishingHandler.EncryptBuffer(0, inputTextBuffer, encryptedTextBuffer, true);
   Console.WriteLine("Original text: {0}", inputText);
   Console.WriteLine("Encrypted text: {0}", Encoding.UTF8.GetString(encryptedTextBuffer));

   //Create a Protection handler for consumption using the same publishing licence
   var serializedPublishingLicense = publishingHandler.GetSerializedPublishingLicense();
   PublishingLicenseInfo plInfo = PublishingLicenseInfo.GetPublishingLicenseInfo(serializedPublishingLicense);
   ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo);
   var consumptionHandler = protectionEngine.CreateProtectionHandlerForConsumption(consumptionSettings);

   //Use the handler to decrypt the encrypted text
   long buffersize = encryptedTextBuffer.Length;
   byte[] decryptedBuffer = new byte[bufferSize];
   var bytesDecrypted = consumptionHandler.DecryptBuffer(0, encryptedTextBuffer, decryptedBuffer, true);
   byte[] OutputBuffer = new byte[bytesDecrypted];
   for (int i = 0; i < bytesDecrypted; i++){
      OutputBuffer[i] = decryptedBuffer[i];
   }

   Console.WriteLine("Decrypted content: {0}", Encoding.UTF8.GetString(OutputBuffer));
   Console.WriteLine("Press a key to quit.");
   Console.ReadKey();

   ```

3. Vers la fin de `Main()`, identifiez le bloc d’arrêt d’application créé lors du premier démarrage rapide et ajoutez les lignes du gestionnaire :

   ```csharp
   // Application Shutdown
   publishingHandler = null;
   consumptionHandler = null;
   protectionEngine = null;
   protectionProfile = null;
   mipContext = null;
   ```

4. Remplacez les valeurs d’espace réservé dans le code source par les valeurs suivantes :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<sample-text\> | Exemple de texte que vous souhaitez chiffrer, par exemple : `My secure text`. |
   | \<template-id\> | ID de modèle, copié à partir de la sortie de la console dans le guide de démarrage rapide précédent, par exemple : `bb7ed207-046a-4caf-9826-647cff56b990`. |

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application *peut* demander une authentification via ADAL chaque fois que le SDK appelle la méthode `AcquireToken()`. Si les informations d’identification ont déjà été mises en cache, vous n’êtes pas invité à vous connecter et à voir la liste des étiquettes, suivie des informations sur l’étiquette appliquée et le fichier modifié.

  ```console
   Original content: My secure text
   Encrypted content: c?_hp???Q??+<?
   Decrypted content: My secure text
   Press a key to quit.
   ```
