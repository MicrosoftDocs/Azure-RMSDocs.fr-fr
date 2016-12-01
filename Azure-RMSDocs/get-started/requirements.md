---
title: Configuration requise pour Azure Information Protection | Azure Information Protection
description: "Identifiez les critères de déploiement d’Azure Information Protection pour votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/17/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8a0bf034c94cde336451b30783b80ff0c85756b1
ms.openlocfilehash: f02dfede37045679c9a88c3ada9e5386666bef97


---

# <a name="requirements-for-azure-information-protection"></a>Configuration requise pour Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Avant de déployer Azure Information Protection pour votre organisation, vérifiez que les conditions préalables suivantes sont respectées. 

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Un abonnement à Azure Information Protection|Examinez les [informations sur les abonnements](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) et la [liste des fonctionnalités](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) du site Azure Information Protection pour vérifier que l’abonnement de votre organisation inclut les fonctionnalités Azure Information Protection que vous voulez utiliser.|
|Azure Active Directory|Votre entreprise doit disposer d’Azure Active Directory afin de prendre en charge l’authentification utilisateur pour Azure Information Protection. De plus, si vous souhaitez utiliser les comptes d’utilisateur de votre annuaire local (AD DS), vous devez également configurer l’intégration d’annuaire.<br /><br />Si vos comptes sont fédérés (par exemple, si vous utilisez AD FS), ils doivent utiliser l’authentification intégrée Windows. L’authentification basée sur les formulaires n’est pas prise en charge pour Azure Information Protection.<br /><br />La solution d’authentification multifacteur (MFA) est prise en charge avec Azure Information Protection si vous disposez du logiciel client nécessaire et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.<br /><br />Pour plus d’informations, consultez [Configuration requise d’Azure Active Directory pour Azure Information Protection](requirements-azure-ad.md).|
|Appareils clients|Les utilisateurs doivent avoir des appareils clients (ordinateurs ou appareils mobiles) exécutant un système d’exploitation qui prend en charge Azure Information Protection.<br /><br />Les appareils suivants prennent en charge le client Azure Information Protection, qui permet aux utilisateurs de classer et d’étiqueter leurs e-mails et documents Office :<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quand ce client protège les données à l’aide du service Azure Rights Management, celles-ci peuvent être utilisées par les mêmes appareils (Windows, Mac, iOS, Android) que ceux qui prennent en charge le service Azure Rights Management. <br /><br />Pour plus d’informations sur les appareils qui prennent en charge le service Azure Rights Management, consultez [Appareils clients prenant en charge la protection des données Azure Rights Management](../get-started/requirements-client-devices.md).|
|Applications|Le client Azure Information Protection prend en charge l’étiquetage et la protection des fichiers et des e-mails créés par les applications Office suivantes : **Word**, **Excel**, **PowerPoint** et **Outlook** des suites Office suivantes :<br /><br /> - Office 365 ProPlus avec des applications 2016 ou 2013 (« Démarrer en un clic » ou installation basée sur Windows Installer)<br /><br />- Office Professionnel Plus 2016<br /><br />- Office Professionnel Plus 2013 avec Service Pack 1<br /><br />- Office Professionnel Plus 2010<br /><br />Pour plus d’informations sur les applications qui prennent en charge le service Azure Rights Management, consultez [Applications prenant en charge la protection des données Azure Rights Management](requirements-applications.md).|
|Infrastructure prenant en charge la connexion Internet et les services cloud dépendants|Si vous avez un pare-feu ou des périphériques réseau intervenants similaires qui doivent être configurés pour autoriser des connexions spécifiques, consultez les informations relatives à **Azure Rights Management (RMS)** dans la section [Portail et services partagés Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) de l’article Office suivant : [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Suivez les instructions fournies dans cet article Office pour être tenu au courant des modifications apportées à ces informations en vous abonnant à un flux RSS.<br /><br />En plus des informations de l’article relatif à Office, voici des informations propres à Azure Information Protection :<br /><br />- Autorisez le trafic HTTPS sur le port TCP 443 pour **api.informationprotection.azure.com**.<br /><br />- N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer une inspection au niveau du paquet). Cela a pour effet d’interrompre l’épinglage de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour sécuriser leur communication avec Azure RMS.<br /><br />- Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer de manière à utiliser l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.|

Si vous souhaitez utiliser le service Azure Rights Management d’Azure Information Protection avec des serveurs locaux, les produits pris en charge sont les suivants :

-   Exchange Server

-   SharePoint Server

-   Serveurs de fichiers Windows Server prenant en charge l’infrastructure de classification des fichiers

Pour plus d’informations sur les conditions requises supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge la protection des données Azure Rights Management](requirements-servers.md).

> [!IMPORTANT]
> Le scénario de déploiement suivant n’est pas pris en charge, sauf si vous utilisez la protection AD RMS avec Azure Information Protection (la configuration HYOK ou « conservez votre propre clé ») :
> 
> -   En cas d’exécution d’AD RMS et d’Azure RMS côte à côte dans la même organisation, sauf pendant la migration, comme décrit dans la rubrique [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Il existe un chemin de migration pris en charge [d’AD RMS vers Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) et [Azure Information Protection vers AD RM](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](../deploy-use/decommission-deactivate.md).






<!--HONumber=Nov16_HO3-->


