---
title: Client Azure Information Protection
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/19/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 59f79f7ac24a575665a2d8350f39b87aaedec7e1
ms.sourcegitcommit: 8558af7116f62414054feffa346aba197a1250d9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55559476"
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


## <a name="see-also"></a>Voir aussi
[Comparaison d’Azure Information Protection avec AD RMS](../compare-on-premise.md)
