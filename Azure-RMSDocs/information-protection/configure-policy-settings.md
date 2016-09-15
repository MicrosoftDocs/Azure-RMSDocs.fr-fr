---
title: "Comment configurer les paramètres de stratégie globaux pour Azure Information Protection | Azure Information Protection"
description: "Il existe 3 paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils."
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: 872ea7da6f3b72a355a73c8b0589beda86ded20d


---

# Comment configurer les paramètres de stratégie globaux pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Il existe 3 paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils :

![Paramètres globaux de la stratégie Azure Information Protection](../media/info-protect-policy-settings.png)


Pour configurer ces paramètres :

1. Si vous ne l’avez pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, configurez les paramètres globaux suivants :

    - **Tous les documents et e-mails doivent avoir une étiquette** : lorsque vous paramétrez cette option sur **Activé**, tous les documents et e-mails envoyés enregistrés doivent avoir une étiquette appliquée. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**. 

    Si aucune étiquette n’est affectée lorsqu’un utilisateur enregistre un document ou envoie un e-mail, il est invité à en sélectionner une :

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-enforce-label.png)

    - **Sélectionner l’étiquette par défaut** : lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes. 

    - **Users must provide justification to set a lower classification label, remove a label, or remove protection** (Les utilisateurs doivent fournir une justification pour définir une étiquette de classification d’un niveau inférieur, supprimer une étiquette ou enlever la protection) : si cette option est définie sur **On** et qu’un utilisateur effectue l’une de ces actions (par exemple, s’il modifie le niveau de l’étiquette **Secret** à **Personnel**), l’utilisateur est invité à justifier cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Application** > **Microsoft Azure Information Protection**.  

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-lower-justification.png)

    Cette option n’est pas applicable pour les sous-étiquettes.

3. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.

4. Pour que les modifications soient disponibles pour les utilisateurs, cliquez sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  












<!--HONumber=Sep16_HO1-->


