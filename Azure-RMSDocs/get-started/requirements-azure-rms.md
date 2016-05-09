---
# required metadata

title: Conditions requises pour Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Conditions requises pour Azure Rights Management

Pour déployer Microsoft Azure Rights Management (Azure RMS) dans votre organisation, vérifiez d’abord que vous disposez des prérequis suivants. Vous pouvez ensuite utiliser la [feuille de route pour le déploiement d’Azure Rights Management](../plan-design/deployment-roadmap.md) pour déployer Rights Management dans votre organisation.

|Configuration requise|Plus d’informations|
|---------------|--------------------|
|Un abonnement au cloud pour RMS|Votre organisation doit posséder un abonnement au cloud prenant en charge RMS.<br /><br />Pour plus d’informations sur les licences, consultez [Abonnements cloud prenant en charge Azure RMS](requirements-subscriptions.md).|
|Annuaire Azure AD|Votre organisation doit disposer d’un annuaire Azure AD pour la prise en charge de l’authentification utilisateur pour RMS. De plus, si vous souhaitez utiliser les comptes d’utilisateur de votre annuaire local (AD DS), vous devez également configurer l’intégration d’annuaire.<br /><br />La solution Multi-Factor Authentication (MFA) est prise en charge avec Azure RMS si vous disposez du logiciel client requis et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.<br /><br />Pour plus d’informations, consultez [Azure Active Directory](requirements-azure-ad.md).|
|Périphériques client|Les utilisateurs doivent posséder des périphériques client (ordinateurs ou appareils mobiles) exécutant un système d’exploitation qui prend en charge RMS.<br /><br />Pour plus d’informations, consultez [Périphériques client prenant en charge Azure RMS](requirements-client-devices.md).|
|Applications|Les utilisateurs doivent exécuter des applications prenant en charge RMS.<br /><br />Pour plus d’informations, consultez [Applications prenant en charge Azure RMS](requirements-applications.md).|
|Infrastructure prenant en charge la connexion Internet et les services cloud dépendants|Si vous avez un pare-feu ou des périphériques réseau intervenants similaires qui nécessitent une configuration pour autoriser des connexions spécifiques, consultez [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />La liste d’URL et d’adresses IP figurant dans les sections **Portail Office 365 et partage** et **Authentification Office 365 et identité** s’applique au portail Office 365, aux ressources Azure Active Directory et à Azure Rights Management. Suivez les instructions fournies dans cet article pour être tenu au courant des modifications apportées à ces informations, en vous abonnant à un flux RSS.<br /><br />En plus des informations de l’article relatif à Office, voici des informations propres à Azure RMS :<br /><br />N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer un inspection au niveau du paquet). Cela a pour effet d’interrompre l’épinglage de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour sécuriser leur communication avec Azure RMS.<br /><br />Si vous utilisez un proxy web qui requiert une authentification, vous devez le configurer pour utiliser l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.|

Si vous souhaitez utiliser Azure RMS avec des serveurs locaux, les produits pris en charge sont les suivants :

-   Exchange Server

-   SharePoint Server

-   Serveurs de fichiers Windows Server prenant en charge l’infrastructure de classification des fichiers

Pour plus d’informations sur les exigences Azure RMS supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge Azure RMS](requirements-servers.md).

> [!IMPORTANT]
> Le scénario de déploiement suivant n’est pas pris en charge :
> 
> -   Exécution côte à côte d’AD RMS et d’Azure RMS dans la même organisation, sauf pendant la migration, comme décrit dans [Migration d’AD RMS vers Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Il existe un chemin de migration pris en charge [d’AD RMS vers Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx) et [d’Azure RMS vers AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si vous déployez Azure RMS et que vous décidez ensuite que vous ne souhaitez plus utiliser ce service cloud, consultez [Mise hors service et désactivation d’Azure Rights Management](../deploy-use/decommission-deactivate.md).





<!--HONumber=Apr16_HO3-->


