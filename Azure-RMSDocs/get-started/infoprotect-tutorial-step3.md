---
title: "Étape 3 du didacticiel de démarrage rapide | Azure Information Protection"
description: "Étape 3 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en environ 30 minutes."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 496f086d4db43a69ef0acca579b290286a5b9e5b


---

# <a name="step-3-install-the-client-and-application"></a>Étape 3 : Installer le client et l’application 

>*S’applique à : Azure Information Protection*

Au cours de cette étape, vous allez commencer par installer le client Azure Information Protection pour que la stratégie que vous venez de configurer soit téléchargée sur un PC Windows, et vous allez afficher les étiquettes dans les applications Office.

Ensuite, vous allez installer l’application de partage Rights Management, afin de pouvoir partager en toute sécurité un document par e-mail, puis effectuer le suivi de son utilisation. 

Ces deux installations s’intègrent aux applications Office et, actuellement, vous devez les installer séparément.


## <a name="install-the-azure-information-protection-client"></a>Installer le client Azure Information Protection

1. Sur un PC où Office est installé (mais où Word n’est pas ouvert), [téléchargez le client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) à partir du Centre de téléchargement Microsoft. 

2. Exécutez **AzInfoProtection.exe** et suivez les invites pour installer le client.

    Pour ce didacticiel, peu importe si vous sélectionnez l’option d’installation d’une stratégie de démonstration, étant donné que la stratégie que nous venons de configurer sera téléchargée à partir d’Azure et remplacera la stratégie de démonstration installée. Toutefois, vous pouvez utiliser l’option de stratégie de démonstration si vous souhaitez simplement découvrir les étiquettes par défaut sans connexion à Azure Information Protection. 

## <a name="install-the-rights-management-sharing-application"></a>installation de l’application de partage Rights Management 

1. Accédez à la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

2. Dans la section **Ordinateurs** , cliquez sur l’icône de l’ **application RMS pour Windows** et enregistrez le fichier **Setup.exe** pour installer l’application de partage Microsoft Rights Management.

3. Dans la page **Installer Microsoft RMS** , cliquez sur **Suivant**, puis attendez que l’installation se termine. Ensuite, cliquez sur **Redémarrer** si vous êtes invité à redémarrer votre ordinateur, ou sur **Fermer** pour terminer l’installation.


## <a name="verify-the-installations"></a>Vérifier les installations

Vérifiez que ces installations se sont déroulées correctement en ouvrant Word et un nouveau document vierge (ne l’enregistrez pas pour l’instant). Si vous êtes invité à entrer votre nom d’utilisateur et votre mot de passe, entrez les détails de votre compte d’administrateur général. 

Pendant le chargement du document, trois nouveaux éléments doivent apparaître :

- Sous l’onglet **Accueil**, un nouveau groupe **Protection** avec un bouton intitulé **Protéger**.

    Cliquez sur **Protéger** > **Aide et de commentaires** puis, dans la boîte de dialogue **Microsoft Azure Information Protection**, vérifiez l’état de votre client. Il doit afficher **Information Protection policy is installed** (La stratégie Information Protection est installée) et une heure de connexion récente. Vérifiez que le nom d’utilisateur affiché correspond à celui de votre locataire.

- En outre, sous l’onglet **Accueil**, un nouveau groupe **RMS** avec un bouton intitulé **Partage protégé**.

- Une nouvelle barre sous le ruban, la barre Information Protection. Elle affiche le titre **Sensitivity** (Niveau de confidentialité) et l’étiquette par défaut **Internal** (Interne) que nous avons configurée. 
    
    ![Didacticiel de démarrage rapide Azure Information Protection Étape 3 : client installé](../media/word2013-callouts2.png)

Vous êtes maintenant prêt à voir Azure Information Protection en action.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’installation du client Azure Information Protection|[Installation du client Azure Information Protection](../rms-client/info-protect-client.md)|
|À propos de l’installation de l’application de partage Rights Management et des instructions utilisateur|[Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)|
|Installation par script de l’application de partage Rights Management pour Windows et informations techniques|[Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; Étape 2](infoprotect-tutorial-step2.md)
[Étape 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Nov16_HO2-->


