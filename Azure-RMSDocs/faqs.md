---
title: FAQ relatives à Azure Information Protection
description: Quelques questions fréquemment posées sur Azure Information Protection et son service de protection, Azure Rights Management (Azure RMS).
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 13e6b4ea47c2aafeec24984c7db6aab99a16e9a0
ms.sourcegitcommit: 8c39347d9b7a120014120860fff89c5616641933
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79483182"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Forum aux questions sur Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous avez une question sur Azure Information Protection ou sur le service Azure Rights Management (Azure RMS) ? Vous trouverez peut-être une réponse ici.

Ces pages de questions fréquentes sont régulièrement actualisées. Les nouveautés sont répertoriées dans les avis de mise à jour mensuels de la documentation sur le [blog technique d’Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Quelle est la différence entre Azure Information Protection et Microsoft Information Protection ?

Contrairement à Azure Information Protection, Microsoft Information Protection n’est pas un abonnement ou un produit que vous pouvez acheter. Au lieu de cela, il s’agit d’un framework pour les produits et les fonctionnalités intégrées qui vous aident à protéger les informations sensibles de votre organisation :

- Les produits individuels de ce framework incluent Azure Information Protection, Office 365 Information Protection (par exemple, Office 365 DLP), Windows Information Protection et Microsoft Cloud App Security. 

- Les fonctions intégrées dans ce framework incluent la gestion d’étiquette unifiée, les expériences d’étiquetage de l’utilisateur final intégrées aux applications Office, la possibilité pour Windows de comprendre les étiquettes unifiées et appliquer une protection aux données, le SDK Microsoft Information Protection et de nouvelles fonctionnalités dans Adobe Acrobat Reader pour afficher les fichiers PDF étiquetés et protégés.

Pour plus d’informations, consultez [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annonce de la disponibilité des fonctionnalités de protection des informations pour protéger vos données sensibles).

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Quelle est la différence entre les étiquettes dans Azure Information Protection et les étiquettes dans Office 365 ?

Au départ, Office 365 disposait uniquement [d’étiquettes de conservation](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) pour vous permettre de classifier les documents et les e-mails à des fins d’audit et de conservation quand ce contenu se trouvait dans les services Office 365. Par comparaison, les étiquettes Azure Information Protection vous permettent d’appliquer une stratégie de classification et de protection cohérente aux documents et aux e-mails, qu’ils soient locaux ou dans le cloud.

Annoncée chez 2018 Microsoft, à Orlando, vous avez désormais la possibilité de créer et de configurer des [étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) en plus des étiquettes de rétention dans l’un des centres d’administration : le Centre de sécurité et de conformité Office 365, le centre de sécurité Microsoft 365 ou le centre de conformité Microsoft 365. Vous pouvez migrer vos étiquettes de Azure Information Protection existantes vers le nouveau magasin d’étiquetage unifié, à utiliser comme étiquettes de sensibilité avec les applications Office. 

Pour plus d’informations sur la gestion de l’étiquetage unifié et la prise en charge de ces étiquettes, lisez le billet de blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

Pour plus d’informations sur la migration de vos étiquettes existantes, consultez [Comment migrer des étiquettes Azure information protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?

Lorsque votre locataire se trouve sur la plateforme d’étiquetage unifiée, il prend en charge les étiquettes de sensibilité qui peuvent être utilisées par [les clients et les services qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). Si vous avez obtenu votre abonnement pour Azure Information Protection en juin 2019 ou une version ultérieure, votre locataire est automatiquement sur la plateforme d’étiquetage unifiée et aucune autre action n’est nécessaire. Votre locataire peut également se trouver sur cette plateforme, car quelqu’un a migré vos étiquettes de Azure Information Protection.

Si votre locataire ne fait pas partie de la plateforme d’étiquetage unifiée, vous voyez la bannière d’informations suivante dans le Portail Azure, dans les volets de **Azure information protection** :

![Bannière d’informations sur la migration](media/migration-status-banner.png)

Vous pouvez également vérifier en accédant à **Azure Information Protection** > **gérer** > **étiquette unifiée**et afficher l’état de l' **étiquetage unifiée**:

- Si vous voyez **activé**, votre locataire se trouve sur la plateforme d’étiquetage unifiée et vous pouvez [créer, configurer et publier des étiquettes](/microsoft-365/compliance/create-sensitivity-labels) à partir du centre de conformité Microsoft 365.

- Si vous **ne voyez pas activé**, votre locataire ne se trouve pas sur la plateforme d’étiquetage unifiée. Pour obtenir des instructions et des instructions de migration, consultez [Comment migrer des étiquettes Azure information protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Quelle est la différence entre le client Azure Information Protection et le client d’étiquetage unifié Azure Information Protection ?

Le **client Azure information protection (Classic)** est disponible depuis que Azure information protection a été annoncé pour la première fois en tant que nouveau service de classification et de protection des fichiers et e-mails. Ce client télécharge des étiquettes et des paramètres de stratégie à partir d’Azure, et vous configurez la stratégie de Azure Information Protection à partir du Portail Azure. Pour plus d’informations, consultez [vue d’ensemble de la stratégie de Azure information protection](overview-policy.md). 

Le **Azure information protection client d’étiquetage unifié** est un ajout plus récent, afin de prendre en charge le magasin d’étiquetage unifié que plusieurs applications et services prennent en charge. Ce client télécharge les étiquettes de sensibilité et les paramètres de stratégie à partir des centres d’administration suivants : le Centre de sécurité et de conformité Office 365, le centre de sécurité Microsoft 365 et le centre de conformité Microsoft 365. Pour plus d’informations, consultez [en savoir plus sur les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

Si vous n’êtes pas sûr du client à utiliser, consultez [choisir le client Azure information protection à utiliser](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

### <a name="identify-which-client-you-have-installed"></a>Identifier le client que vous avez installé

Les deux clients, lorsqu’ils sont installés, affichent **Azure information protection**. Pour vous aider à identifier le client que vous avez installé, utilisez l’option **aide et commentaires** pour ouvrir la boîte de dialogue **Microsoft Azure information protection** :

- Dans l’Explorateur de fichiers : cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**.

- À partir d’une application Office : à partir du bouton **protéger** (client classique) ou du bouton **sensibilité** (client d’étiquetage unifié), sélectionnez **aide et commentaires**.

Utilisez le numéro de **version** affiché pour identifier le client :

- Une version **1**, par exemple, **1.53.10.0**, identifie le client Azure information protection (Classic).

- Une version **2**, par exemple, **2.2.14.0**, identifie le client d’étiquetage unifié Azure information protection.

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>Quand est-il approprié de migrer mes étiquettes ?

Maintenant que l’option de migration des étiquettes dans le Portail Azure est en disponibilité générale, nous vous recommandons d’activer la migration afin que vous puissiez utiliser vos étiquettes comme étiquettes de sensibilité avec [les clients et les services qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

Pour plus d’informations et pour obtenir des instructions, consultez [Comment migrer des étiquettes Azure information protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?

Une fois que vous avez migré vos étiquettes dans le portail Azure :

- Si vous avez des [clients et des services d’étiquetage unifiés](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), accédez à l’un des centres d’administration (Office 365 Centre de sécurité et de conformité, Microsoft 365 Security center ou Microsoft 365 Center Compliance Center) pour publier ces étiquettes et configurer leurs paramètres de stratégie. À l’avenir, utilisez l’un de ces centres d’administration pour toute modification d’étiquette. Les clients d’étiquetage unifié téléchargent les étiquettes et les paramètres de stratégie à partir de ces centres d’administration. Pour obtenir des instructions, consultez [créer et configurer des étiquettes de sensibilité et leurs stratégies](/microsoft-365/compliance/create-sensitivity-labels).

- Si vous avez le [client Azure information protection (Classic)](./rms-client/aip-client.md), continuez à utiliser la portail Azure pour modifier vos étiquettes et paramètres de stratégie. Le client classique continue à télécharger des étiquettes et des paramètres de stratégie à partir d’Azure.

- Si vous avez des [clients d’étiquetage unifiés](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) et des [clients classiques](./rms-client/aip-client.md), vous pouvez utiliser les centres d’administration ou le portail Azure pour modifier l’étiquette. Toutefois, pour que les clients classiques récupèrent les modifications d’étiquette que vous apportez dans les centres d’administration, vous devez revenir à la Portail Azure : utilisez l’option **publier** du volet d' **étiquetage Azure information protection-Unified** dans le portail Azure. 

Continuez à utiliser le portail Azure pour la [centralisation des rapports](reports-aip.md) et le [scanneur](deploy-aip-scanner.md).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection permet à une organisation de classifier, d’étiqueter et de protéger ses documents et e-mails. La technologie de protection utilise le service Azure Rights Management, désormais un composant d’Azure Information Protection.

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Quel est le rôle de la gestion des identités pour Azure Information Protection ?

Un utilisateur doit avoir un nom d’utilisateur et un mot de passe valides pour accéder au contenu protégé par Azure Information Protection. Pour en savoir plus sur la façon dont Azure Information Protection permet de sécuriser vos données, consultez [Rôle d’Azure Information Protection dans la sécurisation des données](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?

Consultez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Si vous avez un abonnement Office 365 qui comprend la protection des données Azure Rights Management, téléchargez la [fiche sur les licences Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Vous avez d’autres questions sur les licences ? Regardez si vous trouvez des réponses dans la section [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. Le client Azure Information Protection (Classic) peut également être utilisé avec les abonnements qui incluent uniquement le service Azure Rights Management pour protéger les données.

Lorsque le client classique est installé et qu’il ne dispose pas d’une stratégie de Azure Information Protection, ce client fonctionne automatiquement en [mode protection uniquement](./rms-client/client-protection-only-mode.md). Dans ce mode, les utilisateurs peuvent facilement appliquer des modèles Rights Management et des autorisations personnalisées. Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?

Les administrateurs généraux d’un locataire Office 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration d’Azure Information Protection. Toutefois, si vous voulez affecter des autorisations d’administration à d’autres utilisateurs, vous avez les options suivantes :

- **Administrateur de Azure information protection**: ce rôle d’administrateur de Azure Active Directory permet à un administrateur de configurer Azure information protection, mais pas d’autres services. Un administrateur qui a ce rôle peut activer et désactiver le service de protection Azure Rights Management, configurer les paramètres de protection et les étiquettes, et configurer la stratégie Azure Information Protection. En outre, un administrateur disposant de ce rôle peut exécuter toutes les applets de commande PowerShell pour le [client Azure information protection](./rms-client/client-admin-guide-powershell.md) et à partir du [module AIPService](administer-powershell.md). Toutefois, ce rôle ne prend pas en charge le suivi et la révocation des documents pour les utilisateurs.
    
    > [!NOTE]
    > Ce rôle n’est pas pris en charge dans le Portail Azure si votre locataire se trouve sur la [plateforme d’étiquetage unifiée](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- Administrateur de **conformité** ou **administrateur des données de conformité**: ces rôles d’administrateur Azure Active Directory permettent à un administrateur de configurer Azure information protection, ce qui comprend l’activation et la désactivation du service de protection Azure Rights Management, la configuration des paramètres de protection et des étiquettes et la configuration de la stratégie de Azure information protection. En outre, un administrateur disposant de l’un de ces rôles peut exécuter toutes les applets de commande PowerShell pour le [client Azure information protection](./rms-client/client-admin-guide-powershell.md) et à partir du [module AIPService](administer-powershell.md). Toutefois, ces rôles ne prennent pas en charge le suivi et la révocation des documents pour les utilisateurs.
    
    Pour affecter un utilisateur à l’un de ces rôles d’administration, consultez [affecter un utilisateur à des rôles d’administrateur dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour connaître les autres autorisations dont dispose un utilisateur avec ces rôles, consultez la section [rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation de Azure Active Directory.

- Lecteur de **sécurité** ou **lecteur Global**: pour [Azure information protection Analytics](reports-aip.md) uniquement. Ce rôle d’administrateur Azure Active Directory permet à un administrateur de visualiser comment vos étiquettes sont utilisées, de surveiller l’accès utilisateur aux documents et e-mails étiquetés, ainsi que les modifications apportées à leur classification, et peut identifier les documents qui contiennent des informations sensibles devant être protégés. Étant donné que cette fonctionnalité utilise Azure Monitor, vous devez également disposer d’un [rôle RBAC](reports-aip.md#permissions-required-for-azure-information-protection-analytics)de prise en charge.

- **Administrateur**de la sécurité : ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer Azure information protection dans le portail Azure, en plus de la configuration de certains aspects des autres services Azure. Un administrateur disposant de ce rôle ne peut pas exécuter les [applets de commande PowerShell à partir du module AIPService](administer-powershell.md), ni suivre et révoquer des documents pour les utilisateurs.
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour connaître les autres autorisations qu’un rôle donne à un utilisateur, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

- Administrateur **général** et administrateur de **connecteur**Azure Rights Management : pour ces rôles d’administrateur Azure Rights Management, le premier accorde aux utilisateurs les autorisations d’exécuter toutes les [applets de commande PowerShell à partir du module AIPService](administer-powershell.md) sans en faire un administrateur global pour d’autres services Cloud, et le second rôle accorde des autorisations pour exécuter uniquement le connecteur Rights Management (RMS). Aucun de ces rôles d’administration n’accorde d’autorisations aux consoles de gestion ou de suivi et de révocation des documents pour les utilisateurs.
    
    Pour affecter l’un de ces rôles d’administration, utilisez l’applet de commande PowerShell AIPService, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

Quelques éléments à prendre en compte :

- Les comptes Microsoft ne sont pas pris en charge pour l’administration déléguée de Azure Information Protection, même si ces comptes sont affectés à l’un des rôles d’administration répertoriés. 

- Si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cette configuration n’affecte pas la possibilité d’administrer Azure Information Protection, à l’exception du connecteur RMS. Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que la capacité à protéger le contenu soit limitée au groupe « département informatique », le compte que vous utilisez pour installer et configurer le connecteur RMS doit être membre de ce groupe. 

- Les utilisateurs avec un rôle d’administration ne peuvent pas supprimer automatiquement la protection des documents ou des e-mails qui ont été protégés par Azure Information Protection. Seuls les super utilisateurs peuvent le faire, sous réserve que la fonctionnalité de super utilisateur soit activée. Toutefois, tout utilisateur avec des autorisations d’administrateur sur Azure Information Protection peut affecter un rôle de super utilisateur, y compris à lui-même. Ils peuvent également activer la fonctionnalité de super utilisateur. Ces actions sont enregistrées dans un journal d’administrateur. Pour plus d’informations, consultez la section meilleures pratiques en matière de sécurité dans [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](configure-super-users.md). 

- Si vous migrez vos étiquettes de Azure Information Protection vers le magasin d’étiquetage unifié, veillez à lire la section suivante dans la documentation sur la migration des étiquettes : les [rôles d’administration qui prennent en charge la plateforme d’étiquetage unifiée](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous possédez Exchange Server, SharePoint Server et des serveurs de fichiers Windows, vous pouvez déployer le [connecteur Rights Management](deploy-rms-connector.md) afin de permettre à ces serveurs locaux d’utiliser le service Azure Rights Management pour protéger vos e-mails et documents. Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD afin d’offrir une expérience d'authentification simple aux utilisateurs, par exemple, en utilisant [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML en fonction des besoins. il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, voir la section [Présentation du fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de l’article [Fonctionnement d’Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quels sont les types de données qu’Azure Information Protection peut classifier et protéger ?

Azure Information Protection peut classifier et protéger des e-mails et des documents, localement ou dans le cloud. Ces documents sont notamment des documents Word, des feuilles de calcul Excel, des présentations PowerPoint, des documents PDF, des fichiers texte et des fichiers image. Pour connaître les types de document pris en charge, consultez la liste des [types de fichier pris en charge](./rms-client/clientv2-admin-guide-file-types.md) dans le guide d’administration.

Azure Information Protection ne pouvez pas classifier et protéger des données structurées telles que des fichiers de base de données, des éléments de calendrier, des publications Yammer, du contenu Sway et des blocs-notes OneNote.

**Récemment annoncé en**préversion : Power bi prend désormais en charge la classification à l’aide d’étiquettes de sensibilité et peut appliquer la protection de ces étiquettes aux données exportées aux formats de fichier suivants :. pdf,. xls et. ppt. Pour plus d’informations, consultez [protection des données en Power bi (version préliminaire)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview).

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?

Oui, dans le cadre d’une offre de préversion, vous pouvez à présent configurer l’accès conditionnel Azure AD pour Azure Information Protection.

Lorsqu’un utilisateur ouvre un document protégé par Azure Information Protection, les administrateurs peuvent à présent lui bloquer ou lui accorder l’accès, selon les contrôles d’accès conditionnel standard. L’authentification multifacteur (MFA) est l’une des conditions les plus couramment demandées. Une autre condition veut que les appareils soient [conformes à vos stratégies Intune](/intune/conditional-access-intune-common-ways-use) afin que, par exemple, les appareils mobiles puissent répondre à vos critères de mot de passe et de version minimale du système d’exploitation, et que les ordinateurs soient joints à un domaine.

Pour plus d’informations et des exemples de procédure pas à pas, consultez le blog suivant : [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Stratégies d’accès conditionnel pour Azure Information Protection).

Informations complémentaires :

- Pour les ordinateurs Windows : pour la préversion actuelle, les stratégies d’accès conditionnel pour Azure Information Protection sont évaluées quand l’[environnement de l’utilisateur est initialisé](./how-does-it-work.md#initializing-the-user-environment) (ce processus est également appelé amorçage), puis tous les 30 jours.

- Vous devrez peut-être ajuster la fréquence à laquelle vos stratégies d’accès conditionnel sont évaluées. Pour cela, configurez la durée de vie des jetons. Pour plus d’informations, consultez [Durées de vie de jeton configurables dans Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Nous vous recommandons de ne pas ajouter de comptes d’administrateur à vos stratégies d’accès conditionnel, car ces comptes ne seront pas en mesure d’accéder au volet de Azure Information Protection dans le Portail Azure.

- Si vous utilisez MFA dans vos stratégies d’accès conditionnel pour collaborer avec d’autres organisations (B2B), vous devez utiliser [Azure AD B2B Collaboration](/azure/active-directory/b2b/what-is-b2b) et créer des comptes Invité pour les utilisateurs de l’autre organisation avec lesquels vous souhaitez partager.

- Avec la préversion d’Azure AD publiée en décembre 2018, vous pouvez inviter les utilisateurs à accepter des conditions d’utilisation avant la première ouverture d’un document protégé. Pour plus d’informations, consultez le billet de blog suivant : [mises à jour de Azure ad fonctionnalités de conditions d’utilisation dans l’accès conditionnel](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- Si vous utilisez un grand nombre d’applications cloud pour l’accès conditionnel, **Microsoft Azure Information Protection** risque de ne pas s’afficher dans la liste de sélection. Dans ce cas, utilisez la zone de recherche située en haut de la liste. Commencez à taper « Microsoft Azure Information Protection » pour filtrer les applications disponibles. À condition d’avoir un abonnement pris en charge, vous pourrez alors sélectionner **Microsoft Azure Information Protection**. 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Je vois qu’Azure Information Protection est répertorié en tant que fournisseur de sécurité pour Microsoft Graph Security, comment cela fonctionne-t-il et quelles alertes vais-je recevoir ?

Oui, dans le cadre d’une offre de préversion publique, vous pouvez à présent recevoir une alerte pour **l’accès anormal aux données Azure Information Protection**. Cette alerte est déclenchée en cas de tentatives inhabituelles d’accès aux données qui sont protégées par Azure Information Protection. Par exemple, l’accès à un volume anormalement élevé de données, à un moment inhabituel de la journée, ou l’accès à partir d’un emplacement inconnu.

Ces alertes peuvent vous aider à détecter les attaques avancées liées aux données et les menaces internes dans votre environnement. Ces alertes utilisent le Machine Learning pour dresser le profil du comportement des utilisateurs qui accèdent à vos données protégées. 

Les alertes d’Azure Information Protection sont accessibles [à l’aide de l’API Microsoft Graph Security](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview), ou vous pouvez [diffuser des alertes](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration) aux solutions SIEM, comme Splunk et IBM Qradar, à l’aide d’Azure Monitor.

Pour plus d’informations sur l’API Microsoft Graph Security, consultez [Vue d’ensemble de l’API Microsoft Graph Security](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Quelle est la différence entre Windows Server FCI et le scanneur Azure Information Protection ?

L’Infrastructure de classification des fichiers (ICF) de Windows Server a toujours été une option permettant de classer les documents et de les protéger à l’aide du [connecteur Rights Management](deploy-rms-connector.md) (documents Office uniquement) ou d’un [script PowerShell](./rms-client/configure-fci.md) (tous types de fichiers). 

Nous vous recommandons maintenant d’utiliser le [scanneur Azure Information Protection](deploy-aip-scanner.md). Ce scanneur utilise le client Azure Information Protection ainsi que votre stratégie Azure Information Protection pour étiqueter les documents (tous les types de fichiers) afin que ces documents soient ensuite classés, et si vous le souhaitez, protégés.

Les principales différences entre ces deux solutions sont les suivantes :

|ICF de Windows Server|Scanneur Azure Information Protection|
|--------------------------------|-------------------------------------|
|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server|Magasins de données pris en charge : <br /><br />- Dossiers locaux sur Windows Server<br /><br />- Dispositif de stockage NAS et partages de fichiers Windows<br /><br />- SharePoint Server 2016 et SharePoint Server 2013. SharePoint Server 2010 est également pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).|
|Mode de fonctionnement : <br /><br />- Temps réel|Mode de fonctionnement : <br /><br />- Analyse systématiquement les magasins de données et ce cycle peut s’exécuter une ou plusieurs fois|
|Prise en charge des types de fichiers : <br /><br />- Tous les types de fichiers sont protégés par défaut <br /><br />- Des types de fichiers spécifiques peuvent être exclus de la protection par modification du registre|Prise en charge des types de fichiers : <br /><br />- Les types de fichiers Office et les documents PDF sont protégés par défaut <br /><br />- Des types de fichiers supplémentaires peuvent être inclus dans la protection par modification du Registre|

Il existe une différence dans la définition de la [Rights Management propriétaire](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) pour les fichiers protégés sur un dossier local ou un partage réseau. Par défaut, dans les deux solutions, le propriétaire de Rights Management est défini sur le compte qui protège le fichier, mais vous pouvez remplacer ce paramètre :

- Pour l’ICF de Windows Server, vous pouvez définir le propriétaire de Rights Management sur un seul compte pour tous les fichiers, ou définir de façon dynamique ce propriétaire pour chaque fichier. Pour définir le propriétaire de Rights Management de façon dynamique, utilisez le paramètre et la valeur **- OwnerMail [Source File Owner Email]** . Cette configuration récupère l’adresse e-mail de l’utilisateur à partir d’Active Directory en utilisant le nom du compte d’utilisateur dans la propriété Propriétaire du fichier.

- Pour le scanneur de Azure Information Protection : pour les fichiers récemment protégés, vous pouvez définir le Rights Management propriétaire comme un compte unique pour tous les fichiers d’une banque de données spécifiée, mais vous ne pouvez pas définir dynamiquement le propriétaire Rights Management pour chaque fichier. Le propriétaire de Rights Management ne change pas pour les fichiers précédemment protégés. Pour définir le compte des nouveaux fichiers protégés, spécifiez le paramètre **Propriétaire par défaut** dans le profil du scanneur. 

Quand le scanneur protège les fichiers sur les sites et bibliothèques SharePoint, le propriétaire de Rights Management est défini dynamiquement pour chaque fichier à l’aide de la valeur de l’éditeur de SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera bientôt disponible, par Azure Information Protection, quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. Pour ce type d’informations, utilisez la feuille de [route Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), consultez le [blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection peut-il être utilisé dans mon pays ?

Les pays ont chacun leurs réglementations et leurs exigences. Pour vous aider à répondre à cette question pour votre organisation, consultez [Adaptation aux différents pays](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Comment Azure Information Protection peut-il aider pour le RGPD ?

Pour savoir comment Azure Information Protection peut vous aider à respecter le Règlement général sur la protection des données (RGPD), consultez l’annonce du billet de blog suivant qui contient une vidéo : [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr).

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>Où puis-je trouver des informations annexes sur Azure Information Protection (considérations juridiques, conformité, contrats de niveau de service, etc.) ?
Consultez [Conformité et informations annexes pour Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Pour le support technique, utilisez vos canaux de support standard ou [contactez le support technique Microsoft](information-support.md#to-contact-microsoft-support).

Nous vous invitons également à contacter l’équipe d’ingénieurs sur son [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que dois-je faire si ma question n’est pas disponible ?

Tout d’abord, passez en revue les questions fréquentes suivantes propres à la classification et à l’étiquetage ou spécifiques de la protection des données. Le service Azure Rights Management (Azure RMS) fournit la technologie de protection des données à Azure Information Protection. Azure RMS peut être utilisé avec la classification et l’étiquetage, ou de façon autonome. 

- [Forum aux questions sur la classification et l’étiquetage](faqs-infoprotect.md)

- [Forum aux questions sur la protection des données](faqs-rms.md)

Si votre question ne fait pas l’objet d’une réponse, utilisez les liens et les ressources figurant dans [Informations et support technique pour Azure Rights Management](information-support.md).

De plus, il existe des questions fréquentes destinées aux utilisateurs finaux :

- [FAQ relatif à l’application Azure Information Protection pour iOS et Android](./rms-client/mobile-app-faq.md)

- [FAQ relatif à l’application de partage RMS pour les ordinateurs Mac](https://technet.microsoft.com/dn451248)

