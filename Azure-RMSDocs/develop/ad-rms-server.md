---
title: Serveur AD RMS | Azure RMS
description: Le composant serveur de Rights Management Services (RMS) est implémenté par un ensemble de services web qui s’exécutent sur Microsoft Internet Information Services.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: b396d65b821f258d08e867bad8331b8603d8ccb9
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "68788635"
---
# <a name="server"></a>Server (Serveur)

Cette rubrique décrit l’objectif et les fonctions du serveur RMS pour Azure et Windows Server.

**Azure RMS** - Pour plus d’informations sur l’utilisation du service Azure Rights Management, consultez [Activer votre application de service pour le fonctionnement avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

> [!IMPORTANT] 
> Nous vous recommandons de développer et tester votre application via Azure RMS.

**Windows Server** - Pour les serveurs locaux, depuis Windows Server 2008, vous pouvez installer et configurer le service RMS en l’ajoutant en tant que rôle. Pour installer le service sur les systèmes d’exploitation antérieurs, téléchargez-le à partir du Centre de téléchargement Microsoft : [Microsoft Windows Rights Management Services avec Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909).

Parmi les nombreux services web installés, ceux-ci sont importants pour le développement d’applications pour serveur RMS sur Windows Server.

| Service | Description |
|---------|-------------|
| Administration | Héberge le site web d’administration qui vous permet de gérer RMS. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences. Vous pouvez utiliser l’API de script Active Directory Rights Management Services pour écrire des scripts d’administration.|
| Certification de compte |Crée des certificats d’ordinateur qui identifient les ordinateurs dans la hiérarchie de certificats RMS, et des certificats de compte de droits qui associent des utilisateurs à des ordinateurs spécifiques. Pour plus d’informations, consultez Activation d’un ordinateur et Activation d’un utilisateur.<p><p>Ce service s’exécute sur le serveur de certification racine. |
|Licences | Émet une *licence utilisateur final*. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.|
|Visual Studio | Crée une *licence d’émission* qui définit les stratégies pouvant être énumérés dans une licence utilisateur final. Pour plus d’informations, consultez [Création d’une licence d’émission](https://msdn.microsoft.com/library/Aa362355).<p><p>Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.|
|Précertification | Permet à un serveur demander un *certificat de compte de droits* pour le compte d’un utilisateur. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.|
|Localisateur de service | Fournit l’URL des services de certification, de gestion des licences et de publication des comptes à Active Directory pour qu’ils puissent être détectés par les clients RMS. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.|

## <a name="related-topics"></a>Rubriques connexes ##
* [Vue d’ensemble](ad-rms-overview.md)
* [Microsoft Internet Information Services](https://www.iis.net/overview)
* [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services avec Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)
* [API de script Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Activation d’un ordinateur](https://msdn.microsoft.com/library/Cc530377)
* [Activation d’un utilisateur](https://msdn.microsoft.com/library/Cc530378)
* [Création d’une licence d’émission](https://msdn.microsoft.com/library/Aa362355)
