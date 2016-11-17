---
title: "Comment configurer une étiquette pour appliquer la protection Rights Management | Azure Information Protection"
description: "Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour éviter la perte de données. Cette protection est appliquée lorsque vous configurez une étiquette pour utiliser un modèle de gestion des droits."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: addc24fed28cee52b57c7e3bde926d6324478e7b
ms.openlocfilehash: 4f3c77df23207c3a76a768a1fe428484339de18f


---

# <a name="how-to-configure-a-label-to-apply-rights-management-protection"></a>Comment configurer une étiquette pour appliquer Rights Management protection

>*S’applique à : Azure Information Protection*

Vous pouvez protéger vos documents et e-mails les plus sensibles à l’aide d’un service Rights Management qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour éviter la perte de données. Cette protection est appliquée lorsque vous configurez une étiquette pour utiliser un modèle de gestion des droits. 

Ce modèle peut être l’un des modèles par défaut créés automatiquement lorsque vous activez Azure Rights Management, ou un modèle personnalisé. Les modèles pour services Azure Rights Management sont pris en charge, mais appliquent la protection uniquement lorsque l’auteur du document ou de l’e-mail figure dans l’étendue configurée du modèle. Si l’utilisateur n’y figure pas, il reçoit un message indiquant qu’Azure Information Protection ne peut pas appliquer l’étiquette.

## <a name="how-the-protection-works"></a>Fonctionnement de la protection

Quand un document ou un e-mail est protégé par Rights Management, il est chiffré au repos et en transit et peut uniquement être déchiffré par les utilisateurs autorisés. Ce chiffrement est conservé avec le document ou l’e-mail, même si ce dernier est renommé. En outre, vous pouvez configurer des droits d’utilisation et des restrictions, comme dans les exemples suivants :

- Seuls les utilisateurs de votre organisation peuvent ouvrir le document ou l’e-mail confidentiel de l’entreprise.

- Seuls les utilisateurs du service marketing peuvent modifier et imprimer le document ou l’e-mail d’annonce de la promotion. Tous les autres utilisateurs de votre organisation peuvent uniquement lire le document ou l’e-mail.

- Les utilisateurs ne peuvent pas transférer un e-mail qui contient des informations sur une réorganisation interne.

- Il est impossible d’ouvrir la liste de prix actuelle envoyée à des partenaires commerciaux après une date spécifiée.

Pour plus d’informations sur les modèles Azure Rights Management et la façon de configurer ces droits et ces restrictions d’utilisation, consultez [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

Pour plus d’informations sur Azure Rights Management et son fonctionnement, consultez [Qu'est-ce qu'Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Pour configurer une étiquette pour appliquer la protection Azure Rights Management, le service Azure Rights Management doit être activé pour votre organisation. Si vous ne le n’avez pas déjà fait, consultez [Activation d'Azure Rights Management](../deploy-use/activate-service.md).


## <a name="to-configure-a-label-to-apply-rights-management-protection"></a>Configuration d’une étiquette pour appliquer Rights Management protection

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général, puis accédez au panneau **Azure Information Protection**. 

    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, sélectionnez l’étiquette que vous souhaitez configurer pour appliquer Rights Management Protection.

3. Dans le panneau **Étiquette**, dans la section **Définir le modèle RMS pour la protection des documents et e-mails contenant cette étiquette**, pour **Sélectionner le modèle RMS à partir de**, sélectionnez **Azure RMS** ou **AD RMS (PRÉVERSION)**.
    
    Dans la plupart des cas, vous devez sélectionner **Azure RMS**. Ne sélectionnez AD RMS que si vous avez lu et compris les conditions préalables et les restrictions qui accompagnent cette configuration, parfois appelée « *conservez votre propre clé* » (HYOK). Pour plus d’informations, consultez [HYOK (conservez votre propre clé) : exigences et restrictions pour la protection AD RMS](configure-adrms-restrictions.md).
    
4. Si vous avez sélectionné Azure RMS : Pour **Sélectionner un modèle RMS**, cliquez sur la zone de liste déroulante et sélectionnez le [modèle](../deploy-use/configure-custom-templates.md) ou l’option Rights Management à utiliser pour protéger des documents et des e-mails avec cette étiquette.
    
    Plus d’informations sur les options :
    
    - Avez-vous créé un modèle après avoir ouvert le panneau **Étiquette**? Fermez ce panneau et retournez à l’étape 2 pour que votre modèle nouvellement créé soit récupéré dans Azure et puisse être sélectionné.
    
    - Si vous sélectionnez un **modèle de service** ou que vous avez configuré des [contrôles d’intégration](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) :
    
        - Les utilisateurs en dehors de l’étendue configurée du modèle ou qui sont exclus de l’application de la protection d’Azure Rights Management continuent de voir l’étiquette, mais ne peuvent pas l’appliquer. S’ils sélectionnent l’étiquette, ils voient le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**
        
    - Si vous sélectionnez **Supprimer la Protection**:
        
        - Les utilisateurs doivent disposer des autorisations nécessaires pour supprimer la protection Rights Management et appliquer une étiquette qui contient cette option. Cette option implique qu’ils disposent du [droit d’utilisation](../deploy-use/configure-usage-rights.md) **Exporter** (pour les documents Office) ou **Control total**, ou qu’ils soient propriétaires de Rights Management (ce qui accorde automatiquement le droit d’utilisation Contrôle total), ou encore un [super utilisateur pour Azure Rights Management](../deploy-use/configure-super-users.md). Les modèles de gestion de droits par défaut n’incluent pas les droits d’utilisation qui permettent aux utilisateurs de supprimer la protection. 

            Si les utilisateurs n’ont pas les autorisations nécessaires pour supprimer la protection Rights Management et qu’ils sélectionnent cette étiquette avec l’option **Supprimer la Protection**, ils reçoivent le message suivant : **Azure Information Protection ne peut pas appliquer cette étiquette. Si le problème persiste, contactez votre administrateur.**

5. Si vous avez sélectionné AD RMS : indiquez le GUID du modèle et l’URL de licence de votre cluster AD RMS. [Plus d’informations](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. Cliquez sur **Enregistrer**.

7. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  



<!--HONumber=Nov16_HO1-->


