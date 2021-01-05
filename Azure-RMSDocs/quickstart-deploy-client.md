---
title: Démarrage rapide - Déploiement du client d’étiquetage unifié Azure Information Protection
description: Introduction rapide au déploiement du client d’étiquetage unifié Azure Information Protection (AIP)
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 468cbe031b22ba07127b75295da98ee9a081048a
ms.sourcegitcommit: 73befea74644d272e2d8d1d4b95df55c7741ccbe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97762330"
---
# <a name="quickstart-deploying-the-azure-information-protection-aip-unified-labeling-client"></a>Démarrage rapide : Déploiement du client d’étiquetage unifié Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne** : [Client d’étiquetage unifié Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Le client d’étiquetage unifié Azure Information Protection (AIP) fait partie de la solution [Microsoft Information Protection](https://aka.ms/MIPdocs) et étend les fonctionnalités intégrées pour l’étiquetage de la sensibilité fournies par Microsoft 365. 

Le client assure la prise en charge de l’étiquetage et de la protection pour l’utilisateur final dans l’Explorateur de fichiers et PowerShell, en plus des applications Office. L’analyseur fourni avec le client d’étiquetage unifié permet aux administrateurs d’analyser les réseaux et les partages de contenu à la recherche de contenu sensible. 

Pour les organisations sans plateforme de protection des informations, le client fournit une visionneuse pour le contenu protégé par d’autres organisations utilisant Microsoft Information Protection.

## <a name="review-aip-client-prerequisites"></a>Passer en revue les prérequis du client Azure Information Protection

Utilisez les articles en lien ci-dessous pour mieux comprendre les prérequis pour le déploiement de l’étiquetage unifié Azure Information Protection dans votre organisation :

- **[Exigences d’Azure Information Protection](requirements.md)** . Décrit la configuration système requise détaillée pour le déploiement du client AIP dans votre organisation, par exemple un abonnement Azure Information Protection et Azure Active Directory. Liste également les appareils clients pris en charge et les applications prises en charge.

- **[Exigences du client d’étiquetage unifié](./rms-client/reqs-ul-client.md)** . Décrit la configuration requise pour chaque machine où le client AIP est installé.

## <a name="install-the-aip-client"></a>Installer le client AIP

AIP fournit les options d’installation du client suivantes :

- **[Télécharger et exécuter le fichier .exe.](rms-client/clientv2-admin-guide-install.md#install-the-aip-unified-labeling-client-using-the-executable-installer)** Cette installation est l’option recommandée pour la plupart des cas d’usage. L’installation peut être exécutée de façon interactive ou silencieuse.

    Une fois l’installation terminée, vous pouvez être invité à redémarrer votre ordinateur ou votre logiciel Office. Redémarrez si nécessaire pour continuer.

- **[Télécharger et exécuter le fichier .msi.](rms-client/clientv2-admin-guide-install.md#install-the-unified-labeling-client-using-the-msi-installer)** Prise en charge pour les installations en mode silencieux qui utilisent un mécanisme de déploiement central, comme des stratégies de groupe, Configuration Manager ou Microsoft Intune.

Les fichiers d’installation du client AIP sont disponibles auprès du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 

Pour plus d’informations, consultez [Guide de l’administrateur : Installation du client d’étiquetage unifié Azure Information Protection pour les utilisateurs](rms-client/clientv2-admin-guide-install.md).

> [!TIP]
> Pour tester et exécuter les dernières fonctionnalités disponibles pour le client AIP, déployez notre préversion publique sur un système de test. Pour plus d’informations, consultez l’[historique des versions](rms-client/unifiedlabelingclient-version-release-history.md) du client d’étiquetage unifié AIP.
> 

## <a name="next-steps"></a>Étapes suivantes

Consultez les tutoriels et guides de démarrage rapide suivants pour commencer à utiliser le client Azure Information Protection :

- [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection](tutorial-install-scanner.md)
- [Tutoriel : Découverte de votre contenu sensible avec le scanneur Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Tutoriel : Empêcher les partages inappropriés avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md) 

**Voir aussi** :

- [Problèmes connus - Azure Information Protection](known-issues.md) 
- [Forum aux questions sur Azure Information Protection](faqs.md) 
- [Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md)        
    
