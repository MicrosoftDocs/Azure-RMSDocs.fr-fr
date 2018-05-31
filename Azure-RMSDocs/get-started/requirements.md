---
title: Configuration requise pour Azure Information Protection
description: Identifiez les critères de déploiement d’Azure Information Protection pour votre organisation.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/18/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9cdb205488c300f1df1e002be105765a90ce1a1a
ms.sourcegitcommit: 09072591f1aa9878d063feb78ffcc4accec63fd1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/18/2018
ms.locfileid: "34308169"
---
# <a name="requirements-for-azure-information-protection"></a>Configuration requise pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Avant de déployer Azure Information Protection pour votre organisation, vérifiez que les conditions préalables suivantes sont respectées. 

## <a name="subscription-for-azure-information-protection"></a>Abonnement à Azure Information Protection

**Pour la classification, l’étiquetage et la protection** : vous devez avoir un plan [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). 

**Pour la protection uniquement** : vous devez avoir un [plan Office 365 incluant Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Pour vérifier que l’abonnement de votre organisation inclut les fonctionnalités Azure Information Protection que vous voulez utiliser, passez en revue la liste des fonctionnalités à partir de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

> [!TIP]
> Vous voulez savoir si votre plan Office 365 ou Exchange Online autonome prend en charge les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) pour envoyer des e-mails protégés à des adresses e-mail personnelles ? Par exemple, Gmail, Yahoo et Microsoft. Consultez les ressources suivantes :
>
> [Description du service Exchange Online](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> [Office 365 Éducation](https://technet.microsoft.com/library/mt844095.aspx)
>
> [Office 365 US Government](https://technet.microsoft.com/library/mt774581.aspx)

Si vous avez des questions sur les abonnements ou les licences, ne les publiez pas sur cette page, mais contactez votre responsable de compte Microsoft ou le [support Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Votre organisation doit disposer d’un annuaire Azure AD (Azure Active Directory) afin de prendre en charge l’authentification utilisateur et l’autorisation pour Azure Information Protection. De plus, si vous souhaitez utiliser les comptes d’utilisateur de votre annuaire local (AD DS), vous devez également configurer l’intégration d’annuaire.

L’authentification unique (SSO) étant prise en charge pour Azure Information Protection, les utilisateurs ne sont pas invités de manière répétée à fournir leurs informations d’identification. Si vous utilisez une autre solution de fournisseur pour la fédération, vérifiez auprès de ce dernier comment la configurer pour Azure AD. WS-Trust est une exigence courante pour ces solutions afin de prendre en charge l’authentification unique. 

La solution d’authentification multifacteur (MFA) est prise en charge avec Azure Information Protection si vous disposez du logiciel client nécessaire et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.

L’accès conditionnel est pris en charge en préversion pour les documents protégés par Azure Information Protection. Pour plus d’informations, consultez la question suivante du FAQ : [Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Pour plus d’informations sur les conditions d’authentification, consultez [Configuration requise d’Azure Active Directory pour Azure Information Protection](requirements-azure-ad.md). 

Pour plus d’informations sur la configuration requise pour les comptes d’utilisateur et de groupe pour l’autorisation, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](../plan-design/prepare.md).

## <a name="client-devices"></a>Appareils clients

Les utilisateurs doivent avoir des appareils clients (ordinateurs ou appareils mobiles) exécutant un système d’exploitation qui prend en charge Azure Information Protection.

Les appareils suivants prennent en charge le client Azure Information Protection, qui permet aux utilisateurs de classer et d’étiqueter leurs e-mails et leurs documents :

- Windows 10 (x86, x64)
    
    - Aucune prise en charge de l’écriture manuscrite dans la build Windows 10 RS4 pour les Insiders. 

- Windows 8.1 (x86, x64)

- Windows 8 (x86, x64)

- Windows 7 Service Pack 1 (x86, x64)

- Windows Server 2016 

- Windows Server 2012 R2 et Windows Server 2012

- Windows Server 2008 R2 

Pour les versions de serveur répertoriées, le client Azure Information Protection est pris en charge pour les Services Bureau à distance. Si vous supprimez des profils utilisateur quand vous utilisez le client Azure Information Protection avec les Services Bureau à distance, ne supprimez pas le dossier **%Appdata%\Microsoft\Protect**.

Quand le client Azure Information Protection protège les données à l’aide du service Azure Rights Management, ces données peuvent être utilisées par les [mêmes appareils](requirements-client-devices.md) que ceux qui prennent en charge le service Azure Rights Management.

## <a name="applications"></a>Applications

Le client Azure Information Protection peut étiqueter et protéger les documents et les e-mails à l’aide des applications Office **Word**, **Excel**, **PowerPoint** et **Outlook** des éditions Office suivantes :

- Office 365 ProPlus avec des applications 2016 ou 2013 (« Démarrer en un clic » ou installation basée sur Windows Installer)
    
    Ces éditions d’Office sont proposées dans la plupart (mais pas dans la totalité) des abonnements Office 365 qui incluent la protection des données à partir d’Azure Information Protection. Vérifiez vos informations d’abonnement pour voir si Office 365 ProPlus est inclus. Vous trouverez également ces informations dans la [feuille de données Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013 avec Service Pack 1

- Office Professionnel Plus 2010 avec Service Pack 2

Les autres éditions d’Office ne peuvent pas protéger les documents et messages électroniques à l’aide d’un service Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour la classification uniquement. Par conséquent, les étiquettes qui appliquent la protection ne s’affichent pas aux utilisateurs sur la barre Azure Information Protection ni à partir du bouton **Protéger** du ruban Office. 

Le client Azure Information Protection ne prend pas en charge plusieurs versions d’Office sur le même ordinateur. Ce client ne prend pas non plus en charge le changement de comptes d’utilisateur dans Office.

Pour plus d’informations sur les éditions d’Office qui prennent en charge le service de protection des données, consultez [Applications prenant en charge la protection des données Azure Rights Management](requirements-applications.md).

## <a name="firewalls-and-network-infrastructure"></a>Pare-feu et infrastructure réseau

Si vous avez un pare-feu ou des périphériques réseau intervenants similaires configurés pour autoriser des connexions spécifiques, consultez les informations relatives à **Azure Rights Management (RMS)** dans la section [Portail et services partagés Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) de l’article Office suivant : [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Suivez les instructions fournies dans cet article Office pour être tenu au courant des modifications apportées à ces informations en vous abonnant à un flux RSS.

En plus des informations de l’article relatif à Office, voici des informations propres à Azure Information Protection :

- Autorisez le trafic HTTPS sur le port TCP 443 pour **api.informationprotection.azure.com**.

- Autorisez le trafic HTTPS sur le port TCP 443 pour **mobile.pipe.aria.microsoft.com**.

- Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer pour qu’il utilise l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.

- N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer une inspection au niveau du paquet) dans le service Azure Rights Management. Cela a pour effet d’interrompre l’épinglage de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour sécuriser leur communication avec le service Azure Rights Management.
    
    - Conseil : en raison de la façon dont Chrome affiche les connexions sécurisées dans la barre d’adresses, vous pouvez utiliser ce navigateur pour vérifier rapidement si la connexion de votre client est terminée avant d’atteindre le service Azure Rights Management. Dans la barre d’adresse du navigateur, entrez l’URL suivante : `https://admin.na.aadrm.com/admin/admin.svc` 
    
        Ne vous inquiétez pas de ce qu’affiche la fenêtre du navigateur. Cliquez sur le verrou dans la barre d’adresses pour afficher les informations du site. Les informations du site vous permettent de voir l’autorité de certification (CA) émettrice. Si le certificat n’est pas émis par une Autorité de certification Microsoft, il est très probable que votre connexion client-à-service sécurisée s’arrête et nécessite une reconfiguration sur votre pare-feu. L’image suivante illustre un exemple d’une autorité de certification Microsoft. Si vous constatez qu’une autorité de certification interne a émis le certificat, cette configuration n’est pas compatible avec Azure Information Protection.
        
        ![Vérification du certificat émis pour les connexions Azure Information Protection](../media/certificate-checking.png)

### <a name="on-premises-servers"></a>Serveurs locaux

Si vous souhaitez utiliser le service Azure Rights Management d’Azure Information Protection avec des serveurs locaux, les produits pris en charge sont les suivants :

- Exchange Server

- SharePoint Server

- Serveurs de fichiers Windows Server prenant en charge l’infrastructure de classification des fichiers

Pour plus d’informations sur les conditions requises supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge la protection des données Azure Rights Management](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coexistence d’AD RMS et Azure RMS

Le scénario de déploiement suivant n’est pas pris en charge, sauf si vous utilisez AD RMS pour la [protection HYOK](../deploy-use/configure-adrms-restrictions.md) avec Azure Information Protection (la configuration « conservez votre propre clé ») :

- En cas d’exécution d’AD RMS et d’Azure RMS côte à côte dans la même organisation, sauf pendant la migration, comme décrit dans [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

Il existe un chemin de migration pris en charge [d’AD RMS vers Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) et [Azure Information Protection vers AD RM](/powershell/module/aadrm/Set-AadrmMigrationUrl). Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](../deploy-use/decommission-deactivate.md).


[!INCLUDE[Commenting house rules](../includes/houserules.md)]


