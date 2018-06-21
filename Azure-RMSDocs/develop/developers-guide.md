---
title: Guide du développeur Azure Information Protection
description: Les développeurs peuvent utiliser Azure Information Protection pour protéger et gérer des fichiers de tout type
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: a32f4d774b67007ccc6638e3151bd6038e3f274c
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
ms.locfileid: "27765525"
---
# <a name="azure-information-protection-developers-guide"></a>Guide du développeur Azure Information Protection

Ce guide vous présente les outils permettant de développer et intégrer le service de gestion des droits d’Azure Informations Protection.

>Le SDK Azure Information Protection actuel inclut le composant de gestion des droits. Un composant de classification et d’étiquetage est en cours de développement.

## <a name="service-applications"></a>Applications de service

Les applications de service proposent des fonctionnalités pour protéger les informations lors de leur exportation à partir d’un système de gestion de contenu d’entreprise, d’une application métier ou d’une solution métier cloud. Les applications Data Loss Prevention (DLP) et Cloud Application Security (CAS) sont des exemples d’applications de service. Notre SDK pour le développement d’applications de service est disponible par le biais de deux modèles de programmation.

- [C++](https://www.microsoft.com/download/details.aspx?id=38397)
- [API managée C#](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>Exemples d’applications de service

- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple d’application DLP compatible RMS qui décrit les étapes de base que chaque application DLP compatible RMS doit effectuer à l’aide de l’API de fichier RMS pour protéger et consommer du contenu limité.
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple qui montre comment utiliser le SDK RMS dans des applications Azure pour protéger des données dans un Stockage Blob Azure.
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un exemple qui montre comment générer une application Windows qui surveille des répertoires du système de fichiers et applique des stratégies de protection RMS lors de chaque modification, par exemple en cas d’ajout ou de modification de fichier.
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) est un exemple d’application de console simple qui prend un répertoire en tant qu’entrée et protège tous les fichiers dans ce répertoire uniquement, sans récursivité.

## <a name="powershell-guides"></a>Guides PowerShell

Généralement utilisées par les administrateurs Azure Rights Management, les applets de commande PowerShell s’avèrent également utiles pour développer et tester vos applications de service. Pour plus d’informations, consultez [Utilisation de PowerShell avec le client Azure Information Protection](/information-protection/rms-client/client-admin-guide-powershell).

## <a name="user-applications"></a>Applications utilisateur

Les applications utilisateur peuvent être développées avec le SDK RMS 2.1 ou le SDK RMS 4.2.
La version 4.2 est un client REST avec des API spécifiques de plusieurs systèmes d’exploitation courants comme iOS/OSX, Android, Linux, Windows. La version 2.1 est utilisée pour développer des applications Windows natives.

### <a name="user-application-development-guides"></a>Guides de développement d’applications utilisateur

- [Développement de votre application](developing-your-application.md)
- [Test de votre application](how-to-set-up-your-test-environment.md)
- [Déploiement de votre application](deploying-your-application.md)

### <a name="user-application-samples"></a>Exemples d’applications utilisateur

- [AzureIP Test](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) est un exemple d’application console qui vous permet de chiffrer des documents avec un modèle Azure ou une stratégie ad hoc.
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) est un exemple d’application compatible RMS qui décrit les étapes de base que chaque application compatible RMS doit effectuer lors de la protection et de la consommation de contenu limité.
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) est un outil qui peut fournir des informations sur n’importe quel fichier protégé par RMS, telles que l’ID de contenu ou les droits d’utilisateur.

## <a name="development-environment-setup"></a>Installation de l’environnement de développement

Les guides suivants vous orientent tout au long des étapes d’installation du système d’exploitation d’un environnement de développement d’applications qui utilise des outils courants.

