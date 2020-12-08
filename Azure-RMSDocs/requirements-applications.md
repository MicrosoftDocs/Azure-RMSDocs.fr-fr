---
title: Prise en charge par les applications de la protection des données RMS pour Azure Information Protection
description: Identifiez les applications et les solutions qui offrent une prise en charge native du service Azure Rights Management (Azure RMS). Azure RMS offre une protection des données pour Azure Information Protection (AIP).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f25b020a72a48e79b24840a597aefd4cc9e594af
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849697"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applications prenant en charge la protection des données Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les applications et solutions figurant sur cette page offrent une prise en charge native du service Azure Rights Management (Azure RMS), qui fournit une protection des données pour Azure Information Protection.

Ces applications et solutions sont appelées « compatibles RMS », et offrent une intégration étroite de Rights Management et des [restrictions d’utilisation](configure-usage-rights.md) à l’aide des API Rights Management.

> [!NOTE]
> Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. 
>
> La prise en charge d’AD RMS sur iOS, Android, macOS et Windows Phone 8.1 a également pour prérequis l’[Extension d’appareils mobiles Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).
> 

## <a name="windows-rms-enlightened-applications"></a>Applications Windows compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Applications Microsoft 365](#microsoft-365-app-support) <br />- Office 2010 <br />- Office 2013<br />- Office 2016 <br />- Office 2019 <br />- [Office pour le Web (affichage de documents protégés)](#viewing-protected-documents-in-office-for-the-web)<br />- [Navigateur web](#web-browser-support)        |
|[**E-mail**](#viewing-protected-content-in-email-clients)      |   - Outlook 2010<br />- Outlook 2013<br />- Outlook 2016 <br />- Outlook 2019 <br />- Outlook de Microsoft 365 Apps for Enterprise<br />- [Navigateur web](#web-browser-support)<br />- [Windows Mail](#email-clients-using-exchange-activesync-irm)|
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    |  - Visio d’applications Microsoft 365, Office 2019 et Office 2016 : **.vsdm,** **.vsdx,** **.vssm**, **.vstm**, **.vssx**, **.vstx** <br />- Client Azure Information Protection pour Windows : texte, images, **pfile** <br />- Plug-in SealPath RMS pour AutoCAD : **.dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>Applications macOS compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  - Microsoft 365 Apps, version 16.40 ou ultérieure <br />- Office 2019 pour Mac, version 16.40 ou ultérieure<br />- Office 2016 pour Mac, version 16.16.27 ou ultérieure<br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />- [Navigateur web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   |   - Outlook 2019 pour Mac, version 16.40 ou ultérieure<br />- Outlook 2016 pour Mac, version 16.16.27 ou ultérieure<br />- [Navigateur web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Application de partage RMS (affichage de textes et d’images protégés, fichiers protégés de façon générique)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Applications Android compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |- GigaTrust App pour Android<br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />- Office Mobile (sauf en cas d’utilisation d’étiquettes de sensibilité ; limité à l’affichage et à la modification des documents protégés) <br />- [Navigateur web](#web-browser-support)      |
|[**E-mail**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />- Application Azure Information Protection (affichage d’e-mails protégés)<br />- BlackBerry Work <br />- [GigaTrust App pour Android](#email-clients-using-exchange-activesync-irm) <br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook pour Android](#email-clients-using-exchange-activesync-irm)<br />- [Samsung Email (S3 et versions ultérieures)](#email-clients-using-exchange-activesync-irm)<br />- TITUS Classification for Mobile <br /><br />- [Navigateur web](#web-browser-support)       |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    |  Application Azure Information Protection (affichage de textes et d’images protégés)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>Applications iOS compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  - GigaTrust<br />- Office Mobile <br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />- TITUS Docs<br />- [Navigateur web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)     |   - Application Azure Information Protection (affichage d’e-mails protégés)<br />- BlackBerry Work<br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook pour iPad et iPhone](#email-clients-using-exchange-activesync-irm)<br />- TITUS Mail <br />- [Navigateur web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)     | - Application Azure Information Protection (affichage de textes et d’images protégés)<br />- TITUS Docs : **Pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Applications Windows 10 mobile compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - Applications Office Mobile (affichage de documents protégés avec Azure RMS) <br />- [Navigateur web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)    |  - Citrix WorxMail <br />- Courrier Outlook (affichage d’e-mails protégés) <br />- [Navigateur web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Non pris en charge   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Applications Blackberry 10 compatibles RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Navigateur web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   | - [ Messagerie Blackberry](#email-clients-using-exchange-activesync-irm) <br />- [Navigateur web](#web-browser-support)      |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Non pris en charge   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>Détails supplémentaires sur les applications compatibles RMS

Pour plus d’informations sur les applications compatibles RMS mentionnées ci-dessus, consultez :

- [Affichage de contenu protégé dans les clients de messagerie](#viewing-protected-content-in-email-clients)
- [Types de fichiers texte et image pris en charge](#supported-text-and-image-file-types)
- [Prise en charge des applications Microsoft 365](#microsoft-365-app-support)
- [Affichage de documents protégés dans Office pour le Web](#viewing-protected-documents-in-office-for-the-web)
- [Prise en charge des navigateurs web](#web-browser-support)
- [Clients de messagerie utilisant la Gestion des droits relatifs à l’information Exchange ActiveSync](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>Affichage de contenu protégé dans les clients de messagerie

Lorsqu’un client de messagerie protège un message, tous les fichiers Office joints au message et actuellement non protégés sont protégés avec l’e-mail. Dans ce cas, l’e-mail et les pièces jointes peuvent être affichés dans le client de messagerie, uniquement par les destinataires autorisés.

Toutefois, si seule la pièce jointe est protégée (mais pas l’e-mail proprement dit), la pièce jointe ne peut pas être prévisualisée par le client de messagerie, même par les destinataires autorisés.

> [!TIP]
> Pour les clients de messagerie qui ne prennent pas en charge la protection des e-mails, envisagez d’utiliser des [règles de flux de messagerie d’Exchange Online pour appliquer cette protection](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

### <a name="supported-text-and-image-file-types"></a>Types de fichiers texte et image pris en charge

Les types de fichiers autres que les fichiers Office et les e-mails incluent les types de fichiers texte et image, avec des extensions telles que **.txt,** **.xml,** **.jpg,** et **.jpeg.** 

Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par Rights Management, puis passent en lecture seule. 

Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier  **.pfile** une fois qu’ils sont protégés de manière générique par Rights Management.

Pour plus d’informations, consultez les [types de fichiers pris en charge](./rms-client/client-admin-guide-file-types.md).

### <a name="microsoft-365-app-support"></a>Prise en charge des applications Microsoft 365

Inclut : 
- Applications Office, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur
- Microsoft 365 Apps for enterprise

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Affichage de documents protégés dans Office pour le web

Prise en charge uniquement avec Microsoft SharePoint et OneDrive, et la protection des documents est retirée avant leur chargement dans une bibliothèque protégée.

### <a name="web-browser-support"></a>Prise en charge du navigateur web

- Les navigateurs web sont pris en charge pour les fichiers **Word, Excel et PowerPoint**, lorsque les [pièces jointes Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sont protégées à l’aide du [chiffrement des messages par Microsoft 365 avec les nouvelles fonctionnalités](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

- Pour les **e-mails**, les navigateurs web sont pris en charge uniquement dans les scénarios suivants :

    - Si l’expéditeur et le destinataire font tous deux partie de la même organisation
    - Si l’expéditeur ou le destinataire utilise Exchange Online
    - Si l’expéditeur utilise Exchange sur site dans une configuration hybride 

### <a name="email-clients-using-exchange-activesync-irm"></a>Clients de messagerie utilisant la Gestion des droits relatifs à l’information Exchange ActiveSync

Les clients de messagerie suivants utilisent la Gestion des droits relatifs à l’information Exchange ActiveSync, qui doit être activée par l’administrateur de services Exchange :

- Windows Mail
- 9Folders
- GigaTrust App pour Android
- NitroDesk
- Outlook pour Android
- Samsung Email (S3 et version ultérieure)
- Office pour iPad et iPhone
- Messagerie Blackberry

Les utilisateurs peuvent afficher, répondre et répondre à tous pour les e-mails protégés, mais ne peuvent pas protéger de nouveaux e-mails.
 
Si l’application de messagerie ne peut pas afficher le message car le serveur Exchange ActiveSync IRM n’est pas activé, le destinataire peut afficher l’e-mail dans un navigateur web quand l’expéditeur utilise Exchange Online ou Exchange local dans une configuration hybride. 

## <a name="azure-rms-support-for-office"></a>Prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). 

- [Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)](#windows-computers-for-information-rights-management-irm)
- [Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)](#mac-computers-for-information-rights-management-irm)

Voir aussi : [Description du service des applications Office](/office365/servicedescriptions/office-applications-service-description/office-applications-service-description)

### <a name="windows-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur les ordinateurs Windows à l’aide du service Azure Rights Management :

- **Applications Office**, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur

- **Microsoft 365 Apps for enterprise**

    Ces éditions d’Office sont proposées dans la plupart (mais pas dans la totalité) des abonnements qui incluent la protection des données à partir d’Azure Information Protection. Vérifiez vos informations d’abonnement pour voir si Microsoft 365 Apps for Enterprise ProPlus est inclus. Vous trouverez également ces informations dans la [feuille de données Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professionnel Plus 2013**

- **Office Professional Plus 2010 avec Service Pack 2**

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Service Azure Rights Management avec Office Professionnel Plus 2010 et Service Pack 2 ou Office Professionnel 2010 avec Service Pack 2

Quand vous utilisez le service Azure Rights Management avec Office Professionnel Plus 2010 et Service Pack 2 ou Office Professionnel 2010 avec Service Pack 2, vous devez également avoir le client AIP pour Windows.

En outre, cette configuration :

- N’est pas prise en charge sur Windows 10.
- Ne prend pas en charge l’authentification basée sur les formulaires pour les comptes d’utilisateur fédéré. Ces comptes doivent utiliser l’authentification intégrée de Windows.
- Ne prend pas en charge la possibilité de remplacer la protection du modèle à l’aide d’autorisations personnalisées sélectionnées avec le client AIP. Dans ce scénario, la protection d’origine doit d’abord être supprimée avant de pouvoir appliquer des autorisations personnalisées.

### <a name="mac-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur macOS à l’aide d’Azure RMS :

- Microsoft 365 Apps for enterprise
- Office Standard 2019 pour Mac
- Office Standard 2016 pour Mac

Toutes les éditions d’Office pour Mac 2019 et Office pour Mac 2016 prennent en charge l’utilisation du contenu protégé.

> [!TIP]
> Pour bien démarrer avec la protection des documents en utilisant Office pour Mac, consultez la question fréquente suivante : [Comment configurer un ordinateur Mac pour protéger et suivre les documents ?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>Applications Azure Information Protection pour iOS et Android

L’application Azure Information Protection pour iOS et Android fournit une visionneuse pour les e-mails protégés par des droits (fichiers **.rpmsg**) lorsque ces appareils mobiles n’ont pas d’application de messagerie capable d’ouvrir les e-mails protégés. Cette application permet également d’ouvrir des fichiers PDF, images et fichiers texte protégés par des droits.

Si vos appareils iOS et Android sont inscrits par Microsoft Intune, les utilisateurs peuvent installer l’application à partir du portail d’entreprise et vous pouvez gérer l’application à l’aide de [stratégies de protection des applications](/intune/apps/app-protection-policies) d’Intune.

Pour plus d’informations sur l’utilisation de l’application, consultez [FAQs for Azure Information Protection app for iOS and Android](./rms-client/mobile-app-faq.md) (Forum Aux Questions concernant l’application Azure Information Protection pour iOS et Android).

## <a name="the-azure-information-protection-client-for-windows"></a>Client Azure Information Protection pour Windows

Le client Azure Information Protection (AIP) comprend deux versions, avec des guides d’administrateur et d’utilisateur pour chaque version :

- **Client d’étiquetage unifié** :
    - [Guide de l’administrateur](./rms-client/clientv2-admin-guide.md)
    - [Guide d’utilisation](./rms-client/clientv2-user-guide.md)

- **Client classique** :
    - [Guide de l’administrateur](./rms-client/client-admin-guide.md)
    - [Guide d’utilisation](./rms-client/client-user-guide.md)

Téléchargez l’application correspondante à partir de la [page Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

> [!NOTE]
> Vous avez des doutes quant aux différences entre ces deux versions ? Consultez le [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) approprié.
> 
## <a name="rights-management-sharing-app"></a>Application de partage Rights Management

Sur les ordinateurs Mac, l’application de partage Rights Management fournit une visionneuse qui permet d’afficher les fichiers PDF protégés ( **.ppdf**), les images de texte protégées et les fichiers protégés de manière générique. Elle peut également protéger des fichiers image, mais pas d’autres types de fichiers. Pour protéger les fichiers Office sur ces ordinateurs, utilisez Office pour Mac ou Microsoft 365 Apps for Enterprise. 

Pour plus d’informations, consultez la [FAQ relative à l’application de partage Microsoft Rights Management pour plateformes mobiles](/previous-versions/msdn10/dn451248(v=msdn.10)).

Téléchargez l’application de partage Rights Management pour les ordinateurs Mac à partir de la [page Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="other-applications-that-support-azure-information-protection"></a>Autres applications qui prennent en charge Azure Information Protection

Outre les applications listées ci-dessus, toute application qui prend en charge les API du service Azure Rights Management peut être intégrée à Azure Information Protection. 

Il peut par exemple s’agir d’applications métier écrites en interne ou d’applications d’éditeurs de logiciels écrites à l’aide des kits SDK RSM.

Pour plus d’informations, consultez le [guide du développeur Azure Information Protection](./develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applications non prises en charge par Azure RMS

Les applications qui ne sont actuellement pas prises en charge par Azure RMS incluent :

- Microsoft OneDrive pour SharePoint Server 2013
- Visionneuse XPS
- Applications qui s’exécutent sur des versions de Windows antérieures à Windows 7, Service Pack 1


## <a name="next-steps"></a>Étapes suivantes

Voir aussi :

- [Configuration requise pour Azure Information Protection](requirements.md).
- [Comment les applications prennent en charge le service Azure Rights Management](./applications-support.md)
- [Configuration d’applications pour Azure Rights Management](configure-applications.md)

Pour obtenir les informations les plus récentes sur les solutions qui prennent en charge le service Azure Rights Management et Azure Information Protection, consultez le billet de blog [Microsoft Ignite 2019 – Microsoft Information Protection solutions Partner ecosystem showcase](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024).