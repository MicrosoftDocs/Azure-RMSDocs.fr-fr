---
title: Migrer un déploiement AD RMS vers Azure Information Protection
description: Instructions pour la migration de votre déploiement AD RMS (Active Directory Rights Management Services) vers Azure Information Protection. Après la migration, les utilisateurs ont toujours accès aux documents et e-mails que votre organisation protégée à l’aide d’AD RMS.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c1fb307d06c277dd6f515adbff35a844f65f77cc
ms.sourcegitcommit: 383b1fa5e65255420d7ec6fbe2f9b17f4439e33e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65708912"
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>Migration d’AD RMS vers Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez l’ensemble d’instructions suivant pour migrer votre déploiement des services AD RMS (Active Directory Rights Management Services) vers Azure Information Protection. 

Après la migration, les serveurs AD RMS ne sont plus utilisés, mais les utilisateurs ont toujours accès aux documents et e-mails que votre organisation a protégés à l’aide d’AD RMS. Le contenu nouvellement protégé utilisera le service Azure RMS (Azure Rights Management Service) à partir d’Azure Information Protection.

Vous n'êtes pas certain de l'opportunité de cette migration AD RMS pour votre organisation ?

- Pour obtenir une présentation d’Azure Information Protection, consultez [Qu’est-ce qu’Azure Information Protection ?](./what-is-information-protection.md)

- Pour obtenir une comparaison d’Azure Information Protection avec AD RMS, consultez [Comparaison d’Azure Information Protection avec AD RMS](./compare-on-premise.md).

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Lecture recommandée avant de migrer vers Azure Information Protection

Bien que ceci ne soit pas obligatoire, il peut s’avérer utile de lire ce qui suit avant de commencer la migration, ceci pour une meilleure compréhension du fonctionnement de la technologie quand elle s’applique à votre étape de migration.

- [Planification et implémentation de votre clé de locataire Azure Information Protection](./plan-implement-tenant-key.md) : Découvrez les options de gestion principales dont vous disposez pour votre locataire Azure Information Protection où votre clé SLC équivalente dans le cloud est gérée par Microsoft (l’option par défaut) ou gérée par vous-même (la configuration BYOK). 

