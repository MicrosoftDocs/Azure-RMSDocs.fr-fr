---
title: Configuration requise pour Azure Information Protection | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fe19726959bc16384120b610183c392031519813
ms.openlocfilehash: ff322e4ff0914ca29c7fe937a41936cb15d9a913


---

# Configuration requise pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Pour évaluer la préversion d’Azure Information Protection, vérifiez que vous disposez des prérequis suivants. 

|Condition requise|Plus d'informations|
|---------------|--------------------|
|Un abonnement au cloud qui inclut Azure RMS.|Votre organisation doit avoir un abonnement au cloud prenant en charge Rights Management.<br /><br />Pour plus d’informations et pour obtenir des liens vers des versions d’essai gratuites, consultez [Abonnements au cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md).|
|Annuaire Azure AD|Votre organisation doit disposer d’un annuaire Azure AD qui prend en charge l’authentification utilisateur pour Azure RMS et Azure Information Protection. De plus, si vous souhaitez utiliser les comptes d’utilisateur de votre annuaire local (AD DS), vous devez également configurer l’intégration d’annuaire.<br /><br />La solution Multi-Factor Authentication (MFA) est prise en charge avec Azure RMS si vous disposez du logiciel client requis et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.<br /><br />Pour plus d’informations, consultez [Annuaire Azure AD](../get-started/requirements-azure-ad.md), où les informations fournies pour Azure RMS s’appliquent également à Azure Information Protection.|
|Appareils clients|Les appareils clients suivants sont pris en charge pour cette préversion :<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quand vous protégez les données, celles-ci peuvent être consommées par les mêmes appareils (Windows, Mac, iOS, Android) que ceux qui prennent en charge Azure Rights Management. Pour plus d’informations sur ces appareils et sur les versions prises en charge, consultez [Conditions requises pour Azure RMS : Appareils clients prenant en charge Azure RMS](../get-started/requirements-client-devices.md).|
|Applications|Pour la préversion et la disponibilité générale (GA), Azure Information Protection prend en charge l’étiquetage et la protection des fichiers et des e-mails créés par les applications Office suivantes : **Word**, **Excel**, **PowerPoint** et **Outlook** des suites Office suivantes :<br /><br />- Office Professionnel Plus 2016<br /><br />- Office Professionnel Plus 2013 avec Service Pack 1<br /><br />- Office Professionnel Plus 2010<br /><br />Après la disponibilité générale, une annonce sera publiée sur le [Blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) quand Azure Information Protection prendra en charge d’autres types de fichiers comme les fichiers audio, vidéo, image et PDF.|
|Infrastructure prenant en charge la connexion Internet et les services cloud dépendants|Si vous avez un pare-feu ou des périphériques réseau intervenants similaires qui doivent être configurés pour autoriser des connexions spécifiques, consultez les informations relatives à **Azure Rights Management (RMS)** dans la section [Portail et services partagés Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) de l’article Office suivant : [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />De plus :<br /><br />- Autorisez le trafic HTTPS sur le port TCP 443 pour **rmsibizaapiprod.cloudapp.net**.<br /><br />- N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer une inspection au niveau du paquet). <br /><br />- Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer pour utiliser l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.|

## Étapes suivantes

Si ces conditions sont remplies, essayez notre démonstration autoguidée pour configurer et tester par vous-même Azure Information Protection : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).




<!--HONumber=Jul16_HO5-->


