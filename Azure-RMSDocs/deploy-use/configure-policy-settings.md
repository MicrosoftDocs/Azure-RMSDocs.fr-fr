---
title: "Comment configurer les paramètres de stratégie globaux | Azure Information Protection"
description: "Il existe 3 paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: addc24fed28cee52b57c7e3bde926d6324478e7b
ms.openlocfilehash: 970a42e89d09af34e9ff16714682d1de250175f6


---

# <a name="how-to-configure-the-global-policy-settings-for-azure-information-protection"></a>Comment configurer les paramètres de stratégie globaux pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Il existe 3 paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils :

![Paramètres globaux de la stratégie Azure Information Protection](../media/info-protect-policy-settings.png)


Pour configurer ces paramètres :

1. Si ce n’est déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, configurez les paramètres globaux suivants :

    - **Tous les documents et e-mails doivent avoir une étiquette** : lorsque vous paramétrez cette option sur **Activé**, tous les documents et e-mails envoyés enregistrés doivent avoir une étiquette appliquée. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**. 

    Si aucune étiquette n’est affectée lorsqu’un utilisateur enregistre un document ou envoie un e-mail, il est invité à en sélectionner une :

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-enforce-label.png)

    - **Sélectionner l’étiquette par défaut** : lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes. 

    - **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection** : si cette option est définie sur **On** et qu’un utilisateur effectue l’une de ces actions (par exemple, s’il modifie le niveau de l’étiquette **Secret** à **Personnel**), l’utilisateur est invité à justifier cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Application** > **Microsoft Azure Information Protection**.  

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-lower-justification.png)

    Cette option n’est pas applicable pour les sous-étiquettes.

3. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.

4. Pour que les modifications soient disponibles pour les utilisateurs, cliquez sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  












<!--HONumber=Nov16_HO1-->


