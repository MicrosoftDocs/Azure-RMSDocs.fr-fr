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
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4e3c194be533adce625d1a15ad3fdfcd863da279
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384330"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>Comment les serveurs de fichiers Windows qui utilisent FCI prennent en charge Azure Rights Management

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

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


