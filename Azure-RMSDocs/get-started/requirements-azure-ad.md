---
title: "Configuration d’Azure Active Directory requise pour AIP"
description: "Identifiez la configuration requise d’Azure AD pour utiliser Azure Information Protection afin de permettre l’authentification des utilisateurs."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 29bc3b414a1fde17aec03702a87f4364b565b848
ms.sourcegitcommit: 65e2d607954dfb6c7529ff200602887b71c39312
translationtype: HT
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Configuration requise d’Azure Active Directory pour Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez besoin d’un annuaire Azure AD pour utiliser Azure Information Protection. Vous devez utiliser le compte de votre organisation correspondant à cet annuaire pour vous connecter au portail Azure Classic, où vous pouvez, par exemple, configurer et gérer les modèles Rights Management.

Si vous n’avez pas d’abonnement Azure pour votre organisation, vous pouvez en obtenir un en vous inscrivant pour une évaluation gratuite. Consultez la page [Bien démarrer avec Azure](https://account.windowsazure.com/organization) et suivez les instructions.

Pour plus d’informations, consultez les ressources suivantes dans la documentation Azure Active Directory :

-   [Qu’est-ce qu’Azure AD Directory ?](/active-directory/active-directory-whatis)

-   [Comment les abonnements Azure sont-ils associés à Azure Active Directory ?](/active-directory/active-directory-how-subscriptions-associated-directory)

Si vous souhaitez intégrer votre annuaire Azure AD à vos forêts AD locales, consultez [Intégration de vos identités locales avec Azure Active Directory](/active-directory/active-directory-aadconnect).

### <a name="scenarios-that-have-specific-requirements"></a>Scénarios avec des exigences spécifiques 

Ordinateurs qui exécutent Office 2010 : 

- Ces ordinateurs nécessitent le [client Azure Information Protection](../rms-client/aip-client.md) (recommandé) ou [l’application de partage Rights Management pour Windows](../rms-client/sharing-app-windows.md) pour s’authentifier auprès d’Azure Information Protection et de son service de protection des données, Azure Rights Management.

- Si vos comptes d’utilisateur sont fédérés (par exemple, si vous utilisez AD FS), ils doivent utiliser l’authentification intégrée de Windows. L’authentification basée sur les formulaires dans ce scénario ne peut pas authentifier les utilisateurs pour Azure Information Protection.

Prise en charge de l’authentification basée sur les certificats :

- L’application Azure Information Protection pour Android prend en charge l’authentification basée sur les certificats quand vous avez Android 5.0 ou ultérieur. Pour des instructions sur la configuration de l’authentification basée sur les certificats, consultez [Bien démarrer avec l’authentification basée sur les certificats dans Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

Appareils mobiles ou ordinateurs Mac qui s’authentifient localement par le biais des services AD FS ou d’un fournisseur d’authentification équivalent :

- Vous devez utiliser les services AD FS sur la version serveur minimale de **Windows Server 2012 R2** ou un autre fournisseur d’authentification prenant en charge le protocole OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Authentification multifacteur (MFA) et Azure Information Protection
Pour utiliser l’authentification multifacteur (MFA) avec Azure Information Protection, vous devez avoir au moins l’un des éléments suivants :

-   Office 2013 (version minimale) :

    -   Si vous avez Office 2013, il peut être nécessaire d’installer une mise à jour supplémentaire pour prendre en charge Active Directory Authentication Library (ADAL). Par exemple, la [mise à jour pour Office 2013 (KB3054853) du 9 juin 2015](https://support.microsoft.com/kb/3054853). Pour plus d’informations sur cette mise à jour et la manière dont l’authentification moderne introduit la connexion basée sur Azure Active Directory Authentication Library (ADAL) à Office 2013, consultez [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sur le blog Office.

- Client Azure Information Protection :

    - Le [client Azure Information Protection](../rms-client/aip-client.md) pour Windows et pour iOS et Android a toujours pris en charge l’authentification MFA ; aucune version minimale n’est requise. 

-   Application de partage Rights Management pour Windows :

    -   Vous devez avoir installé la version minimale 1.0.1908.0, ce que vous pouvez vérifier dans la rubrique Programmes et fonctionnalités du Panneau de configuration. L’application de partage de Rights Management est désormais remplacée par le client Azure Information Protection. Pour plus d’informations sur l’application de partage, consultez [Application de partage Rights Management pour Windows](../rms-client/sharing-app-windows.md).

-   Application de partage Rights Management pour appareils mobiles et ordinateurs Mac :

    -   Assurez-vous d’avoir installé la dernière version. La prise en charge de MFA a été introduite dans la version de septembre 2015 de l’application de partage RMS.

Ensuite, configurez votre solution MFA :

-   Pour les clients gérés par Microsoft (disposant d’Azure Active Directory ou d’Office 365) :

    -   Configurez Azure MAF pour appliquer l’authentification MFA aux utilisateurs. Pour obtenir des instructions, consultez [Prise en main avec Azure Multi-Factor Authentication dans le cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) dans la documentation sur Azure.

        Pour plus d’informations sur l’authentification multifacteur Azure, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](/multi-factor-authentication/multi-factor-authentication).

-   Pour les clients fédérés (utilisant des serveurs de fédération locaux) :

    -   Configurez vos serveurs de fédération pour Azure Active Directory ou Office 365. Par exemple, si vous utilisez les services AD FS, consultez [Configurer des méthodes d’authentification supplémentaires pour AD FS](https://technet.microsoft.com/library/dn758113.aspx) sur TechNet.

        Pour plus d’informations sur ce scénario, consultez [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sur le blog Office.

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements-azure-rms.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
