---
title: "Comment configurer les paramètres de stratégie globaux pour Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 3b22cf76f03a4d36281db7e705359402dcbbde0e


---

# Comment configurer les paramètres de stratégie globaux pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Il existe 3 paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils :

![Paramètres globaux de la stratégie Azure Information Protection](../media/info-protect-policy-settings.png)


Pour configurer ces paramètres :

1. Connectez-vous au [portail Azure](https://portal.azure.com).
 
2. Dans le menu hub, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

3. Dans le panneau **Azure Information Protection**, configurez les paramètres globaux suivants :

    - **Tous les documents et e-mails doivent avoir une étiquette** : lorsque vous paramétrez cette option sur **Activé**, tous les documents et e-mails envoyés enregistrés doivent avoir une étiquette appliquée. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**. 

    Si aucune étiquette n’est affectée lorsqu’un utilisateur enregistre un document ou envoie un e-mail, il est invité à en sélectionner une :

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-enforce-label.png)

    - **Sélectionner l’étiquette par défaut** : lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes. 

    - **Les utilisateurs doivent fournir une justification quand ils abaissent le niveau de confidentialité** : lorsque vous paramétrez cette option sur **Activé** et qu’un utilisateur modifie l’étiquette d’un document ou d’un e-mail existant à une étiquette qui a un niveau de confidentialité inférieur (par exemple, de **Secret** à **Public**), il est invité à fournir une explication pour cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Application** > **Microsoft Azure Information Protection**.  

    ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-lower-justification.png)

    Cette option n’est pas applicable pour les sous-étiquettes.

4. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.

5. Pour que les modifications soient disponibles pour les utilisateurs, cliquez sur **Publier**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  












<!--HONumber=Jul16_HO5-->


