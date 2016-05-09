---
# required metadata

title: Migration d’AD RMS vers Azure Rights Management - Phase 1 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Phase de migration 1 : Configuration côté serveur pour AD RMS
Utilisez les informations suivantes pour la Phase 1 de la migration d’AD RMS vers Azure Rights Management (Azure RMS). Ces procédures couvrent les étapes 1 à 4 de [Migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Étape 1 : Télécharger l’outil d’administration Azure Rights Management
Accédez au Centre de téléchargement Microsoft et [téléchargez l'outil d'administration Azure Rights Management](http://go.microsoft.com/fwlink/?LinkId=257721), qui contient le module d'administration Azure RMS pour Windows PowerShell.

Installez l’outil. Pour obtenir des instructions, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

## Étape 2. Exporter les données de configuration d'AD RMS, puis les importer dans Azure RMS
Cette étape est un processus comprenant deux phases :

1.  Exporter les données de configuration d'AD RMS en exportant les domaines de publication approuvés (TPD) dans un fichier .xml. Ce processus est identique pour toutes les migrations.

2.  Importer les données de configuration dans Azure RMS. Il existe différents processus pour cette étape, en fonction de la configuration actuelle de votre déploiement AD RMS et de votre topologie préférée pour votre clé de client Azure RMS.

### Exportation des données de configuration d'AD RMS
Procédez comme suit sur tous les clusters AD RMS, pour tous les domaines de publication approuvés comprenant un contenu protégé pour votre organisation. Il est inutile d'exécuter cette procédure sur des clusters dédiés uniquement à la gestion des licences.

> [!NOTE]
> Si vous utilisez la gestion des droits Windows Server 2003, au lieu de ces instructions, appliquez la procédure [Exportation de clé privée SLC, TUD, TPD et RMS](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx) décrite dans la rubrique [Migration de Windows RMS vers AD RMS dans une autre Infrastructure](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx).

#### Pour exporter les données de configuration (informations du domaine de publication approuvé)

1.  Connectez-vous au cluster AD RMS en tant qu'utilisateur avec des autorisations d'administration AD RMS.

2.  À partir de la console de gestion AD RMS (**Active Directory Rights Management Services**), développez le nom du cluster AD RMS, **Stratégies d'approbation**, puis cliquez sur **Domaines de publication approuvés**.

3.  Dans le volet Résultats, sélectionnez le domaine de publication approuvé, puis, dans le volet Actions, cliquez sur **Exporter un domaine de publication approuvé**.

4.  Dans la boîte de dialogue **Exporter un domaine de publication approuvé** :

    -   Cliquez sur **Enregistrer sous** , puis définissez le chemin d'accès et le nom de fichier de votre choix. Veillez à spécifier **.xml** comme extension de nom de fichier (l’extension n’est pas ajoutée automatiquement).

    -   Spécifiez et confirmez un mot de passe fort. N'oubliez pas ce mot de passe, car vous en aurez besoin ultérieurement pour importer les données de configuration dans Azure RMS.

    -   N'activez pas la case à cocher pour enregistrer le fichier de domaine approuvé dans RMS version 1.0.

Après avoir exporté tous les domaines de publication approuvés, vous pouvez commencer la procédure d’importation de ces données dans Azure RMS. Pour plus d’informations, 

### importation des données de configuration dans Azure RMS
La procédure exacte de cette étape dépend de la configuration actuelle de votre déploiement AD RMS, et de votre topologie préférée pour votre clé de client Azure RMS.

Votre déploiement AD RMS actuel utilisera l'une des configurations suivantes pour votre clé de certificat de licence serveur (SLC) :

-   Protection par mot de passe dans la base de données AD RMS Il s'agit de la configuration par défaut.

-   Protection HSM à l'aide d'un module de sécurité matériel Thales.

-   Protection HSM à l'aide d'un module de sécurité matériel d'un fournisseur que Thales.

-   Protection par mot de passe à l'aide d'un fournisseur de services de chiffrement externe.

> [!NOTE]
> Pour plus d'informations sur l'utilisation des modules de sécurité matériels avec AD RMS, consultez [Utilisation d'AD RMS avec des modules de sécurité matériels](http://technet.microsoft.com/library/jj651024.aspx).

Les deux options de topologie de clé de locataire Azure RMS sont les suivantes : Microsoft gère votre clé de locataire (**gérée par Microsoft**) ou vous la gérez vous-même (**gérée par le client**). Quand vous gérez votre propre clé de locataire Azure RMS, ce scénario parfois appelé BYOK (« Bring Your Own Key ») nécessite un module de sécurité matériel (HSM) de Thales. Pour plus d’informations, consultez l’article [Planification et implémentation de la clé de locataire Azure Rights Management](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Exchange Online n'est pas compatible actuellement avec la solution BYOK d'Azure RMS.  Si vous souhaitez utiliser la solution BYOK après la migration et envisagez d'utiliser Exchange Online, assurez-vous que vous comprenez la manière dont cette configuration réduit les fonctionnalités de l'IRM pour Exchange Online. Passez en revue les informations contenues dans la section [Tarifs et restrictions BYOK](byok-price-restrictions.md) pour choisir la meilleure topologie de clé de locataire Azure RMS pour votre migration.

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


Pour effectuer l’Étape 2, sélectionnez les instructions correspondant à votre chemin de migration : 


- [Clé logicielle à clé logicielle](migrate-softwarekey-to-softwarekey.md)
- [Clé HSM à clé HSM](migrate-hsmkey-to-hsmkey.md)
- [Clé logicielle à clé HSM](migrate-softwarekey-to-hsmkey.md)


<<<<<<< HEAD
## Étape 3. Activer votre locataire Azure RMS
Les instructions complètes pour cette étape figurent dans l’article [Activation d’Azure Rights Management](../deploy-use/activate-azure-classic.md).
=======
## Étape 3. Activer votre client RMS
Les instructions complètes pour cette étape figurent dans l’article [Activation d’Azure Rights Management](../deploy-use/activate-service.md).
>>>>>>> 32b7eccb741760c33bf45a2ce253454827c6d6ba

> [!TIP]
> Si vous avez un abonnement Office 365, vous pouvez activer Azure RMS à partir du Centre d’administration Office 365 ou du portail Azure Classic. Nous vous recommandons d’utiliser le portail Azure Classic, car vous allez l’utiliser pour exécuter l’étape suivante.

**Que se passe-t-il si votre locataire Azure RMS est déjà activé ?** Si le service Azure RMS est déjà activé pour votre organisation, les utilisateurs ont peut-être déjà utilisé Azure RMS pour protéger du contenu avec une clé de locataire générée automatiquement (et les modèles par défaut) au lieu de vos clés existantes (et les modèles associés) d’AD RMS. Il est peu probable que cela se produise sur des ordinateurs bien gérés sur votre intranet, car ceux-ci sont automatiquement configurés pour votre infrastructure AD RMS. En revanche, cela peut se produire sur des ordinateurs de groupe de travail ou des ordinateurs qui se connectent rarement à votre intranet. Malheureusement, il est également difficile d'identifier ces ordinateurs. C'est pourquoi nous vous recommandons de ne pas activer le service avant d'importer les données de configuration d'AD RMS.

Si votre locataire Azure RMS est déjà activé et que vous pouvez identifier ces ordinateurs, veillez à exécuter le script CleanUpRMS_RUN_Elevated.cmd sur ces ordinateurs, comme décrit à l’Étape 5. L'exécution de ce script force ceux-ci à réinitialiser l'environnement utilisateur, de sorte qu'ils téléchargent la clé de client et les modèles importés mis à jour.

## Étape 4. Configurer les modèles importés
Étant donné que l'état par défaut des modèles importés est **Archivé**, vous devez définir cet état sur **Publié** si vous souhaitez que les utilisateurs soient en mesure de les utiliser avec Azure RMS.

De plus, si vos modèles AD RMS utilisaient le groupe **ANYONE**, ce groupe est automatiquement supprimé pendant l’importation des modèles dans Azure RMS ; vous devez ajouter manuellement le groupe ou les utilisateurs équivalents et les mêmes droits aux modèles importés. Le groupe équivalent pour Azure RMS se nomme **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<nom_locataire>.onmicrosoft.com**. Par exemple, ce groupe peut se présenter comme suit pour Contoso : **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Si vous n’êtes pas sûr que vos modèles AD RMS incluent le groupe ANYONE, vous pouvez utiliser l’exemple de script Windows PowerShell pour identifier ces modèles. Pour plus d’informations sur l’utilisation de Windows PowerShell avec AD RMS, consultez [Utilisation de Windows PowerShell pour administrer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

Vous pouvez voir le groupe créé automatiquement pour votre organisation si vous copiez l’un des modèles de stratégie de droits par défaut dans le portail Azure Classic, et que vous identifiez ensuite le **NOM D’UTILISATEUR** dans la page **DROITS**. En revanche, vous ne pouvez pas ajouter ce groupe à un modèle créé ou importé manuellement à partir du portail Azure Classic et devez utiliser l’une des options PowerShell d’Azure RMS suivantes :

-   Utilisez l’applet de commande PowerShell [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour définir le groupe et les droits « AllStaff » en tant qu’objet de définition de droits, puis réexécutez cette commande pour chacun des autres groupes ou utilisateurs déjà dotés de droits dans le modèle d’origine, outre le groupe ANYONE. Ajoutez ensuite ces objets de définition de droits aux modèles à l’aide de l’applet de commande [Set-AadrmTemplateProperty](https://msdn.microsoft.com/en-us/library/azure/dn727076.aspx).

-   Utilisez l’applet de commande [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) pour exporter le modèle vers un fichier .XML que vous pourrez modifier pour ajouter le groupe et les droits « AllStaff » aux groupes et droits existants, puis utilisez l’applet de commande [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) pour réimporter cette modification dans Azure RMS.

> [!NOTE]
> Ce groupe équivalent « AllStaff » n’est pas exactement identique au groupe ANYONE dans AD RMS : le groupe « AllStaff » comprend tous les utilisateurs de votre client Azure, alors que le groupe ANYONE comprend tous les utilisateurs authentifiés, qui pourraient être extérieurs à votre organisation.
> 
> Compte tenu de cette différence entre les deux groupes, vous pouvez aussi être amené à ajouter des utilisateurs externes, en plus du groupe « AllStaff ». Les adresses de messagerie externes ne sont pas actuellement prises en charge pour les groupes.

Les modèles que vous importez à partir d’AD RMS ressemblent et se comportent comme des modèles personnalisés que vous pouvez créer dans le portail Azure Classic. Pour convertir des modèles importés en modèles publiés pour que les utilisateurs puissent les afficher et les sélectionner à partir d’applications, ou pour apporter d’autres modifications aux modèles, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

> [!TIP]
> Pour offrir une expérience plus cohérente aux utilisateurs pendant le processus de migration, n’apportez pas de modifications aux modèles importés hormis ces deux modifications. De même, et évitez de publier les deux modèles par défaut fournis avec Azure RMS ou d’en créer des nouveaux à ce stade. Au lieu de cela, attendez que le processus de migration soit terminé et d'avoir désaffecté les serveurs AD RMS.

### Exemple de script Windows PowerShell permettant d’identifier les modèles AD RMS qui incluent le groupe ANYONE
Cette section contient l’exemple de script qui vous permet d’identifier les modèles AD RMS pour lesquels le groupe ANYONE a été défini, comme décrit dans la section précédente.

**Exclusion de responsabilité** : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d’aucune sorte.*

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


## Étapes suivantes
Passez à la [Phase 2 : Configuration côté client](migrate-from-ad-rms-phase2.md).



<!--HONumber=Apr16_HO3-->


