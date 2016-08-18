---
title: "Comment configurer une étiquette pour appliquer Rights Management protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 798fb423ff8dab3e9777a33e7b2c483bceb81016


---

# Comment configurer une étiquette pour appliquer Rights Management protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour éviter la perte de données. Cette protection est appliquée lorsque vous configurez une étiquette pour utiliser un modèle de gestion des droits. 

Ce modèle peut être l’un des modèles par défaut créés automatiquement lorsque vous activez Azure Rights Management, ou un modèle personnalisé. Les modèles pour services Azure Rights Management sont pris en charge, mais appliquent la protection uniquement lorsque l’auteur du document ou de l’e-mail figure dans l’étendue configurée du modèle. Si l’utilisateur n’y figure pas, il reçoit un message indiquant qu’Azure Information Protection ne peut pas appliquer l’étiquette.

## Fonctionnement de la protection

Quand un document ou un e-mail est protégé par Rights Management, il est chiffré au repos et en transit et peut uniquement être déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel de l’entreprise.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de la promotion. Tous les autres utilisateurs de votre organisation peuvent uniquement lire le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail qui contient des informations sur une réorganisation interne.

- Il est impossible d’ouvrir la liste de prix actuelle envoyée à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur les modèles Azure Rights Management et la manière de configurer ces droits d’utilisation et restrictions, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

Pour plus d’informations sur Azure Rights Management et son fonctionnement, consultez [Qu'est-ce qu'Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer la protection Azure Rights Management, le service Azure Rights Management doit être activé pour votre organisation. Si vous ne le n’avez pas déjà fait, consultez [Activation d'Azure Rights Management](../deploy-use/activate-service.md).


## Configuration d’une étiquette pour appliquer Rights Management protection

1. Si vous ne l’avez pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com) comme administrateur général pour récupérer les modèles Azure Rights Management. Accédez ensuite au panneau **Azure Information Protection**. 

    Par exemple, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, sélectionnez l’étiquette que vous souhaitez configurer pour appliquer Rights Management Protection.

3. Dans le panneau **Étiquette**, dans la section **Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette**, pour **Sélectionner le modèle RMS à partir de**, sélectionnez **Azure RMS** ou **AD RMS (PRÉVERSION)**.
    
    Dans la plupart des cas, vous devez sélectionner **Azure RMS**. Ne sélectionnez AD RMS que si vous avez lu et compris les conditions préalables et les restrictions qui accompagnent cette configuration, parfois appelée « *conservez votre propre clé* » (HYOK). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md).
    
4. Si vous avez sélectionné Azure RMS : pour **Sélectionner un modèle RMS**, cliquez sur la zone de liste déroulante et sélectionnez le modèle à utiliser pour protéger des documents et des e-mails avec cette étiquette.

    > [!NOTE] 
    > Si vous créez un modèle après avoir ouvert le panneau **Étiquette**, fermez ce panneau et retournez à l’étape 2 pour que votre modèle nouvellement créé soit récupéré depuis Azure en vue de sa sélection.
    
5. Si vous avez sélectionné AD RMS : indiquez le GUID du modèle et l’URL de licence de votre cluster AD RMS.

5. Cliquez sur **Enregistrer**.

6. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  



<!--HONumber=Aug16_HO2-->


