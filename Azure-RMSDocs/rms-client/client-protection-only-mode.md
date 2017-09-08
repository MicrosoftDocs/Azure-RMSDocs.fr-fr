---
title: "Mode Protection uniquement pour Azure Information Protection"
description: "Informations pour les utilisateurs qui exécutent le client Azure Information Protection en mode protection uniquement."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 84644f717a6005245847c9e9598b87c5af885aa7
ms.sourcegitcommit: 6000258a9f973a3ab8e608eda57b88a469e7b754
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/08/2017
---
# <a name="protection-only-mode-for-the-azure-information-protection-client"></a>Mode Protection uniquement pour le client Azure Information Protection

Lorsque le client Azure Information Protection ne dispose pas d’étiquettes pour classifier vos documents et e-mails, il s’exécute en mode **Protection uniquement**. Par exemple, dans ce mode, vous pouvez voir les informations suivantes lorsque vous utilisez l’Explorateur de fichiers Windows, cliquez avec le bouton droit et sélectionnez **Classifier et protéger** :

![Mode Protection uniquement](../media/protection-only-mode.png)

Le mode Protection uniquement s’exécute dans les scénarios suivants :

- Votre organisation n’a pas d’abonnement à Azure Information Protection incluant les fonctionnalités de classification et d’étiquetage, mais elle a un abonnement à Office 365 qui inclut la protection des données à travers le service Azure Rights Management. 
    
    - Vous pouvez utiliser le client Azure Information Protection pour protéger des fichiers et afficher des fichiers protégés. Vous ne pouvez pas classifier ni étiqueter des documents et e-mails.

- Votre organisation a un abonnement à Azure Information Protection uniquement pour un sous-ensemble d’utilisateurs :
    
    - Pour cette combinaison d’abonnements, l’administrateur est responsable de s’assurer que seul le sous-ensemble d’utilisateurs peut utiliser les fonctionnalités de classification et d’étiquetage. Les autres utilisateurs doivent exécuter le client Azure Information Protection en mode Protection uniquement. 

- Votre organisation dispose d’un abonnement à Azure Information Protection, mais vous ne pouvez pas télécharger la stratégie Azure Information Protection. 
    
    - Cela peut se produire lorsque la configuration est incorrecte ou lorsque votre connexion a échoué. Contactez votre support technique ou votre administrateur. En attendant, vous pourrez peut-être utiliser le client Azure Information Protection pour protéger des fichiers et afficher des fichiers protégés.

## <a name="limitations-for-protection-only-mode"></a>Restrictions du mode protection uniquement

- Dans les applications Office, la barre Azure Information Protection ne s’affiche pas. Lorsque vous cliquez sur **Protéger** > **Afficher la barre**, cette option de menu n’est pas disponible.

- Lorsque vous utilisez la boîte de dialogue **Classifier et protéger - Azure Information Protection** avec l’Explorateur de fichiers, vous ne voyez pas les étiquettes de classification. À la place, comme dans l’image précédente, vous voyez une option permettant de sélectionner les modèles Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Tâches prises en charge dans le mode protection uniquement

- Protégez (et annulez la protection) des documents et des e-mails à partir de vos applications Office, à l’aide de la fonctionnalité Information Rights Management (IRM) d’Office. Par exemple : cliquez sur **Fichier** > **Info** > **Protéger le document** > **Restreindre l’accès**. Pour plus d’informations, consultez [Utilisation de la protection des informations avec Office 365, Office 2016 ou Office 2013](../deploy-use/help-users.md).

- Protégez (et annulez la protection) des fichiers à l’aide de l’Explorateur de fichiers Windows : cliquez avec le bouton droit sur le ou les fichiers ou sur le dossier > **Classifier et protéger**. Pour appliquer la protection qui a été configurée par votre administrateur, dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Sélectionner un modèle** et choisissez l’un des modèles disponibles.

- Affichez des fichiers protégés à l’aide de la visionneuse Azure Information Protection.

- Accédez au site de suivi des documents depuis vos applications Office. Toutefois, vous devez disposer d’un abonnement valide pour suivre et révoquer des documents à partir de ce site.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  
