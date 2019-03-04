---
title: Création de rapports centralisée pour Azure Information Protection
description: Guide pratique pour utiliser la création de rapports centralisée pour suivre l’adoption de vos étiquettes Azure Information Protection et identifier les fichiers qui contiennent des informations sensibles
author: cabailey
ms.author: cabailey
ms.date: 02/26/2019
manager: barbkess
ms.topic: article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 319365dd5dfa7c9c5cb82532faa179334c8f0b0f
ms.sourcegitcommit: dde803603371dc30d40ca7225f330163bcc7c103
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56825966"
---
# <a name="central-reporting-for-azure-information-protection"></a>Création de rapports centralisée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée.

Utiliser l’analytique d’Azure Information Protection pour la création de rapports centralisée afin d’effectuer le suivi de l’adoption de vos étiquettes Azure Information Protection. De plus :

- Surveillez l’accès utilisateur aux documents et e-mails étiquetés, et les modifications apportées à leur classification. 

- Identifiez les documents qui contiennent des informations sensibles à protéger.

Actuellement, les données que vous voyez sont agrégées à partir de vos clients Azure Information Protection et des scanneurs Azure Information Protection, et des ordinateurs Windows exécutant [Windows Defender Advanced Threat Protection (Windows Defender ATP)](/windows/security/threat-protection/windows-defender-atp/overview).

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

- À partir du rapport de **découverte de données** :

    - Fichiers qui se trouvent sur vos référentiels de données analysés ou vos ordinateurs Windows 10
    
    - Fichiers étiquetés et protégés, et emplacement des fichiers en fonction des étiquettes
    
    - Fichiers qui contiennent des informations sensibles pour des catégories connues, telles que les données financières et les informations personnelles, et emplacement des fichiers en fonction de ces catégories
    
Les rapports utilisent [Azure Monitor](/azure/log-analytics/log-analytics-overview) pour stocker les données dans un espace de travail Log Analytics appartenant à votre organisation. Si vous êtes familiarisé avec le langage de requête, vous pouvez modifier les requêtes ainsi que créer des rapports et tableaux de bord Power BI. Le tutoriel suivant peut s’avérer utile pour comprendre le langage de requête : [Prise en main des requêtes de journal Azure Monitor](/azure/azure-monitor/log-query/get-started-queries). 

Pour plus d’informations, lisez le billet de blog suivant : 

- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)

- [Discover and protect sensitive data through Azure Information Protection and Windows Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292)

### <a name="information-collected-and-sent-to-microsoft"></a>Informations collectées et envoyées à Microsoft

Pour générer ces rapports, les points de terminaison envoient les types suivants d’informations à Microsoft :

- Action d’étiquette. Par exemple, définir une étiquette, modifier une étiquette, ajouter ou supprimer la protection, étiquettes automatiques et recommandées.

- Nom de l’étiquette avant et après l’action d’étiquette.

- ID de locataire de votre organisation.

- ID d’utilisateur (adresse e-mail ou UPN).

- Nom de l’appareil de l’utilisateur.

- Pour les documents : Chemin et nom de fichier des documents qui sont étiquetés.

- Pour les e-mails : Objet de l’e-mail, expéditeur de l’e-mail et destinataires de l’e-mail pour les e-mails étiquetés. 

