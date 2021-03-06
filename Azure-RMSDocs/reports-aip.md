---
title: Analyses et rapports centralisés pour Azure Information Protection (AIP)
description: Découvrez comment utiliser l’analyse Azure Information Protection (AIP) et les rapports centraux pour suivre l’utilisation des étiquettes et identifier les fichiers qui contiennent des informations sensibles.
author: batamig
ms.author: bagol
ms.date: 03/01/2021
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.subservice: analytics
ms.reviewer: lilukov
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 661baa61f49c6f85f6b52de99ad807f0fcd67ca5
ms.sourcegitcommit: b2af03adcab2d0446114eea1973a919331cfb437
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103561260"
---
# <a name="analytics-and-central-reporting-for-azure-information-protection-public-preview"></a>Analyse et création de rapports centralisées pour Azure Information Protection (version préliminaire publique)

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Cet article explique comment utiliser Azure Information Protection (AIP) Analytics pour la création de rapports centralisés, qui peut vous aider à suivre l’adoption de vos étiquettes qui classent et protègent les données de votre organisation. 

Les analyses AIP vous permettent également d’effectuer les opérations suivantes :

- Surveillez les documents et les e-mails étiquetés et protégés dans votre organisation

- Identifiez les documents qui contiennent des informations sensibles dans votre organisation

- Surveiller l’accès utilisateur aux documents et e-mails étiquetés, et faire le suivi des modifications apportées à la classification des documents.

- Identifiez les documents qui contiennent des informations sensibles susceptibles de mettre votre organisation en péril si elles ne sont pas protégées, et limitez les risques en suivant les recommandations.

- Identifiez le moment où les utilisateurs internes ou externes accèdent à des documents protégés à partir d’ordinateurs Windows, et si l’accès a été accordé ou refusé.

Les données que vous voyez sont agrégées à partir de vos clients et scanneurs Azure Information Protection, de Microsoft Cloud App Security à partir d’ordinateurs Windows 10 utilisant Microsoft Defender-protection avancée contre les menaces et de [journaux d’utilisation](log-analyze-usage.md)de la protection. 

Azure Information Protection Analytics pour la création de rapports centraux est actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 


## <a name="aip-reporting-data"></a>Données de rapport AIP

Par exemple, le Azure Information Protection Analytics pour central Reporting affiche les données suivantes :

|Rapport  |Exemple de données affichées |
|---------|---------|
|**Rapport d’utilisation**     |  Sélectionnez une période pour afficher l’un des éléments suivants : <br /><br />     -Quelles étiquettes sont appliquées <br /><br />-Nombre de documents et d’e-mails étiquetés <br /><br />-Combien de documents et d’e-mails sont protégés <br /><br />-Nombre d’utilisateurs et nombre d’appareils qui étiquettent des documents et des e-mails <br /><br />-Les applications utilisées pour l’étiquetage     |
|**Journaux d’activité**     | Sélectionnez une période pour afficher l’un des éléments suivants : <br /><br />      -Quels fichiers découverts précédemment par le moteur d’analyse ont été supprimés du référentiel analysé <br /> <br /> -Les actions d’étiquetage effectuées par un utilisateur spécifique <br /><br /> -Les actions d’étiquetage qui ont été effectuées à partir d’un appareil spécifique<br /> <br />    -Quels utilisateurs ont accédé à un document étiqueté spécifique<br /> <br />-Les actions d’étiquetage effectuées pour un chemin d’accès de fichier spécifique<br /> <br />-Les actions d’étiquetage effectuées par une application spécifique, telles que l’Explorateur de fichiers et le clic droit, PowerShell, le scanneur ou Microsoft Cloud App Security <br /> <br />-Les documents protégés ont été correctement consultés par les utilisateurs ou l’accès refusé aux utilisateurs, même si le client Azure Information Protection n’est pas installé ou n’est pas situé à l’extérieur de votre organisation <br /> <br />-Explorez les fichiers signalés pour afficher les détails de l' **activité** pour plus d’informations      |
|**Rapport de découverte des données**     |      -Quels fichiers se trouvent dans vos référentiels de données analysés, ordinateurs Windows 10 ou ordinateurs exécutant les clients Azure Information Protection <br /><br />-Quels sont les fichiers étiquetés et protégés, ainsi que l’emplacement des fichiers par étiquettes <br /><br />-Quels fichiers contiennent des informations sensibles pour les catégories connues, telles que les données financières et les informations personnelles, ainsi que l’emplacement des fichiers par ces catégories       |
|**Rapport de recommandations**     | -Identifier les fichiers non protégés qui contiennent un type d’informations sensibles connu. Une recommandation vous permet de configurer immédiatement la condition correspondante pour une de vos étiquettes à appliquer automatique ou pour l’étiquetage recommandé. **<br /> Si vous suivez la recommandation**: la prochaine fois que les fichiers sont ouverts par un utilisateur ou analysés par le scanneur Azure information protection, les fichiers peuvent être automatiquement classés et protégés. <br /><br /> -Les référentiels de données ont des fichiers avec des informations sensibles identifiées, mais ne sont pas analysés par le Azure Information Protection. Une recommandation vous permet d’ajouter immédiatement le magasin de données identifié à un des profils du scanneur. <br />   **Si vous suivez la recommandation**: lors du prochain cycle du scanneur, les fichiers peuvent être automatiquement classés et protégés.        |
| | |

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

