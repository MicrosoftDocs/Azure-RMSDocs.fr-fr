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
ms.openlocfilehash: 51af06c37e6ee23a762f35791b0796b93b52e83b
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/10/2020
ms.locfileid: "84665807"
---
# <a name="rms-sdk-42-deprecation-notice"></a>Avis de désapprobation kit de développement logiciel (SDK) RMS 4,2 

*Applicable à toutes les versions de kit de développement logiciel (SDK) RMS 4,2 antérieures au 2020 mars*

Le 3 mars, 2020, une mise à jour de la kit de développement logiciel (SDK) RMS 4,2 pour Android, iOS et OSX a été publiée par le biais du centre de téléchargement Microsoft. Cette mise à jour est obligatoire pour toutes les applications qui utilisent actuellement ces plateformes de kit de développement logiciel (SDK) RMS.  

Le mardi 15 septembre, 2020 versions de l’kit de développement logiciel (SDK) RMS publiées avant le 1er mars 2020 ne pourront pas se connecter au point de terminaison du service Azure Rights Management. Les applications qui consomment kit de développement logiciel (SDK) RMS 4,2 doivent être mises à jour avant cette date. 

## <a name="reason-for-change"></a>Motif de modification 

Les versions précédentes du kit de développement logiciel (SDK) RMS utilisent l’épinglage de certificat pour s’assurer que le client compatible RMS communique avec le service RMS, en recevant un certificat chaîné à une autorité de certification racine spécifique et attendue.  

Les navigateurs modernes utilisent les journaux de transparence des certificats pour vérifier que les certificats ont été émis pour des propriétaires de domaine légitimes et que ces certificats sont émis par des autorités de certification racines de confiance.  

Pour mieux prendre en charge les navigateurs modernes, le 15 septembre 2020, Microsoft mettra à jour le certificat de `https://api.aadrm.com` à un nouveau certificat émis par une autorité de certification racine de confiance mondiale qui signale des certificats émis pour les journaux de transparence des certificats approuvés par les navigateurs modernes. Une fois cette modification terminée, les versions héritées de kit de développement logiciel (SDK) RMS tentant d’effectuer un épinglage de certificat sur le certificat racine attendu ne parviendront pas à trouver ce certificat et ne pourront pas se connecter.  

## <a name="client-impact"></a>Impact sur le client 

Les applications Microsoft suivantes utilisent les kits de développement logiciel (SDK) RMS dès aujourd’hui. Des mises à jour seront mises à disposition pour ces plateformes et les appareils doivent être mis à jour avant l’échéance du septembre. 

- Office 2019 pour Mac 
- Office 2016 pour Mac 
- Word, Excel et PowerPoint pour iOS 
- Word, Excel et PowerPoint pour Android 

Ressources 

- Android : https://www.microsoft.com/download/details.aspx?id=43673
- Libéréhttps://www.microsoft.com/download/details.aspx?id=43674 
- MacOS : https://www.microsoft.com/download/details.aspx?id=43675 
- Linux : https://azuread.github.io/rms-sdk-for-cpp/annotated.html