---
title: 'Démarrage rapide : Rechercher les informations sensibles dans des fichiers à l’aide du scanneur Azure Information Protection – AIP'
description: Utilisez le scanneur Azure Information Protection pour rechercher les informations sensibles consignées dans les fichiers stockés localement.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 07baee062d994b6efd97084bf0b293adb2d5fb84
ms.sourcegitcommit: 89d2c2595bc7abda9a8b5e505b7dcf963e18c822
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56266010"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Démarrage rapide : Rechercher les informations sensibles dans des fichiers stockés localement

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Dans ce démarrage rapide, vous allez installer et configurer le scanneur Azure Information Protection pour trouver les informations sensibles consignées dans les fichiers stockés dans un magasin de données local. Par exemple, un dossier local, un partage réseau ou SharePoint Server.

Remarque : Ce démarrage rapide utilise la version en disponibilité générale actuelle du scanneur et non pas la préversion qui utilise le portail Azure pour la configuration.

Cette configuration prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

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

## <a name="install-the-scanner"></a>Installer le scanneur

1. Ouvrez une session PowerShell avec l’option **Exécuter en tant qu’administrateur**.

2. Utilisez la commande suivante pour installer le scanneur, en spécifiant le nom de votre ordinateur :
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS
    
    Lorsque vous y êtes invité, fournissez vos propres informations d’identification pour le scanneur au format \<domain\user name>, puis saisissez votre mot de passe. 

## <a name="specify-your-test-data-store"></a>Spécifier votre magasin de données de test

Dans votre session PowerShell, tapez la commande suivante :

    Add-AIPScannerRepository -Path C:\TestScanner

## <a name="configure-the-scanner-to-discover-all-information-types"></a>Configurer le scanneur pour découvrir tous les types d’informations

Dans votre session PowerShell, tapez la commande suivante :

    Set-AIPScannerConfiguration -Enforce Off -Schedule Manual -DiscoverInformationTypes All

Cette commande configure le scanneur pour une détection à usage unique de tous les fichiers dans votre référentiel de données spécifié. Cette analyse recherche tous les types connus d’informations sensibles et ne nécessite aucune configuration préalable de vos étiquettes Azure Information Protection ou paramètres de stratégie.

## <a name="start-the-scan-and-confirm-it-finished"></a>Démarrer l’analyse et confirmer la fin de l’opération

1. Dans votre session PowerShell, tapez la commande suivante pour lancer le scanneur :
    
        Start-AIPScan
    
    Comme il n’y a qu’un petit fichier à examiner, cette analyse de test initiale sera très rapide. 

2. Accédez à votre journal d’événements Windows **Observateur d’événements** > **Applications et services** > **Azure Information Protection**. 
    
    Vérifiez qu’Azure Information Protection affiche l’ID d’événement d’information **911** pour le processus **MSIP. Scanneur**. L’entrée du journal d’événements contient également un résumé des résultats de l’analyse.

## <a name="see-detailed-results"></a>Afficher les résultats détaillés

À l’aide de l’Explorateur de fichiers, recherchez les rapports d’analyse sous %*localappdata*% \Microsoft\MSIP\Scanner\Reports. Ouvrez le fichier de rapport détaillé au format .csv.

Dans Excel, les deux premières colonnes affichent le nom du répertoire du magasin de données et du fichier. En examinant les colonnes, vous verrez une colonne intitulée **Information Type Name** (Nom du type d’informations), qui est la colonne qui vous intéresse le plus. Pour notre test initial, elle affiche la valeur **Credit Card Number** (Numéro de carte de crédit), un des nombreux types d’informations sensibles que le scanneur peut trouver.

## <a name="scan-your-own-data"></a>Analyser vos propres données

1. Exécutez de nouveau Add-AIPScannerRepository, cette fois en spécifiant vos propres magasin de données locaux dans lesquels vous souhaitez rechercher des informations sensibles. 
    
    Vous pouvez spécifier un dossier local, un partage réseau (chemin UNC) ou une URL SharePoint Server pour un site SharePoint ou une bibliothèque. 
    
    - Exemple pour un dossier local :
        
            Add-AIPScannerRepository -Path D:\Data\Finance
    
    - Exemple pour un partage réseau
        
            Add-AIPScannerRepository -Path \\NAS\HR
    
    - Exemple pour un dossier SharePoint :
        
            Add-AIPScannerRepository -Path "http://sp2016/Shared Documents"

2. Redémarrez le scanneur :
    
        Start-AIPScan

3. Affichez les nouveaux résultats lorsque l’analyse est terminée. 
    
    La durée de cette analyse varie selon le nombre de fichiers figurant dans votre magasin de données, la taille de ces fichiers et le type de fichier. 

## <a name="clean-up-resources"></a>Nettoyer les ressources

Dans un environnement de production, vous exécutez le scanneur sur un serveur Windows, à l’aide d’un compte de service qui s’authentifie de façon silencieuse auprès du service Azure Information Protection. Vous utilisez également une version SQL Server de niveau entreprise et spécifiez probablement plusieurs référentiels de données. 

Pour nettoyer les ressources et les préparer pour ce déploiement de production, dans votre session PowerShell, exécutez la commande suivante pour désinstaller le scanneur :

    Uninstall-AIPScanner

Puis redémarrez votre ordinateur.

Cette commande ne supprime pas les éléments suivants et vous devez les supprimer manuellement si vous ne souhaitez pas les conserver après ce démarrage rapide :

- La base de données SQL Server nommée **AzInfoProtection** qui a été créé en exécutant l’applet de commande Install-AIPScanner lors de l’installation du scanneur Azure Information Protection. 

- Les rapports d’analyse situés sous %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- Les droits d’utilisateur **Ouvrir une session en tant que service** qui ont été accordés à votre compte de domaine pour votre ordinateur local.


## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut la configuration minimale vous permettant de constater rapidement comment le scanneur peut trouver des informations sensibles dans un partage réseau. Si vous êtes prêt à installer le scanneur dans un environnement de production, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

Si vous souhaitez classer et protéger les fichiers contenant des informations sensibles, vous devez configurer des étiquettes Azure Information Protection pour la classification et la protection automatiques :

- [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md)

- [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md)
