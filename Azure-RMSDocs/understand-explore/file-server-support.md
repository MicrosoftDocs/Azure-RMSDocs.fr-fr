---
# required metadata

title: Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF) | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)

*S’applique à : Azure Rights Management, Office 365*


Quand vous configurez Windows Server pour utiliser l’infrastructure de classification des fichiers, la fonctionnalité Outils de gestion de ressources pour serveur de fichiers (FSRM) peut analyser les fichiers locaux pour déterminer s’ils contiennent des données sensibles. Quand les fichiers répondent à ces critères, ils sont balisés avec des propriétés de classification définies par un administrateur. L’infrastructure de classification des fichiers peut effectuer automatiquement une action, selon la classification. L’une de ces actions inclut l’application de la protection des informations via [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] et le déploiement du connecteur Rights Management (également appelé connecteur RMS). Les fichiers Office sont alors automatiquement protégés par Azure RMS.

Pour protéger tous les types de fichiers, au lieu d’utiliser le connecteur RMS, exécutez un script Windows PowerShell à l’aide des applets de commande de l’[outil de protection RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256).

Les stratégies de classification sont entièrement configurables et très extensibles pour vous permettre d’empêcher d’éventuelles fuites de données par des utilisateurs autorisés ou non autorisés. L’outil de protection peut même contribuer à réduire le risque de fuite de données dues aux administrateurs réseau, car vous pouvez configurer des stratégies qui n’exigent pas que ceux-ci aient accès aux fichiers.

Pour obtenir des instructions relatives au déploiement et à la configuration du connecteur RMS pour les fichiers Office, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

Pour savoir comment utiliser le script Windows PowerShell pour tous les types de fichiers, consultez [Protection RMS avec l’infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](../rms-client/configure-fci.md).



## Étapes suivantes
À présent que vous savez comment les applications et services prennent en charge Azure RMS, vous pouvez comparer Azure RMS à la version locale de Rights Management, les services AD RMS (Active Directory Rights Management Services). Pour obtenir une comparaison des fonctionnalités et pour plus de détails sur les conditions requises et les contrôles de sécurité, consultez [Comparaison d’Azure Rights Management avec AD RMS](compare-azure-rms-ad-rms.md).




<!--HONumber=Apr16_HO4-->


