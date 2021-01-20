---
title: Tutoriel - Installer le scanneur d’étiquetage unifié Azure Information Protection (AIP)
description: Installez le scanner d’étiquetage unifié Azure Information Protection (AIP) pour découvrir les données sensibles stockées dans vos partages réseau locaux.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 54bb64810e2dc71f6356dfe60c0443dccfb87315
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240867"
---
# <a name="tutorial-installing-the-azure-information-protection-aip-unified-labeling-scanner"></a>Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne** : [Client d’étiquetage unifié Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Ce tutoriel explique comment installer le scanneur local Azure Information Protection (AIP). Le scanneur permet aux administrateurs AIP d’analyser leurs réseaux et leurs partages de contenu pour y rechercher des données sensibles, et d’appliquer des étiquettes de classification et de protection comme configuré dans la stratégie de leur organisation.

**Temps nécessaire** : Vous pouvez effectuer ce tutoriel en 30 minutes.

## <a name="tutorial-prerequisites"></a>Configuration requise pour le didacticiel

Pour installer le scanneur d’étiquetage unifié et suivre ce tutoriel, vous avez besoin des éléments suivants :

|Condition requise  |Description  |
|---------|---------|
|**Un abonnement avec prise en charge**     |  Il vous faut un abonnement Azure comportant [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). <br /><br />Si vous n’avez aucun de ces abonnements, créez un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.       |
|**Accès administrateur au portail Azure** |Vérifiez que vous pouvez vous connecter au [portail Azure](https://portal.azure.com/) avec un des comptes d’administrateur suivants : <br /><br />- **Administrateur de conformité**<br />- **Administrateur des données de conformité**<br />- **Administrateur de la sécurité**<br />- **Administrateur général** |
|**Client installé**    |   Installez le client d’étiquetage unifié AIP sur votre ordinateur pour accéder à l’installation du scanneur. <br /><br />Téléchargez et exécutez **AzInfoProtection_UL.exe** à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). <br /><br />Une fois l’installation terminée, vous pouvez être invité à redémarrer votre ordinateur ou votre logiciel Office. Redémarrez si nécessaire pour continuer. <br /><br />Pour plus d’informations, consultez [Démarrage rapide : Déploiement du client d’étiquetage unifié Azure Information Protection (AIP)](quickstart-deploy-client.md)|
|**SQL Server**     | Pour exécuter le scanneur, SQL Server doit être installé sur la machine du scanneur. <br /><br /> Pour l’installer, accédez à la [page de téléchargement de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads), puis sélectionnez **Télécharger maintenant** sous l’option d’installation que vous voulez utiliser. Dans le programme d’installation, sélectionnez le type d’installation **De base**. <br /><br />**Remarque** : Nous vous recommandons d’installer SQL Server Entreprise pour les environnements de production et l’édition Express seulement pour les environnements de test.       |
|**Compte Active Directory Azure**     |  Quand vous utilisez un environnement standard connecté au cloud, le compte de service de domaine que vous utilisez pour le scanneur doit être synchronisé avec [Azure Active Directory](https://azure.microsoft.com/services/active-directory/). Ce n’est pas nécessaire si vous travaillez hors connexion. <br /><br />Si vous avez un doute sur votre compte, contactez un de vos administrateurs système pour vérifier l’état de la synchronisation.   |
|**Des étiquettes de sensibilité et une stratégie publiée** |Vous devez avoir créé des étiquettes de sensibilité et publié une stratégie avec au moins une étiquette dans le Centre d’administration d’étiquetage, pour le compte de service du scanneur. <br /><br />Configurez des étiquettes de sensibilité dans le Centre d’administration d’étiquetage, notamment le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité Microsoft 365. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels). |
| | |

