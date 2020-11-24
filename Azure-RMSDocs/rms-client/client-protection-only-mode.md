---
title: Mode Protection uniquement pour Azure Information Protection
description: Informations pour les utilisateurs qui exécutent le client Azure Information Protection en mode protection uniquement.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: a91aab5d0d12744fb782bac331cf4b3b4bbc2589
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568104"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>Guide de l’utilisateur : Mode Protection uniquement pour le client Azure Information Protection

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Lorsque le client Azure Information Protection ne dispose pas d’étiquettes pour classifier vos documents et e-mails, il s’exécute en mode **Protection uniquement**. Par exemple, dans ce mode, vous pouvez voir les informations suivantes lorsque vous utilisez l’Explorateur de fichiers Windows, cliquez avec le bouton droit et sélectionnez **Classifier et protéger** :

![Mode Protection uniquement](../media/protection-only-mode.png)

Le mode Protection uniquement s’exécute dans les scénarios suivants :

- Votre organisation n’a pas d’abonnement pour Azure Information Protection qui inclut des fonctionnalités de classification et d’étiquetage, mais qui a un abonnement pour Microsoft 365 qui inclut la protection des données à l’aide du service de Rights Management Azure. 
    
    - Vous pouvez utiliser le client Azure Information Protection pour protéger des fichiers et afficher des fichiers protégés. Vous ne pouvez pas classifier ni étiqueter des documents et e-mails.

- Votre organisation a un abonnement à Azure Information Protection uniquement pour un sous-ensemble d’utilisateurs :
    
    - Pour cette combinaison d’abonnements, est de la responsabilité de l’administrateur de s’assurer que seul le sous-ensemble d’utilisateurs peut utiliser les fonctionnalités de classification et d’étiquetage. Les autres utilisateurs doivent exécuter le client Azure Information Protection en mode Protection uniquement. 

- Votre organisation a un abonnement à Azure Information Protection, mais vous n’avez pas d’étiquette configurée pour vous.
    
    - Cela peut se produire quand toutes les étiquettes de la stratégie globale sont désactivées et que votre compte n’est pas ajouté à une stratégie délimitée. Votre service informatique commence peut-être tout juste le lancement d’Azure Information Protection et ne vous a pas encore fourni les étiquettes permettant de classer vos documents et e-mails. En attendant, vous pouvez utiliser le client Azure Information Protection pour protéger des fichiers et afficher des fichiers protégés.

- Votre organisation dispose d’un abonnement à Azure Information Protection, mais vous ne pouvez pas télécharger la stratégie Azure Information Protection. 
    
    - Cela peut se produire lorsque la configuration est incorrecte ou lorsque votre connexion a échoué. Contactez votre support technique ou votre administrateur. En attendant, vous pourrez peut-être utiliser le client Azure Information Protection pour protéger des fichiers et afficher des fichiers protégés.

- Votre organisation n’utilise que les services AD RMS (Active Directory Rights Management Services). 


## <a name="limitations-for-protection-only-mode"></a>Restrictions du mode protection uniquement

- Dans les applications Office, la barre Azure Information Protection ne s’affiche pas. Lorsque vous cliquez sur **protéger**  >  la **barre afficher**, cette option de menu n’est pas disponible.

- Lorsque vous utilisez la boîte de dialogue **Classifier et protéger - Azure Information Protection** avec l’Explorateur de fichiers, vous ne voyez pas les étiquettes de classification. À la place, comme dans l’image précédente, vous voyez une option permettant de sélectionner les modèles Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Tâches prises en charge dans le mode protection uniquement

- Protégez (et ôtez la protection) des documents et des e-mails à partir de vos applications Office, à l’aide de la fonctionnalité Office Information Rights Management (IRM) : par exemple : cliquez sur **fichier**  >  **informations**  >  **protéger le document**  >  **restreindre l’accès**. Pour plus d’informations, consultez [Utilisation de la protection des informations avec Office 365, Office 2019, Office 2016 ou Office 2013](../help-users.md#using-information-protection-with-office365-office-2019-office-2016-or-office2013).

- Protégez (et annulez la protection) des fichiers à l’aide de l’Explorateur de fichiers Windows : cliquez avec le bouton droit sur le ou les fichiers ou sur le dossier > **Classifier et protéger**. Pour appliquer la protection qui a été configurée par votre administrateur, dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, cliquez sur **Sélectionner un modèle** et choisissez l’un des modèles disponibles.

- Affichez des fichiers protégés à l’aide de la visionneuse Azure Information Protection.

- Accédez au site de suivi des documents depuis vos applications Office. Toutefois, vous devez disposer d’un abonnement valide pour suivre et révoquer des documents à partir de ce site.
  
