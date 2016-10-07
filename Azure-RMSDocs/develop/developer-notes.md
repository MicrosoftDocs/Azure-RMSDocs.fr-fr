---
title: "Guide et informations pour développeurs | Azure RMS"
description: "Cette rubrique traite de recommandations propres à différents scénarios de développement importants."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: d7e718c2e982702bef16c242370771d991b29db9


---

# Guide et informations pour développeurs

Cette section traite de recommandations spécifiques pour plusieurs scénarios de développement importants, ainsi que des informations générales sur le développement avec ce SDK. Les scénarios de cette section sont spécifiques à cette version du SDK Rights Management Services 2.1 et peuvent être modifiés dans les versions ultérieures.
- [Comment : utiliser l’authentification ADAL](how-to-use-adal-authentication.md) - Authentification auprès d’Azure RMS pour votre application à l’aide de la bibliothèque d’authentification ADAL (Azure Active Directory Authentication Library).
- [Comment : ajouter des droits de propriétaire explicites](add-explicit-owner-rights.md) - Votre application doit ajouter explicitement des droits &quot;Propriétaire&quot; lors de la création d’une licence ex nihilo ([IpcCreateLicenseFromScratch](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Comment : déboguer une application avec gestion des droits](debugging-applications-that-use-ad-rms.md) - Cette rubrique indique comment déboguer votre application et utiliser le journal des événements Windows.
- [Comment : activer le suivi et la révocation des documents](tracking-content.md) - Cette rubrique décrit les instructions de base pour implémenter le suivi des documents pour le contenu ainsi que l’exemple de code pour les mises à jour de métadonnées et la création d’un bouton **Suivre l'utilisation** pour votre application.
- [Comment : activer les notifications par e-mail](how-to-enable-email-notification.md) - Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.
- [Comment : permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md) - Cette rubrique décrit les étapes permettant de configurer votre application de service pour qu’elle utilise Azure Rights Management.
- [Comment : installer et configurer un serveur RMS](how-to-install-and-configure-an-rms-server.md) - Cette rubrique décrit les étapes de connexion à un serveur RMS ou à Azure RMS à des fins de test de votre application avec gestion des droits.
- [Comment : définir le mode de sécurité de l’API](setting-the-api-security-mode-api-mode.md) - Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Comment : utiliser des paramètres de chiffrement](working-with-encryption.md) - Cette rubrique vous oriente vers nos offres de chiffrement et présente quelques extraits de code pour illustrer leur utilisation.
- [Types d’applications](application-types.md) : cette rubrique traite des types d’applications que vous pouvez choisir de créer avec une gestion des droits.
- [Configuration de l’API de fichier](file-api-configuration.md) - Le comportement de l’API de fichier peut être configuré via des paramètres du Registre.
- [Formats de fichier pris en charge](supported-file-formats.md) - L’API de fichier prend en charge les formats natif et Pfile.
- [Plateformes prises en charge](supported-platforms.md) - Cette rubrique identifie les plateformes client et serveur prises en charge par RMS SDK 2.1.
- [Comprendre les restrictions d’utilisation](understanding-usage-restrictions.md) : toutes les applications activées pour RMS doivent appliquer des restrictions d’utilisation.
- [Informations de référence sur les restrictions d’utilisation](usage-restriction-reference.md) - Les restrictions d’utilisation sont définies par les constantes répertoriées dans cette rubrique.

 
## Rubriques connexes ##
* [Vue d'ensemble](ad-rms-overview.md)
 

 



<!--HONumber=Sep16_HO5-->


