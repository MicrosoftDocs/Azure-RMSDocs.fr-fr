---
# required metadata

title: Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Protection RMS avec l’infrastructure de classification des fichiers (ICF) de Windows Server
Cet article contient des instructions et un script pour utiliser le client Rights Management (RMS) avec l'outil de protection RMS pour configurer les outils de gestion de ressources pour serveur de fichiers et l'infrastructure de classification des fichiers (ICF).

Cette solution vous permet de protéger automatiquement tous les fichiers figurant dans un dossier sur un serveur de fichiers exécutant Windows Server, ou des fichiers répondant à un critère spécifique. Il s'agit, par exemple, de fichiers qui ont été classés comme contenant des informations confidentielles ou sensibles. Cette solution utilisant Azure Rights Management (Azure RMS) pour protéger les fichiers, vous devez déployer cette technologie dans votre organisation.

> [!NOTE]
> Bien qu’Azure RMS inclue un [connecteur](../deploy-use/deploy-rms-connector.md) prenant en charge l’infrastructure de classification des fichiers, cette solution prend en charge uniquement la protection native (par exemple, celle des fichiers Office).
> 
> Pour prendre en charge tous les types de fichiers avec l'infrastructure de classification des fichiers, vous devez utiliser le module **Protection RMS** de Windows PowerShell, comme décrit dans cet article. Les applets de commande de protection RMS, telle l'application de partage RMS, prenant en charge les protections générique et native, tous les fichiers peuvent être protégés. Pour plus d’informations sur les différents niveaux de protection, consultez la section [Niveaux de protection : native et générique](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic) du [Guide de l’administrateur de l’application de partage Rights Management](sharing-app-admin-guide.md).

Les instructions qui suivent ont trait à Windows Server 2012 R2 ou à Windows Server 2012. Si vous exécutez d'autres versions prises en charge de Windows, il se peut que vous deviez adapter certaines étapes en fonction de différences existant entre votre version du système d'exploitation et celle évoquée dans cet article.

## Conditions préalables pour l'utilisation de la protection Azure RMS avec l'ICF de Windows Server
Conditions préalables pour ces instructions :

-   Sur chaque serveur de fichiers où vous allez exécuter le Gestionnaire de ressources de fichiers avec l'infrastructure de classification des fichiers :

    -   Vous avez installé les outils de gestion de ressources pour serveur de fichiers comme l'un des services de rôle pour le rôle Services de fichiers.

    -   Vous avez identifié un dossier local contenant des fichiers à protéger avec Rights Management. Par exemple, C:\FileShare.

    -   Vous avez installé l'outil de protection RMS, y compris les éléments correspondant aux conditions préalables pour l'outil (tel le client RMS) et pour Azure RMS (tel le compte de principal du service). Pour plus d'informations, voir [Applets de commande de Protection RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).

    -   Si vous souhaitez modifier le niveau par défaut de protection RMS (native ou générique) pour des extensions de nom de fichier spécifiques, vous avez modifié le Registre comme décrit dans la page [Configuration de l’API de fichier](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx) .

    -   Vous disposez d'une connexion Internet, avec des paramètres d'ordinateur configurés, si nécessaire, pour un serveur proxy. Exemple : `netsh winhttp import proxy source=ie`

-   Vous avez configuré les conditions préalables supplémentaires pour votre déploiement d’Azure Rights Management, comme décrit dans [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx). En particulier, vous avez défini les valeurs suivantes pour la connexion à Azure RMS à l'aide d'un principal du service :

    -   BposTenantId

    -   AppPrincipalId

    -   Clé symétrique

-   Vous avez synchronisé vos comptes d'utilisateurs Active Directory locaux avec Azure Active Directory ou Office 365, y compris leurs adresses électroniques. Cela est obligatoire pour tous les utilisateurs qui peuvent devoir accéder à des fichiers une fois qu'ils sont protégés par ICF et Azure RMS. Si vous n'exécutez pas cette étape (par exemple, dans un environnement de test), il se peut que l'accès des utilisateurs à ces fichiers soit bloqué. Pour plus d’informations sur la configuration de ce compte, consultez [Préparation pour Azure Rights Management](../plan-design/prepare.md).

