---
title: Configuration requise pour Azure Information Protection (article complet)
description: "Identifiez les critères de déploiement d’Azure Information Protection pour votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2a5791dfd571091e8c9e510447b0a5b36818a8df
ms.sourcegitcommit: 17f593b099dddcbb1cf0422353d594ab964b2736
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="requirements-for-azure-information-protection"></a>Configuration requise pour Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*


Avant de déployer Azure Information Protection pour votre organisation, vérifiez que les conditions préalables suivantes sont respectées. 

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Un abonnement à Azure Information Protection|Examinez les [informations sur les abonnements](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) et la [liste des fonctionnalités](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) du site Azure Information Protection pour vérifier que l’abonnement de votre organisation inclut les fonctionnalités Azure Information Protection que vous voulez utiliser.|
|Azure Active Directory|Votre entreprise doit disposer d’Azure Active Directory afin de prendre en charge l’authentification utilisateur pour Azure Information Protection. De plus, si vous souhaitez utiliser les comptes d’utilisateur de votre annuaire local (AD DS), vous devez également configurer l’intégration d’annuaire.<br /><br />Si vos comptes sont fédérés (par exemple, si vous utilisez AD FS), ils doivent utiliser l’authentification intégrée Windows. L’authentification basée sur les formulaires n’est pas prise en charge pour Azure Information Protection.<br /><br />La solution d’authentification multifacteur (MFA) est prise en charge avec Azure Information Protection si vous disposez du logiciel client nécessaire et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.<br /><br />Pour plus d’informations, consultez [Configuration requise d’Azure Active Directory pour Azure Information Protection](requirements-azure-ad.md).|
|Appareils clients|Les utilisateurs doivent avoir des appareils clients (ordinateurs ou appareils mobiles) exécutant un système d’exploitation qui prend en charge Azure Information Protection.<br /><br />Les appareils suivants prennent en charge le client Azure Information Protection, qui permet aux utilisateurs de classer et d’étiqueter leurs e-mails et documents Office :<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quand ce client protège les données à l’aide du service Azure Rights Management, celles-ci peuvent être utilisées par les mêmes appareils (Windows, Mac, iOS, Android) que ceux qui prennent en charge le service Azure Rights Management. <br /><br />Pour plus d’informations sur les appareils qui prennent en charge le service Azure Rights Management, consultez [Appareils clients prenant en charge la protection des données Azure Rights Management](../get-started/requirements-client-devices.md).|
|Applications|Le client Azure Information Protection prend en charge l’étiquetage et la protection des fichiers et des e-mails créés par les applications Office suivantes : **Word**, **Excel**, **PowerPoint** et **Outlook** des suites Office suivantes :<br /><br />- Office Professionnel Plus 2016<br /><br />- Office Professionnel Plus 2013 avec Service Pack 1<br /><br />- Office Professionnel Plus 2010<br /><br />Pour plus d’informations sur les applications qui prennent en charge le service Azure Rights Management, consultez [Applications prenant en charge la protection des données Azure Rights Management](requirements-applications.md).|
|Infrastructure prenant en charge la connexion Internet et les services cloud dépendants|Si vous avez un pare-feu ou des périphériques réseau intervenants similaires qui doivent être configurés pour autoriser des connexions spécifiques, consultez les informations relatives à **Azure Rights Management (RMS)** dans la section [Portail et services partagés Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) de l’article Office suivant : [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Suivez les instructions fournies dans cet article Office pour être tenu au courant des modifications apportées à ces informations en vous abonnant à un flux RSS.<br /><br />En plus des informations de l’article relatif à Office, voici des informations propres à Azure Information Protection :<br /><br />- Autorisez le trafic HTTPS sur le port TCP 443 pour **api.informationprotection.azure.com**.<br /><br />- N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer une inspection au niveau du paquet). Cela a pour effet d’interrompre l’épinglage de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour sécuriser leur communication avec Azure RMS.<br /><br />- Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer de manière à utiliser l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.|

Si vous souhaitez utiliser le service Azure Rights Management d’Azure Information Protection avec des serveurs locaux, les produits pris en charge sont les suivants :

-   Exchange Server

-   SharePoint Server

-   Serveurs de fichiers Windows Server prenant en charge l’infrastructure de classification des fichiers

