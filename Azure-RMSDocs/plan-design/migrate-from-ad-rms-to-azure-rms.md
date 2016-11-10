---
title: "Migration d’AD RMS vers Azure Information Protection | Azure Information Protection"
description: "Instructions pour la migration de votre déploiement AD RMS (Active Directory Rights Management Services) vers Azure Information Protection. Après la migration, les utilisateurs auront toujours accès aux documents et e-mails que votre organisation a protégés à l’aide d’AD RMS, et le contenu nouvellement protégé utilisera Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 10/27/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5774a94582e6a685f84a1fc6cd9915258bf7cbe0
ms.openlocfilehash: 49c65779e5651f25082369822b60b09435c41041


---

# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>Migration d’AD RMS vers Azure Information Protection

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*

Utilisez l’ensemble d’instructions suivant pour migrer votre déploiement AD RMS (Active Directory Rights Management Services) vers Azure Information Protection. Après la migration, les utilisateurs auront toujours accès aux documents et e-mails que votre organisation a protégés à l’aide d’AD RMS, et le contenu nouvellement protégé utilisera le service Azure Rights Management d’Azure Information Protection.

Vous n'êtes pas certain de l'opportunité de cette migration AD RMS pour votre organisation ?

-   Pour obtenir une présentation d’Azure Information Protection, consultez [What is Azure Information Protection?](../understand-explore/what-is-information-protection.md) (Qu’est-ce qu’Azure Information Protection ?).