Une fois que vous avez vérifié vos prérequis, [configurez Azure Information Protection dans le portail Azure](#configure-azure-information-protection-in-the-azure-portal).

## <a name="configure-azure-information-protection-in-the-azure-portal"></a>Configurer Azure Information Protection dans le portail Azure

Azure Information Protection peut ne pas être disponible pour vous dans le portail Azure ou la protection peut ne pas être activée. 

Effectuez une des actions suivantes ou les deux, selon ce qui est nécessaire :

- [Ajouter Azure Information Protection au Portail Azure](#add-azure-information-protection-to-the-azure-portal)
- [Vérifier que la protection est activée](#confirm-that-protection-is-activated)

Ensuite, poursuivez avec [Configurer les paramètres initiaux du scanneur dans le portail Azure](#configure-initial-scanner-settings-in-the-azure-portal).

### <a name="add-azure-information-protection-to-the-azure-portal"></a>Ajouter Azure Information Protection au Portail Azure

1. Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un [compte d’administrateur approprié](#tutorial-prerequisites).

1. Sélectionnez **+ Créer une ressource**. Dans la zone de recherche, recherchez puis sélectionnez **Azure Information Protection**. Sur la page Azure Information Protection, sélectionnez **Créer**, puis à nouveau **Créer**.

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Ajout d’Azure Information Protection au Portail Azure":::

    > [!TIP]
    > Si c’est la première fois que vous effectuez cette étape, une icône **Épingler au tableau de bord** ![icône Épingler au tableau de bord](media/qs-tutor/pin-to-dashboard.png "Icône Épingler au tableau de bord") apparaît à côté du nom du volet. Sélectionnez l’icône d’épingle pour créer une vignette sur votre tableau de bord qui vous permet d’y accéder directement la prochaine fois.

Poursuivez avec [Vérifier que la protection est activée](#confirm-that-protection-is-activated).

### <a name="confirm-that-protection-is-activated"></a>Vérifier que la protection est activée

Si Azure Information Protection est déjà disponible, vérifiez que la protection est activée :

1. Dans la zone Azure Information Protection, sous **Gérer** sur la gauche, sélectionnez **Activation de la protection**.

1. Vérifiez que la protection est activée pour votre locataire. Par exemple :

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="Vérification de l’activation d’AIP":::

Si la protection n’est pas activée, sélectionnez ![Activer AIP](media/qs-tutor/activate.png "Activer AIP") **Activer**. Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

Poursuivez avec [Configurer les paramètres initiaux du scanneur dans le portail Azure](#configure-initial-scanner-settings-in-the-azure-portal).

### <a name="configure-initial-scanner-settings-in-the-azure-portal"></a>Configurer les paramètres initiaux du scanneur dans le portail Azure

Préparez les paramètres initiaux de votre scanneur dans le portail Azure avant d’installer le scanneur sur votre machine.

1. Dans la zone Azure Information Protection, sous **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/i-clusters.png" border="false"::: **Clusters**.

1. Dans la page Clusters, sélectionnez :::image type="icon" source="media/i-add.PNG" border="false"::: **Ajouter** afin de créer un cluster pour gérer votre scanneur.

1. Dans le volet **Ajouter un nouveau cluster** qui s’ouvre à droite, entrez un nom de cluster explicite et une description facultative.

    > [!IMPORTANT]
    > Vous aurez besoin du nom de ce cluster lors de l’installation de votre scanneur.
    > 
    
    Exemple :

    :::image type="content" source="media/qs-tutor/qs-add-new-cluster.png" alt-text="Ajouter un nouveau cluster pour le tutoriel":::

1. Créez un travail d’analyse de contenu initial. Dans le menu **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Travaux d’analyse de contenu**, puis sélectionnez :::image type="icon" source="media/i-add.PNG" border="false"::: **Ajouter**.

1. Dans le volet **Ajouter un nouveau travail d’analyse de contenu**, entrez un nom explicite pour votre travail d’analyse de contenu et une description facultative.

    Ensuite, faites défiler la page jusqu’à **Application de la stratégie**, puis sélectionnez **Désactivé**.

    Quand vous avez terminé, enregistrez vos modifications. 

    Ce travail d’analyse par défaut va rechercher tous les types d’informations sensibles connus.

1. Fermez le volet d’informations de votre travail d’analyse de contenu, puis revenez à la grille :::image type="icon" source="media/i-content-scan-jobs.png" border="false"::: **Travaux d’analyse de contenu**. 

    Dans la nouvelle ligne qui apparaît pour votre travail d’analyse de contenu, dans la colonne **Nom du cluster**, sélectionnez **+ Affecter au cluster**. Ensuite, dans le volet **Affecter au cluster** qui apparaît à droite, sélectionnez votre cluster. 

    :::image type="content" source="media/qs-tutor/assign-cluster-all.png" alt-text="Affecter au cluster":::

Vous êtes maintenant prêt à [installer le scanneur d’étiquetage unifié AIP](#install-the-aip-unified-labeling-scanner).

## <a name="install-the-aip-unified-labeling-scanner"></a>Installer le scanneur d’étiquetage unifié AIP

Une fois que vous avez [configuré les paramètres de base du scanneur dans le portail Azure](#configure-azure-information-protection-in-the-azure-portal), installez le scanneur d’étiquetage unifié sur votre ordinateur client AIP.

1. Sur votre ordinateur client, ouvrez une session PowerShell avec l’option **Exécuter en tant qu’administrateur**.

1. Utilisez la commande suivante pour installer le scanneur. Dans votre commande, spécifiez où vous voulez installer le scanneur ainsi que le nom du [cluster que vous avez créé dans le portail Azure](#configure-initial-scanner-settings-in-the-azure-portal).

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <your SQL installation location>\SQLEXPRESS -Cluster <cluster name>
    ```
    Exemple :

    ```powershell
    Install-AIPScanner -SqlServerInstance localhost\SQLEXPRESS -Cluster Quickstart
    ```

    Quand PowerShell vous invite à entrer vos informations d’identification, entrez le nom d’utilisateur et le mot de passe. 

    Pour le champ **Nom d’utilisateur**, utilisez la syntaxe suivante : `<domain\user name>`. Par exemple : `emea\contososcanner`.

1. Revenez au portail Azure. Dans le menu **Scanneur** sur la gauche, sélectionnez :::image type="icon" source="media/qs-tutor/i-nodes.png" border="false"::: **Nœuds**. 

    Vous devez maintenant voir votre scanneur ajouté à la grille. Exemple :

    :::image type="content" source="media/qs-tutor/qs-post-install-scanner.png" alt-text="Scanneur nouvellement installé affiché dans la grille Nœuds":::

Poursuivez avec [Obtenir un jeton Azure Active Directory pour le scanneur](#get-an-azure-active-directory-token-for-the-scanner) pour permettre à votre compte de service de scanneur de s’exécuter de manière non interactive.

## <a name="get-an-azure-active-directory-token-for-the-scanner"></a>Obtenir un jeton Azure Active Directory pour le scanneur

Effectuez cette procédure quand vous utilisez un environnement standard connecté au cloud pour permettre à l’analyseur de s’authentifier auprès du service AIP, ce qui permet au service de s’exécuter de manière non interactive.

Cette procédure n’est pas nécessaire si vous travaillez en mode hors connexion uniquement.

Pour plus d’informations, consultez [Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection](rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)

**Pour obtenir un jeton Azure AD pour le scanneur** :

1. Dans le portail Azure, créez une application Azure AD pour spécifier un jeton d’accès à des fins d’authentification.

1. Sur la machine de votre scanneur, connectez-vous avec un compte de service de scanneur auquel le droit **Se connecter en local** a été accordé et démarrez une session PowerShell.

1. Démarrez une session PowerShell et exécutez la commande suivante, en utilisant les valeurs copiées depuis votre application Azure AD.

    ```PowerShell
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```

    Exemple :

    ```PowerShell
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds

    Acquired application access token on behalf of CONTOSO\scanner.
    ``` 

    > [!TIP]
    > Si le droit **Se connecter en local** ne peut pas être accordé à votre compte de service de scanneur, utilisez le paramètre **OnBehalfOf** avec **Set-AIPAuthentication** au lieu du paramètre **DelegatedUser**.

Le scanneur a maintenant un jeton pour s’authentifier auprès d’Azure AD. Ce jeton est valide aussi longtemps que ce que vous avez configuré dans Azure Active Directory. Vous devez répéter cette procédure quand le jeton expire.

Poursuivez avec [Installation du service de découverte du réseau facultatif](#install-the-network-discovery-service), qui vous permet d’analyser les référentiels de votre réseau à la recherche de contenu susceptible d’être à risque, puis d’ajouter ces référentiels à un travail d’analyse de contenu.

## <a name="install-the-network-discovery-service"></a>Installer le service de découverte du réseau

À compter de la version [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850) du client d’étiquetage unifié AIP, les administrateurs peuvent utiliser le scanneur AIP pour analyser les référentiels du réseau, puis ajouter les référentiels qui semblent être à risque à un travail d’analyse de contenu.

Les travaux d’analyse du réseau vous aident à comprendre *où* votre contenu peut être à risque, en tentant d’accéder à des référentiels configurés à la fois en tant qu’administrateur et en tant qu’utilisateur public.

Par exemple, si vous trouvez qu’un référentiel est accessible publiquement à la fois en lecture et en écriture, vous pouvez effectuer une analyse plus poussée et vérifier qu’aucune donnée sensible n’y est stockée.

> [!NOTE]
> Cette fonctionnalité est actuellement en PRÉVERSION. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.

**Pour installer le service de découverte du réseau** :

1. Sur la machine du scanneur, ouvrez une session PowerShell en tant qu’administrateur.

1. Définissez les informations d’identification qui doivent être utilisées par AIP lors de l’exécution du service de découverte du réseau, et lors de la simulation d’accès en tant qu’administrateur et en tant qu’utilisateur public. 

    Entrez les informations d’identification pour chaque commande quand vous y êtes invité en utilisant la syntaxe suivante : `domain\user`. Par exemple : `emea\msanchez`

    Exécutez : 

    **Informations d’identification pour exécuter le service de découverte du réseau :**

    ``` PowerShell 
    $serviceacct= Get-Credential 
    ``` 

    **Informations d’identification pour simuler l’accès en tant qu’administrateur** :

    ``` PowerShell 
    $shareadminacct= Get-Credential 
    ``` 

    **Informations d’identification pour simuler l’accès en tant qu’utilisateur public** :

    ``` PowerShell  
    $publicaccount= Get-Credential 
    ``` 

1. Pour installer le service de découverte du réseau, exécutez :

    ```PowerShell
    Install-MIPNetworkDiscovery [-ServiceUserCredentials] <PSCredential> [[-StandardDomainsUserAccount] <PSCredential>] [[-ShareAdminUserAccount] <PSCredential>] [-SqlServerInstance] <String> -Cluster <String> [-WhatIf] [-Confirm] [<CommonParameters>]

    For example:

    ```PowerShell
    Install-MIPNetworkDiscovery -SqlServerInstance SQLSERVER1\SQLEXPRESS -Cluster Quickstart -ServiceUserCredentials $serviceacct  -ShareAdminUserAccount $shareadminacct -StandardDomainsUserAccount $publicaccount
 
    ```

Le système affiche un message de confirmation quand l’installation est terminée.

## <a name="next-steps"></a>Étapes suivantes

Une fois que le scanneur et le service de découverte du réseau sont installés, vous êtes prêt à démarrer l’analyse. 

Pour plus d’informations, consultez [Tutoriel : Découverte de votre contenu sensible avec le scanneur Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md).

> [!TIP]
> Si vous avez installé la [version 2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850), nous vous recommandons d’analyser votre réseau pour découvrir les référentiels dont le contenu peut être à risque. 
>
>Pour rechercher les données sensibles dans vos référentiels à risque, puis classifier et protéger ces données des utilisateurs externes, mettez à jour votre travail d’analyse de contenu avec les informations des référentiels que vous avez trouvés.
>

**Voir aussi** :

- [Qu’est-ce que le scanneur d’étiquetage unifié Azure Information Protection ?](deploy-aip-scanner.md)
- [Prérequis pour l’installation et le déploiement du scanneur d’étiquetage unifié Azure Information Protection](deploy-aip-scanner-prereqs.md)
- [Tutoriel : Empêcher les partages inappropriés avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)
- [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md)