---
title: TEST Migration d’AD RMS vers Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# AVANT : Migration d’AD RMS vers Azure Rights Management
Utilisez l'ensemble suivant d'instructions pour migrer votre déploiement Active Directory Rights Management Services (AD RMS) vers Azure Rights Management (Azure RMS). Après la migration, les utilisateurs auront toujours accès aux documents et messages électroniques que votre organisation a protégés à l'aide d'AD RMS, et le contenu nouvellement protégé utilisera Azure RMS.

Vous n'êtes pas certain de l'opportunité de cette migration AD RMS pour votre organisation ?

-   Pour une présentation d’Azure RMS, des problèmes professionnels que cette solution peut résoudre, de son aspect pour les administrateurs et les utilisateurs, et de son fonctionnement, consultez [En quoi consiste Azure Rights Management ?](what-is-azure-rms.md)

-   Pour obtenir une comparaison d’Azure RMS et d’AD RMS, consultez [Comparaison d’Azure Rights Management avec AD RMS](compare-azure-rms-ad-rms.md).

## Conditions préalables à une migration d'AD RMS vers Azure RMS
Avant de procéder à la migration vers Azure RMS, assurez-vous que les conditions préalables suivantes sont réunies et que vous comprenez les limitations de ce processus.

|Condition requise|Plus d'informations|
|---------------|--------------------|
|Un déploiement RMS pris en charge|Toutes les versions d'AD RMS, de Windows Server 2008 à Windows Server 2012 R2, prennent en charge une migration vers Azure RMS :<br /><br />Windows Server 2008 (x86 ou x64)<br /><br />Windows Server 2008 R2 (x64)<br /><br />Windows Server 2012 (x64)<br /><br />Windows Server 2012 R2 (x64)<br /><br />Toutes les topologies AD RMS valides sont prises en charge :<br /><br />Forêt unique, cluster RMS unique<br /><br />Forêt unique, plusieurs clusters RMS dédiés uniquement à la gestion des licences<br /><br />Plusieurs forêts, plusieurs clusters RMS<br /><br />**Remarque** : Par défaut, plusieurs clusters RMS migrent vers un seul client Azure RMS. Si vous souhaitez disposer de plusieurs clients RMS, vous devez les traiter comme des migrations différentes. Une clé d'un cluster RMS ne peut pas être importée dans plus d'un client Azure RMS.|
|Toutes les configurations requises pour exécuter Azure RMS, y compris un client Azure RMS (non activé)|Consultez [Configuration requise pour Azure Rights Management](requirements-azure-rms.md).<br /><br />Bien que vous deviez disposer d'un client Azure RMS pour pouvoir migrer à partir d'AD RMS, nous vous recommandons de ne pas activer le service Rights Management avant d'avoir procédé à la migration. Le processus de migration inclut cette étape après l'exportation des clés et modèles à partir d'AD RMS, et leur importation dans Azure RMS. Toutefois, si Azure RMS est déjà activé, vous pouvez toujours migrer à partir d'AD RMS.|
|Préparation pour Azure RMS :<br /><br />Synchronisation d'annuaires entre votre annuaire local et Azure Active Directory<br /><br />Groupes à extension messagerie dans Azure Active Directory|Consultez [Préparation pour Azure Rights Management](prepare.md).|
|Si vous avez utilisé la fonctionnalité de Gestion des droits relatifs à l'information (IRM) d'Exchange Server (par exemple, règles de transport et Outlook Web Access) ou de SharePoint Server avec AD RMS :<br /><br />Prévoyez une courte période pendant laquelle cette fonctionnalité ne sera pas disponible sur ces serveurs.|Vous pouvez continuer à utiliser la fonctionnalité IRM sur ces serveurs avec Azure RMS après la migration. Toutefois, une des étapes de migration consiste à désactiver temporairement le service IRM, à installer et à configurer un connecteur, à reconfigurer les serveurs, puis à réactiver le service IRM.<br /><br />Il s'agit de l'unique interruption de service durant le processus de migration.|
Limitations :

