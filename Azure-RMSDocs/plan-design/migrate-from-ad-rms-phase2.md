---
title: Migrer un déploiement AD RMS vers Azure Information Protection - Phase 2
description: Phase 2 de la migration d’AD RMS vers Azure Information Protection, couvrant les étapes 4 à 6 de la migration d’AD RMS vers Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 033504a26ae04bae3e4f1179503855bcfce63d73
ms.sourcegitcommit: 0fda9ea4a7b91d4bb3a9e4f9d5cc4106ce1e2d43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38973400"
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>Phase de migration 2 : Configuration côté serveur pour AD RMS

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations suivantes pour la Phase 2 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent les étapes 4 à 6 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>Étape 4. Exporter les données de configuration d’AD RMS, puis les importer dans Azure Information Protection
Cette étape est un processus comprenant deux phases :

1. Exporter les données de configuration d'AD RMS en exportant les domaines de publication approuvés (TPD) dans un fichier .xml. Ce processus est identique pour toutes les migrations.

2. Importez les données de configuration dans Azure Information Protection. Il existe différents processus pour cette étape, en fonction de la configuration actuelle de votre déploiement AD RMS et de votre topologie préférée pour votre clé de client Azure RMS.

### <a name="export-the-configuration-data-from-ad-rms"></a>Exportation des données de configuration d'AD RMS

Procédez comme suit sur tous les clusters AD RMS, pour tous les domaines de publication approuvés comprenant un contenu protégé pour votre organisation. Il est inutile d’exécuter cette procédure sur des clusters dédiés uniquement à la gestion des licences.

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>Pour exporter les données de configuration (informations du domaine de publication approuvé)

1. Connectez-vous au cluster AD RMS en tant qu'utilisateur avec des autorisations d'administration AD RMS.

2. À partir de la console de gestion AD RMS (**Active Directory Rights Management Services**), développez le nom du cluster AD RMS, **Stratégies d'approbation**, puis cliquez sur **Domaines de publication approuvés**.

3. Dans le volet Résultats, sélectionnez le domaine de publication approuvé, puis, dans le volet Actions, cliquez sur **Exporter un domaine de publication approuvé**.

4. Dans la boîte de dialogue **Exporter un domaine de publication approuvé** :

    - Cliquez sur **Enregistrer sous**, puis définissez le chemin d'accès et le nom de fichier de votre choix. Spécifiez **.xml** comme extension de nom de fichier (l’extension n’est pas ajoutée automatiquement).

    - Spécifiez et confirmez un mot de passe fort. N’oubliez pas ce mot de passe, car vous en aurez besoin ultérieurement pour importer les données de configuration dans Azure Information Protection.

    - N'activez pas la case à cocher pour enregistrer le fichier de domaine approuvé dans RMS version 1.0.

Après avoir exporté tous les domaines de publication approuvés, vous pouvez commencer la procédure d’importation de ces données dans Azure Information Protection.

Notez que les domaines de publication approuvés incluent les clés de certificat de licence serveur (SLC) pour déchiffrer les fichiers précédemment protégés. Il est donc important d’exporter (et d’importer ultérieurement dans Azure) tous les domaines de publication approuvés et pas uniquement le domaine actuellement actif.

Par exemple, vous aurez plusieurs domaines de publication approuvés si vous mettez à niveau vos serveurs AD RMS du Mode de chiffrement 1 au Mode de chiffrement 2. Si vous n’exportez et n’importez pas le domaine de publication approuvé qui contient votre clé archivée qui utilisait le Mode de chiffrement 1, les utilisateurs ne seront pas en mesure d’ouvrir le contenu protégé avec la clé du Mode de chiffrement 1 après la migration.


### <a name="import-the-configuration-data-to-azure-information-protection"></a>Importer les données de configuration dans Azure Information Protection
La procédure exacte de cette étape dépend de la configuration actuelle de votre déploiement AD RMS, ainsi que de votre topologie préférée pour votre clé de propriétaire Azure Information Protection.

Votre déploiement AD RMS actuel utilise l’une des configurations suivantes pour votre clé de certificat de licence serveur (SLC) :

- Protection par mot de passe dans la base de données AD RMS. Il s'agit de la configuration par défaut.

- Protection HSM à l'aide d'un module de sécurité matériel Thales.

- Protection HSM à l'aide d'un module de sécurité matériel d'un fournisseur que Thales.

- Protection par mot de passe à l'aide d'un fournisseur de services de chiffrement externe.