- [Découverte du service RMS](./rms-client/client-deployment-notes.md#rms-service-discovery) : Cette section des notes de déploiement du client RMS explique que l’ordre de découverte des services est **Registre**, puis **SCP**, puis **cloud**. Pendant le processus de migration, alors que le point de connexion de service est toujours installé, vous configurez les clients avec des paramètres de Registre pour votre locataire Azure Information Protection de façon à ce qu’ils n’utilisent pas le cluster AD RMS retourné depuis le point de connexion de service.

- [Vue d’ensemble du connecteur Microsoft Rights Management](./deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector) : Cette section de la documentation du connecteur RMS explique comment vos serveurs locaux peuvent se connecter au service Azure Rights Management pour protéger des documents et des e-mails.

En outre, si vous êtes familiarisé avec le fonctionnement d’AD RMS, il peut s’avérer utile de lire [Comment fonctionne Azure RMS ? En coulisse](./how-does-it-work.md) pour vous aider à identifier les processus technologiques qui sont identiques ou différents pour la version de cloud.

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>Conditions préalables à une migration d’AD RMS vers Azure Information Protection

Avant de procéder à la migration vers Azure Information Protection, assurez-vous que les conditions préalables suivantes sont réunies et que vous comprenez les limitations de ce processus.

- **Un déploiement RMS pris en charge :**
    
  - Les versions suivantes d’AD RMS prennent en charge une migration vers Azure Information Protection :
    
      - Windows Server 2008 R2 (x64)
        
      - Windows Server 2012 (x64)
        
      - Windows Server 2012 R2 (x64)
        
      - Windows Server 2016 (x64)
        
  - Toutes les topologies AD RMS valides sont prises en charge :
    
      - Forêt unique, cluster RMS unique
        
      - Forêt unique, plusieurs clusters RMS dédiés uniquement à la gestion des licences
        
      - Plusieurs forêts, plusieurs clusters RMS
        
    Remarque : Par défaut, plusieurs clusters AD RMS migrent vers un seul locataire pour Azure Information Protection. Si vous voulez des locataires séparés pour Azure Information Protection, vous devez les traiter comme des migrations différentes. Une clé d’un cluster RMS ne peut pas être importée dans plusieurs locataires.

- **Toutes les configurations requises pour exécuter Azure Information Protection, notamment un abonnement pour Azure Information Protection (le service Azure Rights Management n’est pas activé) :**

    Consultez [Configuration requise pour Azure Information Protection](./requirements.md).

    Notez que si vous avez des ordinateurs qui exécutent Office 2010, vous devez installer le [client Azure Information Protection ou le client étiquetage Azure Information Protection unifié pour les utilisateurs](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client), car ces clients permettent de authentifier les utilisateurs aux services cloud. Pour les versions ultérieures d’Office, ces clients sont requis pour la classification et l’étiquetage, et le client Azure Information Protection est facultatif mais recommandée si vous souhaitez uniquement protéger les données. Pour plus d’informations, consultez les guides d’administration pour le [client Azure Information Protection](./rms-client/client-admin-guide.md) et [étiquetage client unifié, Azure Information Protection](./rms-client/clientv2-admin-guide.md).

    Bien qu’un abonnement à Azure Information Protection soit nécessaire pour pouvoir migrer à partir d’AD RMS, nous recommandons de ne pas activer le service Rights Management du client (tenant) avant de commencer la migration. Le processus de migration comporte cette étape d’activation après l’exportation des clés et des modèles à partir d’AD RMS, et leur importation dans le client (tenant) pour Azure Information Protection. Toutefois, si le service Rights Management est déjà activé, la migration sera toujours possible à partir d’AD RMS moyennant quelques étapes supplémentaires.


- **Préparation pour Azure Information Protection :**

  - Synchronisation d'annuaires entre votre annuaire local et Azure Active Directory

  - Groupes à extension messagerie dans Azure Active Directory

    Consultez [Préparation des utilisateurs et groupes pour Azure Information Protection](prepare.md).

- **Si vous avez utilisé la fonctionnalité IRM (Gestion des droits relatifs à l’information) d’Exchange Server** (par exemple, règles de transport et Outlook Web Access) ou SharePoint Server avec AD RMS :

  - Prévoyez une courte période pendant laquelle cette fonctionnalité ne sera pas disponible sur ces serveurs.
 
    Vous pouvez continuer à utiliser la fonctionnalité IRM sur ces serveurs après la migration. Toutefois, une des étapes de migration consiste à désactiver temporairement le service IRM, à installer et à configurer un connecteur, à reconfigurer les serveurs, puis à réactiver le service IRM.

    Il s'agit de l'unique interruption de service durant le processus de migration.

- **Si vous voulez gérer votre propre clé de locataire Azure Information Protection en utilisant une clé protégée par HSM** :

    - Cette configuration facultative nécessite Azure Key Vault et un abonnement Azure qui prend en charge Key Vault avec des clés protégées par HSM. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/). 


### <a name="cryptographic-mode-considerations"></a>Considérations relatives au mode de chiffrement

Si votre cluster AD RMS est actuellement en mode de chiffrement 1, ne le mettez pas à niveau vers le mode de chiffrement 2 avant de commencer la migration. Au lieu de cela, effectuez la migration en mode de chiffrement 1. Vous pouvez alors renouveler votre clé une fois la migration terminée (dans le cadre des tâches suivant la migration).

Pour confirmer le mode de chiffrement AD RMS :
 
- Pour Windows Server 2012 R2 et Windows 2012 : Propriétés du cluster AD RMS > Onglet **Général**. 

