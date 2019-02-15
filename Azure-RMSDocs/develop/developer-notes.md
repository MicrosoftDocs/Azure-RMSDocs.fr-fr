---
title: Guide pour développeurs de l'Azure Information Protection SDK 2.1 | Microsoft Docs
description: Une collection de rubriques de procédures pour développer avec l'AIP SDK 2.1
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c6f20fe10580e5dc6dd56912e53b878940598f3a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255884"
---
# <a name="developer-guidance"></a>Guide pour développeurs

Cette section traite de recommandations spécifiques pour plusieurs scénarios de développement importants, ainsi que des informations générales sur le développement avec ce SDK. Les scénarios de cette section sont spécifiques à cette version du SDK Rights Management Services 2.1 et peuvent être modifiés dans les versions ultérieures.
- [Comment : utiliser l’authentification ADAL](how-to-use-adal-authentication.md) - Authentification auprès d’Azure RMS pour votre application à l’aide de la bibliothèque d’authentification ADAL (Azure Active Directory Authentication Library).
- [Guide pratique pour ajouter des droits de propriétaire explicites](add-explicit-owner-rights.md) : votre application doit ajouter explicitement des droits « Propriétaire » lors de la création d’une licence ex nihilo ([IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)).
- [Comment : déboguer une application avec gestion des droits](debugging-applications-that-use-ad-rms.md) - Cette rubrique indique comment déboguer votre application et utiliser le journal des événements Windows.
- [Comment déployer une application dans un locataire du client](how-to-deploy-app.md) - Cette rubrique souligne les étapes nécessaires au déploiement d’une application depuis son locataire Azure AD de développement dans un locataire Azure AD de production.
- [Comment : activer le suivi et la révocation des documents](tracking-content.md) - Cette rubrique décrit les instructions de base pour implémenter le suivi des documents pour le contenu ainsi que l’exemple de code pour les mises à jour de métadonnées et la création d’un bouton **Suivre l'utilisation** pour votre application.
- [Comment : activer les notifications par e-mail](how-to-enable-email-notification.md) - Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.
- [Comment : permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md) - Cette rubrique décrit les étapes permettant de configurer votre application de service pour qu’elle utilise Azure Rights Management.
- [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md) - Cette rubrique décrit les étapes de connexion à un serveur RMS ou à Azure RMS à des fins de test de votre application avec gestion des droits.
- [Comment : définir le mode de sécurité de l’API](setting-the-api-security-mode-api-mode.md) - Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).
- [Comment : utiliser des paramètres de chiffrement](working-with-encryption.md) - Cette rubrique vous oriente vers nos offres de chiffrement et présente quelques extraits de code pour illustrer leur utilisation.
- [Types d’applications](application-types.md) : cette rubrique traite des types d’applications que vous pouvez choisir de créer avec une gestion des droits.
- [Configuration de l’API de fichier](file-api-configuration.md) - Le comportement de l’API de fichier peut être configuré via des paramètres du Registre.
- [Instructions de sécurité](security-guidelines.md) : fournit aux développeurs d’applications toutes les instructions et tous les conseils nécessaires pour travailler correctement dans l’écosystème AIP.
- [Formats de fichier pris en charge](supported-file-formats.md) - L’API de fichier prend en charge les formats natif et Pfile.
- [Plateformes prises en charge](supported-platforms.md) - Cette rubrique identifie les plateformes client et serveur prises en charge par RMS SDK 2.1.
- [Comprendre les restrictions d’utilisation](understanding-usage-restrictions.md) : toutes les applications compatibles RMS doivent appliquer des restrictions d’utilisation définies par les constantes répertoriées dans cette rubrique.

 
## <a name="related-topics"></a>Rubriques connexes
* [Vue d'ensemble](ad-rms-overview.md)
