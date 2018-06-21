---
title: Prise en charge d’Azure RMS d’Azure Information Protection par les serveurs de fichiers utilisant ICF
description: Découvrez comment utiliser l’infrastructure de classification des fichiers Windows Server avec Azure RMS quand vous déployez le connecteur RMS pour protéger automatiquement des documents Office.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f36e39ba4fbd04fca9277bd45986e021c82df0a5
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206231"
---
# <a name="how-file-servers-that-run-windows-server-and-use-file-classification-infrastructure-fci-support-azure-rights-management"></a>Prise en charge d’Azure Rights Management par les serveurs de fichiers exécutant Windows Server et utilisant l’infrastructure de classification des fichiers (ICF)

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Quand vous configurez Windows Server pour utiliser l’infrastructure de classification des fichiers, la fonctionnalité Outils de gestion de ressources pour serveur de fichiers (FSRM) peut analyser les fichiers locaux pour déterminer s’ils contiennent des données sensibles. Quand les fichiers répondent à ces critères, ils sont balisés avec des propriétés de classification définies par un administrateur. L’infrastructure de classification des fichiers peut effectuer automatiquement une action, selon la classification. L’une de ces actions inclut l’application de la protection des informations via [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] et le déploiement du connecteur Rights Management (également appelé connecteur RMS). Les fichiers Office sont alors automatiquement protégés par Azure RMS.

Pour protéger tous les types de fichier, au lieu d’utiliser le connecteur RMS, exécutez un script Windows PowerShell qui utilise des applets de commande du [module Azure Information Protection](../rms-client/client-admin-guide-powershell.md).

Les stratégies de classification sont entièrement configurables et très extensibles pour vous permettre d’empêcher d’éventuelles fuites de données par des utilisateurs autorisés ou non autorisés. L’outil de protection peut même contribuer à réduire le risque de fuite de données dues aux administrateurs réseau, car vous pouvez configurer des stratégies qui n’exigent pas que ceux-ci aient accès aux fichiers.

Pour obtenir des instructions relatives au déploiement et à la configuration du connecteur RMS pour les fichiers Office, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Pour savoir comment utiliser le script Windows PowerShell pour tous les types de fichier, consultez [Protection RMS avec l’infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](../rms-client/configure-fci.md).



## <a name="next-steps"></a>Étapes suivantes
À présent que vous savez comment les applications et services prennent en charge Azure RMS, vous pouvez comparer Azure RMS à la version locale de Rights Management, les services AD RMS (Active Directory Rights Management Services). Pour une comparaison des fonctionnalités, des conditions requises et des contrôles de sécurité, consultez [Comparaison d’Azure Rights Management avec AD RMS](compare-azure-rms-ad-rms.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