> [!NOTE]
> Pour plus d'informations sur l'utilisation des modules de sécurité matériels avec AD RMS, consultez [Utilisation d'AD RMS avec des modules de sécurité matériels](http://technet.microsoft.com/library/jj651024.aspx).

Les deux options de topologie de clé de locataire Azure Information Protection sont les suivantes : Microsoft gère votre clé de locataire (**Gérée par Microsoft**) ou vous la gérez vous-même (**Gérée par le client**) dans Azure Key Vault. Le scénario dans lequel vous gérez votre propre clé de locataire Azure Information Protection est parfois appelé BYOK (« Bring Your Own Key »). Pour plus d’informations, consultez l’article [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

Le tableau suivant permet d'identifier la procédure à utiliser pour votre migration. 

|Déploiement AD RMS actuel|Topologie de clé de locataire Azure Information Protection choisie|Instructions de migration|
|-----------------------------|----------------------------------------|--------------------------|
|Protection par mot de passe dans la base de données AD RMS|Gérée par Microsoft|Consultez la procédure **Migration de clé protégée par logiciel à clé protégée par logiciel** après ce tableau.<br /><br />Ce chemin de migration, qui est le plus simple, nécessite uniquement que vous transfériez vos données de configuration vers Azure Information Protection.|
|Protection HSM à l'aide d'un module de sécurité matériel Thales nShield (HSM) |Gérée par le client (BYOK)|Consultez la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.<br /><br />Cette opération nécessite l’ensemble d’outils BYOK d’Azure Key Vault et trois procédures, d’abord pour transférer la clé de votre module HSM local vers les modules HSM Azure Key Vault, puis pour autoriser le service Azure Rights Management d’Azure Information Protection à utiliser votre clé de locataire, et enfin pour transférer vos données de configuration vers Azure Information Protection.|
|Protection par mot de passe dans la base de données AD RMS|Gérée par le client (BYOK)|Consultez la procédure **Migration de clé protégée par logiciel à clé protégée par HSM** après ce tableau.<br /><br />Cette opération nécessite l’ensemble d’outils BYOK d’Azure Key Vault et quatre procédures, d’abord pour extraire votre clé logicielle et l’importer dans un module HSM local, puis pour transférer la clé de votre module HSM local vers les modules HSM Azure Information Protection, ensuite pour transférer vos données Key Vault vers Azure Information Protection, et enfin pour transférer vos données de configuration vers Azure Information Protection.|
|Protection HSM à l'aide d'un module de sécurité matériel d'un fournisseur que Thales |Gérée par le client (BYOK)|Contactez le fournisseur de votre HSM pour obtenir des instructions sur le transfert de votre clé de ce HSM vers un HSM nShield Thales. Suivez ensuite les instructions de la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.|
|Protection par mot de passe à l'aide d'un fournisseur de services de chiffrement externe|Gérée par le client (BYOK)|Contactez le fournisseur de votre HSM pour obtenir des instructions concernant le transfert de votre clé vers un HSM nShield Thales. Suivez ensuite les instructions de la procédure **Migration de clé protégée par HSM à clé protégée par HSM** après ce tableau.|

Si vous avez une clé protégée par HSM que vous ne pouvez pas exporter, vous pouvez quand même migrer vers Azure Information Protection en configurant votre cluster AD RMS pour un mode en lecture seule. Dans ce mode, le contenu précédemment protégé peut toujours être ouvert, mais le contenu nouvellement protégé utilise une nouvelle clé de locataire que vous gérez vous-même (BYOK) ou qui est gérée par Microsoft. Pour plus d’informations, consultez [Une mise à jour d’Office est disponible pour prendre en charge les migrations d’AD RMS vers Azure RMS](https://support.microsoft.com/help/4023955/an-update-is-available-for-office-to-support-migrations-from-ad-rms-to).

Avant de commencer ces procédures de migration de clés, vérifiez que vous avez accès aux fichiers .xml créés lors de l’exportation des domaines de publication approuvés. Par exemple, ceux-ci peuvent être enregistrés sur une clé USB que vous déplacez du serveur AD RMS vers la station de travail connectée à Internet.

> [!NOTE]
> Quelle que soit la manière dont vous stockez ces fichiers, suivez les meilleures pratiques pour les protéger, car ces données incluent votre clé privée.

Pour effectuer l’étape 4, sélectionnez les instructions correspondant à votre chemin de migration : 

- [Clé protégée par logiciel vers clé protégée par logiciel](migrate-softwarekey-to-softwarekey.md)
- [Clé protégée par HSM vers clé protégée par HSM](migrate-hsmkey-to-hsmkey.md)
- [Clé protégée par logiciel vers clé protégée par HSM](migrate-softwarekey-to-hsmkey.md)

## <a name="step-5-activate-the-azure-rights-management-service"></a>Étape 5. Activer le service Azure Rights Management

Ouvrez une session PowerShell et exécutez les commandes suivantes :

1. Connectez-vous au service Azure Rights Management et indiquez vos informations d’identification d’administrateur général quand vous y êtes invité :
    
        Connect-Aadrmservice

2. Activez le service Azure Rights Management :
    
        Enable-Aadrm

**Que se passe-t-il si votre locataire Azure Information Protection est déjà activé ?** Si le service Azure Rights Management est déjà activé pour votre organisation et que vous avez créé des modèles personnalisés que vous souhaitez utiliser après la migration, vous devez exporter et importer ces modèles. Cette procédure est détaillée dans l’étape suivante. 

## <a name="step-6-configure-imported-templates"></a>Étape 6. Configurer les modèles importés

Étant donné que l’état par défaut des modèles importés est **Archivé**, vous devez définir cet état sur **Publié** si vous voulez que les utilisateurs soient en mesure d’utiliser ces modèles avec le service Azure Rights Management.

Les modèles que vous importez à partir d’AD RMS ressemblent à et se comportent comme des modèles personnalisés que vous pouvez créer dans le portail Azure. Pour changer des modèles importés et les publier pour que les utilisateurs puissent les voir et les sélectionner à partir d’applications, consultez [Configuration et gestion des modèles pour Azure Rights Management](../deploy-use/configure-policy-templates.md).

En plus de publier vos modèles nouvellement importés, vous devrez peut-être effectuer deux modifications importantes pour les modèles avant de poursuivre la migration. Pour offrir une expérience plus cohérente aux utilisateurs pendant le processus de migration, n’apportez pas de modifications supplémentaires aux modèles importés et évitez de publier les deux modèles par défaut fournis avec Azure Information Protection ou d’en créer à ce stade. Au lieu de cela, attendez que le processus de migration soit terminé et d’avoir annulé l’approvisionnement des serveurs AD RMS.

Voici les modifications que vous pouvez être amené à apporter aux modèles pour cette étape :

- Si vous avez créé des modèles personnalisés Azure Information Protection avant la migration, vous devez les exporter et importer manuellement.

- Si vos modèles dans AD RMS utilisaient le groupe **ANYONE**, vous devrez peut-être ajouter des utilisateurs ou des groupes extérieurs à votre organisation. 
    
    Dans AD RMS, le groupe ANYONE accordait des droits à tous les utilisateurs authentifiés. Ce groupe est automatiquement converti à tous les utilisateurs dans votre locataire Azure AD. Si vous n’avez pas besoin d’accorder des droits à d’autres utilisateurs, aucune action supplémentaire n’est nécessaire. En revanche, si vous utilisiez le groupe ANYONE pour inclure des utilisateurs externes, vous devez ajouter manuellement ces utilisateurs et les droits que vous souhaitez leur accorder.

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>Procédure à effectuer si vous avez créé des modèles personnalisés avant la migration

Si vous avez créé des modèles personnalisés avant la migration, que ce soit avant ou après l’activation du service Azure Rights Management, les modèles ne sont pas disponibles pour les utilisateurs après la migration, même si vous les avez définis sur **Publié**. Pour les mettre à la disposition des utilisateurs, vous devez effectuer les opérations suivantes : 

1. Identifiez ces modèles et notez leur ID de modèle, en exécutant l’applet de commande [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate). 

2. Exportez les modèles à l’aide de l’applet de commande PowerShell d’Azure RMS [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate).

3. Importez les modèles à l’aide de l’applet de commande PowerShell d’Azure RMS [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate).

Vous pouvez ensuite publier ou archiver ces modèles comme vous le feriez pour tout autre modèle que vous créez après la migration.

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>Procédure à effectuer si vos modèles dans AD RMS utilisaient le groupe **ANYONE**

Si vos modèles AD RMS utilisaient le groupe **ANYONE**, celui-ci est automatiquement converti pour utiliser le groupe nommé **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<nom_client>.onmicrosoft.com**. Par exemple, ce groupe peut se présenter sous la même forme que dans l’exemple suivant pour Contoso : **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**. Ce groupe contient tous les utilisateurs de votre locataire Azure AD.

Quand vous gérez des modèles et des étiquettes dans le portail Azure, ce groupe apparaît comme le nom de domaine de votre locataire dans Azure AD. Par exemple, ce groupe peut se présenter comme suit pour Contoso : **contoso.onmicrosoft.com**. Pour ajouter ce groupe, l’option affiche **Ajouter \<nom_organisation> - Tous les membres**.

Si vous n’êtes pas sûr que vos modèles AD RMS incluent le groupe ANYONE, vous pouvez utiliser l’exemple de script Windows PowerShell suivant pour identifier ces modèles. Pour plus d’informations sur l’utilisation de Windows PowerShell avec AD RMS, consultez [Utilisation de Windows PowerShell pour administrer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx).

Vous pouvez facilement ajouter des utilisateurs externes à des modèles quand vous convertissez ces derniers en étiquettes dans le portail Azure. Ensuite, dans le panneau **Ajouter des autorisations**, choisissez **Entrez les détails** pour spécifier manuellement les adresses e-mail de ces utilisateurs. 

Pour plus d’informations sur cette configuration, consultez [Comment configurer une étiquette pour la protection offerte par Rights Management](../deploy-use/configure-policy-protection.md).

#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>Exemple de script Windows PowerShell permettant d’identifier les modèles AD RMS qui incluent le groupe ANYONE
Cette section contient l’exemple de script qui vous permet d’identifier n’importe quel modèle AD RMS pour lequel le groupe ANYONE a été défini, comme décrit dans la section précédente.

**Exclusion de responsabilité** : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d'aucune sorte.

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


## <a name="next-steps"></a>Étapes suivantes
Passez à la [Phase 3 : Configuration côté client](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]