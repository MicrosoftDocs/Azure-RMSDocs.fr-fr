---
title: "Opérations pour votre clé de locataire Azure Information Protection"
description: "Identifiez les différents niveaux de contrôle et de responsabilité associés à votre clé de locataire Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: afe33bcee3516589bd87642b0f15206b90a4bb41
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Opérations pour votre clé de locataire Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Selon la topologie de votre clé de locataire pour Azure Information Protection, différents niveaux de contrôle et de responsabilité sont possibles pour votre clé de locataire Azure Information Protection. Les deux topologies de clé sont : **Gérée par Microsoft** et **Gérée par le client**.

La gestion de votre propre clé de locataire dans Azure Key Vault est souvent appelée BYOK (Bring Your Own Key). Pour plus d’informations sur ce scénario et découvrir comment choisir entre les deux topologies de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

Le tableau suivant présente les opérations que vous pouvez faire, en fonction de la topologie que vous avez choisie pour votre clé de locataire Azure Information Protection.

|Opération de cycle de vie|Gérée par Microsoft (par défaut)|Gérée par le client (BYOK)|
|-----------------------|-------------------------------|---------------------------|
|Révocation de votre clé de locataire|Non (automatique)|Oui|
|Renouvellement de votre clé de locataire|Oui|Oui|
|Sauvegarde et récupération de votre clé de locataire|Non|Oui|
|Exportation de votre clé de locataire|Oui|Non|
|Réponse à une violation|Oui|Oui|

Après avoir identifié la topologie implémentée, sélectionnez un des liens suivants pour obtenir plus d’informations sur ces opérations pour votre clé de locataire Azure Information Protection :

- [Clé de locataire gérée par Microsoft](operations-microsoft-managed-tenant-key.md)
- [Clé de locataire gérée par le client](operations-customer-managed-tenant-key.md)

Toutefois, si vous souhaitez créer une clé de client Azure Information Protection en important un domaine de publication approuvé (TPD) à partir d’Active Directory Rights Management Services, cette opération d’importation fait partie de la [migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
