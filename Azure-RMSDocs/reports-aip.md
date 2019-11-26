---
title: Création de rapports centralisée pour Azure Information Protection
description: Guide pratique pour utiliser la création de rapports centralisée pour suivre l’adoption de vos étiquettes Azure Information Protection et identifier les fichiers qui contiennent des informations sensibles
author: cabailey
ms.author: cabailey
ms.date: 11/25/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7c310122ac72bc7312fe0bd8d41bd3dc80715d76
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474289"
---
# <a name="central-reporting-for-azure-information-protection"></a>Création de rapports centralisée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée.

Use Azure Information Protection analytics for central reporting to help you track the adoption of your labels that classify and protect your organization's data. De plus :

- Surveillez les documents et les e-mails étiquetés et protégés dans votre organisation

- Identifiez les documents qui contiennent des informations sensibles dans votre organisation

- Surveiller l’accès utilisateur aux documents et e-mails étiquetés, et faire le suivi des modifications apportées à la classification des documents.

- Identifiez les documents qui contiennent des informations sensibles susceptibles de mettre votre organisation en péril si elles ne sont pas protégées, et limitez les risques en suivant les recommandations.

- Identify when protected documents are accessed by internal or external users from Windows computers, and whether access was granted or denied.

The data that you see is aggregated from your Azure Information Protection clients and scanners, from Microsoft Cloud App Security, from Windows 10 computers using Microsoft Defender Advanced Threat Protection, and from [protection usage logs](log-analyze-usage.md).

Par exemple, vous serez en mesure de voir ce qui suit :

- À partir du **rapport d’utilisation**, où vous pouvez sélectionner une période de temps :
    
    - Étiquettes qui sont appliquées
    
    - Nombre de documents et d’e-mails étiquetés
    
    - Nombre de documents et d’e-mails protégés
    
    - Nombre d’utilisateurs et nombre d’appareils qui étiquettent des documents et e-mails
    
    - Applications utilisées pour l’étiquetage

- Dans **Journaux d’activité**, en sélectionnant une période :
    
    - Quelles actions d’étiquetage ont été effectuées par un utilisateur donné
    
    - Quelles actions d’étiquetage ont été effectuées sur un appareil donné
    
    - Quels utilisateurs ont accédé à un document étiqueté donné
    
    - Quelles actions d’étiquetage ont été effectuées pour un chemin d’accès donné
    
    - What labeling actions were performed by a specific application, such File Explorer and right-click, PowerShell, the scanner, or Microsoft Cloud App Security
    
    - Which protected documents were accessed successfully by users or denied access to users, even if those users don't have the Azure Information Protection client installed or are outside your organization

    - Explorez les fichiers signalés pour afficher les **détails de l’activité** afin d’obtenir plus d’informations

- À partir du rapport de **découverte de données** :

    - What files are on your scanned data repositories, Windows 10 computers, or computers running the Azure Information Protection clients
    
    - Fichiers étiquetés et protégés, et emplacement des fichiers en fonction des étiquettes
    
    - Fichiers qui contiennent des informations sensibles pour des catégories connues, telles que les données financières et les informations personnelles, et emplacement des fichiers en fonction de ces catégories

- À partir du rapport **Recommandations** :
    
    - Identifiez les fichiers non protégés qui contiennent un type connu d’informations sensibles. Une recommandation vous permet de configurer immédiatement la condition correspondante pour une de vos étiquettes à appliquer automatique ou pour l’étiquetage recommandé.
        
        If you follow the recommendation: The next time the files are opened by a user or scanned by the Azure Information Protection scanner, the files can be automatically classified and protected.
    
    - Référentiels de données ayant des fichiers avec des informations confidentielles identifiées, mais qui ne sont pas analysés par Azure Information Protection. Une recommandation vous permet d’ajouter immédiatement le magasin de données identifié à un des profils du scanneur.
        
        If you follow the recommendation: On the next scanner cycle, the files can be automatically classified and protected.

Les rapports utilisent [Azure Monitor](/azure/log-analytics/log-analytics-overview) pour stocker les données dans un espace de travail Log Analytics appartenant à votre organisation. Si vous êtes familiarisé avec le langage de requête, vous pouvez modifier les requêtes ainsi que créer des rapports et tableaux de bord Power BI. You might find the following tutorial helpful to understand the query language: [Get started with Azure Monitor log queries](/azure/azure-monitor/log-query/get-started-queries).