-   Vous avez identifié le modèle Rights Management à utiliser pour protéger les fichiers. Assurez-vous de connaître l'ID de ce modèle à l'aide de l'applet de commande [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) .

## Instructions de configuration de l'ICF des outils de gestion de ressources pour serveur de fichiers pour la protection Azure RMS
Suivez ces instructions pour protéger automatiquement tous les fichiers figurant dans un dossier, en utilisant un script Windows PowerShell en tant que tâche personnalisée. Exécutez les procédures suivantes, dans l'ordre indiqué :

1.  Exécution du script Windows PowerShell

2.  Création d'une propriété de classification pour Rights Management (RMS)

3.  Création d'une règle de classification (Classifier pour RMS)

4.  Configuration de la planification de la classification

5.  Création d'une tâche de gestion de fichiers personnalisée (Protéger les fichiers avec RMS)

6.  Test de la configuration en exécutant manuellement la règle et la tâche

Quand vous aurez suivi ces instructions, tous les fichiers figurant dans votre dossier sélectionné seront classifiés avec la propriété personnalisée de RMS, et seront protégés par Rights Management. Pour une configuration plus complexe qui protège sélectivement certains fichiers et pas d'autres, vous pouvez ensuite créer ou utiliser une propriété et une règle de classification différentes, avec une tâche de gestion de fichiers qui protège uniquement ces fichiers.

### Exécution du script Windows PowerShell

1.  Copiez le contenu du [script Windows PowerShell](fci-script.md) pour la protection Azure RMS à l’aide des outils de gestion de ressources pour serveur de fichiers. Collez le contenu du script et nommez le fichier **RMS-Protect-FCI.ps1** sur votre ordinateur.

