---
title: Configuration requise pour Azure Information Protection - AIP
description: Identifiez les critères de déploiement d’Azure Information Protection pour votre organisation.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: fc76b7da1f687ab9876a6831539bf515df59aea1
ms.sourcegitcommit: 9221a0a9f3862739446b9027931a05023e0d5fc3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68286999"
---
# <a name="requirements-for-azure-information-protection"></a>Configuration requise pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Avant de déployer Azure Information Protection pour votre organisation, vérifiez que les conditions préalables suivantes sont respectées. 

## <a name="subscription-for-azure-information-protection"></a>Abonnement à Azure Information Protection

**Pour la classification, l’étiquetage et la protection** : Vous devez disposer d’un [plan Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). 

**Pour la protection uniquement** : vous devez disposer d’un [plan Office 365 incluant Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Pour vérifier que l’abonnement de votre organisation inclut les fonctionnalités Azure Information Protection que vous voulez utiliser, passez en revue la liste des fonctionnalités à partir de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Si vous avez des questions sur les licences, lisez le [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

> [!TIP]
> Vous voulez savoir si votre plan Office 365 ou Exchange Online autonome prend en charge les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) pour envoyer des e-mails protégés à des adresses e-mail personnelles ? Par exemple, Gmail, Yahoo et Microsoft. Consultez les ressources suivantes :
>
> - [Description du service Exchange Online](https://technet.microsoft.com/library/exchange-online-service-description.aspx)
>
> - [Office 365 Éducation](https://technet.microsoft.com/library/mt844095.aspx)
>
> - [Office 365 US Government](https://technet.microsoft.com/library/mt774581.aspx)

Si vous avez des questions sur les abonnements ou les licences, ne les postez pas sur cette page. Regardez plutôt si vous trouvez des réponses dans le [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences. Si aucune réponse n’existe à votre question, contactez votre responsable de compte Microsoft ou le [Support Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Votre organisation doit disposer d’un annuaire Azure AD (Azure Active Directory) afin de prendre en charge l’authentification utilisateur et l’autorisation pour Azure Information Protection. De plus, si vous souhaitez utiliser vos comptes d’utilisateur à partir de votre annuaire local (AD DS), vous devez également configurer une intégration d’annuaire.

L’authentification unique (SSO) étant prise en charge pour Azure Information Protection, les utilisateurs ne sont pas invités de manière répétée à fournir leurs informations d’identification. Si vous utilisez une autre solution de fournisseur pour la fédération, vérifiez auprès de ce dernier comment la configurer pour Azure AD. WS-Trust est une exigence courante pour ces solutions afin de prendre en charge l’authentification unique. 

La solution d’authentification multifacteur (MFA) est prise en charge avec Azure Information Protection si vous disposez du logiciel client nécessaire et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.

L’accès conditionnel est pris en charge en préversion pour les documents protégés par Azure Information Protection. Pour plus d’informations, consultez la question fréquente suivante : [Je vois qu’Azure Information Protection est répertorié en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Pour plus d’informations sur les conditions d’authentification, consultez [Configuration requise d’Azure Active Directory pour Azure Information Protection](requirements-azure-ad.md). 

Pour plus d’informations sur la configuration requise pour les comptes d’utilisateur et de groupe pour l’autorisation, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

## <a name="client-devices"></a>Appareils clients

Les utilisateurs doivent avoir des appareils clients (ordinateurs ou appareils mobiles) exécutant un système d’exploitation qui prend en charge Azure Information Protection.

Les appareils suivants prennent en charge le client d’étiquetage Azure Information Protection unifié et le client Azure Information Protection. [Les deux clients](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) permettent aux utilisateurs de classer et d’étiqueter leurs documents et e-mails:

- Windows 10 (x86, x64)
    
    - Aucune prise en charge de l’écriture manuscrite dans la build Windows 10 RS4 et versions ultérieures. 

- Windows 8.1 (x86, x64)

- Windows 8 (x86, x64)

- Windows 7 Service Pack 1 (x86, x64)

- Windows Server 2016 

- Windows Server 2012 R2 et Windows Server 2012

- Windows Server 2008 R2 

Outre l’installation du client sur des ordinateurs physiques, vous pouvez également l’installer sur des machines virtuelles. Vérifiez si le fournisseur de logiciels de la solution de bureau virtuel dispose d’une configuration supplémentaire qui peut être nécessaire pour exécuter le client d’étiquetage Azure Information Protection unifié ou le client Azure Information Protection. Par exemple, pour les solutions Citrix, vous devrez peut-être désactiver les hooks de l' [interface de programmation d’applications (API) Citrix](https://support.citrix.com/article/CTX107825) pour Office (Winword. exe, Excel. exe, Outlook. exe, PowerPoint. exe) et l’exécutable pour le Azure information protection Unified étiquetage du client ou du client Azure Information Protection (MSIP. app. exe, MSIP. Viewer. exe).

Pour les versions de serveur répertoriées, les clients Azure Information Protection sont pris en charge pour la Services Bureau à distance. Si vous supprimez des profils utilisateur quand vous utilisez les clients Azure Information Protection avec Services Bureau à distance, ne supprimez pas le dossier **%AppData%\Microsoft\Protect** .

Lorsque les clients Azure Information Protection protègent les données à l’aide du service Azure Rights Management, les données peuvent être consommées par les [mêmes appareils](requirements-client-devices.md) qui prennent en charge le service de Rights Management Azure.

Les clients Azure Information Protection ont des conditions préalables supplémentaires qui sont répertoriées dans leurs guides d’administration respectifs:

- Client d’étiquetage unifié Azure Information Protection : [Composants requis](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- Client Azure Information Protection : [Composants requis](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)


## <a name="applications"></a>APPLICATIONS

Les clients Azure Information Protection peuvent étiqueter et protéger des documents et des e-mails à l’aide des applications Office **Word**, **Excel**, **PowerPoint**et **Outlook** de l’une des éditions Office suivantes:

- Applications Office version minimale 1805, build 9330.2078 d’Office 365 Business ou de Microsoft 365 Business quand une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est affectée à l’utilisateur

- Office 365 ProPlus

- Office Professionnel Plus 2019

- Office Professionnel Plus 2016

- Office Professionnel Plus 2013 avec Service Pack 1

- Office Professionnel Plus 2010 avec Service Pack 2

Les autres éditions d’Office ne peuvent pas protéger les documents et messages électroniques à l’aide d’un service Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour la classification uniquement. Par conséquent, les étiquettes qui appliquent la protection ne s’affichent pas aux utilisateurs sur la barre Azure Information Protection ni à partir du bouton **Protéger** du ruban Office. 

Les clients Azure Information Protection ne prennent pas en charge plusieurs versions d’Office sur le même ordinateur. Ces clients ne prennent pas non plus en charge le changement de comptes d’utilisateur dans Office.

Pour plus d’informations sur les éditions d’Office qui prennent en charge le service de protection, consultez [Applications prenant en charge la protection des données Azure Rights Management](requirements-applications.md).

## <a name="firewalls-and-network-infrastructure"></a>Pare-feu et infrastructure réseau

Si vous avez un pare-feu ou des appareils réseau intervenants similaires qui nécessitent une configuration pour autoriser des connexions spécifiques, les exigences de connectivité réseau sont incluses dans l’article relatif à Office, [URL et plages d’adresses IP Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). Consultez la section **Microsoft 365 Common et Office Online**.

En plus des informations de l’article relatif à Office, voici des informations propres à Azure Information Protection :

- Pour que le client d’étiquetage unifié télécharge des étiquettes et des stratégies d’étiquette: Autorisez l’URL * **. protection.Outlook.com** sur HTTPS.

- Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer pour qu’il utilise l’authentification Windows intégrée avec les informations d’identification d’ouverture de session Active Directory de l’utilisateur.

- N’interrompez pas la connexion du client au service TLS (par exemple, pour effectuer une inspection au niveau du paquet) vers l’URL **aadrm.com**. Cela a pour effet d’interrompre l’épinglage de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour sécuriser leur communication avec le service Azure Rights Management.
    
    - Conseil : En raison de la façon dont Chrome affiche les connexions sécurisées dans la barre d’adresses, vous pouvez utiliser ce navigateur pour vérifier rapidement si la connexion de votre client est arrêtée avant d’atteindre le service Azure Rights Management. Dans la barre d’adresse du navigateur, entrez l’URL suivante : `https://admin.na.aadrm.com/admin/admin.svc` 
    
        Ne vous inquiétez pas de ce qu’affiche la fenêtre du navigateur. Cliquez sur le verrou dans la barre d’adresses pour afficher les informations du site. Les informations du site vous permettent de voir l’autorité de certification (CA) émettrice. Si le certificat n’est pas émis par une Autorité de certification Microsoft, il est très probable que votre connexion client-à-service sécurisée s’arrête et nécessite une reconfiguration sur votre pare-feu. L’image suivante illustre un exemple d’une autorité de certification Microsoft. Si vous constatez qu’une autorité de certification interne a émis le certificat, cette configuration n’est pas compatible avec Azure Information Protection.
        
        ![Vérification du certificat émis pour les connexions Azure Information Protection](./media/certificate-checking.png)

### <a name="on-premises-servers"></a>Serveurs locaux

Si vous souhaitez utiliser le service Azure Rights Management d’Azure Information Protection avec des serveurs locaux, les produits pris en charge sont les suivants :

- Exchange Server

- SharePoint Server

- Serveurs de fichiers Windows Server prenant en charge l’infrastructure de classification des fichiers

Pour plus d’informations sur les conditions requises supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge la protection des données Azure Rights Management](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coexistence d’AD RMS et Azure RMS

Le scénario de déploiement suivant n’est pas pris en charge, sauf si vous utilisez AD RMS pour la [protection HYOK](configure-adrms-restrictions.md) avec Azure Information Protection (la configuration « conservez votre propre clé ») :

- En cas d’exécution d’AD RMS et d’Azure RMS côte à côte dans la même organisation, sauf pendant la migration, comme le décrit la rubrique [Migrer d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

Il existe un chemin de migration pris en charge [d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) et [d’Azure Information Protection vers AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl). Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](decommission-deactivate.md).

