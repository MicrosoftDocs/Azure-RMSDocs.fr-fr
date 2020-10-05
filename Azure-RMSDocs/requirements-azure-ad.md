---
title: Prérequis supplémentaires pour Azure AD et Azure Information Protection
description: Découvrez les prérequis Azure AD supplémentaires pour Azure Information Protection dans des scénarios spécifiques, comme l’authentification multifacteur ou basée sur les certificats, ou encore les ordinateurs utilisant Office 2010 et plus encore.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/22/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: 858a2ebb1bbc5040d564d9df05943c10a3f58a4a
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91428353"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Prérequis Azure AD supplémentaires pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Un [annuaire Azure AD est requis](requirements.md#azure-active-directory) pour utiliser Azure Information Protection. Utilisez un compte d’un annuaire Azure AD pour vous connecter au portail Azure, dans lequel vous pouvez configurer les paramètres Azure Information Protection.

Si vous avez un abonnement incluant Azure Information Protection ou Azure Rights Management, votre annuaire Azure AD est créé automatiquement pour vous si nécessaire.

Les sections suivantes liste les prérequis AIP et Azure AD supplémentaires pour des scénarios spécifiques. 

## <a name="computers-running-office-2010"></a>Ordinateurs qui exécutent Office 2010

En plus du compte Azure AD, les ordinateurs qui exécutent Microsoft Office 2010 nécessitent le [client d’étiquetage unifié Azure Information Protection](./rms-client/aip-clientv2.md) ou le [client classique Azure Information Protection](./rms-client/aip-client.md) pour s’authentifier auprès d’Azure Information Protection et son service de protection des données, Azure Rights Management.

Si vos comptes d’utilisateur sont fédérés (par exemple, si vous utilisez AD FS), ces ordinateurs doivent utiliser l’authentification intégrée de Windows. L’authentification basée sur les formulaires dans ce scénario ne peut pas authentifier les utilisateurs pour Azure Information Protection.

## <a name="support-for-certificate-based-authentication-cba"></a>Prise en charge de l’authentification basée sur les certificats

Les applications Azure Information Protection pour iOS et Android prennent en charge l’authentification par certificat. 

Pour plus d’informations, consultez [Bien démarrer avec l’authentification basée sur les certificats dans Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Authentification multifacteur (MFA) et Azure Information Protection

Pour utiliser l’authentification multifacteur (MFA) avec Azure Information Protection, vous devez avoir installé au moins l’un des éléments suivants :

- **Microsoft Office,** version 2013 ou ultérieure
- **Un client AIP**. Aucune version minimale requise. Les clients AIP pour Windows, ainsi que les applications de visionneuse pour iOS et Android prennent tous en charge MFA.
- **Application de partage Rights Management pour les ordinateurs Mac**. Les applications de partage RMS prennent en charge MFA depuis la version de septembre 2015.

> [!NOTE]
> Si vous avez Office 2013, vous risquez de devoir installer une mise à jour supplémentaire pour prendre en charge Active Directory Authentication Library (ADAL), comme la [mise à jour pour Office 2013 du 9 juin 2015 (KB3054853)](https://support.microsoft.com/kb/3054853). 
>
> Pour plus d’informations, consultez la [préversion publique de l’authentification moderne Office 2013 annoncée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sur le blog Office.       

Une fois que vous avez confirmé ces prérequis, effectuez l’une des opérations suivantes, en fonction de la configuration de votre locataire :

- **Locataires gérés par Microsoft, avec Azure AD ou Microsoft 365**. Configurez Azure MAF pour appliquer l’authentification MFA aux utilisateurs. 

    Pour plus d'informations, consultez les pages suivantes : 
    - [Prise en main avec Azure Multi-Factor Authentication dans le cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [Présentation d'Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication)

- **Locataires fédérés, où les serveurs de fédération fonctionnent en local**. Configurez vos serveurs de fédération pour Azure Active Directory ou Microsoft 365. Par exemple, si vous utilisez les services AD FS, consultez [Configurer des méthodes d’authentification supplémentaires pour AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs). 

    Pour plus d’informations sur ce scénario, consultez [The Works with Microsoft 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sur le blog Office. 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Configuration requise pour le connecteur Rights Management/ le moteur d’analyse AIP

Le connecteur Azure Rights Management et le moteur d’analyse Azure Information Protection ne prennent pas en charge la MFA. 

Si vous déployez le connecteur ou le moteur d’analyse, les comptes suivants ne doivent pas exiger l’authentification multifacteur :

- Le compte qui installe et configure le connecteur.
- Le compte principal du service dans Azure AD, **Aadrm_S-1-7-0** créé par le connecteur.
- Le compte de service qui exécute le moteur d’analyse.

## <a name="user-upn-values-dont-match-their-email-addresses"></a>Les valeurs UPN des utilisateurs ne correspondent pas à leurs adresses e-mail

La configuration où les valeurs UPN des utilisateurs ne correspondent pas à leurs adresses e-mail n’est pas recommandée et ne prend pas en charge l’authentification unique pour Azure Information Protection.

Si vous ne pouvez pas changer la valeur UPN, configurez d’autres ID pour les utilisateurs concernés et indiquez-leur comment se connecter à Office avec cet autre ID. 

Pour plus d'informations, consultez les pages suivantes :

- [Configuration des ID de connexion alternatif](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Les applications Office sont régulièrement invitées à entrer des informations d’identification pour SharePoint, OneDrive et Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).

> [!TIP]
> Si le nom de domaine dans la valeur UPN est un domaine qui est vérifié pour votre locataire, ajoutez la valeur UPN de l’utilisateur comme autre adresse e-mail à l’attribut **proxyAddresses** d’Azure AD. L’utilisateur est ainsi autorisé à utiliser Azure Rights Management si sa valeur UPN est spécifiée au moment où les droits d’utilisation sont accordés. 

Pour plus d’informations, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

## <a name="authenticating-on-premises-using-adfs-or-another-authentication-provider"></a>Authentification locale avec AD FS ou un autre fournisseur d’authentification

Si vous utilisez un appareil mobile ou un ordinateur Mac qui s’authentifie localement avec AD FS, ou un fournisseur d’authentification équivalent, vous devez utiliser AD FS sur l’une des configurations suivantes :

- Version serveur minimale de **Windows Server 2012 R2**
- Un autre fournisseur d’authentification qui prend en charge le protocole OAuth 2.0

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements.md).