2.  Examinez le script et apportez les modifications suivantes :

    -   Recherchez la chaîne suivante, et remplacez-la par votre propre AppPrincipalId (ID de principal d'application) que vous utilisez avec l'applet de commande [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) pour vous connecter à Azure RMS :

        ```
        <enter your AppPrincipalId here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   Recherchez la chaîne suivante, et remplacez-la par votre propre clé symétrique que vous utilisez avec l'applet de commande [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) pour vous connecter à Azure RMS :

        ```
        <enter your key here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   Recherchez la chaîne suivante, et remplacez-la par votre propre BposTenantId (ID de client) que vous utilisez avec l'applet de commande [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) pour vous connecter à Azure RMS :

        ```
        <enter your BposTenantId here>
        ```
        Par exemple, le script peut se présenter comme suit :

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   Si votre serveur exécute Windows Server 2012, vous devrez charger manuellement le module de protection RMS au début du script. Ajoutez la commande suivante (ou son équivalent si le dossier « Program Files » se trouve sur un lecteur autre que le lecteur C:) :

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  Exécutez le script. Si vous ne vous signez pas le script (plus sécurisé), vous devez configurer Windows PowerShell sur les serveurs qui l'exécutent. Par exemple, exécutez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**, puis tapez : **Set-ExecutionPolicy Unrestricted**. Toutefois, cette configuration laisse tous les scripts non signés s'exécuter (moins sécurisé).

    Pour plus d'informations sur la signature des scripts Windows PowerShell, voir [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) dans la bibliothèque de documentation PowerShell.

4.  Enregistrez le fichier localement sur chaque serveur de fichiers devant exécuter le Gestionnaire de ressources de fichiers avec l'infrastructure de classification des fichiers. Par exemple, enregistrez le fichier dans **C:\RMS-Protection**. Sécurisez ce fichier à l'aide d'autorisations NTFS afin que les utilisateurs non autorisés ne puissent pas le modifier.

Vous êtes maintenant prêt à configurer les outils de gestion de ressources pour serveur de fichiers.

### Création d'une propriété de classification pour Rights Management (RMS)

-   Dans Outils de gestion de ressources pour serveur de fichiers, Gestion de la classification, créez une propriété locale :

    -   **Nom**: Tapez **RMS**

    -   **Description**:   Tapez **Protection de Rights Management**

    -   **Type de propriété** : sélectionnez **Oui/Non**

    -   **Valeur**: Sélectionnez **Oui**

Nous pouvons maintenant créer une règle de classification utilisant cette propriété.

### Création d'une règle de classification (Classifier pour RMS)

-   Créez une règle de classification :

    -   Sous l'onglet **Général** :

        -   **Nom**: Tapez **Classifier pour RMS**

        -   **Activé**: Conservez la valeur par défaut, c'est-à-dire que cette case à cocher est activée.

        -   **Description**: Tapez **Classifier tous les fichiers dans le dossier &lt;nom de dossier&gt; pour Rights Management**.

            Remplacez *&lt;nom de dossier&gt;* par le nom du dossier choisi. Par exemple, **Classifier tous les fichiers dans le dossier C:\FileShare pour Rights Management**.

        -   **Étendue**: Ajoutez le dossier que vous avez choisi. Par exemple, **C:\FileShare**.

            N'activez pas les cases à cocher.

    -   Sous l'onglet **Classification** :

    -   **Méthode de classification**: Sélectionnez **Classificateur de dossiers**

    -   Nom de**Propriété** : Sélectionnez **RMS**.

    -   **Valeur** de propriété : sélectionnez **Oui**.

Bien que vous puissiez exécuter les règles de classification manuellement pour les opérations en cours, vous souhaitez probablement que cette règle s'exécute selon une planification, afin que les nouveaux fichiers soient classifiés avec la propriété RMS.

### Configuration de la planification de la classification

-   Sous l'onglet **Classification automatique** :

    -   **Activer la planification fixe**: Activez cette case à cocher.

    -   Configurez la planification pour toutes les règles de classification à exécuter, qui inclut notre nouvelle règle de classification des fichiers avec la propriété RMS.

    -   **Autoriser la classification continue de nouveaux fichiers**: Activez cette case à cocher pour que les nouveaux fichiers soient classifiés.

    -   Facultatif : Apportez toutes les autres modifications souhaitées, par exemple, en configurant des options pour les rapports et notifications.

À présent que vous avez terminé la configuration de la classification, vous êtes prêt à configurer une tâche de gestion pour appliquer la protection RMS aux fichiers.

### Création d'une tâche de gestion de fichiers personnalisée (Protéger les fichiers avec RMS)

-   Dans **Tâches de gestion de fichiers**, créez une tâche de gestion de fichier :

    -   Sous l'onglet **Général** :

        -   **Nom de la tâche**: Tapez **Protéger les fichiers avec RMS**

        -   Conservez la case à cocher **Activer** sélectionnée.

        -   **Description**: Tapez **Protéger les fichiers dans &lt;nom de dossier&gt; avec Rights Management et un modèle à l'aide d'un script Windows PowerShell**

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

        -   **Argument**: Spécifiez les informations suivantes, en fournissant vos propres valeurs pour &lt;chemin&gt; et &lt;ID de modèle&gt; :

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            Par exemple, si vous avez copié le script dans C:\RMS-Protection et si l'ID de modèle que vous avez identifié à partir des conditions préalables est e6ee2481-26b9-45e5-b34a-f744eacd53b0, spécifiez ce qui suit :

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            Dans cette commande, **[Source File Path]** et **[Source File Owner Email]** étant deux variables spécifiques de l’ICF, tapez-les exactement telles qu’elles apparaissent dans la commande ci-dessus. La première est utilisée par l'ICF pour spécifier automatiquement le fichier identifié dans le dossier, et la deuxième pour récupérer automatiquement l'adresse de messagerie du propriétaire nommé du fichier identifié. Cette commande est répétée pour chaque fichier figurant, dans notre exemple, dans le dossier C:\FileShare qui dispose en outre de RMS en tant que propriété de classification des fichiers.

            > [!NOTE]
            > Le paramètre **-OwnerMail [Source File Owner Email]** et sa valeur garantissent que le propriétaire d’origine du fichier est le propriétaire des droits de gestion du fichier après la protection de celui-ci. Il est ainsi certain que le propriétaire d'origine du fichier dispose de tous les droits de gestion sur ses propres fichiers. Quand un utilisateur de domaine crée des fichiers, l'adresse de messagerie est automatiquement extraite d'Active Directory à l'aide du nom de compte d'utilisateur figurant dans la propriété Owner du fichier. À cette fin, le serveur de fichiers doit se trouver dans le même domaine ou domaine approuvé que l'utilisateur.
            > 
            > Autant que possible, affectez les propriétaires d'origine aux documents protégés, pour vous assurer que ces utilisateurs continuent à contrôler pleinement les fichiers qu'ils ont créés. Toutefois, si vous utilisez la variable [Source File Owner Email] comme indiqué ci-dessus, et si un fichier n'a pas d'utilisateur de domaine défini comme propriétaire (par exemple, un compte local a été utilisé pour créer le fichier, de sorte que l'utilisateur affiche SYSTEM), l'exécution du script échoue.
            > 
            > Pour les fichiers n'ayant pas d'utilisateur de domaine en tant que propriétaire, vous pouvez les copier et enregistrer vous-même en tant qu'utilisateur de domaine afin d'en devenir le propriétaire. Si vous disposez d'autorisations, vous pouvez aussi modifier manuellement le propriétaire.  Ou bien, vous pouvez fournir une adresse de messagerie spécifique (par exemple, la vôtre ou une adresse de groupe pour le département informatique) au lieu de la variable [Source File Owner Email], de sorte que tous les fichiers que vous protégez à l'aide de ce script utilisent cette adresse de messagerie pour définir le nouveau propriétaire.

    -   **Exécuter la commande en tant que**: Sélectionnez **Système local**

    -   Sous l'onglet **Condition** :

        -   **Propriété**: Sélectionnez **RMS**

        -   **Opérateur**: Sélectionnez **Égal**

        -   **Valeur**: Sélectionnez **Oui**

    -   Sous l'onglet **Planifier** :

        -   **Exécuter à**: Configurez la planification de votre choix.

            Définissez un temps conséquent pour l'exécution du script. Bien que cette solution protège tous les fichiers figurant dans le dossier, le script s'exécute une fois pour chacun d'eux à chaque fois. Bien que cela prenne plus de temps que la protection simultanée de tous les fichiers, que l'outil de protection RMS prend en charge, cette configuration fichier par fichier pour l'ICF est plus puissante. Par exemple, les fichiers protégés peuvent avoir des propriétaires différents (conserver le propriétaire d'origine) lorsque vous utilisez la variable [Source File Owner Email], et cette action fichier par fichier sera requise si vous modifiez ultérieurement la configuration afin de protéger les fichiers de façon sélective plutôt que tous les fichiers d'un dossier.

        -   **Exécuter en continu sur les nouveaux fichiers**: Activez cette case à cocher.

### Test de la configuration en exécutant manuellement la règle et la tâche

1.  Exécutez la règle de classification :

    1.  Cliquez sur **Règles de Classification** &gt; **Exécuter la classification avec toutes les règles maintenant**.

    2.  Cliquez sur **Attendre la fin de la classification**, puis sur **OK**.

2.  Attendez que la boîte de dialogue **Classification en cours d'exécution** se ferme, puis consultez les résultats dans le rapport qui s'affiche automatiquement. Vous devez voir **1** pour le champ **Propriétés** , et le nombre de fichiers figurant dans votre dossier. Vérifiez en contrôlant dans l'Explorateur de fichiers les propriétés des fichiers figurant dans le dossier que vous avez choisi. Sous l'onglet **Classification** , **RMS** doit apparaître en tant que nom de propriété, et **Oui** en tant que **Valeur**.

3.  Exécutez la tâche de gestion de fichiers :

    1.  Cliquez sur **Tâches de gestion de fichiers** &gt; **Protéger les fichiers avec RMS** &gt; **Exécuter maintenant une tâche de gestion de fichiers**.

    2.  Cliquez sur **Attendre la fin de l’exécution de la tâche**, puis sur **OK**.

4.  Attendez que la boîte de dialogue **Exécution de la tâche de gestion des fichiers** se ferme, puis consultez les résultats dans le rapport qui s'affiche automatiquement. Le champ **Fichiers** doit indiquer le nombre de fichiers figurant dans le dossier que vous avez choisi. Vérifiez que les fichiers figurant dans le dossier choisi sont à présent protégés par RMS. Par exemple, si votre dossier choisi est C:\FileShare, tapez ce qui suit dans une session Windows PowerShell, et vérifiez qu’aucun fichier ne présente l’état **Non protégé** :

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > Conseils de dépannage :
    > 
    > -   Si le rapport indique **0** au lieu du nombre de fichiers figurant dans votre dossier, cela indique que le script ne s'est pas exécuté. Commencez par contrôler le script proprement dit en le chargeant dans Windows PowerShell ISE pour valider son contenu, puis essayez de l'exécuter pour voir si des erreurs s'affichent. Si aucun argument n'est spécifié, le script tente de se connecter et de s'authentifier auprès d'Azure RMS.
    > 
    >     -   Si le script signale qu'il n'a pas pu se connecter à Azure RMS, vérifiez les valeurs affichées pour le compte de principal du service, que vous avez spécifiées dans le script.  Pour plus d'informations sur la création de ce compte de principal du service, consultez la deuxième condition préalable dans [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx).
    >     -   Si le script signale qu’il n’a pas pu se connecter à Azure RMS, vérifiez qu’il peut trouver le modèle spécifié en exécutant [Get-RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx) directement à partir de Windows PowerShell sur le serveur. Le modèle que vous avez spécifié doit figurer dans les résultats.
    > -   Si le script s'exécute par lui-même dans Windows PowerShell ISE sans erreur, essayez de l'exécuter comme suit à partir d'une session PowerShell, en spécifiant un nom de fichier à protéger, sans le paramètre -OwnerEmail :
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   Si le script s'exécute correctement dans cette session Windows PowerShell, vérifiez les entrées **Executive** et **Argument** dans l'action de tâche de gestion de fichiers.  Si vous avez spécifié **-OwnerEmail [Source File Owner Email]**, essayez de supprimer ce paramètre.
    > 
    >         Si la tâche de gestion de fichier fonctionne correctement sans **-OwnerEmail [Source File Owner Email]**, vérifiez que les fichiers non protégés ont un utilisateur de domaine répertorié comme le propriétaire du fichier, plutôt que **SYSTEM**.  Pour ce faire, sous l’onglet **Sécurité** des propriétés du fichier, cliquez sur **Avancées**. La valeur **Propriétaire** s’affiche immédiatement après le **Nom** du fichier. Vérifiez également que le serveur de fichiers se trouve dans le même domaine ou domaine approuvé pour rechercher l'adresse électronique de l'utilisateur dans les services de domaine Active Directory.
    > -   Si l'état indique le nombre correct de fichiers, mais que ceux-ci ne sont pas protégés, essayez de les protéger manuellement à l'aide de l'applet de commande [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) pour voir si des erreurs s'affichent.

Après avoir vérifié que ces tâches s'exécutent correctement, vous pouvez fermer le Gestionnaire de ressources de fichiers. Les nouveaux fichiers sont automatiquement protégés et tous les fichiers sont de nouveau protégés lors de l'exécution des planifications. Le renouvellement de la protection des fichiers garantit que toutes les modifications apportées aux modèles sont appliquées aux fichiers.


## Modification des instructions pour protéger des fichiers de façon sélective
Lorsque les instructions précédentes fonctionnent, il est très facile de les modifier pour obtenir une configuration plus sophistiquée. Par exemple, vous pouvez protéger des fichiers en utilisant le même script, mais uniquement pour les fichiers contenant des informations d'identification personnelle, voire sélectionner un modèle associé à des droits plus restrictifs.

Pour ce faire, utilisez l’une des propriétés de classification intégrées (par exemple, **Informations d’identification personnelle**) ou créez votre propre propriété. Créez ensuite une règle utilisant cette propriété. Par exemple, vous pouvez sélectionner le **Classifieur de contenus**, choisir la propriété **Informations d'identification personnelle** avec une valeur **Haute**, et configurer le modèle de chaîne ou d'expression qui identifie le fichier à configurer pour cette propriété (par exemple, la chaîne «**Date de naissance**»).

À présent, il ne vous reste plus qu'à créer une tâche de gestion de fichiers utilisant le même script, éventuellement avec un autre modèle, puis à configurer la condition pour la propriété de classification que vous venez de configurer. Par exemple, au lieu de la condition que nous avons configurée précédemment (propriété**RMS** , **Égal**, **Oui**), sélectionnez la propriété **Informations d'identification personnelle** avec la valeur **Opérateur** définie sur **Égal** et la **Valeur** **Haute**.



<!--HONumber=Apr16_HO3-->


