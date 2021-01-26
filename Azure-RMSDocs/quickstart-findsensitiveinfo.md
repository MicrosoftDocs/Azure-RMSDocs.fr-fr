---
title: 'Démarrage rapide : rechercher les informations sensibles à l’aide du scanneur Azure Information Protection'
description: Utilisez le scanneur Azure Information Protection pour rechercher les informations sensibles consignées dans les fichiers stockés localement.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.custom: admin
ms.subservice: aiplabels
ms.openlocfilehash: 19070e1e661718c70b21cd16d76130afed91b17f
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809395"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Démarrage rapide : Rechercher les informations sensibles dans des fichiers stockés localement

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne** : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Dans ce guide de démarrage rapide, vous allez autoriser SharePoint à permettre l’analyse, et installer et configurer le scanneur Azure Information Protection de façon à trouver d’éventuelles données sensibles stockées dans un magasin de données local.

**Temps nécessaire** : Cette configuration prend moins de 15 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

|Condition requise  |Description  |
|---------|---------|
|**Un abonnement avec prise en charge**     |  Il vous faut un abonnement comportant [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). </br></br>Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.       |
|**Client installé**    |   Le client classique ou le client d’étiquetage unifié doit être installé sur votre ordinateur. </br></br>- Pour installer le client d’étiquetage unifié, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018) et téléchargez **AzInfoProtection_UL.exe** sur la page Azure Information Protection. </br>- Pour déployer le client classique AIP, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.       |
|**SQL Server Express**     | SQL Server Express doit être installé sur votre ordinateur. </br></br> Pour l’installer, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/sql-server/sql-server-editions-express) et sélectionnez **Télécharger maintenant** sous l’option Express. Dans le programme d’installation, sélectionnez le type d’installation **De base**.        |
|**Azure AD**     |  Votre compte de domaine doit être synchronisé avec Azure AD. </br></br>Si vous avez un doute sur votre compte, contactez l’un de vos administrateurs système.      |
|**Accès à SharePoint**     | Pour activer une analyse SharePoint, vous devez disposer d’un accès et d’autorisations sur votre stratégie SharePoint. |
| | |

## <a name="prepare-a-test-folder-and-file"></a>Préparer un dossier et un fichier de test

Pour effectuer un test initial afin de confirmer que le scanneur fonctionne :

1. Créez un dossier sur un partage réseau accessible. Par exemple, nommez ce dossier **TestScanner**.

1. Créez et enregistrez un document Word dans ce dossier, contenant le texte **Carte de crédit : 4242-4242-4242-4242**.

## <a name="permission-users-to-scan-sharepoint-repositories"></a>Autoriser les utilisateurs à analyser des référentiels SharePoint

Pour utiliser le scanneur dans tous les référentiels SharePoint, spécifiez l’URL du site. Azure Information Protection découvrira tous les sites présents sous cette URL et les analysera.

Pour activer les analyses des référentiels, ajoutez les autorisations SharePoint suivantes pour l’utilisateur que vous souhaitez utiliser pour l’analyse :

1. Ouvrez SharePoint et sélectionnez **Stratégie d’autorisation**, puis sélectionnez **Ajouter un niveau de stratégie d’autorisation**.

    ![Créer un niveau de stratégie d’autorisation pour un utilisateur spécifique](./media/aip-quick-set-sp-permissions.png)

1. Sous **Autorisations relatives à la collection de sites**, sélectionnez l’option **Auditeur du collecteur de sites**.

1. Sous **Autorisations**, sélectionnez **Accorder** pour l’option **Afficher les pages de l’application** et **enregistrez** vos modifications.  

    ![Sélectionner les options Auditeur du collecteur de sites pour un utilisateur spécifique](./media/aip-quick-set-site-permissions.png)

1. Après avoir confirmé vos modifications, cliquez sur **OK** dans le message **Stratégie de l’application web** qui s’ouvre.

1. Dans la page **Ajouter des utilisateurs**, ajoutez l’utilisateur que vous souhaitez utiliser pour l’analyse dans le champ **Choisir des utilisateurs**. Sous **Choisir des autorisations**, sélectionnez l’option **Collection de sites**, puis cliquez sur **Terminer** pour appliquer les autorisations créées à l’utilisateur ajouté ou sélectionné.

    ![Ajouter un utilisateur à de nouvelles options d’autorisation](./media/aip-quick-set-user-permissions.png)

