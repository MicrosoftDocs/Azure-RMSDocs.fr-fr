---
title: "Opérations pour votre clé de locataire Azure Rights Management | Azure Information Protection"
description: "Identifiez les différents niveaux de contrôle et de responsabilité associés à votre clé de locataire Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: 780c4db3e791dd427828550e428ec4ea18d55fd5


---

# Opérations pour votre clé de locataire Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Selon la typologie de votre clé de locataire (gérée par Microsoft ou par le client), différents niveaux de contrôle et de responsabilité s’offrent à vous pour votre clé de locataire Azure Information Protection après l’implémentation de celle-ci.

La gestion de votre propre clé de locataire dans Azure Key Vault est souvent appelée BYOK (Bring Your Own Key). Pour plus d’informations sur ce scénario et découvrir comment choisir entre les deux typologies de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

Le tableau suivant présente les opérations que vous pouvez faire, selon la typologie que vous avez choisie pour votre clé de locataire Azure Information Protection.

|Opération de cycle de vie|Gérée par Microsoft (par défaut)|Gérée par le client (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Révocation de votre clé de locataire|Non (automatique)|Oui|
|Renouvellement de votre clé de locataire|Oui|Oui|
|Sauvegarde et récupération de votre clé de locataire|Non|Oui|
|Exportation de votre clé de locataire|Oui|Non|
|Réponse à une violation|Oui|Oui|

Après avoir identifié la typologie implémentée, sélectionnez l’une des sections suivantes pour obtenir plus d’informations sur ces opérations pour votre clé de locataire Azure Information Protection :


- [Clé de locataire gérée par Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clé de locataire gérée par le client](operations-customer-managed-tenant-key.md)







<!--HONumber=Sep16_HO4-->


