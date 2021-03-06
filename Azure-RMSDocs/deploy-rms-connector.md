---
title: Déployer le connecteur Azure Rights Management - AIP
description: Instructions pour déployer le connecteur RMS, qui fournit le service de protection des données dans le cas des déploiements locaux existants utilisant Exchange Server, SharePoint Server ou Windows Server et l’Infrastructure de classification des fichiers (ICF).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/10/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a495ea2ca1cc08da081c10496c8e2b51f7718706
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382528"
---
# <a name="deploying-the-azure-rights-management-connector"></a>Déploiement du connecteur Azure Rights Management

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Utilisez ces informations pour découvrir le connecteur Azure Rights Management et pour savoir comment le déployer correctement dans votre organisation. Ce connecteur assure la protection des données pour les déploiements locaux existants qui utilisent Microsoft **Exchange Server**, **SharePoint Server** ou des serveurs de fichiers qui exécutent Windows Server et **infrastructure de classification des fichiers** (FCI).


## <a name="overview-of-the-microsoft-rights-management-connector"></a>Vue d'ensemble du connecteur Microsoft Rights Management

Le connecteur Microsoft Rights Management (RMS) permet d'activer rapidement des serveurs locaux existants pour utiliser les services RMS avec le service Microsoft Rights Management (Azure RMS) basé sur le cloud. Cette fonctionnalité permet au service informatique et aux utilisateurs de protéger facilement des documents et des images à l'intérieur comme à l'extérieur de l'organisation, sans avoir à installer des infrastructures supplémentaires ou à établir des relations de confiance avec d'autres organisations. 

Le connecteur RMS est un service à faible encombrement que vous installez localement, sur des serveurs qui exécutent Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012. Outre la possibilité d'exécuter le connecteur sur des ordinateurs physiques, vous pouvez l'exécuter sur des machines virtuelles, y compris des machines virtuelles Azure IaaS. Une fois déployé, le connecteur joue le rôle d’interface de communication (relais) entre les serveurs locaux et le service cloud, comme le montre l’illustration suivante. Les flèches indiquent le sens dans lequel les connexions réseau sont démarrées.

![Vue d’ensemble de l’architecture du connecteur RMS](./media/RMS_connector.png)


### <a name="on-premises-servers-supported"></a>Serveurs locaux pris en charge

Le connecteur RMS prend en charge les serveurs locaux suivants : Exchange Server, SharePoint Server, ainsi que les serveurs de fichiers exécutant Windows Server et utilisant l’infrastructure de classification des fichiers pour classer et appliquer des stratégies à des documents Office dans un dossier. 

> [!NOTE]
> Si vous voulez protéger plusieurs types de fichiers (pas seulement les documents Office) à l’aide de l’Infrastructure de classification des fichiers, n’utilisez pas le connecteur RMS, mais des [applets de commande AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).

Pour connaître les versions de ces serveurs locaux qui sont prises en charge par le connecteur RMS, consultez [Serveurs locaux qui prennent en charge Azure RMS](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection).


### <a name="support-for-hybrid-scenarios"></a>Prise en charge des scénarios hybrides

Vous pouvez utiliser ce connecteur RMS même si certains de vos utilisateurs se connectent à des services en ligne dans le cadre d’un scénario hybride. Par exemple, les boîtes aux lettres de certains utilisateurs utilisent Exchange Online et celles d'autres utilisateurs utilisent Exchange Server. Après installation du connecteur RMS, tous les utilisateurs peuvent protéger et consommer des courriers électroniques et pièces jointes à l'aide d'Azure RMS, et la protection des informations fonctionne de façon transparente entre les deux configurations de déploiement.

### <a name="support-for-customer-managed-keys-byok"></a>Prise en charge des clés gérées par le client (BYOK)

Si vous gérez votre propre clé de locataire pour Azure RMS (scénario BYOK, Bring You Own Key), le connecteur RMS et les serveurs locaux qui l’utilisent n’accèdent pas au module de sécurité matériel (HSM) qui contient votre clé de locataire. En effet, toutes les opérations de chiffrement qui utilisent la clé de locataire sont effectuées dans Azure RMS et non en local.