-   Pour obtenir une comparaison d’Azure Information Protection avec AD RMS, consultez [Comparaison d’Azure Information Protection avec AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Lecture recommandée avant de migrer vers Azure Information Protection

Bien qu’elle ne soit pas obligatoire, il peut s’avérer utile de lire ce qui suit avant de commencer la migration, ceci pour une meilleure compréhension du fonctionnement de la technologie quand elle s’applique à votre étape de migration :

- [Planification et implémentation de votre clé de locataire Azure Information Protection](../plan-design/plan-implement-tenant-key.md) : découvrez les options de gestion clés dont vous disposez pour votre locataire Azure Information Protection où votre clé SLC équivalente dans le cloud est gérée par Microsoft (l’option par défaut) ou gérée par vous (la configuration BYOK). 

- [Découverte du service RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) : cette section des notes de déploiement du client RMS explique que l’ordre de découverte des services est **Registre** > **SCP** > **Cloud**. Pendant le processus de migration, alors que le point de connexion de service est toujours installé, vous configurez les clients avec des paramètres de Registre pour votre locataire Azure Information Protection de façon à ce qu’ils n’utilisent pas le cluster AD RMS retourné depuis le point de connexion de service.

- [Vue d’ensemble du connecteur Microsoft Rights Management](../deploy-use/deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector) : cette section de la documentation du connecteur RMS explique comment vos serveurs locaux peuvent se connecter au service Azure Rights Management pour protéger des documents et des e-mails.

En outre, si vous êtes familiarisé avec le fonctionnement d’AD RMS, il peut s’avérer utile de lire [Comment fonctionne Azure RMS ? En coulisse](../understand-explore/how-does-it-work.md) pour vous aider à identifier les processus technologiques qui sont identiques ou différents pour la version de cloud.

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>Conditions préalables à une migration d’AD RMS vers Azure Information Protection
Avant de procéder à la migration vers Azure Information Protection, assurez-vous que les conditions préalables suivantes sont réunies et que vous comprenez les limitations de ce processus.

- **Un déploiement RMS pris en charge :**
    
    - Les versions suivantes d’AD RMS prennent en charge une migration vers Azure Information Protection :
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
        - Windows Server 2016 (x64)
        
    - Mode de chiffrement 2 :

        - Vos serveurs et vos clients AD RMS doivent s’exécuter en mode de chiffrement 2 avant de pouvoir commencer la migration vers Azure Information Protection.
        
        Même si la clé de certificat de licence serveur (SLC) doit utiliser le mode de chiffrement 2, les clés configurées précédemment pour le mode de chiffrement 1 sont prises en charge par Azure Information Protection en tant que clés archivées. Pour plus d’informations sur les modes de chiffrement et pour savoir comment passer au mode de chiffrement 2, consultez [AD RMS Cryptographic Modes](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx) (Modes de chiffrement AD RMS).
        
    - Toutes les topologies AD RMS valides sont prises en charge :
    
        - Forêt unique, cluster RMS unique
        
        - Forêt unique, plusieurs clusters RMS dédiés uniquement à la gestion des licences
        
        - Plusieurs forêts, plusieurs clusters RMS
        
    Remarque : Par défaut, plusieurs clusters RMS migrent vers un seul locataire Azure Information Protection. Si vous voulez des clients Azure Information Protection, vous devez les traiter comme des migrations différentes. Une clé d’un cluster RMS ne peut pas être importée dans plusieurs clients Azure Information Protection.

- **Toutes les configurations requises pour exécuter Azure Information Protection, notamment un locataire Azure Information Protection (non activé) :**

    Consultez [Configuration requise pour Azure Information Protection](../get-started/requirements-azure-rms.md).

    Bien que vous deviez disposer d’un locataire Azure Information Protection pour pouvoir effectuer une migration à partir d’AD RMS, nous vous recommandons que le service Rights Management ne soit pas activé avant d’avoir procédé à la migration. Le processus de migration inclut cette étape après l’exportation des clés et modèles à partir d’AD RMS, et leur importation dans Azure Information Protection. Toutefois, si le service Rights Management est déjà activé, vous pouvez toujours migrer à partir d’AD RMS.


- **Préparation pour Azure Information Protection :**

    - Synchronisation d'annuaires entre votre annuaire local et Azure Active Directory

    - Groupes à extension messagerie dans Azure Active Directory

    Consultez [Préparation d’Azure Information Protection](prepare.md).


- **Si vous avez utilisé la fonctionnalité de Gestion des droits relatifs à l’information (IRM) d’Exchange Server** (par exemple, règles de transport et Outlook Web Access) ou SharePoint Server avec AD RMS :

    - Prévoyez une courte période pendant laquelle cette fonctionnalité ne sera pas disponible sur ces serveurs.
 
    Vous pouvez continuer à utiliser la fonctionnalité IRM sur ces serveurs avec le service Azure Rights Management après la migration. Toutefois, une des étapes de migration consiste à désactiver temporairement le service IRM, à installer et à configurer un connecteur, à reconfigurer les serveurs, puis à réactiver le service IRM.

    Il s'agit de l'unique interruption de service durant le processus de migration.

- **Si vous voulez gérer votre propre clé de locataire Azure Information Protection en utilisant une clé protégée par HSM** :

    - Cette configuration facultative nécessite Azure Key Vault et un abonnement Azure qui prend en charge Key Vault avec des clés protégées par HSM. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


Limitations :

-   Bien que le processus de migration prenne en charge la migration de votre clé de certificat de licence serveur (SLC) vers un module de sécurité matériel (HSM) pour Azure Information Protection, Exchange Online ne prend pas actuellement en charge cette configuration pour le service Rights Management utilisé par Azure Information Protection. Si vous souhaitez disposer de toutes les fonctionnalités IRM avec Exchange Online après la migration vers Azure Information Protection, votre clé de locataire Azure Information Protection doit être [Gérée par Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). Vous pouvez également exécuter IRM avec des fonctionnalités réduites dans Exchange Online quand vous gérez vous-même votre locataire Azure Information Protection (à l’aide de la solution BYOK). Pour plus d’informations sur l’utilisation d’Exchange Online avec le service Azure Rights Management, consultez l’[Étape 6. Configurer l’intégration de l’IRM pour Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) dans ces instructions de migration.

-   Si vous disposez de logiciels et de clients non pris en charge par le service Rights Management qui est utilisé par Azure Information Protection, ceux-ci ne peuvent pas protéger ou utiliser du contenu protégé par Azure Rights Management. Consultez les sections relatives aux applications et aux clients pris en charge dans l’article [Conditions requises pour Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Si vous importez votre clé locale dans Azure Information Protection en tant que clé archivée (vous ne définissez pas le domaine de publication approuvé comme étant actif pendant le processus d’importation), et que vous migrez ensuite des utilisateurs par lots dans le cadre d’une migration en plusieurs phases, le contenu qui vient d’être protégé par les utilisateurs migrés n’est plus accessible aux utilisateurs qui restent sur AD RMS. Dans ce cas, autant que possible, veillez à ce que la durée de la migration soit courte et migrez les utilisateurs par lots logiques, par exemple, d'utilisateurs collaborant entre eux.

    Cette limitation ne s'applique pas quand vous définissez le domaine de publication approuvé comme étant actif pendant le processus d'importation, car tous les utilisateurs protégeront le contenu à l'aide de la même clé. Nous recommandons cette configuration, car elle vous permet de migrer tous les utilisateurs de façon indépendante et à votre propre rythme.

-   Si vous collaborez avec des partenaires externes (par exemple, en utilisant des domaines d’utilisateurs approuvés ou une fédération), ceux-ci doivent également migrer vers Azure Information Protection, soit au moment de votre migration, soit dès que possible par la suite. Pour continuer à accéder au contenu que votre organisation protégeait précédemment à l’aide d’Azure Information Protection, les utilisateurs doivent apporter à la configuration du client des modifications similaires à celles que vous apportez, qui sont incluses dans ce document.

    En raison de la diversité des configurations possibles de vos partenaires, des instructions précises pour cette reconfiguration sortent du cadre de ce document. Pour obtenir de l’aide, [contactez le support Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>Présentation des étapes de migration d’AD RMS vers Azure Information Protection


Les étapes de migration peuvent être divisées en quatre phases, qui peuvent être effectuées à des moments différents et par des administrateurs différents.

[**PHASE 1 : CONFIGURATION CÔTÉ SERVEUR POUR AD RMS**](migrate-from-ad-rms-phase1.md)

- **Étape 1 : Télécharger l’outil d’administration pour la gestion d’Azure RMS**

    Le processus de migration impose l’exécution d’une ou plusieurs des applets de commande Windows PowerShell à partir du module Azure RMS qui est installé avec l’outil d’administration pour la gestion d’Azure RMS.

- **Étape 2 : Exporter les données de configuration depuis AD RMS, puis les importer dans Azure Information Protection**

    Vous exportez les données de configuration (clés, modèles, URL) d’AD RMS vers un fichier XML, puis vous chargez ce fichier dans le service Azure Rights Management d’Azure Information Protection à l’aide de l’applet de commande Windows PowerShell Import-AadrmTpd. Des étapes supplémentaires peuvent être nécessaires en fonction la configuration de votre clé AD RMS :

    - **Migration de clé protégée par logiciel à clé protégée par logiciel** :

        De clé basée sur un mot de passe et gérée de façon centralisée dans AD RMS à clé de locataire Azure Information Protection gérée par Microsoft. Ce chemin de migration le plus simple ne nécessite aucune étape supplémentaire.

    - **Migration de clé protégée par HSM à clé protégée par HSM** :

        De clé stockée par un module HSM pour AD RMS à clé de locataire Azure Information Protection gérée par le client (scénario BYOK, « Bring Your Own Key »). Cette migration nécessite des étapes supplémentaires pour transférer la clé de votre module HSM Thales local vers Azure Key Vault et pour autoriser le service Azure Rights Management à utiliser cette clé. Votre clé protégée par HSM existante doit être protégée par module. Les clés protégées par OCS ne sont pas prises en charge par les services RMS.

    - **Migration de clé protégée par logiciel à clé protégée par HSM** :

        De clé basée sur un mot de passe et gérée de façon centralisée dans AD RMS à clé de locataire Azure Information Protection gérée par le client (scénario BYOK, « Bring Your Own Key »). Cette migration est celle qui nécessite le plus de configuration, car vous devez d’abord extraire votre clé logicielle et l’importer dans un module HSM local, puis effectuer les étapes supplémentaires pour transférer la clé de votre module HSM Thales local vers le module HSM Azure Key Vault, et enfin autoriser le service Azure Rights Management à utiliser le coffre de clés qui stocke la clé.

- **Étape 3 : Activer votre locataire Azure Information Protection**

    Si possible, effectuez cette étape après le processus d'importation et non avant.

- **Étape 4 :. Configurer les modèles importés**

    Lorsque vous importez vos modèles de stratégie de droits, leur état est archivé. Si vous souhaitez que les utilisateurs puissent voir et utiliser ces modèles, vous devez modifier leur état en publié dans le portail Azure Classic.


[**PHASE 2 : CONFIGURATION CÔTÉ CLIENT**](migrate-from-ad-rms-phase2.md)


- **Étape 5 : Reconfigurer les clients pour utiliser Azure Information Protection**

    Les ordinateurs Windows existants doivent être reconfigurés pour utiliser le service Azure Information Protection au lieu d’AD RMS. Cette étape s'applique aux ordinateurs de votre organisation ainsi qu'à ceux des organisations partenaires avec lesquelles vous avez collaboré lorsque vous exécutiez AD RMS.

    De plus, si vous avez déployé l’[extension d’appareil mobile](http://technet.microsoft.com/library/dn673574.aspx) pour prendre en charge des appareils mobiles tels que des téléphones et iPad iOS, des téléphones et tablettes Android, des téléphones Windows Phone et des ordinateurs Mac, vous devez supprimer les enregistrements SRV dans le système DNS qui redirigeaient ces clients pour utiliser AD RMS.


[**PHASE 3 : CONFIGURATION DES SERVICES DE PRISE EN CHARGE**](migrate-from-ad-rms-phase3.md)


- **Étape 6 : Configurer l’intégration d’IRM à Exchange Online**

    Cette étape est nécessaire si vous souhaitez utiliser Exchange Online avec le service Azure Rights Management d’Azure Information Protection.


- **Étape 7 : Déployer le connecteur RMS**

    Cette étape est nécessaire si vous souhaitez utiliser l’un des services locaux suivants avec le service Azure Rights Management pour protéger les e-mails et les documents Office :

    - Exchange Server (par exemple, règles de transport et Outlook Web Access)

    - SharePoint Server

    - Windows Server exécutant une infrastructure de classification des fichiers (FCI, File Classification Infrastructure)


[**PHASE 4 : TÂCHES POSTÉRIEURES À LA MIGRATION**](migrate-from-ad-rms-phase4.md )

- **Étape 8 : Désaffecter AD RMS**

    Après avoir vérifié que tous les clients utilisent Azure Information Protection et n’accèdent plus aux serveurs AD RMS, vous pouvez désaffecter votre déploiement AD RMS.


- **Étape 9 : Renouveler votre clé de locataire Azure Information Protection**

    Cette étape est facultative, mais elle est recommandée si la topologie de clé de locataire Azure Information Protection choisie à l’étape 2 est Gérée par Microsoft. Cette étape n’est pas applicable si la topologie de clé de locataire Azure Information Protection choisie est Gérée par le client (BYOK).


## <a name="next-steps"></a>Étapes suivantes
Pour démarrer la migration, passez à la [Phase 1 : Configuration côté serveur](migrate-from-ad-rms-phase1.md).




<!--HONumber=Oct16_HO4-->


