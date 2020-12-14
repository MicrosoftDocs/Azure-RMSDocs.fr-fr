---
title: Prise en main de l’utilisation et de la gestion de votre clé racine de locataire
description: Découvrez les étapes suivantes après avoir planifié la gestion de clé racine de locataire, y compris la clé par défaut générée par Microsoft et la protection BYOK.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9756710e29c82ef953633697cb989942d1844496
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382239"
---
# <a name="getting-started-with-tenant-root-keys"></a>Prise en main des clés racines du locataire

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Une fois la [planification, la création et la configuration de votre clé de locataire](plan-implement-tenant-key.md) si nécessaire, poursuivez avec les étapes suivantes :

- [Commencer à utiliser votre clé de locataire](#start-using-your-tenant-key)
- [Envisagez la journalisation de l’utilisation](#consider-usage-logging)

Pour plus d’informations sur les opérations de cycle de vie prises en charge pour votre clé de locataire, consultez [opérations pour votre clé de locataire Azure information protection](./operations-tenant-key.md).

Si votre organisation a besoin d’une protection locale pour du contenu hautement sensible, configurez la [protection DKE](plan-implement-tenant-key.md#double-key-encryption-dke) (client d’étiquetage unifié uniquement).

Si vous avez besoin d’une protection locale et que vous utilisez le client Classic, configurez la [protection hyok](configure-adrms-restrictions.md) à la place.
 

## <a name="start-using-your-tenant-key"></a>Commencer à utiliser votre clé de locataire

Activez le service Rights Management s’il n’est pas encore activé, pour permettre à votre organisation de commencer à utiliser Azure Information Protection. Les utilisateurs commencent immédiatement à utiliser votre clé de locataire.

Pour plus d’informations, consultez [Activation du service de protection à partir d’Azure Information Protection](./activate-service.md).

> [!NOTE]
> Si vous avez décidé de gérer votre propre clé de locataire après l’activation du service Rights Management, les utilisateurs passent graduellement de l’ancienne clé à la nouvelle clé au cours de quelques semaines.
>
>Pendant cette transition, les documents et les fichiers qui ont été protégés avec l’ancienne clé de locataire restent accessibles aux utilisateurs autorisés.

## <a name="consider-usage-logging"></a>Envisagez la journalisation de l’utilisation

La journalisation de l’utilisation journalise chaque transaction effectuée par le service Azure Rights Management.

Selon votre méthode de gestion de clés, les informations de journalisation peuvent inclure des détails sur votre clé de locataire. L’illustration suivante montre un exemple d’un fichier journal affiché dans Excel, où les types de demandes **KeyVaultDecryptRequest** et **KeyVaultSignRequest** indiquent que la clé de locataire est utilisée.
    
![fichier journal dans Excel où la clé de locataire est utilisée](./media/RMS_Logging.png)
    
Pour plus d’informations sur la journalisation de l’utilisation, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).
