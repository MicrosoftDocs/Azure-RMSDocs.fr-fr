---
title: Client Azure Information Protection
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8fe14ef040b00e2f54f535be2927efd7284a5287
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148271"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- Le client peut être le client Azure Information Protection ou le client Rights Management, et s’intègre aux applications que vous exécutez sur des ordinateurs et appareils mobiles. 

- Le service réside dans le cloud (Azure Information Protection, qui utilise le service Azure Rights Management pour la protection des données) ou localement (Active Directory Rights Management Services). 

Le client Azure Information Protection prend en charge la classification et l’étiquetage, en plus de la protection. Ce client s’intègre aux applications Office et doit être installé séparément.

Le client Rights Management (RMS) est installé automatiquement avec certaines applications, telles que les applications Office, le client Azure Information Protection, et les applications d’éditeurs de logiciels compatibles avec RMS. Toutefois, il peut également être installé de manière autonome, par exemple quand des développeurs souhaitent intégrer la protection Rights Management aux applications métier.

Consultez la documentation suivante si vous avez besoin de plus d’informations sur la façon de déployer et d’utiliser ces clients, qui peuvent être utilisés avec Azure Information Protection et Active Directory Rights Management Services pour aider à protéger les données de votre organisation :

- [Client Azure Information Protection](AIP-client.md)

- [Notes sur le déploiement du client RMS](client-deployment-notes.md)

- [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](configure-fci.md)

- [Application de partage Rights Management pour Windows](sharing-app-windows.md)

L’application de partage de Rights Management pour Windows et l’outil de protection RMS sont désormais remplacés par le client Azure Information Protection. 


## <a name="see-also"></a>Voir aussi
[Comparaison d’Azure Information Protection avec AD RMS](../compare-on-premise.md)
