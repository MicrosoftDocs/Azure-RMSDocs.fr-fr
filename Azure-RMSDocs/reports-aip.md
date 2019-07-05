---
title: Création de rapports centralisée pour Azure Information Protection
description: Guide pratique pour utiliser la création de rapports centralisée pour suivre l’adoption de vos étiquettes Azure Information Protection et identifier les fichiers qui contiennent des informations sensibles
author: cabailey
ms.author: cabailey
ms.date: 07/04/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: c39e2be3fef7568179f3859f834f92cc761b6259
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563418"
---
# <a name="central-reporting-for-azure-information-protection"></a>Création de rapports centralisée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée.

Utiliser l’analytique d’Azure Information Protection pour la création de rapports centralisée afin de vous aider à effectuer le suivi de l’adoption de vos étiquettes Azure Information Protection. De plus :

- Surveillez les documents et les e-mails étiquetés et protégés dans votre organisation

- Identifiez les documents qui contiennent des informations sensibles dans votre organisation

- Surveiller l’accès utilisateur aux documents et e-mails étiquetés, et faire le suivi des modifications apportées à la classification des documents.

- Identifiez les documents qui contiennent des informations sensibles susceptibles de mettre votre organisation en péril si elles ne sont pas protégées, et limitez les risques en suivant les recommandations.

