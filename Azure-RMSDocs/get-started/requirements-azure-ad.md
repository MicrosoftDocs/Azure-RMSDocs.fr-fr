---
title: "Conditions requises pour Azure RMS : Azure AD Directory | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 75b2414cc360704deb6107d6c0038f5b0bf7fa70


---

# Conditions requises pour Azure RMS : Azure AD Directory

*S’applique à : Azure Rights Management, Office 365*


Vous devez disposer d’un annuaire Azure AD pour pouvoir utiliser Azure Rights Management (Azure RMS). Vous devez utiliser le compte de votre organisation correspondant à cet annuaire pour vous connecter au portail Azure Classic, où vous pouvez, par exemple, configurer et gérer les modèles Rights Management.

Si vous n’avez pas encore d’abonnement Azure pour votre organisation, vous pouvez en obtenir un en vous inscrivant pour une évaluation gratuite : accédez à la page [Prise en main d’Azure](https://account.windowsazure.com/organization) et suivez les instructions.

Pour plus d’informations, consultez les ressources suivantes dans la documentation Azure Active Directory :

-   [Qu’est-ce qu’Azure AD Directory ?](/active-directory/active-directory-whatis)

-   [Comment sont associés les abonnements Azure et Azure Active Directory ?](/active-directory/active-directory-how-subscriptions-associated-directory)

Si vous souhaitez intégrer votre annuaire Azure AD à vos forêts AD locales, consultez [Intégration de vos identités locales avec Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Si vous avez des appareils mobiles ou des ordinateurs Mac qui s'authentifient localement par le biais des services AD FS ou d'un fournisseur d'authentification équivalent :
> 
> -   Vous devez utiliser les services AD FS sur la version serveur minimale de **Windows Server 2012 R2** ou un autre fournisseur d’authentification prenant en charge le protocole OAuth 2.0.

## Multi-Factor Authentication (MFA) et Azure RMS
L’utilisation de Multi-Factor Authentication avec Azure RMS requiert au moins l’un des éléments suivants :

-   Office 2013 (version minimale) :

    -   Si vous avez Office 2013, vous devez également installer la [mise à jour du 9 juin 2015 pour Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Pour plus d’informations sur cette mise à jour et la manière dont l’authentification moderne introduit la connexion basée sur Azure Active Directory Authentication Library (ADAL) à Office 2013, consultez [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sur le blog Office.

-   Application de partage Rights Management pour Windows :

    -   Vous devez avoir installé la version minimale 1.0.1908.0, ce que vous pouvez vérifier dans la rubrique Programmes et fonctionnalités du Panneau de configuration. Pour plus d’informations sur l’application de partage, consultez [Application de partage Rights Management pour Windows](../rms-client/sharing-app-windows.md).

-   Application de partage Rights Management pour appareils mobiles et ordinateurs Mac :

    -   Assurez-vous que vous avez installé la dernière version. La prise en charge de MFA a été introduite dans la version de septembre 2015 de l’application de partage RMS.

Ensuite, configurez votre solution MFA :

-   Pour les clients gérés par Microsoft (disposant d’Azure Active Directory ou d’Office 365) :

    -   Configurez Azure MAF pour appliquer l’authentification MFA aux utilisateurs. Pour obtenir des instructions, consultez [Prise en main avec Azure Multi-Factor Authentication dans le cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) dans la documentation sur Azure.

        Pour plus d’informations sur l’authentification multifacteur Azure, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](/multi-factor-authentication/multi-factor-authentication).

-   Pour les clients fédérés (utilisant des serveurs de fédération locaux) :

    -   Configurez vos serveurs de fédération pour Azure Active Directory ou Office 365. Par exemple, si vous utilisez les services AD FS, consultez [Configurer des méthodes d’authentification supplémentaires pour AD FS](https://technet.microsoft.com/library/dn758113.aspx) sur TechNet.

        Pour plus d’informations sur ce scénario, consultez [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sur le blog Office.

## Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Conditions requises pour Azure Rights Management](requirements-azure-rms.md).




<!--HONumber=Jul16_HO3-->


