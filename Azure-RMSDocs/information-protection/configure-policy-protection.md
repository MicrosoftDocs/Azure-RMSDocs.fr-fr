---
title: "Comment configurer une étiquette pour appliquer Rights Management protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# Comment configurer une étiquette pour appliquer Rights Management protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’Azure Rights Management, qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour éviter la perte de données. Cette protection est appliquée lorsque vous configurez une étiquette pour utiliser un modèle de gestion des droits. 

Ce modèle peut être l’un des modèles par défaut créés automatiquement lorsque vous activez Azure Rights Management, ou un modèle personnalisé. Les modèles pour départements sont pris en charge, mais appliquent la protection uniquement lorsque l’auteur du document ou de l’e-mail figure dans l’étendue configurée du modèle. Si l’utilisateur n’y figure pas, il reçoit un message indiquant qu’Azure Information Protection ne peut pas appliquer l’étiquette.

## Fonctionnement de la protection

Lorsqu’un document ou un e-mail est protégé par Azure Rights Management, il est chiffré au repos et en transit et peut uniquement être déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail. Tous les autres utilisateurs de votre organisation peuvent uniquement afficher le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail.

- Il est impossible d’ouvrir des documents ou des e-mails envoyés à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur les modèles et la manière de configurer ces droits d’utilisation et restrictions, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

Pour plus d’informations sur Azure Rights Management et son fonctionnement, consultez [Qu'est-ce qu'Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer la Rights Management Protection, le service Azure Rights Management doit être activé pour votre organisation. Si vous ne le n’avez pas déjà fait, consultez [Activation d'Azure Rights Management](../deploy-use/activate-service.md).


## Configuration d’une étiquette pour appliquer Rights Management protection

1. Connectez-vous au [portail Azure](https://portal.azure.com).
 
2. Dans le menu hub, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

3. Dans le panneau **Azure Information Protection**, sélectionnez l’étiquette que vous souhaitez configurer pour appliquer Rights Management Protection.

4. Dans le panneau **Étiquette**, dans la section **Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette**, configurez les éléments suivants :

    - Si vous voyez **Sélectionner le modèle RMS à partir de :**, sélectionnez **Azure RMS**. 
    
        Ne sélectionnez pas **AD RMS** et les options de configuration associées sans l’assistance de Microsoft. Si vous êtes intéressé par un test d’Azure Information Protection avec Active Directory Rights Management Services, envoyez un e-mail à askipteam@microsoft.com. 
    
    - Pour **Sélectionner un modèle RMS** : cliquez sur la zone de liste déroulante et sélectionnez le modèle que vous souhaitez utiliser pour protéger des documents et des e-mails avec cette étiquette.

        > [!NOTE] Si vous créez un nouveau modèle après avoir ouvert le panneau **Étiquette**, fermez ce panneau et retourner à l’étape 3, afin que votre modèle nouvellement créé soit récupéré depuis Azure en vue de sa sélection.

5. Cliquez sur **Enregistrer**.

6. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  



<!--HONumber=Jul16_HO5-->


