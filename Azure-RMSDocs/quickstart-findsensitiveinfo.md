---
title: 'Démarrage rapide : rechercher les informations sensibles à l’aide du scanneur Azure Information Protection'
description: Utilisez le scanneur Azure Information Protection pour rechercher les informations sensibles consignées dans les fichiers stockés localement.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 6cb4739d0da222f8748c4f4684290b7193093bcc
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960441"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Démarrage rapide : Rechercher les informations sensibles dans des fichiers stockés localement

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Lors de ce démarrage rapide, vous autoriserez SharePoint à permettre l’analyse, et vous installerez et configurerez le scanneur Azure Information Protection pour trouver des informations sensibles dans vos fichiers stockés dans un magasin de données local. Par exemple, un dossier local, un partage réseau ou SharePoint Server.

> [!NOTE]
> Vous pouvez utiliser ce guide de démarrage rapide avec la version en disponibilité générale actuelle du client Azure Information Protection (classique) ou la version en disponibilité générale du client d’étiquetage unifié Azure Information Protection, qui inclut une préversion du scanneur.
>  
> Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client).

Cette configuration prend moins de 15 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. L’un des clients Azure Information Protection suivants est installé sur votre ordinateur :
    
    - Le client classique : Pour installer ce client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection.exe** depuis la page Azure Information Protection.
    
    - Le client d’étiquetage unifié : Pour installer ce client, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et téléchargez **AzInfoProtection_UL.exe** depuis la page Azure Information Protection.
    
3. SQL Server Express est également installé sur votre ordinateur.
    
    Si cette édition SQL Server n’est pas déjà installée, vous pouvez la télécharger à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) et sélectionner une installation de base.

4. Votre compte de domaine est synchronisé avec Azure AD.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

5. Accès aux autorisations de stratégie SharePoint si vous choisissez d’autoriser une analyse SharePoint.

## <a name="prepare-a-test-folder-and-file"></a>Préparer un dossier et un fichier de test

Pour effectuer un test initial afin de confirmer que le scanneur fonctionne :

1. Créez un dossier local sur votre ordinateur. Par exemple, **TestScanner** sur votre lecteur C local.

2. Créez et enregistrez un document Word dans ce dossier, contenant le texte **Carte de crédit : 4242-4242-4242-4242**.

## <a name="permission-users-to-scan-sharepoint-repositories"></a>Autoriser les utilisateurs à analyser des référentiels SharePoint

Vous pouvez utiliser le scanneur dans tous les référentiels SharePoint en spécifiant l’URL du site. Azure Information Protection découvrira tous les sites sous cette URL et les analysera.

Pour activer les analyses des référentiels, ajoutez les autorisations SharePoint suivantes pour l’utilisateur que vous souhaitez utiliser pour l’analyse :

1. Ouvrez SharePoint et sélectionnez **Stratégie d’autorisation**, puis sélectionnez **Ajouter un niveau de stratégie d’autorisation**. 

    ![Créer un niveau de stratégie d’autorisation pour un utilisateur spécifique](./media/aip-quick-set-sp-permissions.png)


2. Sous **Autorisations de collection de sites**, sélectionnez l’option **Auditeur du collecteur de sites**.   

3. Sous **Autorisations**, sélectionnez **Accorder** pour l’option **Afficher les pages de l’application** et **enregistrez** vos modifications.  

    ![Sélectionner les options Auditeur du collecteur de sites pour un utilisateur spécifique](./media/aip-quick-set-site-permissions.png)

4. Après avoir confirmé vos modifications, cliquez sur **OK** dans la notice **Stratégie de l’application web** qui s’ouvre,   

5. Dans la page **Ajouter des utilisateurs**, ajoutez l’utilisateur que vous souhaitez utiliser pour l’analyse dans le champ **Choisir des utilisateurs**. Sous **Choisir des autorisations**, sélectionnez l’option **Collection de sites**, puis cliquez sur **Terminer** pour appliquer les autorisations créées à l’utilisateur ajouté ou sélectionné. 

    ![Ajouter un utilisateur à de nouvelles options d’autorisation](./media/aip-quick-set-user-permissions.png)

## <a name="configure-a-profile-for-the-scanner"></a>Configurer un profil pour le scanneur

Avant d’installer le scanneur, créez un profil pour celui-ci dans le portail Azure. Ce profil contient les paramètres du scanneur et les emplacements des référentiels de données à analyser.