- Pour Windows Server 2008 R2 : Vérifiez que le correctif [La longueur de clé RSA est augmentée à 2 048 bits pour AD RMS dans Windows Server 2008 R2 et dans Windows Server 2008](https://support.microsoft.com/help/2627272/rsa-key-length-is-increased-to-2048-bits-for-ad-rms-in-windows-server ) est installé. Dans le cas contraire, votre cluster AD RMS est exécuté en Mode de chiffrement 1.

### <a name="migration-limitations"></a>Limites de migration

- Si vous disposez de logiciels et de clients non pris en charge par le service Rights Management utilisé par Azure Information Protection, ils ne peuvent pas protéger ou utiliser du contenu protégé par Azure Rights Management. Consultez les sections relatives aux applications et aux clients pris en charge dans [Conditions requises pour Azure Rights Management](./requirements.md).

- Si votre déploiement des services AD RMS est configuré pour collaborer avec des partenaires externes (par exemple, en utilisant des domaines d’utilisateurs approuvés ou une fédération), ceux-ci doivent également migrer vers Azure Information Protection, soit au moment de votre migration, soit dès que possible par la suite. Pour continuer à accéder au contenu que votre organisation protégeait précédemment à l’aide d’Azure Information Protection, les utilisateurs doivent apporter à la configuration du client des modifications similaires à celles que vous apportez, qui sont incluses dans ce document.
    
    En raison de la diversité des configurations possibles de vos partenaires, des instructions précises pour cette reconfiguration sortent du cadre de ce document. Toutefois, consultez la section suivante pour obtenir des conseils sur la planification et [contactez le support technique Microsoft](./information-support.md#support-options-and-community-resources) pour une aide supplémentaire.

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>Planification de la migration si vous collaborez avec des partenaires externes

Ajoutez vos partenaires AD RMS dans votre phase de planification de la migration, car ils doivent également migrer vers Azure Information Protection. Avant d’effectuer l’une des étapes de migration ci-après, vérifiez que les conditions suivantes sont réunies :

- Ils ont un locataire Azure Active Directory qui prend en charge le service Azure Rights Management.  
    
    Par exemple, ils disposent d’un abonnement Office 365 E3 ou E5, ou Enterprise Mobility + Security, ou autonome pour Azure Information Protection.

- Leur service Azure Rights Management n’est pas encore activé, mais ils connaissent leur URL de service Azure Rights Management.

    Ils peuvent obtenir ces informations en installant l’outil Azure Rights Management, en se connectant au service ([Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)), puis en affichant les informations du locataire pour le service Azure Rights Management ([Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)).

- Ils vous fournissent les URL de leur cluster AD RMS et l’URL de service Azure Rights Management pour que vous puissiez configurer les clients migrés afin de rediriger les demandes de contenu protégé AD RMS vers le service Azure Rights Management de leur locataire. Les instructions pour la configuration de la redirection des clients figurent à l’étape 7.

- Ils importent leurs clés racines de cluster (SLC) AD RMS dans leur locataire avant que vous ne commenciez à migrer vos utilisateurs. De même, vous devez importer vos clés racines de cluster AD RMS avant qu’ils ne commencent à migrer leurs utilisateurs. Les instructions pour l’importation de la clé sont abordées dans ce processus de migration, [Étape 4. Exporter des données de configuration d’AD RMS pour les importer dans Azure Information Protection](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection). 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>Présentation des étapes de migration d’AD RMS vers Azure Information Protection

Les étapes de migration peuvent être divisées en cinq phases qui peuvent être effectuées à des moments différents et par des administrateurs différents.

[**PHASE 1 : PRÉPARATION DE LA MIGRATION**](migrate-from-ad-rms-phase1.md)

- **Étape 1 : Installer le module PowerShell AADRM et identifier l’URL de votre locataire**

    Le processus de migration vous oblige à exécuter une ou plusieurs des applets de commande PowerShell du module AADRM. Vous devez également connaître l’URL du service Azure Rights Management de votre locataire pour pouvoir réaliser différentes étapes de migration, et vous pouvez identifier cette valeur à l’aide de PowerShell.

- **Étape 2. Préparer la migration des clients**

    Si vous ne pouvez pas migrer tous les clients à la fois et que vous allez les migrer par lots, utilisez les contrôles d’intégration et déployez un script de prémigration. Toutefois, si vous les migrez tous à la fois au lieu d’effectuer une migration en plusieurs phases, vous pouvez ignorer cette étape.

- **Étape 3 : Préparer votre déploiement Exchange pour la migration**

    Cette étape est nécessaire si vous utilisez la fonctionnalité IRM d’Exchange Online ou Exchange sur site afin de protéger les e-mails. Toutefois, si vous les migrez tous à la fois au lieu d’effectuer une migration en plusieurs phases, vous pouvez ignorer cette étape.

[**PHASE 2 : CONFIGURATION CÔTÉ SERVEUR POUR AD RMS**](migrate-from-ad-rms-phase2.md)

- **Étape 4 :. Exporter des données de configuration d’AD RMS pour les importer dans Azure Information Protection**

    Vous exportez les données de configuration (clés, modèles, URL) d’AD RMS vers un fichier XML, puis vous chargez ce fichier dans le service Azure Rights Management d’Azure Information Protection à l’aide de l’applet de commande PowerShell Import-AadrmTpd. Ensuite, identifiez la clé de certificat de licence serveur (SLC) importée à utiliser comme clé de locataire pour le service Azure Rights Management. Des étapes supplémentaires peuvent être nécessaires en fonction de la configuration de votre clé AD RMS :

    - **Migration de clé protégée par logiciel à clé protégée par logiciel** :

        De clés de type mot de passe gérées de façon centralisée dans AD RMS à une clé de client (tenant) Azure Information Protection gérée par Microsoft. Ce chemin de migration le plus simple ne nécessite aucune étape supplémentaire.

    - **Migration de clé protégée par HSM à clé protégée par HSM** :

        De clé stockée par un module HSM pour AD RMS à clé de locataire Azure Information Protection gérée par le client (scénario BYOK, « Bring Your Own Key »). Cela nécessite des étapes supplémentaires pour transférer la clé à partir de votre nCipher local HSM vers Azure Key Vault et autoriser le service Azure Rights Management d’utiliser cette clé. Votre clé protégée par HSM existante doit être protégée par module. Les clés protégées par OCS ne sont pas prises en charge par les services RMS.

    - **Migration de clé protégée par logiciel à clé protégée par HSM** :

        De clé basée sur un mot de passe et gérée de façon centralisée dans AD RMS à clé de locataire Azure Information Protection gérée par le client (scénario BYOK, « Bring Your Own Key »). Cela nécessite le plus de configuration, car vous devez tout d’abord extraire votre clé logicielle et l’importer vers un HSM local et puis effectuez les étapes supplémentaires pour transférer la clé à partir de votre HSM de nCipher sur site vers un HSM Azure Key Vault et autoriser les droits d’Azure Service de gestion à utiliser le coffre de clés qui stocke la clé.

- **Étape 5. Activer le service Azure Rights Management**

    Si possible, effectuez cette étape après le processus d'importation et non avant. Des étapes supplémentaires sont nécessaires si le service a été activé avant l’importation.

- **Étape 6. Configurer les modèles importés**

    Lorsque vous importez vos modèles de stratégie de droits, leur état est archivé. Si vous souhaitez que les utilisateurs puissent voir et utiliser ces modèles, vous devez changer leur état en publié dans le portail Azure Classic.


[**PHASE 3 : CONFIGURATION CÔTÉ CLIENT**](migrate-from-ad-rms-phase3.md)

- **Étape 7 : Reconfigurer les ordinateurs Windows pour qu’ils utilisent Azure Information Protection**

    Les ordinateurs Windows existants doivent être reconfigurés pour utiliser le service Azure Rights Management au lieu d’AD RMS. Cette étape s'applique aux ordinateurs de votre organisation ainsi qu'à ceux des organisations partenaires avec lesquelles vous avez collaboré lorsque vous exécutiez AD RMS.

[**PHASE 4 : CONFIGURATION DES SERVICES DE PRISE EN CHARGE**](migrate-from-ad-rms-phase4.md)

- **Étape 8 : Configurer l’intégration d’IRM pour Exchange Online**

    Cette étape termine la migration AD RMS pour Exchange Online pour à présent utiliser le service Azure Rights Management.

- **Étape 9 : Configurer l’intégration d’IRM pour Exchange Server et SharePoint Server**

    Cette étape termine la migration AD RMS pour Exchange ou SharePoint sur site pour à présent utiliser le service Azure Rights Management, qui nécessite le déploiement du connecteur Rights Management.


[**PHASE 5 : TÂCHES DE POST-MIGRATION**](migrate-from-ad-rms-phase5.md )

- **Étape 10 : Déprovisionner AD RMS**

    Après avoir vérifié que tous les ordinateurs Windows utilisent le service Azure Rights Management et n’accèdent plus aux serveurs AD RMS, vous pouvez annuler l’approvisionnement de votre déploiement AD RMS.

- **Étape 11 : Effectuer les tâches de migration des clients**

    Si vous avez déployé l’[extension d’appareil mobile](https://technet.microsoft.com/library/dn673574.aspx) pour prendre en charge des appareils mobiles tels que des iPad et téléphones iOS, des téléphones et tablettes Android, des téléphones et tablettes Windows et des ordinateurs Mac, vous devez supprimer les enregistrements SRV dans le système DNS qui redirigeaient ces clients pour utiliser AD RMS. 
    
    Les contrôles d’intégration que vous avez configurés au cours de la phase de préparation ne sont plus nécessaires. Toutefois, si vous n’utilisez pas de contrôles d’intégration parce que vous avez choisi de tout migrer à la fois au lieu d’effectuer une migration en plusieurs phases, vous pouvez ignorer les instructions pour supprimer les contrôles d’intégration.
    
    Si vos ordinateurs Windows exécutent Office 2010, vérifiez si vous devez désactiver la tâche de **gestion des modèles de stratégie de droits AD RMS (automatique)**.

- **Étape 12 : Renouveler votre clé de locataire Azure Information Protection**

    Cette étape est recommandée si vous n’utilisiez pas le mode de chiffrement 2 avant la migration.


## <a name="next-steps"></a>Étapes suivantes
Pour démarrer la migration, accédez à [Phase 1 : Préparation](migrate-from-ad-rms-phase1.md).

