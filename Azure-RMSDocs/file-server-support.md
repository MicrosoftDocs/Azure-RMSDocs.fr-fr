---
title: Comment les serveurs de fichiers Windows qui utilisent FCI prennent en charge Azure RMS-AIP
description: Découvrez comment utiliser l’infrastructure de classification des fichiers Windows Server avec Azure RMS quand vous déployez le connecteur RMS pour protéger automatiquement des documents Office.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ROBOTS: NOINDEX
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2de7d165c72dbd6c96f76d7027c1a2d3ba62bff1
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806190"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>Comment les serveurs de fichiers Windows qui utilisent FCI prennent en charge Azure Rights Management

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Quand vous configurez Windows Server pour utiliser l’infrastructure de classification des fichiers, la fonctionnalité Outils de gestion de ressources pour serveur de fichiers (FSRM) peut analyser les fichiers locaux pour déterminer s’ils contiennent des données sensibles. 

Les fichiers qui répondent à ces critères sont marqués avec les propriétés de classification définies par un administrateur. L’infrastructure de classification des fichiers peut effectuer automatiquement une action, selon la classification. 

L’une de ces actions comprend l’application de la protection des informations à l’aide d’Azure Rights Management et le déploiement du connecteur Rights Management (également appelé connecteur RMS). Les fichiers Office sont alors automatiquement protégés par Azure RMS.

> [!TIP]
> Pour protéger tous les types de fichier, au lieu d’utiliser le connecteur RMS, exécutez un script Windows PowerShell qui utilise des applets de commande du [module Azure Information Protection](./rms-client/client-admin-guide-powershell.md).
> 

Les stratégies de classification sont entièrement configurables et très extensibles pour vous permettre d'empêcher d'éventuelles fuites de données par des utilisateurs autorisés ou non autorisés. L’outil de protection peut même contribuer à réduire le risque de fuite de données dues aux administrateurs réseau, car vous pouvez configurer des stratégies qui n’exigent pas que ceux-ci aient accès aux fichiers.

Pour obtenir des instructions sur le déploiement et la configuration du connecteur RMS pour les fichiers Office, consultez [déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Pour obtenir des instructions sur l’utilisation du script Windows PowerShell pour tous les types de fichiers, consultez 

- [Protection RMS avec Windows Server Infrastructure de classification des fichiers &#40;FCI&#41;](./rms-client/configure-fci.md)
- [Script Windows PowerShell pour la protection Azure RMS à l’aide de l’ICF des outils de gestion de ressources pour serveur de fichiers](rms-client/fci-script.md)


## <a name="next-steps"></a>Étapes suivantes

À présent que vous savez comment les applications et services prennent en charge Azure RMS, vous pouvez comparer Azure RMS à la version locale de Rights Management, les services AD RMS (Active Directory Rights Management Services). Pour une comparaison des fonctionnalités, des exigences et des contrôles de sécurité, consultez [comparaison d’Azure Rights Management et AD RMS](compare-on-premise.md).


