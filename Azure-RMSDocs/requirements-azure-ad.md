---
title: Configuration requise d’Azure AD pour Azure Information Protection – AIP
description: Identifiez la configuration requise d’Azure AD pour utiliser Azure Information Protection afin de permettre l’authentification des utilisateurs.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f8e5ceec7fe868e16f79bfdd058611f7da96c52f
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793748"
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Configuration requise d’Azure Active Directory pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Un annuaire Azure AD est nécessaire pour pouvoir utiliser Azure Information Protection. Vous utilisez un compte de cet annuaire pour vous connecter au portail Azure, où vous pouvez par exemple configurer et gérer des étiquettes Azure Information Protection et des modèles Azure Rights Management.

Si vous avez un abonnement incluant Azure Information Protection ou Azure Rights Management, votre annuaire Azure AD est créé automatiquement pour vous si nécessaire.  

Pour plus d’informations sur Azure AD, consultez [Qu’est-ce que l’annuaire Azure AD ?](/azure/active-directory/fundamentals/active-directory-whatis)

Pour intégrer un annuaire Azure AD à des forêts AD locales, voir [Intégrer des domaines Active Directory locaux à Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad).

### <a name="scenarios-that-have-specific-requirements"></a>Scénarios avec des exigences spécifiques 

Ordinateurs qui exécutent Office 2010 : 

- Ces ordinateurs nécessitent l' [Azure information protection client d’étiquetage unifié](./rms-client/aip-clientv2.md) ou [Azure information protection client](./rms-client/aip-client.md) pour s’authentifier auprès d’Azure information protection et de son service de protection des données, Azure Rights Management.

- Si vos comptes d’utilisateur sont fédérés (par exemple, si vous utilisez AD FS), ils doivent utiliser l’authentification intégrée de Windows. L’authentification basée sur les formulaires dans ce scénario ne peut pas authentifier les utilisateurs pour Azure Information Protection.

Prise en charge de l’authentification basée sur les certificats :

- Les applications Azure Information Protection pour iOS et Android prennent en charge l’authentification par certificat. Pour des instructions sur la configuration de l’authentification basée sur les certificats, consultez [Bien démarrer avec l’authentification basée sur les certificats dans Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

La valeur UPN des utilisateurs ne correspond pas à leur adresse e-mail :

- Cette configuration n’est pas recommandée. Si vous ne pouvez pas changer la valeur UPN, configurez un autre ID de connexion pour les utilisateurs et indiquez-leur comment se connecter à Office à l’aide de cette connexion de remplacement. Pour plus d’informations, consultez [Configuration d’un autre ID de connexion](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) et [Les applications Office demandent régulièrement des informations d’identification pour SharePoint Online, OneDrive et Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).
    
    Quand le nom de domaine dans la valeur UPN est un domaine qui est vérifié pour votre locataire, ajoutez la valeur UPN de l’utilisateur comme une autre adresse e-mail à l’attribut proxyAddresses d’Azure AD. L’utilisateur est ainsi autorisé à utiliser Azure Rights Management si sa valeur UPN est spécifiée au moment où les droits d’utilisation sont accordés. Pour plus d’informations sur ce sujet et sur la façon dont les comptes d’utilisateur sont autorisés, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

Appareils mobiles ou ordinateurs Mac qui s’authentifient localement avec AD FS ou un fournisseur d’authentification équivalent :

- Vous devez utiliser AD FS sur la version serveur minimale de **Windows Server 2012 R2**, ou un autre fournisseur d’authentification prenant en charge le protocole OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Authentification multifacteur (MFA) et Azure Information Protection
Pour utiliser l’authentification multifacteur (MFA) avec Azure Information Protection, vous devez avoir au moins l’un des éléments suivants :

-   Office 2013 (version minimale) :

    -   Si vous avez Office 2013, il peut être nécessaire d’installer une mise à jour supplémentaire pour prendre en charge Active Directory Authentication Library (ADAL). Par exemple, la [mise à jour pour Office 2013 (KB3054853) du 9 juin 2015](https://support.microsoft.com/kb/3054853). Pour plus d’informations sur cette mise à jour et la manière dont l’authentification moderne introduit la connexion basée sur Azure Active Directory Authentication Library (ADAL) à Office 2013, consultez [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sur le blog Office.

- Client Azure Information Protection :

    - Les clients Azure Information Protection pour Windows et l’application de visionneuse pour iOS et Android ont toujours pris en charge MFA; aucune version minimale n’est requise. 

-   Application de partage Rights Management et ordinateurs Mac :

    -   La prise en charge de MFA a été introduite dans la version de septembre 2015 de l’application de partage RMS.

Ensuite, configurez votre solution MFA :

-   Pour les clients gérés par Microsoft (disposant d’Azure Active Directory ou d’Office 365) :

    - Configurez Azure MAF pour appliquer l’authentification MFA aux utilisateurs. Pour obtenir des instructions, consultez [Prise en main avec Azure Multi-Factor Authentication dans le cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) dans la documentation sur Azure.

        Pour plus d’informations sur l’authentification multifacteur Azure, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](/multi-factor-authentication/multi-factor-authentication).

- Pour les clients fédérés (utilisant des serveurs de fédération locaux) :

    - Configurez vos serveurs de fédération pour Azure Active Directory ou Office 365. Par exemple, si vous utilisez AD FS, consultez [configurer des méthodes d’authentification supplémentaires pour les AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

        Pour plus d’informations sur ce scénario, consultez [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sur le blog Office.

Le connecteur Azure Rights Management et le moteur d’analyse Azure Information Protection ne prennent pas en charge la MFA. Si vous déployez le connecteur ou le moteur d’analyse, les comptes suivants ne doivent pas exiger l’authentification multifacteur :

- Le compte qui installe et configure le connecteur.

- Le compte principal du service dans Azure AD, **Aadrm_S-1-7-0** créé par le connecteur.
 
- Le compte de service qui exécute le moteur d’analyse.

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements.md).

