---
title: Installation du client Azure Information Protection | Azure Information Protection
description: "Instructions pour installer le client qui ajoute une barre Information Protection à vos applications Office, à partir de laquelle vous pouvez sélectionner des étiquettes de classification pour vos documents et e-mails."
manager: mbaldwin
ms.date: 09/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 2ecdfe905694b3d14727abdb5e6176d24f675d2e
ms.openlocfilehash: cd6684dd25a721272c073fcc972724a6b81c0c72


---

# Installation du client Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Pour classer les documents et les e-mails à l’aide d’Azure Information Protection, vous devez d’abord installer le client Azure Information Protection client. Cette installation ajoute une barre Information Protection à vos applications Office (Word, Excel, PowerPoint, Outlook), qui affiche les étiquettes de classification pour votre organisation, en plus d’un nouveau groupe **Protection** dans l’onglet **Accueil** (Word, Excel, PowerPoint), qui contient un bouton nommé **Protéger** :

L’illustration suivante montre cette barre Information Protection et les étiquettes de la [stratégie par défaut](configure-policy-default.md) :

![Barre Azure Information Protection avec la stratégie par défaut](../media/info-protect-bar-default.png)

Téléchargez le client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Avant d’installer le client, vérifiez que vous disposez des versions et des applications nécessaires du système d’exploitation : [Configuration requise pour Azure Information Protection](requirements-azure-infoprotect.md).


## Installation manuelle du client Azure Information Protection

1. Après avoir [téléchargé le client](https://www.microsoft.com/en-us/download/details.aspx?id=53018), exécutez **AzInfoProtection.exe** et suivez les invites pour installer le client. Cette installation nécessite des autorisations administratives locales.

    Sélectionnez l’option d’installation d’une stratégie de démonstration si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation. 

2. Pour commencer à utiliser le client Azure Information Protection : si votre ordinateur exécute Office 2010, redémarrez votre ordinateur. Pour d’autres versions d’Office, redémarrez les applications Office.

## Installation du client Azure Information Protection pour des utilisateurs

- Vous pouvez créer un script pour automatiser l’installation du client Azure Information Protection à l’aide d’options de ligne de commande. Pour afficher les options d’installation, exécutez `AzInfoProtection.exe /help`.

    Par exemple, pour installer le client en mode silencieux : `AzInfoProtection.exe /passive | quiet`


## Désinstallation du client Azure Information Protection

Choisissez l’une des méthodes suivantes :

- Utilisez le panneau de configuration pour désinstaller un programme : cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez **AzInfoProtection.exe** et, dans la page **Modifier l’installation**, cliquez sur **Désinstaller**. 

- Exécuter `AzInfoProtection.exe /uninstall`


## Vérification de l’installation et de l’état de la connexion, ou signalisation d’un problème

1. Ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**.

2. Notez les éléments suivants dans la boîte de dialogue **Microsoft Azure Information Protection** :

    - La valeur de la **Dernière connexion** qui identifie la date/heure de la dernière connexion du client au service Azure Information Protection de votre organisation. Lorsque le client se connecte au service, il télécharge automatiquement la dernière stratégie s’il détecte des modifications dans sa stratégie actuelle. Si vous avez apporté des modifications à la stratégie après l’heure affichée, fermez et rouvrez l’application Office.

    - Le nom d’utilisateur affiché qui identifie le compte utilisé pour vous authentifier auprès d’Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory.

    - La version du client Azure Information Protection.

    - Le lien **Envoyer des commentaires**, que vous pouvez utiliser pour joindre automatiquement vos journaux de client à un e-mail qui peut être envoyé à l’équipe d’Information Protection à des fins d’analyse.

    - Le lien **Exécuter les diagnostics** : cette fonctionnalité n’est pas implémentée actuellement.

## Raccourcis clavier de la barre Azure Information Protection

Pour accéder à la barre Azure Information Protection à l’aide du clavier, utilisez la combinaison de touches suivante :

- Appuyez sur **Ctrl** + **Maj** + **~** 

Utilisez ensuite la touche de tabulation pour sélectionner les étiquettes et autres commandes de la barre (icônes **Masquer les étiquettes** et **Supprimer les étiquettes**), puis appuyez sur la touche Entrée pour les sélectionner.


## Emplacements des fichiers

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichier de stratégie actuellement installé :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**


## Étapes suivantes

Pour modifier les étiquettes dans la barre Information Protection, vous devez configurer la stratégie Azure Information Protection. Pour en savoir plus, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md). 



<!--HONumber=Sep16_HO2-->