## <a name="configure-a-profile-for-the-scanner"></a>Configurer un profil pour le scanneur

Avant d’installer le scanneur, créez un profil pour celui-ci dans le portail Azure. Ce profil contient les paramètres du scanneur et les emplacements des référentiels de données à analyser.

1. Ouvrez une nouvelle fenêtre de navigateur, puis [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.

    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

1. Recherchez les options du **Scanneur** dans le volet de gauche et sélectionnez **Profils**.

1. Dans le volet **Azure Information Protection - Profils**, sélectionnez **Ajouter** :

    :::image type="content" source="media/scanner-add-profile.png" alt-text="Ajout d’un profil pour le scanneur Azure Information Protection":::

1. Dans le volet **Ajouter un nouveau profil**, donnez un nom au scanneur utilisé pour identifier ses paramètres de configuration et référentiels de données à analyser. Par exemple, pour ce démarrage rapide, vous pouvez spécifier **Démarrage rapide**. Lorsque vous installerez le scanneur ultérieurement, vous devrez spécifier le même nom de profil.

    Si vous le souhaitez, entrez une description des raisons administratives, pour vous aider à identifier le nom de profil du scanneur.

1. Recherchez la section **Application de la stratégie**, dans laquelle pour ce démarrage rapide, vous allez sélectionner un seul paramètre : Pour **Appliquer**, sélectionnez **Désactivé**. Puis sélectionnez **Enregistrer** mais ne fermez pas le volet.

    Les paramètres configurent le scanneur pour une détection à usage unique de tous les fichiers dans vos référentiels de données spécifiés. Cette analyse recherche tous les types connus d’informations sensibles et ne nécessite aucune configuration préalable de vos étiquettes Azure Information Protection ou paramètres de stratégie.

1. Maintenant que le profil est créé et enregistré, vous pouvez revenir à l’option **Configurer des référentiels** pour spécifier votre dossier réseau en tant que magasin de données à analyser.

    Toujours dans le volet **Ajouter un nouveau profil**, sélectionnez **Configurer les référentiels** pour ouvrir le volet **Référentiels** :

    :::image type="content" source="./media/scanner-repositories-bar.png" alt-text="Configuration de référentiels de données pour le scanneur Azure Information Protection":::

1. Dans le volet **Référentiels**, sélectionnez **Ajouter** :

    :::image type="content" source="media/scanner-repository-add.png" alt-text="Ajout d’un référentiel de données pour le scanneur Azure Information Protection":::

1. Dans le volet **Référentiel**, spécifiez le dossier que vous avez créé plus tôt. Par exemple : `\\server\TestScanner`

    Ne modifiez pas les autres paramètres de ce volet. Conservez les **Paramètres par défaut du profil** ; ainsi, le référentiel de données héritera les paramètres du profil du scanneur.

    Sélectionnez **Enregistrer**.

1. De retour dans le volet **Azure Information Protection - Profils**, votre nom de profil est maintenant répertorié, avec la colonne **PLANIFICATION** affichant **Manuel** et la colonne **APPLIQUER** étant vide.

    La colonne **NŒUDS** affiche **0** parce que vous n’avez pas encore installé le scanneur pour ce profil.

Vous pouvez maintenant installer le scanneur avec le profil que vous avez créé.

## <a name="install-the-scanner"></a>Installer le scanneur

1. Ouvrez une session PowerShell avec l’option **Exécuter en tant qu’administrateur**.

1. Utilisez la commande suivante pour installer le scanneur, en spécifiant le nom de votre partage réseau et le nom du profil que vous avez enregistré dans le portail Azure :

    ```ps
    Install-AIPScanner -SqlServerInstance <your network share name>\SQLEXPRESS -Profile <profile name>
    ```

    Lorsque vous y êtes invité, fournissez vos propres informations d’identification pour le scanneur au format \<domain\user name>, puis saisissez votre mot de passe.

## <a name="start-the-scan-and-confirm-it-finished"></a>Démarrer l’analyse et confirmer la fin de l’opération

1. Dans le portail Azure, actualisez le volet **Azure Information Protection - Profils** et la colonne **NŒUDS** doit maintenant afficher **1**.

1. Sélectionnez votre nom de profil, puis l’option **Analyser maintenant** :

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Lancement de l’analyse du scanneur Azure Information Protection":::

    Si cette option n’est pas disponible une fois que vous avez sélectionné votre profil, le scanneur n’est pas connecté à Azure Information Protection. Vérifiez votre configuration et votre connectivité Internet.

1. Comme il n’y a qu’un petit fichier à examiner, cette analyse de test initiale sera rapide :

    Attendez que des valeurs s’affichent dans les colonnes **RÉSULTATS DE LA DERNIÈRE ANALYSE** et **DERNIÈRE ANALYSE (HEURE DE FIN)** .

> [!TIP]
> Sinon, pour le scanneur du client classique uniquement :
>
> Consultez le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Confirmer l’ID d’événement d’information **911** pour le processus **MSIP.Scanneur**. L’entrée du journal d’événements contient également un résumé des résultats de l’analyse.
>
## <a name="see-detailed-results"></a>Afficher les résultats détaillés

À l’aide de l’Explorateur de fichiers, recherchez les rapports du scanneur dans **%*localappdata*%\Microsoft\MSIP\Scanner\Reports**. Ouvrez le fichier de rapport détaillé au format **.csv**.

Dans Excel :

- Les deux premières colonnes indiquent le répertoire du magasin de données et le nom du fichier.
- En examinant les colonnes, vous verrez une colonne intitulée **Information Type Name** (Nom du type d’informations), qui est la colonne qui vous intéresse le plus.

    Pour notre test initial, elle affiche la valeur **Credit Card Number** (Numéro de carte de crédit), un des nombreux types d’informations sensibles que le scanneur peut trouver.

## <a name="scan-your-own-data"></a>Analyser vos propres données

1. Modifiez votre profil du scanneur et ajoutez un nouveau référentiel de données, cette fois en spécifiant vos propres magasin de données locaux dans lesquels vous souhaitez rechercher des informations sensibles.

    Indiquez un partage réseau (chemin UNC) ou une URL SharePoint Server pour un site ou une bibliothèque SharePoint.

    Par exemple :

    - **Pour un partage réseau** : `\\NAS\HR`
    - **Pour un dossier SharePoint** : `http://sp2016/Shared Documents`

1. Redémarrez à nouveau le scanneur.

    Dans le volet **Azure Information Protection - Profils**, assurez-vous que votre profil est sélectionné, puis sélectionnez l’option **Analyser maintenant** :

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Lancement de l’analyse du scanneur Azure Information Protection":::

1. Affichez les nouveaux résultats lorsque l’analyse est terminée.

    La durée de cette analyse varie selon le nombre de fichiers figurant dans votre magasin de données, la taille de ces fichiers et le type de fichier.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Dans un environnement de production, vous exécutez le scanneur sur un serveur Windows, à l’aide d’un compte de service qui s’authentifie de façon silencieuse auprès du service Azure Information Protection. Vous utilisez également une version SQL Server de niveau entreprise et spécifiez probablement plusieurs référentiels de données.

Pour nettoyer les ressources et préparer votre système à un déploiement en production, exécutez la commande suivante dans votre session PowerShell afin de désinstaller le scanneur :

```ps
Uninstall-AIPScanner
```

Puis redémarrez votre ordinateur.

Cette commande ne supprime pas les éléments suivants et vous devez les supprimer manuellement si vous ne souhaitez pas les conserver après ce démarrage rapide :

- La base de données SQL Server qui a été créée en exécutant l’applet de commande Install-AIPScanner lors de l’installation du scanneur Azure Information Protection : **AIPScanner_\<profile>**

- Les rapports du scanneur situés dans **%*localappdata*%\Microsoft\MSIP\Scanner\Reports**.

- Les droits d’utilisateur **Ouvrir une session en tant que service** qui ont été accordés à votre compte de domaine pour votre ordinateur local.

## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide inclut la configuration minimale vous permettant de constater rapidement comment le scanneur peut trouver des informations sensibles dans des magasins de données locaux. Si vous êtes prêt à installer le scanneur dans un environnement de production, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

Si vous souhaitez classifier et protéger les fichiers contenant des informations sensibles, vous devez configurer des étiquettes pour la classification et la protection automatiques :

- [Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection](configure-policy-classification.md)
- [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md)
