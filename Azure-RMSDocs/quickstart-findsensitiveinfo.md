---
title: 'Démarrage rapide : rechercher les informations sensibles à l’aide du scanneur Azure Information Protection'
description: Utilisez le scanneur Azure Information Protection pour rechercher les informations sensibles consignées dans les fichiers stockés localement.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 9678aeed589c1b4d9beee5f304ac9d8fdbd5cbf1
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156715"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Démarrage rapide : Rechercher les informations sensibles dans des fichiers stockés localement

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Dans ce démarrage rapide, vous allez installer et configurer le scanneur Azure Information Protection pour trouver les informations sensibles consignées dans les fichiers stockés dans un magasin de données local. Par exemple, un dossier local, un partage réseau ou SharePoint Server.

Remarque : Ce démarrage rapide utilise la version en disponibilité générale actuelle du scanneur, qui utilise le portail Azure pour la configuration au lieu des cmdlets PowerShell utilisées par les versions précédentes.

Cette configuration prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Le client Azure Information Protection est installé sur votre ordinateur. 
    
    Pour installer le client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection.exe** sur la page Azure Information Protection.
    
3. SQL Server Express est également installé sur votre ordinateur.
    
    Si cette édition SQL Server n’est pas déjà installée, vous pouvez la télécharger à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) et sélectionner une installation de base.

4. Votre compte de domaine est synchronisé avec Azure AD.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="prepare-a-test-folder-and-file"></a>Préparer un dossier et un fichier de test

Pour effectuer un test initial afin de confirmer que le scanneur fonctionne :

1. Créez un dossier local sur votre ordinateur. Par exemple, **TestScanner** sur votre lecteur C local.

2. Créez et enregistrez un document Word dans ce dossier, contenant le texte **4242-4242-4242-4242** (un numéro de carte de crédit connu pour le test).

## <a name="configure-a-profile-for-the-scanner"></a>Configurer un profil pour le scanneur

Avant d’installer le scanneur, créez un profil pour celui-ci dans le portail Azure. Ce profil contient les paramètres du scanneur et les emplacements des référentiels de données à analyser.

