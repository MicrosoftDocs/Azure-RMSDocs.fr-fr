---
title: FAQ relatives à Azure Information Protection
description: Some frequently asked questions about Azure Information Protection and its protection service, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: f4583260708267575f35d4c67d6cd2afc5add68d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474340"
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

Announced at Microsoft Ignite 2018 in Orlando, you now have an option to create and configure [sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) in addition to retention labels in one of the admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, or the Microsoft 365 compliance center. You can migrate your existing Azure Information Protection labels to the new unified labeling store, to be used as sensitivity labels with Office apps. 

Pour plus d’informations sur la gestion de l’étiquetage unifié et la prise en charge de ces étiquettes, lisez le billet de blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967).

For more information about migrating your existing labels, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>How can I determine if my tenant is on the unified labeling platform?

When your tenant is on the unified labeling platform, sensitivity labels can be used by [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). If you obtained your subscription for Azure Information Protection in June 2019 or later, your tenant is automatically on the unified labeling platform and no further action is needed. Your tenant might also be on this platform because somebody migrated your Azure Information Protection labels.

To check the status, in the Azure portal, go to **Azure Information Protection** > **Manage** > **Unified labeling**, and view the status of **Unified labeling**:

- If you see **Activated**, your tenant is on the unified labeling platform.

- If you see **Not activated**, your tenant is not on the unified labeling platform. For migration instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>What's the difference between the Azure Information Protection client and the Azure Information Protection unified labeling client?

The **Azure Information Protection client (classic)** has been available since Azure Information Protection was first announced as a new service for classifying and protecting files and emails. This client downloads labels and policy settings from Azure, and you configure the Azure Information Protection policy from the Azure portal. For more information, see [Overview of the Azure Information Protection policy](overview-policy.md). 

