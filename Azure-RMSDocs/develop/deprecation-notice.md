---
title: Avis de désapprobation kit de développement logiciel (SDK) RMS 4,2
description: Avis de désapprobation kit de développement logiciel (SDK) RMS 4,2
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
ms.date: 03/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: dbf96e317f70e41e76223cf6512eaa32427ff4c9
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844300"
---
# <a name="rms-sdk-42-deprecation-notice"></a>Avis de désapprobation kit de développement logiciel (SDK) RMS 4,2 

*Applicable à toutes les versions de kit de développement logiciel (SDK) RMS 4,2 antérieures au 2020 mars*

Le 3 mars, 2020, une mise à jour de la kit de développement logiciel (SDK) RMS 4,2 pour Android, iOS et OSX a été publiée via le centre de téléchargement Microsoft. Cette mise à jour est obligatoire pour toutes les applications qui utilisent actuellement ces plateformes de kit de développement logiciel (SDK) RMS.  

Depuis le 2021 janvier, les versions du kit de développement logiciel (SDK) RMS publiées avant le 1er mars 2020 ne pourront pas se connecter au point de terminaison du service Azure Rights Management. Les applications qui ne sont pas encore mises à jour ne peuvent pas établir de connexion TLS avec le service Azure Rights Management. 

## <a name="reason-for-change"></a>Motif de modification 

Les versions précédentes du kit de développement logiciel (SDK) RMS utilisent l’épinglage de certificat pour s’assurer que le client compatible RMS communique avec le service RMS, en recevant un certificat chaîné à une autorité de certification racine spécifique et attendue.  

Les navigateurs modernes utilisent les journaux de transparence des certificats pour vérifier que les certificats ont été émis pour des propriétaires de domaine légitimes et que ces certificats sont émis par des autorités de certification racines de confiance.  

Pour mieux prendre en charge les navigateurs modernes, le 1er décembre 2020, Microsoft mettra à jour le certificat de `https://api.aadrm.com` à un nouveau certificat émis par une autorité de certification racine de confiance mondiale qui signale des certificats émis pour les journaux de transparence des certificats approuvés par les navigateurs modernes. Une fois cette modification terminée, les versions héritées de kit de développement logiciel (SDK) RMS tentant d’effectuer un épinglage de certificat sur le certificat racine attendu ne parviendront pas à trouver ce certificat et ne pourront pas se connecter.  

## <a name="client-impact"></a>Impact sur le client 

Les applications Microsoft suivantes utilisent les kits de développement logiciel (SDK) RMS dès aujourd’hui. Des mises à jour ont été mises à disposition pour ces plateformes et les appareils doivent être mis à jour avant l’échéance du mois de décembre. 

- Office Pro plus/2019 pour Mac version 16,40 ou ultérieure.
- Office 2016 pour Mac version 16.16.27 ou ultérieure.
- Word, Excel et PowerPoint pour iOS version 2.40.20071600 ou ultérieure.
- Word, Excel et PowerPoint pour Android version 16.0.12827.20140 ou ultérieure.

Ressources 

- Android : https://www.microsoft.com/download/details.aspx?id=43673
- iOS : https://www.microsoft.com/download/details.aspx?id=43674 
- MacOS : https://www.microsoft.com/download/details.aspx?id=43675 
- Linux : https://azuread.github.io/rms-sdk-for-cpp/annotated.html
