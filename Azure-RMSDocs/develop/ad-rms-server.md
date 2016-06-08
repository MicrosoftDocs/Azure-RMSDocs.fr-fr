---
# required metadata

title: Serveur AD RMS | Azure RMS
description: Le composant serveur de Rights Management Services (RMS) est implémenté par un ensemble de services web qui s’exécutent sur Microsoft Internet Information Services.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Ce contenu de SDK n’est pas à jour. Vous trouverez temporairement la [version actuelle](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentation sur MSDN. **

# Serveur AD RMS
Cette rubrique décrit l’objectif et les fonctions du serveur RMS.

Le composant serveur de Rights Management Services (RMS) est implémenté par un ensemble de services web qui s’exécutent sur [Microsoft Internet Information Services](http://www.iis.net/overview) (IIS). Vous pouvez également utiliser l’implémentation cloud via RMS sur Azure. Pour plus d’informations sur l’utilisation du service Azure Rights Management, consultez [Activer votre application de service pour le fonctionnement avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

Pour les serveurs locaux, depuis Windows Server 2008, vous pouvez installer et configurer le service RMS en l’ajoutant en tant que rôle. Pour installer le service sur les systèmes d’exploitation antérieurs, téléchargez-le à partir du Centre de téléchargement Microsoft : [Microsoft Windows Rights Management Services avec Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909).

Parmi les nombreux services web installés, ceux-ci sont importants pour le développement d’applications.

**Administration** : héberge le site web d’administration qui vous permet de gérer RMS. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences. Vous pouvez utiliser l’[API de script Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797) pour écrire des scripts d’administration.

**Certification de compte** : crée des certificats d’ordinateur qui identifient les ordinateurs dans la hiérarchie de certificats RMS, et des certificats de compte de droits qui associent des utilisateurs à des ordinateurs spécifiques. Pour plus d’informations, consultez [Activation d’un utilisateur](https://msdn.microsoft.com/library/Cc530378).

Ce service s’exécute sur le serveur de certification racine.

**Gestion des licences** : émet une licence d’utilisateur final qui permet aux utilisateurs finaux de consommer du contenu protégé. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.

**Publication** : crée une [licence d’émission](https://msdn.microsoft.com/library/Aa362355). Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.

**Précertification** : permet à un serveur demander un certificat de compte de droits pour le compte d’un utilisateur. Un certificat de compte de droits utilise le certificat d’ordinateur à partir de l’activation de RMS pour lier des comptes d’utilisateur à des ordinateurs ou des groupes d’ordinateurs spécifiques, et est utilisé pour permettre aux consommateurs d’utiliser du contenu protégé. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.

**Localisateur de service** : fournit l’URL des services de certification de compte, de gestion des licences et de publication à Active Directory, pour qu’ils puissent être détectés par les clients RMS. Le service s’exécute sur des serveurs de certification racine et sur des serveurs de licences.

 

## Rubriques connexes ##
* [Vue d'ensemble](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services avec Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [API de script Active Directory Rights Management Services](https://msdn.microsoft.com/library/Bb968797)
* [Activation d’un ordinateur](https://msdn.microsoft.com/library/Cc530377)
* [Activation d’un utilisateur](https://msdn.microsoft.com/library/Cc530378)
* [Création d’une licence d’émission](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Jun16_HO1-->