Pour plus d’informations sur les conditions requises supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge la protection des données Azure Rights Management](requirements-servers.md).

> [!IMPORTANT]
> Le scénario de déploiement suivant n’est pas pris en charge, sauf si vous utilisez la protection AD RMS avec Azure Information Protection (la configuration HYOK ou « conservez votre propre clé ») :
> 
> -   En cas d’exécution d’AD RMS et d’Azure RMS côte à côte dans la même organisation, sauf pendant la migration, comme décrit dans la rubrique [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> Il existe un chemin de migration pris en charge [d’AD RMS vers Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) et [Azure Information Protection vers AD RM](http://msdn.microsoft.com/library/azure/dn629429.aspx). Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](../deploy-use/decommission-deactivate.md).

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Configuration requise d’Azure Active Directory pour Azure Information Protection

Vous avez besoin d’un annuaire Azure AD pour utiliser Azure Information Protection. Vous devez utiliser le compte de votre organisation correspondant à cet annuaire pour vous connecter au portail Azure Classic, où vous pouvez, par exemple, configurer et gérer les modèles Rights Management.

Si vous n’avez pas encore d’abonnement Azure pour votre organisation, vous pouvez en obtenir un en vous inscrivant pour une évaluation gratuite : accédez à la page [Prise en main d’Azure](https://account.windowsazure.com/organization) et suivez les instructions.

Pour plus d’informations, consultez les ressources suivantes dans la documentation Azure Active Directory :

-   [Qu’est-ce qu’Azure AD Directory ?](/active-directory/active-directory-whatis)

-   [Comment les abonnements Azure sont-ils associés à Azure Active Directory ?](/active-directory/active-directory-how-subscriptions-associated-directory)

Si vous souhaitez intégrer votre annuaire Azure AD à vos forêts AD locales, consultez [Intégration de vos identités locales avec Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Si vous avez des appareils mobiles ou des ordinateurs Mac qui s'authentifient localement par le biais des services AD FS ou d'un fournisseur d'authentification équivalent :
> 
> -   Vous devez utiliser les services AD FS sur la version serveur minimale de **Windows Server 2012 R2** ou un autre fournisseur d’authentification prenant en charge le protocole OAuth 2.0.

### <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Authentification multifacteur (MFA) et Azure Information Protection
Pour utiliser l’authentification multifacteur (MFA) avec Azure Information Protection, vous devez avoir au moins l’un des éléments suivants :

-   Office 2013 (version minimale) :

    -   Si vous avez Office 2013, vous devez également installer la [mise à jour du 9 juin 2015 pour Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Pour plus d’informations sur cette mise à jour et la manière dont l’authentification moderne introduit la connexion basée sur Azure Active Directory Authentication Library (ADAL) à Office 2013, consultez [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sur le blog Office.

-   Application de partage Rights Management pour Windows :

    -   Vous devez avoir installé la version minimale 1.0.1908.0, ce que vous pouvez vérifier dans la rubrique Programmes et fonctionnalités du Panneau de configuration. Pour plus d’informations sur l’application de partage, consultez [Application de partage Rights Management pour Windows](../rms-client/sharing-app-windows.md).

-   Application de partage Rights Management pour appareils mobiles et ordinateurs Mac :

    -   Assurez-vous que vous avez installé la dernière version. La prise en charge de MFA a été introduite dans la version de septembre 2015 de l’application de partage RMS.

Ensuite, configurez votre solution MFA :

-   Pour les clients gérés par Microsoft (disposant d’Azure Active Directory ou d’Office 365) :

    -   Configurez Azure MAF pour appliquer l’authentification MFA aux utilisateurs. Pour obtenir des instructions, consultez [Prise en main avec Azure Multi-Factor Authentication dans le cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) dans la documentation sur Azure.

        Pour plus d’informations sur l’authentification multifacteur Azure, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](/multi-factor-authentication/multi-factor-authentication).

-   Pour les clients fédérés (utilisant des serveurs de fédération locaux) :

    -   Configurez vos serveurs de fédération pour Azure Active Directory ou Office 365. Par exemple, si vous utilisez les services AD FS, consultez [Configurer des méthodes d’authentification supplémentaires pour AD FS](https://technet.microsoft.com/library/dn758113.aspx) sur TechNet.

        Pour plus d’informations sur ce scénario, consultez [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sur le blog Office.

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>Appareils clients prenant en charge la protection des données Azure Rights Management

Consultez les sections suivantes pour identifier les appareils prenant en charge le service Azure Rights Management, qui assure la protection des données pour Azure Information Protection.

### <a name="computers"></a>Ordinateurs
Les systèmes d’exploitation d’ordinateur suivants prennent en charge le service Azure Rights Management :

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X** : version minimale Mac OS X 10.8 (Mountain Lion)

### <a name="mobile-devices"></a>Appareils mobiles
Les systèmes d’exploitation d’appareils mobiles suivants prennent en charge le service Azure Rights Management :

-   **Windows Phone** : Windows Phone 8.1

-   **Téléphones et tablettes Android** : version minimale Android 4.0.3

-   **iPhone et iPad** : version minimale iOS 7.0

-   **Tablettes Windows** : Windows Mobile 10 et Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>Applications prenant en charge la protection des données Azure Rights Management

Consultez le tableau suivant pour identifier les applications prenant en charge le service Azure Rights Management (Azure RMS) en mode natif, qui assure la protection des données pour Azure Information Protection. 

Pour ces applications, la prise en charge de Rights Management est étroitement intégrée à l’aide des API Rights Management pour prendre en charge les restrictions d’utilisation. Ces applications sont également appelées « applications compatibles avec RMS ».

Sauf indication contraire, les fonctionnalités prises en charge s’appliquent à Azure RMS et à AD RMS. Par ailleurs, la prise en charge d’AD RMS sur iOS, Android, OS X et Windows Phone 8.1 nécessite [Active Directory Rights Management Services Mobile Device Extension](https://technet.microsoft.com/library/dn673574.aspx).

Informations sur les colonnes du tableau :

-   **PDF protégé** : fichiers avec l’extension de nom de fichier .ppdf qui sont créés automatiquement quand vous utilisez l’application de partage RMS pour partager des fichiers Office et des fichiers PDF par e-mail. L’application de partage RMS et l’application Azure Information Protection pour iOS et Android comprennent un lecteur de fichiers PDF protégés. Si vous avez précédemment créé des fichiers PDF protégés avec Azure RMS or AD RMS, utilisez Foxit Reader ou Nitro Pro pour continuer à lire ces fichiers sur des appareils Windows, iOS et Android.

-   **E-mail** : les clients de messagerie répertoriés peuvent protéger le message électronique proprement dit, ce qui a pour effet de protéger automatiquement tout fichier joint. Dans ce scénario, la fonctionnalité d’aperçu du client peut afficher le contenu protégé (message et pièce jointe) aux destinataires autorisés. Cependant, si une pièce jointe est protégée mais pas le message électronique qui la contient, la fonctionnalité d’aperçu du client ne peut pas afficher la pièce jointe protégée aux destinataires autorisés.

-   **Autres types de fichier** : les fichiers texte et image incluent les fichiers ayant une extension de nom de fichier .txt, .xml, .jpg et .jpeg. Ces fichiers changent d’extension de nom de fichier une fois qu’ils sont protégés en mode natif par Rights Management, puis passent en lecture seule. Les fichiers qui ne peuvent pas être protégés en mode natif ont une extension de nom de fichier .pfile une fois qu’ils sont protégés de manière générique par Rights Management. Pour plus d’informations, consultez le [guide d’administration de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).


|**Système d’exploitation de l’appareil**|Word, Excel, PowerPoint|PDF protégé|E-mail|Autres types de fichiers|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Applications Office Mobile (Azure RMS uniquement) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />Client PDF GigaTrust Desktop pour Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />Application de partage RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Application de partage RMS pour Windows : texte, images, pfile<br /><br />Siemens JT2Go : fichiers JT (Windows 10 uniquement)|
|**iOS**|Office pour iPad et iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />Docs TITUS|Application Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />Docs TITUS|Application Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Office pour iPad et iPhone [[4]](#footnote-4)<br /><br />OWA pour iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Application Azure Information Protection [[1]](#footnote-1) : texte, images<br /><br />Docs TITUS : Pfile|
|**Android**|GigaTrust App pour Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (Azure RMS uniquement)[[1]](#footnote-1)|Application Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App pour Android<br /><br />Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Application Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App pour Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook pour Android [[4]](#footnote-4)<br /><br />OWA pour Android [[3]](#footnote-3) et [[7]](#footnote-7)<br /><br />Samsung Email (S3 et versions ultérieures) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Application Azure Information Protection [[1]](#footnote-1) : texte, images|
|**OS X**|Office 2011 (AD RMS uniquement)<br /><br />Office 2016 pour Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />Application de partage RMS [[1]](#footnote-1)|Outlook 2011 (AD RMS uniquement)<br /><br />Outlook 2016 pour Mac<br /><br />Outlook pour Mac|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Windows 10 Mobile**|Applications Office Mobile (Azure RMS uniquement)[[1]](#footnote-1)|Non pris en charge|Citrix WorxMail [[6]](#footnote-6)<br /><br />Courrier Outlook|Non prise en charge|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non pris en charge|Outlook 2013 RT<br /><br />Application de messagerie pour Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go : fichiers JT|
|**Windows Phone 8.1**|Office Mobile (AD RMS uniquement)|Application de partage RMS [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|Application de partage RMS [[1]](#footnote-1) : texte, images, pfile|
|**Blackberry 10**|Non prise en charge|Non pris en charge|Messagerie Blackberry [[4]](#footnote-4)|Non pris en charge|


##### <a name="footnote-1"></a>Note 1
Prend en charge l’affichage de contenu protégé.

##### <a name="footnote-2"></a>Note 2 
Prend en charge l’affichage des documents protégés quand un document non protégé est chargé dans une bibliothèque protégée dans SharePoint Online et OneDrive Entreprise. 

##### <a name="footnote-3"></a>Note 3
Si un destinataire reçoit un e-mail protégé et qu’il n’utilise pas Exchange comme serveur de messagerie, ou si l’émetteur appartient à une autre organisation, ce contenu ne peut être ouvert que dans un client de messagerie avancé, comme Outlook. Ce contenu ne peut être ouvert à partir d’Outlook Web Access.

##### <a name="footnote-4"></a>Note 4
Utilise l’IRM Exchange ActiveSync, qui doit être activée par l’administrateur Exchange. Les utilisateurs peuvent afficher, répondre et répondre à tous pour les e-mails protégés, mais ne peuvent pas protéger eux-mêmes de nouveaux e-mails.

Si un destinataire reçoit un e-mail protégé et qu’il n’utilise pas Exchange comme serveur de messagerie, ou si l’émetteur appartient à une autre organisation, ce contenu ne peut être ouvert que dans un client de messagerie avancé, comme Outlook. Ce contenu ne peut pas être ouvert à partir d’Outlook Web Access ou de clients de messagerie mobile via Exchange Active Sync IRM.

##### <a name="footnote-5"></a>Note 5
Prend en charge l’affichage et l’édition de documents protégés. Pour plus d’informations, consultez le billet suivant sur le blog Office : [Azure Rights Management support comes to Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### <a name="footnote-6"></a>Note 6
Pour plus d’informations, consultez la [documentation produit Citrix pour WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

##### <a name="footnote-7"></a>Note 7
Pour plus d’informations, consultez le billet suivant sur le blog Office : [OWA for Android now available on select devices](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## <a name="more-information-about-azure-rms-support-for-office"></a>Plus d’informations sur la prise en charge d’Azure RMS pour Office

Azure RMS est étroitement intégré aux applications Word, Excel, PowerPoint et Outlook, où cette fonctionnalité est souvent appelée Gestion des droits relatifs à l’information (IRM). Les éditions clientes Office suivantes prennent en charge la protection des fichiers et des e-mails à l’aide d’Azure RMS :

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013

- Office Professionnel Plus 2010

Toutes les éditions d’Office (à l’exception d’Office 2007) prennent en charge l’utilisation du contenu protégé.

Azure RMS avec Office Professionnel Plus 2010 ou Office Professionnel 2010 :

- Requiert l’application de partage Rights Management pour Windows

- Non pris en charge sur Windows 10

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Pour plus d’informations sur l’application Azure Information Protection pour iOS et Android

L’application Azure Information Protection pour iOS et Android remplace l’application de partage RMS pour ces appareils. Elle fournit les mêmes fonctionnalités et, en plus, prend en charge les e-mails protégés par des droits et les fichiers PDF protégés par des droits sur SharePoint Online.

Si vos appareils iOS et Android sont inscrits par Microsoft Intune, vous pouvez déployer et gérer cette application à l’aide d’une application gérée par une stratégie. Pour plus d’informations, consultez [Configurer et déployer des stratégies de gestion des applications mobiles dans la console Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) dans la documentation Intune. Pour l’étape 2 de cette documentation Intune, suivez les instructions pour publier une application gérée par une stratégie.

Pour plus d’informations, consultez [FAQs for Azure Information Protection app for iOS and Android](../rms-client/mobile-app-faq.md) (Forum Aux Questions concernant l’application Azure Information Protection pour iOS et Android).


### <a name="more-information-about-the-rights-management-sharing-application"></a>Plus d’informations sur l’application de partage Rights Management

Pour plus d’informations sur l’application de partage Rights Management pour Windows, reportez-vous aux ressources suivantes :

-   [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)

Pour plus d’informations sur l’application de partage Rights Management pour plateformes mobiles, reportez-vous aux ressources suivantes :

-   Téléchargez l’application correspondante à l’aide des liens de la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   [FAQ relatif à l’application de partage Microsoft Rights Management pour plateformes mobiles](https://technet.microsoft.com/dn451248)

> [!NOTE]
> L’application de partage RMS pour iOS et Android est maintenant remplacée par l’application Azure Information Protection.

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>Plus d’informations sur les autres applications qui prennent en charge Azure RMS

Outre les applications mentionnées dans le tableau, toute application prenant en charge ces API RMS peut être intégrée à Azure RMS, notamment :

- Applications métier écrites en interne avec le RMS SDK

- Applications de fournisseurs de logiciels écrites avec le RMS SDK

Pour plus d’informations sur le SDK, consultez [Microsoft Rights Management SDK](../develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Applications non prises en charge par Azure RMS

Les applications suivantes ne sont pas prises en charge actuellement par Azure RMS :

-   Microsoft Office pour Mac 2011

-   Microsoft OneDrive Entreprise pour SharePoint Server 2013

-   Visionneuse XPS
 
De plus, l’application de partage RMS présente les restrictions suivantes :

-   Pour les ordinateurs Windows : nécessite au minimum la version Windows 7 Service Pack 1

## <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Serveurs locaux prenant en charge la protection des données Azure Rights Management

Les produits de serveurs locaux suivants sont pris en charge avec Azure Information Protection quand vous utilisez le connecteur Azure Rights Management. Ce connecteur fait office d’interface de communication (relais) entre les serveurs locaux et le service Azure Rights Management utilisé par Azure Information Protection pour protéger les e-mails et les documents Office. 

Pour utiliser ce connecteur, vous devez configurer la synchronisation des annuaires entre vos forêts Active Directory et Azure Active Directory.

-   **Exchange Server** :

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server** :

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)** :

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Les serveurs de fichiers qui exécutent Windows Server 2008 R2 n’ont pas d’action de tâche de gestion de fichiers intégrée pour appliquer la protection de Rights Management. Par conséquent, vous ne pouvez pas utiliser le connecteur Rights Management pour ce scénario. En revanche, vous pouvez utiliser l’infrastructure de classification des fichiers et Azure RMS sur ces systèmes d’exploitation si vous configurez une tâche de gestion de fichiers personnalisée de sorte qu’elle exécute un exécutable ou un script capable de protéger les fichiers à l’aide d’Azure RMS. Par exemple, un script Windows PowerShell qui utilise les [applets de commande de protection RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Vous pouvez également utiliser ces applets de commande avec des serveurs exécutant des versions ultérieures de Windows Server, l’avantage étant que ces applets de commande peuvent protéger tous les types de fichiers. Le connecteur RMS protège uniquement les fichiers Office. Pour obtenir des instructions, consultez [Protection RMS avec l’Infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](../rms-client/configure-fci.md).

Le connecteur Rights Management est pris en charge sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.

Pour plus d’informations sur la configuration du connecteur Rights Management pour ces serveurs locaux, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
