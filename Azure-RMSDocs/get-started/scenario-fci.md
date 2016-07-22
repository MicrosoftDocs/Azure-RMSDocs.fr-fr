---
title: "Scénario - Protéger les fichiers situés sur un partage de serveur de fichiers | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 283c7db3-5730-439e-a215-40a1088ed506
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: c16098a2d0fe41748280704716a2eeef8921a6fa


---

# Scénario - Protéger les fichiers situés sur un partage de serveur de fichiers

*S’applique à : Azure Rights Management, Office 365*

Ce scénario et la documentation utilisateur associée utilisent Azure Rights Management pour protéger en bloc tous les fichiers situés sur un serveur de fichiers pour vous assurer que seuls les employés de votre organisation peuvent y accéder, même s’ils sont copiés et enregistrés sur un stockage qui n’est pas sous le contrôle de votre service informatique ou envoyés par e-mail à d’autres utilisateurs.

Ces instructions utilisent un des modèles par défaut, ce qui limite l’accès à tous les employés ayant tous les droits d’utilisation. Toutefois, si nécessaire, vous pouvez restreindre les droits d’accès et d’utilisation en configurant un modèle personnalisé au lieu d’utiliser un modèle par défaut.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Vous devez protéger tous les types de fichiers et pas seulement les fichiers Office. Les fichiers qui ne peuvent pas être protégés en mode natif par Azure RMS seront protégés de façon générique.

-   Tous les fichiers du chemin d’accès spécifié (y compris les sous-dossiers) seront protégés.

-   La protection de tous les fichiers est réappliquée selon une planification, pour s’assurer que les modifications apportées aux modèles de stratégie de droits sont appliquées aux fichiers protégés.

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont réunies, puis suivez les instructions pour mener à bien les procédures associées avant de poursuivre avec la documentation utilisateur.

## Conditions requises pour ce scénario
Pour pouvoir appliquer les instructions de ce scénario, les conditions suivantes doivent être réunies :

