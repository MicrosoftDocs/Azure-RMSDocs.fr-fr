---
title: Le client | Azure Information Protection
description: "Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ROBOTS: noindex,nofollow
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 70f10569884811b0b8dfab9b138399720ff48267


---

# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*S’applique à : Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- Le client peut être le client Azure Information Protection ou le client Rights Management, et s’intègre aux applications que vous exécutez sur des ordinateurs et appareils mobiles. 

- Le service réside dans le cloud (Azure Information Protection, qui utilise le service Azure Rights Management pour la protection des données) ou localement (Active Directory Rights Management Services). 

Le client Azure Information Protection prend en charge la classification et l’étiquetage, en plus de la protection. Ce client s’intègre aux applications Office et doit être installé séparément.

Le client Rights Management (RMS) est installé automatiquement avec certaines applications, telles que les applications Office, l’application de partage RMS et les applications d’éditeurs de logiciels compatibles avec RMS. Toutefois, il peut également être installé de manière autonome, par exemple quand des développeurs souhaitent intégrer la protection Rights Management à leurs applications métier ou quand des administrateurs ou des utilisateurs avec pouvoir souhaitent protéger en bloc des fichiers à l’aide de l’outil de protection RMS.

Consultez la documentation suivante si vous avez besoin de plus d’informations sur la façon de déployer et d’utiliser ces clients, qui peuvent être utilisés avec Azure Information Protection et Active Directory Rights Management Services pour aider à protéger les données de votre organisation :

- [Installation du client Azure Information Protection](info-protect-client.md)

- [Notes sur le déploiement du client RMS](client-deployment-notes.md)

- [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](configure-fci.md)

- [Application de partage Rights Management pour Windows](sharing-app-windows.md)


## <a name="see-also"></a>Voir aussi
[Comparaison d’Azure Information Protection avec AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)



<!--HONumber=Nov16_HO2-->


