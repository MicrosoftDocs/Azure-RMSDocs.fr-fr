---
title: Prise en main de l’utilisation et de la gestion de votre clé racine de locataire
description: Découvrez les étapes suivantes après avoir planifié la gestion de clé racine de locataire, y compris la clé par défaut générée par Microsoft et la protection BYOK.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0d0fe05fa31e14c583362183e28cc14835d78268
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86869644"
---
# <a name="getting-started-with-tenant-root-keys"></a>Prise en main des clés racines du locataire

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Une fois la planification, la création et la configuration de votre clé de locataire si nécessaire, poursuivez avec les étapes suivantes :

- [Commencer à utiliser votre clé de locataire](#start-using-your-tenant-key)
- [Envisagez la journalisation de l’utilisation](#consider-usage-logging)

Pour plus d’informations sur les opérations de cycle de vie prises en charge pour votre clé de locataire, consultez [opérations pour votre clé de locataire Azure information protection](./operations-tenant-key.md).

> [!TIP]
> Si votre organisation a besoin d’une protection locale pour du contenu hautement sensible, configurez la [protection hyok](configure-adrms-restrictions.md) (clients classiques uniquement) ou la [protection DKE](plan-implement-tenant-key.md#double-key-encryption-dke-aip-unified-labeling-client-only) (client d’étiquetage unifié uniquement).
> 

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
