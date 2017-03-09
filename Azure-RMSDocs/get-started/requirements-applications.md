---
title: "Prise en charge d’applications pour la protection des données RMS - AIP"
description: "Identifiez les applications qui utilisent les API RMS pour prendre en charge le service Azure Rights Management d’Azure Information Protection en mode natif."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: d8a3c8a054412280df341edd4078294c3e05979e
ms.lasthandoff: 02/24/2017


---


# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applications prenant en charge la protection des données Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*


Consultez le tableau suivant pour identifier les applications prenant en charge le service Azure Rights Management (Azure RMS) en mode natif, qui assure la protection des données pour Azure Information Protection. 

Pour ces applications, la prise en charge de Rights Management est étroitement intégrée à l’aide des API Rights Management pour prendre en charge les restrictions d’utilisation. Ces applications sont également appelées « applications compatibles avec RMS ».

Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. Par ailleurs, la prise en charge d’AD RMS sur iOS, Android, OS X et Windows Phone 8.1 nécessite [Active Directory Rights Management Services Mobile Device Extension](https://technet.microsoft.com/library/dn673574.aspx).

Informations sur les colonnes du tableau :

-   **PDF protégé** : fichiers avec l’extension de nom de fichier .ppdf qui sont créés automatiquement quand vous utilisez l’application de partage RMS pour partager des fichiers Office et des fichiers PDF par e-mail. L’application de partage RMS, l’application Azure Information Protection pour iOS et Android et le client Azure Information Protection pour Windows incluent un lecteur pour les fichiers PDF protégés. Si vous avez précédemment créé des fichiers PDF protégés avec Azure RMS or AD RMS, utilisez Foxit Reader ou Nitro Pro pour continuer à lire ces fichiers sur des appareils Windows, iOS et Android.

-   **E-mail** : les clients de messagerie répertoriés peuvent protéger le message électronique proprement dit, ce qui a pour effet de protéger automatiquement tout fichier joint. Dans ce scénario, la fonctionnalité d’aperçu du client peut afficher le contenu protégé (message et pièce jointe) aux destinataires autorisés. Cependant, si une pièce jointe est protégée mais pas le message électronique qui la contient, la fonctionnalité d’aperçu du client ne peut pas afficher la pièce jointe protégée aux destinataires autorisés.

-   **Autres types de fichier** : les fichiers texte et image incluent les fichiers ayant une extension de nom de fichier .txt, .xml, .jpg et .jpeg. Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par Rights Management, puis passent en lecture seule. Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier .pfile une fois qu’ils sont protégés de manière générique par Rights Management. Pour plus d’informations, consultez [Types de fichiers pris en charge](../rms-client/client-admin-guide-file-types.md) dans le guide de l’administrateur du client Azure Information Protection.


|**Système d’exploitation de l’appareil**|Word, Excel, PowerPoint|PDF protégé|Courrier électronique|Autres types de fichiers|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Applications Office Mobile (Azure RMS uniquement) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Client Azure Information Protection pour Windows <br /><br />Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Application de partage RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Client Azure Information Protection pour Windows : texte, images, pfile<br /><br />Application de partage RMS pour Windows : texte, images, pfile<br /><br />Plug-in SealPath RMS pour AutoCAD [[8]](#footnote-8) : .dwg<br />|
|**iOS**|Office pour iPad et iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Docs TITUS|Application Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />Docs TITUS|Application Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Office pour iPad et iPhone [[4]](#footnote-4)<br /><br />OWA pour iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Application Azure Information Protection [[1]](#footnote-1) : texte, images<br /><br />Docs TITUS : Pfile|
|**Android**|GigaTrust App pour Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (Azure RMS uniquement)[[1]](#footnote-1)|Application Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App pour Android<br /><br />Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Application Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App pour Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook pour Android [[4]](#footnote-4)<br /><br />OWA pour Android [[3]](#footnote-3) et [[7]](#footnote-7)<br /><br />Samsung Email (S3 et versions ultérieures) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Application Azure Information Protection [[1]](#footnote-1) : texte, images|
|**OS X**|Office 2011 (AD RMS uniquement)<br /><br />Office 2016 pour Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|Outlook 2011 (AD RMS uniquement)<br /><br />Outlook 2016 pour Mac<br /><br />Outlook pour Mac|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Windows 10 Mobile**|Applications Office Mobile (Azure RMS uniquement) [[1]](#footnote-1)|Non prise en charge|Citrix WorxMail [[6]](#footnote-6)<br /><br />Courrier Outlook|Non prise en charge|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non pris en charge|Outlook 2013 RT<br /><br />Application de messagerie pour Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go : fichiers JT|
|**Windows Phone 8.1**|Office Mobile (AD RMS uniquement)|Application de partage RMS [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Blackberry 10**|Non prise en charge|Non pris en charge|Messagerie Blackberry [[4]](#footnote-4)|Non pris en charge|


###### <a name="footnote-1"></a>Note 1
Prend en charge l’affichage de contenu protégé.

###### <a name="footnote-2"></a>Note 2 
Prend en charge l’affichage des documents protégés quand un document non protégé est chargé dans une bibliothèque protégée dans SharePoint Online et OneDrive Entreprise. 

###### <a name="footnote-3"></a>Note 3
Si un destinataire reçoit un e-mail protégé et qu’il n’utilise pas Exchange comme serveur de messagerie, ou si l’émetteur appartient à une autre organisation, ce contenu ne peut être ouvert que dans un client de messagerie riche, comme Outlook. Ce contenu ne peut être ouvert à partir d’Outlook Web Access.

###### <a name="footnote-4"></a>Note 4
Utilise l’IRM Exchange ActiveSync, qui doit être activée par l’administrateur Exchange. Les utilisateurs peuvent afficher, répondre et répondre à tous pour les messages électroniques protégés, mais ne peuvent pas protéger eux-mêmes de nouveaux messages.

Si un destinataire reçoit un e-mail protégé et qu’il n’utilise pas Exchange comme serveur de messagerie, ou si l’émetteur appartient à une autre organisation, ce contenu ne peut être ouvert que dans un client de messagerie riche, comme Outlook. Ce contenu ne peut pas être ouvert à partir d’Outlook Web Access ou de clients de messagerie mobile via Exchange Active Sync IRM.

###### <a name="footnote-5"></a>Note 5
Prend en charge l’affichage et la modification de documents protégés pour iOS ; prend en charge l’affichage de documents protégés pour Android. Pour plus d’informations, consultez le billet suivant sur le blog Office : [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### <a name="footnote-6"></a>Note 6
Pour plus d’informations, consultez la [documentation produit Citrix pour WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

###### <a name="footnote-7"></a>Note 7
Pour plus d’informations, consultez le billet suivant sur le blog Office : [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

###### <a name="footnote-8"></a>Note 8
Pour plus d’informations, consultez le billet suivant sur le blog Enterprise and Mobility : [SealPath apporte une protection RMS à AutoCAD](https://blogs.technet.microsoft.com/enterprisemobility/2015/09/08/sealpath-brings-rms-protection-to-autocad/)


## <a name="more-information-about-azure-rms-support-for-office"></a>Plus d’informations sur la prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). Les éditions clientes Office suivantes prennent en charge la protection des fichiers et des e-mails à l’aide d’Azure RMS :

- Office 365 ProPlus : Office 2016 et Office 2013

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013

- Office Professionnel Plus 2010

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

Azure RMS avec Office Professionnel Plus 2010 ou Office Professionnel 2010 :

- Requiert le client Azure Information Protection pour Windows ou l’application de partage Rights Management pour Windows

- Non pris en charge sur Windows 10

- Ne prend pas en charge l’authentification basée sur les formulaires pour les comptes d’utilisateur fédéré. Ces comptes doivent utiliser l’authentification intégrée de Windows.

## <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Pour plus d’informations sur l’application Azure Information Protection pour iOS et Android

L’application Azure Information Protection pour iOS et Android remplace l’application de partage RMS pour ces appareils. Elle fournit les mêmes fonctionnalités et, en plus, prend en charge les e-mails protégés par des droits et les fichiers PDF protégés par des droits sur SharePoint Online.

Si vos appareils iOS et Android sont inscrits par Microsoft Intune, vous pouvez déployer et gérer cette application à l’aide d’une application gérée par une stratégie. Pour plus d’informations, consultez [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) dans la documentation Intune. Pour l’étape 2 de cette documentation Intune, suivez les instructions pour publier une application gérée par une stratégie.

Pour plus d’informations, consultez [FAQs for Azure Information Protection app for iOS and Android](../rms-client/mobile-app-faq.md) (Forum Aux Questions concernant l’application Azure Information Protection pour iOS et Android).


## <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Plus d’informations sur le client Azure Information Protection pour Windows

Ce client remplace désormais l’application de partage Rights Management pour Windows. 

Pour plus d'informations, consultez les ressources suivantes :

- [Client Azure Information Protection - Guide de l’administrateur](../rms-client/client-admin-guide.md)

- [Guide de l’utilisateur du client Azure Information Protection](../rms-client/client-user-guide.md)

- [FAQ relatifs à l’application Azure Information Protection pour iOS et Android](../rms-client/mobile-app-faq.md)

Téléchargez l’application correspondante à l’aide des liens de la [page Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="more-information-about-the-rights-management-sharing-application"></a>Plus d’informations sur l’application de partage Rights Management

Cette application est remplacée par le client Azure Information Protection. Elle reste requise pour les ordinateurs Mac et les appareils mobiles Windows Phone. 

Pour plus d'informations, consultez les ressources suivantes :

-   [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)

-   [FAQ relatif à l’application de partage Microsoft Rights Management pour plateformes mobiles](https://technet.microsoft.com/dn451248)

Télécharger l’application pour les ordinateurs Mac et Windows Phone en utilisant les liens sur la [page Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970).


## <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Plus d’informations sur les autres applications qui prennent en charge Azure Information Protection

En plus des applications indiquées dans le tableau, toute application qui prend en charge les API du service Azure Rights Management peut être intégrée à Azure Information Protection, notamment :

- Applications métier écrites en interne avec les SDK RMS

- Applications de fournisseurs de logiciels écrites avec les SDK RMS

Pour plus d’informations, consultez le [guide du développeur Azure Information Protection](../develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applications non prises en charge par Azure RMS

Les applications suivantes ne sont pas prises en charge actuellement par Azure RMS :

-   Microsoft Office pour Mac 2011

-   Microsoft OneDrive Entreprise pour SharePoint Server 2013

-   Visionneuse XPS
 
En outre, l’application de partage RMS et le client Azure Information Protection présente les restrictions suivantes :

-   Pour les ordinateurs Windows : nécessite au minimum la version Windows 7 Service Pack 1



## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements-azure-rms.md).

Pour plus d’informations sur la prise en charge d’Azure RMS par les applications les plus courantes, consultez [Comment les applications prennent en charge le service Azure Rights Management](../understand-explore/applications-support.md).

Pour plus d’informations sur la façon de configurer les applications les plus courantes pour Azure RMS, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