Les données que vous voyez sont agrégées à partir de vos clients d’Azure Information Protection et les scanneurs d’Azure Information Protection, à partir d’ordinateurs Windows en cours d’exécution [Microsoft Defender Advanced Threat Protection (ATP Microsoft Defender)](/windows/security/threat-protection/microsoft-defender-atp/overview)et à partir de [les clients qui prennent en charge l’étiquetage unifiée](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

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
    
    - Quelles actions d’étiquetage ont été effectuées par une application donnée, comme l’Explorateur de fichiers et le clic droit, ou le module PowerShell AzureInformationProtection
    
    - Explorez les fichiers signalés pour afficher les **détails de l’activité** afin d’obtenir plus d’informations

- À partir du rapport de **découverte de données** :

    - Les fichiers se trouvent sur vos référentiels de données analysé, Windows 10 ordinateurs ou les ordinateurs qui exécutent le client Azure Information Protection ou [les clients qui prennent en charge l’étiquetage unifiée](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling)
    
    - Fichiers étiquetés et protégés, et emplacement des fichiers en fonction des étiquettes
    
    - Fichiers qui contiennent des informations sensibles pour des catégories connues, telles que les données financières et les informations personnelles, et emplacement des fichiers en fonction de ces catégories

- À partir du rapport **Recommandations** :
    
    - Identifiez les fichiers non protégés qui contiennent un type connu d’informations sensibles. Une recommandation vous permet de configurer immédiatement la condition correspondante pour une de vos étiquettes à appliquer automatique ou pour l’étiquetage recommandé.
        
        Si vous suivez la recommandation : La prochaine fois que les fichiers sont ouverts par un utilisateur ou analysés par le scanneur Azure Information Protection, ils peuvent être classifiés et protégés automatiquement.
    
    - Référentiels de données ayant des fichiers avec des informations confidentielles identifiées, mais qui ne sont pas analysés par Azure Information Protection. Une recommandation vous permet d’ajouter immédiatement le magasin de données identifié à un des profils du scanneur.
        
        Si vous suivez la recommandation : Lors du prochain cycle du scanneur, les fichiers peuvent être classifiés et protégés automatiquement.

Les rapports utilisent [Azure Monitor](/azure/log-analytics/log-analytics-overview) pour stocker les données dans un espace de travail Log Analytics appartenant à votre organisation. Si vous êtes familiarisé avec le langage de requête, vous pouvez modifier les requêtes ainsi que créer des rapports et tableaux de bord Power BI. Le tutoriel suivant peut s’avérer utile pour comprendre le langage de requête : [Prise en main des requêtes de journal Azure Monitor](/azure/azure-monitor/log-query/get-started-queries).

Pour plus d’informations, lisez le billet de blog suivant : 
- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [Découvrir et de protéger les données sensibles via Azure Information Protection et Microsoft Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informations collectées et envoyées à Microsoft

Pour générer ces rapports, les points de terminaison envoient les types suivants d’informations à Microsoft :

- Action d’étiquette. Par exemple, définir une étiquette, modifier une étiquette, ajouter ou supprimer la protection, étiquettes automatiques et recommandées.

- Nom de l’étiquette avant et après l’action d’étiquette.

- ID de locataire de votre organisation.

- ID d’utilisateur (adresse e-mail ou UPN).

- Nom de l’appareil de l’utilisateur.

- Pour les documents : Chemin et nom de fichier des documents qui sont étiquetés.

- Pour les e-mails : Objet de l’e-mail et expéditeur de l’e-mail pour les e-mails étiquetés. 

- Types d’informations sensibles ([prédéfinis](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) et personnalisés) détectés dans le contenu.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics appartenant à votre organisation et consultable indépendamment d’Azure Information Protection par les utilisateurs qui disposent des droits d’accès correspondants. Pour plus d’informations, voir la section [Autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Pour plus d’informations sur la gestion de l’accès à votre espace de travail, consultez la section [Gérer l’accès à l’espace de travail Log Analytics avec des autorisations Azure](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) de la documentation Azure.

Pour empêcher les clients Azure Information Protection d’envoyer ces données, définissez le [paramètre de stratégie](configure-policy-settings.md) **Envoyer des données d’audit à l’analytique des journaux d'activité Azure Information Protection** sur **Désactivé** :

- Pour que la plupart des utilisateurs envoient ces données d’audit et qu’un sous-ensemble ne puisse pas en envoyer : 
    - Définissez **Envoyer des données d’audit à l’analytique des journaux d'activité Azure Information Protection** sur **Désactivé** dans une stratégie délimitée autour de ce sous-ensemble d’utilisateurs. Cette configuration est généralement utilisée dans les scénarios de production.

- Pour que seul un sous-ensemble d’utilisateurs envoie des données d’audit : 
    - Définissez **Envoyer des données d’audit à l’analytique des journaux d'activité Azure Information Protection** sur **Désactivé** dans la stratégie globale, et sur **Activé** dans une stratégie délimitée autour de ce sous-ensemble d’utilisateurs. Cette configuration est généralement utilisée dans les scénarios de test.

#### <a name="content-matches-for-deeper-analysis"></a>Correspondances de contenu pour approfondir l’analyse 

Votre espace de travail Azure Log Analytics pour Azure Information Protection comporte une case à cocher permettant de collecter et de stocker également les données identifiées par les types d’informations sensibles ou vos conditions personnalisées. Il peut s’agir, par exemple, de numéros de carte de crédit trouvés, mais aussi de numéros de sécurité sociale, de passeport et de compte bancaire. Si vous ne voulez pas envoyer ces données supplémentaires, ne cochez pas cette case. Si vous souhaitez que la plupart des utilisateurs envoient ces données supplémentaires et qu’un sous-ensemble ne puisse pas en envoyer, cochez la case et configurez un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) dans une stratégie délimitée autour de cette fraction d’utilisateurs.

Une fois recueillies, les correspondances de contenu s’affichent dans les rapports : descendez dans la hiérarchie jusqu’aux fichiers des journaux d’activité pour afficher **Détails de l’activité**. Ces informations sont également consultables et récupérables avec des requêtes.

## <a name="prerequisites"></a>Prérequis
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Un abonnement Azure qui inclut Log Analytics et qui concerne le même locataire qu’Azure Information Protection|Consultez la page de [tarification d’Azure Monitor](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.|
|Le client Azure Information Protection ou le client d’étiquetage unifié Azure Information Protection|Si vous ne disposez pas d’un de ces clients, vous pouvez télécharger et les installer à partir de la [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). <br /><br /> Vérifiez que vous disposez de la version la plus récente pour prendre en charge [toutes les fonctionnalités](#features-that-require-a-minimum-version-of-the-client) pour l’analytique d’Azure Information Protection.|
|Pour le rapport de **découverte et des risques** : <br /><br />-Pour afficher des données à partir de banques de données locales, vous avez déployé au moins une instance du scanneur Azure Information Protection <br /><br />-Pour afficher des données à partir d’ordinateurs Windows 10, ils doivent être une version minimale de 1809, à l’aide de Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP), et vous avez activé la fonctionnalité d’intégration Azure Information Protection à partir de Microsoft Defender Security Center|Pour obtenir des instructions d’installation pour le scanneur, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md). <br /><br />Pour plus d’informations sur la configuration et à l’aide de la fonctionnalité d’intégration Azure Information Protection depuis Microsoft Defender Security Center, consultez [protection des informations dans la vue d’ensemble de Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).|
|Pour le rapport **Recommandations** : <br /><br />-Pour ajouter un nouveau référentiel de données à partir du portail Azure en tant qu’une action recommandée, vous devez utiliser la dernière version de disponibilité générale du scanneur Azure Information Protection |Pour déployer le scanneur, consultez [déploiement du scanneur Azure Information Protection pour classifier et protéger les fichiers automatiquement](deploy-aip-scanner.md).|

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
    
    - Une fois l’espace de travail créé, vous pouvez utiliser le rôle suivant avec moins d’autorisations pour afficher les données collectées :
    
        - **Lecteur Sécurité**
    
    > [!NOTE] 
    > Si votre client a été migré vers le magasin d’étiquetage unifié, vous ne pouvez pas utiliser le rôle d’administrateur Azure Information Protection. [Plus d’informations](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. Par ailleurs, vous devez disposer de l’un des [rôles Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/manage-access#manage-access-to-log-analytics-workspace-using-azure-permissions) ou [rôles Azure](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments) standard pour accéder à votre espace de travail Azure Log Analytics :
    
    - Pour créer l’espace de travail Log Analytics ou des requêtes personnalisées :
    
        - **Contributeur Log Analytics**
        - **Contributeur**
        - **Propriétaire**
    
    - Une fois l’espace de travail créé, vous pouvez utiliser l’un des rôles suivants avec moins d’autorisations pour afficher les données collectées :
    
        - **Lecteur Log Analytics**
        - **Lecteur**

#### <a name="minimum-roles-to-view-the-reports"></a>Rôles minimaux permettant d’afficher les rapports

Une fois l’espace de travail configuré pour l’analytique Azure Information Protection, les deux rôles nécessaires au minimum pour afficher les rapports d’analytique Azure Information Protection sont les suivants :

- Rôle Administrateur d’Azure AD : **Lecteur Sécurité**
- Rôle Azure : **Lecteur Log Analytics**

Toutefois, de nombreuses organisations attribuent le rôle Azure AD **Lecteur Sécurité** et le rôle Azure **Lecteur**.

### <a name="features-that-require-a-minimum-version-of-the-client"></a>Fonctionnalités qui nécessitent une version minimale du client

Vous pouvez utiliser les informations d’historique de version pour le [étiquetage client unifié, Azure Information Protection](./rms-client/unifiedlabelingclient-version-release-history.md) et [client Azure Information Protection](./rms-client/client-version-release-history.md) pour confirmer si votre version du client prend en charge toutes les fonctionnalités de création de rapports centrales. Les versions minimales pour les clients :

Pour le client d’étiquetage Azure Information Protection unifié :

- Prise en charge pour la découverte de l’audit et de point de terminaison : Version 2.0.778.0

Pour le client Azure Information Protection :

- Prise en charge pour l’audit : Version 1.41.51.0
- Prise en charge pour la découverte de point de terminaison : Version 1.48.204.0

### <a name="storage-requirements-and-data-retention"></a>Rétention de données et des besoins de stockage

La quantité de données collectées et stockées dans votre espace de travail Azure Information Protection peut varier considérablement pour chaque client, en fonction de facteurs tels que la procédure de nombreux clients Azure Information Protection et autres points de terminaison pris en charge vous disposez, que vous soyez collecte de données de découverte de point de terminaison, vous avez déployé des scanneurs et ainsi de suite.

Toutefois, en tant que point de départ, vous pouvez trouver les estimations suivantes utiles :

- Pour les données d’audit générées par les clients Azure Information Protection uniquement : 2 Go par 10 000 utilisateurs actifs par mois.

- Pour les données d’audit générées par les clients Azure Information Protection, les scanneurs et les Microsoft Defender ATP : 20 Go par 10 000 utilisateurs actifs par mois.

Si vous utilisez l’étiquetage obligatoire ou que vous avez configuré une étiquette par défaut dans la stratégie globale, aux tarifs sont susceptibles d’être beaucoup plus importante.

Journaux d’analyse Azure a un **l’utilisation et estimation des coûts** des fonctionnalités pour vous aider à estimer et vérifiez la quantité de données stockées, et vous pouvez également contrôler la période de rétention de données pour votre espace de travail Analytique de journal. Pour plus d’informations, consultez [gérer l’utilisation et les coûts avec les journaux d’Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](https://portal.azure.com) avec un compte qui possède les [autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options du menu **Gérer**, puis sélectionnez **Configurer l’analytique (préversion)** .

3. Dans le panneau **Azure Information Protection - Log Analytics**, vous pouvez voir une liste des espaces de travail Log Analytics qui sont détenus par votre locataire. Effectuez l'une des opérations suivantes :
    
    - Pour créer un espace de travail Log Analytics : Sélectionnez **Créer un espace de travail** puis, dans le panneau **Espace de travail Log Analytics**, spécifiez les informations demandées.
    
    - Pour utiliser un espace de travail Log Analytics : Sélectionnez l’espace de travail dans la liste.

Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quand l’espace de travail est configuré, vous êtes prêt à afficher les rapports.

> [!NOTE] 
> Il se produit actuellement un problème connu lors du premier affichage des données dans les rapports. Dans ce cas, définissez le [paramètre de stratégie](configure-policy-settings.md) **Envoyer des données d’audit à l’analytique des journaux d'activité Azure Information Protection** sur **Désactivé** dans la stratégie globale et enregistrez-la. Ensuite, redéfinissez le même paramètre sur **Activé** et enregistrez la stratégie. Une fois que les clients ont [téléchargé la modification](configure-policy.md#making-changes-to-the-policy), leurs événements d’audit sont visibles dans votre espace de travail Log Analytics au bout de 30 minutes maximum.

## <a name="how-to-view-the-reports"></a>Comment afficher les rapports

Dans le panneau Azure Information Protection, recherchez les options du menu **Tableaux de bord**, puis sélectionnez l’une des options suivantes :

- **Rapport d’utilisation (préversion)**  : Utilisez ce rapport pour voir comment vos étiquettes sont utilisées.

- **Journaux d’activité (préversion)**  : Utilisez ce rapport pour voir les actions d’étiquetage effectuées par les utilisateurs sur les appareils et les chemins de fichiers.
    
    Ce rapport comporte une option **Colonnes** qui permet d’afficher plus d’informations sur l’activité que l’affichage par défaut. Vous pouvez également voir plus de détails sur un fichier en le sélectionnant pour afficher les **détails de l’activité**.

- **Découverte de données (préversion)**  : Utilisez ce rapport pour voir des informations sur les fichiers étiquetés trouvés par les scanneurs et les points de terminaison pris en charge.
    
    Conseil : À partir des informations collectées, vous pouvez trouver des utilisateurs qui accèdent à des fichiers contenant des informations sensibles à partir d’un emplacement que vous ne connaissez pas ou qui n’est pas actuellement analysé :
    
    - Si les emplacements sont locaux, vous pouvez envisager de les ajouter en tant que référentiels de données supplémentaires pour le scanneur Azure Information Protection.
    - Si les emplacements sont dans le cloud, envisagez d’utiliser Microsoft Cloud App Security pour les gérer. 
    
- **Recommandations (préversion)**  : Utilisez ce rapport pour identifier les fichiers qui ont des informations sensibles et limiter les risques en suivant les recommandations.
    
    Quand vous sélectionnez un élément, l’option **Afficher les données** affiche les activités d’audit qui ont déclenché la recommandation.


## <a name="how-to-modify-the-reports-and-create-custom-queries"></a>Comment modifier les rapports et créer des requêtes personnalisées

Sélectionnez l’icône de requête dans le tableau de bord pour ouvrir un panneau **Recherche dans les journaux** : 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


Les données consignées pour Azure Information Protection sont stockées dans la table suivante : **InformationProtectionLogs_CL**

Lorsque vous créez vos propres requêtes, utilisez les noms de schéma conviviaux qui ont été implémentés en tant que fonctions **InformationProtectionEvents**. Ces fonctions sont dérivées des attributs qui sont pris en charge pour les requêtes personnalisées (certains attributs sont à usage interne uniquement) et leurs noms ne changeront pas au fil du temps, même si les attributs sous-jacents changent à des fins d’amélioration et de nouvelle fonctionnalité.

### <a name="friendly-schema-reference-for-event-functions"></a>Référence de schéma conviviale pour les fonctions d’événement

Utilisez le tableau suivant pour identifier le nom convivial des fonctions d’événement que vous pouvez utiliser pour les requêtes personnalisées avec l’analytique Azure Information Protection.

|Nom de la colonne|Description|
|-----------|-----------|
|Time|Heure de l’événement : Heure UTC au format AAAA-MM-JJThh|
|Utilisateur|Utilisateur : Format UPN ou domaine\nom d’utilisateur|
|ItemPath|Objet de chemin d’accès ou de courrier électronique l’élément complet|
|ItemName|Fichier objet de nom ou e-mail |
|Méthode|Nom attribué de méthode : Manuel, automatique, recommandé, par défaut ou obligatoire|
|Activité|Activité d’audit : DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, découvrir, accès, RemoveCustomProtection, ChangeCustomProtection ou NewCustomProtection |
|LabelName|Nom de l’étiquette (ne pas localisé)|
|LabelNameBefore |Nom d’étiquette avant modification (non localisée) |
|ProtectionType|Type de protection [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  "TemplateID": "GUID" <br /> } <br />|
|ProtectionBefore|Type de protection avant modification [JSON] |
|InformationTypesMatches|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) ne trouvé dans les données où un tableau vide ne signifie aucun type d’informations est trouvé et null signifie aucune information disponible|
|MachineName |Nom de domaine complet lorsqu’il est disponible ; nom d’hôte dans le cas contraire|
|DeviceRisk|Score de risque d’appareil à partir de Windows Defender ATP lorsqu’il est disponible|
|Plateforme|Plateforme d’appareil (Win, OSX, Android, iOS) |
|ApplicationName|Nom convivial de l’application|
|AIPVersion|Version du client Azure Information Protection qui a effectué l’action d’audit |
|TenantId|ID de locataire Azure AD |
|AzureApplicationId|ID (GUID) de l’application inscrits à Azure AD|
|ProcessName|Processus qui héberge du SDK MIP|
|LabelId|GUID de l’étiquette ou la valeur null|
|IsProtected|Si des protégés : Oui/non |
|ProtectionOwner |Propriétaire Rights Management au format UPN|
|LabelIdBefore|GUID de l’étiquette ou la valeur null avant modification|
|InformationTypesAbove55|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvées dans les données avec le niveau de confiance 55 ou ultérieure |
|InformationTypesAbove65|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvées dans les données avec le niveau de confiance 65 ou version ultérieure |
|InformationTypesAbove75|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvées dans les données avec le niveau de confiance 75 ou version ultérieure |
|InformationTypesAbove85|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvées dans les données avec le niveau de confiance 85 ou version ultérieure |
|InformationTypesAbove95|Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvées dans les données avec le niveau de confiance de 95 ou version ultérieure|
|DiscoveredInformationTypes |Tableau JSON des [SensitiveInformation](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) trouvé dans les données et leur mise en correspondance du contenu (si activé) où un tableau vide ne signifie aucun type d’informations est trouvé et null signifie aucune information disponible |
|ProtectedBefore|Indique si le contenu a été protégé avant modification : Oui/non |
|ProtectionOwnerBefore|Propriétaire Rights Management avant modification |
|UserJustification|Justification quand rétrogradation ou de supprimer l’étiquette|
|LastModifiedBy|Utilisateur au format UPN qui a modifié le fichier. Disponible pour Office et SharePoint Online uniquement|
|LastModifiedDate|Heure UTC au format AAAA-MM-JJThh : Disponible pour Office et SharePoint Online uniquement |


#### <a name="examples-using-informationprotectionevents"></a>Exemples d’utilisation d’InformationProtectionEvents

Utilisez les exemples suivants pour voir comment vous pouvez utiliser le schéma convivial pour créer des requêtes personnalisées.

##### <a name="example-1-return-all-users-who-sent-audit-data-in-the-last-31-days"></a>Exemple 1 : Retourner tous les utilisateurs ayant envoyé des données d’audit au cours des 31 derniers jours 

```
InformationProtectionEvents 
| where Time > ago(31d) 
| distinct User 
```

 
##### <a name="example-2-return-the-number-of-labels-that-were-downgraded-per-day-in-the-last-31-days"></a>Exemple 2 : Retourner le nombre d’étiquettes qui ont été rétrogradées par jour au cours des 31 derniers jours 


```
InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| summarize Label_Downgrades_per_Day = count(Activity) by bin(Time, 1d) 
 
```
 
##### <a name="example-3-return-the-number-of-labels-that-were-downgraded-from-confidential-by-user-in-the-last-31-days"></a>Exemple 3 : Retourner le nombre d’étiquettes qui ont été rétrogradées depuis l’état Confidentiel par utilisateur au cours des 31 derniers jours 

```

InformationProtectionEvents 
| where Time > ago(31d) 
| where Activity == "DowngradeLabel"  
| where LabelNameBefore contains "Confidential" and LabelName !contains "Confidential"  
| summarize Label_Downgrades_by_User = count(Activity) by User | sort by Label_Downgrades_by_User desc 

```

Dans cet exemple, une étiquette rétrogradée est comptabilisée uniquement si le nom de l’étiquette avant l’action contenait le nom **Confidentiel** et le nom de l’étiquette après l’action ne contenait pas le nom **Confidentiel**. 


## <a name="next-steps"></a>Étapes suivantes
Après avoir examiné les informations contenues dans les rapports, si vous utilisez le client Azure Information Protection, vous pouvez décider à apporter des modifications à votre stratégie Azure Information Protection. Pour obtenir des instructions, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Si vous avez un abonnement Microsoft 365, vous pouvez également consulter l’utilisation des étiquettes dans le Centre de conformité Microsoft 365 et le Centre de sécurité Microsoft 365. Pour plus d’informations, voir [Afficher l’utilisation des étiquettes avec l’Analyse des étiquettes](/Office365/SecurityCompliance/label-analytics).
