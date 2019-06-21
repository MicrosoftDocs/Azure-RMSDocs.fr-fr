---
title: FAQ relatives à Azure Information Protection
description: Certaines questions fréquentes sur Azure Information Protection et son service de protection des données, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 1e0933a88afc355dbcbab0dc667e28f49f10c0b9
ms.sourcegitcommit: 599306e271392afa4bc05c87982549785ce1860e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67305772"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Forum aux questions sur Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous avez une question sur Azure Information Protection ou sur le service Azure Rights Management (Azure RMS) ? Vous trouverez peut-être une réponse ici.

Ces pages de questions fréquentes sont régulièrement actualisées. Les nouveautés sont répertoriées dans les avis de mise à jour mensuels de la documentation sur le [blog technique d’Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Quelle est la différence entre Azure Information Protection et Microsoft Information Protection ?

Contrairement à Azure Information Protection, Microsoft Information Protection n’est pas un abonnement ou un produit que vous pouvez acheter. Au lieu de cela, il s’agit d’un framework pour les produits et les fonctionnalités intégrées qui vous aident à protéger les informations sensibles de votre organisation :

- Les produits individuels de ce framework incluent Azure Information Protection, Office 365 Information Protection (par exemple, Office 365 DLP), Windows Information Protection et Microsoft Cloud App Security. 

- Les fonctions intégrées dans ce framework incluent la gestion d’étiquette unifiée, les expériences d’étiquetage de l’utilisateur final intégrées aux applications Office, la possibilité pour Windows de comprendre les étiquettes unifiées et appliquer une protection aux données, le SDK Microsoft Information Protection et de nouvelles fonctionnalités dans Adobe Acrobat Reader pour afficher les fichiers PDF étiquetés et protégés.

Pour plus d’informations, consultez [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annonce de la disponibilité des fonctionnalités de protection des informations pour protéger vos données sensibles).

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Quelle est la différence entre les étiquettes dans Azure Information Protection et celles dans Office 365 ?

Au départ, Office 365 disposait uniquement [d’étiquettes de conservation](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) pour vous permettre de classifier les documents et les e-mails à des fins d’audit et de conservation quand ce contenu se trouvait dans les services Office 365. Par comparaison, les étiquettes Azure Information Protection vous permettent d’appliquer une stratégie de classification et de protection cohérente aux documents et aux e-mails, qu’ils soient locaux ou dans le cloud.

Comme cela a été annoncé lors de la conférence Microsoft Ignite 2018 à Orlando, il est maintenant possible de créer et de configurer des [étiquettes de confidentialité](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels) en plus des étiquettes de rétention dans l’un des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. Vous pouvez migrer vos étiquettes de l’étiquetage unifiée nouvelle stocker, à utiliser comme étiquettes de sensibilité avec Office 365 Azure Information Protection existant. 

Pour plus d’informations sur la gestion de l’étiquetage unifié et la prise en charge de ces étiquettes, lisez le billet de blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

Pour plus d’informations sur la migration d’étiquettes existantes, voir [Guide pratique pour migrer des étiquettes Azure Information Protection vers Office 365](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Quelle est la différence entre le client Azure Information Protection et Azure Information Protection unifiée client étiquetage ?

Le **client Azure Information Protection (classique)** a été disponible dans la mesure où Azure Information Protection a été annoncée en tant que nouveau service pour la classification et protection des fichiers et e-mails. Ce client télécharge les étiquettes et les paramètres de stratégie à partir d’Azure, et vous configurez la stratégie Azure Information Protection à partir du portail Azure. Pour plus d’informations, consultez [vue d’ensemble de la stratégie Azure Information Protection](overview-policy.md). 

Le **Azure Information Protection unifiée client étiquetage** est un ajout récent de plus, pour prendre en charge l’étiquetage unifiée stocker qui prennent en charge plusieurs applications et services. Ce client télécharge les étiquettes de sensibilité et des paramètres de stratégie depuis les centres d’administration suivants : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 et le Centre de conformité Microsoft 365. Pour plus d’informations, consultez [vue d’ensemble des étiquettes de sensibilité](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels).

Si vous ne savez pas quel client utiliser, consultez [choisissez le client Azure Information Protection à utiliser](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use).

### <a name="identify-which-client-you-have-installed"></a>Identifier le client que vous avez installé

Affichent les deux clients, lorsqu’ils sont installés, **Azure Information Protection**. Pour vous aider à identifier le client que vous avez installé, utilisez le **aide et commentaires** option pour ouvrir la **Microsoft Azure Information Protection** boîte de dialogue :

- Depuis l’Explorateur de fichiers : Cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**.

- À partir d’une application Office : À partir de la **protéger** bouton (le client classique) ou **sensibilité** bouton (client unifiée étiquetage), sélectionnez **aide et commentaires**.

Utilisez le **Version** nombre affiché pour identifier le client :

- Une version **1**, par exemple, **1.48.204.0**, identifie le client Azure Information Protection (classique).

- Une version **2**, par exemple, **2.0.778.0**, identifie le client d’étiquetage unifié Azure Information Protection.

## <a name="when-is-the-right-time-to-migrate-my-labels-to-office-365"></a>Comment définir le bon moment pour migrer mes étiquettes vers Office 365 ?

Maintenant que l’option de migration des étiquettes dans le portail Azure est en disponibilité générale, nous vous recommandons d’activer la migration afin que vous pouvez utiliser vos étiquettes en tant qu’étiquettes de sensibilité avec [les clients et les services qui prennent en charge l’étiquetage unifiée](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) .

Pour plus d’informations et pour obtenir des instructions, consultez [comment migrer des étiquettes Azure Information Protection pour les étiquettes de sensibilité d’Office 365](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?

Une fois que vous avez migré vos étiquettes dans le portail Azure :

- Si vous avez [unifiée de l’étiquetage des clients et services](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), accédez à un des centres d’administration (Office 365 Security & centre de conformité, centre de sécurité Microsoft 365 ou centre de conformité de Microsoft 365) pour publier ces étiquettes et pour configurer leurs paramètres de stratégie. À l’avenir, utilisez l’un de ces centres d’administration pour toute modification d’étiquette. Les clients d’étiquetage unifié téléchargent les étiquettes et les paramètres de stratégie à partir de ces centres d’administration.

- Si vous avez des [clients Azure Information Protection](./rms-client/aip-client.md), continuez à utiliser le portail Azure pour modifier vos étiquettes et vos paramètres de stratégie. Les clients Azure Information Protection continuent à télécharger les étiquettes et les paramètres de stratégie à partir d’Azure.

- Si vous avez à la fois des [clients d’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) et des [clients Azure Information Protection](./rms-client/aip-client.md), vous pouvez utiliser les centres d’administration ou le Portail Azure pour effectuer des modifications d’étiquettes. Toutefois, pour que les clients Azure Information Protection récupèrent les changements effectués dans les centres d’administration, vous devez revenir sur le Portail Azure : Utilisez l’option **Publier** du panneau **Azure Information Protection - Étiquetage unifié** dans le portail Azure. 

Continuez à utiliser le portail Azure pour la [centralisation des rapports](reports-aip.md) et le [scanneur](deploy-aip-scanner.md).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection permet à une organisation de classifier, d’étiqueter et de protéger ses documents et e-mails. La technologie de protection utilise le service Azure Rights Management, désormais un composant d’Azure Information Protection.

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Quel est le rôle de gestion des identités pour Azure Information Protection ?

Un utilisateur doit avoir un nom d’utilisateur et un mot de passe valides pour accéder au contenu protégé par Azure Information Protection. Pour en savoir plus sur la façon dont Azure Information Protection permet de sécuriser vos données, consultez [Rôle d’Azure Information Protection dans la sécurisation des données](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?

Consultez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Si vous avez un abonnement Office 365 qui comprend la protection des données Azure Rights Management, téléchargez la [fiche sur les licences Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Vous avez d’autres questions sur les licences ? Regardez si vous trouvez des réponses dans la section [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. Bien que la plupart des présentations et démonstrations du client Azure Information Protection que vous avez vues montrent comment il prend en charge la classification et l’étiquetage, il peut également servir avec les abonnements incluant simplement le service Azure Rights Management pour la protection des données.

Lorsque le client Azure Information Protection pour Windows est installé et qu’il n’a pas de stratégie Azure Information Protection, le client fonctionne automatiquement en [mode protection seule](./rms-client/client-protection-only-mode.md). Dans ce mode, les utilisateurs peuvent facilement appliquer des modèles Rights Management et des autorisations personnalisées. Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?

Les administrateurs généraux d’un locataire Office 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration d’Azure Information Protection. Toutefois, si vous voulez affecter des autorisations d’administration à d’autres utilisateurs, vous avez les options suivantes :

- **Administrateur Azure Information Protection**: Ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer Azure Information Protection, mais pas d’autres services. Un administrateur qui a ce rôle peut activer et désactiver le service de protection Azure Rights Management, configurer les paramètres de protection et les étiquettes, et configurer la stratégie Azure Information Protection. Par ailleurs, un administrateur avec ce rôle peut exécuter toutes les applets de commande PowerShell du [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) et du [module AADRM](administer-powershell.md). Toutefois, ce rôle ne prend en charge le suivi et révocation de documents pour les utilisateurs.
    
    > [!NOTE]
    > Après avoir [migré votre locataire vers le magasin d’étiquetage unifié](configure-policy-migrate-labels.md), ce rôle n’est plus pris en charge pour le portail Azure.
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Administrateur de conformité** ou **administrateur des données de conformité**: Ces Azure Active Directory des rôles d’administrateur permettent à un administrateur de configurer Azure Information Protection, notamment activer et désactiver le service de protection Azure Rights Management, configurer les paramètres de protection et des étiquettes et configurer le Stratégie de Protection des informations Azure. En outre, un administrateur avec un de ces rôles permettre exécuter toutes les applets de commande PowerShell pour le [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) et à partir de la [module AADRM](administer-powershell.md). Toutefois, ces rôles ne prennent en charge le suivi et révocation de documents pour les utilisateurs.
    
    Pour affecter un utilisateur à un de ces rôles d’administration, consultez [affecter un utilisateur à des rôles d’administrateur dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour voir ce qu’ont les autorisations autres un utilisateur avec ces rôles, consultez le [rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) section à partir de la documentation Azure Active Directory.

- **Lecteur Sécurité** : Pour [l’analytique Azure Information Protection](reports-aip.md) uniquement. Ce rôle d’administrateur Azure Active Directory permet à un administrateur de visualiser comment vos étiquettes sont utilisées, de surveiller l’accès utilisateur aux documents et e-mails étiquetés, ainsi que les modifications apportées à leur classification, et peut identifier les documents qui contiennent des informations sensibles devant être protégés. Étant donné que cette fonctionnalité utilise Azure Log Analytics, vous devez également avoir un [rôle RBAC](reports-aip.md#permissions-required-for-azure-information-protection-analytics).

- **Administrateur de sécurité** : Ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer Azure Information Protection dans le portail Azure, en plus de configurer certains aspects d’autres services Azure. Un administrateur disposant de ce rôle ne peut pas exécuter n’importe laquelle de le [applets de commande PowerShell du module AADRM](administer-powershell.md), ou suivre et révoquer des documents pour les utilisateurs.
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour connaître les autres autorisations qu’un rôle donne à un utilisateur, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

- **Administrateur général** et **Administrateur du connecteur** Azure Rights Management : Le premier de ces rôles d’administrateur Azure Rights Management accorde aux utilisateurs l’autorisation d’exécuter toutes les [applets de commande PowerShell du module AADRM](administer-powershell.md) sans pour autant être l’administrateur général des autres services cloud. Le deuxième rôle accorde l’autorisation d’exécuter uniquement le connecteur Rights Management (RMS). Ces rôles d’administration accorder des autorisations aux consoles de gestion ni prise en charge du suivi et révocation de documents pour les utilisateurs.

    Pour affecter un de ces rôles d’administration, utilisez l’applet de commande PowerShell AADRM [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).

Quelques éléments à prendre en compte :

- Si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cette configuration n’affecte pas la possibilité d’administrer Azure Information Protection, à l’exception du connecteur RMS. Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que seul le groupe « Département informatique » puisse protéger du contenu, le compte que vous utilisez pour installer et configurer le connecteur RMS doit être membre de ce groupe. 

- Les utilisateurs avec un rôle d’administration ne peuvent pas supprimer automatiquement la protection des documents ou des e-mails qui ont été protégés par Azure Information Protection. Seuls les super utilisateurs peuvent le faire, sous réserve que la fonctionnalité de super utilisateur soit activée. Toutefois, tout utilisateur avec des autorisations d’administrateur sur Azure Information Protection peut affecter un rôle de super utilisateur, y compris à lui-même. Ils peuvent également activer la fonctionnalité de super utilisateur. Ces actions sont enregistrées dans un journal d’administrateur. Pour plus d’informations, consultez la section des bonnes pratiques dans [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](configure-super-users.md). 

- Si vous migrez vos étiquettes Azure Information Protection dans le magasin d’étiquetage unifié, veillez à lire la section suivante à partir de la documentation de migration d’étiquette : [Informations importantes sur les rôles d’administration](configure-policy-migrate-labels.md#important-information-about-administrative-roles).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous possédez Exchange Server, SharePoint Server et des serveurs de fichiers Windows, vous pouvez déployer le [connecteur Rights Management](deploy-rms-connector.md) afin de permettre à ces serveurs locaux d’utiliser le service Azure Rights Management pour protéger vos e-mails et documents. Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD afin d’offrir une expérience d'authentification simple aux utilisateurs, par exemple, en utilisant [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML en fonction des besoins. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : Première utilisation, protection du contenu, consommation du contenu](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de l’article [Fonctionnement d’Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quels sont les types de données qu’Azure Information Protection peut classifier et protéger ?

Azure Information Protection peut classifier et protéger des e-mails et des documents, localement ou dans le cloud. Ces documents sont notamment des documents Word, des feuilles de calcul Excel, des présentations PowerPoint, des documents PDF, des fichiers texte et des fichiers image. Pour connaître les types de document pris en charge, consultez la liste des [types de fichier pris en charge](./rms-client/client-admin-guide-file-types.md) dans le guide d’administration.

Azure Information Protection ne peut pas classifier et protéger les données structurées telles que les fichiers de base de données, éléments de calendrier, les rapports Power BI, publications Yammer, contenu Sway et blocs-notes OneNote.

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?

Oui, dans le cadre d’une offre de préversion, vous pouvez à présent configurer l’accès conditionnel Azure AD pour Azure Information Protection.

Lorsqu’un utilisateur ouvre un document protégé par Azure Information Protection, les administrateurs peuvent à présent lui bloquer ou lui accorder l’accès, selon les contrôles d’accès conditionnel standard. L’authentification multifacteur (MFA) est l’une des conditions les plus couramment demandées. Une autre condition veut que les appareils soient [conformes à vos stratégies Intune](/intune/conditional-access-intune-common-ways-use) afin que, par exemple, les appareils mobiles puissent répondre à vos critères de mot de passe et de version minimale du système d’exploitation, et que les ordinateurs soient joints à un domaine.

Pour plus d’informations et des exemples de procédure pas à pas, consultez le billet de blog suivant : [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/).

Informations complémentaires :

- Pour les ordinateurs Windows : Pour la préversion actuelle, les stratégies d’accès conditionnel pour Azure Information Protection sont évaluées quand l’[environnement de l’utilisateur est initialisé](./how-does-it-work.md#initializing-the-user-environment) (ce processus est également appelé amorçage), puis tous les 30 jours.

- Vous devrez peut-être ajuster la fréquence à laquelle vos stratégies d’accès conditionnel sont évaluées. Pour cela, configurez la durée de vie des jetons. Pour plus d’informations, consultez [Durées de vie de jeton configurables dans Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Nous vous recommandons de ne pas ajouter de comptes d’administrateur à vos stratégies d’accès conditionnel sans quoi ces comptes ne seront plus en mesure d’accéder au panneau Azure Information Protection dans le portail Azure.

- Si vous utilisez MFA dans vos stratégies d’accès conditionnel pour collaborer avec d’autres organisations (B2B), vous devez utiliser [Azure AD B2B Collaboration](/azure/active-directory/b2b/what-is-b2b) et créer des comptes Invité pour les utilisateurs de l’autre organisation avec lesquels vous souhaitez partager.

- Avec la préversion d’Azure AD publiée en décembre 2018, vous pouvez inviter les utilisateurs à accepter des conditions d’utilisation avant la première ouverture d’un document protégé. Pour plus d’informations, consultez l’annonce dans le billet de blog suivant : [Mises à jour apportées à la fonctionnalité des conditions d’utilisation d’Azure AD dans l’accès conditionnel](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- Si vous utilisez un grand nombre d’applications cloud pour l’accès conditionnel, **Microsoft Azure Information Protection** risque de ne pas s’afficher dans la liste de sélection. Dans ce cas, utilisez la zone de recherche située en haut de la liste. Commencez à taper « Microsoft Azure Information Protection » pour filtrer les applications disponibles. À condition d’avoir un abonnement pris en charge, vous pourrez alors sélectionner **Microsoft Azure Information Protection**. 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Je vois qu’Azure Information Protection est répertorié en tant que fournisseur de sécurité pour Microsoft Graph Security, comment cela fonctionne-t-il et quelles alertes vais-je recevoir ?

Oui, dans le cadre d’une offre de préversion publique, vous pouvez à présent recevoir une alerte pour **l’accès anormal aux données Azure Information Protection**. Cette alerte est déclenchée en cas de tentatives inhabituelles d’accès aux données qui sont protégées par Azure Information Protection. Par exemple, l’accès à un volume anormalement élevé de données, à un moment inhabituel de la journée, ou l’accès à partir d’un emplacement inconnu.

Ces alertes peuvent vous aider à détecter les attaques avancées liées aux données et les menaces internes dans votre environnement. Ces alertes utilisent le Machine Learning pour dresser le profil du comportement des utilisateurs qui accèdent à vos données protégées. 

Les alertes d’Azure Information Protection sont accessibles [à l’aide de l’API Microsoft Graph Security](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview), ou vous pouvez [diffuser des alertes](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration) aux solutions SIEM, comme Splunk et IBM Qradar, à l’aide d’Azure Monitor.

Pour plus d’informations sur l’API Microsoft Graph Security, consultez [Vue d’ensemble de l’API Microsoft Graph Security](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Quelle différence y a-t-il entre l’ICF de Windows Server et le scanneur d’Azure Information Protection ?

L’Infrastructure de classification des fichiers (ICF) de Windows Server a toujours été une option permettant de classer les documents et de les protéger à l’aide du [connecteur Rights Management](deploy-rms-connector.md) (documents Office uniquement) ou d’un [script PowerShell](./rms-client/configure-fci.md) (tous types de fichiers). 

Nous vous recommandons maintenant d’utiliser le [scanneur Azure Information Protection](deploy-aip-scanner.md). Ce scanneur utilise le client Azure Information Protection ainsi que votre stratégie Azure Information Protection pour étiqueter les documents (tous les types de fichiers) afin que ces documents soient ensuite classés, et si vous le souhaitez, protégés.

Les principales différences entre ces deux solutions sont les suivantes :

|ICF de Windows Server|Scanneur Azure Information Protection|
|--------------------------------|-------------------------------------|
|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server<br /><br />- Dispositif de stockage NAS et partages de fichiers Windows<br /><br />- SharePoint Server 2016 et SharePoint Server 2013. SharePoint Server 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).|
|Mode de fonctionnement : <br /><br />- Temps réel|Mode de fonctionnement : <br /><br />- Analyse systématiquement les magasins de données et ce cycle peut s’exécuter une ou plusieurs fois|
|Prise en charge des types de fichiers : <br /><br />- Tous les types de fichiers sont protégés par défaut <br /><br />- Des types de fichiers spécifiques peuvent être exclus de la protection par modification du registre|Prise en charge des types de fichiers : <br /><br />- Les types de fichiers Office et les documents PDF sont protégés par défaut <br /><br />- Des types de fichiers supplémentaires peuvent être inclus dans la protection par modification du Registre|

Actuellement, il existe une différence dans la définition du [propriétaire de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) pour les fichiers qui sont protégés sur un partage réseau ou dans un dossier local. Par défaut, dans les deux solutions, le propriétaire de Rights Management est défini sur le compte qui protège le fichier, mais vous pouvez remplacer ce paramètre :

- Pour l’ICF Windows Server : Vous pouvez définir le propriétaire de Rights Management sur un seul compte pour tous les fichiers, ou définir de façon dynamique ce propriétaire pour chaque fichier. Pour définir le propriétaire de Rights Management de façon dynamique, utilisez le paramètre et la valeur **- OwnerMail [Source File Owner Email]** . Cette configuration récupère l’adresse e-mail de l’utilisateur à partir d’Active Directory en utilisant le nom du compte d’utilisateur dans la propriété Propriétaire du fichier.

- Pour le scanneur Azure Information Protection : Pour les fichiers récemment protégés, vous pouvez définir un seul compte comme propriétaire de Rights Management pour tous les fichiers d’un magasin de données spécifique, mais vous ne pouvez pas définir de façon dynamique ce propriétaire pour chaque fichier. Le propriétaire de Rights Management ne change pas pour les fichiers précédemment protégés. Pour définir le compte des nouveaux fichiers protégés, spécifiez le paramètre **Propriétaire par défaut** dans le profil du scanneur. 

Quand le scanneur protège les fichiers sur les sites et bibliothèques SharePoint, le propriétaire de Rights Management est défini dynamiquement pour chaque fichier à l’aide de la valeur de l’éditeur de SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera disponible prochainement pour Azure Information Protection : quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. Pour ce type d’informations et pour les annonces des versions publiées, consultez le [blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

Si vous êtes intéressé par une version d’Office, n’oubliez pas de consulter également le [blog Office 365](https://techcommunity.microsoft.com/t5/Office-365-Blog/bg-p/Office365Blog) et le [blog Office Apps](https://techcommunity.microsoft.com/t5/Office-Apps-Blog/bg-p/OfficeAppsBlog).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection peut-il être utilisé dans mon pays ?

Les pays ont chacun leurs réglementations et leurs exigences. Pour vous aider à répondre à cette question pour votre organisation, consultez [Adaptation aux différents pays](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Comment Azure Information Protection peut-il aider pour le RGPD ?

Pour savoir comment Azure Information Protection peut vous aider à respecter le Règlement général sur la protection des données (RGPD), consultez l’annonce du billet de blog suivant qui contient une vidéo : [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr).

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>Où puis-je trouver des informations annexes sur Azure Information Protection (considérations juridiques, conformité, contrats de niveau de service, etc.) ?
Consultez [Conformité et informations annexes pour Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Pour le support technique, utilisez vos canaux de support standard ou [contactez le support technique Microsoft](information-support.md#to-contact-microsoft-support).

Nous vous invitons également à contacter l’équipe d’ingénieurs sur son [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que puis-je faire si ma question ne figure pas dans cette rubrique ?

Tout d’abord, passez en revue les questions fréquentes suivantes propres à la classification et à l’étiquetage ou spécifiques de la protection des données. Le service Azure Rights Management (Azure RMS) fournit la technologie de protection des données à Azure Information Protection. Azure RMS peut être utilisé avec la classification et l’étiquetage, ou de façon autonome. 

- [Forum aux questions sur la classification et l’étiquetage](faqs-infoprotect.md)

- [Forum aux questions sur la protection des données](faqs-rms.md)

Si votre question ne fait pas l’objet d’une réponse, utilisez les liens et les ressources figurant dans [Informations et support technique pour Azure Rights Management](information-support.md).

De plus, il existe des questions fréquentes destinées aux utilisateurs finaux :

- [FAQ relatif à l’application Azure Information Protection pour iOS et Android](./rms-client/mobile-app-faq.md)

- [FAQ relatif à l’application de partage RMS pour les ordinateurs Mac](https://technet.microsoft.com/dn451248)

