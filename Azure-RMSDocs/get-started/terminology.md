---
title: "Terminologie relative à Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 7d6e1d818c8eb4f6d2e4e7d320e44c7f159eabb4


---

# Terminologie relative à Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Vous ne comprenez pas un mot, une expression ou un acronyme lié à Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) ? Recherchez ici la définition de termes et d’abréviations propres à Azure RMS, ou qui ont un sens particulier dans le contexte de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].

|Terme|Définition|
|--------|--------------|
|AADRM|Nom du module Windows PowerShell pour Azure Rights Management, dérivé de l’abréviation non officielle d’[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] quand la solution s’appelait (Windows) Azure Active Directory Rights Management.|
|activer|Permet d’activer le service [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] pour qu’une organisation puisse ajouter la protection des informations à ses documents et ses e-mails. Cette action active également les fonctionnalités Rights Management dans Exchange Online et SharePoint Online.|
|Active Directory Rights Management Services|Souvent abrégé *AD RMS*.<br /><br />Rôle Windows Server qui assure la protection des informations par le biais du chiffrement et de stratégies, à des fins de sécurisation des documents, des fichiers et des courriers électroniques.|
|AD RMS|Voir *Services Active Directory Rights Management*.|
|Azure Rights Management|Souvent abrégée en *Azure RMS*.<br /><br />Service Azure qui assure la protection des informations par le biais du chiffrement et de stratégies, à des fins de sécurisation des documents, des fichiers et des courriers électroniques.  Également appelé *service Rights Management Azure*. Les noms précédents étaient les suivants :<br /><br />*Windows Azure Active Directory Rights Management* : souvent abrégé en service Windows Azure AD Rights Management.<br /><br />*RMS Online* : nom proposé à l’origine, que vous pouvez rencontrer parfois dans les messages d’erreur et les entrées de fichier journal.|
|Azure RMS|Voir *Azure Rights Management*.|
|BYOK|Voir *Bring your own key*.|
|Bring your own key|Souvent abrégé *BYOK*.<br /><br />Option de configuration choisie par une organisation afin de pouvoir générer et gérer sa propre clé de client pour [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].|
|clé de contenu|Clé unique créée par des applications compatibles RMS pour chaque document ou e-mail protégé à l’aide de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] et qui aide à limiter le risque de divulgation des informations.|
|consommer|Permet de déverrouiller un fichier protégé par [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] afin de le lire ou de l’utiliser.|
|désactiver|Permet de désactiver le service Rights Management pour que l’organisation ne puisse plus utiliser [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].|
|modèle de service|Modèle de stratégie de droits que vous créez (modèle personnalisé) et que vous configurez pour être visible pour les utilisateurs sélectionnés, et non par tous les utilisateurs de votre organisation.|
|applications compatibles|Applications qui prennent nativement en charge Rights Management, telles que les applications Office, comme Word et Excel. Les éditeurs de logiciels indépendants et les développeurs peuvent également créer des applications qui prennent nativement en charge [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|gestion des droits d'entreprise|Terme générique standard couramment utilisé pour décrire les produits et solutions permettant aux organisations de protéger leurs informations sensibles ou précieuses par le biais d'une association d'outils de chiffrement et de stratégies d'autorisation. Microsoft Rights Management est un exemple de solution de gestion des droits d'entreprise (ERM).|
|ERM (Enterprise Rights Management)|Voir *Gestion des droits d’entreprise*.|
|protection générique|Niveau de protection permettant de chiffrer tout type de données et d'empêcher les personnes non autorisées d'accéder aux fichiers. Une fois le fichier ouvert, il est déchiffré et utilisable dans une application qui ne prend pas nativement en charge [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].|
|protection des informations|Souvent abrégé *IP*.<br /><br />Terme générique standard qui fait référence à la protection des données et des fichiers par le biais d'un accès limité, même après que les données et les fichiers ont quitté les frontières de l'organisation par courrier électronique ou via le partage de documents. Microsoft Rights Management est un exemple de solution de protection des informations.|
|Gestion des droits relatifs à l'information|Souvent abrégé *IRM*.<br /><br />Terme utilisé avec les services Office, comme Exchange Server, Word et SharePoint Online, pour décrire la capacité à prendre en charge Rights Management.|
|IRM|Voir *Gestion des droits relatifs à l’information*.|
|MSDRM|Vu parfois comme référence au client RMS 1.0, qui est remplacé par le nouveau client RMS, MSIPC. Cet ancien client prend en charge les applications développées avec RMS SDK 1.0, ainsi qu'Office 2010 et Office 2007, Exchange 2010 et Exchange 2013, SharePoint 2010 et SharePoint 2007.|
|MSIPC|Vu parfois comme référence au client RMS 2.0, qui remplace l'ancien client RMS, MSDRM. Ce nouveau client prend en charge les applications développées avec RMS SDK 2.0, ainsi qu'Office 2016 et Office 2013, SharePoint 2013 et l'application de partage RMS.|
|protection native|Niveau de protection disponible dans toutes les applications compatibles, qui empêche l'accès aux fichiers aux personnes non autorisées et qui permet également d'appliquer des stratégies restrictives, comme la lecture seule et l'interdiction d'impression. Il s'agit d'une protection permanente, même en cas de transfert des fichiers ou de sauvegarde dans un lieu public accessible à d'autres personnes.|
|.pfile|Extension de nom de fichier annexée à tous les fichiers protégés via Rights Management.|
|.ppdf|Extension de nom de fichier créée par Rights Management au moment de la création automatique d'une copie PDF d'un fichier (Word, Excel, PowerPoint ou PDF) que vous partagez par courrier électronique, de sorte que le fichier puisse être lu (mais pas modifié) sur tous les appareils.|
|niveau d’autorisation|Regroupement logique des droits d’utilisation qui permet aux utilisateurs finals et aux administrateurs de choisir plus facilement les options de configuration basées sur des rôles. Par exemple, Réviseur et Coauteur.|
|protéger|Appliquer des contrôles de Rights Management à des fichiers ou à des messages électroniques via des stratégies de chiffrement, d'identité et de contrôle d'accès afin de sécuriser vos données.|
|publish|Protection des fichiers en vue d'empêcher tout accès et utilisation non autorisés.|
|connecteur Rights Management|Relais de proxy sortant que vous pouvez déployer pour des services locaux, comme Exchange Server et SharePoint, afin de protéger les données à l’aide d’Azure Rights Management.|
|services Rights Management|Terme générique qui s’applique à la fois à la version cloud de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) et à la version locale de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS).|
|application de partage Rights Management|Application téléchargeable optionnelle pour Windows et les appareils mobiles les plus courants, qui prend en charge le partage sécurisé de fichiers en local et par courrier électronique.|
|RMS|Voir *Services Rights Management*.|
|connecteur RMS|Voir *Connecteur Rights Management*.|
|RMS for individuals|Abonnement gratuit permettant à un utilisateur d’utiliser [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] quand son organisation ne possède pas d’abonnement Office 365 ou Azure Active Directory.|
|Application de partage RMS|Voir *Application de partage Rights Management*.|
|super utilisateur|Groupe d'administrateurs de confiance possédant un droit d'accès et de déchiffrement sur les fichiers protégés par l'organisation à l'aide de Rights Management. Ce niveau d'accès est généralement requis pour le processus eDiscovery légal et les audits.|
|clé de locataire|Ou clé de certificat de licence serveur (SLC).<br /><br />Clé propre à l’organisation, qui sécurise de façon optimale toutes les fonctions de chiffrement de [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] qui lui sont associées.|
|ôter la protection|Supprimer des contrôles Rights Management de fichiers ou de messages électroniques, qui utilisent des stratégies de chiffrement, d'identité et de contrôle d'accès afin de sécuriser vos données.|
|licence d'utilisation|Certificat associé à un document, qui est accordé à un utilisateur qui ouvre un fichier ou un e-mail protégé par [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Ce certificat contient les droits d'utilisateur du fichier ou de l'e-mail, la clé de chiffrement qui est utilisée pour chiffrer le contenu, ainsi que les restrictions d'accès supplémentaires définies dans la stratégie du document.|






<!--HONumber=Jun16_HO4-->


