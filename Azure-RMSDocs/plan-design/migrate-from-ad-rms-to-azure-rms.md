---
title: "Migration d’AD RMS vers Azure Rights Management | Azure RMS"
description: "Instructions à suivre pour migrer votre déploiement Active Directory Rights Management Services (AD RMS) vers Azure Rights Management (Azure RMS). Après la migration, les utilisateurs auront toujours accès aux documents et messages électroniques que votre organisation a protégés à l'aide d'AD RMS, et le contenu nouvellement protégé utilisera Azure RMS."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: 6aa75f5e6b326068951b3d4d65f337c15a475029


---

# Migration d'AD RMS vers Azure Rights Management

>*S’applique à : Active Directory Rights Management Services, Azure Rights Management*

Utilisez l'ensemble suivant d'instructions pour migrer votre déploiement Active Directory Rights Management Services (AD RMS) vers Azure Rights Management (Azure RMS). Après la migration, les utilisateurs auront toujours accès aux documents et messages électroniques que votre organisation a protégés à l'aide d'AD RMS, et le contenu nouvellement protégé utilisera Azure RMS.

Vous n'êtes pas certain de l'opportunité de cette migration AD RMS pour votre organisation ?

-   Pour obtenir une présentation d’Azure RMS, des problèmes professionnels que cette solution peut résoudre, de son aspect pour les administrateurs et utilisateurs et de son fonctionnement, consultez [En quoi consiste Azure Rights Management ?](../understand-explore/what-is-azure-rms.md)

-   Pour obtenir une comparaison d’Azure RMS et d’AD RMS, consultez [Comparaison d’Azure Rights Management avec AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Conditions préalables à une migration d'AD RMS vers Azure RMS
Avant de procéder à la migration vers Azure RMS, assurez-vous que les conditions préalables suivantes sont réunies et que vous comprenez les limitations de ce processus.


- **Un déploiement RMS pris en charge :**
    
    - Les versions suivantes d’AD RMS prennent en charge une migration vers Azure RMS :
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - Mode de chiffrement 2 :
    
        - Vos serveurs et vos clients AD RMS doivent s’exécuter en Mode de chiffrement 2 avant de pouvoir commencer la migration vers Azure RMS. Pour plus d’informations, consultez [Modes de chiffrement d’AD RMS](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx).
        
    - Toutes les topologies AD RMS valides sont prises en charge :
    
        - Forêt unique, cluster RMS unique
        
        - Forêt unique, plusieurs clusters RMS dédiés uniquement à la gestion des licences
        
        - Plusieurs forêts, plusieurs clusters RMS
        
    Remarque : Par défaut, plusieurs clusters RMS migrent vers un seul locataire Azure RMS. Si vous voulez plusieurs locataires RMS, vous devez les traiter comme des migrations différentes. Une clé d'un cluster RMS ne peut pas être importée dans plus d'un locataire Azure RMS.

- **Toutes les configurations requises pour exécuter Azure RMS, notamment un locataire Azure RMS (non activé) :**

    Consultez [Conditions requises pour Azure Rights Management](../get-started/requirements-azure-rms.md).

    Bien que vous deviez disposer d'un locataire Azure RMS pour pouvoir migrer à partir d'AD RMS, nous vous recommandons de ne pas activer le service Rights Management avant d'avoir procédé à la migration. Le processus de migration inclut cette étape après l'exportation des clés et modèles à partir d'AD RMS, et leur importation dans Azure RMS. Toutefois, si Azure RMS est déjà activé, vous pouvez toujours migrer à partir d'AD RMS.


- **Préparation pour Azure RMS :**

    - Synchronisation d'annuaires entre votre annuaire local et Azure Active Directory

    - Groupes à extension messagerie dans Azure Active Directory

    Consultez [Préparation pour Azure Rights Management](prepare.md).


- **Si vous avez utilisé la fonctionnalité de Gestion des droits relatifs à l’information (IRM) d’Exchange Server** (par exemple, règles de transport et Outlook Web Access) ou SharePoint Server avec AD RMS :

    - Prévoyez une courte période pendant laquelle cette fonctionnalité ne sera pas disponible sur ces serveurs.
 
    Vous pouvez continuer à utiliser la fonctionnalité IRM sur ces serveurs avec Azure RMS après la migration. Toutefois, une des étapes de migration consiste à désactiver temporairement le service IRM, à installer et à configurer un connecteur, à reconfigurer les serveurs, puis à réactiver le service IRM.

    Il s'agit de l'unique interruption de service durant le processus de migration.

- **Si vous voulez gérer votre propre clé de locataire Azure RMS en utilisant une clé protégée par HSM** :

    - Cette configuration facultative nécessite Azure Key Vault et un abonnement Azure qui prend en charge Key Vault avec des clés protégées par HSM. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


Limitations :

-   Bien que le processus de migration prenne en charge la migration de votre clé de certificat de licence serveur (SLC) vers un module de sécurité matériel (HSM) pour Azure RMS, Exchange Online ne prend pas actuellement en charge cette configuration. Si vous souhaitez disposer de toutes les fonctionnalités d’IRM avec Exchange Online après la migration vers Azure RMS, votre clé de locataire Azure RMS doit être [gérée par Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). Vous pouvez également exécuter l'IRM avec des fonctionnalités réduites dans Exchange Online quand vous gérez vous-même votre locataire Azure RMS (à l'aide de la solution BYOK). Pour plus d’informations sur l’utilisation d’Exchange Online avec Azure RMS, consultez l’[Étape 6. Configurer l’intégration de l’IRM pour Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) dans ces instructions de migration.

