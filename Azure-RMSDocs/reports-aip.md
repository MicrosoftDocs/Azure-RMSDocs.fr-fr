---
title: Création de rapports centralisée pour Azure Information Protection
description: Guide pratique pour utiliser la création de rapports centralisée pour suivre l’adoption de vos étiquettes Azure Information Protection et identifier les fichiers qui contiennent des informations sensibles
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/27/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: cf951bba3cc74a82e31841986dde9e75ec34a630
ms.sourcegitcommit: e70bb1a02e96d701fd5ae2a25536fa485bbf2e87
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862122"
---
# <a name="central-reporting-for-azure-information-protection"></a>Création de rapports centralisée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et susceptible d’être modifiée. Des données collectées au cours de cette préversion peuvent ne pas être prises en charge quand la fonctionnalité passe en disponibilité générale.


Utilisez l’analytique Azure Information Protection pour la création de rapports centralisée afin de suivre l’adoption de vos étiquettes Azure Information Protection et de superviser l’accès utilisateur aux e-mails et documents étiquetés ainsi que les modifications apportées à leur classification. Vous pouvez également identifier les documents qui contiennent des informations sensibles à protéger.

Les données que vous voyez sont agrégées à partir de vos clients Azure Information Protection, scanneurs Azure Information Protection et [clients qui prennent en charge l’étiquetage unifié](configure-policy-migrate-labels.md#clients-that-support-unified-labeling).

Par exemple, vous serez en mesure de voir ce qui suit :

- À partir du **rapport d’utilisation**, où vous pouvez sélectionner une période de temps :
    
    - Étiquettes qui sont appliquées
    
    - Nombre de documents et d’e-mails étiquetés
    
    - Nombre de documents et d’e-mails protégés
    
    - Nombre d’utilisateurs et nombre d’appareils qui étiquettent des documents et e-mails
    
    - Applications utilisées pour l’étiquetage

- À partir du rapport de **découverte de données** :

    - Fichiers qui se trouvent sur vos référentiels de données analysés
    
    - Fichiers étiquetés et protégés, et emplacement des fichiers en fonction des étiquettes
    
    - Fichiers qui contiennent des informations sensibles pour des catégories connues, telles que les données financières et les informations personnelles, et emplacement des fichiers en fonction de ces catégories
    
Les rapports utilisent [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) pour stocker les données dans un espace de travail qui vous appartient. Si vous êtes familiarisé avec le langage de requête, vous pouvez modifier les requêtes ainsi que créer des rapports et tableaux de bord Power BI. Le tutoriel suivant peut s’avérer utile pour comprendre le langage de requête : [Prise en main du portail Analytics](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal). 

Pour plus d’informations, lisez le billet de blog : [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854).

### <a name="information-collected-and-sent-to-microsoft"></a>Informations collectées et envoyées à Microsoft

Pour générer ces rapports, les points de terminaison envoient les types suivants d’informations à Microsoft :

- Action d’étiquette. Par exemple, définir une étiquette, modifier une étiquette, ajouter ou supprimer la protection, étiquettes automatiques et recommandées.

- ID de locataire de votre organisation.

- ID d’utilisateur (adresse e-mail ou UPN).

- Chemin et nom de fichier des documents qui sont étiquetés.

- Version du client Azure Information Protection.

- Version du système d’exploitation client.

Ces informations sont stockées dans un espace de travail Azure Log Analytics qui vous appartient.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Prérequis pour l’analytique Azure Information Protection
Pour afficher les rapports Azure Information Protection et créer les vôtres, vérifiez que les conditions suivantes sont respectées.

|Condition requise|Plus d’informations|
|---------------|--------------------|
|Abonnement Azure qui inclut Log Analytics|Consultez la page [Tarifs Azure Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si vous ne possédez pas un abonnement Azure ou n’utilisez pas Azure Log Analytics, la page des tarifs inclut un lien pour un essai gratuit.|
|Préversion actuelle du client Azure Information Protection.|Si vous n’avez pas déjà installé la préversion actuelle du client, vous pouvez la télécharger et l’installer à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Pour le rapport de **découverte et des risques** : <br /><br />- Vous avez déployé au moins une instance du scanneur Azure Information Protection (préversion actuelle)|Pour obtenir des instructions d’installation, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md). <br /><br />Si vous effectuez la mise à niveau à partir d’une version précédente du scanneur, consultez [Mise à niveau du scanneur Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|


## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configurer un espace de travail Log Analytics pour les rapports

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options du menu **GÉRER**, puis sélectionnez **Configurer l’analytique (préversion)**.

3. Dans le panneau **Azure Information Protection - Log Analytics**, vous pouvez voir une liste des espaces de travail Log Analytics qui sont détenus par votre locataire. Effectuez l'une des opérations suivantes :
    
    - Pour créer un espace de travail Log Analytics : sélectionnez **Créer un espace de travail** puis, dans le panneau **Espace de travail Log Analytics**, fournissez les informations demandées.
    
    - Pour utiliser un espace de travail Log Analytics existant : sélectionnez l’espace de travail dans la liste.

Si vous avez besoin d’aide pour créer l’espace de travail Log Analytics, consultez [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Quand l’espace de travail est configuré, vous êtes prêt à afficher les rapports.

## <a name="how-to-view-the-reports"></a>Comment afficher les rapports

Dans le panneau Azure Information Protection, recherchez les options du menu **TABLEAUX DE BORD (PRÉVERSION)**, puis sélectionnez l’une des options suivantes :

- **Rapport d’utilisation** : utilisez ce rapport pour voir comment vos étiquettes sont utilisées. 

- **Découverte de données** : utilisez ce rapport pour afficher des informations sur les fichiers détectés par les scanneurs.

## <a name="how-to-modify-the-reports"></a>Comment modifier les rapports

Sélectionnez l’icône de requête dans le tableau de bord pour ouvrir un panneau **Recherche dans les journaux** : 

![Icône Log Analytics pour personnaliser les rapports Azure Information Protection](./media/log-analytics-icon.png)


## <a name="next-steps"></a>Étapes suivantes
Après avoir examiné les informations contenues dans les rapports, vous pouvez décider d’apporter des modifications à votre stratégie Azure Information Protection. Pour obtenir des instructions, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).