- Types d’informations sensibles ([prédéfinis](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) et personnalisés) détectés dans le contenu.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics appartenant à votre organisation et consultable indépendamment d’Azure Information Protection par les utilisateurs qui disposent des droits d’accès correspondants. Pour plus d’informations, voir la section [Autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Pour plus d’informations sur la gestion de l’accès à votre espace de travail, consultez la section [Gérer les comptes et les utilisateurs](/azure/azure-monitor/platform/manage-access#manage-accounts-and-users) dans la documentation Azure.

> [!NOTE]
> Votre espace de travail Azure Log Analytics pour Azure Information Protection inclut une case à cocher pour les correspondances de contenu de document. Quand vous cochez cette case, les données réelles identifiées par les types d’informations sensibles ou vos conditions personnalisées sont également collectées. Il peut s’agir, par exemple, de numéros de carte de crédit trouvés, mais aussi de numéros de sécurité sociale, de passeport et de compte bancaire. Si vous ne souhaitez pas collecter ces données, ne cochez pas cette case.
>
> Ces informations ne figurent pas actuellement dans les rapports, mais vous pouvez les consulter et les récupérer au moyen de requêtes.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Prérequis pour l’analytique Azure Information Protection
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Abonnement Azure qui inclut Log Analytics|Consultez la page de [tarification d’Azure Monitor](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.|
|Client Azure Information Protection (version actuelle en disponibilité générale ou préversion) ou préversion du client d’étiquetage unifié Azure Information Protection|Si vous n’avez pas déjà installé l’une de ces versions du client, vous pouvez les télécharger et les installer à partir du Centre de téléchargement Microsoft :<br /> - [Client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018) <br /> - [Client d’étiquetage unifié Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=57440)|
|Pour le rapport de **découverte et des risques** : <br /><br />- Pour afficher les données à partir de magasins de données locaux, vous avez déployé au moins une instance du scanneur Azure Information Protection (version en disponibilité générale ou préversion) <br /><br />- Pour afficher les données à partir d’ordinateurs Windows 10, ils doivent au minimum avoir la build 1809, vous utilisez Windows Defender Advanced Threat Protection (Windows Defender ATP), et vous avez activé la fonctionnalité d’intégration Azure Information Protection à partir de Windows Defender Security Center|Pour obtenir des instructions d’installation pour le scanneur, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md). Si vous effectuez la mise à niveau à partir d’une version précédente du scanneur, consultez [Mise à niveau du scanneur Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).<br /><br />Pour obtenir des informations sur la configuration et l’utilisation de la fonctionnalité d’intégration Azure Information Protection à partir de Windows Defender Security Center, consultez [Vue d’ensemble de la protection des informations dans Windows](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview).|

### <a name="permissions-required-for-azure-information-protection-analytics"></a>Autorisations requises pour l’analytique Azure Information Protection

Caractéristique propre à l’analytique Azure Information Protection, après que vous avez configuré votre espace de travail Azure Log Analytics, vous pouvez utiliser le rôle Administrateur d’Azure AD de Lecteur Sécurité comme alternative aux autres rôles Azure AD qui prennent en charge la gestion d’Azure Information Protection dans le portail Azure.

Comme cette fonctionnalité utilise Azure Monitoring, le contrôle d’accès en fonction du rôle (RBAC) pour Azure contrôle également l’accès à votre espace de travail. Vous avez donc besoin d’un rôle Azure ainsi que d’un rôle Administrateur d’Azure AD pour gérer l’analytique Azure Information Protection. Si vous ne connaissez pas les rôles Azure, il peut s’avérer utile de lire [Différences entre les rôles RBAC Azure et les rôles d’administrateur Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#differences-between-azure-rbac-roles-and-azure-ad-administrator-roles).

Détails :

1. Pour accéder au panneau d’analytique d’Azure Information Protection dans le portail Azure, vous devez avoir l’un de ces [rôles d’administrateur Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) :
    
    - Pour créer votre espace de travail Log Analytics ou des requêtes personnalisées, vous avez besoin de l’un des rôles suivants :
    
        - **Administrateur Information Protection**
        - **Administrateur de sécurité**
        - **Administrateur général**
    
    - Pour afficher les données après avoir créé l’espace de travail Log Analytics, vous avez besoin de l’un des rôles suivants :
    
        - **Lecteur Sécurité**
        - **Administrateur Information Protection**
        - **Administrateur de sécurité**
        - **Administrateur général**
    
    > [!NOTE] 
    > Si votre locataire a été migré vers le magasin d’étiquetage unifié, votre compte doit être un compte d’administrateur général ou l’un des rôles répertoriés avec les autorisations pour accéder au Centre de sécurité et de conformité Office 365. [Plus d’informations](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

2. Pour accéder à votre espace de travail Azure Log Analytics, vous devez disposer de l’un des [rôles Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access#managing-access-to-log-analytics-using-azure-permissions) ou [rôles Azure](https://docs.microsoft.com/azure/role-based-access-control/overview#role-assignments) standard :
    
    - Pour créer un espace de travail Log Analytics ou créer des requêtes personnalisées, un des éléments suivants :
    
        - **Contributeur Log Analytics**
        - Rôle Azure : **Propriétaire** ou **Contributeur**
    
    - Pour afficher les données dans un espace de travail Log Analytics après que vous l’avez créé, vous avez besoin de l’un des rôles suivants :
    
        - **Lecteur Log Analytics**
        - Rôle Azure : **Lecteur**

#### <a name="minimum-roles-to-view-the-reports"></a>Rôles minimaux permettant d’afficher les rapports

Une fois que vous avez configuré votre espace de travail pour l’analytique Azure Information Protection, les deux rôles minimaux nécessaires pour afficher les rapports sont les suivants :

- Rôle Administrateur d’Azure AD : **Lecteur Sécurité**
- Rôle Azure : **Lecteur Log Analytics**

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si ce n’est déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](https://portal.azure.com) avec un compte qui possède les [autorisations requises pour l’analytique Azure Information Protection](#permissions-required-for-azure-information-protection-analytics). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options du menu **Gérer**, puis sélectionnez **Configurer l’analytique (préversion)**.

3. Dans le panneau **Azure Information Protection - Log Analytics**, vous pouvez voir une liste des espaces de travail Log Analytics qui sont détenus par votre locataire. Effectuez l'une des opérations suivantes :
    
    - Pour créer un espace de travail Log Analytics : Sélectionnez **Créer un espace de travail** puis, dans le panneau **Espace de travail Log Analytics**, spécifiez les informations demandées.
    
    - Pour utiliser un espace de travail Log Analytics : Sélectionnez l’espace de travail dans la liste.

Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quand l’espace de travail est configuré, vous êtes prêt à afficher les rapports.

## <a name="how-to-view-the-reports"></a>Comment afficher les rapports

Dans le panneau Azure Information Protection, recherchez les options du menu **Tableaux de bord**, puis sélectionnez l’une des options suivantes :

- **Rapport d’utilisation (préversion)**  : Utilisez ce rapport pour voir comment vos étiquettes sont utilisées. 

- **Journaux d’activité (préversion)**  : Utilisez ce rapport pour voir les actions d’étiquetage effectuées par les utilisateurs sur les appareils et les chemins de fichiers.
    
    Ce rapport comporte une option **Colonnes** qui permet d’afficher plus d’informations sur l’activité que l’affichage par défaut.

- **Découverte de données (préversion)**  : Utilisez ce rapport pour voir des informations sur les fichiers détectés par les scanneurs ou Windows Defender ATP.

> [!NOTE]
> Les caractères non-ASCII dans les chemins et les noms de fichiers sont remplacés par des points d’interrogation (**?**) quand les paramètres régionaux du système d’exploitation d’envoi sont configurés en anglais. Il s’agit d’un problème connu.

## <a name="how-to-modify-the-reports"></a>Comment modifier les rapports

Sélectionnez l’icône de requête dans le tableau de bord pour ouvrir un panneau **Recherche dans les journaux** : 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


Les données consignées pour Azure Information Protection sont stockées dans la table suivante : **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Étapes suivantes
Après avoir examiné les informations contenues dans les rapports, vous pouvez décider d’apporter des modifications à votre stratégie Azure Information Protection. Pour obtenir des instructions, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).
