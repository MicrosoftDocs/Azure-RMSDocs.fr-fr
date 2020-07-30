---
title: Prise en charge des applications pour la protection des données RMS pour Azure Information Protection
description: Identifiez les applications et les solutions qui prennent en charge nativement le service Azure Rights Management (Azure RMS). Azure RMS fournit la protection des données pour Azure Information Protection (AIP).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/20/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9ed56f635c4210c9989fb0e02209f4e3c29129a3
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87298170"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applications prenant en charge la protection des données Azure Rights Management

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les applications et solutions figurant sur cette page prennent en charge nativement le service Azure Rights Management (Azure RMS), qui fournit la protection des données pour Azure Information Protection.

Ces applications et solutions sont connues sous le nom de « RMS », et les [restrictions d’utilisation](configure-usage-rights.md) et de Rights Management sont étroitement intégrées à l’aide des API Rights Management.

> [!NOTE]
> Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. 
>
> La prise en charge de AD RMS sur iOS, Android, macOS et Windows Phone 8,1 requiert également l' [extension d’appareil Mobile services AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).
> 

## <a name="windows-rms-enlightened-applications"></a>Applications compatibles Windows RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Applications Office 365](#office-365-app-support) <br />- Office 2010 <br />-Office 2013<br />- Office 2016 <br />-Office 2019 <br />- [Office pour le Web (affichage de documents protégés)](#viewing-protected-documents-in-office-for-the-web)<br />- [Navigateur Web](#web-browser-support)        |
|[**E-mail**](#viewing-protected-content-in-email-clients)      |   -Outlook 2010<br />-Outlook 2013<br />-Outlook 2016 <br />-Outlook 2019 <br />-Outlook à partir d’Office de Microsoft 365 apps pour l’entreprise<br />- [Navigateur Web](#web-browser-support)<br />- [Messagerie Windows](#email-clients-using-exchange-activesync-irm)|
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    |  -Visio à partir d’Office 365 Apps, Office 2019 et Office 2016 : **. VSDM,** **. vsdx,** **. VSSM**, **. vstm**, **. vssx**, **. vstx** <br />-Azure Information Protection client pour Windows : texte, images, **pfile** <br />-Plug-in RMS SealPath pour AutoCAD : **. DWG**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>applications compatibles macOS RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  -Applications Office 365<br />-Office 2019 pour Mac<br />-Office 2016 pour Mac<br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />- [Navigateur Web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   |   -Outlook 2019 pour Mac<br />-Outlook 2016 pour Mac<br />- [Navigateur Web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Application de partage RMS (affichage de textes et d’images protégés, fichiers protégés de façon générique)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Applications compatibles Android RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |-Application GigaTrust pour Android<br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />-Office Mobile (sauf en utilisant des étiquettes de sensibilité, limitées à l’affichage et à la modification des documents protégés) <br />- [Navigateur Web](#web-browser-support)      |
|[**E-mail**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />-Azure Information Protection application (affichage d’e-mails protégés)<br />-BlackBerry-travail <br />- [Application GigaTrust pour Android](#email-clients-using-exchange-activesync-irm) <br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook pour Android](#email-clients-using-exchange-activesync-irm)<br />- [E-mail Samsung (S3 et versions ultérieures)](#email-clients-using-exchange-activesync-irm)<br />-Classification TITUS pour les appareils mobiles <br /><br />- [Navigateur Web](#web-browser-support)       |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    |  Application Azure Information Protection (affichage de textes et d’images protégés)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>applications compatibles iOS RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  -GigaTrust<br />-Office Mobile <br />- [Office pour le Web](#viewing-protected-documents-in-office-for-the-web)<br />-TITUS docs<br />- [Navigateur Web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)     |   -Azure Information Protection application (affichage de l’e-mail protégé)<br />-BlackBerry-travail<br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook pour iPad et iPhone](#email-clients-using-exchange-activesync-irm)<br />-TITUS mail <br />- [Navigateur Web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)     | -Azure Information Protection application (affichage de la protection du texte et des images)<br />-TITUS docs : **pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Applications compatibles RMS Windows 10 mobile

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | -Office Mobile Apps (affichage de documents protégés à l’aide de Azure RMS) <br />- [Navigateur Web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)    |  -Citrix WorxMail <br />-Outlook Mail (affichage des e-mails protégés) <br />- [Navigateur Web](#web-browser-support)     |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Non pris en charge   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Applications compatibles BlackBerry 10 RMS

|Type  |Applications prises en charge   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Navigateur Web](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   | - [E-mail BlackBerry](#email-clients-using-exchange-activesync-irm) <br />- [Navigateur Web](#web-browser-support)      |
|[**Autres types de fichiers**](#supported-text-and-image-file-types)    | Non pris en charge   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>Détails supplémentaires sur les applications compatibles RMS

Pour plus d’informations sur les tables des applications compatibles RMS mentionnées ci-dessus, consultez :

- [Affichage de contenu protégé dans les clients de messagerie](#viewing-protected-content-in-email-clients)
- [Types de fichiers texte et image pris en charge](#supported-text-and-image-file-types)
- [Prise en charge des applications Office 365](#office-365-app-support)
- [Affichage de documents protégés dans Office pour le Web](#viewing-protected-documents-in-office-for-the-web)
- [Prise en charge des navigateurs Web](#web-browser-support)
- [Clients de messagerie utilisant les informations d’Rights Management Exchange ActiveSync (IRM)](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>Affichage de contenu protégé dans les clients de messagerie

Lorsqu’un client de messagerie protège un message, tous les fichiers Office attachés au message et non protégés ne sont pas protégés, et sont protégés avec le message électronique. Dans ce cas, le message électronique et les pièces jointes peuvent être affichés dans le client de messagerie, par les destinataires autorisés uniquement.

Toutefois, si seule la pièce jointe est protégée mais pas le message électronique lui-même, la pièce jointe ne peut pas être prévisualisée par le client de messagerie, même par les destinataires autorisés.

> [!TIP]
> Pour les clients de messagerie qui ne prennent pas en charge la protection des e-mails, envisagez d’utiliser des [règles de flux de messagerie d’Exchange Online pour appliquer cette protection](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

### <a name="supported-text-and-image-file-types"></a>Types de fichiers texte et image pris en charge

Les types de fichiers autres que les fichiers Office et les messages électroniques incluent des types de fichiers texte et image, avec des extensions telles que **. txt,** **. xml,** **. jpg** et **. jpeg.** 

Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par Rights Management, puis sont en lecture seule. 

Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier **. pfile** une fois qu’ils sont protégés de manière générique par Rights Management.

Pour plus d’informations, consultez [types de fichiers pris en charge](./rms-client/client-admin-guide-file-types.md).

### <a name="office-365-app-support"></a>Prise en charge des applications Office 365

Inclut : 
- Applications Office version 1805 minimum, Build 9330,2078 à partir de [Microsoft 365 Apps for Business](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename). Pris en charge uniquement lorsque l’utilisateur se voit attribuer une licence pour Azure Rights Management (également appelée Azure Information Protection pour Office 365).
- [Microsoft 365 des applications pour l’entreprise](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename).

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Affichage de documents protégés dans Office pour le Web

Pris en charge uniquement avec Microsoft SharePoint et OneDrive, et les documents ne sont pas protégés avant d’être téléchargés dans une bibliothèque protégée.

### <a name="web-browser-support"></a>Prise en charge du navigateur web

- Les navigateurs Web sont pris en charge pour les fichiers **Word, Excel et PowerPoint** , lorsque les [pièces jointes Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sont protégées à l’aide [du chiffrement de messages Office 365 avec les nouvelles fonctionnalités](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

- Pour les **e-mails,** les navigateurs Web sont pris en charge uniquement dans les scénarios suivants :

    - Si l’expéditeur et le destinataire font tous deux partie de la même organisation
    - Si l’expéditeur ou le destinataire utilise Exchange Online
    - Si l’expéditeur utilise Exchange sur site dans une configuration hybride 

### <a name="email-clients-using-exchange-activesync-irm"></a>Clients de messagerie utilisant Exchange ActiveSync IRM

Les clients de messagerie suivants utilisent la gestion des droits relatifs à Exchange ActiveSync, qui doit être activée par l’administrateur Exchange :

- Windows Mail
- 9Folders
- GigaTrust App pour Android
- NitroDesk
- Outlook pour Android
- Samsung Email (S3 et version ultérieure)
- Office pour iPad et iPhone
- E-mail BlackBerry

Les utilisateurs peuvent afficher, répondre et répondre à tous les messages électroniques protégés, mais ne peuvent pas protéger de nouveaux messages électroniques.
 
Si l’application de messagerie ne peut pas afficher le message car le serveur Exchange ActiveSync IRM n’est pas activé, le destinataire peut afficher l’e-mail dans un navigateur web quand l’expéditeur utilise Exchange Online ou Exchange local dans une configuration hybride. 

## <a name="azure-rms-support-for-office"></a>Prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). 

- [Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)](#windows-computers-for-information-rights-management-irm)
- [Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)](#mac-computers-for-information-rights-management-irm)

Voir aussi : [Description du service des applications Office](https://technet.microsoft.com/library/office-applications-service-description.aspx)

### <a name="windows-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur les ordinateurs Windows à l’aide du service Azure Rights Management :

|Version d’Office  |Détails de la prise en charge  |
|---------|---------|
|[**Microsoft 365 des applications pour l’entreprise**](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename)     |  Les applications Office minimales version 1805, Build 9330,2078, lorsque l’utilisateur se voit attribuer une licence pour Azure Rights Management (également appelée Azure Information Protection pour Office 365)       |
|[**Applications Microsoft 365 pour l’entreprise**](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename)     | Les éditions suivantes d’Office sont incluses avec la plupart des abonnements Office 365, mais pas tous, qui incluent la protection des données de Azure Information Protection. </br>Vérifiez vos informations d’abonnement pour voir si Microsoft 365 applications pour l’entreprise est incluse. Vous trouverez également ces informations dans la [feuille de données Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf). </br></br>-Microsoft 365 applications pour l’entreprise 2019 </br>-Microsoft 365 applications pour l’entreprise 2016 </br>-Microsoft 365 applications pour l’entreprise 2013 </br>-Microsoft 365 apps pour Enterprise 2010 avec Service Pack 2       |

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

#### <a name="azure-rights-management-service-with-microsoft-365-apps-for-enterprise-2010"></a>Service Azure Rights Management avec les applications Microsoft 365 pour Enterprise 2010

Quand vous utilisez le service Azure Rights Management avec les [applications Microsoft 365 pour Enterprise](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename) 2010 et Service Pack 2 ou Office Professionnel 2010 avec Service Pack 2, vous devez également disposer du client AIP pour Windows.

En outre, cette configuration :

- N’est pas pris en charge sur Windows 10.
- Ne prend pas en charge l’authentification basée sur les formulaires pour les comptes d’utilisateur fédéré. Ces comptes doivent utiliser l’authentification intégrée de Windows.
- Ne prend pas en charge la possibilité de remplacer la protection du modèle à l’aide des autorisations personnalisées sélectionnées avec le client AIP. Dans ce scénario, la protection d’origine doit d’abord être supprimée avant de pouvoir appliquer des autorisations personnalisées.

### <a name="mac-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur macOS à l’aide d’Azure RMS :

- [Applications Microsoft 365 pour l’entreprise](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename)
- Office Standard 2019 pour Mac
- Office Standard 2016 pour Mac

Toutes les éditions d’Office pour Mac 2019 et Office pour Mac 2016 prennent en charge l’utilisation du contenu protégé.

> [!TIP]
> Pour commencer à protéger des documents à l’aide d’Office pour Mac, vous trouverez peut-être le FAQ suivant : [Comment faire configurer un ordinateur Mac pour protéger et suivre les documents ?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>Applications Azure Information Protection pour iOS et Android

L’application Azure Information Protection pour iOS et Android fournit une visionneuse pour les messages électroniques protégés par des droits **(fichiers. rpmsg** ) quand ces appareils mobiles ne disposent pas d’une application de messagerie capable d’ouvrir des e-mails protégés. Cette application permet également d’ouvrir des fichiers PDF, images et fichiers texte protégés par des droits.

Si vos appareils iOS et Android sont inscrits par Microsoft Intune, les utilisateurs peuvent installer l’application à partir du portail d’entreprise et vous pouvez gérer l’application à l’aide de [stratégies de protection des applications](/intune/app-protection-policies) d’Intune.

Pour plus d’informations sur l’utilisation de l’application, consultez [FAQs for Azure Information Protection app for iOS and Android](./rms-client/mobile-app-faq.md) (Forum Aux Questions concernant l’application Azure Information Protection pour iOS et Android).

## <a name="the-azure-information-protection-client-for-windows"></a>Client Azure Information Protection pour Windows

Le client Azure Information Protection (AIP) comprend deux versions, avec des guides d’administrateur et d’utilisateur pour chaque version :

- **Client d’étiquetage unifié**:
    - [Guide de l’administrateur](./rms-client/clientv2-admin-guide.md)
    - [Guide d’utilisation](./rms-client/clientv2-user-guide.md)

- **Client classique**:
    - [Guide de l’administrateur](./rms-client/client-admin-guide.md)
    - [Guide d’utilisation](./rms-client/client-user-guide.md)

Téléchargez l’application appropriée à partir de la [page Microsoft Azure information protection](https://go.microsoft.com/fwlink/?LinkId=303970).

> [!NOTE]
> Vous n’êtes pas sûr des différences entre ces deux versions ? Consultez le [Forum aux questions](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).
> 
## <a name="rights-management-sharing-app"></a>Application de partage Rights Management

Pour les ordinateurs Mac, l’application de partage Rights Management offre une visionneuse pour les fichiers PDF protégés **(. ppdf),** les images de texte protégées et les fichiers protégés de manière générique. Elle peut également protéger des fichiers image, mais pas d’autres types de fichiers. Pour protéger des fichiers Office sur ces ordinateurs, utilisez Office pour Mac ou [des applications Microsoft 365 pour l’entreprise](https://www.microsoft.com/microsoft-365/partners/smb-sku-rename). 

Pour plus d’informations, consultez le [Forum aux questions sur l’application de partage Microsoft Rights Management pour les plateformes mobiles](https://technet.microsoft.com/dn451248) .

Téléchargez l’application de partage Rights Management pour les ordinateurs Mac à partir de la [page Microsoft Azure information protection](https://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="other-applications-that-support-azure-information-protection"></a>Autres applications prenant en charge Azure Information Protection

Outre les applications listées ci-dessus, toute application prenant en charge les API du service Azure Rights Management peut être intégrée à Azure Information Protection. 

Les exemples peuvent inclure des applications métier écrites en interne, ou des applications de fournisseurs de logiciels, écrites à l’aide des kits de développement logiciel (SDK) RSM.

Pour plus d’informations, consultez le [guide du développeur Azure Information Protection](./develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applications non prises en charge par Azure RMS

Les applications qui ne sont actuellement pas prises en charge par Azure RMS incluent :

- Microsoft OneDrive pour SharePoint Server 2013
- Visionneuse XPS
- Applications qui s’exécutent sur des versions de Windows antérieures à Windows 7, Service Pack 1


## <a name="next-steps"></a>Étapes suivantes

Voir aussi :

- [Configuration requise pour Azure information protection](requirements.md).
- [Comment les applications prennent en charge le service Azure Rights Management](./applications-support.md).
- [Configuration d’applications pour Azure Rights Management](configure-applications.md).

Pour obtenir les informations les plus récentes sur les solutions qui prennent en charge le service et les Azure Information Protection Azure Rights Management, consultez le billet de blog [microsoft 2019 – microsoft information Protection Solutions Partner écosystème Showcase](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024).