-   Si vous disposez de logiciels et de clients non pris en charge avec Azure RMS, ceux-ci ne peuvent pas protéger ou utiliser du contenu protégé par Azure RMS. Consultez les sections relatives aux applications et aux clients pris en charge dans l’article [Conditions requises pour Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Si vous importez votre clé locale dans Azure RMS en tant que clé archivée (vous ne définissez pas le domaine de publication approuvé comme étant actif pendant le processus d’importation), et que vous migrez ensuite des utilisateurs par lots dans le cadre d’une migration en plusieurs phases, le contenu qui vient d’être protégé par les utilisateurs migrés n’est plus accessible aux utilisateurs qui restent sur AD RMS. Dans ce cas, autant que possible, veillez à ce que la durée de la migration soit courte et migrez les utilisateurs par lots logiques, par exemple, d'utilisateurs collaborant entre eux.

    Cette limitation ne s'applique pas quand vous définissez le domaine de publication approuvé comme étant actif pendant le processus d'importation, car tous les utilisateurs protégeront le contenu à l'aide de la même clé. Nous recommandons cette configuration, car elle vous permet de migrer tous les utilisateurs de façon indépendante et à votre propre rythme.

-   Si vous collaborez avec des partenaires externes (par exemple, en utilisant des domaines d'utilisateurs approuvés ou une fédération), ceux-ci doivent également migrer vers Azure RMS, soit au moment de votre migration, soit dès que possible par la suite. Pour continuer à accéder au contenu que votre organisation protégeait précédemment à l'aide d'AD RMS, les utilisateurs doivent apporter à la configuration du client des modifications similaires à celles que vous apportez, qui sont incluses dans ce document.

    En raison de la diversité des configurations possibles de vos partenaires, des instructions précises pour cette reconfiguration sortent du cadre de ce document. Pour obtenir de l’aide, [contactez le support Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## Présentation des étapes de migration d’AD RMS vers Azure RMS


Les étapes de migration peuvent être divisées en quatre phases, qui peuvent être effectuées à des moments différents et par des administrateurs différents.

[**PHASE 1 : CONFIGURATION CÔTÉ SERVEUR POUR AD RMS**](migrate-from-ad-rms-phase1.md)

- **Étape 1 : Télécharger l’outil d’administration pour la gestion d’Azure RMS**

    Le processus de migration impose l’exécution d’une ou plusieurs des applets de commande Windows PowerShell à partir du module Azure RMS qui est installé avec l’outil d’administration pour la gestion d’Azure RMS.

- **Étape 2. Exporter les données de configuration d'AD RMS, puis les importer dans Azure RMS**

    Vous exportez les données de configuration (clés, modèles, URL) d'AD RMS vers un fichier XML, puis vous chargez ce fichier dans Azure RMS à l'aide de l'applet de commande Windows PowerShell Import-AadrmTpd. Des étapes supplémentaires peuvent être nécessaires en fonction la configuration de votre clé AD RMS :

    - **Migration de clé protégée par logiciel à clé protégée par logiciel** :

        de clé basée sur un mot de passe gérée de façon centralisée dans AD RMS à clé de locataire Azure RMS gérée par Microsoft. Ce chemin de migration le plus simple ne nécessite aucune étape supplémentaire.

    - **Migration de clé protégée par HSM à clé protégée par HSM** :

        de clés stockées par un HSM pour AD RMS à clé de locataire Azure RMS gérée par le locataire (scénario BYOK, « Bring Your Own Key »). Cette migration nécessite des étapes supplémentaires pour transférer la clé de votre HSM Thales local vers Azure Key Vault et pour autoriser Azure RMS à utiliser cette clé. Votre clé protégée par HSM existante doit être protégée par module. Les clés protégées par OCS ne sont pas prises en charge par les services RMS.

    - **Migration de clé protégée par logiciel à clé protégée par HSM** :

        de clé basée sur un mot de passe gérée de façon centralisée dans AD RMS à clé de locataire Azure RMS gérée par le locataire (scénario BYOK). Cette migration est celle qui nécessite le plus de configuration, car vous devez d’abord extraire votre clé logicielle et l’importer dans un HSM local, puis effectuer les étapes supplémentaires pour transférer la clé de votre HSM Thales local vers le HSM Azure Key Vault et pour autoriser Azure RMS à utiliser le coffre de clés qui stocke la clé.

- **Étape 3. Activer votre locataire Azure RMS**

    Si possible, effectuez cette étape après le processus d'importation et non avant.

- **Étape 4. Configurer les modèles importés**

    Lorsque vous importez vos modèles de stratégie de droits, leur état est archivé. Si vous souhaitez que les utilisateurs puissent voir et utiliser ces modèles, vous devez modifier leur état en publié dans le portail Azure Classic.


[**PHASE 2 : CONFIGURATION CÔTÉ CLIENT**](migrate-from-ad-rms-phase2.md)


- **Étape 5 : Reconfigurer les clients pour utiliser Azure RMS**

    Les ordinateurs Windows existants doivent être reconfigurés pour utiliser le service Azure RMS au lieu d'AD RMS. Cette étape s'applique aux ordinateurs de votre organisation ainsi qu'à ceux des organisations partenaires avec lesquelles vous avez collaboré lorsque vous exécutiez AD RMS.

    De plus, si vous avez déployé l’[extension d’appareil mobile](http://technet.microsoft.com/library/dn673574.aspx) pour prendre en charge des appareils mobiles tels que des téléphones et iPad iOS, des téléphones et tablettes Android, des téléphones Windows Phone et des ordinateurs Mac, vous devez supprimer les enregistrements SRV dans le système DNS qui redirigeaient ces clients pour utiliser AD RMS.


[**PHASE 3 : CONFIGURATION DES SERVICES DE PRISE EN CHARGE**](migrate-from-ad-rms-phase3.md)


- **Étape 6 : Configurer l’intégration de l’IRM avec Exchange Online**

    Cette étape est requise si vous souhaitez utiliser Exchange Online avec Azure RMS.


- **Étape 7 : Déployer le connecteur RMS**

    Cette étape est requise si vous souhaitez utiliser l'un des services locaux suivants avec Azure RMS :

    - Exchange Server (par exemple, règles de transport et Outlook Web Access)

    - SharePoint Server

    - Windows Server exécutant une infrastructure de classification des fichiers (FCI, File Classification Infrastructure)


[**PHASE 4 : TÂCHES DE POST-MIGRATION**](migrate-from-ad-rms-phase4.md )

- **Étape 8 : Désaffecter AD RMS**

    Après avoir vérifié que tous les clients utilisent Azure RMS et n'accèdent plus aux serveurs AD RMS, vous pouvez désaffecter votre déploiement AD RMS.


- **Étape 9 : Renouveler votre clé de locataire Azure RMS**

    Cette étape est facultative, mais elle est recommandée si la topologie de clé de locataire Azure RMS choisie à l’étape 2 est Gérée par Microsoft. Cette étape n’est pas applicable si la topologie de clé de locataire Azure RMS choisie est Gérée par le client (BYOK).


## Étapes suivantes
Pour démarrer la migration, passez à la [Phase 1 : Configuration côté serveur](migrate-from-ad-rms-phase1.md).




<!--HONumber=Aug16_HO4-->


