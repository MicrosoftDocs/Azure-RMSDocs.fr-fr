---
title: Prise en charge d’applications pour la protection des données RMS - AIP
description: Identifiez les applications qui utilisent les API RMS pour prendre en charge le service Azure Rights Management d’Azure Information Protection en mode natif.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/11/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 789257fca83a56a9fd2cbfd010f6cfad4b8ea254
ms.sourcegitcommit: 03614b97515c799d085bfa741e9a49bc8074c56b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72279142"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applications prenant en charge la protection des données Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Consultez le tableau suivant pour identifier les applications et solutions prenant en charge le service Azure Rights Management (Azure RMS) en mode natif, qui assure la protection des données pour Azure Information Protection.

Pour ces applications et solutions, la prise en charge de Rights Management est étroitement intégrée en utilisant les API Rights Management pour la prise en charge des restrictions d’utilisation. Ces applications et solutions sont également qualifiées de « compatibles RMS ».

Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. Par ailleurs, la prise en charge d’AD RMS sur iOS, Android, macOS et Windows Phone 8.1 a pour prérequis [l’extension des services AD RMS (Active Directory Rights Management Services) pour appareils mobiles](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).

## <a name="rms-enlightened-applications"></a>Applications compatibles avec RMS

Le tableau suivant affiche les applications clientes compatibles avec RMS proposées par Microsoft et d’autres fournisseurs de logiciels. 

Pour plus d’informations sur l’affichage des documents PDF protégés, consultez [Lecteurs PDF protégés pour Microsoft Information Protection](./rms-client/protected-pdf-readers.md).

Informations sur les colonnes du tableau :