-   Bien que le processus de migration prenne en charge la migration de votre clé de certificat de licence serveur (SLC) vers un module de sécurité matériel (HSM) pour Azure RMS, Exchange Online ne prend pas actuellement en charge cette configuration. Si vous voulez disposer de toutes les fonctionnalités d’IRM avec Exchange Online après la migration vers Azure RMS, votre clé de client Azure RMS doit être [gérée par Microsoft](http://technet.microsoft.com/library/dn440580.aspx). Vous pouvez également exécuter l'IRM avec des fonctionnalités réduites dans Exchange Online quand vous gérez vous-même votre client Azure RMS (à l'aide de la solution BYOK). Pour plus d’informations sur l’utilisation d’Exchange Online avec Azure RMS, consultez l’[Étape 6. Configurer l’intégration d’IRM pour Exchange Online](#BKMK_Step6Migration) dans ces instructions.

-   Si vous disposez de logiciels et de clients non pris en charge avec Azure RMS, ceux-ci ne peuvent pas protéger ou utiliser du contenu protégé par Azure RMS. Consultez les sections relatives aux applications et aux clients pris en charge dans la rubrique [Configuration requise pour Azure Rights Management](requirements-azure-rms.md).

-   Si vous importez votre clé locale dans Azure RMS en tant que clé archivée (vous ne définissez pas le TPD comme étant actif pendant le processus d’importation), puis migrez des utilisateurs par lots dans le cadre d’une migration en plusieurs phases, le contenu qui vient d’être protégé par les utilisateurs migrés n’est plus accessible aux utilisateurs qui restent sur AD RMS. Dans ce cas, autant que possible, veillez à ce que la durée de la migration soit courte et migrez les utilisateurs par lots logiques, par exemple, d'utilisateurs collaborant entre eux.

    Cette limitation ne s'applique pas quand vous définissez le domaine de publication approuvé comme étant actif pendant le processus d'importation, car tous les utilisateurs protégeront le contenu à l'aide de la même clé. Nous recommandons cette configuration, car elle vous permet de migrer tous les utilisateurs de façon indépendante et à votre propre rythme.

-   Si vous collaborez avec des partenaires externes (par exemple, en utilisant des domaines d'utilisateurs approuvés ou une fédération), ceux-ci doivent également migrer vers Azure RMS, soit au moment de votre migration, soit dès que possible par la suite. Pour continuer à accéder au contenu que votre organisation protégeait précédemment à l'aide d'AD RMS, les utilisateurs doivent apporter à la configuration du client des modifications similaires à celles que vous apportez, qui sont incluses dans ce document.

    En raison de la diversité des configurations possibles de vos partenaires, des instructions précises pour cette reconfiguration sortent du cadre de ce document. Pour obtenir de l'aide, contactez services de support technique Microsoft.

## Étapes de la migration d'AD RMS vers Azure RMS

|Étapes de migration|Plus d'informations|
|------------------|--------------------|
|**1. Télécharger les outils d'administration pour la gestion d'Azure RMS**|Pour obtenir des instructions, consultez [Étape 1 : Télécharger l’outil d’administration Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step1Migration).|
|**2. Exporter les données de configuration d'AD RMS, puis les importer dans Azure RMS**|Vous exportez les données de configuration (clés, modèles, URL) d'AD RMS vers un fichier XML, puis vous chargez ce fichier dans Azure RMS à l'aide de l'applet de commande Windows PowerShell Import-AadrmTpd. Des étapes supplémentaires peuvent être nécessaires en fonction la configuration de votre clé AD RMS :<br /><br />**Migration de clé protégée par logiciel à clé protégée par logiciel** : Clés basées sur un mot de passe gérées de façon centralisée dans AD RMS à clé de client Azure RMS gérée par Microsoft. Ce chemin de migration le plus simple ne nécessite aucune étape supplémentaire.<br /><br />**Migration de clé protégée par HSM à clé protégée par HSM** : Clés stockées par un HSM pour AD RMS à clé de client Azure RMS gérée par le client (scénario BYOK, « Bring Your Own Key »). Cette migration nécessite des étapes supplémentaires pour transférer la clé de votre HSM Thales local vers le HSM Azure RMS. Votre clé protégée par HSM existante doit être protégée par module. Les clés protégées par OCS ne sont pas prises en charge par l’ensemble d’outils BYOK.<br /><br />**Migration de clé protégée par logiciel à clé protégée par HSM** : Clés basées sur un mot de passe, gérées de façon centralisée dans AD RMS à clé de client Azure RMS gérée par le client (scénario BYOK, « Bring Your Own Key »). Cette migration est celle qui nécessite le plus de configuration, car vous devez extraire votre clé logicielle et l'importer dans un HSM local, puis la transférer de votre HSM Thales vers le HSM Azure RMS.<br /><br />Pour obtenir des instructions, consultez [Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step2Migration).|
|**3. Activer votre client RMS**|Si possible, effectuez cette étape après le processus d'importation et non avant.<br /><br />Pour plus d’informations et pour obtenir des instructions, consultez [Étape 3. Activer votre client RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).|
|**4. Configurer les modèles importés**|Lorsque vous importez vos modèles de stratégie de droits, leur état est archivé. Si vous souhaitez que les utilisateurs puissent voir et utiliser ces modèles, vous devez modifier leur état en publié dans le portail Azure Classic.<br /><br />Pour obtenir des instructions, consultez [Étape 4. Configurer les modèles importés](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step4Migration).|
|**5. Reconfigurer les clients pour utiliser Azure RMS**|Les ordinateurs Windows existants doivent être reconfigurés pour utiliser le service Azure RMS au lieu d'AD RMS. Cette étape s'applique aux ordinateurs de votre organisation ainsi qu'à ceux des organisations partenaires avec lesquelles vous avez collaboré lorsque vous exécutiez AD RMS.<br /><br />En outre, si vous avez déployé les [extensions d'appareil mobile](http://technet.microsoft.com/library/dn673574.aspx) pour prendre en charge des appareils mobiles tels que des téléphones et iPad iOS, des téléphones et tablettes Android, des téléphones Windows Phone et des ordinateurs Mac, vous devez supprimer les enregistrements SRV dans DNS, qui redirigeaient ces clients pour utiliser AD RMS.<br /><br />Pour obtenir des instructions, consultez [Étape 5. Reconfigurer les clients pour utiliser Azure RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step5Migration).|
|**6. Configurer l'intégration de l'IRM avec Exchange Online**|Cette étape est requise si vous souhaitez utiliser Exchange Online avec Azure RMS.<br /><br />Pour obtenir des instructions, consultez [Étape 6. Configurer l’intégration d’IRM pour Exchange Online](#BKMK_Step6Migration).|
|**7. Déployer le connecteur RMS**|Cette étape est requise si vous souhaitez utiliser l'un des services locaux suivants avec Azure RMS :<br /><br />Exchange Server (par exemple, règles de transport et Outlook Web Access)<br /><br />SharePoint Server<br /><br />Windows Server exécutant une infrastructure de classification des fichiers<br /><br />Pour obtenir des instructions, consultez [Étape 7. Déployer le connecteur RMS](#BKMK_Step7Migration).|
|**8. Désaffecter AD RMS**|Après avoir vérifié que tous les clients utilisent Azure RMS et n'accèdent plus aux serveurs AD RMS, vous pouvez désaffecter votre déploiement AD RMS.<br /><br />Pour obtenir des instructions, consultez [Étape 8. Désaffecter AD RMS](#BKMK_Step8Migration).|
|**9. Renouveler votre clé de client Azure RMS**|Cette étape est obligatoire si vous n'utilisiez pas le mode de chiffrement 2 avant la migration, et facultative mais recommandée pour toutes les migrations afin de protéger la sécurité de votre clé de client Azure RMS.<br /><br />Pour obtenir des instructions, consultez [Étape 9. Renouveler votre clé de client Azure RMS](#BKMK_Step9Migration).|

### <a name="BKMK_Step1Migration"></a>Étape 1 : Télécharger l’outil d’administration Azure Rights Management
Accédez au Centre de téléchargement Microsoft et [téléchargez l'outil d'administration Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), qui contient le module d'administration Azure RMS pour Windows PowerShell.

### <a name="BKMK_Step2Migration"></a>Étape 2. Exporter les données de configuration d'AD RMS, puis les importer dans Azure RMS
Cette étape est un processus comprenant deux phases :

1.  Exporter les données de configuration d'AD RMS en exportant les domaines de publication approuvés (TPD) dans un fichier .xml. Ce processus est identique pour toutes les migrations.

2.  Importer les données de configuration dans Azure RMS. Il existe différents processus pour cette étape, en fonction de la configuration actuelle de votre déploiement AD RMS et de votre topologie préférée pour votre clé de client Azure RMS.

#### Exportation des données de configuration d'AD RMS
Procédez comme suit sur tous les clusters AD RMS, pour tous les domaines de publication approuvés comprenant un contenu protégé pour votre organisation. Il est inutile d'exécuter cette procédure sur des clusters dédiés uniquement à la gestion des licences.

> [!NOTE]
> Si vous utilisez la gestion des droits Windows Server 2003, au lieu de ces instructions, suivez la procédure [Export SLC, TUD, TPD and RMS private key](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) (Exportation de clé privée SLC, TUD, TPD et RMS) décrite dans la rubrique [Migrating from Windows RMS to AD RMS in a Different Infrastructure](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) (Migration de Windows RMS vers AD RMS dans une autre infrastructure).

###### Pour exporter les données de configuration (informations du domaine de publication approuvé)

1.  Connectez-vous au cluster AD RMS en tant qu'utilisateur avec des autorisations d'administration AD RMS.

2.  À partir de la console de gestion AD RMS (**Active Directory Rights Management Services**), développez le nom du cluster AD RMS, **Stratégies d'approbation**, puis cliquez sur **Domaines de publication approuvés**.

3.  Dans le volet Résultats, sélectionnez le domaine de publication approuvé, puis, dans le volet Actions, cliquez sur **Exporter un domaine de publication approuvé**.

4.  Dans la boîte de dialogue **Exporter un domaine de publication approuvé** :

    -   Cliquez sur **Enregistrer sous** , puis définissez le chemin d'accès et le nom de fichier de votre choix. Spécifiez **.xml** comme extension de nom de fichier (l’extension n’est pas ajoutée automatiquement).

    -   Spécifiez et confirmez un mot de passe fort. N'oubliez pas ce mot de passe, car vous en aurez besoin ultérieurement pour importer les données de configuration dans Azure RMS.

    -   N'activez pas la case à cocher pour enregistrer le fichier de domaine approuvé dans RMS version 1.0.

Après avoir exporté tous les domaines de publication approuvés, vous pouvez commencer la procédure d'importation de ces données dans Azure RMS.

#### importation des données de configuration dans Azure RMS
La procédure exacte de cette étape dépend de la configuration actuelle de votre déploiement AD RMS, et de votre topologie préférée pour votre clé de client Azure RMS.

Votre déploiement AD RMS actuel utilisera l'une des configurations suivantes pour votre clé de certificat de licence serveur (SLC) :

-   Protection par mot de passe dans la base de données AD RMS Il s'agit de la configuration par défaut.

-   Protection HSM à l'aide d'un module de sécurité matériel Thales.

-   Protection HSM à l'aide d'un module de sécurité matériel d'un fournisseur que Thales.

-   Protection par mot de passe à l'aide d'un fournisseur de services de chiffrement externe.

> [!NOTE]
> Pour plus d'informations sur l'utilisation des modules de sécurité matériels avec AD RMS, consultez [Utilisation d'AD RMS avec des modules de sécurité matériels](http://technet.microsoft.com/library/jj651024.aspx).

Les deux options de topologie de clé de client Azure RMS sont les suivantes : Microsoft gère votre clé de client (**gérée par Microsoft**) ou vous la gérez vous-même (**gérée par le client**). Quand vous gérez votre propre clé de client Azure RMS, ce scénario parfois appelé BYOK (« Bring Your Own Key ») nécessite un module de sécurité matériel (HSM) de Thales. Pour plus d’informations, consultez la section [Choix de la topologie de clé de client : gestion Microsoft (par défaut) ou gestion BYOK](plan-implement-tenant-key.md#BKMK_ChooseTenantKey) dans la rubrique [Planification et implémentation de la clé de client Azure Rights Management](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Exchange Online n'est pas compatible actuellement avec la solution BYOK d'Azure RMS.  Si vous souhaitez utiliser la solution BYOK après la migration et envisagez d'utiliser Exchange Online, assurez-vous que vous comprenez la manière dont cette configuration réduit les fonctionnalités de l'IRM pour Exchange Online. Consultez les informations de la section [Tarifs et restrictions BYOK](plan-implement-tenant-key.md#BKMK_Pricing) de la rubrique [Planification et implémentation de la clé de client Azure Rights Management](plan-implement-tenant-key.md) pour vous aider à choisir la meilleure topologie de clé de client Azure RMS pour la migration.

Le tableau suivant permet d'identifier la procédure à utiliser pour votre migration. Les combinaisons non répertoriées ne sont pas prises en charge.

|Déploiement AD RMS actuel|Topologie de clé de client Azure RMS choisie|Instructions de migration|
|-----------------------------|----------------------------------------|--------------------------|
|Protection par mot de passe dans la base de données AD RMS|Gérée par Microsoft|Consultez la procédure **Migration de clé protégée par logiciel à clé protégée par logiciel** après ce tableau.<br /><br />Ce chemin de migration le plus simple nécessite uniquement que vous transfériez vos données de configuration vers Azure RMS.|
|Protection HSM à l'aide d'un module de sécurité matériel Thales nShield (HSM)|Gérée par le client (BYOK)|Consultez la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.<br /><br />Ceci nécessite l'ensemble d'outils BYOK et deux séries d'étapes pour transférer la clé de votre HSM local vers le HSM Azure RMS, puis transférer vos données de configuration vers Azure RMS.|
|Protection par mot de passe dans la base de données AD RMS|Gérée par le client (BYOK)|Consultez la procédure **Migration de clé protégée par logiciel à clé protégée par HSM** après ce tableau.<br /><br />Cela requiert l'ensemble d'outils BYOK et trois séries d'étapes pour extraire votre clé logicielle et l'importer dans un HSM local, transférer la clé de votre HSM local vers le HSM Azure RMS, puis transférer vos données de configuration vers Azure RMS.|
|Protection HSM à l'aide d'un module de sécurité matériel d'un fournisseur que Thales|Gérée par le client (BYOK)|Contactez le fournisseur de votre HSM pour obtenir des instructions concernant le transfert de votre clé de ce HSM vers un HSM nShield Thales. Suivez ensuite les instructions de la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.|
|Protection par mot de passe à l'aide d'un fournisseur de services de chiffrement externe|Gérée par le client (BYOK)|Contactez le fournisseur de votre HSM pour obtenir des instructions concernant le transfert de votre clé vers un HSM nShield Thales. Suivez ensuite les instructions de la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.|
Avant de commencer ces procédures, assurez-vous que vous avez accès aux fichiers .xml créés lors de l'exportation des domaines de publication approuvés. Par exemple, ceux-ci peuvent être enregistrés sur une clé USB que vous déplacez du serveur AD RMS vers la station de travail connectée à Internet.

> [!NOTE]
> Quelle que soit la manière dont vous stockez ces fichiers, suivez les meilleures pratiques pour les protéger, car ces données incluent votre clé privée.

##### Migration de clé protégée par logiciel à clé protégée par logiciel
Cette procédure permet d'importer la configuration d'AD RMS dans Azure RMS, de façon à ce que votre clé de client Azure RMS soit gérée par Microsoft.

###### Pour importer les données de configuration dans Azure RMS

1.  Sur une station de travail connectée à Internet, téléchargez et installez le module Windows PowerShell pour Azure RMS (version minimale 2.1.0.0), qui comprend l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx).

    > [!TIP]
    > Si vous avez précédemment téléchargé et installé le module, vérifiez le numéro de version en exécutant la commande suivante : `(Get-Module aadrm -ListAvailable).Version`

    Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

2.  Démarrez Windows PowerShell avec l'option **Exécuter en tant qu'administrateur** , puis utilisez l'applet de commande [Connect-AadrmService](http://msdn.microsoft.com/library/azure/dn629415.aspx) pour vous connecter au service Azure RMS :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (en général, vous utilisez un compte d’administrateur global pour Azure Active Directory ou Office 365).

3.  Utilisez l’applet de commande [Import-AadrmTpd](http://msdn.microsoft.com/library/azure/dn857523.aspx) pour charger le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -Active $True -Verbose
    ```
    Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

4.  Une fois la commande exécutée, répétez l'étape 3 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import. Par exemple : **Import-AadrmTpd -TpdFile E:\contosokey2.xml -ProtectionPassword -Active $false -Verbose**

5.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/azure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).

##### Migration de clé protégée par HSM à clé protégée par HSM

> [!NOTE]
> Ces instructions supposent que votre clé AD RMS est protégée par module. C’est le cas habituel. Si votre clé AD RMS est protégée par OCS, contactez [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) avant de suivre ces instructions.

Cette procédure en deux parties permet d'importer votre clé HSM et la configuration d'AD RMS dans Azure RMS pour que votre clé de client Azure RMS soit gérée par vous (scénario BYOK).

Vous devez d'abord empaqueter votre clé HSM pour la préparer au transfert vers Azure RMS, puis l'importer avec les données de configuration.

###### Partie 1 : empaquetage et transfert de votre clé HSM vers Azure RMS

1.  Suivez les étapes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md), à l’aide de la procédure **Générer et transférer votre clé de client par Internet** avec les exceptions suivantes :

    -   Ne suivez pas la procédure de **Génération de la clé de client**, car vous avez déjà l'équivalent de votre déploiement AD RMS. Vous devez identifier la clé utilisée par votre serveur AD RMS dans l'installation Thales, et utiliser cette clé lors de la migration. Les fichiers de clé chiffrés Thales sont généralement nommés **key_(keyAppName)_(keyIdentifier)** localement sur le serveur.

    -   Ne suivez pas la procédure de **Transfert de votre clé de client vers Azure RMS**, qui utilise la commande Add-AadrmKey.  Au lieu de cela, vous transférerez la clé HSM que vous avez préparée lors du téléchargement du domaine de publication approuvé exporté à l'aide de la commande Import-AadrmTpd.

2.  Sur la station de travail connectée à Internet, dans la session Windows PowerShell, reconnectez-vous au service Azure RMS.

Maintenant que vous avez préparé votre clé HSM pour Azure RMS, vous êtes prêt à importer votre fichier de clé HSM et les données de configuration d'AD RMS.

###### Partie 2 : importation de la clé HSM et des données de configuration dans Azure RMS

1.  Toujours sur la station de travail connectée à Internet et dans la session Windows PowerShell, téléchargez le premier fichier (.xml) de domaine de publication approuvé exporté. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté correspondant à la clé HSM que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    Par exemple : **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

2.  Une fois la commande exécutée, répétez l'étape 1 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import.  Par exemple : **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).

##### Migration de clé protégée par logiciel à clé protégée par HSM
Cette procédure en trois parties permet d'importer la configuration d'AD RMS dans Azure RMS pour que votre clé de client Azure RMS soit gérée par vous (scénario BYOK).

Vous devez extraire votre clé de certificat de licence serveur (SLC) des données de configuration, transférer la clé vers un HSM Thales local, empaqueter et transférer votre clé HSM vers Azure RMS, puis importer les données de configuration.

###### Première partie : Extraction de votre SLC à partir des données de configuration et importation de la clé dans votre HSM local

1.  Utilisez les étapes suivantes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md) :

    -   **Générer et transférer votre clé de client par Internet** : **préparation de la station de travail connectée à Internet**

    -   **Générer et transférer votre clé de client par Internet**: **préparation du poste de travail déconnecté**

    Ne suivez pas ces étapes pour générer votre clé de client, car vous avez déjà l'équivalent dans le fichier (.xml) de données de configuration exporté. Au lieu de cela, vous allez exécuter une commande pour extraire cette clé du fichier et l'importer dans votre HSM local.

2.  Sur la station de travail déconnectée, exécutez la commande suivante :

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Par exemple, pour l’Amérique du Nord : **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Informations supplémentaires :

    -   le paramètre ImportRmsCentrallyManagedKey indique que l'opération consiste à importer la clé SLC.

    -   Si vous n'avez pas spécifié le mot de passe dans la commande, vous êtes invité à l'entrer.

    -   Le paramètre KeyIdentifier est un nom convivial de clé, qui crée le nom de fichier de clé. Vous devez utiliser uniquement des caractères ASCII minuscules.

    -   Le paramètre ExchangeKeyPackage spécifie un package de clé d'échange de clés (KEK) spécifique d'une région, dont le nom commence par BYOK-KEK-pkg-.

    -   Le paramètre NewSecurityWorldPackage spécifie un package de monde de sécurité spécifique d'une région, dont le nom commence par BYOK-SecurityWorld-pkg-.

    Cette commande renvoie les éléments suivants :

    -   Un fichier de clé HSM : %NFAST_KMDATA%\local\key_mscapi_&lt;ID_clé&gt;

    -   Fichier de données de configuration RMS avec le certificat de licence serveur supprimé : %NFAST_KMDATA%\local\no_key_tpd_&lt;ID_clé&gt;.xml

3.  Si vous avez plusieurs fichiers de données de configuration RMS, répétez l'étape 2 pour les autres fichiers.

Maintenant que votre SLC a été extrait et converti en clé basée sur HSM, vous êtes prêt à empaqueter et à transférer celle-ci vers Azure RMS.

###### Partie 2 : empaquetage et transfert de votre clé HSM vers Azure RMS

1.  Utilisez les étapes suivantes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md) :

    -   **Générer et transférer votre clé de client par Internet**: **préparation de la clé de client pour le transfert**

    -   **Générer et transférer votre clé de client par Internet**: **transfert de votre clé de client vers Azure RMS**

Maintenant que vous avez transféré votre clé HSM vers Azure RMS, vous êtes prêt à importer vos données de configuration AD RMS, qui contiennent uniquement un pointeur vers la clé de client qui vient d'être transférée.

###### Partie 3 : importation des données de configuration dans Azure RMS

1.  Toujours sur la station de travail connectée à Internet et dans la session Windows PowerShell, recopiez les fichiers de configuration RMS avec le SLC supprimé (à partir de la station de travail déconnectée, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Téléchargez le premier fichier. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté correspondant à la clé HSM que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Par exemple : **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

3.  Une fois la commande exécutée, répétez l'étape 2 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import. Par exemple : **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).

### <a name="BKMK_Step3Migration"></a>Étape 3. Activer votre client RMS
Les instructions complètes pour cette étape figurent dans la rubrique [Activation d’Azure Rights Management](activate-service.md).

> [!TIP]
> Si vous avez un abonnement Office 365, vous pouvez activer Azure RMS à partir du Centre d’administration Office 365 ou du portail Azure Classic. Nous vous recommandons d’utiliser le portail Azure Classic, car vous allez l’utiliser pour exécuter l’étape suivante.

**Que se passe-t-il si votre client Azure RMS est déjà activé ?** Si le service Azure RMS est déjà activé pour votre organisation, les utilisateurs ont peut-être déjà utilisé Azure RMS pour protéger du contenu avec une clé de client générée automatiquement (et les modèles par défaut) au lieu de vos clés existantes (et les modèles associés) d’AD RMS. Il est peu probable que cela se produise sur des ordinateurs bien gérés sur votre intranet, car ceux-ci sont automatiquement configurés pour votre infrastructure AD RMS. En revanche, cela peut se produire sur des ordinateurs de groupe de travail ou des ordinateurs qui se connectent rarement à votre intranet. Malheureusement, il est également difficile d'identifier ces ordinateurs. C'est pourquoi nous vous recommandons de ne pas activer le service avant d'importer les données de configuration d'AD RMS.

Si votre client Azure RMS est déjà activé et que vous pouvez identifier ces ordinateurs, exécutez le script CleanUpRMS_RUN_Elevated.cmd sur ces ordinateurs, comme décrit à l’Étape 5. L'exécution de ce script force ceux-ci à réinitialiser l'environnement utilisateur, de sorte qu'ils téléchargent la clé de client et les modèles importés mis à jour.

### <a name="BKMK_Step4Migration"></a>Étape 4. Configurer les modèles importés
Étant donné que l'état par défaut des modèles importés est **Archivé**, vous devez définir cet état sur **Publié** si vous souhaitez que les utilisateurs soient en mesure de les utiliser avec Azure RMS.

De plus, si vos modèles AD RMS utilisaient le groupe **ANYONE**, ce groupe est automatiquement supprimé pendant l’importation des modèles dans Azure RMS. Vous devez ajouter manuellement le groupe ou les utilisateurs équivalents et les mêmes droits aux modèles importés. Le nom du groupe équivalent pour Azure RMS est **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<nom_client>.onmicrosoft.com**. Par exemple, ce groupe peut se présenter comme suit pour Contoso : **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Si vous n’êtes pas certain que vos modèles AD RMS incluent le groupe ANYONE, développez la section [Exemple de script Windows PowerShell permettant d’identifier les modèles AD RMS qui incluent le groupe ANYONE](#BKMK_ScriptForANYONE) de cette étape pour copier et utiliser l’exemple de script PowerShell afin d’identifier ces modèles. Pour plus d’informations sur l’utilisation de Windows PowerShell avec AD RMS, consultez [Using Windows PowerShell to Administer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx) (Utilisation de Windows PowerShell pour administrer AD RMS).

Vous pouvez afficher le groupe créé automatiquement pour votre organisation si vous copiez l’un des modèles de stratégie de droits par défaut dans le portail Azure Classic et que vous identifiez ensuite le **NOM D’UTILISATEUR** dans la page **DROITS**. En revanche, vous ne pouvez pas ajouter ce groupe à un modèle créé ou importé manuellement à partir du portail Azure Classic et devez utiliser l’une des options PowerShell d’Azure RMS suivantes :

-   Utilisez l’applet de commande PowerShell [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour définir le groupe et les droits « AllStaff » en tant qu’objet de définition de droits, puis réexécutez cette commande pour chacun des autres groupes ou utilisateurs déjà dotés de droits dans le modèle d’origine, outre le groupe ANYONE. Ajoutez ensuite ces objets de définition de droits aux modèles à l’aide de l’applet de commande [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx).

-   Utilisez l’applet de commande [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) pour exporter le modèle vers un fichier .XML que vous pourrez modifier pour ajouter le groupe et les droits « AllStaff » aux groupes et droits existants, puis utilisez l’applet de commande [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) pour réimporter cette modification dans Azure RMS.

> [!NOTE]
> Ce groupe équivalent « AllStaff » n’est pas exactement identique au groupe ANYONE dans AD RMS : Le groupe « AllStaff » comprend tous les utilisateurs de votre client Azure, alors que le groupe ANYONE comprend tous les utilisateurs authentifiés, qui pourraient être extérieurs à votre organisation.
> 
> Compte tenu de cette différence entre les deux groupes, vous pouvez aussi être amené à ajouter des utilisateurs externes, en plus du groupe « AllStaff ». Les adresses de messagerie externes ne sont pas actuellement prises en charge pour les groupes.

Les modèles que vous importez à partir d’AD RMS ressemblent et se comportent comme des modèles personnalisés que vous pouvez créer dans le portail Azure Classic. Pour convertir des modèles importés en modèles publiés pour que les utilisateurs puissent les afficher et les sélectionner à partir d’applications, ou pour apporter d’autres modifications aux modèles, consultez [Configuration de modèles personnalisés pour Azure Rights Management](configure-custom-templates.md).

> [!TIP]
> Pour offrir une expérience plus cohérente aux utilisateurs pendant le processus de migration, n’apportez pas de modifications aux modèles importés hormis ces deux modifications. De même, et évitez de publier les deux modèles par défaut fournis avec Azure RMS ou d’en créer des nouveaux à ce stade. Au lieu de cela, attendez que le processus de migration soit terminé et d'avoir désaffecté les serveurs AD RMS.

#### <a name="BKMK_ScriptForANYONE"></a>Exemple de script Windows PowerShell permettant d’identifier les modèles AD RMS qui incluent le groupe ANYONE
Cette section contient l’exemple de script qui vous permet d’identifier les modèles AD RMS pour lesquels le groupe ANYONE a été défini, comme décrit dans la section précédente.

**Exclusion de responsabilité** : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d’aucune sorte.*

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```

### <a name="BKMK_Step5Migration"></a>Étape 5. Reconfigurer les clients pour utiliser Azure RMS
Pour des clients Windows :

1.  [Téléchargez les scripts de migration](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Ces scripts réinitialisent la configuration sur des ordinateurs Windows afin qu'ils utilisent le service RMS Azure plutôt qu'AD RMS.

2.  Suivez les instructions du script de redirection (Redirect_OnPrem.cmd) pour modifier celui-ci pour qu’il pointe sur votre nouveau client Azure RMS.

3.  Sur les ordinateurs Windows, exécutez ces scripts avec des privilèges élevés dans le contexte de l'utilisateur.

Pour des clients appareils mobiles et des ordinateurs Mac :

-   Supprimez les enregistrements SRV DNS que vous avez créés lors du déploiement de l’ [extension d'appareil mobile AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Modifications apportées par les scripts de migration
Cette section décrit les modifications apportées par les scripts de migration. Vous pouvez utiliser ces informations uniquement à des fins de référence ou de dépannage, ou si vous voulez apporter personnellement ces modifications.

CleanUpRMS_RUN_Elevated.cmd :

-   Supprimez le contenu des dossiers %userprofile%\AppData\Local\Microsoft\DRM et %userprofile%\AppData\Local\Microsoft\MSIPC, y compris les sous-dossiers et fichiers portant un nom long.

-   Supprimez le contenu des clés de Registre suivantes :

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Supprimez les valeurs de Registre suivantes :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd :

-   Créez les valeurs de Registre suivantes pour chaque URL fournie en tant que paramètre sous chacun des emplacements suivants :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Chaque entrée a une valeur REG_SZ **https://OldRMSserverURL/_wmcs/licensing**, dont les données sont au format suivant : **https://&lt;URL_votre_client&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;URL_votre_client&gt;* a le format suivant : **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Par exemple : 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Vous pouvez trouver cette valeur en identifiant la valeur **RightsManagementServiceId** lorsque vous exécutez l'applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS.

### <a name="BKMK_Step6Migration"></a>Étape 6. Configurer l'intégration de l'IRM pour Exchange Online
Si vous avez précédemment importé votre TDP d'AD RMS dans Exchange Online, vous devez supprimer cette TDP pour éviter des conflits de modèles et de stratégies après la migration vers Azure RMS. Pour ce faire, utilisez l’applet de commande [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) d’Exchange Online.

Si vous avez choisi une topologie de clé de locataire Azure RMS **gérée par Microsoft**:

-   Consultez la section [Exchange Online : Configuration IRM](configure-applications.md#BKMK_ExchangeOnline) de la rubrique [Configuration des applications pour Azure Rights Management](configure-applications.md). Cette section inclut des commandes spécifiques à exécuter, qui établissent une connexion au service Exchange Online, importent la clé de locataire d'Azure RMS, et activent les fonctionnalités de l'IRM pour Exchange Online. Après avoir effectué ces étapes, vous disposez de toutes les fonctionnalités RMS avec Exchange Online.

Si vous avez choisi une topologie de clé de client Azure RMS **gérée par le client (BYOK)** :

-   Vous avez moins de fonctionnalités RMS avec Exchange Online, comme décrit dans la section [Tarifs et restrictions BYOK](plan-implement-tenant-key.md#BKMK_Pricing) de la rubrique [Planification et implémentation de la clé de client Azure Rights Management](plan-implement-tenant-key.md).

### <a name="BKMK_Step7Migration"></a>Étape 7. Déployer le connecteur RMS
Si vous avez utilisé la fonctionnalité Information Rights Management (IRM) d'Exchange Server ou de SharePoint Server avec AD RMS, vous devez d'abord désactiver l'IRM sur ces serveurs, puis supprimer la configuration AD RMS. Ensuite, déployez le connecteur Rights Management (RMS), qui agit comme interface de communication (relais) entre les serveurs locaux et Azure RMS.

Enfin, pour cette étape, si vous avez importé plusieurs TPD dans Azure RMS, qui ont été utilisés pour protéger des messages électroniques, vous devez modifier manuellement le Registre sur les ordinateurs Exchange Server afin de rediriger toutes les URL de TPD vers le connecteur RMS.

> [!NOTE]
> Avant de commencer, vérifiez les versions des serveurs locaux que le connecteur RMS prend en charge dans « Serveurs locaux prenant en charge Azure RMS » de la section [Applications prenant en charge Azure RMS](requirements-azure-rms.md#BKMK_SupportedApplications) de la rubrique [Configuration requise pour Azure Rights Management](requirements-azure-rms.md).

##### Désactivation de l'IRM sur les serveurs Exchange et suppression de la configuration AD RMS

1.  Sur chaque serveur Exchange, recherchez le dossier suivant, puis supprimez toutes ses entrées : \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  Sur l'un des serveurs Exchange, commencez par utiliser l'applet de commande [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) pour désactiver les fonctionnalités de l'IRM pour les messages envoyés à des destinataires internes :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Puis, utilisez la même applet de commande pour désactiver les fonctionnalités IRM pour les messages envoyés à des destinataires externes :

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Ensuite, utilisez la même applet de commande pour désactiver IRM dans Microsoft Office Outlook Web App et dans Microsoft Exchange ActiveSync :

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Enfin, utilisez la même applet de commande pour effacer les certificats mis en cache :

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  Sur chaque serveur Exchange, réinitialisez IIS, par exemple, en exécutant une invite de commandes en tant qu’administrateur et en tapant **iisreset**.

##### Désactivation d'IRM sur les serveurs SharePoint et suppression de la configuration AD RMS

1.  Assurez-vous qu'aucun document n'est extrait des bibliothèques protégées par RMS. Les documents extraits deviendront inaccessibles à la fin de cette procédure.

2.  Sur le site web Administration centrale de SharePoint, dans la section **Lancement rapide** , cliquez sur **Sécurité**.

3.  Dans la page **Sécurité** , dans la section **Stratégie d'information** , cliquez sur **Configurer la gestion des droits relatifs à l'information**.

4.  Dans la page **Gestion des droits relatifs à l'information** , dans la section **Gestion des droits relatifs à l'information** , sélectionnez **Ne pas utiliser IRM sur ce serveur**, puis cliquez sur **OK**.

5.  Sur chaque ordinateur SharePoint Server, supprimez le contenu du dossier \ProgramData\Microsoft\MSIPC\Server\*&lt;SID du compte exécutant SharePoint Server&gt;*.

##### Installation et configuration du connecteur RMS

-   Suivez les instructions de la rubrique [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

##### Pour Exchange uniquement et plusieurs TPD : modifier le Registre

-   Sur chaque serveur Exchange, ajoutez manuellement les clés de Registre suivantes pour chaque TPD que vous avez importé afin de rediriger les URL de TPD vers le connecteur RMS. Ces entrées de Registre sont spécifiques de la migration et ne sont pas ajoutées par l'outil de configuration de serveur pour le connecteur Microsoft RMS.

    Lorsque vous apportez ces modifications au Registre, suivez les instructions suivantes :

    -   Remplacez *ConnectorFQDN* par le nom défini dans le DNS pour le connecteur. Par exemple, **rmsconnector.contoso.com**.

    -   Utilisez le préfixe HTTP ou HTTPS pour l'URL du connecteur, selon que vous avez configuré le connecteur pour utiliser le protocole HTTP ou HTTPS pour communiquer avec vos serveurs locaux.

    **Pour Exchange 2013 :**

    |Chemin d'accès au registre|Type|Valeur|Niveau|
    |-----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;URL de gestion des licences intranet AD RMS&gt;/_wmcs/licensing|L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :<br /><br />http://&lt;FQDNDuConnecteur&gt;/_wmcs/licensing<br /><br />https://&lt;NomDuConnecteur&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;URL de gestion des licences extranet AD RMS&gt;/_wmcs/licensing|L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :<br /><br />http://&lt;FQDNDuConnecteur&gt;/_wmcs/licensing<br /><br />https://&lt;FQDNDuConnecteur&gt;/_wmcs/licensing|
    **Pour Exchange Server 2010 :**

    |Chemin d'accès au registre|Type|Valeur|Niveau|
    |-----------------|--------|---------|--------|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;URL de gestion des licences intranet AD RMS&gt;/_wmcs/licensing|L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :<br /><br />http://&lt;NomDuConnecteur&gt;/_wmcs/licensing<br /><br />https://&lt;NomDuConnecteur&gt;/_wmcs/licensing|
    |HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection|Reg_SZ|https://&lt;URL de gestion des licences extranet AD RMS&gt;/_wmcs/licensing|L'une des options suivantes, selon que vous utilisez le protocole HTTP ou HTTPS entre votre serveur Exchange et votre connecteur RMS :<br /><br />http://&lt;NomDuConnecteur&gt;/_wmcs/licensing<br /><br />https://&lt;NomDuConnecteur&gt;/_wmcs/licensing|

Une fois ces procédures terminées, lisez la section **Étapes suivantes** de la rubrique [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

### <a name="BKMK_Step8Migration"></a>Étape 8. Désaffecter AD RMS
Facultatif : Supprimez le point de connexion de service d’Active Directory pour empêcher des ordinateurs de découvrir votre infrastructure Rights Management locale. Cela est facultatif en raison de la redirection que vous avez configurée dans le Registre (par exemple, en exécutant le script de migration). Pour supprimer le point de connexion de service, utilisez l'outil AD SCP Register de la [Boîte à outil d'Administration des services Rights Management](http://www.microsoft.com/download/details.aspx?id=1479).

Surveillez l’activité de vos serveurs AD RMS, par exemple, en vérifiant [les demandes dans le rapport d’intégrité système](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [Table ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) ou [l’audit de l’accès utilisateur au contenu protégé](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Après avoir confirmé que les clients RMS ne communiquent plus avec ces serveurs, et que les clients utilisent avec succès Azure RMS, vous pouvez supprimer le rôle serveur AD RMS de ces serveurs. Si vous utilisez des serveurs dédiés, vous pouvez prendre la précaution de les arrêter pendant un certain temps pour vous assurer qu'aucun problème n'est signalé, qui pourrait nécessiter un redémarrage de ces serveurs pour garantir la continuité de service pendant que vous étudiez la raison pour laquelle les clients n'utilisent pas Azure RMS.

Après la désaffectation de vos serveurs AD RMS, vous pouvez réviser vos modèles dans le portail Azure Classic et les consolider afin que les utilisateurs aient moins de choix, les reconfigurer ou même ajouter de nouveaux modèles. Il serait également judicieux de publier les modèles par défaut. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour Azure Rights Management](configure-custom-templates.md).

### <a name="BKMK_Step9Migration"></a>Étape 9. Renouveler votre clé de client Azure RMS
Cette étape est obligatoire une fois la migration terminée si votre déploiement AD RMS utilisait le mode de chiffrement RMS 1, car le renouvellement de clé crée une clé de client qui utilise le mode de chiffrement RMS 2. L'utilisation d'Azure RMS avec le mode de chiffrement 1 est prise en charge uniquement pendant le processus de migration.

Cette étape est facultative mais recommandée une fois la migration terminée, même si vous utilisiez le mode de chiffrement RMS 2, car elle permet de sécuriser votre clé de client Azure RMS contre d'éventuelles failles de sécurité de votre clé AD RMS. Quand vous renouvelez votre clé de client Azure RMS (« déploiement de la clé »), une nouvelle clé est créée et la clé d'origine est archivée. Toutefois, étant donné que le basculement d'une clé à l'autre ne se produit pas immédiatement mais en quelques semaines, n'attendez pas de soupçonner une violation de votre clé d'origine, mais renouvelez votre clé de client RMS dès la fin de la migration.

Pour renouveler votre clé de client Azure RMS :

-   Si votre clé de client RMS est gérée par Microsoft : Appelez les services de support technique Microsoft (CSS) et prouvez que vous êtes l'administrateur du client RMS.

-   Si votre clé de client RMS est gérée par vous (BYOK) : Répétez la procédure BYOK pour générer et créer une clé sur Internet ou en personne.

Pour plus d’informations sur la gestion de votre clé de client RMS, consultez [Opérations pour votre clé de client Azure Rights Management](operations-tenant-key.md).

## Voir aussi
[Configuration d'Azure Rights Management](configuring-azure-rights-management.md)



<!--HONumber=Apr16_HO3-->


