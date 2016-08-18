---
title: "Didacticiel de démarrage rapide Azure Information Protection Étape 3 | Azure Rights Management"
description: "Étape 3 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en seulement quatre étapes et moins de 15 minutes."
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 264f2be6c62dc7fa670171493941332fe7ff20e5
ms.openlocfilehash: 42649148e58a8ea1baab6317d181c24e6a21d709


---

# Étape 3 : Installer le client Azure Information Protection 

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Lors de cette étape, vous allez installer le client Azure Information Protection pour que la stratégie que vous venez de configurer soit téléchargée sur un PC Windows, et vous allez afficher les étiquettes dans les applications Office. 

1. Sur un PC où Office est installé (mais où Word n’est pas ouvert), [téléchargez le client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) à partir du Centre de téléchargement Microsoft. 

2. Exécutez **AZInfoProtection.exe** et suivez les invites pour installer le client.

    Pour ce didacticiel, peu importe si vous sélectionnez l’option d’installation d’une stratégie de démonstration, étant donné que la stratégie que nous venons de configurer sera téléchargée à partir d’Azure et remplacera la stratégie de démonstration installée. Toutefois, vous pouvez utiliser l’option de stratégie de démonstration si vous souhaitez simplement découvrir les étiquettes par défaut sans connexion à Azure Information Protection. 

3. Vérifiez que le client a été installé en ouvrant Word et un nouveau document vierge (ne l’enregistrez pas pour l’instant). Si vous êtes invité à entrer votre nom d’utilisateur et votre mot de passe, entrez les détails de votre compte d’administrateur général. Lors du chargement du document, deux nouveaux éléments doivent apparaître :

    - Sous l’onglet **Accueil**, un nouveau groupe **Protection** avec un bouton intitulé **Protéger**.

        Cliquez sur **Protéger** > **Aide et de commentaires** puis, dans la boîte de dialogue **Microsoft Azure Information Protection**, vérifiez l’état de votre client. Il doit afficher **Information Protection policy is installed** (La stratégie Information Protection est installée) et une heure de connexion récente. Vérifiez que le nom d’utilisateur affiché correspond à celui de votre locataire.

    - Une nouvelle barre s’affiche sous le ruban, la barre Information Protection. Elle affiche le titre **Sensitivity** (Niveau de confidentialité) et l’étiquette par défaut **Internal** (Interne) que nous avons configurée. 
    
        ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : client installé](../media/word2013-callouts2.png)

Vous êtes prêt pour l’étape finale, pour découvrir la classification, l’étiquetage et la protection en action.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’installation du client|[Installation du client Azure Information Protection](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; Étape 2](infoprotect-tutorial-step2.md)
[Étape 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Aug16_HO2-->