Pour plus d’informations, lisez le billet de blog suivant : 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [Discover and protect sensitive data through Azure Information Protection and Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informations collectées et envoyées à Microsoft

Pour générer ces rapports, les points de terminaison envoient les types suivants d’informations à Microsoft :

- Action d’étiquette. Par exemple, définir une étiquette, modifier une étiquette, ajouter ou supprimer la protection, étiquettes automatiques et recommandées.

- Nom de l’étiquette avant et après l’action d’étiquette.

- ID de locataire de votre organisation.

- ID d’utilisateur (adresse e-mail ou UPN).

- Nom de l’appareil de l’utilisateur.

- Pour les documents : chemin et nom de fichier des documents qui sont étiquetés.

- For emails: The email subject and email sender  for emails that are labeled. 

- Types d’informations sensibles ([prédéfinis](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) et personnalisés) détectés dans le contenu.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics appartenant à votre organisation et consultable indépendamment d’Azure Information Protection par les utilisateurs qui disposent des droits d’accès correspondants. Pour plus d’informations, voir la section [Autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Pour plus d’informations sur la gestion de l’accès à votre espace de travail, consultez la section [Gérer l’accès à l’espace de travail Log Analytics avec des autorisations Azure](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) de la documentation Azure.

To prevent Azure Information Protection clients (classic) from sending this data, set the [policy setting](configure-policy-settings.md) of **Send audit data to Azure Information Protection analytics** to **Off**:

- Pour que la plupart des utilisateurs envoient ces données d’audit et qu’un sous-ensemble ne puisse pas en envoyer : 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in a scoped policy for the subset of users. Cette configuration est généralement utilisée dans les scénarios de production.

- Pour que seul un sous-ensemble d’utilisateurs envoie des données d’audit : 
    - Set **Send audit data to Azure Information Protection analytics** to **Off** in the global policy, and **On** in a scoped policy for the subset of users. Cette configuration est généralement utilisée dans les scénarios de test.

To prevent Azure Information Protection unified clients from sending this data, configure a label policy [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics).

#### <a name="content-matches-for-deeper-analysis"></a>Correspondances de contenu pour approfondir l’analyse

Azure Information Protection lets you collect and store the actual data that's identified as being a sensitive information type (predefined or custom). Il peut s’agir, par exemple, de numéros de carte de crédit trouvés, mais aussi de numéros de sécurité sociale, de passeport et de compte bancaire. The content matches are displayed when you select an entry from **Activity logs**, and view the **Activity Details**. 

By default, Azure Information Protection clients don't send content matches. To change this behavior so that content matches are sent:

- For the classic client, select a checkbox as part of the [configuration](#configure-a-log-analytics-workspace-for-the-reports) for Azure Information Protection analytics. The checkbox is named **Enable deeper analytics into your sensitive data**.
    
    If you want most users who are using this client to send content matches but a subset of users cannot send content matches, select the checkbox and then configure an [advanced client setting](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) in a scoped policy for the subset of users.

- For the unified labeling client, configure an [advanced setting](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) in a label policy.

## <a name="prerequisites"></a>Conditions préalables
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Autres informations|
|---------------|--------------------|
|Un abonnement Azure qui inclut Log Analytics et qui concerne le même locataire qu’Azure Information Protection|Consultez la page de [tarification d’Azure Monitor](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.|
|For reporting information from labeling clients: <br /><br />- Azure Information Protection clients|Both the unified labeling client and the classic client are supported. <br /><br />If not already installed, you can download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|For reporting information from cloud-based data stores: <br /><br />- Microsoft Cloud App Security |To display information from Microsoft Cloud App Security, configure [Azure Information Protection integration](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|For reporting information from on-premises data stores: <br /><br />- Azure Information Protection scanner |Pour obtenir des instructions d’installation pour le scanneur, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md). |
|For reporting information from Windows 10 computers:  <br /><br />- Minimum build of 1809 with Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP)|You must enable the Azure Information Protection integration feature from Microsoft Defender Security Center. For more information, see [Information protection in Windows overview](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorisations requises pour l’analytique Azure Information Protection

Caractéristique propre à l’analytique Azure Information Protection, après que vous avez configuré votre espace de travail Azure Log Analytics, vous pouvez utiliser le rôle Administrateur d’Azure AD de Lecteur Sécurité comme alternative aux autres rôles Azure AD qui prennent en charge la gestion d’Azure Information Protection dans le portail Azure. This additional role is supported only if your tenant isn't on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

Because Azure Information Protection analytics uses Azure Monitoring, role-based access control (RBAC) for Azure also controls access to your workspace. Vous avez donc besoin d’un rôle Azure ainsi que d’un rôle Administrateur d’Azure AD pour gérer l’analytique Azure Information Protection. Si vous ne connaissez pas les rôles Azure, il peut s’avérer utile de lire [Différences entre les rôles RBAC Azure et les rôles d’administrateur Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Détails :

1. One of the following [Azure AD administrator roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) to access the Azure Information Protection analytics pane:
    
    - Pour créer votre espace de travail Log Analytics ou des requêtes personnalisées :
    
        - **Azure Information Protection administrator**
        - **Administrateur de sécurité**
        - **Administrateur de conformité**
        - **Compliance data administrator**
        - **Administrateur général**
    
    - After the workspace has been created, you can then use the following roles with fewer permissions to view the data collected:
    
        - **Lecteur Sécurité**
        - **Global reader**
    
    > [!NOTE] 
    > You cannot use the Azure Information Protection administrator role, the Security reader role, or the Global reader role if your tenant is on the [unified labeling platform](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

2. Par ailleurs, vous devez disposer de l’un des [rôles Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) ou [rôles Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) standard pour accéder à votre espace de travail Azure Log Analytics :
    
    - Pour créer l’espace de travail Log Analytics ou des requêtes personnalisées :
    
        - **Contributeur Log Analytics**
        - **Contributeur**
        - **Propriétaire**
    
    - Une fois l’espace de travail créé, vous pouvez utiliser l’un des rôles suivants avec moins d’autorisations pour afficher les données collectées :
    
        - **Lecteur Log Analytics**
        - **Lecteur**

#### <a name="minimum-roles-to-view-the-reports"></a>Rôles minimaux permettant d’afficher les rapports

Une fois l’espace de travail configuré pour l’analytique Azure Information Protection, les deux rôles nécessaires au minimum pour afficher les rapports d’analytique Azure Information Protection sont les suivants :

- Azure AD administrator role: **Security reader**
- Azure role: **Log Analytics Reader**

Toutefois, de nombreuses organisations attribuent le rôle Azure AD **Lecteur Sécurité** et le rôle Azure **Lecteur**.

### <a name="storage-requirements-and-data-retention"></a>Storage requirements and data retention

The amount of data collected and stored in your Azure Information Protection workspace will vary significantly for each tenant, depending on factors such as how many Azure Information Protection clients and other supported endpoints you have, whether you're collecting endpoint discovery data, you've deployed scanners, the number of protected documents that are accessed, and so on.

However, as a starting point, you might find the following estimates useful:

- For audit data generated by Azure Information Protection clients only: 2 GB per 10,000 active users per month.

- For audit data generated by Azure Information Protection clients, scanners, and Microsoft Defender ATP: 20 GB per 10,000 active users per month.

If you use mandatory labeling or you've configured a default label for most users, your rates are likely to be significantly higher.

Azure Monitor Logs has a **Usage and estimated costs** feature to help you estimate and review the amount of data stored, and you can also control the data retention period for your Log Analytics workspace. For more information, see [Manage usage and costs with Azure Monitor Logs](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](https://portal.azure.com) avec un compte qui possède les [autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Accédez ensuite au volet **Azure Information Protection**. 
    
    For example, in the search box for resources, services, and docs: Start typing **Information** and select **Azure Information Protection**.
    
2. Recherchez les options du menu **Gérer**, puis sélectionnez **Configurer l’analytique (préversion)** .

3. On the **Azure Information Protection log analytics** pane, you see a list of any Log Analytics workspaces that are owned by your tenant. Procédez de l'une des façons suivantes :
    
    - To create a new Log Analytics workspace: Select **Create new workspace**, and on the **Log analytics workspace** pane, supply the requested information.
    
    - Pour utiliser un espace de travail Log Analytics existant : sélectionnez l’espace de travail dans la liste.
    
    Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

4. If you have Azure Information Protection clients (classic), select the checkbox **Enable deeper analytics into your sensitive data** if you want to store the actual data that's identified as being a sensitive information type. For more information about this setting, see the [Content matches for deeper analysis](#content-matches-for-deeper-analysis) section on this page.

5. Sélectionnez **OK**.

You're now ready to view the reports.

## <a name="how-to-view-the-reports"></a>Comment afficher les rapports

From the Azure Information Protection pane, locate the **Dashboards** menu options, and select one of the following options:

- **Rapport d’utilisation (préversion)**  : utilisez ce rapport pour voir comment vos étiquettes sont utilisées.

- **Journaux d’activité (préversion)** : utilisez ce rapport pour voir les actions d’étiquetage effectuées par les utilisateurs sur les appareils et les chemins d'accès. In addition, for protected documents, you can see access attempts (successful or denied) for users both inside and outside your organization, even if they don't have the Azure Information Protection client installed
    
    Ce rapport comporte une option **Colonnes** qui permet d’afficher plus d’informations sur l’activité que l’affichage par défaut. Vous pouvez également voir plus de détails sur un fichier en le sélectionnant pour afficher les **détails de l’activité**.

- **Data discovery (Preview)** : Use this report to see information about labeled files found by scanners and supported endpoints.
    
    Tip: From the information collected, you might find users accessing files that contain sensitive information from location that you didn't know about or aren't currently scanning:
    
    - Si les emplacements sont locaux, vous pouvez envisager de les ajouter en tant que référentiels de données supplémentaires pour le scanneur Azure Information Protection.
    - Si les emplacements sont dans le cloud, envisagez d’utiliser Microsoft Cloud App Security pour les gérer. 
    
- **Recommendations (Preview)** : Use this report to identify files that have sensitive information and mitigate your risk by following the recommendations.
    
    Quand vous sélectionnez un élément, l’option **Afficher les données** affiche les activités d’audit qui ont déclenché la recommandation.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Comment modifier les rapports et créer des requêtes personnalisées

Select the query icon in the dashboard to open a **Log Search** pane: 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


Les données enregistrées pour Azure Information Protection sont stockées dans le tableau suivant : **InformationProtectionLogs_CL**

Lorsque vous créez vos propres requêtes, utilisez les noms de schéma conviviaux qui ont été implémentés en tant que fonctions **InformationProtectionEvents**. Ces fonctions sont dérivées des attributs qui sont pris en charge pour les requêtes personnalisées (certains attributs sont à usage interne uniquement) et leurs noms ne changeront pas au fil du temps, même si les attributs sous-jacents changent à des fins d’amélioration et de nouvelle fonctionnalité.

### <a name="friendly-schema-reference-for-event-functions"></a>Référence de schéma conviviale pour les fonctions d’événement

Utilisez le tableau suivant pour identifier le nom convivial des fonctions d’événement que vous pouvez utiliser pour les requêtes personnalisées avec l’analytique Azure Information Protection.

|Nom de la colonne|Description|
|-----------|-----------|
|Heure|Event time: UTC in format YYYY-MM-DDTHH:MM:SS|
|Utilisateur|User: Format UPN or DOMAIN\USER|
|ItemPath|Full item path or email subject|
|ItemName|File name or email subject |
|Méthode|Label assigned method: Manual, Automatic, Recommended, Default, or Mandatory|
|Activité|Audit activity: DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, or NewCustomProtection |
|LabelName|Label name (not localized)|
|LabelNameBefore |Label name before change (not localized) |
|ProtectionType|Protection type [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Protection type before change [JSON] |
|MachineName |FQDN when available; otherwise host name|
|DeviceRisk|Device risk score from WDATP when available|
|Plate-forme|Device platform (Win, OSX, Android, iOS) |
|ApplicationName|Application friendly name|
|AIPVersion|Version of the Azure Information Protection client that performed the audit action |
|TenantId|ID de locataire Azure AD |
|AzureApplicationId|Azure AD registered application ID (GUID)|
|ProcessName|Process that hosts MIP SDK|
|LabelId|Label GUID or null|
|IsProtected|Whether protected: Yes/No |
|ProtectionOwner |Rights Management owner in UPN format|
|LabelIdBefore|Label GUID or null before change|
|InformationTypesAbove55|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 55 or above |
|InformationTypesAbove65|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 65 or above |
|InformationTypesAbove75|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 75 or above |
|InformationTypesAbove85|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 85 or above |
|InformationTypesAbove95|JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data with confidence level 95 or above|
|DiscoveredInformationTypes |JSON array of [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) found in data and their matched content (if enabled) where an empty array means no information types found, and null means no information available |
|ProtectedBefore|Whether the content was protected before change: Yes/No |
|ProtectionOwnerBefore|Rights Management owner before change |
|UserJustification|Justification when downgrading or removing label|
|LastModifiedBy|User in UPN format who last modified the file. Available for Office and SharePoint Online only|
|LastModifiedDate|UTC in format YYYY-MM-DDTHH:MM:SS: Available for Office & SharePoint Online only |


#### <a name="examples-using-informationprotectionevents"></a>Exemples d’utilisation d’InformationProtectionEvents

Utilisez les exemples suivants pour voir comment vous pouvez utiliser le schéma convivial pour créer des requêtes personnalisées.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Example 1: Return all users who sent audit data in the last 31 days 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Example 2: Return the number of labels that were downgraded per day in the last 31 days 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Example 3: Return the number of labels that were downgraded from Confidential by user, in the last 31 days 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

Dans cet exemple, une étiquette rétrogradée est comptabilisée uniquement si le nom de l’étiquette avant l’action contenait le nom **Confidentiel** et le nom de l’étiquette après l’action ne contenait pas le nom **Confidentiel**. 


## <a name="next-steps"></a>Étapes suivantes
After reviewing the information in the reports, if you are using the Azure Information Protection client, you might decide to make changes to your Azure Information Protection policy. Pour obtenir des instructions, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Si vous avez un abonnement Microsoft 365, vous pouvez également consulter l’utilisation des étiquettes dans le Centre de conformité Microsoft 365 et le Centre de sécurité Microsoft 365. Pour plus d’informations, voir [Afficher l’utilisation des étiquettes avec l’Analyse des étiquettes](/microsoft-365/compliance/label-analytics).
