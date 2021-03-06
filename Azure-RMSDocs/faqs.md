---
title: FAQ pour Azure Information Protection (AIP)
description: Obtenir des réponses aux questions fréquemment posées sur Azure Information Protection (AIP) et son service de protection, Azure Rights Management (Azure RMS).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 9f19b02045ea98fe7c7dc54299ea60abaa6d3312
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415005"
---
# <a name="frequently-asked-questions-for-azure-information-protection-aip"></a>Forum aux questions pour Azure Information Protection (AIP)

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous avez une question sur Azure Information Protection (AIP) ou sur le service Azure Rights Management (Azure RMS) ? 

Regardez si la réponse est indiquée ci-dessous ou sur les [pages de FAQ plus spécifiques, plus spécifiques](#what-do-i-do-if-my-question-isnt-here).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Quelle est la différence entre Azure Information Protection et Microsoft Information Protection ?

Contrairement à Azure Information Protection, [Microsoft information protection](https://www.microsoft.com/security/business/information-protection) n’est pas un abonnement ou un produit que vous pouvez acheter. Au lieu de cela, il s’agit d’une infrastructure pour les produits et des fonctionnalités intégrées qui vous aident à protéger les informations sensibles de votre organisation.

Les **produits Microsoft information protection sont** les suivants :
- Azure Information Protection
- Microsoft 365 Information Protection, comme Microsoft 365 DLP
- Protection des informations Windows
- Microsoft Cloud App Security

Les **fonctionnalités de Microsoft information protection sont** les suivantes :
- Gestion unifiée des étiquettes
- Expériences d’étiquetage des utilisateurs finaux intégrés aux applications Office
- La capacité de Windows à comprendre les étiquettes unifiées et à appliquer la protection aux données
- Kit de développement logiciel (SDK) Microsoft Information Protection
- Fonctionnalités d’Adobe Acrobat Reader pour afficher les fichiers PDF étiquetés et protégés

Pour plus d’informations, consultez [fonctionnalités de protection des informations pour vous aider à protéger vos données sensibles](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

## <a name="whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection"></a>Quelle est la différence entre les étiquettes dans Microsoft 365 et les étiquettes dans Azure Information Protection ?

À l’origine, Microsoft 365 aviez uniquement des [étiquettes de rétention](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30), ce qui vous permettait de classer les documents et les e-mails à des fins d’audit et de rétention lorsque ce contenu a été stocké dans Microsoft 365 services. 

En revanche, Azure Information Protection étiquettes, configurées au moment de l’utilisation du client standard AIP dans le Portail Azure, vous permettait d’appliquer une stratégie de classification et de protection cohérente pour les documents et e-mails, qu’ils aient été stockés localement ou dans le Cloud.

Microsoft 365 prend désormais en charge les [étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) en plus des étiquettes de rétention. Des étiquettes de sensibilité peuvent être créées et configurées dans les centres d’administration suivants :

- Centre de sécurité et conformité Office 365
- Centre de sécurité Microsoft 365
- Centre de conformité Microsoft 365

Si des étiquettes AIP héritées sont configurées dans le Portail Azure, nous vous recommandons de les migrer vers des étiquettes de sensibilité et un client d’étiquetage unifié. Pour plus d’informations, consultez [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md).

Pour plus d’informations, consultez [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annonce de la disponibilité des fonctionnalités de protection des informations pour protéger vos données sensibles).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?

Lorsque votre locataire se trouve sur la plateforme d’étiquetage unifiée, il prend en charge les étiquettes de sensibilité qui peuvent être utilisées par [les clients et les services qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). Si vous avez obtenu votre abonnement pour Azure Information Protection en juin 2019 ou une version ultérieure, votre locataire est automatiquement sur la plateforme d’étiquetage unifiée et aucune autre action n’est nécessaire. Votre locataire peut également se trouver sur cette plateforme, car quelqu’un a migré vos étiquettes de Azure Information Protection.

Si votre locataire ne se trouve pas sur la plateforme d’étiquetage unifiée, vous verrez la bannière d’informations suivante dans le Portail Azure, dans les volets de **Azure information protection** :

![Bannière d’informations sur la migration](media/migration-status-banner.png)

Vous pouvez également vérifier en accédant à **Azure information protection**  >  **gérer**  >  l'**étiquetage unifiée** et afficher l’état d' **étiquetage unifiée** :

|Statut |Description  |
|---------|---------|
|**Activat**     |  Votre locataire se trouve sur la plateforme d’étiquetage unifiée. <br />Vous pouvez [créer, configurer et publier des étiquettes](/microsoft-365/compliance/create-sensitivity-labels) à partir du centre de conformité Microsoft 365.       |
|**Non activé**    |  Votre locataire n’est pas sur la plateforme d’étiquetage unifiée. <br />Pour obtenir des instructions et des instructions de migration, consultez [Comment migrer des étiquettes Azure information protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md).       |
| | |

## <a name="whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients"></a>Quelle est la différence entre les Azure Information Protection clients d’étiquetage classiques et unifiés ?

Le client de Azure Information Protection hérité, appelé client *classique* , télécharge des étiquettes et des paramètres de stratégie à partir d’Azure, et vous permet de configurer la [stratégie AIP](overview-policy.md) à partir du portail Azure.

Le *client d’étiquetage unifié* est le client le plus récent avec les mises à jour les plus récentes et prend en charge la plateforme d’étiquetage unifiée utilisée par plusieurs applications et services. Le client d’étiquetage unifié télécharge les [étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) et les paramètres de stratégie à partir des centres d’administration suivants :

- Centre de sécurité et conformité Office 365
- Centre de sécurité Microsoft 365
- Centre de conformité Microsoft 365

Si vous êtes un administrateur, pour en savoir plus, consultez [choisir votre solution d’étiquetage Windows](rms-client/use-client.md#choose-your-windows-labeling-solution).

### <a name="classic-client-deprecation"></a>Désapprobation du client classique

Pour fournir une expérience client unifiée et rationalisée, le Azure Information Protection la gestion des clients et des **étiquettes** **classic** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. 

Après la désapprobation, le client continuera de fonctionner comme prévu. Toutefois, les administrateurs ne seront pas en mesure de mettre à jour les stratégies sur le portail, et aucun autre correctif ou changement ne sera fourni pour le client classique.

Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Si le client classique est actuellement déployé, nous vous recommandons d’effectuer la mise à niveau vers le client d’étiquetage unifié. Pour plus d’informations, consultez ;

- [Didacticiel : migration du client classique vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md)
- [Comment migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md)
### <a name="identify-the-client-you-have-installed"></a>Identifier le client que vous avez installé

Si vous êtes un utilisateur qui souhaite savoir si le client classique ou le client d’étiquetage unifié est installé, vous pouvez effectuer l’une des opérations suivantes :

- Dans vos applications Office, recherchez le bouton **sensibilité** ou **protéger** la barre d’outils. Le client d’étiquetage unifié affiche le bouton **sensibilité** :::image type="icon" source="media/i-sensitivity.PNG" border="false"::: , tandis que le client classique affiche le bouton **protéger** . 

- Vérifiez le numéro de version de l’application Azure Information Protection que vous avez installée.

    - Les versions **1. x** indiquent que vous disposez du client classique. Exemple : **1.54.59.0**
    - Les versions **2. x** indiquent que vous disposez du client d’étiquetage unifié. Exemple : **2.8.85.0**

    Par exemple, dans les **Paramètres Windows > zone applications et fonctionnalités** , faites défiler jusqu’à l’application **Microsoft Azure information protection** , puis vérifiez le numéro de version.

    :::image type="content" source="media/client-about.png" alt-text="Vérifier la version du client Azure Information Protection":::

## <a name="when-is-the-right-time-to-migrate-my-labels-to-unified-labeling"></a>Quand est-il approprié de migrer mes étiquettes vers un étiquetage unifié ?

Nous vous recommandons de migrer vos étiquettes Azure Information Protection vers la plateforme d’étiquetage unifiée afin de pouvoir les utiliser en tant qu’étiquettes de sensibilité avec d’autres [clients et services qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

Pour plus d’informations et pour obtenir des instructions, consultez [Comment migrer des étiquettes Azure information protection vers des étiquettes de sensibilité unifiée](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-to-unified-labeling-which-management-portal-do-i-use"></a>Une fois que j’ai migré mes étiquettes vers l’étiquetage unifié, quel portail de gestion dois-je utiliser ?

Une fois que vous avez migré vos étiquettes dans le Portail Azure, continuez à les gérer dans l’un des emplacements suivants, selon les clients que vous avez installés :

|Client  |Description  |
|---------|---------|
|[Clients et services d’étiquetage unifiés](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) uniquement    |  Si vous avez uniquement des clients d’étiquetage unifiés installés, gérez vos étiquettes dans l’un des centres d’administration : Office 365 Security & Compliance Center, Microsoft 365 Security Center ou Microsoft 365 Center Compliance Center. Les clients d’étiquetage unifié téléchargent les étiquettes et les paramètres de stratégie à partir de ces centres d’administration. <br /><br />Pour obtenir des instructions, consultez [créer et configurer des étiquettes de sensibilité et leurs stratégies](/microsoft-365/compliance/create-sensitivity-labels).     |
|[Client classique](./rms-client/aip-client.md) uniquement  | Si vous avez migré vos étiquettes, mais que le client Classic est toujours installé, continuez à utiliser la Portail Azure pour modifier les étiquettes et les paramètres de stratégie. Le client classique continue à télécharger des étiquettes et des paramètres de stratégie à partir d’Azure.
|Le [client standard](./rms-client/aip-client.md) AIP et les clients d' [étiquetage unifiés](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)     | Si vous avez installé les deux clients, utilisez les centres d’administration ou le Portail Azure pour apporter des modifications aux étiquettes. <br /><br />Pour que les clients classiques récupèrent les modifications apportées aux étiquettes dans les centres d’administration, revenez à la Portail Azure pour les publier. Dans le volet Portail Azure > **Azure information protection-nom unifié** , sélectionnez **publier**.  <br /><br /> Continuez à utiliser le portail Azure pour la [centralisation des rapports](reports-aip.md) et le [scanneur](deploy-aip-scanner.md).     |
| | |

## <a name="do-i-need-to-re-encrypt-my-files-after-moving-to-sensitivity-labels-and-the-unified-labeling-platform"></a>Dois-je rechiffrer mes fichiers après leur passage à des étiquettes de sensibilité et à la plateforme d’étiquetage unifiée ?

Non, vous n’avez pas besoin de chiffrer à nouveau vos fichiers après avoir déplacé vers les étiquettes de sensibilité et la plateforme d’étiquetage unifiée après la migration à partir du client classique AIP et des étiquettes gérées dans le Portail Azure.

Après la migration, gérez vos étiquettes et vos stratégies d’étiquetage à partir de votre centre d’administration d’étiquetage, y compris Microsoft Security Center, Microsoft Compliance Center ou Microsoft Security & Compliance Center. 

Pour plus d’informations, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365 et le blog présentation de la migration de l' [étiquetage unifié](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185) .


## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection (AIP) fournit la classification, l’étiquetage et la protection des documents et e-mails d’une organisation.

Le contenu est protégé à l’aide du service Azure Rights Management, qui est désormais un composant d’AIP. 

Pour plus d’informations, consultez [Comment AIP protège vos données](aip-classification-and-protection.md#how-aip-protects-your-data) et [qu’est-ce qu’Azure Rights Management ?](what-is-azure-rms.md).

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Quel est le rôle de la gestion des identités pour Azure Information Protection ?

La gestion des identités est un composant important d’AIP, car les utilisateurs doivent disposer d’un nom d’utilisateur et d’un mot de passe valides pour accéder au contenu protégé.

Pour en savoir plus sur la façon dont Azure Information Protection permet de sécuriser vos données, consultez [Rôle d’Azure Information Protection dans la sécurisation des données](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?

Pour en savoir plus sur les abonnements AIP, consultez les informations d’abonnement et la liste des fonctionnalités sur la page de [tarification Azure information protection](https://azure.microsoft.com/pricing/details/information-protection) .

Si vous disposez d’un abonnement Microsoft 365 qui comprend la protection des données Azure Rights Management, téléchargez la [fiche technique de licence Azure information protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) pour plus d’informations sur l’intégration avec AIP.

Vous avez d’autres questions sur les licences ? Regardez si vous trouvez des réponses dans la section [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?

Les administrateurs généraux pour un locataire Microsoft 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration pour Azure Information Protection. 

Toutefois, si vous souhaitez affecter des autorisations d’administration à d’autres utilisateurs, utilisez les rôles suivants :

- [Administrateur Azure Information Protection](#azure-information-protection-administrator)
- [Administrateur de conformité ou administrateur des données de conformité](#compliance-administrator-or-compliance-data-administrator)
- [Lecteur de sécurité ou lecteur global](#security-reader-or-global-reader)
- [Administrateur de sécurité](#security-administrator)
- [Administrateur général et administrateur du connecteur Azure Rights Management](#azure-rights-management-global-administrator-and-connector-administrator)

En outre, notez les points suivants lors de la gestion des tâches et des rôles d’administration :

|Problème  |Détails  |
|---------|---------|
|**Types de comptes pris en charge**     | Les comptes Microsoft ne sont pas pris en charge pour l’administration déléguée de Azure Information Protection, même si ces comptes sont affectés à l’un des rôles d’administration répertoriés.         |
|**Contrôles d’intégration**     |Si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cette configuration n’affecte pas la possibilité d’administrer Azure Information Protection, à l’exception du connecteur RMS. <br /><br />Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que la capacité à protéger le contenu soit limitée au groupe *service informatique* , le compte utilisé pour installer et configurer le connecteur RMS doit être membre de ce groupe.          |
|**Suppression de la protection**     |  Les administrateurs ne peuvent pas supprimer automatiquement la protection des documents ou des e-mails qui ont été protégés par Azure Information Protection. <br /><br />Seuls les utilisateurs qui sont affectés en tant que super utilisateurs peuvent supprimer la protection et uniquement lorsque la fonctionnalité de super utilisateur est activée. <br /><br />Tout utilisateur disposant d’autorisations d’administration pour Azure Information Protection peut activer la fonctionnalité de super utilisateur et affecter des utilisateurs en tant que super utilisateurs, y compris leur propre compte.<br /><br />Ces actions sont enregistrées dans un journal d’administrateur. <br /><br />Pour plus d’informations, consultez la section meilleures pratiques en matière de sécurité dans [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](configure-super-users.md). <br><br>**Conseil**: Si votre contenu est stocké dans SharePoint ou OneDrive, les administrateurs peuvent exécuter l’applet de commande [Unlock-SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) pour supprimer l’étiquette de sensibilité et le chiffrement. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document). |
|**Migration vers le magasin d’étiquetage unifié**      |  Si vous migrez vos étiquettes de Azure Information Protection vers le magasin d’étiquetage unifié, veillez à lire la section suivante dans la documentation relative à la migration des étiquettes : <br />[Rôles d’administration qui prennent en charge la plateforme d’étiquetage unifiée](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform). |
| | |
### <a name="azure-information-protection-administrator"></a>Administrateur Azure Information Protection

Ce rôle d’administrateur Azure Active Directory permet à un administrateur de configurer Azure Information Protection mais pas d’autres services. 

Les administrateurs disposant de ce rôle peuvent :

- Activer et désactiver le service de protection Azure Rights Management
- Configurer les paramètres de protection et les étiquettes
- Configurer la stratégie Azure Information Protection
- Exécuter toutes les applets de commande PowerShell pour le [client Azure information protection](./rms-client/clientv2-admin-guide-powershell.md) et à partir du [module AIPService](administer-powershell.md)
    
Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

> [!NOTE]
> Ce rôle ne prend pas en charge le suivi et la révocation des documents pour les utilisateurs, et n’est pas pris en charge dans le Portail Azure si votre locataire se trouve sur la [plateforme d’étiquetage unifiée](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
### <a name="compliance-administrator-or-compliance-data-administrator"></a>Administrateur de conformité ou administrateur des données de conformité

Ces rôles d’administrateur Azure Active Directory permettent aux administrateurs d’effectuer les opérations suivantes :

- Configurer Azure Information Protection, y compris l’activation et la désactivation du service Azure Rights Management protection
- Configurer les paramètres de protection et les étiquettes
- Configurer la stratégie Azure Information Protection
- Exécutez toutes les applets de commande PowerShell pour le [client Azure information protection](./rms-client/clientv2-admin-guide-powershell.md) et à partir du [module AIPService](administer-powershell.md). 

Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). 

Pour connaître les autres autorisations dont dispose un utilisateur avec ces rôles, consultez la section [rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation de Azure Active Directory.

> [!NOTE]
> Ces rôles ne prennent pas en charge le suivi et la révocation des documents pour les utilisateurs.
>     
    
### <a name="security-reader-or-global-reader"></a>Lecteur de sécurité ou lecteur global

Ces rôles sont utilisés pour [Azure information protection Analytics](reports-aip.md) uniquement et permettent aux administrateurs d’effectuer les opérations suivantes :

- Afficher l’utilisation de vos étiquettes
- Surveiller l’accès des utilisateurs aux documents étiquetés et aux e-mails
- Afficher les modifications apportées à la classification
- Identifier les documents qui contiennent des informations sensibles qui doivent être protégées 

Étant donné que cette fonctionnalité utilise Azure Monitor, vous devez également disposer d’un [rôle RBAC](reports-aip.md#permissions-required-for-azure-information-protection-analytics)de prise en charge.

### <a name="security-administrator"></a>Administrateur de sécurité

Ce rôle d’administrateur Azure Active Directory permet aux administrateurs de configurer Azure Information Protection dans le Portail Azure et certains aspects des autres services Azure. 

Les administrateurs disposant de ce rôle ne peuvent pas exécuter les [applets de commande PowerShell à partir du module AIPService](administer-powershell.md), ni suivre et révoquer des documents pour les utilisateurs.
    
Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). 

Pour connaître les autres autorisations qu’un rôle donne à un utilisateur, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

### <a name="azure-rights-management-global-administrator-and-connector-administrator"></a>Administrateur général et administrateur du connecteur Azure Rights Management

Le rôle d’administrateur général permet aux utilisateurs d’exécuter toutes les [applets de commande PowerShell à partir du module AIPService](administer-powershell.md) sans en faire un administrateur global pour d’autres services Cloud.

Le rôle d’administrateur de connecteur permet aux utilisateurs d’exécuter uniquement le connecteur Rights Management (RMS). 

Ces rôles d’administration n’accordent pas d’autorisations aux consoles de gestion, ou prennent en charge le suivi et la révocation des documents pour les utilisateurs.
    
Pour affecter l’un de ces rôles d’administration, utilisez l’applet de commande PowerShell AIPService, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous avez Exchange Server, SharePoint Server et les serveurs de fichiers Windows, utilisez l’une des méthodes suivantes, ou les deux :

- Déployer le [connecteur Rights Management](deploy-rms-connector.md) afin que ces serveurs locaux puissent utiliser le service Azure Rights Management pour protéger vos e-mails et vos documents
- Synchronisez et fédérer vos contrôleurs de domaine Active Directory avec Azure AD pour une expérience d’authentification plus transparente pour les utilisateurs. Par exemple, utilisez [Azure ad Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML en fonction des besoins. il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. 

Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, consultez la [procédure pas à pas de fonctionnement de Azure RMS : première utilisation, protection du contenu, consommation du contenu](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quels sont les types de données qu’Azure Information Protection peut classifier et protéger ?

Azure Information Protection peut classifier et protéger des e-mails et des documents, localement ou dans le cloud. Ces documents sont notamment des documents Word, des feuilles de calcul Excel, des présentations PowerPoint, des documents PDF, des fichiers texte et des fichiers image. 

Pour plus d’informations, consultez la liste complète des [types de fichiers pris en charge](./rms-client/clientv2-admin-guide-file-types.md).

> [!NOTE]
> Azure Information Protection ne pouvez pas classifier et protéger des données structurées telles que des fichiers de base de données, des éléments de calendrier, des publications Yammer, du contenu Sway et des blocs-notes OneNote.
> 

> [!TIP]
> Power BI prend en charge la classification à l’aide d’étiquettes de sensibilité et peut appliquer la protection de ces étiquettes aux données exportées aux formats de fichier suivants :. pdf,. xls et. ppt. Pour plus d’informations, consultez [Protection des données dans Power BI](/power-bi/admin/service-security-data-protection-overview).
> 
## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?

Oui, en tant qu’offre de préversion, vous pouvez configurer l’accès conditionnel Azure AD pour Azure Information Protection.

Lorsqu’un utilisateur ouvre un document protégé par Azure Information Protection, les administrateurs peuvent à présent lui bloquer ou lui accorder l’accès, selon les contrôles d’accès conditionnel standard. L’authentification multifacteur (MFA) est l’une des conditions les plus couramment demandées. Une autre est que les appareils doivent être [conformes à vos stratégies Intune](/intune/protect/conditional-access-intune-common-ways-use) afin que, par exemple, les appareils mobiles répondent à vos exigences de mot de passe et à une version minimale du système d’exploitation, et que les ordinateurs doivent être joints à un domaine.

Pour plus d’informations et des exemples de procédure pas à pas, consultez le blog suivant : [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Stratégies d’accès conditionnel pour Azure Information Protection).

Informations complémentaires :

|Rubrique  |Détails  |
|---------|---------|
|**Fréquence d’évaluation**    | Pour les ordinateurs Windows et la version préliminaire actuelle, les stratégies d’accès conditionnel pour les Azure Information Protection sont évaluées lorsque l' [environnement utilisateur est initialisé](./how-does-it-work.md#initializing-the-user-environment) (ce processus est également appelé amorçage), puis tous les 30 jours.<br /><br />Pour ajuster la fréquence à laquelle vos stratégies d’accès conditionnel sont évaluées, [configurez la durée de vie du jeton](/azure/active-directory/active-directory-configurable-token-lifetimes).       |
|**Comptes d’administrateur**     |Nous vous recommandons de ne pas ajouter de comptes d’administrateur à vos stratégies d’accès conditionnel, car ces comptes ne seront pas en mesure d’accéder au volet de Azure Information Protection dans le Portail Azure.         |
|**MFA et B2B collaboration**     | Si vous utilisez MFA dans vos stratégies d’accès conditionnel pour collaborer avec d’autres organisations (B2B), vous devez utiliser [Azure AD B2B Collaboration](/azure/active-directory/b2b/what-is-b2b) et créer des comptes Invité pour les utilisateurs de l’autre organisation avec lesquels vous souhaitez partager.        |
|**Invites de conditions d’utilisation**     |  Avec la version préliminaire de Azure AD décembre 2018, vous pouvez désormais [inviter les utilisateurs à accepter les conditions d’utilisation](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822) avant d’ouvrir un document protégé pour la première fois.       |
|**Applications cloud**     |  Si vous utilisez un grand nombre d’applications cloud pour l’accès conditionnel, **Microsoft Azure Information Protection** risque de ne pas s’afficher dans la liste de sélection. <br /><br />Dans ce cas, utilisez la zone de recherche située en haut de la liste. Commencez à taper « Microsoft Azure Information Protection » pour filtrer les applications disponibles. À condition d’avoir un abonnement pris en charge, vous pourrez alors sélectionner **Microsoft Azure Information Protection**.        |
| | |

> [!NOTE]
> La prise en charge Azure Information Protection de l’accès conditionnel est actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 
> 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Je vois qu’Azure Information Protection est répertorié en tant que fournisseur de sécurité pour Microsoft Graph Security, comment cela fonctionne-t-il et quelles alertes vais-je recevoir ?

Oui, dans le cadre d’une offre de préversion publique, vous pouvez à présent recevoir une alerte pour **l’accès anormal aux données Azure Information Protection**. Cette alerte est déclenchée en cas de tentatives inhabituelles d’accès aux données qui sont protégées par Azure Information Protection. Par exemple, l’accès à un volume anormalement élevé de données, à un moment inhabituel de la journée, ou l’accès à partir d’un emplacement inconnu.

Ces alertes peuvent vous aider à détecter les attaques avancées liées aux données et les menaces internes dans votre environnement. Ces alertes utilisent le Machine Learning pour dresser le profil du comportement des utilisateurs qui accèdent à vos données protégées. 

Les alertes d’Azure Information Protection sont accessibles [à l’aide de l’API Microsoft Graph Security](/graph/api/resources/security-api-overview), ou vous pouvez [diffuser des alertes](/graph/security-integration) aux solutions SIEM, comme Splunk et IBM Qradar, à l’aide d’Azure Monitor.

Pour plus d’informations sur l’API Microsoft Graph Security, consultez [Vue d’ensemble de l’API Microsoft Graph Security](/graph/security-concept-overview).

> [!NOTE]
> La prise en charge Azure Information Protection pour la sécurité des Microsoft Graph est actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 
> 

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera bientôt disponible, par Azure Information Protection, quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. Pour ce type d’informations, utilisez la feuille de [route Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), consultez le [blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection peut-il être utilisé dans mon pays ?

Les pays ont chacun leurs réglementations et leurs exigences. Pour vous aider à répondre à cette question pour votre organisation, consultez [Adaptation aux différents pays](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>Comment Azure Information Protection peut-il aider pour le RGPD ?

[!INCLUDE [gdpr-hybrid-note](includes/gdpr-hybrid-note.md)]

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>Où puis-je trouver des informations annexes sur Azure Information Protection (considérations juridiques, conformité, contrats de niveau de service, etc.) ?
Consultez [Conformité et informations annexes pour Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Comment puis-je signaler un problème ou envoyer des commentaires pour Azure Information Protection ?

Pour le support technique, utilisez vos canaux de support standard ou [contactez le support technique Microsoft](information-support.md#to-contact-microsoft-support).

Nous vous invitons également à contacter l’équipe d’ingénieurs sur son [site Yammer Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Que dois-je faire si ma question n’est pas disponible ?

Tout d’abord, passez en revue les questions fréquemment posées répertoriées ci-dessous, qui sont spécifiques à la classification et à l’étiquetage, ou spécifiques à la protection des données. Le [service Azure Rights Management (Azure RMS)](what-is-azure-rms.md) fournit la technologie de protection des données pour Azure information protection. Azure RMS peut être utilisé avec la classification et l’étiquetage, ou de façon autonome. 

- [FAQ sur la classification et l’étiquetage](faqs-infoprotect.md)

- [FAQ sur la protection des données](faqs-rms.md)

- [FAQ pour le client classique uniquement](faqs-classic.md)

Si votre question n’a pas de réponse, consultez les liens et les ressources figurant dans [informations et support pour Azure information protection](information-support.md).
