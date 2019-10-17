---
title: Création de rapports centralisée pour Azure Information Protection
description: Guide pratique pour utiliser la création de rapports centralisée pour suivre l’adoption de vos étiquettes Azure Information Protection et identifier les fichiers qui contiennent des informations sensibles
author: cabailey
ms.author: cabailey
ms.date: 10/14/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8b7884de10999518d0c6cf9806b546181277a113
ms.sourcegitcommit: 07ae7007c79c998bbf3b8cf37808daf0eec68ad1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72447838"
---
# <a name="central-reporting-for-azure-information-protection"></a>Création de rapports centralisée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée.

Utilisez Azure Information Protection Analytics pour la création de rapports centralisés pour vous aider à suivre l’adoption de vos étiquettes qui classent et protègent les données de votre organisation. De plus :

- Surveillez les documents et les e-mails étiquetés et protégés dans votre organisation

- Identifiez les documents qui contiennent des informations sensibles dans votre organisation

- Surveiller l’accès utilisateur aux documents et e-mails étiquetés, et faire le suivi des modifications apportées à la classification des documents.

- Identifiez les documents qui contiennent des informations sensibles susceptibles de mettre votre organisation en péril si elles ne sont pas protégées, et limitez les risques en suivant les recommandations.

- Identifiez le moment où les utilisateurs internes ou externes accèdent à des documents protégés à partir d’ordinateurs Windows, et si l’accès a été accordé ou refusé.

Les données que vous voyez sont agrégées à partir de vos clients et scanneurs Azure Information Protection, à partir des [clients et des services qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)et depuis les [journaux d’utilisation](log-analyze-usage.md)de la protection.

> [!NOTE]
> Actuellement, à l’exception de la préversion du client d’étiquetage unifié, Azure Information Protection Analytics n’inclut pas les types d’informations personnalisées pour les clients et les services qui prennent en charge l’étiquetage unifié.

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
    
    - Les actions d’étiquetage effectuées par une application spécifique, telles que l’Explorateur de fichiers et le clic droit, PowerShell, le scanneur ou Microsoft Cloud App Security
    
    - Les documents protégés auxquels les utilisateurs ont accédé avec succès ou qui ont refusé l’accès aux utilisateurs, même s’ils n’ont pas le client Azure Information Protection installé ou se trouvent en dehors de votre organisation

    - Explorez les fichiers signalés pour afficher les **détails de l’activité** afin d’obtenir plus d’informations