Si vous voulez découvrir plus en détail ce scénario dans lequel vous gérez votre clé de locataire, consultez [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

## <a name="prerequisites-for-the-rms-connector"></a>Conditions requises pour l'installation du connecteur RMS

Avant d'installer le connecteur RMS, assurez-vous que les conditions requises suivantes sont remplies.

|Condition requise|Informations complémentaires|
|---------------|--------------------|
|Le service de protection est activé|[Activation du service de protection à partir de Azure Information Protection](activate-service.md)|
|Synchronisation des annuaires entre vos forêts Active Directory locales et Azure Active Directory|Une fois RMS activé, Azure Active Directory doit être configuré pour travailler avec les utilisateurs et les groupes de votre base de données Active Directory.<br /><br />**Important** : vous devez effectuer cette étape de synchronisation des annuaires pour que le connecteur RMS fonctionne, même pour un réseau de test. Bien que vous puissiez utiliser des Microsoft 365 et des Azure Active Directory à l’aide de comptes que vous créez manuellement dans Azure Active Directory, ce connecteur exige que les comptes de Azure Active Directory soient synchronisés avec Active Directory Domain Services ; la synchronisation manuelle des mots de passe n’est pas suffisante.<br /><br />Pour plus d’informations, consultez les ressources suivantes :<br /><br />- [Intégrer des domaines de Active Directory locaux avec Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad)<br /><br />- [Comparaison des outils d’intégration d’annuaire d’identités hybrides](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-tools-comparison)|
|Au moins deux ordinateurs membres sur lesquels installer le connecteur RMS :<br /><br />-Un ordinateur physique ou virtuel 64 bits exécutant l’un des systèmes d’exploitation suivants : Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012.<br /><br />- 1 Go de RAM minimum.<br /><br />- 64 Go d’espace disque minimum.<br /><br />- Au moins une interface réseau.<br /><br />-Accès à Internet via un pare-feu (ou un proxy Web) qui ne requiert pas d’authentification.<br /><br />- Un emplacement au sein d’une forêt ou d’un domaine qui approuve les autres forêts de l’organisation contenant les installations des serveurs Exchange ou SharePoint à utiliser avec le connecteur RMS.|Pour une tolérance de panne et une haute disponibilité, vous devez installer le connecteur RMS sur un minimum de deux ordinateurs.<br /><br />**Conseil** : si vous utilisez Outlook Web Access ou des appareils mobiles qui utilisent Exchange ActiveSync IRM et qu’il est essentiel de maintenir l’accès aux messages électroniques et pièces jointes protégés par Azure RMS, nous vous recommandons de déployer un groupe de serveurs de connecteur faisant l’objet d’un équilibrage de charge pour garantir une haute disponibilité.<br /><br />Vous n'avez pas besoin de serveurs dédiés pour exécuter le connecteur, mais vous devez l'installer sur un ordinateur différent des serveurs qui utiliseront le connecteur.<br /><br />**Important** : n’installez pas le connecteur sur un ordinateur qui exécute Exchange Server, SharePoint Server ou un serveur de fichiers configuré pour l’infrastructure de classification des fichiers si vous voulez utiliser la fonctionnalité depuis ces services avec Azure RMS. En outre, n'installez pas ce connecteur sur un contrôleur de domaine.<br /><br />Si vous avez des charges de travail de serveur que vous souhaitez utiliser avec le connecteur RMS, mais que leurs serveurs se trouvent dans des domaines qui ne sont pas approuvés par le domaine depuis lequel vous souhaitez exécuter le connecteur, vous pouvez installer des serveurs supplémentaires pour le connecteur RMS dans ces domaines non approuvés ou dans d’autres domaines de leur forêt. <br /><br />Le nombre de serveurs de connecteur que vous pouvez exécuter pour votre organisation n’est pas limité et tous les serveurs de connecteur installés dans une organisation partagent la même configuration. Toutefois, pour configurer le connecteur pour autoriser des serveurs, vous devez être en mesure de rechercher le serveur ou les comptes de service que vous souhaitez autoriser, ce qui signifie que vous devez exécuter l’outil d’administration RMS dans une forêt depuis laquelle vous pouvez rechercher ces comptes.|


## <a name="steps-to-deploy-the-rms-connector"></a>Procédure de déploiement du connecteur RMS

Étant donné que le connecteur ne vérifie pas automatiquement toutes les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) nécessaires à la réussite d’un déploiement, assurez-vous qu’elles sont réunies avant de commencer. À cet effet, vous devez installer le connecteur, le configurer et configurer ensuite les serveurs appelés à utiliser le connecteur. 

-   **Étape 1**:  [installation du connecteur RMS](install-configure-rms-connector.md#installing-the-rms-connector)

-   **Étape 2**:  [Saisie des informations d’identification](install-configure-rms-connector.md#entering-credentials)

-   **Étape 3**:  [autoriser les serveurs à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **Étape 4**:  [configuration de l’équilibrage de charge et de la haute disponibilité](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

    -   Facultatif : [Configuration du connecteur RMS pour le protocole HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

    -   Facultatif : [Configuration du connecteur RMS pour un serveur proxy web](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

    -   Facultatif : [Installation de l'outil d'administration du connecteur RMS sur les ordinateurs d'administration](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **Étape 5**:  [Configuration des serveurs pour utiliser le connecteur RMS](configure-servers-rms-connector.md)

    -   [Configuration d’un serveur Exchange pour utiliser le connecteur](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [Configuration d’un serveur SharePoint afin d’utiliser le connecteur](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [Configuration d’un serveur de fichiers pour l’infrastructure de classification des fichiers afin d’utiliser le connecteur](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## <a name="next-steps"></a>Étapes suivantes

Accédez à l’étape 1 : [Installation et configuration du connecteur Azure Rights Management](install-configure-rms-connector.md).
