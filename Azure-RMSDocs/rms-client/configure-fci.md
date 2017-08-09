---
title: "Protection RMS avec l’infrastructure ICF de Windows Server - AIP"
description: "Instructions d’utilisation du client Rights Management (RMS) avec l’outil de protection RMS pour configurer les outils de gestion de ressources pour serveur de fichiers et l’infrastructure de classification des fichiers (ICF)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e67bc3d82c1269343cd4e64f8a608a2a86d381ef
ms.sourcegitcommit: 7cd6ff39731c7abe990a72a49bc10d104f47764d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2017
---
# <a name="rms-protection-with-windows-server-file-classification-infrastructure-fci"></a>Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server

>*S’applique à : Azure Information Protection, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2*

Cet article contient des instructions et un script pour utiliser le client Azure Information Protection et PowerShell pour configurer les outils de gestion de ressources pour serveur de fichiers et l’infrastructure de classification des fichiers (ICF).

Cette solution vous permet de protéger automatiquement tous les fichiers figurant dans un dossier sur un serveur de fichiers exécutant Windows Server, ou des fichiers répondant à un critère spécifique. Il s'agit, par exemple, de fichiers qui ont été classés comme contenant des informations confidentielles ou sensibles. Cette solution se connecte directement au service Azure Rights Management d’Azure Information Protection pour protéger les fichiers, vous devez déployer ce service pour votre organisation.

> [!NOTE]
> Bien qu’Azure Information Protection inclue un [connecteur](../deploy-use/deploy-rms-connector.md) prenant en charge l’infrastructure de classification des fichiers, cette solution prend en charge uniquement la protection native (par exemple, celle des fichiers Office).
> 
> Pour prendre en charge plusieurs types de fichiers avec l’infrastructure de classification des fichiers Windows Server, vous devez utiliser le module **AzureInformationProtection** de PowerShell, comme décrit dans cet article. Les applets de commande Azure Information Protection, telles que le client Azure Information Protection, prennent en charge la protection générique ainsi que la protection native, ce qui signifie que les types de fichiers autres que les documents Office peuvent être protégés. Pour plus d’informations, consultez [Types de fichiers pris en charge par le client Azure Information Protection](client-admin-guide-file-types.md) dans le guide de l’administrateur du client Azure Information Protection.

Les instructions qui suivent ont trait à Windows Server 2012 R2 ou à Windows Server 2012. Si vous exécutez d'autres versions prises en charge de Windows, il se peut que vous deviez adapter certaines étapes en fonction de différences existant entre votre version du système d'exploitation et celle évoquée dans cet article.

## <a name="prerequisites-for-azure-rights-management-protection-with-windows-server-fci"></a>Conditions préalables pour l’utilisation de la protection Azure Rights Management avec l’ICF de Windows Server
Conditions préalables pour ces instructions :