The **Azure Information Protection unified labeling client** is a more recent addition, to support the unified labeling store that multiple applications and services support. This client downloads sensitivity labels and policy settings from the following admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, and the Microsoft 365 compliance center. For more information, see [Overview of sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

If you're not sure which client to use, see [Choose which Azure Information Protection client to use](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

### <a name="identify-which-client-you-have-installed"></a>Identify which client you have installed

Both clients, when they are installed, display **Azure Information Protection**. To help you identify which client you have installed, use the **Help and feedback** option to open the **Microsoft Azure Information Protection** dialog box:

- Dans l’Explorateur de fichiers : cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**.

- From an Office application: From the **Protect** button (the classic client) or **Sensitivity** button (unified labeling client), select **Help and Feedback**.

Use the **Version** number displayed to identify the client:

- A version **1**, for example, **1.53.10.0**, identifies the Azure Information Protection client (classic).

- A version **2**, for example, **2.2.14.0**, identifies the Azure Information Protection unified labeling client.

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>When is the right time to migrate my labels?

Now that the option to migrate labels in the Azure portal is in general availability, we recommend you activate the migration so that you can use your labels as sensitivity labels with [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

For more information and instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?

Une fois que vous avez migré vos étiquettes dans le portail Azure :

- If you have [unified labeling clients and services](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), go to one of the admin centers (Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center) to publish these labels, and to configure their policy settings. À l’avenir, utilisez l’un de ces centres d’administration pour toute modification d’étiquette. Les clients d’étiquetage unifié téléchargent les étiquettes et les paramètres de stratégie à partir de ces centres d’administration.

- If you have the [Azure Information Protection client (classic)](./rms-client/aip-client.md), continue to use the Azure portal to edit your labels and policy settings. The classic client continues to download labels and policy settings from Azure.

- If you have both [unified labeling clients](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) and [classic clients](./rms-client/aip-client.md), you can use the admin centers or the Azure portal to make label changes. However, for the classic clients to pick up the label changes that you make in the admin centers, you must return to the Azure portal: Use the **Publish** option from the **Azure Information Protection - Unified labeling** pane in the Azure portal. 

Continuez à utiliser le portail Azure pour la [centralisation des rapports](reports-aip.md) et le [scanneur](deploy-aip-scanner.md).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quelle est la différence entre Information Protection et Azure Rights Management ?

Azure Information Protection permet à une organisation de classifier, d’étiqueter et de protéger ses documents et e-mails. La technologie de protection utilise le service Azure Rights Management, désormais un composant d’Azure Information Protection.

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>What's the role of identity management for Azure Information Protection?

Un utilisateur doit avoir un nom d’utilisateur et un mot de passe valides pour accéder au contenu protégé par Azure Information Protection. Pour en savoir plus sur la façon dont Azure Information Protection permet de sécuriser vos données, consultez [Rôle d’Azure Information Protection dans la sécurisation des données](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?

Consultez les informations sur les abonnements et la liste des fonctionnalités de la page [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Si vous avez un abonnement Office 365 qui comprend la protection des données Azure Rights Management, téléchargez la [fiche sur les licences Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Vous avez d’autres questions sur les licences ? Regardez si vous trouvez des réponses dans la section [Forum aux questions](https://azure.microsoft.com/pricing/details/information-protection#faq) sur les licences.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Le client Azure Information Protection est-il réservé aux abonnements qui comprennent la classification et l’étiquetage ?

Non. The Azure Information Protection client (classic) can also be used with subscriptions that include just the Azure Rights Management service to protect data.

When the classic client is installed and it doesn't have an Azure Information Protection policy, this client automatically operates in [protection-only mode](./rms-client/client-protection-only-mode.md). Dans ce mode, les utilisateurs peuvent facilement appliquer des modèles Rights Management et des autorisations personnalisées. Si vous décidez, plus tard, de souscrire un abonnement qui n’inclut ni la classification ni l’étiquetage, le client passe automatiquement en mode standard lors du téléchargement de la stratégie Azure Information Protection.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?

Les administrateurs généraux d’un locataire Office 365 ou Azure AD peuvent évidemment exécuter toutes les tâches d’administration d’Azure Information Protection. Toutefois, si vous voulez affecter des autorisations d’administration à d’autres utilisateurs, vous avez les options suivantes :

- **Azure Information Protection administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection but not other services. Un administrateur qui a ce rôle peut activer et désactiver le service de protection Azure Rights Management, configurer les paramètres de protection et les étiquettes, et configurer la stratégie Azure Information Protection. In addition, an administrator with this role can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, this role doesn't support tracking and revoking documents for users.
    
    > [!NOTE]
    > This role is not supported in the Azure portal if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Compliance administrator** or **Compliance data administrator**: These Azure Active Directory administrator roles let an administrator configure Azure Information Protection, which includes activate and deactivate the Azure Rights Management protection service, configure protection settings and labels, and configure the Azure Information Protection policy. In addition, an administrator with either of these roles can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, these roles don't support tracking and revoking documents for users.
    
    To assign a user to one of these administrative roles, see [Assign a user to administrator roles in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). To see what other permissions a user with these roles have, see the [Available roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) section from the Azure Active Directory documentation.

- **Security reader** or **Global reader**: For [Azure Information Protection analytics](reports-aip.md) only. Ce rôle d’administrateur Azure Active Directory permet à un administrateur de visualiser comment vos étiquettes sont utilisées, de surveiller l’accès utilisateur aux documents et e-mails étiquetés, ainsi que les modifications apportées à leur classification, et peut identifier les documents qui contiennent des informations sensibles devant être protégés. Because this feature uses Azure Monitor, you must also have a supporting [RBAC role](reports-aip.md#permissions-required-for-azure-information-protection-analytics).
    
    > [!NOTE]
    > The Security reader and Global reader roles are not supported if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

- **Security administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection in the Azure portal, in addition to configuring some aspects of other Azure services. An administrator with this role cannot run any of the [PowerShell cmdlets from the AIPService module](administer-powershell.md), or track and revoke documents for users.
    
    Pour affecter un utilisateur à ce rôle d’administration, consultez [Affecter un utilisateur à des rôles d’administration dans Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Pour connaître les autres autorisations qu’un rôle donne à un utilisateur, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

- Azure Rights Management **Global Administrator** and **Connector Administrator**: For these Azure Rights Management administrator roles, the first grants users permissions to run all [PowerShell cmdlets from the AIPService module](administer-powershell.md) without making them a global administrator for other cloud services, and the second role grants permissions to run only the Rights Management (RMS) connector. Neither of these administrative roles grant permissions to management consoles or tracking and revoking documents for users.
    
    To assign either of these administrative roles, use the AIPService PowerShell cmdlet, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

Quelques éléments à prendre en compte :

- Microsoft accounts are not supported for delegated administration of Azure Information Protection, even if these accounts are assigned to one of the administrative roles listed. 

- Si vous avez configuré des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), cette configuration n’affecte pas la possibilité d’administrer Azure Information Protection, à l’exception du connecteur RMS. Par exemple, si vous avez configuré des contrôles d’intégration de manière à ce que seul le groupe « Département informatique » puisse protéger du contenu, le compte que vous utilisez pour installer et configurer le connecteur RMS doit être membre de ce groupe. 

- Les utilisateurs avec un rôle d’administration ne peuvent pas supprimer automatiquement la protection des documents ou des e-mails qui ont été protégés par Azure Information Protection. Seuls les super utilisateurs peuvent le faire, sous réserve que la fonctionnalité de super utilisateur soit activée. Toutefois, tout utilisateur avec des autorisations d’administrateur sur Azure Information Protection peut affecter un rôle de super utilisateur, y compris à lui-même. Ils peuvent également activer la fonctionnalité de super utilisateur. Ces actions sont enregistrées dans un journal d’administrateur. For more information, see the security best practices section in [Configuring super users for Azure Information Protection and discovery services or data recovery](configure-super-users.md). 

- If you are migrating your Azure Information Protection labels to the unified labeling store, be sure to read the following section from the label migration documentation: [Administrative roles that support the unified labeling platform](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>La solution Azure Information Protection prend-elle en charge les scénarios sur site et hybrides ?

Oui. Bien qu’Azure Information Protection soit une solution basée sur le cloud, elle peut classer, étiqueter et protéger des documents et des e-mails stockés sur site, ainsi que dans le cloud.

Si vous possédez Exchange Server, SharePoint Server et des serveurs de fichiers Windows, vous pouvez déployer le [connecteur Rights Management](deploy-rms-connector.md) afin de permettre à ces serveurs locaux d’utiliser le service Azure Rights Management pour protéger vos e-mails et documents. Vous pouvez également synchroniser et fédérer vos contrôleurs de domaine Active Directory avec Azure AD afin d’offrir une expérience d'authentification simple aux utilisateurs, par exemple, en utilisant [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Le service Azure Rights Management génère et gère automatiquement les certificats XrML en fonction des besoins. Il n’utilise donc pas d’infrastructure à clé publique (PKI) locale. Pour plus d’informations sur la façon dont Azure Rights Management utilise les certificats, voir la section [Présentation du fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de l’article [Fonctionnement d’Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quels sont les types de données qu’Azure Information Protection peut classifier et protéger ?

Azure Information Protection peut classifier et protéger des e-mails et des documents, localement ou dans le cloud. Ces documents sont notamment des documents Word, des feuilles de calcul Excel, des présentations PowerPoint, des documents PDF, des fichiers texte et des fichiers image. Pour connaître les types de document pris en charge, consultez la liste des [types de fichier pris en charge](./rms-client/clientv2-admin-guide-file-types.md) dans le guide d’administration.

Azure Information Protection cannot classify and protect structured data such as database files, calendar items, Yammer posts, Sway content, and OneNote notebooks.

**Newly announced in preview**: Power BI now supports classification by using sensitivity labels and can apply protection from those labels to data that is exported to the following file formats: .pdf, .xls, and .ppt. For more information, see [Data protection in Power BI (preview)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview).

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Je vois qu’Azure Information Protection est répertoriée en tant qu’application cloud disponible pour l’accès conditionnel : comment cela fonctionne-t-il ?

Oui, dans le cadre d’une offre de préversion, vous pouvez à présent configurer l’accès conditionnel Azure AD pour Azure Information Protection.

Lorsqu’un utilisateur ouvre un document protégé par Azure Information Protection, les administrateurs peuvent à présent lui bloquer ou lui accorder l’accès, selon les contrôles d’accès conditionnel standard. L’authentification multifacteur (MFA) est l’une des conditions les plus couramment demandées. Une autre condition veut que les appareils soient [conformes à vos stratégies Intune](/intune/conditional-access-intune-common-ways-use) afin que, par exemple, les appareils mobiles puissent répondre à vos critères de mot de passe et de version minimale du système d’exploitation, et que les ordinateurs soient joints à un domaine.

Pour plus d’informations et des exemples de procédure pas à pas, consultez le blog suivant : [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Stratégies d’accès conditionnel pour Azure Information Protection).

Informations complémentaires :

- Pour les ordinateurs Windows : pour la préversion actuelle, les stratégies d’accès conditionnel pour Azure Information Protection sont évaluées quand l’[environnement de l’utilisateur est initialisé](./how-does-it-work.md#initializing-the-user-environment) (ce processus est également appelé amorçage), puis tous les 30 jours.

- Vous devrez peut-être ajuster la fréquence à laquelle vos stratégies d’accès conditionnel sont évaluées. Pour cela, configurez la durée de vie des jetons. Pour plus d’informations, consultez [Durées de vie de jeton configurables dans Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- We recommend that you do not add administrator accounts to your conditional access policies because these accounts will not be able to access the Azure Information Protection pane in the Azure portal.

- Si vous utilisez MFA dans vos stratégies d’accès conditionnel pour collaborer avec d’autres organisations (B2B), vous devez utiliser [Azure AD B2B Collaboration](/azure/active-directory/b2b/what-is-b2b) et créer des comptes Invité pour les utilisateurs de l’autre organisation avec lesquels vous souhaitez partager.

- Avec la préversion d’Azure AD publiée en décembre 2018, vous pouvez inviter les utilisateurs à accepter des conditions d’utilisation avant la première ouverture d’un document protégé. For more information, see the following blog post announcement: [Updates to Azure AD Terms of Use functionality within conditional access](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

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

There is a difference in setting the [Rights Management owner](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) for files that are protected on a local folder or network share. Par défaut, dans les deux solutions, le propriétaire de Rights Management est défini sur le compte qui protège le fichier, mais vous pouvez remplacer ce paramètre :

- Pour l’ICF de Windows Server, vous pouvez définir le propriétaire de Rights Management sur un seul compte pour tous les fichiers, ou définir de façon dynamique ce propriétaire pour chaque fichier. Pour définir le propriétaire de Rights Management de façon dynamique, utilisez le paramètre et la valeur **- OwnerMail [Source File Owner Email]** . Cette configuration récupère l’adresse e-mail de l’utilisateur à partir d’Active Directory en utilisant le nom du compte d’utilisateur dans la propriété Propriétaire du fichier.

- For the Azure Information Protection scanner: For newly protected files, you can set the Rights Management owner to be a single account for all files on a specified data store, but you cannot dynamically set the Rights Management owner for each file. Le propriétaire de Rights Management ne change pas pour les fichiers précédemment protégés. Pour définir le compte des nouveaux fichiers protégés, spécifiez le paramètre **Propriétaire par défaut** dans le profil du scanneur. 

Quand le scanneur protège les fichiers sur les sites et bibliothèques SharePoint, le propriétaire de Rights Management est défini dynamiquement pour chaque fichier à l’aide de la valeur de l’éditeur de SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>J’ai entendu dire qu’une nouvelle version sera disponible prochainement pour Azure Information Protection : quand sera-t-elle publiée ?

La documentation technique ne contient pas d’informations sur les versions à venir. For this type of information, use the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), check the [Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

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

