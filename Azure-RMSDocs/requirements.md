---
title: Configuration requise pour Azure Information Protection - AIP
description: Identifiez les conditions préalables nécessaires pour déployer Azure Information Protection dans votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 229b67b152845cfb1e0499f1df9eb08ba28b49df
ms.sourcegitcommit: 73befea74644d272e2d8d1d4b95df55c7741ccbe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97762302"
---
# <a name="azure-information-protection-requirements"></a>Configuration requise pour Azure Information Protection

>****S’applique à**  _: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)_
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).*

Avant de déployer Azure Information Protection, assurez-vous que votre système répond aux conditions préalables suivantes :

- [Abonnement à Azure Information Protection](#subscription-for-azure-information-protection)
- [Azure Active Directory](#azure-active-directory)
- [Appareils clients](#client-devices)
- [Applications](#applications)
- [Pare-feux et infrastructure réseau](#firewalls-and-network-infrastructure)

## <a name="subscription-for-azure-information-protection"></a>Abonnement à Azure Information Protection

Vous devez disposer de l’un des éléments suivants, selon les fonctionnalités d’Azure Information Protection que vous allez utiliser :

- **Un [plan Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/)** . Requis pour la classification, l’étiquetage et la protection à l’aide du lecteur ou du client Azure Information Protection.

- **Un [plan Office 365 incluant Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)** . Requis uniquement pour la protection.

Pour vérifier que l’abonnement inclut les fonctionnalités Azure Information Protection que vous voulez utiliser, passez en revue la liste des fonctionnalités sur [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Si vous avez des questions sur les licences, lisez le [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

> [!TIP]
> Vous voulez savoir si votre plan prend en charge les [nouvelles fonctionnalités de chiffrement de messages Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) pour envoyer des e-mails protégés à des adresses e-mail personnelles ? Par exemple, Gmail, Yahoo et Microsoft. Consultez les ressources suivantes :
>
> - [Description du service Exchange Online](/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description)
>
> - [Comparaison des licences Conformité Microsoft 365](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-business-service-description)
>
> - [Office 365 Éducation](/office365/servicedescriptions/office-365-platform-service-description/office-365-education)
>
> - [Office 365 US Government](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/office-365-us-government)

Si vous avez des questions sur les abonnements ou les licences, ne les postez pas sur cette page. Regardez plutôt si vous trouvez des réponses dans le [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences. Si aucune réponse n’existe à votre question, contactez votre responsable de compte Microsoft ou le [Support Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Pour prendre en charge l’authentification et l’autorisation pour Azure Information Protection, vous devez disposer d’un Azure Active Directory (AD). Pour utiliser des comptes d'utilisateur à partir de votre annuaire local (AD DS), vous devez également configurer l’intégration d'annuaire.

- **L’authentification unique (SSO)** étant prise en charge pour Azure Information Protection, les utilisateurs ne sont pas invités de manière répétée à fournir leurs informations d’identification. Si vous utilisez une autre solution de fournisseur pour la fédération, vérifiez auprès de ce dernier comment la configurer pour Azure AD. WS-Trust est une exigence courante pour ces solutions afin de prendre en charge l’authentification unique. 

- **La solution d’authentification multifacteur (MFA)** est prise en charge avec Azure Information Protection si vous disposez du logiciel client nécessaire et que vous avez correctement configuré l’infrastructure de prise en charge de MFA.

L’accès conditionnel est pris en charge en préversion pour les documents protégés par Azure Information Protection. Pour plus d'informations, voir : [Je vois qu’Azure Information Protection est répertorié en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)

Des conditions préalables supplémentaires sont requises pour des scénarios spécifiques, par exemple lors de l’utilisation de l’authentification par certificat ou multifacteur, lorsque les valeurs UPN ne correspondent pas aux adresses e-mail des utilisateurs ou lors de l’utilisation d’[Office 2010](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

Pour plus d’informations, consultez :

- [Prérequis Azure AD supplémentaires pour Azure Information Protection](requirements-azure-ad.md).
- [Qu’est-ce qu’Azure AD Directory ?](/azure/active-directory/fundamentals/active-directory-whatis)
- [Intégrer des domaines Active Directory locaux avec Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad).

## <a name="client-devices"></a>Appareils clients

Les ordinateurs des utilisateurs ou les appareils mobiles doivent s’exécuter sur un système d’exploitation qui prend en charge Azure Information Protection.

- [Systèmes d’exploitation pris en charge pour les appareils clients](#supported-operating-systems-for-client-devices)
- [Machines virtuelles](#virtual-machines)
- [Prise en charge de serveur](#server-support)
- [Configuration requise supplémentaire par client](#additional-requirements-per-client)

### <a name="supported-operating-systems-for-client-devices"></a>Systèmes d’exploitation pris en charge pour les appareils clients

Les clients Azure Information Protection pour Windows sont pris en charge sur les systèmes d’exploitation suivants :

- **Windows 10** (x86, x64). L’écriture manuscrite n’est pas prise en charge dans la build Windows 10 RS4 et versions ultérieures.
 
- **Windows 8.1** (x86, x64)

- **Windows 8** (x86, x64)

- **Windows Server 2019**

- **Windows Server 2016**

- **Windows Server 2012 R2** et **Windows Server 2012**

Pour plus d’informations sur la prise en charge dans les versions antérieures de Windows, contactez votre compte Microsoft ou un représentant du support technique.

> [!NOTE]
> Quand les clients Azure Information Protection protègent les données à l’aide du service Azure Rights Management, ces données peuvent être utilisées par les [mêmes appareils](#client-devices) que ceux qui prennent en charge le service Azure Rights Management.
>
### <a name="arm64"></a>ARM64 

ARM64 n’est **pas** pris en charge actuellement. 

### <a name="virtual-machines"></a>Machines virtuelles

Si vous utilisez des machines virtuelles, vérifiez si le fournisseur de logiciels de votre solution de bureau virtuel utilise des configurations supplémentaires requises pour exécuter étiquetage unifié Azure Information Protection ou le client Azure Information Protection. 

Par exemple, pour les solutions Citrix, vous devrez peut-être [désactiver les hooks d’API (Application Programming Interface) Citrix](https://support.citrix.com/article/CTX107825) pour Office et le client d’étiquetage unifié Azure Information Protection ou le client Azure Information Protection. 

Ces applications utilisent les fichiers suivants, respectivement : **winword.exe**, **excel.exe**, **outlook.exe**, **powerpnt.exe**, **msip.app.exe**, **msip.viewer.exe**

### <a name="server-support"></a>Prise en charge du serveur

Pour chaque version de serveur répertoriée ci-dessus, les clients Azure Information Protection sont pris en charge pour les Services Bureau à distance. 

Si vous supprimez des profils utilisateur quand vous utilisez les clients Azure Information Protection avec les Services Bureau à distance, ne supprimez pas le dossier **%Appdata%\Microsoft\Protect**.

En outre, Server Core et Nano Server ne sont pas pris en charge.

### <a name="additional-requirements-per-client"></a>Configuration requise supplémentaire par client

Chaque client Azure Information Protection impose des exigences supplémentaires. Pour plus d’informations, consultez :

- [Exigences du client d’étiquetage unifié Azure Information Protection](./rms-client/reqs-ul-client.md)

- [Exigences du client Azure Information Protection](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client)

## <a name="applications"></a>Applications

Les clients Azure Information Protection peuvent étiqueter et protéger des documents et des e-mails à l’aide de **Word**, **Excel**, **PowerPoint** et **Outlook** de Microsoft à partir de toutes les éditions Office suivantes :

- **Applications Office**, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur

- **Microsoft 365 Apps for enterprise**

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013 avec Service Pack 1**

- **Office Professional Plus 2010 avec Service Pack 2**

Les autres éditions d’Office ne peuvent pas protéger les documents et messages électroniques à l’aide d’un service Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour la classification uniquement et les étiquettes qui appliquent la protection ne s’affichent pas pour les utilisateurs. 

Les étiquettes sont visibles dans une barre affichée en haut du document Office, accessible avec le bouton **Sensibilité** dans le client d’étiquetage unifié ou avec le bouton **Protéger** dans le client classique.

Pour plus d’informations, consultez [Applications prenant en charge la protection des données Azure Rights Management](requirements-applications.md) et [AIP pour les versions Windows et Office en support étendu](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).

### <a name="office-features-and-capabilities-not-supported"></a>Fonctionnalités et caractéristiques Office non prises en charge

- Les clients Azure Information Protection pour Windows ne prennent pas en charge l’utilisation de plusieurs versions d’Office sur le même ordinateur, ni le changement de comptes d’utilisateur dans Office.

- La fonctionnalité [Publipostage](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) n’est pas prise en charge avec les fonctionnalités Azure Information Protection.

## <a name="firewalls-and-network-infrastructure"></a>Pare-feu et infrastructure réseau

Si vous avez un pare-feu ou des appareils réseau intervenants similaires qui nécessitent une configuration pour autoriser des connexions spécifiques, les exigences de connectivité réseau sont incluses dans l’article relatif à Office : [Microsoft 365 Common et Office Online](/office365/enterprise/urls-and-ip-address-ranges#microsoft-365-common-and-office-online).

Azure Information Protection présente les exigences supplémentaires suivantes :

- **Client d’étiquetage unifié**. Pour télécharger des étiquettes et des stratégies d’étiquettes, autorisez l’URL suivante sur HTTPS : **_.protection.outlook.com_*.

- **Proxys web**. Si vous utilisez un proxy web qui nécessite une authentification, vous devez le configurer pour qu’il utilise l’authentification Windows intégrée avec les informations d’identification de connexion Active Directory de l’utilisateur.

    Pour prendre en charge les fichiers **Proxy.pac** si vous utilisez un proxy pour acquérir un jeton, ajoutez la nouvelle clé de Registre suivante :

    - **Path** (Chemin) : `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIP\`
    - **Clé** : `UseDefaultCredentialsInProxy`
    - **Type** : `DWORD`
    - **Valeur** : `1`
    
- **Connexions client à service TLS**. N’interrompez pas la connexion du client au service TLS, par exemple, pour effectuer une inspection au niveau du paquet vers l’URL **aadrm.com**. Cela annule l’association de certificat que les clients RMS utilisent avec les autorités de certification gérées par Microsoft pour vous aider à sécuriser leur communication avec le service Azure Rights Management.
     
    Pour déterminer si votre connexion cliente est terminée avant d’atteindre le service Rights Management Azure, utilisez les commandes PowerShell suivantes :

    ```PowerShell
    $request = [System.Net.HttpWebRequest]::Create("https://admin.na.aadrm.com/admin/admin.svc")
    $request.GetResponse()
    $request.ServicePoint.Certificate.Issuer
    ```

    Le résultat doit indiquer que l’autorité de certification émettrice provient d’une autorité de certification Microsoft, par exemple : `CN=Microsoft Secure Server CA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`. 
    
    Si vous voyez un nom de l'autorité de certification émettrice qui ne provient pas de Microsoft, il est très probable que votre connexion client-à-service sécurisée s’arrête et nécessite une reconfiguration sur votre pare-feu.

- **TLS version 1.2 ou ultérieure** (client d’étiquetage unifié uniquement). Le client d’étiquetage unifié requiert une version TLS de 1.2 ou une version ultérieure pour garantir l’utilisation de protocoles sécurisés par chiffrement et s’aligner sur les consignes de sécurité Microsoft.

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coexistence d’AD RMS et Azure RMS

L’utilisation de AD RMS et Azure RMS côte à côte, au sein d’une même organisation, pour protéger du contenu par le même utilisateur dans la même organisation, est **uniquement** pris en charge dans AD RMS pour [HYOK (maintenir votre propre clé)](configure-adrms-restrictions.md) de protection avec Azure Information Protection.

Ce scénario n’est *pas* pris en charge pendant la [migration](migrate-from-ad-rms-to-azure-rms.md).
Les chemins d’accès de migration pris en charge sont les suivants :

* [Depuis AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)

* [Depuis Azure Information Protection avec AD RMS](/powershell/module/aipservice/Set-AipServiceMigrationUrl)

> [!TIP]
> Si vous déployez Azure Information Protection et que vous décidez ensuite que vous ne voulez plus utiliser ce service cloud, consultez [Désaffectation et désactivation d’Azure Information Protection](decommission-deactivate.md).

Pour les autres scénarios de non-migration, où les deux services sont actifs dans la même organisation, les deux services doivent être configurés de sorte qu’un seul d’entre eux autorise un utilisateur donné à protéger du contenu. Configurez de tels scénarios comme suit :

* Utiliser les redirections pour une [migration AD RMS vers Azure RMS](migrate-from-ad-rms-to-azure-rms.md)

* Si les deux services doivent être actifs pour différents utilisateurs en même temps, utilisez des configurations côté service pour appliquer l’exclusivité.  Utilisez les contrôles d’intégration Azure RMS dans le service cloud et une liste de contrôle d’accès (ACL) sur l’URL de publication pour définir le mode **Lecture seule** pour AD RMS.

### <a name="service-tags"></a>Étiquettes de service

Si vous utilisez un point de terminaison Azure et un groupe de sécurité réseau, veillez à autoriser l’accès à tous les ports pour les étiquettes de service suivantes :

- **AzureInformationProtection**
- **AzureActiveDirectory**
- **AzureFrontDoor.Frontend**

De plus, dans ce cas, le service Azure Information Protection dépend également de deux adresses IP spécifiques :

 - **13.107.6.181** 
 - **13.107.9.181**
 - **Port 443** pour le trafic HTTPS

Veillez à créer des règles pour autoriser l’accès sortant à ces adresses IP spécifiques et via ce port.

## <a name="supported-on-premises-servers-for-azure-rights-management-data-protection"></a>Serveurs locaux pris en charge la protection des données Azure Rights Management

Les serveurs locaux suivants sont pris en charge avec Azure Information Protection quand vous utilisez le connecteur Azure Rights Management.

Ce connecteur fait office d’interface de communication et de relais entre les serveurs locaux et le service Azure Rights Management utilisé par Azure Information Protection pour protéger les e-mails et documents Office. 

Pour utiliser ce connecteur, vous devez configurer la synchronisation des annuaires entre vos forêts Active Directory et Azure Active Directory.

Serveurs pris en charge :

|Type de serveur  |Versions prises en charge  |
|---------|---------|
|**Exchange Server**     | - Exchange Server 2016 </br>- Exchange Server 2013 </br>- Exchange Server 2010       |
|**Office SharePoint Server**     |- Office SharePoint Server 2016 </br>- Office SharePoint Server 2013 </br>- Office SharePoint Server 2010         |
|**Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)**     |- Windows Server 2016 </br>- Windows Server 2012 R2 </br>- Windows Server 2012       |
| | |

Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

## <a name="supported-operating-systems-for-azure-rights-management"></a>Systèmes d’exploitation pris en charge pour Azure Rights Management

Les systèmes d’exploitation suivants prennent en charge le service Azure Rights Management qui fournit la protection des données pour AIP :

|Système d''exploitation  |Versions prises en charge  |
|---------|---------|
|**Ordinateurs Windows**     |- Windows 7 (x86, x64) </br>- Windows 8 (x86, x64) </br>- Windows 8.1 (x86, x64) </br>- Windows 10 (x86, x64)       | 
|**macOS**     |   la version minimale de macOS est 10.8 (Mountain Lion)      |
|**Téléphones et tablettes Android**     | Version minimale d’Android 6.0        |
|**iPhone et iPad**     | Version minimale d’iOS 11.0        |
|**Téléphones et tablettes Windows** | Windows 10 Mobile|
| | |



## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez examiné toutes les exigences AIP et vérifié que votre système est conforme, poursuivez avec [Préparation des utilisateurs et des groupes pour Azure Information Protection](prepare.md).