|Configuration requise|Si vous avez besoin d'informations supplémentaires|
|---------------|--------------------------------|
|Azure Rights Management est activé|[Activation d'Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Vous avez synchronisé vos comptes d'utilisateurs Active Directory locaux avec Azure Active Directory ou Office 365, y compris leurs adresses électroniques. Cela est obligatoire pour tous les utilisateurs qui peuvent devoir accéder à des fichiers une fois qu’ils sont protégés par ICF et Azure Rights Management.|[Préparation pour Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Une des causes suivantes :<br /><br />- Pour utiliser un modèle par défaut pour tous les utilisateurs, consultez : Vous n’avez pas archivé le modèle par défaut &lt;nom de l’organisation&gt; - Confidentiel<br /><br />- Pour utiliser un modèle personnalisé pour des utilisateurs spécifiques, consultez : Vous avez créé et publié ce modèle personnalisé|[Configuration de modèles personnalisés pour Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|L'application de partage Rights Management est déployée sur les ordinateurs des utilisateurs qui exécutent Windows|[Déploiement automatique de l'application de partage Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|
|Vous avez téléchargé l’outil Protection RMS et configuré les conditions préalables pour Azure RMS|Pour obtenir des instructions relatives au téléchargement de l’outil et aux conditions préalables : [Applets de commande de Protection RMS](https://msdn.microsoft.com/library/mt433195.aspx)<br /><br />Pour configurer d’autres conditions préalables pour Azure RMS, telles que le compte du principal du service : [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)|

### Configuration d’un serveur de fichiers pour protéger tous les fichiers à l’aide d’Azure RMS et des Outils de gestion de ressources avec l’infrastructure de classification des fichiers

1.  Démarrez une session Windows PowerShell. Il est inutile d’exécuter cette session en tant qu’administrateur.

2.  Authentification auprès d’Azure RMS :

    ```
    Set-RMSServerAuthentication
    ```
    Lorsque vous y êtes invité, indiquez les valeurs du compte du principal du service créé en tant que condition préalable pour les applets de commande de Protection RMS.

3.  Exécutez la commande suivante pour identifier l’ID de modèle qui sera utilisé pour protéger les fichiers :

    ```
    Get-RMSTemplate
    ```
    Pour utiliser le modèle par défaut qui limite l’accès à tous les employés disposant de tous les droits d’utilisation, recherchez le nom du modèle de **&lt;nom de l’organisation&gt; - Confidentiel**. Par exemple **VanArsdel, Ltd - Confidentiel**.

4.  Suivez les instructions pas à pas de [Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx).

    Ces instructions incluent un script Windows PowerShell que vous spécifiez pour s’exécuter comme un exécutable personnalisé dans les Outils de gestion de ressources pour serveur de fichiers. Les instructions incluent également comment vérifier que les fichiers sont protégés par Azure Rights Management.

## Instructions de la documentation utilisateur
Si les fichiers que vous protégez sont uniquement des fichiers Office, il se peut que vous n’ayez à fournir aucune instruction concernant les fichiers protégés aux utilisateurs. Lorsque des utilisateurs autorisés ouvrent ces documents, ils le font comme d’habitude dans Office, à la seule différence qu’ils peuvent être invités à s’authentifier. Par ailleurs, ils verront probablement une barre d’informations en haut du document qui les informe que le document est protégé.

Si les noms de fichiers protégés comportent une extension **.ppdf** ou s’il s’agit d’un fichier texte ou image protégé (dont l’extension est, par exemple, **.ptxt** ou.**pjpg**), cela signifie qu’ils sont désormais en lecture seule et ne peuvent pas être modifiés. Les utilisateurs peuvent les afficher à l’aide de la visionneuse d’application de partage RMS, qui se charge automatiquement pour ces types de fichiers. Ces fichiers sont protégés en mode natif par Azure RMS et appliquent tous les paramètres de stratégie à partir du modèle que vous avez appliqué à l’exception des droits d’utilisation, car le fichier lui-même est en lecture seule. Sauf si vous savez que vous prévoyez de protéger ces types de fichiers, il est peu probable que vous ayez besoin d’instructions utilisateur pour ce scénario. Toutefois, avertissez votre support technique qu’il devra peut-être expliquer aux utilisateurs pourquoi ces fichiers ne peuvent pas être modifiés.

Si les noms des fichiers protégés comportent une extension **.pfile**, les utilisateurs peuvent afficher ces derniers. Toutefois, ils doivent être enregistrés sous leur nom de fichier d’origine (supprimez l’extension de nom de fichier .pfile) si les utilisateurs souhaitent modifier et enregistrer leurs modifications. Ces fichiers sont protégés par Azure RMS de manière générique et ne peuvent pas mettre en œuvre les droits d’utilisation du modèle appliqué, ce qui signifie que la protection est perdue si le fichier est enregistré sous un nouveau nom. Ce scénario a besoin d’instructions destinées aux utilisateurs.

À l’aide du modèle suivant, copiez et collez les instructions destinées aux utilisateurs finaux afin qu’ils sachent comment modifier des fichiers protégés de manière générique. Apportez les modifications suivantes en les adaptant à votre environnement :

-   Remplacez *&lt;type de fichier&gt;* et *&lt;partage de serveur de fichiers&gt;* par le type de fichier qui sera protégé de façon générique et le nom du partage de serveur de fichiers.

-   Remplacez *&lt;nom de l’organisation&gt;* par le nom de votre organisation, tel qu’il s’affiche sur vos modèles Azure Rights Management par défaut.

-   Remplacez *&lt;nom de l’organisation&gt;* par le nom de votre organisation.

-   Remplacez *&lt;Instructions relatives à l’enregistrement du fichier et à la suppression de l’extension de nom de fichier .pfile&gt;* par des instructions propres à l’application pour ce type de fichier.

-   Remplacez les coordonnées par des instructions indiquant comment contacter le support technique, telles qu’un lien vers un site web, une adresse e-mail ou un numéro de téléphone.

-   Apportez toute autre modification de votre choix à cet ensemble d’instructions, puis adressez-le à ces utilisateurs.

L’exemple de documentation illustre la façon dont ces instructions se présentent aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### Procédure de modification de &lt;type de fichier&gt; à partir du &lt;partage de serveur de fichiers&gt;

1.  Double-cliquez sur le fichier pour l’ouvrir. Il se peut que vous soyez invité à fournir vos informations d’identification.

2.  Une boîte de dialogue de **fichier protégé** issue de l’application de partage Microsoft Rights Management, s’affiche. Elle vous indique que vous êtes censé respecter les autorisations relatives à **&lt;nom de l’organisation&gt; - Confidentiel**. Cela signifie que vous ne devez pas partager ce document avec d’autres personnes si elles ne travaillent pas pour &lt;nom de l’organisation&gt;.

3.  Cliquez sur **Ouvrir**.

4.  Pour modifier le fichier, commencez par l’enregistrer et supprimer l’extension de nom de fichier .pfile :

    -   &lt;Instructions relatives à l’enregistrement du fichier et à la suppression de l’extension de nom de fichier .pfile&gt;

5.  Vous pouvez maintenant modifier et enregistrer le fichier comme d’habitude.

Périodiquement, le fichier sera de nouveau protégé, ce qui ajoutera une nouvelle fois l’extension de nom de fichier .pfile et vous contraindra à répéter ces étapes.

**Vous avez besoin d'aide ?**

-   Pour plus d'informations :

    -   [Afficher et utiliser des fichiers protégés](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contactez le support technique :

    -   *&lt;coordonnées&gt;*

### Exemple de documentation utilisateur personnalisée
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Procédure de modification de dessins de CAO à partir du partage ProjectNextGen

1.  Double-cliquez sur le fichier pour l’ouvrir. Il se peut que vous soyez invité à fournir vos informations d’identification.

2.  Une boîte de dialogue de **fichier protégé** issue de l’application de partage Microsoft Rights Management, s’affiche, qui vous indique que vous êtes censé respecter les autorisations relatives à **VanArsdel, Ltd - Confidential**. Cela signifie de ne pas partager ce document avec d’autres personnes si elles ne travaillent pas pour VanArsdel, Ltd.

3.  Cliquez sur **Ouvrir**.

4.  Pour modifier le fichier, commencez par l’enregistrer et supprimer l’extension de nom de fichier .pfile :

    -   **Fichier** &gt; **Enregistrer sous**

    -   Supprimez **.pfile** de la fin du nom de fichier et cliquez sur **OK**.

5.  Vous pouvez maintenant modifier et enregistrer le fichier comme d’habitude.

Périodiquement, le fichier sera de nouveau protégé, ce qui ajoutera une nouvelle fois l’extension de nom de fichier .pfile et vous contraindra à répéter ces étapes.

**Vous avez besoin d'aide ?**

-   Pour plus d'informations :

    -   [Afficher et utiliser des fichiers protégés](https://technet.microsoft.com/library/dn574741%28v=ws.10%29)

-   Contactez le support technique : helpdesk@vanarsdelltd.com




<!--HONumber=Jul16_HO3-->


