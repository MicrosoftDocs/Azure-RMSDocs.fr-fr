---
title: Azure Information Protection l’historique des versions du client classique & la stratégie de support
description: Découvrez les nouveautés ou les modifications apportées dans une version du client Azure Information Protection Classic et comprenez la stratégie de cycle de vie du support.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/11/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9e03169c4c30bbad4ff9ed9ccaf06b6992994785
ms.sourcegitcommit: 99f1a1ab40eea7802e6c4f98724958409ee779ba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103558093"
---
# <a name="azure-information-protection-classic-client-version-release-history-and-support-policy"></a>Client Classic Azure Information Protection : historique de publication des versions et stratégie de support


>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Concerne :** [Azure information protection client classique pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez l' [historique des versions du client d’étiquetage unifié](unifiedlabelingclient-version-release-history.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

**Pour déployer le client classique AIP**, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. À l’exception de cette section, la documentation n’inclut pas d’informations sur les versions du client non prises en charge. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
|1.54.33.0 | 23/10/2019|
|1.53.10|07/15/2019|
|1.48.204.0|04/16/2019|
|1.41.51.0|27/11/2018|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|15/03/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|27/10/2016|
|1.1.23.0|10/01/2016|

Le format de date utilisé sur cette page est *mois/jour/année*.

À compter du 6/2/2019, le service d’étiquetage pour Azure Information Protection nécessite des connexions qui utilisent TLS 1,2.

Toutes les versions du client de 1.4.21.0 publiées 03/15/2017 prennent en charge TLS 1,2. Les versions clientes **1.3.155.2**, **1.2.4.0** et **1.1.23.0** n’utilisent pas TLS 1,2 et ne peuvent donc plus télécharger la stratégie de Azure information protection.

### <a name="release-history"></a>Historique des mises en production

Utilisez les informations suivantes pour découvrir les nouveautés ou les modifications apportées à une version prise en charge du client Azure Information Protection Classic pour Windows. La dernière version est répertoriée en première position.

Notez que les fonctionnalités de Azure Information Protection sont actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 

> [!NOTE]
>  Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).
>
## <a name="version-156250"></a>Version 1.56.25.0

**Publication**: 11/05/2020

**Pris en charge via**: 03/31/2021

Correctifs de bogues mineurs liés à la prise en charge d’Outlook.

## <a name="version-154590"></a>Version 1.54.59.0

**Publication**: 02/12/2020

**Pris en charge via**: 03/31/2021

Cette version comprend uniquement des correctifs.

**Correctifs** :

- Problème dans lequel les fichiers protégés par IQP affichent les options de **récupération** et/ou d' **enregistrement sous** après la suppression de la protection, sont résolus. 

- De nombreux textes d’info-bulles de fonctionnalités de produit ont été améliorés pour plus de clarté et de compréhension. 

- Les problèmes de stabilité du client lors de l’utilisation de fichiers PDF protégés sont résolus. 

- Les étiquettes de protection sont maintenant supprimées comme prévu si l’étiquette est supprimée de l’e-mail pendant le processus de création de l’e-mail. 

## <a name="next-steps"></a>Étapes suivantes

Vous ne savez pas s’il s’agit du bon client à installer ?  Consultez [choisir votre solution d’étiquetage Windows](use-client.md#choose-your-windows-labeling-solution).

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)