- À partir du rapport de **découverte de données** :

    - Quels sont les fichiers présents dans les référentiels de données analysés, les ordinateurs Windows 10 ou les ordinateurs qui exécutent le client Azure Information Protection ou les [clients qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - Fichiers étiquetés et protégés, et emplacement des fichiers en fonction des étiquettes
    
    - Fichiers qui contiennent des informations sensibles pour des catégories connues, telles que les données financières et les informations personnelles, et emplacement des fichiers en fonction de ces catégories

- À partir du rapport **Recommandations** :
    
    - Identifiez les fichiers non protégés qui contiennent un type connu d’informations sensibles. Une recommandation vous permet de configurer immédiatement la condition correspondante pour une de vos étiquettes à appliquer automatique ou pour l’étiquetage recommandé.
        
        Si vous suivez la recommandation : la prochaine fois que les fichiers sont ouverts par un utilisateur ou analysés par le scanneur Azure Information Protection, les fichiers peuvent être automatiquement classés et protégés.
    
    - Référentiels de données ayant des fichiers avec des informations confidentielles identifiées, mais qui ne sont pas analysés par Azure Information Protection. Une recommandation vous permet d’ajouter immédiatement le magasin de données identifié à un des profils du scanneur.
        
        Si vous suivez la recommandation : lors du prochain cycle du scanneur, les fichiers peuvent être automatiquement classés et protégés.

Les rapports utilisent [Azure Monitor](/azure/log-analytics/log-analytics-overview) pour stocker les données dans un espace de travail Log Analytics appartenant à votre organisation. Si vous êtes familiarisé avec le langage de requête, vous pouvez modifier les requêtes ainsi que créer des rapports et tableaux de bord Power BI. Vous trouverez peut-être le didacticiel suivant utile pour comprendre le langage de requête : [prise en main des requêtes de journal Azure Monitor](/azure/azure-monitor/log-query/get-started-queries).

Pour plus d’informations, lisez le billet de blog suivant : 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [Détectez et protégez les données sensibles via Azure Information Protection et Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informations collectées et envoyées à Microsoft

Pour générer ces rapports, les points de terminaison envoient les types suivants d’informations à Microsoft :

- Action d’étiquette. Par exemple, définir une étiquette, modifier une étiquette, ajouter ou supprimer la protection, étiquettes automatiques et recommandées.

- Nom de l’étiquette avant et après l’action d’étiquette.

- ID de locataire de votre organisation.

- ID d’utilisateur (adresse e-mail ou UPN).

- Nom de l’appareil de l’utilisateur.

- Pour les documents : chemin et nom de fichier des documents qui sont étiquetés.

- Pour les e-mails : l’objet de l’e-mail et l’expéditeur de l’e-mail pour les e-mails étiquetés. 

- [Types d’informations sensibles prédéfinis](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) qui ont été détectés dans le contenu.
    
    Si vous utilisez Azure Information Protection étiquettes avec des conditions personnalisées, les noms de vos types d’informations personnalisées sont également envoyés. À l’exception de la préversion du client d’étiquetage unifié, les types d’informations sensibles personnalisés que vous créez dans votre centre d’étiquetage ne sont pas envoyés.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics appartenant à votre organisation et consultable indépendamment d’Azure Information Protection par les utilisateurs qui disposent des droits d’accès correspondants. Pour plus d’informations, voir la section [Autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Pour plus d’informations sur la gestion de l’accès à votre espace de travail, consultez la section [Gérer l’accès à l’espace de travail Log Analytics avec des autorisations Azure](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) de la documentation Azure.

Pour empêcher les clients Azure Information Protection (Classic) d’envoyer ces données, affectez au [paramètre de stratégie](configure-policy-settings.md) envoyer des données d’audit la valeur **désactivé** **à Azure information protection Analytics** :

- Pour que la plupart des utilisateurs envoient ces données d’audit et qu’un sous-ensemble ne puisse pas en envoyer : 
    - Affectez à l’option **Envoyer les données d’audit** la valeur **désactivé** à Azure information protection Analytics dans une stratégie délimitée pour le sous-ensemble d’utilisateurs. Cette configuration est généralement utilisée dans les scénarios de production.

- Pour que seul un sous-ensemble d’utilisateurs envoie des données d’audit : 
    - Définissez **Envoyer les données d’audit à Azure information protection Analytics** sur **désactivé** dans la stratégie globale, et **sur** dans une stratégie délimitée pour le sous-ensemble d’utilisateurs. Cette configuration est généralement utilisée dans les scénarios de test.

Pour empêcher Azure Information Protection clients unifiés d’envoyer ces données, configurez un [paramètre avancé](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)de stratégie d’étiquette.

#### <a name="content-matches-for-deeper-analysis"></a>Correspondances de contenu pour approfondir l’analyse

Azure Information Protection vous permet de collecter et de stocker les données réelles identifiées comme étant un type d’informations sensibles (prédéfini ou personnalisé). Il peut s’agir, par exemple, de numéros de carte de crédit trouvés, mais aussi de numéros de sécurité sociale, de passeport et de compte bancaire. Les correspondances de contenu s’affichent lorsque vous sélectionnez une entrée dans les **journaux d’activité**et affichez les détails de l' **activité**. 

Par défaut, les clients Azure Information Protection n’envoient pas de correspondances de contenu. Pour modifier ce comportement afin que les correspondances de contenu soient envoyées :

- Pour le client classique, activez une case à cocher dans le cadre de la [configuration](#configure-a-log-analytics-workspace-for-the-reports) de Azure information protection Analytics. La case à cocher est appelée **activer des analyses plus approfondies dans vos données sensibles**.
    
    Si vous souhaitez que la plupart des utilisateurs qui utilisent ce client puissent envoyer des correspondances de contenu, mais qu’un sous-ensemble d’utilisateurs ne peut pas envoyer de correspondances de contenu, activez la case à cocher, puis configurez un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) dans une stratégie délimitée pour le sous-ensemble d’utilisateurs.

- Pour le client d’étiquetage unifié, configurez un [paramètre avancé](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) dans une stratégie d’étiquette.

## <a name="prerequisites"></a>Conditions préalables
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Autres informations|
|---------------|--------------------|
|Un abonnement Azure qui inclut Log Analytics et qui concerne le même locataire qu’Azure Information Protection|Consultez la page de [tarification d’Azure Monitor](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.|
|Pour signaler des informations provenant de clients d’étiquetage : <br /><br />-Azure Information Protection les clients|Le client d’étiquetage unifié et le client classique sont pris en charge. <br /><br />S’il n’est pas déjà installé, vous pouvez télécharger et installer ces clients à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Pour la création de rapports d’informations à partir de banques de données basées sur le Cloud : <br /><br />-Microsoft Cloud App Security |Pour afficher des informations à partir de Microsoft Cloud App Security, configurez l' [intégration Azure information protection](https://docs.microsoft.com/cloud-app-security/azip-integration).|
|Pour la création de rapports d’informations à partir de magasins de données locaux : <br /><br />-Azure Information Protection scanneur |Pour obtenir des instructions d’installation pour le scanneur, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md). |
|Pour obtenir des informations sur les rapports à partir d’ordinateurs Windows 10 :  <br /><br />-Version minimale de 1809 avec Microsoft Defender-protection avancée contre les menaces (Microsoft Defender ATP)|Vous devez activer la fonctionnalité d’intégration de Azure Information Protection à partir de Microsoft Defender Security Center. Pour plus d’informations, consultez [vue d’ensemble de la protection des informations dans Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorisations requises pour l’analytique Azure Information Protection

Caractéristique propre à l’analytique Azure Information Protection, après que vous avez configuré votre espace de travail Azure Log Analytics, vous pouvez utiliser le rôle Administrateur d’Azure AD de Lecteur Sécurité comme alternative aux autres rôles Azure AD qui prennent en charge la gestion d’Azure Information Protection dans le portail Azure.

Comme cette fonctionnalité utilise Azure Monitoring, le contrôle d’accès en fonction du rôle (RBAC) pour Azure contrôle également l’accès à votre espace de travail. Vous avez donc besoin d’un rôle Azure ainsi que d’un rôle Administrateur d’Azure AD pour gérer l’analytique Azure Information Protection. Si vous ne connaissez pas les rôles Azure, il peut s’avérer utile de lire [Différences entre les rôles RBAC Azure et les rôles d’administrateur Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Détails :

1. Il vous faut l’un des [rôles d’administrateur Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants pour accéder au panneau d’analytique d’Azure Information Protection :
    
    - Pour créer votre espace de travail Log Analytics ou des requêtes personnalisées :
    
        - **Administrateur Azure Information Protection**
        - **Administrateur de sécurité**
        - **Administrateur de conformité**
        - **Administrateur des données de conformité**
        - **Administrateur général**
    
    - Une fois l’espace de travail créé, vous pouvez utiliser les rôles suivants avec moins d’autorisations pour afficher les données collectées :
    
        - **Lecteur Sécurité**
        - **Lecteur global**
    
    > [!NOTE] 
    > Vous ne pouvez pas utiliser le rôle d’administrateur Azure Information Protection ou le rôle lecteur global si votre locataire se trouve sur la [plateforme d’étiquetage unifiée](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

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

- Rôle d’administrateur Azure AD : **lecteur de sécurité**
- Rôle Azure : **log Analytics Reader**

Toutefois, de nombreuses organisations attribuent le rôle Azure AD **Lecteur Sécurité** et le rôle Azure **Lecteur**.

### <a name="storage-requirements-and-data-retention"></a>Exigences de stockage et rétention des données

La quantité de données collectées et stockées dans votre espace de travail Azure Information Protection varie considérablement pour chaque locataire, en fonction de facteurs tels que le nombre de clients Azure Information Protection et d’autres points de terminaison pris en charge, que vous soyez la collecte de données de découverte de point de terminaison, vous avez déployé des scanneurs, le nombre de documents protégés auxquels vous accédez, etc.

Toutefois, comme point de départ, vous pouvez trouver les estimations suivantes utiles :

- Pour les données d’audit générées par les clients Azure Information Protection uniquement : 2 Go par 10 000 utilisateurs actifs par mois.

- Pour les données d’audit générées par les clients Azure Information Protection, les scanneurs et Microsoft Defender ATP : 20 Go par 10 000 utilisateurs actifs par mois.

Si vous utilisez l’étiquetage obligatoire ou si vous avez configuré une étiquette par défaut pour la plupart des utilisateurs, vos tarifs seront probablement beaucoup plus élevés.

Azure Monitor journaux a une fonctionnalité d' **utilisation et de coûts estimés** pour vous aider à estimer et à examiner la quantité de données stockées, et vous pouvez également contrôler la période de rétention des données pour votre espace de travail log Analytics. Pour plus d’informations, consultez [gérer l’utilisation et les coûts avec Azure Monitor journaux](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](https://portal.azure.com) avec un compte qui possède les [autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options du menu **Gérer**, puis sélectionnez **Configurer l’analytique (préversion)** .

3. Dans le panneau **Azure Information Protection - Log Analytics**, vous pouvez voir une liste des espaces de travail Log Analytics qui sont détenus par votre locataire. Procédez de l'une des façons suivantes :
    
    - Pour créer un espace de travail Log Analytics : sélectionnez **Créer un espace de travail** puis, dans le panneau **Espace de travail Log Analytics**, fournissez les informations demandées.
    
    - Pour utiliser un espace de travail Log Analytics existant : sélectionnez l’espace de travail dans la liste.
    
    Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

4. Si vous avez des clients Azure Information Protection (Classic), activez la case à cocher **activer l’analyse plus profonde dans vos données sensibles** si vous souhaitez stocker les données réelles identifiées comme étant un type d’informations sensibles. Pour plus d’informations sur ce paramètre, consultez la section [correspondances de contenu pour une analyse plus profonde](#content-matches-for-deeper-analysis) sur cette page.

5. Sélectionnez **OK**.

Une fois l’espace de travail configuré, procédez comme suit si vous publiez des étiquettes de sensibilité dans l’un des centres d’administration suivants : Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center, Microsoft 365 Compliance Center :

- Dans la Portail Azure accédez à **Azure Information Protection** > **gérer**l'**étiquetage unifié** > , puis sélectionnez **publier**.
    
    Sélectionnez cette option de **publication** chaque fois que vous effectuez une modification d’étiquette (créer, modifier, supprimer) dans votre centre d’étiquetage. 

Vous êtes maintenant prêt à afficher les rapports.

## <a name="how-to-view-the-reports"></a>Comment afficher les rapports

Dans le panneau Azure Information Protection, recherchez les options du menu **Tableaux de bord**, puis sélectionnez l’une des options suivantes :

- **Rapport d’utilisation (préversion)**  : utilisez ce rapport pour voir comment vos étiquettes sont utilisées.

- **Journaux d’activité (préversion)** : utilisez ce rapport pour voir les actions d’étiquetage effectuées par les utilisateurs sur les appareils et les chemins d'accès. En outre, pour les documents protégés, vous pouvez voir les tentatives d’accès (réussies ou refusées) pour les utilisateurs à l’intérieur et à l’extérieur de votre organisation, même s’ils n’ont pas le client Azure Information Protection installé.
    
    Ce rapport comporte une option **Colonnes** qui permet d’afficher plus d’informations sur l’activité que l’affichage par défaut. Vous pouvez également voir plus de détails sur un fichier en le sélectionnant pour afficher les **détails de l’activité**.

- **Découverte des données (** préversion) : utilisez ce rapport pour afficher des informations sur les fichiers étiquetés trouvés par les scanneurs et les points de terminaison pris en charge.
    
    Conseil : à partir des informations collectées, vous pouvez trouver des utilisateurs qui accèdent à des fichiers contenant des informations sensibles à partir d’un emplacement que vous ne connaissez pas ou qui ne sont pas en train d’analyser :
    
    - Si les emplacements sont locaux, vous pouvez envisager de les ajouter en tant que référentiels de données supplémentaires pour le scanneur Azure Information Protection.
    - Si les emplacements sont dans le cloud, envisagez d’utiliser Microsoft Cloud App Security pour les gérer. 
    
- **Recommandations (** préversion) : utilisez ce rapport pour identifier les fichiers qui contiennent des informations sensibles et pour réduire les risques en suivant les recommandations.
    
    Quand vous sélectionnez un élément, l’option **Afficher les données** affiche les activités d’audit qui ont déclenché la recommandation.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Comment modifier les rapports et créer des requêtes personnalisées

Sélectionnez l’icône de requête dans le tableau de bord pour ouvrir un panneau **Recherche dans les journaux** : 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


Les données enregistrées pour Azure Information Protection sont stockées dans le tableau suivant : **InformationProtectionLogs_CL**

Lorsque vous créez vos propres requêtes, utilisez les noms de schéma conviviaux qui ont été implémentés en tant que fonctions **InformationProtectionEvents**. Ces fonctions sont dérivées des attributs qui sont pris en charge pour les requêtes personnalisées (certains attributs sont à usage interne uniquement) et leurs noms ne changeront pas au fil du temps, même si les attributs sous-jacents changent à des fins d’amélioration et de nouvelle fonctionnalité.

### <a name="friendly-schema-reference-for-event-functions"></a>Référence de schéma conviviale pour les fonctions d’événement

Utilisez le tableau suivant pour identifier le nom convivial des fonctions d’événement que vous pouvez utiliser pour les requêtes personnalisées avec l’analytique Azure Information Protection.

|Nom de la colonne|Description|
|-----------|-----------|
|Accès|Un document protégé a été ouvert avec succès, identifié par le nom de fichier s’il est suivi, ou ID s’il n’est pas suivi.|
|AccessDenied|L’accès à un document protégé a été refusé, identifié par le nom de fichier s’il est suivi, ou ID s’il n’est pas suivi.|
|Heure|Heure de l’événement : UTC au format AAAA-MM-JJThh : MM : SS|
|Utilisateur|Utilisateur : format UPN ou domaine\utilisateur|
|ItemPath|Chemin d’accès complet de l’élément ou objet de l’e-mail|
|ItemName|Nom de fichier ou objet de l’e-mail |
|Méthode|Méthode assignée à l’étiquette : Manual, auto, Recommended, default ou Mandatory|
|Activité|Activité d’audit : DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection ou NewCustomProtection |
|LabelName|Nom de l’étiquette (non localisé)|
|LabelNameBefore |Nom de l’étiquette avant modification (non localisé) |
|ProtectionType|Type de protection [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  « TemplateID » : « GUID » <br /> } <br />|
|ProtectionBefore|Type de protection avant modification [JSON] |
|InformationTypesMatches|Tableau JSON de [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvé dans les données où un tableau vide signifie qu’aucun type d’information n’a été trouvé, et null signifie qu’aucune information n’est disponible|
|MachineName |FQDN, le cas échéant ; sinon nom d’hôte|
|DeviceRisk|Score de risque de l’appareil à partir de émission quand il est disponible|
|Plate-forme|Plateforme d’appareils (Win, OSX, Android, iOS) |
|ApplicationName|Nom convivial de l’application|
|AIPVersion|Version du client Azure Information Protection qui a effectué l’action d’audit |
|TenantId|ID de locataire Azure AD |
|AzureApplicationId|ID d’application inscrite Azure AD (GUID)|
|ProcessName|Processus qui héberge le kit de développement logiciel MIP|
|ID|GUID de l’étiquette ou null|
|IsProtected|Si protégé : oui/non |
|ProtectionOwner |Rights Management propriétaire au format UPN|
|LabelIdBefore|GUID de l’étiquette ou null avant modification|
|InformationTypesAbove55|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 55 ou supérieur |
|InformationTypesAbove65|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 65 ou supérieur |
|InformationTypesAbove75|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 75 ou supérieur |
|InformationTypesAbove85|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 85 ou supérieur |
|InformationTypesAbove95|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 95 ou supérieur|
|DiscoveredInformationTypes |Tableau JSON de [SensitiveInformation](https://docs.microsoft.com/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données et leur contenu mis en correspondance (s’il est activé) où un tableau vide signifie qu’aucun type d’information n’a été trouvé, et null signifie qu’aucune information n’est disponible |
|ProtectedBefore|Si le contenu a été protégé avant modification : oui/non |
|ProtectionOwnerBefore|Rights Management propriétaire avant modification |
|UserJustification|Justification de la rétrogradation ou de la suppression d’une étiquette|
|LastModifiedBy|Utilisateur au format UPN qui a modifié le fichier pour la dernière fois. Disponible uniquement pour Office et SharePoint Online|
|LastModifiedDate &|UTC au format AAAA-MM-JJThh : MM : SS : disponible pour Office & SharePoint Online uniquement |


#### <a name="examples-using-informationprotectionevents"></a>Exemples d’utilisation d’InformationProtectionEvents

Utilisez les exemples suivants pour voir comment vous pouvez utiliser le schéma convivial pour créer des requêtes personnalisées.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Exemple 1 : renvoyer tous les utilisateurs qui ont envoyé des données d’audit au cours des 31 derniers jours 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Exemple 2 : retourner le nombre d’étiquettes qui ont été rétrogradées par jour au cours des 31 derniers jours 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Exemple 3 : retourner le nombre d’étiquettes qui ont été rétrogradées de confidentielles par utilisateur, au cours des 31 derniers jours 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

Dans cet exemple, une étiquette rétrogradée est comptabilisée uniquement si le nom de l’étiquette avant l’action contenait le nom **Confidentiel** et le nom de l’étiquette après l’action ne contenait pas le nom **Confidentiel**. 


## <a name="next-steps"></a>Étapes suivantes
Après avoir vérifié les informations dans les rapports, si vous utilisez le client Azure Information Protection, vous pouvez décider d’apporter des modifications à votre stratégie de Azure Information Protection. Pour obtenir des instructions, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Si vous avez un abonnement Microsoft 365, vous pouvez également consulter l’utilisation des étiquettes dans le Centre de conformité Microsoft 365 et le Centre de sécurité Microsoft 365. Pour plus d’informations, voir [Afficher l’utilisation des étiquettes avec l’Analyse des étiquettes](/microsoft-365/compliance/label-analytics).
