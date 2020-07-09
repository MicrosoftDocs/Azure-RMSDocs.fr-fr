---
title: Opérations pour votre clé de locataire Azure Information Protection
description: Identifiez les différents niveaux de contrôle et de responsabilité associés à votre clé de locataire Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1284d0ee-0a72-45ba-a64c-3dcb25846c3d
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c8fc10aed7bcb0d42dab72afd4c1fc100a3962ba
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136370"
---
# <a name="operations-for-your-azure-information-protection-tenant-key"></a>Opérations pour votre clé de locataire Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Selon la topologie de votre clé de locataire pour Azure Information Protection, différents niveaux de contrôle et de responsabilité sont possibles pour votre clé de locataire Azure Information Protection. Les deux topologies de clé sont : **Gérée par Microsoft** et **Gérée par le client**.

La gestion de votre propre clé de locataire dans Azure Key Vault est souvent appelée BYOK (Bring Your Own Key). Pour plus d’informations sur ce scénario et découvrir comment choisir entre les deux topologies de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

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

Toutefois, si vous souhaitez créer une clé de client Azure Information Protection en important un domaine de publication approuvé (TPD) à partir d’Active Directory Rights Management Services, cette opération d’importation fait partie de la [migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).  