-   **E-Mail :** Les clients de messagerie listés peuvent protéger l’e-mail proprement dit, ce qui a pour effet de protéger automatiquement tout fichier Office joint qui n’est pas déjà protégé. Dans ce scénario, la fonctionnalité d'aperçu du client peut afficher le contenu protégé (message et pièce jointe) aux destinataires autorisés. Cependant, si une pièce jointe est protégée mais pas le message électronique qui la contient, la fonctionnalité d’aperçu du client ne peut pas afficher la pièce jointe protégée aux destinataires autorisés. 
    
    Conseil : Pour les clients de messagerie qui ne prennent pas en charge la protection des e-mails, envisagez d’utiliser des [règles de flux de messagerie d’Exchange Online pour appliquer cette protection](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

-   **Autres types de fichiers** : Les fichiers texte et image incluent les fichiers ayant une extension de nom de fichier .txt, .xml, .jpg et .jpeg. Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par Rights Management, puis passent en lecture seule. Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier .pfile une fois qu’ils sont protégés de manière générique par Rights Management. Pour plus d’informations, consultez [Types de fichiers pris en charge](./rms-client/client-admin-guide-file-types.md) dans le guide de l’administrateur du client Azure Information Protection.


|**Système d’exploitation de l’appareil**|Word, Excel, PowerPoint|E-mail|Autres types de fichiers|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Applications Office 365 [[1]](#footnote-1)<br /><br />Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office 2019 <br /><br />Office pour le Web (affichage de documents protégés) [[2]](#footnote-2)<br /><br />Navigateur web [[3]](#footnote-3)|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Office 2019 <br /><br />Office 365 ProPlus<br /><br />Navigateur web [[4]](#footnote-4)<br /><br />Windows Mail [[5]](#footnote-5) |Visio à partir d’Office 365 Apps, Office 2019 et Office 2016 :. VSDM,. vsdx,. VSSM,. vstm,. vssx,. vstx <br /><br />Client Azure Information Protection pour Windows : Texte, images, pfile<br /><br />Plug-in SealPath RMS pour AutoCAD : .dwg|
|**iOS**|GigaTrust<br /><br /> Office Mobile <br /><br />Office pour le Web [[2]](#footnote-2)<br /><br />TITUS Docs<br /><br />Navigateur web [[3]](#footnote-3)|Application Azure Information Protection (affichage d’e-mails protégés)<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />Office pour iPad et iPhone [[5]](#footnote-5)<br /><br />TITUS Mail <br /><br />Navigateur web [[4]](#footnote-4)|Application Azure Information Protection (affichage et protection de textes et d’images)<br /><br />TITUS docs : Pfile|
|**Android**|GigaTrust App pour Android<br /><br />Office pour le Web [[2]](#footnote-2)<br /><br />Office Mobile (sauf en utilisant des étiquettes de sensibilité, limitées à l’affichage et à la modification des documents protégés) <br /><br />Navigateur web [[3]](#footnote-3)|9Folders [[5]](#footnote-5)<br /><br />Application Azure Information Protection (affichage d’e-mails protégés)<br /><br />BlackBerry Work <br /><br />GigaTrust App pour Android [[5]](#footnote-5)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[5]](#footnote-5)<br /><br />Outlook pour Android [[5]](#footnote-5)<br /><br />Samsung Email (S3 et versions ultérieures) [[5]](#footnote-5)<br /><br />TITUS Classification for Mobile <br /><br />Navigateur web [[4]](#footnote-4)|Application Azure Information Protection (affichage de textes et d’images protégés)|
|**macOS**|Applications Office 365<br /><br />Office 2019 pour Mac<br /><br />Office 2016 pour Mac<br /><br />Office pour le Web [[2]](#footnote-2)<br /><br />Navigateur web [[3]](#footnote-3)|Outlook 2019 pour Mac<br /><br /> Outlook 2016 pour Mac<br /><br />Navigateur web [[4]](#footnote-4)|Application de partage RMS (affichage de textes et d’images protégés, fichiers protégés de façon générique)|
|**Windows 10 Mobile**|Applications Office Mobile (affichage des documents protégés avec Azure RMS) <br /><br />Navigateur web [[3]](#footnote-3)|Citrix WorxMail <br /><br />Courrier Outlook (affichage des e-mails protégés) <br /><br />Navigateur web [[4]](#footnote-4)|Non prise en charge|
|**BlackBerry 10**|Navigateur web [[3]](#footnote-3)|Messagerie Blackberry [[5]](#footnote-5) <br /><br />Navigateur web [[4]](#footnote-4)|Non prise en charge|

###### <a name="footnote-1"></a>Note 1
Inclut : 
- Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est affectée à l’utilisateur
- Applications Office 365 ProPlus

###### <a name="footnote-2"></a>Note 2
Uniquement prise en charge avec SharePoint Online et OneDrive Entreprise et la protection des documents est retirée avant leur chargement sur une bibliothèque protégée.

###### <a name="footnote-3"></a>Note 3
Pour les [pièces jointes Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) qui sont protégées avec le [chiffrement de messages Office 365 avec les nouvelles fonctionnalités](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

###### <a name="footnote-4"></a>Note 4
Si l’expéditeur et le destinataire font partie de la même organisation, ou bien si une des conditions suivantes est remplie :
- L’expéditeur ou le destinataire utilise Exchange Online.
- L’expéditeur utilise Exchange local dans une configuration hybride. 

###### <a name="footnote-5"></a>Note 5
utilise l’IRM Exchange ActiveSync, qui doit être activée par l’administrateur Exchange. Les utilisateurs peuvent afficher, répondre et répondre à tous pour les e-mails protégés, mais ne peuvent pas protéger de nouveaux e-mails.
 
Si l’application de messagerie ne peut pas afficher le message car le serveur Exchange ActiveSync IRM n’est pas activé, le destinataire peut afficher l’e-mail dans un navigateur web quand l’expéditeur utilise Exchange Online ou Exchange local dans une configuration hybride. 

### <a name="more-information-about-azure-rms-support-for-office"></a>Plus d’informations sur la prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). 

Voir aussi : [Description du service des applications Office](https://technet.microsoft.com/library/office-applications-service-description.aspx)

#### <a name="windows-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur les ordinateurs Windows à l’aide du service Azure Rights Management :

- Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est affectée à l’utilisateur

- Office 365 ProPlus
    
    Ces éditions d’Office sont proposées dans la plupart (mais pas dans la totalité) des abonnements Office 365 qui incluent la protection des données à partir d’Azure Information Protection. Vérifiez vos informations d’abonnement pour voir si Office 365 ProPlus est inclus. Vous trouverez également ces informations dans la [feuille de données Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- Office Professionnel Plus 2019

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013

- Office Professionnel Plus 2010 avec Service Pack 2

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

Quand vous utilisez le service Azure Rights Management avec Office Professionnel Plus 2010 et Service Pack 2 ou Office Professionnel 2010 avec Service Pack 2 :

- Nécessite le client Azure Information Protection pour Windows.

- Non pris en charge sur Windows 10.

- Ne prend pas en charge l’authentification basée sur les formulaires pour les comptes d’utilisateur fédéré. Ces comptes doivent utiliser l’authentification intégrée de Windows.

- Ne prend pas en charge le remplacement de la protection du modèle par des autorisations personnalisées sélectionnées par un utilisateur avec le client Azure Information Protection. Dans ce scénario, la protection d’origine doit d’abord être supprimée avant de pouvoir appliquer des autorisations personnalisées.

#### <a name="mac-computers-for-information-rights-management-irm"></a>Ordinateurs Windows pour la gestion des droits relatifs à l’information (IRM)

Les suites clientes Office suivantes prennent en charge la protection des fichiers et des e-mails sur macOS à l’aide d’Azure RMS :

- Office 365 ProPlus

- Office Standard 2019 pour Mac

- Office Standard 2016 pour Mac

Toutes les éditions d’Office pour Mac 2019 et Office pour Mac 2016 prennent en charge l’utilisation du contenu protégé.

Conseil : Pour bien démarrer avec la protection des documents en utilisant Office pour Mac, consultez la question fréquente suivante : [Comment configurer un ordinateur Mac pour protéger et suivre les documents ?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Pour plus d’informations sur l’application Azure Information Protection pour iOS et Android

L’application Azure Information Protection pour iOS et Android fournit une visionneuse pour les e-mails protégés par des droits (fichiers .rpmsg) lorsque ces appareils mobiles n’ont pas d’application de messagerie capable d’ouvrir les e-mails protégés. Cette application permet également d’ouvrir des fichiers PDF, images et fichiers texte protégés par des droits.

Si vos appareils iOS et Android sont inscrits par Microsoft Intune, les utilisateurs peuvent installer l’application à partir du portail d’entreprise et vous pouvez gérer l’application à l’aide de [stratégies de protection des applications](/intune/app-protection-policies) d’Intune.

Pour plus d’informations sur l’utilisation de l’application, consultez [FAQs for Azure Information Protection app for iOS and Android](./rms-client/mobile-app-faq.md) (Forum Aux Questions concernant l’application Azure Information Protection pour iOS et Android).


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Plus d’informations sur le client Azure Information Protection pour Windows

Pour plus d'informations, consultez les ressources suivantes :

- [Client Azure Information Protection - Guide de l’administrateur](./rms-client/client-admin-guide.md)

- [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md)

- [FAQ relatifs à l’application Azure Information Protection pour iOS et Android](./rms-client/mobile-app-faq.md)

Téléchargez l’application correspondante à l’aide des liens de la [page Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

### <a name="more-information-about-the-rights-management-sharing-app"></a>Plus d’informations sur l’application de partage Rights Management

Sur les ordinateurs Mac, l’application de partage Rights Management fournit une visionneuse qui permet d’afficher les fichiers PDF protégés (.ppdf), les images de texte protégées et les fichiers protégés de manière générique. Elle peut également protéger des fichiers image, mais pas d’autres types de fichiers. Pour protéger les fichiers Office sur ces ordinateurs, utilisez Office pour Mac ou Office 365 ProPlus. 

Pour plus d'informations, consultez les ressources suivantes :

-   [FAQ relatif à l’application de partage Microsoft Rights Management pour plateformes mobiles](https://technet.microsoft.com/dn451248)

Téléchargez l’application de partage Rights Management pour les ordinateurs Mac en utilisant le lien dans la [page Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Plus d’informations sur les autres applications qui prennent en charge Azure Information Protection

En plus des applications indiquées dans le tableau, toute application qui prend en charge les API du service Azure Rights Management peut être intégrée à Azure Information Protection, notamment :

- Applications métier écrites en interne avec les SDK RMS

- Applications de fournisseurs de logiciels écrites avec les SDK RMS

Pour plus d’informations, consultez le [guide du développeur Azure Information Protection](./develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Applications non prises en charge par Azure RMS

Les applications suivantes ne sont pas prises en charge actuellement par Azure RMS :

- Microsoft OneDrive Entreprise pour SharePoint Server 2013

- Visionneuse XPS

De plus, le client Azure Information Protection présente les restrictions suivantes :

- Pour les ordinateurs Windows : Nécessite une version minimale de Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>Solutions compatibles avec RMS

Le tableau suivant affiche les solutions compatibles avec RMS proposées par différents fournisseurs de logiciels.

Si vous êtes fournisseur de logiciels et que vous proposez une solution compatible avec RMS qui n’est pas répertoriée dans ce tableau, vous pouvez inscrire votre application avec Azure AD. Pour en savoir plus, consultez l’article [Procédure d’inscription et d’activation RMS de votre application dans Azure AD](./develop/authentication-integration.md).


|Produit|Fabricant|Description|
|-------------------------------|---------------------------|-----------------|
|Absolu|Absolu|Protection contre la perte de données (DLP) pour protéger le contenu.|
|Stockage sécurisé du contenu|VMware|Stocke, utilise et crée du contenu protégé.|
|Contrôle|TakeControle|eDiscovery avec l’étiquetage et la protection.|
|Forcepoint|Protection contre la perte de données Forcepoint|Solution de protection contre la perte de données du point de terminaison pour appliquer les stratégies de sécurité des données d’une organisation.|
|Halocore|Secude|Protège les fichiers exportés à partir d’environnements SAP.|
|MaaS 360|IBM|Intégration pour utiliser et protéger les documents.|
|Mobiliya|Mobiliya|Sécurise les documents provenant des référentiels Documentum EMC.
|Ramessys|Ramessys|Intégration de Chemcart et Documentum.
|Sealpath|Sealpath Technologies|Intégration avec les outils de conception CAO, comme AutoCAD et Siemens Jt2GO.
|SecRMM|Sqaudra Technologies |Protection des documents pour supports amovibles.
|Security Sheriff|CryptZone |Gestion des accès sur SharePoint et protection des documents, en fonction de leurs autorisations d’accès et de leur classification.
|Symantec DLP|Symantec |Détection et analyse des fichiers protégés.

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements.md).

Pour plus d’informations sur la prise en charge d’Azure RMS par les applications les plus courantes, consultez [Comment les applications prennent en charge le service Azure Rights Management](./applications-support.md).

Pour plus d’informations sur la façon de configurer les applications les plus courantes pour Azure RMS, consultez [Configuration d’applications pour Azure Rights Management](configure-applications.md).

