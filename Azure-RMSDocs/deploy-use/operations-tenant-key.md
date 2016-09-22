---
title: "Opérations pour votre clé de locataire Azure Rights Management | Azure RMS"
description: "Identifiez les différents niveaux de contrôle et de responsabilité associés à votre clé de locataire Azure Rights Management (Azure RMS)."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: d496a99c4b05e0cf0ba5929f44cdbd1906d31341


---

# Opérations pour votre clé de client Azure Rights Management

>*S’applique à : Azure Rights Management, Office 365*

Selon la typologie de votre clé de locataire (gérée par Microsoft ou par le client), différents niveaux de contrôle et de responsabilité sont disponibles pour votre clé de locataire Microsoft Azure Rights Management (Azure RMS) après l'implémentation de celle-ci.

La gestion de votre propre clé de locataire dans Azure Key Vault est souvent appelée BYOK (Bring Your Own Key). Pour plus d’informations sur ce scénario et découvrir comment choisir entre les deux typologies de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

Le tableau suivant présente les opérations que vous pouvez faire, selon la typologie que vous avez choisie pour votre clé de locataire Azure.

|Opération de cycle de vie|Gérée par Microsoft (par défaut)|Gérée par le client (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Révocation de votre clé de locataire|Non (automatique)|Oui|
|Renouvellement de votre clé de locataire|Oui|Oui|
|Sauvegarde et récupération de votre clé de locataire|Non|Oui|
|Exportation de votre clé de locataire|Oui|Non|
|Réponse à une violation|Oui|Oui|

Après avoir identifié la typologie implémentée, sélectionnez l’une des sections suivantes pour obtenir plus d’informations sur ces opérations pour votre clé de locataire Azure RMS :


- [Clé de locataire gérée par Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clé de locataire gérée par le client](operations-customer-managed-tenant-key.md)







<!--HONumber=Aug16_HO4-->


