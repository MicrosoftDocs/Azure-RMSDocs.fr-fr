---
title: "Didacticiel de démarrage rapide, étape 3 - AIP"
description: "Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 3 : installer le client."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
ms.openlocfilehash: 61c0d2c97ae1db15bf2ec5c4586aa54270502117
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
translationtype: HT
---
# <a name="step-3-install-the-client"></a>Étape 3 : Installer le client

>*S’applique à : Azure Information Protection*

Lors de cette étape, vous allez installer le client Azure Information Protection pour que la stratégie que vous venez de configurer soit téléchargée sur un PC Windows, et vous allez afficher les étiquettes dans les applications Office.


## <a name="install-the-azure-information-protection-client"></a>Installer le client Azure Information Protection

1. Sur un PC où Office est installé (mais où Word n’est pas ouvert), [téléchargez le client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) à partir du Centre de téléchargement Microsoft. 

2. Exécutez **AzInfoProtection.exe** et suivez les invites pour installer le client.

    Pour ce didacticiel, peu importe si vous sélectionnez l’option d’installation d’une stratégie de démonstration, étant donné que la stratégie que nous venons de configurer sera téléchargée à partir d’Azure et remplacera la stratégie de démonstration installée. Toutefois, vous pouvez utiliser l’option de stratégie de démonstration si vous souhaitez simplement découvrir les étiquettes par défaut sans connexion à Azure Information Protection. 

## <a name="verify-the-installations"></a>Vérifier les installations

Vérifiez que l’installation s’est déroulée correctement en ouvrant Word et un nouveau document vierge (ne l’enregistrez pas pour l’instant). Si vous êtes invité à entrer votre nom d’utilisateur et votre mot de passe, entrez les détails de votre compte d’administrateur général. 

Si c’est la première fois que vous installez le client, vous verrez une page **Félicitations** avec des instructions de base. Après l’avoir lue, cliquez sur **Fermer**.

Lors du chargement du document, deux nouveaux éléments doivent apparaître :

- Sous l’onglet **Accueil**, un nouveau groupe **Protection** avec un bouton intitulé **Protéger**.

    Cliquez sur **Protéger** > **Aide et commentaires** puis, dans la boîte de dialogue **Microsoft Azure Information Protection**, vérifiez l’état de votre client. La mention **Connecté en tant que** et votre nom d’utilisateur s’affichent. En outre, vous devriez également voir une heure et une date récente pour la dernière connexion et l’installation de la stratégie Information Protection. Vérifiez que le nom d’utilisateur affiché correspond à celui de votre locataire.

- Une nouvelle barre sous le ruban, la barre Information Protection. Elle affiche le titre **Sensitivity** (Niveau de confidentialité) et l’étiquette par défaut **Internal** (Interne) que nous avons configurée. 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : client installé](../media/word2013-callouts2.png)

Vous êtes maintenant prêt à voir Azure Information Protection en action.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’installation du client Azure Information Protection|[Télécharger et installer le client Azure Information Protection](../rms-client/install-client-app.md)|
|Instructions de l’administrateur pour le client Azure Information Protection|[Client Azure Information Protection - Guide de l’administrateur](../rms-client/client-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Étape 2](infoprotect-tutorial-step2.md)
[Étape 4 &#187;](infoprotect-tutorial-step4.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]