1. Ouvrez une nouvelle fenêtre de navigateur, puis [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
2. Recherchez les options de menu **Scanneur**, puis sélectionnez **Profils**.

3. Dans le panneau **Azure Information Protection - Profils**, sélectionnez **Ajouter** :
    
    ![Ajouter un profil pour le scanneur Azure Information Protection](./media/scanner-add-profile.png)

4. Dans le panneau **Ajouter un nouveau profil**, donnez un nom au scanneur utilisé pour identifier ses paramètres de configuration et référentiels de données à analyser. Par exemple, pour ce démarrage rapide, vous pouvez spécifier **Démarrage rapide**. Lorsque vous installerez le scanneur ultérieurement, vous devrez spécifier le même nom de profil.
    
    Si vous le souhaitez, entrez une description des raisons administratives, pour vous aider à identifier le nom de profil du scanneur.

5. Pour ce démarrage rapide, sélectionnez un seul paramètre : Pour **Application des stratégies**, sélectionnez **Désactivé**. Puis sélectionnez **Enregistrer** mais ne fermez pas le panneau.
    
    Les paramètres configurent le scanneur pour une détection à usage unique de tous les fichiers dans vos référentiels de données spécifiés. Cette analyse recherche tous les types connus d’informations sensibles et ne nécessite aucune configuration préalable de vos étiquettes Azure Information Protection ou paramètres de stratégie

6. Maintenant que le profil est créé et enregistré, vous pouvez revenir à l’option **Configurer des référentiels** pour spécifier votre dossier local en tant que magasin de données à analyser.
    
    Toujours dans le panneau **Ajouter un nouveau profil**, sélectionnez **Configurer des référentiels** pour ouvrir le panneau **Référentiels** :
    
    ![Configurer des référentiels de données pour le scanneur Azure Information Protection](./media/scanner-repositories-bar.png)

7. Dans le panneau **Référentiels**, sélectionnez **Ajouter** :
    
    ![Ajouter un référentiel de données pour le scanneur Azure Information Protection](./media/scanner-repository-add.png)

8. Dans le panneau **Référentiel**, spécifiez votre dossier local que vous avez créé dans la première étape. Par exemple : `C:\TestScanner`
    
    Pour les autres paramètres de ce panneau, ne les modifiez pas, mais conservez-les comme **profil par défaut**. Cela signifie que le référentiel de données hérite des paramètres du profil de scanneur. 
    
    Sélectionnez **Enregistrer**.

9. Vous pouvez maintenant fermer le panneau **Ajouter un nouveau profil**. Votre nom de profil apparaît dans le panneau **Azure Information Protection - Profils**, la colonne **Planification** affichant **Manuel** et la colonne **Appliquer** étant vide.

Vous pouvez maintenant installer le scanneur avec le profil de scanneur que vous venez de créer.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Ouvrez une session PowerShell avec l’option **Exécuter en tant qu’administrateur**.

2. Utilisez la commande suivante pour installer le scanneur, en spécifiant le nom de votre ordinateur et le nom du profil que vous avez enregistré dans le portail Azure :
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    Lorsque vous y êtes invité, fournissez vos propres informations d’identification pour le scanneur au format \<domain\user name>, puis saisissez votre mot de passe. 

## <a name="start-the-scan-and-confirm-it-finished"></a>Démarrer l’analyse et confirmer la fin de l’opération

1. De retour dans le portail Azure, revenez à Azure Information Protection pour démarrer le scanneur. Dans l’option de menu **Scanneur**, sélectionnez **Nœuds**. Sélectionnez le nom de votre ordinateur, puis l’option **Analyser maintenant** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

2. Comme il n’y a qu’un petit fichier à examiner, cette analyse de test initiale sera très rapide :
    
    - Dans le panneau **Azure Information Protection - Nœuds**, la valeur de la colonne **ÉTAT** passe de **Analyse** à **Inactif**.
    
    - Vous pouvez aussi consulter le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Confirmer l’ID d’événement d’information **911** pour le processus **MSIP.Scanneur**. L’entrée du journal d’événements contient également un résumé des résultats de l’analyse.

## <a name="see-detailed-results"></a>Afficher les résultats détaillés

À l’aide de l’Explorateur de fichiers, recherchez les rapports d’analyse sous %*localappdata*% \Microsoft\MSIP\Scanner\Reports. Ouvrez le fichier de rapport détaillé au format .csv.

Dans Excel, les deux premières colonnes affichent le nom du répertoire du magasin de données et du fichier. En examinant les colonnes, vous verrez une colonne intitulée **Information Type Name** (Nom du type d’informations), qui est la colonne qui vous intéresse le plus. Pour notre test initial, elle affiche la valeur **Credit Card Number** (Numéro de carte de crédit), un des nombreux types d’informations sensibles que le scanneur peut trouver.

## <a name="scan-your-own-data"></a>Analyser vos propres données

1. Modifiez votre profil du scanneur et ajoutez un nouveau référentiel de données, cette fois en spécifiant vos propres magasin de données locaux dans lesquels vous souhaitez rechercher des informations sensibles. 
    
    Vous pouvez spécifier un dossier local, un partage réseau (chemin UNC) ou une URL SharePoint Server pour un site SharePoint ou une bibliothèque. 
    
    - Exemple pour un dossier local :
        
            D:\Data\Finance
    
    - Exemple pour un partage réseau
        
            \\NAS\HR
    
    - Exemple pour un dossier SharePoint :
        
            http://sp2016/Shared Documents

2. Redémarrez le scanneur à nouveau : À partir de l’option de menu **Scanneur**, sélectionnez **Nœuds**, sélectionnez le nom de votre ordinateur, puis l’option **Analyser maintenant** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

3. Affichez les nouveaux résultats lorsque l’analyse est terminée. 
    
    La durée de cette analyse varie selon le nombre de fichiers figurant dans votre magasin de données, la taille de ces fichiers et le type de fichier. 

## <a name="clean-up-resources"></a>Nettoyer les ressources

Dans un environnement de production, vous exécutez le scanneur sur un serveur Windows, à l’aide d’un compte de service qui s’authentifie de façon silencieuse auprès du service Azure Information Protection. Vous utilisez également une version SQL Server de niveau entreprise et spécifiez probablement plusieurs référentiels de données. 

Pour nettoyer les ressources et les préparer pour ce déploiement de production, dans votre session PowerShell, exécutez la commande suivante pour désinstaller le scanneur :

    Uninstall-AIPScanner

Puis redémarrez votre ordinateur.

Cette commande ne supprime pas les éléments suivants et vous devez les supprimer manuellement si vous ne souhaitez pas les conserver après ce démarrage rapide :

- La base de données SQL Server nommée **AIPScanner_\<profil>** qui a été créée en exécutant la cmdlet Install-AIPScanner lors de l’installation du scanneur Azure Information Protection. 

- Les rapports d’analyse situés sous %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- Les droits d’utilisateur **Ouvrir une session en tant que service** qui ont été accordés à votre compte de domaine pour votre ordinateur local.


## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut la configuration minimale vous permettant de constater rapidement comment le scanneur peut trouver des informations sensibles dans un partage réseau. Si vous êtes prêt à installer le scanneur dans un environnement de production, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

Si vous souhaitez classer et protéger les fichiers contenant des informations sensibles, vous devez configurer des étiquettes Azure Information Protection pour la classification et la protection automatiques :

- [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md)

- [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md)
