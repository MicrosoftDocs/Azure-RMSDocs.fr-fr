---
title: Tutoriel - Découverte de votre contenu sensible avec le scanneur Azure Information Protection (AIP)
description: Utilisez le scanneur Azure Information Protection (AIP) pour localiser les référentiels qui peuvent être menacés. Explorez ensuite les partages de fichiers pour y rechercher du contenu sensible.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: b55178f6cd0bef2fa14eb7fcf9ecaefa3ea75f7a
ms.sourcegitcommit: df6ee1aca02e089e3a72006ecf0747f14213979c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503670"
---
# <a name="tutorial-discovering-your-sensitive-content-with-the-azure-information-protection-aip-scanner"></a>Tutoriel : Découverte de votre contenu sensible avec le scanneur Azure Information Protection (AIP)

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client d’étiquetage unifié Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Le client Azure Information Protection fournit un analyseur local qui permet aux administrateurs système d’analyser les réseaux et les référentiels de fichiers locaux à la recherche de contenu sensible. 

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un travail d’analyse du réseau et rechercher les référentiels à risque
> * Ajouter tous les référentiels à risque trouvés à un travail d’analyse de contenu
> * Analyser vos partages de contenu à la recherche de contenu sensible et comprendre les résultats trouvés

> [!NOTE]
> La découverte du réseau est disponible seulement à partir de la version [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) du client d’étiquetage unifié, qui est actuellement en préversion. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.
>
> Si vous n’avez pas installé cette version du client et du scanneur, passez en revue les [prérequis du tutoriel](#tutorial-prerequisites), puis passez directement à [Définir et exécuter votre travail d’analyse de contenu](#define-and-run-your-content-scan-job).


**Temps nécessaire :** Vous pouvez terminer cette configuration en 15 minutes.

## <a name="tutorial-prerequisites"></a>Configuration requise pour le didacticiel

|Condition requise  |Description  |
|---------|---------|
|**Un abonnement avec prise en charge**     |  Il vous faut un abonnement Azure comportant [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br /><br />Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.       |
|**Accès administrateur au portail Azure** |Vérifiez que vous pouvez vous connecter au [portail Azure](https://portal.azure.com/) avec un compte d’administrateur pris en charge et que la protection est activée. Les comptes d’administrateur pris en charge sont les suivants : <br /><br />- **Administrateur de conformité**<br />- **Administrateur des données de conformité**<br />- **Administrateur de la sécurité**<br />- **Administrateur général**   |
|**Client, scanneur et service de découverte du réseau AIP**   |   Pour suivre la totalité de ce tutoriel, vous devez avoir installé le client d’étiquetage unifiés et le scanneur Azure Information Protection ainsi que le service de découverte du réseau (préversion publique). <br /><br />Pour plus d’informations, consultez : <br /><br />- [Démarrage rapide : Déploiement du client d’étiquetage unifié Azure Information Protection (AIP)](quickstart-deploy-client.md) <br />- [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection](tutorial-install-scanner.md) |
|**Un travail d’analyse de contenu** | Veillez à avoir un travail d’analyse de contenu de base que vous pouvez utiliser pour le test. Vous en avez peut-être créé un quand vous avez [installé votre scanneur](tutorial-install-scanner.md).<br /><br />Si vous devez en créer un maintenant, vous pouvez utiliser les instructions de [Configurer Azure Information Protection dans le portail Azure](tutorial-install-scanner.md#configure-azure-information-protection-in-the-azure-portal). Si vous avez un travail d’analyse de contenu simple, revenez ici pour suivre ce tutoriel. |
|**SQL Server**     | Pour exécuter le scanneur, SQL Server doit être installé sur la machine du scanneur. <br /><br /> Pour l’installer, accédez à la [page de téléchargement de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads), puis sélectionnez **Télécharger maintenant** sous l’option d’installation que vous voulez utiliser. Dans le programme d’installation, sélectionnez le type d’installation **De base**. <br /><br />**Remarque** : Nous vous recommandons d’installer SQL Server Entreprise pour les environnements de production et l’édition Express seulement pour les tests.    |
|**Compte Active Directory Azure**     |  Quand vous utilisez un environnement standard connecté au cloud, votre compte de domaine doit être synchronisé avec [Azure Active Directory](https://azure.microsoft.com/services/active-directory/). Ce n’est pas nécessaire si vous travaillez hors connexion. <br /><br />Si vous avez un doute sur votre compte, contactez un de vos administrateurs système pour vérifier l’état de la synchronisation. Pour plus d’informations, consultez [Déploiement du scanneur avec d’autres configurations](deploy-aip-scanner-prereqs.md#deploying-the-scanner-with-alternative-configurations).  |
|**Des étiquettes de sensibilité et une stratégie publiée** |Vous devez avoir créé des étiquettes de sensibilité et publié une stratégie avec au moins une étiquette dans le Centre d’administration d’étiquetage, pour le compte de service du scanneur. <br /><br />Configurez des étiquettes de sensibilité dans le Centre d’administration d’étiquetage, notamment le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité Microsoft 365. Pour plus d’informations, consultez la [documentation Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels). |
| | | 


Quand vous êtes prêt, poursuivez avec [Créer un travail d’analyse du réseau](#create-a-network-scan-job).

## <a name="create-a-network-scan-job"></a>Créer un travail d’analyse du réseau

Créez un travail d’analyse du réseau pour analyser une adresse IP ou une plage d’adresses IP spécifiées pour y rechercher les référentiels à risque.

> [!NOTE]
> Cette fonctionnalité est disponible uniquement à compter de la version [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) et est actuellement en préversion. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.
> 

**Pour créer un travail d’analyse du réseau :**

1. Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’[administrateur pris en charge](#tutorial-prerequisites), puis accédez à la zone **Azure Information Protection**.
        
1. Dans le menu **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **Travaux d’analyse du réseau (préversion)** .

1. Sélectionnez :::image type="icon" source="media/i-add.PNG" border="false"::: **Ajouter** pour ajouter un nouveau travail. Dans le volet **Ajouter un nouveau travail d’analyse du réseau**, entrez les informations suivantes :
    
    |Option  |Description  |
    |---------|---------|
    |**Nom du travail d’analyse du réseau** et **Description**     |Entrez un nom explicite, comme `Quickstart`, et une description facultative.         |
    |**Sélectionner le cluster.**     | Sélectionnez le nom de votre cluster dans la liste déroulante.<br /><br /> Par exemple, si vous avez effectué le [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection (AIP)](tutorial-install-scanner.md) et que ce cluster est encore disponible, sélectionnez **Démarrage rapide**.       |
    |**Configurer des plages d’adresses IP à découvrir**     | Sélectionnez la ligne pour ouvrir le volet **Choisir des plages d’adresses IP**. Entrez une adresse IP ou une plage d’adresses IP à analyser. <br /><br />**Remarque** : Veillez à entrer les adresses IP qui sont accessibles à partir de la machine du scanneur.      |
    |**Définir le calendrier**     | Conservez la valeur par défaut, **Une fois**.        |
    |**Définir l’heure de début (UTC)**     |  Calculez l’heure UTC actuelle, en tenant compte de votre fuseau horaire, et définissez l’heure de début pour qu’elle s’exécute dans les 5 minutes à partir de maintenant.     |
    |     |         |

    Exemple : 

    :::image type="content" source="media/qs-tutor/network-scan-job.png" alt-text="Entrer les détails de votre travail d’analyse du réseau":::

1. En haut de la page, sélectionnez :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Enregistrer**.

1. Revenez à la grille :::image type="icon" source="media/qs-tutor/i-network-scan-jobs.png" border="false"::: **Tâches d’analyse du réseau (préversion)** et attendez que votre analyse démarre.

Les données de la grille sont mises à jour à mesure que votre analyse est effectuée. Exemple :

:::image type="content" source="media/qs-tutor/scanned-network.png" alt-text="Travaux d’analyse du réseau actualisés":::

> [!TIP]
> Si votre travail d’analyse du réseau ne s’exécute pas, vérifiez que le [service de découverte du réseau est correctement installé](tutorial-install-scanner.md#install-the-network-discovery-service) sur la machine du scanneur.

Poursuivez avec [Ajouter les référentiels à risque à un travail d’analyse de contenu](#add-risky-repositories-to-a-content-scan-job).

## <a name="add-risky-repositories-to-a-content-scan-job"></a>Ajouter les référentiels à risque à un travail d’analyse de contenu

Une fois votre travail d’analyse du réseau terminé, vous pouvez vérifier s’il existe des référentiels à risque. 

Par exemple, si vous trouvez qu’un référentiel est accessible publiquement à la fois en lecture et en écriture, vous pouvez effectuer une analyse plus poussée et vérifier qu’aucune donnée sensible n’y est stockée.

> [!NOTE]
> Cette fonctionnalité est disponible uniquement à compter de la version [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) et est actuellement en préversion. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.
> 

**Pour ajouter des référentiels à risque à votre travail d’analyse de contenu** :

1. Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’[administrateur pris en charge](#tutorial-prerequisites), puis accédez au volet **Azure Information Protection**.
        
1. Dans le menu **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/qs-tutor/i-repos.png" border="false"::: **Référentiels (préversion)** .

    :::image type="content" source="media/small/risky-repos-small.png" alt-text="Afficher les référentiels trouvés par votre travail d’analyse du réseau" lightbox="media/qs-tutor/risky-repos.png":::

1. Dans la grille située sous les graphiques, recherchez un référentiel qui n’est pas encore géré par le scanneur. Non géré par le scanneur signifie qu’il n’est pas inclus dans un travail d’analyse de contenu et qu’il n’est pas analysé à la recherche de contenu sensible.

    > [!TIP]
    > Par exemple, les référentiels pour lesquels **Accès public effectif** a été trouvé avec la valeur **R** (Read, pour lecture) ou **RW** (Read/Write, pour lecture/écriture) sont disponibles publiquement et peuvent avoir du contenu à risque.
    > 

1. Sélectionnez la ligne puis, au-dessus de la grille, sélectionnez :::image type="icon" source="media/i-add.PNG" border="false"::: **Affecter les éléments sélectionnés**. 

1. Dans le volet **Affecter à un travail d’analyse de contenu** qui apparaît sur la droite, sélectionnez votre travail d’analyse de contenu dans la liste déroulante, puis sélectionnez :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Enregistrer**.

    Exemple :

    :::image type="content" source="media/qs-tutor/assign-content-scan-job.png" alt-text="Affecter un référentiel à risque à un travail d’analyse de contenu":::

Lors de l’exécution suivante de votre travail d’analyse de contenu, celui-ci inclut désormais ce référentiel nouvellement découvert, et il identifie, étiquette, classifie et protège le contenu sensible trouvé, selon ce qui est configuré dans votre stratégie.

Poursuivez avec [Définir et exécuter votre travail d’analyse de contenu](#define-and-run-your-content-scan-job).

## <a name="define-and-run-your-content-scan-job"></a>Définir et exécuter votre travail d’analyse de contenu

Utilisez le travail d’analyse de contenu que vous avez préparé avec les [prérequis du tutoriel](#tutorial-prerequisites) pour analyser votre contenu. 

Si vous n’avez pas encore de travail d’analyse de contenu, suivez [Configurer les paramètres initiaux dans le portail Azure](tutorial-install-scanner.md#configure-initial-scanner-settings-in-the-azure-portal), puis revenez ici pour continuer.


1. Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’[administrateur pris en charge](#tutorial-prerequisites), puis accédez au volet **Azure Information Protection**.
        
1. Dans le menu **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Travaux d’analyse de contenu**, puis sélectionnez votre travail d’analyse de contenu.
 
1. Modifiez les paramètres de votre travail d’analyse de contenu et vérifiez qu’il a un nom explicite et une description facultative. 

    Conservez les valeurs par défaut pour la plupart des paramètres et changez seulement les paramètres suivants :

    -  **Traiter l’étiquetage recommandé comme automatique**. Définissez-le sur **Activé**.
    
    - **Configurer les référentiels**. Vérifiez qu’au moins un référentiel est défini. 
    
        > [!TIP]
        > Si vous avez ajouté des référentiels supplémentaires à votre travail d’analyse de contenu après avoir scanné votre réseau dans [Ajouter des référentiels à risque à un travail d’analyse de contenu](#add-risky-repositories-to-a-content-scan-job), vous pouvez maintenant choisir de les voir listés ici. 

    - **Appliquer**. Définissez-le sur **Activé**.
    
1. Sélectionnez :::image type="icon" source="media/qs-tutor/save-icon.png" border="false"::: **Enregistrer**, puis revenez à la grille :::image type="icon" source="media/i-content-scan-jobs.PNG" border="false"::: **Travaux d’analyse de contenu**.

1. Pour analyser votre contenu, revenez à la zone :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Travaux d’analyse de contenu**, puis sélectionnez votre travail d’analyse de contenu.

    Dans la barre d’outils au-dessus de la grille, sélectionnez :::image type="icon" source="media/i-scan-now.PNG" border="false"::: **Analyser maintenant** pour démarrer l’analyse.

    Une fois l’analyse terminée, poursuivez avec [Afficher les résultats de l’analyse](#view-scan-results).

### <a name="view-scan-results"></a>Afficher les résultats de l’analyse

Une fois l’analyse terminée, consultez les rapports dans la zone **Azure Information Protection > Analytique** dans le portail Azure.

Exemple :

:::image type="content" source="media/qs-tutor/content-scan-job-data-discovery.PNG" alt-text="Rapport de découverte des données d’analytique des résultats du scanneur":::
    
> [!TIP]
> Si vos résultats sont vides et que vous souhaitez exécuter une analyse significative, créez un fichier nommé **Payment info** dans un des référentiels inclus dans votre travail d’analyse de contenu. Enregistrez le fichier avec le contenu suivant :
> 
> **Credit card:** 2384 2328 5436 3489
>
> Réexécutez votre analyse pour voir la différence dans les résultats.
> 

Pour plus d’informations, consultez [Rapports centralisés pour Azure Information Protection (préversion publique)](reports-aip.md).

#### <a name="local-scanner-reports"></a>Rapports locaux du scanneur

Les journaux sont également stockés localement dans le **répertoire %localappdata%\Microsoft\MSIP\Scanner\Reports** sur la machine du scanneur et incluent :

|Type  |Description  |
|---------|---------|
|**Fichiers de récapitulatif .txt**     |  Inclut la durée de l’analyse, le nombre de fichiers analysés et le nombre de fichiers pour lesquels une correspondance avec les types d’informations a été trouvée.       |
|**Fichiers de détails .csv.**     | Contient des descriptions détaillées pour chaque fichier analysé. Le répertoire peut contenir jusqu’à 60 rapports pour chaque cycle d’analyse.         |
|     |         |

## <a name="next-steps"></a>Étapes suivantes

Si vous voulez suivre d’autres tutoriels, consultez :

- [Tutoriel : Empêcher les partages inappropriés avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md)

**Voir aussi :**

- [Qu’est-ce que le scanneur d’étiquetage unifié Azure Information Protection ?](deploy-aip-scanner.md)
- [Prérequis pour l’installation et le déploiement du scanneur d’étiquetage unifié Azure Information Protection](deploy-aip-scanner-prereqs.md)
- [Configuration et installation du scanneur d’étiquetage unifié Azure Information Protection](deploy-aip-scanner-configure-install.md)
- [Exécution du scanneur Azure Information Protection](deploy-aip-scanner-manage.md)