[![Installation iOS/OSX](../media/develop/ios-icon.png)](ios-sdk.md)
[![Installation Android](../media/develop/android-icon.png)](android-sdk.md)
[![Installation Windows Phone](../media/develop/windows-phone-icon.png)](windows-phone-apps.md)
[![Installation Windows Service](../media/develop/windows-icon.png)](install-the-rms-sdk.md)
[![Installation Linux](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>Guides pratiques

Chacune des rubriques suivantes présente les instructions spécifiques d’un aspect de l’implémentation de votre application. Les applications de service sont développées à l’aide du SDK RMS 2.x. Les applications utilisateur sont développées à l’aide du SDK RMS 4.x. Le lien de l’article est attribué avec le type d’application, le service, l’utilisateur.

### <a name="general"></a>Général

- [Guide pratique pour activer le suivi et la révocation de documents (service)](tracking-content.md)
- [Guide pratique pour déployer votre client](../rms-client/client-deployment-notes.md)
- [Comment déployer votre application de service sur un autre locataire] (how-to-deploy-app.md)
- [Guide pratique pour installer et configurer un serveur RMS (service)](how-to-install-and-configure-an-rms-server.md)
- [Guide pratique pour utiliser le suivi de documents (utilisateur)](how-to-use-document-tracking.md)
- [Guide pratique pour renouveler une clé symétrique dans Azure Information Protection](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>Sécurité et authentification

- [Guide pratique pour configurer votre application de service pour utiliser une connexion Azure Active Directory](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)
- [Guide pratique pour utiliser l’authentification Active Directory Azure (ADAL)](how-to-use-adal-authentication.md)
- [Configuration d’Azure RMS pour l’authentification (service)](adal-auth.md)
- [Guide pratique pour définir le mode de sécurité de l’API (service)](setting-the-api-security-mode-api-mode.md)
- [Permettre à vos applications d’utiliser Azure RMS (service)](how-to-use-file-api-with-aadrm-cloud.md)
- [Guide pratique pour inscrire et activer votre application RMS dans Azure AD (utilisateur)](authentication-integration.md)

### <a name="configuration-and-performance-management"></a>Configuration et gestion des performances

- [Guide pratique pour ajouter des droits de propriétaire explicites (service)](add-explicit-owner-rights.md)
- [Configuration de l’API de fichier (service)](file-api-configuration.md)
- [Guide pratique pour utiliser des droits intégrés (utilisateur)](built-in-rights-usage-restriction-reference.md)
- [Guide pratique pour activer la journalisation des erreurs et des performances (utilisateur)](enabling-logging.md)

## <a name="introduction-and-datasheets"></a>Introduction et feuilles de données

[Présentation d’Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)

## <a name="other-resources"></a>Autres ressources

- [Guide des bonnes pratiques en matière de sécurité](security-guidelines.md)
- [Blog Coin du développeur RMS](https://blogs.msdn.microsoft.com/rms/)
- [Forum aux questions sur Azure Information Protection](https://docs.microsoft.com/information-protection/get-started/faqs)

### <a name="support-articles"></a>Articles sur la prise en charge

- [Formats de fichier pris en charge](supported-file-formats.md)
- [Plateformes prises en charge](supported-platforms.md)
- [Comprendre les restrictions d’utilisation](understanding-usage-restrictions.md)

### <a name="message-protocol-and-file-formats"></a>Protocole de message et formats de fichiers

- [Protocole client vers serveur](https://msdn.microsoft.com/library/cc243191.aspx)
- [Protocole d’objet e-mail géré par des droits](https://msdn.microsoft.com/library/cc463909(v=EXCHG.80).aspx)
- [Format de fichier binaire de fichier composé](https://msdn.microsoft.com/library/dd942138.aspx)

#### <a name="rights-managed-email-message"></a>E-mail géré par des droits

- [Format de fichier .MSG (partie 1)](https://blogs.msdn.microsoft.com/openspecification/2009/11/06/msg-file-format-part-1/)
- [Format de fichier .MSG (partie 2)](https://blogs.msdn.microsoft.com/openspecification/2010/06/20/msg-file-format-rights-managed-email-message-part-2/)

### <a name="api-reference"></a>Informations de référence sur les API

- [Informations de référence sur l’API Windows](https://msdn.microsoft.com/library/hh535292.aspx)
  - [Codes d’erreur du SDK Windows](https://msdn.microsoft.com/library/hh535248.aspx)
- [Informations de référence sur les API du Windows Store et de Windows Phone](https://msdn.microsoft.com/library/dn891914.aspx)
- [Informations de référence sur les API iOS/OSX](https://msdn.microsoft.com/library/dn758306.aspx)
- [Informations de référence sur les API Android](https://msdn.microsoft.com/library/dn758245.aspx)
- [Référence d’API Linux](http://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>Versions précédentes

- Le [SDK AD RMS](https://msdn.microsoft.com/library/cc530379.aspx) est la première version du SDK RMS.
- L’[Outil de script AD RMS](https://msdn.microsoft.com/library/bb968797.aspx) est un outil administratif pour une installation AD RMS.

### <a name="see-also"></a>Voir aussi

- [Terminologie du développeur](terms.md)
- [Terminologie liée à Azure Information Protection - ITPro](../get-started/terminology.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
