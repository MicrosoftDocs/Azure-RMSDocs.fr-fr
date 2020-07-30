---
title: Instructions pour Azure Information Protection des scénarios courants
description: Identifiez les cas d’usage qui classent et protègent les données de votre organisation à l’aide de Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6308234bb778969c8e5d3b8e55260f042e501906
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298221"
---
# <a name="how-to-guides-for-common-scenarios-that-use-azure-information-protection"></a>Guides pratiques pour les scénarios courants qui utilisent Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Il existe de nombreux scénarios dans lesquels vous pouvez utiliser Azure Information Protection pour classer et, le cas échéant, protéger les documents et e-mails de votre organisation. 

Les déploiements les plus performants sont ceux qui identifient des cas d’utilisation spécifiques qui offrent le plus d’avantages à l’organisation. Utilisez la liste suivante de scénarios courants et d’instructions pour optimiser votre déploiement.

## <a name="common-scenarios"></a>Scénarios courants

|Scénario : je souhaite...|Instructions|
|----------------|---------------|
|Identifier les informations sensibles stockées localement par mon entreprise|[Démarrage rapide : Rechercher les informations sensibles dans des fichiers stockés localement](quickstart-findsensitiveinfo.md)|
|Aider les utilisateurs à protéger leurs e-mails contenant des informations sensibles|[Démarrage rapide : Configurer une étiquette pour permettre aux utilisateurs de protéger facilement les e-mails qui contiennent des informations sensibles](quickstart-label-dnf-protectedemail.md)|
|Aider les utilisateurs à classer les données qu’ils ont créées ou modifiées, et à les protéger si elles contiennent des informations sensibles| [Tutoriel : Modifier la stratégie et créer une nouvelle étiquette](infoprotect-quick-start-tutorial.md)|
|Aider les utilisateurs à collaborer sur un document protégé|[Configuration d’une collaboration sécurisée autour de documents à l’aide d’Azure Information Protection](secure-collaboration-documents.md)|
|Protéger automatiquement les e-mails des utilisateurs qui sont envoyés en dehors de l’organisation| [Configuration des règles de flux de messagerie pour les étiquettes Azure Information Protection](configure-exo-rules.md)
|Classer et protéger automatiquement les données existantes dans mes banques de données locales|[Déploiement du scanneur Azure Information Protection](deploy-aip-scanner.md)|
|Utiliser ma propre clé pour protéger les données de mon organisation| [Planification et implémentation de la clé de client](plan-implement-tenant-key.md)|
|Migrer à partir d’AD RMS|[Migration depuis AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)|

## <a name="additional-deployment-instructions"></a>Instructions de déploiement supplémentaires

Notre [blog technique Azure information protection](https://aka.ms/AIPblog) comprend des conseils supplémentaires dans les trancheuses.

Par exemple, une méthodologie avec les meilleures pratiques pour les décideurs d’entreprise et les responsables de l’implémentation informatique :

- [Guide d’accélération du déploiement d’Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Deployment-Acceleration-Guide/ba-p/334423)

Instructions pas à pas :

- [Comment créer un portail de suivi AIP personnalisé](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-Build-a-Custom-AIP-Tracking-Portal/ba-p/875849)

- [Créez des rapports plus riches avec Microsoft Information Protection et Azure AD les données de connexion](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Create-richer-reports-with-Microsoft-Information-Protection-and/ba-p/392713)

- [Tirez parti de Microsoft Cloud App Security pour appliquer des étiquettes Azure Information Protection dans le Cloud](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Leverage-Microsoft-Cloud-App-Security-to-apply-Azure-Information/ba-p/388638)

- [Comment préparer un plan de « sortie Cloud » Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631)

- [Visualisation des étiquettes entre locataires](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cross-Tenant-Label-Visualization/ba-p/356588)

- [Using Azure Information Protection to protect PDF’s and Adobe Acrobat Reader to view them](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Using-Azure-Information-Protection-to-protect-PDF-s-and-Adobe/ba-p/282010)

- [Cataloging your Sensitive Data with AIP, Even Before Configuring Labels!](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Cataloging-your-Sensitive-Data-with-AIP-Even-Before-Configuring/ba-p/267241)

- [Azure Information Protection Scanner Express Installation](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-Scanner-Express-Installation/ba-p/265424)

- [Discovery of Sensitive Data Using the AIP Scanner (AIP Premium P1)](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discovery-of-Sensitive-Data-Using-the-AIP-Scanner-AIP-Premium-P1/ba-p/252040)

## <a name="next-steps"></a>Étapes suivantes

Votre scénario n’est pas répertorié ? Pour obtenir la liste complète des étapes de planification et de déploiement, consultez les [feuilles de route](deployment-roadmap.md) pour le déploiement.

Si vous débutez avec Azure Information Protection, consultez [Qu’est-ce qu’Azure Information Protection ?](what-is-information-protection.md) pour une présentation rapide du service avant de commencer votre déploiement.