1. Ouvrez une nouvelle fenêtre de navigateur, puis [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.
    
2. Recherchez les options du **Scanneur** dans le volet de gauche et sélectionnez **Profils**.

3. Dans le volet **Azure Information Protection - Profils**, sélectionnez **Ajouter** :
    
    ![Ajouter un profil pour le scanneur Azure Information Protection](./media/scanner-add-profile.png)

4. Dans le volet **Ajouter un nouveau profil**, donnez un nom au scanneur utilisé pour identifier ses paramètres de configuration et référentiels de données à analyser. Par exemple, pour ce démarrage rapide, vous pouvez spécifier **Démarrage rapide**. Lorsque vous installerez le scanneur ultérieurement, vous devrez spécifier le même nom de profil.
    
    Si vous le souhaitez, entrez une description des raisons administratives, pour vous aider à identifier le nom de profil du scanneur.

5. Recherchez la section **Application de la stratégie**, dans laquelle pour ce démarrage rapide, vous allez sélectionner un seul paramètre : Pour **Appliquer**, sélectionnez **Désactivé**. Puis sélectionnez **Enregistrer** mais ne fermez pas le volet.
    
    Les paramètres configurent le scanneur pour une détection à usage unique de tous les fichiers dans vos référentiels de données spécifiés. Cette analyse recherche tous les types connus d’informations sensibles et ne nécessite aucune configuration préalable de vos étiquettes Azure Information Protection ou paramètres de stratégie.

6. Maintenant que le profil est créé et enregistré, vous pouvez revenir à l’option **Configurer des référentiels** pour spécifier votre dossier local en tant que magasin de données à analyser.
    
    Toujours dans le volet **Ajouter un nouveau profil**, sélectionnez **Configurer les référentiels** pour ouvrir le volet **Référentiels** :
    
    ![Configurer des référentiels de données pour le scanneur Azure Information Protection](./media/scanner-repositories-bar.png)

7. Dans le volet **Référentiels**, sélectionnez **Ajouter** :
    
    ![Ajouter un référentiel de données pour le scanneur Azure Information Protection](./media/scanner-repository-add.png)

8. Dans le volet **Référentiel**, spécifiez votre dossier local que vous avez créé dans la première étape. Par exemple : `C:\TestScanner`
    
    Pour les autres paramètres de ce volet, ne les modifiez pas, mais conservez-les comme **profil par défaut**. Cela signifie que le référentiel de données hérite des paramètres du profil de scanneur. 
    
    Sélectionnez **Enregistrer**.

9. De retour dans le volet **Azure Information Protection - Profils**, votre nom de profil est maintenant répertorié, avec la colonne **PLANIFICATION** affichant **Manuel** et la colonne **APPLIQUER** étant vide. 
    
    La colonne **NŒUDS** affiche **0** parce que vous n’avez pas encore installé le scanneur pour ce profil.

Vous pouvez maintenant installer le scanneur avec le profil de scanneur que vous venez de créer.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Ouvrez une session PowerShell avec l’option **Exécuter en tant qu’administrateur**.

2. Utilisez la commande suivante pour installer le scanneur, en spécifiant le nom de votre ordinateur et le nom du profil que vous avez enregistré dans le portail Azure :
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS -Profile <profile name>
    
    Lorsque vous y êtes invité, fournissez vos propres informations d’identification pour le scanneur au format \<domain\user name>, puis saisissez votre mot de passe. 

## <a name="start-the-scan-and-confirm-it-finished"></a>Démarrer l’analyse et confirmer la fin de l’opération

1. Dans le portail Azure, actualisez le volet **Azure Information Protection - Profils** et la colonne **NŒUDS** doit maintenant afficher **1**.

2. Sélectionnez votre nom de profil, puis l’option **Analyser maintenant** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)
    
    Si cette option n’est pas disponible une fois que vous avez sélectionné votre profil, le scanneur n’est pas connecté à Azure Information Protection. Vérifiez votre configuration et votre connectivité Internet.

3. Comme il n’y a qu’un petit fichier à examiner, cette analyse de test initiale sera très rapide :
    
    Attendez que des valeurs s’affichent dans les colonnes **RÉSULTATS DE LA DERNIÈRE ANALYSE** et **DERNIÈRE ANALYSE (HEURE DE FIN)** .
    
    Sinon, pour le scanneur du client classique uniquement : Consultez le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Confirmer l’ID d’événement d’information **911** pour le processus **MSIP.Scanneur**. L’entrée du journal d’événements contient également un résumé des résultats de l’analyse.

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

2. Redémarrez le scanneur à nouveau : Dans le volet **Azure Information Protection - Profils**, assurez-vous que votre profil est sélectionné, puis sélectionnez l’option **Analyser maintenant** :
    
    ![Lancer l’analyse pour le scanneur Azure Information Protection](./media/scanner-scan-now.png)

3. Affichez les nouveaux résultats lorsque l’analyse est terminée. 
    
    La durée de cette analyse varie selon le nombre de fichiers figurant dans votre magasin de données, la taille de ces fichiers et le type de fichier. 

## <a name="clean-up-resources"></a>Nettoyer les ressources

Dans un environnement de production, vous exécutez le scanneur sur un serveur Windows, à l’aide d’un compte de service qui s’authentifie de façon silencieuse auprès du service Azure Information Protection. Vous utilisez également une version SQL Server de niveau entreprise et spécifiez probablement plusieurs référentiels de données. 

Pour nettoyer les ressources et les préparer pour ce déploiement de production, dans votre session PowerShell, exécutez la commande suivante pour désinstaller le scanneur :

    Uninstall-AIPScanner

Puis redémarrez votre ordinateur.

Cette commande ne supprime pas les éléments suivants et vous devez les supprimer manuellement si vous ne souhaitez pas les conserver après ce démarrage rapide :

- La base de données SQL Server qui a été créée en exécutant l’applet de commande Install-AIPScanner lors de l’installation du scanneur Azure Information Protection :
    - Pour le client classique : **AIPScanner_\<profile>**
    - Pour le client d’étiquetage unifié : **AIPScannerUL_\<profile_name>**

- Les rapports d’analyse situés sous %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- Les droits d’utilisateur **Ouvrir une session en tant que service** qui ont été accordés à votre compte de domaine pour votre ordinateur local.


## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut la configuration minimale vous permettant de constater rapidement comment le scanneur peut trouver des informations sensibles dans des magasins de données locaux. Si vous êtes prêt à installer le scanneur dans un environnement de production, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

Si vous souhaitez classifier et protéger les fichiers contenant des informations sensibles, vous devez configurer des étiquettes pour la classification et la protection automatiques :

- Pour le client classique :
    - [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md)
    - [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md)

- Pour le client d’étiquetage unifié :
    - [Appliquer automatiquement une étiquette sensibilité au contenu](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)
    - [Restriction de l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/encryption-sensitivity-labels)