-  Sur chaque serveur de fichiers où vous allez exécuter le Gestionnaire de ressources de fichiers avec l'infrastructure de classification des fichiers :
    
    - Vous avez installé les outils de gestion de ressources pour serveur de fichiers comme l'un des services de rôle pour le rôle Services de fichiers.
    
    - Vous avez identifié un dossier local contenant des fichiers à protéger avec Rights Management. Par exemple, C:\FileShare.
    
    - Vous avez installé le module PowerShell AzureInformationProtection et configuré les conditions préalables pour que ce module puisse se connecter à Azure Rights Management.
    
    Le module PowerShell AzureInformationProtection est fourni avec le client Azure Information Protection. Pour des instructions d’installation détaillées, consultez [Procédure d’installation du client Azure Information Protection pour les utilisateurs](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) dans le guide de l’administrateur d’Azure Information Protection. Si nécessaire, vous pouvez installer uniquement le module PowerShell à l’aide du paramètre `PowerShellOnly=true`.
    
    Les [conditions préalables pour l’utilisation de ce module PowerShell](client-admin-guide-powershell.md#azure-information-protection-and-azure-rights-management-service) comprennent l’activation du service Azure Rights Management, la création d’un principal de service et la modification du registre si votre client se trouve en dehors de l’Amérique du Nord. Avant de commencer à suivre les instructions fournies dans cet article, assurez-vous d’avoir des valeurs pour **BposTenantId**, **AppPrincipalId** et **Clé symétrique**, comme indiqué dans ces conditions préalables. 
    
    - Si vous souhaitez modifier le niveau par défaut de protection (native ou générique) pour des extensions de nom de fichier spécifiques, vous avez modifié le Registre comme décrit dans la section [Modification du niveau de protection par défaut des fichiers](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) du guide d’administrateur.
    
    - Vous disposez d’une connexion Internet et vous avez configuré les paramètres de votre ordinateur s’ils sont nécessaires pour un serveur proxy. Par exemple : `netsh winhttp import proxy source=ie`
    
- Vous avez synchronisé vos comptes d’utilisateur Active Directory locaux avec Azure Active Directory ou Office 365, dont leurs adresses e-mail. Cela est obligatoire pour tous les utilisateurs qui peuvent devoir accéder à des fichiers une fois qu’ils sont protégés par ICF et le service Azure Rights Management. Si vous n’exécutez pas cette étape (par exemple, dans un environnement de test), il se peut que l’accès des utilisateurs à ces fichiers soit bloqué. Si vous avez besoin de plus d’informations sur cette exigence, consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](../plan-design/prepare.md).
    
- Vous avez téléchargé les modèles Rights Management sur le serveur de fichiers, puis identifié l’identifiant de modèle qui va protéger les fichiers. Pour cela, utilisez la cmdlet [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate). Ce scénario ne prend pas en charge les modèles de services. Par conséquent, vous devez utiliser un modèle qui n’est pas configuré pour une étendue ou la configuration de l’étendue doit inclure l’option de compatibilité des applications de manière à ce que la case à cocher **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l’identité de l’utilisateur** soit activée.

## <a name="instructions-to-configure-file-server-resource-manager-fci-for-azure-rights-management-protection"></a>Instructions de configuration de l’ICF des outils de gestion de ressources pour serveur de fichiers pour la protection Azure Rights Management
Suivez ces instructions pour protéger automatiquement tous les fichiers figurant dans un dossier, en utilisant un script PowerShell en tant que tâche personnalisée. Exécutez les procédures suivantes, dans l'ordre indiqué :

1. Enregistrer le script PowerShell

2. Création d'une propriété de classification pour Rights Management (RMS)

3. Création d'une règle de classification (Classifier pour RMS)

4. Configuration de la planification de la classification

5. Création d'une tâche de gestion de fichiers personnalisée (Protéger les fichiers avec RMS)

6. Test de la configuration en exécutant manuellement la règle et la tâche

Quand vous aurez suivi ces instructions, tous les fichiers figurant dans votre dossier sélectionné seront classifiés avec la propriété personnalisée de RMS, et seront protégés par Rights Management. Pour une configuration plus complexe qui protège sélectivement certains fichiers et pas d'autres, vous pouvez ensuite créer ou utiliser une propriété et une règle de classification différentes, avec une tâche de gestion de fichiers qui protège uniquement ces fichiers.

Notez que si vous apportez des modifications au modèle Rights Management que vous utilisez pour l’ICF, vous devez exécuter `Get-RMSTemplate -Force` sur l’ordinateur du serveur de fichiers pour obtenir le modèle mis à jour. Le modèle mis à jour est ensuite utilisé pour protéger de nouveaux fichiers. Si les modifications apportées au modèle sont suffisamment importantes pour protéger de nouveau les fichiers sur le serveur de fichiers, vous faites cela en exécutant l’applet de commande Protect-RMSFile de façon interactive avec un compte ayant des droits d’utilisation Contrôle total ou Exportation sur les fichiers. Si vous publiez un nouveau modèle que vous souhaitez utiliser pour l’ICF, vous devez également exécuter `Get-RMSTemplate -Force` sur ce serveur de fichiers.

### <a name="save-the-windows-powershell-script"></a>Exécution du script Windows PowerShell