- Adresse IP de l’appareil de l’utilisateur. 

- Le nom du processus approprié, par exemple **Outlook** ou **MSIP. app**.

- Nom de l’application qui a effectué l’étiquetage, comme **Outlook** ou l' **Explorateur de fichiers**

- Pour les documents : chemin et nom de fichier des documents qui sont étiquetés.

- Pour les e-mails : l’objet de l’e-mail et l’expéditeur de l’e-mail pour les e-mails étiquetés. 

- Types d’informations sensibles ([prédéfinis](/office365/securitycompliance/what-the-sensitive-information-types-look-for) et personnalisés) détectés dans le contenu.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics appartenant à votre organisation et consultable indépendamment d’Azure Information Protection par les utilisateurs qui disposent des droits d’accès correspondants. 

Pour plus d'informations, consultez la page suivante :

- [Autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics)
- [Gérer l’accès à l’espace de travail Log Analytics à l’aide des autorisations Azure](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions)
- [Référence du journal d’audit Azure Information Protection](audit-logs.md)

#### <a name="prevent-the-aip-clients-from-sending-auditing-data"></a>Empêcher les clients AIP d’envoyer des données d’audit

**Client d’étiquetage unifié** 

Pour empêcher l’Azure Information Protection client d’étiquetage unifié d’envoyer des données d’audit, configurez un [paramètre avancé](./rms-client/clientv2-admin-guide-customizations.md#disable-sending-audit-data-to-azure-information-protection-analytics)de stratégie d’étiquette.

**Client classique**

Pour empêcher le client Azure Information Protection Classic d’envoyer ces données, affectez la valeur **off** au [paramètre de stratégie](configure-policy-settings.md) envoyer des **données d’audit à Azure information protection Analytics** :

|Condition requise  |Instructions  |
|---------|---------|
|**Pour configurer la plupart des utilisateurs pour envoyer des données, avec un sous-ensemble d’utilisateurs qui ne peuvent pas envoyer de données**     |  Affectez à l’option **Envoyer les données d’audit** la valeur **désactivé** à Azure information protection Analytics dans une stratégie délimitée pour le sous-ensemble d’utilisateurs. <br><br> Cette configuration est généralement utilisée dans les scénarios de production.     |
|**Pour configurer uniquement un sous-ensemble d’utilisateurs qui envoient des données**     |  Définissez **Envoyer les données d’audit à Azure information protection Analytics** sur **désactivé** dans la stratégie globale, et **sur** dans une stratégie délimitée pour le sous-ensemble d’utilisateurs. <br><br>Cette configuration est généralement utilisée dans les scénarios de test.       |
| | |

#### <a name="content-matches-for-deeper-analysis"></a>Correspondances de contenu pour approfondir l’analyse

Azure Information Protection vous permet de collecter et de stocker les données réelles identifiées comme étant un type d’informations sensibles (prédéfini ou personnalisé). Il peut s’agir, par exemple, de numéros de carte de crédit trouvés, mais aussi de numéros de sécurité sociale, de passeport et de compte bancaire. Les correspondances de contenu s’affichent lorsque vous sélectionnez une entrée dans les **journaux d’activité** et affichez les détails de l' **activité**. 

Par défaut, les clients Azure Information Protection n’envoient pas de correspondances de contenu. Pour modifier ce comportement afin que les correspondances de contenu soient envoyées :

|Client  |Instructions  |
|---------|---------|
|**Client d’étiquetage unifié**      |  Configurez un [paramètre avancé](./rms-client/clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics) dans une stratégie d’étiquette.       |
|**Client classique**      |   Activez une case à cocher dans le cadre de la [configuration](#configure-a-log-analytics-workspace-for-the-reports) de Azure information protection Analytics. La case à cocher est appelée **activer des analyses plus approfondies dans vos données sensibles**. <br><br> Si vous souhaitez que la plupart des utilisateurs qui utilisent ce client puissent envoyer des correspondances de contenu, mais qu’un sous-ensemble d’utilisateurs ne peut pas envoyer de correspondances de contenu, activez la case à cocher, puis configurez un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users) dans une stratégie délimitée pour le sous-ensemble d’utilisateurs.     |
|     |         |


## <a name="prerequisites"></a>Prérequis
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise  |Détails  |
|---------|---------|
|**Un abonnement Azure**     |   Votre abonnement Azure doit inclure des Log Analytics sur le même locataire que Azure Information Protection. <br><br> Pour plus d’informations, consultez la page de [tarification Azure Monitor](https://azure.microsoft.com/pricing/details/log-analytics) . <br><br>Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.   |
| **URL de journalisation d’audit connectivité réseau** | AIP doit pouvoir accéder aux URL suivantes afin de prendre en charge les journaux d’audit AIP :<br>- `https://*.events.data.microsoft.com` <br>- `https://*.aria.microsoft.com` (Données de l’appareil Android uniquement)
|**Client Azure Information Protection**    |Pour la création de rapports à partir du client. <br><br>Si vous n’avez pas encore de client installé, vous pouvez télécharger et installer le client d’étiquetage unifié à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).      <br><br>**Remarque**: le client d’étiquetage unifié et le client classique sont pris en charge. Pour le déployer, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.     |
|**Azure Information Protection de l’analyseur local**    | Pour la création de rapports à partir de magasins de données locaux. <br><br>      Pour plus d’informations, consultez [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement des fichiers](deploy-aip-scanner.md).   |
|**Microsoft Cloud App Security (MCAS)**     | Pour la création de rapports à partir de magasins de données basés sur le Cloud. <br><br>Pour plus d’informations, consultez [Azure information protection Integration](/cloud-app-security/azip-integration) dans la documentation de MCAS.        |
|**Version minimale de 1809 avec Microsoft Defender-protection avancée contre les menaces (Microsoft Defender ATP)**     | Pour la création de rapports à partir d’ordinateurs Windows 10. <br>  <br>   Vous devez activer la fonctionnalité d’intégration de Azure Information Protection à partir de Microsoft Defender Security Center. <br><br>Pour plus d’informations, consultez [vue d’ensemble de la protection des informations dans Windows](/windows/security/threat-protection/microsoft-defender-atp/information-protection-in-windows-overview).   |
|     |         |


### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorisations requises pour l’analytique Azure Information Protection

Caractéristique propre à l’analytique Azure Information Protection, après que vous avez configuré votre espace de travail Azure Log Analytics, vous pouvez utiliser le rôle Administrateur d’Azure AD de Lecteur Sécurité comme alternative aux autres rôles Azure AD qui prennent en charge la gestion d’Azure Information Protection dans le portail Azure. Ce rôle supplémentaire est pris en charge uniquement si votre locataire n’est pas sur la [plateforme d’étiquetage unifiée](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

Étant donné que Azure Information Protection Analytics utilise la surveillance Azure, le contrôle d’accès en fonction du rôle (RBAC) pour Azure contrôle également l’accès à votre espace de travail. Vous avez donc besoin d’un rôle Azure ainsi que d’un rôle Administrateur d’Azure AD pour gérer l’analytique Azure Information Protection. Si vous ne connaissez pas les rôles Azure, il peut s’avérer utile de lire [Différences entre les rôles RBAC Azure et les rôles d’administrateur Azure AD](/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Pour plus d'informations, consultez les pages suivantes :

- [Rôles d’administrateur Azure AD requis](#required-azure-ad-administrator-roles)
- [Rôles de Log Analytics Azure requis](#required-azure-log-analytics-roles)
- [Rôles minimaux permettant d’afficher les rapports](#minimum-roles-to-view-the-reports)

#### <a name="required-azure-ad-administrator-roles"></a>Rôles d’administrateur Azure AD requis

Vous devez disposer de l’un des [rôles d’administrateur Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants pour accéder au volet analyse des Azure information protection :

- Pour créer votre espace de travail Log Analytics ou des requêtes personnalisées :
    
    - **Administrateur Azure Information Protection**
    - **Administrateur de sécurité**
    - **Administrateur de conformité**
    - **Administrateur des données de conformité**
    - **Administrateur général**
    
- Une fois l’espace de travail créé, vous pouvez utiliser les rôles suivants avec moins d’autorisations pour afficher les données collectées :
    
    - **Lecteur de sécurité**
    - **Lecteur global**

#### <a name="required-azure-log-analytics-roles"></a>Rôles de Log Analytics Azure requis

Vous devez disposer de l’un des [rôles azure log Analytics](/azure/azure-monitor/platform/manage-access#manage-access-using-azure-permissions) suivants ou des [rôles Azure](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-rbac-roles) standard pour accéder à votre espace de travail Azure log Analytics :
    
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

La quantité de données collectées et stockées dans votre espace de travail Azure Information Protection varie considérablement pour chaque locataire, en fonction de facteurs tels que le nombre de clients Azure Information Protection et d’autres points de terminaison pris en charge, que vous collectiez des données de découverte de point de terminaison, que vous ayez déployé des scanneurs, le nombre de documents protégés auxquels vous accédez, etc.

Toutefois, comme point de départ, vous pouvez trouver les estimations suivantes utiles :

- Pour les données d’audit générées par les clients Azure Information Protection uniquement : 2 Go par 10 000 utilisateurs actifs par mois.

- Pour les données d’audit générées par les clients Azure Information Protection, les scanneurs et Microsoft Defender ATP : 20 Go par 10 000 utilisateurs actifs par mois.

Si vous utilisez l’étiquetage obligatoire ou si vous avez configuré une étiquette par défaut pour la plupart des utilisateurs, vos tarifs seront probablement beaucoup plus élevés.

Azure Monitor journaux a une fonctionnalité d' **utilisation et de coûts estimés** pour vous aider à estimer et à examiner la quantité de données stockées, et vous pouvez également contrôler la période de rétention des données pour votre espace de travail log Analytics. Pour plus d’informations, consultez [gérer l’utilisation et les coûts avec Azure Monitor journaux](/azure/azure-monitor/platform/manage-cost-storage).

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](https://portal.azure.com) avec un compte qui possède les [autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.
    
1. Recherchez les options du menu **gérer** , puis sélectionnez **configurer Analytics (version préliminaire)**.

1. Dans le volet **Azure information protection log Analytics** , vous voyez une liste de tous les espaces de travail log Analytics détenus par votre locataire. Effectuez l’une des opérations suivantes :
    
    - **Pour créer un espace de travail log Analytics**: sélectionnez **créer un nouvel espace** de travail, puis dans le volet **espace de travail log Analytics** , fournissez les informations demandées.
    
    - **Pour utiliser un espace de travail log Analytics existant**: sélectionnez l’espace de travail dans la liste.
    
    Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](/azure/log-analytics/log-analytics-quick-create-workspace).

1. **Client classique AIP uniquement**: cochez la case **activer l’analyse plus profonde dans vos données sensibles** si vous souhaitez stocker les données réelles identifiées comme étant un type d’informations sensibles. 

    Pour plus d’informations sur ce paramètre, consultez la section [correspondances de contenu pour une analyse plus profonde](#content-matches-for-deeper-analysis) sur cette page.

1. Sélectionnez **OK**.

Vous êtes maintenant prêt à afficher les rapports.

## <a name="view-the-aip-analytics-reports"></a>Afficher les rapports d’analyse AIP

Dans le volet Azure Information Protection, recherchez les options du menu **tableaux de bord** , puis sélectionnez l’une des options suivantes :

|Rapport  |Description  |
|---------|---------|
|**Rapport d’utilisation (préversion)**     |  Utilisez ce rapport pour voir comment vos étiquettes sont utilisées.       |
|**Journaux d’activité (version préliminaire)**     |  Utilisez ce rapport pour voir les actions d’étiquetage effectuées par les utilisateurs sur les appareils et les chemins de fichiers. En outre, pour les documents protégés, vous pouvez voir les tentatives d’accès (réussies ou refusées) pour les utilisateurs à l’intérieur et à l’extérieur de votre organisation, même s’ils n’ont pas le client Azure Information Protection installé. <br><br>  Ce rapport comporte une option **colonnes** qui vous permet d’afficher plus d’informations sur l’activité que l’affichage par défaut. Vous pouvez également voir plus de détails sur un fichier en le sélectionnant pour afficher les **détails de l’activité**.     |
|**Découverte de données (version préliminaire)**     |    Utilisez ce rapport pour voir des informations sur les fichiers étiquetés trouvés par les scanneurs et les points de terminaison pris en charge.  <br><br>**Conseil**: à partir des informations collectées, vous pouvez trouver des utilisateurs qui accèdent à des fichiers contenant des informations sensibles à partir d’un emplacement que vous ne connaissez pas ou qui ne sont pas en train d’analyser : <br><br>-Si les emplacements sont locaux, envisagez d’ajouter les emplacements en tant que référentiels de données supplémentaires pour le scanneur Azure Information Protection. <br>  -Si les emplacements se trouvent dans le Cloud, envisagez d’utiliser Microsoft Cloud App Security pour les gérer.    |
|**Recommandations (version préliminaire)**     | Utilisez ce rapport pour identifier les fichiers qui ont des informations sensibles et limiter les risques en suivant les recommandations.  <br><br> Quand vous sélectionnez un élément, l’option **Afficher les données** affiche les activités d’audit qui ont déclenché la recommandation.     |
|     |         |


## <a name="modify-the-aip-analytics-reports-and-create-custom-queries"></a>Modifier les rapports d’analyse AIP et créer des requêtes personnalisées

Sélectionnez l’icône de requête dans le tableau de bord pour ouvrir un volet de recherche dans les **journaux** : 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


Les données enregistrées pour Azure Information Protection sont stockées dans le tableau suivant : **InformationProtectionLogs_CL**

Lorsque vous créez vos propres requêtes, utilisez les noms de schéma conviviaux qui ont été implémentés en tant que fonctions **InformationProtectionEvents**. Ces fonctions sont dérivées des attributs qui sont pris en charge pour les requêtes personnalisées (certains attributs sont à usage interne uniquement) et leurs noms ne changeront pas au fil du temps, même si les attributs sous-jacents changent à des fins d’amélioration et de nouvelle fonctionnalité.

### <a name="friendly-schema-reference-for-event-functions"></a>Référence de schéma conviviale pour les fonctions d’événement

Utilisez le tableau suivant pour identifier le nom convivial des fonctions d’événement que vous pouvez utiliser pour les requêtes personnalisées avec l’analytique Azure Information Protection.

|Nom de la colonne|Description|
|-----------|-----------|
|**Time**|Heure de l’événement : UTC au format AAAA-MM-JJThh : MM : SS|
|**Utilisateur**|Utilisateur : format UPN ou domaine\utilisateur|
|**ItemPath**|Chemin d’accès complet de l’élément ou objet de l’e-mail|
|**ItemName**|Nom de fichier ou objet de l’e-mail |
|**Méthode**|Méthode assignée à l’étiquette : Manual, auto, Recommended, default ou Mandatory|
|**Activité**|Activité d’audit : DowngradeLabel, UpgradeLabel, RemoveLabel, NewLabel, Discover, Access, RemoveCustomProtection, ChangeCustomProtection, NewCustomProtection ou FileRemoved |
|**ResultStatus**|État du résultat de l’action :<br /><br /> Réussite ou échec (signalé par le scanneur AIP uniquement)|
|**ErrorMessage_s**|Contient les détails du message d’erreur si ResultStatus = failed. Signalé par le scanneur AIP uniquement|
|**LabelName**|Nom de l’étiquette (non localisé)|
|**LabelNameBefore** |Nom de l’étiquette avant modification (non localisé) |
|**ProtectionType**|Type de protection [JSON] <br />{ <br />"Type": ["Template", "Custom", "DoNotForward"], <br />  « TemplateID » : « GUID » <br /> } <br />|
|**ProtectionBefore**|Type de protection avant modification [JSON] |
|**MachineName** |FQDN, le cas échéant ; sinon nom d’hôte|
|**DeviceRisk**|Score de risque de l’appareil à partir de émission quand il est disponible|
|**Plateforme**|Plateforme d’appareils (Win, OSX, Android, iOS) |
|**ApplicationName**|Nom convivial de l’application|
|**AIPVersion**|Version du client Azure Information Protection qui a effectué l’action d’audit |
|**TenantId**|ID de locataire Azure AD |
|**AzureApplicationId**|ID d’application inscrite Azure AD (GUID)|
|**ProcessName**|Processus qui héberge le kit de développement logiciel MIP|
|**ID**|GUID de l’étiquette ou null|
|**IsProtected**|Si protégé : oui/non |
|**ProtectionOwner** |Rights Management propriétaire au format UPN|
|**LabelIdBefore**|GUID de l’étiquette ou null avant modification|
|**InformationTypesAbove55**|Tableau JSON des [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 55 ou supérieur |
|**InformationTypesAbove65**|Tableau JSON des [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 65 ou supérieur |
|**InformationTypesAbove75**|Tableau JSON des [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 75 ou supérieur |
|**InformationTypesAbove85**|Tableau JSON des [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 85 ou supérieur |
|**InformationTypesAbove95**|Tableau JSON des [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données avec un niveau de confiance de 95 ou supérieur|
|**DiscoveredInformationTypes** |Tableau JSON de [SensitiveInformation](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) trouvés dans les données et leur contenu mis en correspondance (s’il est activé) où un tableau vide signifie qu’aucun type d’information n’a été trouvé, et null signifie qu’aucune information n’est disponible |
|**ProtectedBefore**|Si le contenu a été protégé avant modification : oui/non |
|**ProtectionOwnerBefore**|Rights Management propriétaire avant modification |
|**UserJustification**|Justification de la rétrogradation ou de la suppression d’une étiquette|
|**LastModifiedBy**|Utilisateur au format UPN qui a modifié le fichier pour la dernière fois. Disponible pour Office et SharePoint uniquement|
|**LastModifiedDate &**|UTC au format AAAA-MM-JJThh : MM : SS : disponible uniquement pour Office et SharePoint |
| | |
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
Après avoir vérifié les informations contenues dans les rapports, si vous utilisez le client Azure Information Protection, vous pouvez décider d’apporter des modifications à votre stratégie d’étiquetage. 

- **Client d’étiquetage unifié**: apportez des modifications à votre stratégie d’étiquetage dans le centre d’administration d’étiquetage, y compris le centre de sécurité Microsoft 365, le centre de conformité Microsoft 365, ou le centre de conformité Microsoft 365 Security &. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

- **Client classique**: apportez des modifications à votre stratégie dans le portail Azure. Pour plus d’informations, consultez [configuration de la stratégie de Azure information protection](configure-policy.md).

Les journaux d’audit AIP sont également envoyés à l’Explorateur d’activités Microsoft 365, où ils peuvent être affichés avec des noms différents. Pour plus d'informations, consultez les pages suivantes :

- [Version préliminaire publique : journaux d’audit AIP dans l’Explorateur d’activités](https://www.yammer.com/askipteam/#/Threads/show?threadId=1085834054254592)
- [Prise en main de l’Explorateur d’activités](/microsoft-365/compliance/data-classification-activity-explorer).