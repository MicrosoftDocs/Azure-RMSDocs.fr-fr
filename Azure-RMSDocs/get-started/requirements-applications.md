---
title: "Conditions requises pour Azure RMS : Applications | Azure RMS"
description: "Utilisez le tableau suivant pour identifier les applications qui prennent en charge Azure RMS en mode natif. RMS est étroitement intégré à ces applications grâce à l’utilisation d’API RMS pour la prise en charge des restrictions d’utilisation. Ces applications sont également appelées « applications compatibles avec RMS »."
author: cabailey
manager: mbaldwin
ms.date: 08/19/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: d3408f954381978287852dd74a38c5903f583dda


---


# Conditions requises pour Azure RMS : Applications

>*S’applique à : Azure Rights Management, Office 365*


Utilisez le tableau suivant pour identifier les applications qui prennent en charge Azure RMS en mode natif. RMS est étroitement intégré à ces applications grâce à l’utilisation d’API RMS pour la prise en charge des restrictions d’utilisation. Ces applications sont également appelées « applications compatibles avec RMS ».

Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. Par ailleurs, la prise en charge d’AD RMS sur iOS, Android, OS X et Windows Phone 8.1 nécessite [Active Directory Rights Management Services Mobile Device Extension](https://technet.microsoft.com/library/dn673574.aspx).

Informations sur les colonnes du tableau :

-   **PDF protégé** : fichiers avec l’extension de nom de fichier .ppdf qui sont créés automatiquement quand vous utilisez l’application de partage RMS pour partager des fichiers Office et des fichiers PDF par e-mail. L’application de partage RMS comprend un lecteur de fichiers PDF protégés. Si vous avez précédemment créé des fichiers PDF protégés avec Azure RMS or AD RMS, utilisez Foxit Reader ou Nitro Pro pour continuer à lire ces fichiers sur des appareils Windows, iOS et Android.

-   **E-mail** : les clients de messagerie répertoriés peuvent protéger le message électronique proprement dit, ce qui a pour effet de protéger automatiquement tout fichier joint. Dans ce scénario, la fonctionnalité d’aperçu du client peut afficher le contenu protégé (message et pièce jointe) aux destinataires autorisés. Cependant, si une pièce jointe est protégée mais pas le message électronique qui la contient, la fonctionnalité d’aperçu du client ne peut pas afficher la pièce jointe protégée aux destinataires autorisés.

-   **Autres types de fichier** : les fichiers texte et image incluent les fichiers ayant une extension de nom de fichier .txt, .xml, .jpg et jpeg. Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par RMS et ils basculent en lecture seule. Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier .pfile une fois qu’ils sont protégés de manière générique par RMS. Pour plus d’informations, consultez le [guide d’administration de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).


|**Système d’exploitation de l’appareil**|Word, Excel, PowerPoint|PDF protégé|Courrier électronique|Autres types de fichiers|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Applications Office Mobile (Azure RMS uniquement) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Application de partage RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Application de partage RMS pour Windows : texte, images, pfile<br /><br />Siemens JT2Go : fichiers JT (Windows 10 uniquement)|
|**iOS**|Office pour iPad et iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Docs TITUS|Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)<br /><br />Docs TITUS|Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Office pour iPad et iPhone [[4]](#footnote-4)<br /><br />OWA pour iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile<br /><br />Docs TITUS : Pfile|
|**Android**|GigaTrust App pour Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (Azure RMS uniquement)[[1]](#footnote-1)|GigaTrust App pour Android<br /><br />Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App pour Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook pour Android [[4]](#footnote-4)<br /><br />OWA pour Android [[3]](#footnote-3) et [[7]](#footnote-7)<br /><br />Samsung Email (S3 et versions ultérieures) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**OS X**|Office 2011 (AD RMS uniquement)<br /><br />Office 2016 pour Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|Outlook 2011 (AD RMS uniquement)<br /><br />Outlook 2016 pour Mac<br /><br />Outlook pour Mac|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Windows 10 Mobile**|Applications Office Mobile (Azure RMS uniquement)[[1]](#footnote-1)|Non pris en charge|Citrix WorxMail [[6]](#footnote-6)<br /><br />Courrier Outlook|Non pris en charge|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non pris en charge|Outlook 2013 RT<br /><br />Application de messagerie pour Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go : fichiers JT|
|**Windows Phone 8.1**|Office Mobile (AD RMS uniquement)|Application de partage RMS [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Blackberry 10**|Non pris en charge|Non pris en charge|Messagerie Blackberry [[4]](#footnote-4)|Non pris en charge|


###### Note 1
Prend en charge l’affichage de contenu protégé.

###### Note 2 
Prend en charge l’affichage de contenu protégé dans SharePoint Online, OneDrive Entreprise et Outlook Web Access.

###### Note 3
Si un destinataire possédant une boîte aux lettres Exchange sur site reçoit un message électronique protégé, il ne peut ouvrir ce contenu que dans un client de messagerie riche, tel qu’Outlook.  Ce contenu ne peut être ouvert à partir d’Outlook Web Access.

###### Note 4
Utilise l’IRM Exchange ActiveSync, qui doit être activée par l’administrateur Exchange. Les utilisateurs peuvent afficher, répondre et répondre à tous pour les messages électroniques protégés, mais ne peuvent pas protéger eux-mêmes de nouveaux messages.

Si un destinataire possédant une boîte aux lettres Exchange sur site reçoit un message électronique protégé en provenance d’une autre organisation utilisant Exchange, il ne peut ouvrir ce contenu que dans un client de messagerie riche, tel qu’Outlook.  Ce contenu ne peut être ouvert à partir sur un appareil utilisant l’IRM Exchange ActiveSync.

###### Note 5
Prend en charge l’affichage et l’édition de documents protégés. Pour plus d’informations, consultez le billet suivant sur le blog Office : [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### Note 6
Pour plus d’informations, consultez la [documentation produit Citrix pour WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

###### Note 7
Pour plus d’informations, consultez le billet suivant sur le blog Office : [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Plus d’informations sur la prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). Les éditions clientes Office suivantes prennent en charge la protection des fichiers et des e-mails à l’aide d’Azure RMS :

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013

- Office Professionnel Plus 2010

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

Azure RMS avec Office Professionnel Plus 2010 ou Office Professionnel 2010 :

- Requiert l’application de partage Rights Management pour Windows

- Non pris en charge sur Windows 10


## Plus d’informations sur l’application de partage Rights Management

Pour plus d’informations sur l’application de partage Rights Management pour Windows, reportez-vous aux ressources suivantes :

-   [Guide de l'administrateur de l'application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)

Pour plus d’informations sur l’application de partage Rights Management pour plateformes mobiles, reportez-vous aux ressources suivantes :

-   Téléchargez l’application correspondante en utilisant les liens figurant dans la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   Si vous avez Microsoft Intune, vous pouvez déployer et gérer l’application à l’aide d’une application gérée par une stratégie : 

    -   Pour les appareils iOS et Android inscrits par Intune : [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)

    -   Pour les appareils Android qui ne sont pas inscrits par Intune : [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)

-   [FAQ relatif à l'application de partage Microsoft Rights Management pour plateformes mobiles](https://technet.microsoft.com/dn451248)



## Plus d’informations sur les autres applications qui prennent en charge Azure RMS

Outre les applications mentionnées dans le tableau, toute application prenant en charge ces API RMS peut être intégrée à Azure RMS, notamment :

- Applications métier écrites en interne avec le RMS SDK

- Applications de fournisseurs de logiciels écrites avec le RMS SDK

Pour plus d’informations sur le SDK, consultez [Microsoft Rights Management SDK](../develop/developers-guide.md).

## Applications non prises en charge par Azure RMS

Les applications suivantes ne sont pas prises en charge actuellement par Azure RMS :

-   Microsoft Office pour Mac 2011

-   Microsoft OneDrive Entreprise pour SharePoint Server 2013

-   Visionneuse XPS
 
De plus, l’application de partage RMS présente les restrictions suivantes :

-   Pour les ordinateurs Windows : nécessite au minimum la version Windows 7 Service Pack 1



## Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Conditions requises pour Azure Rights Management](requirements-azure-rms.md).

Pour plus d’informations sur la prise en charge d’Azure RMS par les applications les plus courantes, consultez [Mode de prise en charge d’Azure Rights Management par les applications](../understand-explore/applications-support.md).

Pour plus d’informations sur la façon de configurer les applications les plus courantes pour Azure RMS, consultez [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).


<!--HONumber=Aug16_HO4-->