1.  Copiez le contenu du [script Windows PowerShell](fci-script.md) pour la protection Azure RMS à l’aide des outils de gestion de ressources pour serveur de fichiers. Collez le contenu du script et nommez le fichier **RMS-Protect-FCI.ps1** sur votre ordinateur.

2.  Examinez le script et apportez les modifications suivantes :
    
    - Recherchez la chaîne suivante et remplacez-la par votre propre AppPrincipalId que vous utilisez avec l’applet de commande [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) pour vous connecter au service Azure Rights Management :

        ```
        <enter your AppPrincipalId here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Recherchez la chaîne suivante, et remplacez-la par votre propre clé symétrique que vous utilisez avec l’applet de commande [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) pour vous connecter au service Azure Rights Management :

        ```
        <enter your key here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Recherchez la chaîne suivante, et remplacez-la par votre propre BposTenantId (ID de locataire) que vous utilisez avec l’applet de commande [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) pour vous connecter au service Azure Rights Management :

        ```
        <enter your BposTenantId here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

3.  Exécutez le script. Si vous ne vous signez pas le script (plus sécurisé), vous devez configurer Windows PowerShell sur les serveurs qui l'exécutent. Par exemple, exécutez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**, puis tapez : **Set-ExecutionPolicy RemoteSigned**. Toutefois, cette configuration laisse s’exécuter tous les scripts non signés quand ils sont stockés sur ce serveur (moins sécurisé).

    Pour plus d'informations sur la signature des scripts Windows PowerShell, voir [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) dans la bibliothèque de documentation PowerShell.

4.  Enregistrez le fichier localement sur chaque serveur de fichiers qui exécute le Gestionnaire de ressources de fichier avec l’infrastructure de classification des fichiers. Par exemple, enregistrez le fichier dans **C:\RMS-Protection**. Si vous utilisez un chemin ou un nom de dossier différent, choisissez un chemin et un dossier ne contenant pas d’espaces. Sécurisez ce fichier à l'aide d'autorisations NTFS afin que les utilisateurs non autorisés ne puissent pas le modifier.

Vous êtes maintenant prêt à configurer les outils de gestion de ressources pour serveur de fichiers.

### <a name="create-a-classification-property-for-rights-management-rms"></a>Création d'une propriété de classification pour Rights Management (RMS)

-   Dans Outils de gestion de ressources pour serveur de fichiers, Gestion de la classification, créez une propriété locale :

    -   **Nom**: Tapez **RMS**

    -   **Description**:   Tapez **Protection de Rights Management**

    -   **Type de propriété** : sélectionnez **Oui/Non**

    -   **Valeur**: Sélectionnez **Oui**

Nous pouvons maintenant créer une règle de classification utilisant cette propriété.

### <a name="create-a-classification-rule-classify-for-rms"></a>Création d'une règle de classification (Classifier pour RMS)

-   Créez une règle de classification :

    -   Sous l'onglet **Général** :

        -   **Nom**: Tapez **Classifier pour RMS**

        -   **Activé**: Conservez la valeur par défaut, c'est-à-dire que cette case à cocher est activée.

        -   **Description** : Tapez **Classifier tous les fichiers dans le dossier &lt;nom de dossier&gt; pour Rights Management**.

            Remplacez *&lt;nom de dossier&gt;* par le nom du dossier choisi. Par exemple, **Classifier tous les fichiers dans le dossier C:\FileShare pour Rights Management**.

        -   **Étendue**: Ajoutez le dossier que vous avez choisi. Par exemple, **C:\FileShare**.

            N'activez pas les cases à cocher.

    -   Sous l'onglet **Classification** :

    -   **Méthode de classification**: Sélectionnez **Classificateur de dossiers**

    -   Nom de**Propriété** : Sélectionnez **RMS**.

    -   **Valeur** de propriété : sélectionnez **Oui**.

Bien que vous puissiez exécuter les règles de classification manuellement, pour les opérations en cours, vous voulez que cette règle s’exécute selon une planification, afin que les nouveaux fichiers soient classifiés avec la propriété RMS.

### <a name="configure-the-classification-schedule"></a>Configuration de la planification de la classification

-   Sous l'onglet **Classification automatique** :

    -   **Activer la planification fixe**: Activez cette case à cocher.

    -   Configurez la planification pour toutes les règles de classification à exécuter, qui inclut notre nouvelle règle de classification des fichiers avec la propriété RMS.

    -   **Autoriser la classification continue de nouveaux fichiers** : activez cette case à cocher pour que les nouveaux fichiers soient classifiés.

    -   Facultatif : Apportez toutes les autres modifications souhaitées, par exemple, en configurant des options pour les rapports et notifications.

À présent que vous avez terminé la configuration de la classification, vous êtes prêt à configurer une tâche de gestion pour appliquer la protection RMS aux fichiers.

### <a name="create-a-custom-file-management-task-protect-files-with-rms"></a>Création d'une tâche de gestion de fichiers personnalisée (Protéger les fichiers avec RMS)

-   Dans **Tâches de gestion de fichiers**, créez une tâche de gestion de fichier :

    -   Sous l'onglet **Général** :

        -   **Nom de la tâche**: Tapez **Protéger les fichiers avec RMS**

        -   Conservez la case à cocher **Activer** sélectionnée.

        -   **Description** : Tapez **Protéger les fichiers dans &lt;nom de dossier&gt; avec Rights Management et un modèle à l’aide d’un script Windows PowerShell.**

            Remplacez *&lt;nom de dossier&gt;* par le nom du dossier choisi. Par exemple, **Protéger les fichiers dans C:\FileShare avec Rights Management et un modèle à l’aide d’un script Windows PowerShell**.

        -   **Étendue**: Sélectionnez le dossier que vous avez choisi. Par exemple, **C:\FileShare**.

            N'activez pas les cases à cocher.

    -   Sous l'onglet **Action** :

        -   **Type**: Sélectionnez **Personnalisée**

        -   **Exécutable**: Spécifiez ce qui suit :

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Si Windows n'est pas sur votre lecteur C:, modifiez ce chemin d'accès ou accédez à ce fichier.

        -   **Argument** : Spécifiez les informations suivantes, en fournissant vos propres valeurs pour &lt;chemin&gt; et &lt;ID de modèle&gt; :

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Par exemple, si vous avez copié le script dans C:\RMS-Protection et si l'ID de modèle que vous avez identifié à partir des conditions préalables est e6ee2481-26b9-45e5-b34a-f744eacd53b0, spécifiez ce qui suit :

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            Dans cette commande, **[Source File Path]** et **[Source File Owner Email]** étant deux variables spécifiques de l’ICF, tapez-les exactement telles qu’elles apparaissent dans la commande précédente. La première variable est utilisée par l’ICF pour spécifier automatiquement le fichier identifié dans le dossier, et la deuxième variable pour récupérer automatiquement l’adresse e-mail du propriétaire nommé du fichier identifié. Cette commande est répétée pour chaque fichier figurant, dans notre exemple, dans le dossier C:\FileShare qui dispose en outre de RMS en tant que propriété de classification des fichiers.

            > [!NOTE]
            > Le paramètre **-OwnerMail [Source File Owner Email]** et sa valeur garantissent que le propriétaire d’origine du fichier est le propriétaire des droits de gestion du fichier après la protection de celui-ci. Cette configuration garantit que le propriétaire d’origine du fichier dispose de tous les droits Rights Management sur ses propres fichiers. Quand un utilisateur de domaine crée des fichiers, l'adresse de messagerie est automatiquement extraite d'Active Directory à l'aide du nom de compte d'utilisateur figurant dans la propriété Owner du fichier. À cette fin, le serveur de fichiers doit se trouver dans le même domaine ou domaine approuvé que l'utilisateur.
            > 
            > Autant que possible, affectez les propriétaires d'origine aux documents protégés, pour vous assurer que ces utilisateurs continuent à contrôler pleinement les fichiers qu'ils ont créés. Cependant, si vous utilisez la variable [Source File Owner Email] comme dans la commande précédente, et si un fichier n’a pas d’utilisateur de domaine défini comme propriétaire (par exemple, un compte local a été utilisé pour créer le fichier, de sorte que le propriétaire affiché est SYSTEM), le script échoue.
            > 
            > Pour les fichiers n'ayant pas d'utilisateur de domaine en tant que propriétaire, vous pouvez les copier et enregistrer vous-même en tant qu'utilisateur de domaine afin d'en devenir le propriétaire. Si vous disposez d'autorisations, vous pouvez aussi modifier manuellement le propriétaire.  Vous pouvez aussi fournir une adresse e-mail spécifique (par exemple, la vôtre ou une adresse de groupe pour le département informatique) au lieu de la variable [Source File Owner Email], de sorte que tous les fichiers que vous protégez à l’aide de ce script utilisent cette adresse e-mail pour définir le nouveau propriétaire.

    -   **Exécuter la commande en tant que**: Sélectionnez **Système local**

    -   Sous l'onglet **Condition** :

        -   **Propriété**: Sélectionnez **RMS**

        -   **Opérateur**: Sélectionnez **Égal**

        -   **Valeur**: Sélectionnez **Oui**

    -   Sous l'onglet **Planifier** :

        -   **Exécuter à**: Configurez la planification de votre choix.

            Définissez un temps conséquent pour l'exécution du script. Bien que cette solution protège tous les fichiers du dossier, le script s'exécute une fois pour chacun d'eux à chaque fois. Bien que cela prenne plus de temps que de protéger tous les fichiers en même temps, ce qui est pris en charge le client Azure Information Protection, cette configuration fichier par fichier pour l'ICF est plus puissante. Par exemple, les fichiers protégés peuvent avoir des propriétaires différents (conserver le propriétaire d’origine) quand vous utilisez la variable [Source File Owner Email], et cette action fichier par fichier est nécessaire si vous modifiez ultérieurement la configuration pour protéger les fichiers de façon sélective plutôt que tous les fichiers d’un dossier.

        -   **Exécuter en continu sur les nouveaux fichiers**: Activez cette case à cocher.

### <a name="test-the-configuration-by-manually-running-the-rule-and-task"></a>Test de la configuration en exécutant manuellement la règle et la tâche

1.  Exécutez la règle de classification :

    1.  Cliquez sur **Règles de classification** &gt; **Exécuter la classification avec toutes les règles maintenant**

    2.  Cliquez sur **Attendre la fin de la classification**, puis sur **OK**.

2.  Attendez que la boîte de dialogue **Classification en cours d'exécution** se ferme, puis consultez les résultats dans le rapport qui s'affiche automatiquement. Vous devez voir **1** pour le champ **Propriétés** , et le nombre de fichiers figurant dans votre dossier. Vérifiez en contrôlant dans l'Explorateur de fichiers les propriétés des fichiers figurant dans le dossier que vous avez choisi. Sous l'onglet **Classification** , **RMS** doit apparaître en tant que nom de propriété, et **Oui** en tant que **Valeur**.

3.  Exécutez la tâche de gestion de fichiers :

    1.  Cliquez sur **Tâches de gestion de fichiers** &gt; **Protéger les fichiers avec RMS** &gt; **Exécuter maintenant une tâche de gestion de fichiers**

    2.  Cliquez sur **Attendre la fin de l’exécution de la tâche**, puis sur **OK**.

4.  Attendez que la boîte de dialogue **Exécution de la tâche de gestion des fichiers** se ferme, puis consultez les résultats dans le rapport qui s'affiche automatiquement. Le champ **Fichiers** doit indiquer le nombre de fichiers figurant dans le dossier que vous avez choisi. Vérifiez que les fichiers figurant dans le dossier choisi sont à présent protégés par Rights Management. Par exemple, si vous avez choisi le dossier C:\FileShare, tapez la commande suivante dans une session Windows PowerShell, et vérifiez qu’aucun fichier n’est dans l’état **Non protégé** :

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Conseils de dépannage :
    > 
    > -   Si le rapport indique **0** au lieu du nombre de fichiers figurant dans votre dossier, cela indique que le script ne s’est pas exécuté. Commencez par contrôler le script proprement dit en le chargeant dans Windows PowerShell ISE pour valider son contenu, puis essayez de l'exécuter pour voir si des erreurs s'affichent. Si aucun argument n’est spécifié, le script tente de se connecter et de s’authentifier auprès du service Azure Rights Management.
    > 
    >     -   Si le script signale qu'il n'a pas pu se connecter au service Azure Rights Management (Azure RMS), vérifiez les valeurs affichées pour le compte de principal du service que vous avez spécifiées dans le script. Pour plus d’informations sur la création de ce compte de principal du service, consultez la page [Condition préalable 3 : protéger ou annuler la protection des fichiers sans interaction](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction) dans le guide de l’administrateur du client Azure Information Protection.
    >     -   Si le script signale qu’il n’a pas pu se connecter à Azure RMS, vérifiez qu’il peut trouver le modèle spécifié en exécutant [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate) directement à partir de Windows PowerShell sur le serveur. Le modèle que vous avez spécifié doit figurer dans les résultats.
    > -   Si le script s'exécute par lui-même dans Windows PowerShell ISE sans erreur, essayez de l'exécuter comme suit à partir d'une session PowerShell, en spécifiant un nom de fichier à protéger, sans le paramètre -OwnerEmail :
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Si le script s'exécute correctement dans cette session Windows PowerShell, vérifiez les entrées **Executive** et **Argument** dans l'action de tâche de gestion de fichiers.  Si vous avez spécifié **-OwnerEmail [Source File Owner Email]**, essayez de supprimer ce paramètre.
    > 
    >         Si la tâche de gestion de fichier fonctionne correctement sans **-OwnerEmail [Source File Owner Email]**, vérifiez que les fichiers non protégés ont un utilisateur de domaine répertorié comme le propriétaire du fichier, plutôt que **SYSTEM**.  Pour faire cette vérification, sous l’onglet **Sécurité** des propriétés du fichier, cliquez sur **Avancé**. La valeur **Propriétaire** s’affiche immédiatement après le **Nom** du fichier. Vérifiez également que le serveur de fichiers se trouve dans le même domaine ou dans un domaine approuvé pour rechercher l’adresse e-mail de l’utilisateur dans les services de domaine Active Directory.
    > -   Si l'état indique le nombre correct de fichiers, mais que ceux-ci ne sont pas protégés, essayez de les protéger manuellement à l'aide de l'applet de commande [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) pour voir si des erreurs s'affichent.

Après avoir vérifié que ces tâches s'exécutent correctement, vous pouvez fermer le Gestionnaire de ressources de fichiers. Les nouveaux fichiers sont automatiquement classifiés et protégés quand les tâches planifiées s’exécutent. 

## <a name="modifying-the-instructions-to-selectively-protect-files"></a>Modification des instructions pour protéger des fichiers de façon sélective
Quand les instructions précédentes fonctionnent, il est facile de les modifier pour obtenir une configuration plus sophistiquée. Par exemple, vous pouvez protéger des fichiers en utilisant le même script, mais uniquement pour les fichiers contenant des informations d'identification personnelle, voire sélectionner un modèle associé à des droits plus restrictifs.

Pour faire cette modification, utilisez une des propriétés de classification prédéfinie (par exemple, **Informations d’identification personnelle**) ou créez votre propre propriété. Créez ensuite une règle utilisant cette propriété. Par exemple, vous pouvez sélectionner le **Classifieur de contenus**, choisir la propriété **Informations d'identification personnelle** avec une valeur **Haute**, et configurer le modèle de chaîne ou d'expression qui identifie le fichier à configurer pour cette propriété (par exemple, la chaîne «**Date de naissance**»).

À présent, il ne vous reste plus qu'à créer une tâche de gestion de fichiers utilisant le même script, éventuellement avec un autre modèle, puis à configurer la condition pour la propriété de classification que vous venez de configurer. Par exemple, au lieu de la condition que nous avons configurée précédemment (propriété**RMS** , **Égal**, **Oui**), sélectionnez la propriété **Informations d'identification personnelle** avec la valeur **Opérateur** définie sur **Égal** et la **Valeur** **Haute**.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
