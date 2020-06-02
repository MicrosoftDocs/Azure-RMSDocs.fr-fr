---
title: Configuration requise pour Azure Information Protection - AIP
description: Identifiez les conditions préalables requises pour déployer des Azure Information Protection dans votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/25/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 24797e570dada67ca304667b2e4d64147aa17580
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84249842"
---
# <a name="azure-information-protection-requirements"></a>Configuration requise pour la Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Avant de déployer Azure Information Protection, assurez-vous que votre système répond aux conditions préalables suivantes :

- [Abonnement à Azure Information Protection](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [Appareils clients](#client-devices)
- [Applications](#applications)
- [Pare-feux et infrastructure réseau](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Abonnement à Azure Information Protection

Vous devez disposer de l’un des éléments suivants, selon les fonctionnalités de Azure Information Protection que vous allez utiliser :

- ** [Plan de Azure information protection](https://azure.microsoft.com/pricing/details/information-protection/)**. Requis pour la classification, l’étiquetage et la protection à l’aide du scanneur ou du client Azure Information Protection (étiquetage classique ou unifié)

- ** [Plan Office 365 qui comprend des Azure information protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)**. Obligatoire uniquement pour la protection.

Pour vérifier que votre abonnement comprend les fonctionnalités Azure Information Protection que vous souhaitez utiliser, consultez la liste des fonctionnalités au [tarif Azure information protection](https://azure.microsoft.com/pricing/details/information-protection).

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

Pour prendre en charge l’authentification et l’autorisation pour Azure Information Protection, vous devez disposer d’un Azure Active Directory (AD). Pour utiliser des comptes d’utilisateur à partir de votre directeur local (AD DS), vous devez également configurer l’intégration d’annuaire.

- L’authentification **unique (SSO)** est prise en charge pour les Azure information protection afin que les utilisateurs ne soient pas invités à saisir leurs informations d’identification à plusieurs reprises. Si vous utilisez une autre solution de fournisseur pour la Fédération, contactez ce fournisseur pour savoir comment le configurer pour Azure AD. WS-Trust est une exigence courante pour ces solutions afin de prendre en charge l’authentification unique. 

- L' **authentification multifacteur (MFA)** est prise en charge avec Azure information protection lorsque vous disposez du logiciel client requis et que vous avez correctement configuré l’infrastructure de prise en charge de l’authentification mfa.

L’accès conditionnel est pris en charge en préversion pour les documents protégés par Azure Information Protection. Pour plus d’informations, consultez : [je vois Azure information protection est listé comme une application Cloud disponible pour l’accès conditionnel, comment cela fonctionne-t-il ?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Pour plus d'informations, consultez la page suivante :

- [Configuration requise d’Azure Active Directory pour Azure Information Protection](requirements-azure-ad.md)

- [Préparation des utilisateurs et des groupes pour Azure Information Protection](prepare.md)

## <a name="client-devices"></a>Appareils clients

Les ordinateurs des utilisateurs ou les appareils mobiles doivent s’exécuter sur un système d’exploitation qui prend en charge Azure information protection.

### <a name="supported-operating-systems-for-client-devices"></a>Systèmes d’exploitation pris en charge pour les périphériques clients

Les systèmes d’exploitation suivants prennent en charge à la fois l’étiquetage unifié Azure Information Protection et les clients Azure Information Protection : 

- **Windows 10** (x86, x64). L’écriture manuscrite n’est pas prise en charge dans Windows 10 RS4 Build et versions ultérieures.
 
- **Windows 8.1** (x86, x64)

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows server 2012 R2** et **Windows Server 2012**

[Les deux clients](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) permettent aux utilisateurs de classer et d’étiqueter leurs documents et e-mails.

Pour plus d’informations sur la prise en charge dans les versions antérieures de Windows, contactez votre compte Microsoft ou un représentant du support technique.

> [!NOTE]
> Lorsque les clients Azure Information Protection protègent les données à l’aide du service Azure Rights Management, les données peuvent être consommées par les [mêmes appareils](requirements-client-devices.md) qui prennent en charge le service de Rights Management Azure.
>

### <a name="virtual-machines"></a>Machines virtuelles
Si vous utilisez des machines virtuelles, vérifiez si le fournisseur de logiciels de votre solution de bureau virtuel utilise des configurations supplémentaires requises pour exécuter le Azure Information Protection l’étiquetage unifié ou le client Azure Information Protection. 

Par exemple, pour les solutions Citrix, vous devrez peut-être désactiver les hooks de l' [interface de programmation d’applications (API) Citrix](https://support.citrix.com/article/CTX107825) pour Office, le client d’étiquetage unifié Azure information protection ou le client Azure information protection. 

Ces applications utilisent les fichiers suivants respectivement : **WINWORD. exe**, **Excel. exe**, **Outlook. exe**, **Powerpnt. exe**, **MSIP. app. exe**, **MSIP. Viewer. exe**

### <a name="server-support"></a>Prise en charge du serveur

Pour chacune des versions de serveur répertoriées ci-dessus, les clients Azure Information Protection sont pris en charge pour les Services Bureau à distance. 

Si vous supprimez des profils utilisateur quand vous utilisez les clients Azure Information Protection avec Services Bureau à distance, ne supprimez pas le dossier **%AppData%\Microsoft\Protect** .

En outre, Server Core et nano Server ne sont pas pris en charge.

### <a name="additional-requirements-per-client"></a>Exigences supplémentaires par client

Chaque client Azure Information Protection a des conditions préalables supplémentaires. Pour plus d'informations, consultez :

- [Prérequis du client d’étiquetage unifié Azure Information Protection](./rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)

- [Prérequis du client Azure Information Protection](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>Applications

Les clients Azure Information Protection peuvent étiqueter et protéger des documents et des e-mails à l’aide de Microsoft **Word**, **Excel**, **PowerPoint**et **Outlook** , à partir des éditions Office suivantes :

- **Applications Office version 1805 minimum**, Build 9330,2078 à partir d’Office 365 Business ou Microsoft 365 Business. 

    Cette édition est prise en charge uniquement lorsque l’utilisateur se voit attribuer une licence pour Azure Rights Management, également appelée Azure Information Protection pour Office 365.

- **Office 365 ProPlus**

- **Office professionnel plus 2019**

- **Office Professionnel Plus 2016**

- **Office professionnel plus 2013 avec Service Pack 1**

- **Office Professionnel Plus 2010 avec Service Pack 2**

Les autres éditions d’Office ne peuvent pas protéger les documents et messages électroniques à l’aide d’un service Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour la classification uniquement, et les étiquettes qui appliquent la protection ne sont pas affichées pour les utilisateurs. 

Ces étiquettes auraient sinon été affichées dans la barre de Azure Information Protection ou dans le client d’étiquetage unifié sur le ruban Office (à partir du bouton **protéger** dans le client classique ou du bouton **sensibilité** dans le client d’étiquetage unifié). 

Pour plus d’informations, consultez [applications prenant en charge Azure Rights Management la protection des données](requirements-applications.md).

### <a name="office-features-and-capabilities-not-supported"></a>Fonctionnalités et fonctionnalités Office non prises en charge

- Les clients Azure Information Protection, y compris les étiquetages classiques et unifiés, ne prennent pas en charge plusieurs versions d’Office sur le même ordinateur ou n’échangent pas de comptes d’utilisateur dans Office.

- La fonctionnalité de [fusion et](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) publipostage d’Office n’est pas prise en charge avec les fonctionnalités de Azure information protection.

## <a name="firewalls-and-network-infrastructure"></a>Pare-feu et infrastructure réseau

Si vous avez un pare-feu ou des périphériques réseau intermédiaires similaires qui sont configurés pour autoriser des connexions spécifiques, les exigences en matière de connectivité réseau sont répertoriées dans cet article Office : [URL office 365 et plages d’adresses IP > Microsoft 365 Common et Office Online](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online).

Azure Information Protection présente les exigences supplémentaires suivantes :

- **Client d’étiquetage unifié**. Pour télécharger des étiquettes et des stratégies d’étiquette, autorisez l’URL suivante sur HTTPs : ***. protection.Outlook.com**

- **Proxys Web**. Si vous utilisez un proxy Web qui nécessite une authentification, vous devez configurer le proxy pour utiliser l’authentification Windows intégrée avec les informations d’identification d’ouverture de session de l’utilisateur Active Directory.

    
- **Connexions client à service TLS**. Ne mettez pas fin à des connexions de client à service TLS, par exemple pour effectuer une inspection au niveau du paquet, vers l’URL **aadrm.com** . Cela annule l’association de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour vous aider à sécuriser leur communication avec le service Azure Rights Management.
     
    Pour déterminer si votre connexion cliente est terminée avant d’atteindre le service Rights Management Azure, utilisez les commandes PowerShell suivantes :
    
        $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
        $request.GetResponse()
        $request.ServicePoint.Certificate.Issuer

    Le résultat doit indiquer que l’autorité de certification émettrice provient d’une autorité de certification Microsoft, par exemple : `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US` . 
    
    Si vous voyez un nom d’autorité de certification émettrice qui ne provient pas de Microsoft, il est très probable que votre connexion sécurisée client-à-service est interrompue et nécessite une reconfiguration sur votre pare-feu.

- **TLS version 1,2 ou ultérieure** (client d’étiquetage unifié uniquement). Le client d’étiquetage unifié requiert une version TLS de 1,2 ou une version ultérieure pour garantir l’utilisation de protocoles sécurisés par chiffrement et s’aligner sur les consignes de sécurité Microsoft.
    
### <a name="on-premises-servers"></a>Serveurs locaux

Les serveurs locaux suivants sont pris en charge avec le service Azure Rights Management à partir de Azure Information Protection :

- **Exchange Server**

- **SharePoint Server**

- **Serveurs de fichiers Windows Server** prenant en charge infrastructure de classification des fichiers

Pour plus d’informations sur les conditions requises supplémentaires pour ce scénario, consultez [Serveurs locaux prenant en charge la protection des données Azure Rights Management](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coexistence d’AD RMS et Azure RMS

L’utilisation de AD RMS et Azure RMS côte à côte, dans la même organisation, pour protéger du contenu par le même utilisateur au sein de la même organisation, est prise en charge **uniquement** dans AD RMS pour la [protection hyok (maintenir votre propre clé)](configure-adrms-restrictions.md) avec Azure information protection.

Ce scénario n’est *pas* pris en charge lors de la [migration](migrate-from-ad-rms-to-azure-rms.md).
Les chemins de migration pris en charge sont les suivants :

* [De AD RMS à Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

* [De Azure Information Protection à AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](decommission-deactivate.md).

Pour les autres scénarios de non-migration, où les deux services sont actifs dans la même organisation, les deux services doivent être configurés de sorte qu’un seul d’entre eux autorise un utilisateur donné à protéger du contenu. Vous pouvez le configurer comme suit :

* Utiliser les redirections pour une [AD RMS pour Azure RMS la migration](migrate-from-ad-rms-to-azure-rms.md)

* Si les deux services doivent être actifs pour différents utilisateurs en même temps, utilisez des configurations côté service pour appliquer l’exclusivité.  Utilisez les Azure RMS contrôles d’intégration dans le service Cloud et une liste de contrôle d’accès sur l’URL de publication pour définir le mode **lecture seule** pour AD RMS.

### <a name="service-tags"></a>Étiquettes de service

Veillez à autoriser l’accès à tous les ports pour les balises de service suivantes :

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor. FrontEnd**

Le service Azure Information Protection dépend également de deux adresses IP spécifiques :
 - **13.107.6.181** 
 - **13.107.9.181**

Veillez à créer des règles pour autoriser l’accès sortant à ces adresses IP spécifiques. 
