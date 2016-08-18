---
title: "Problèmes résolus par Azure RMS | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 06f615c993d54ab1e8e4a94d7414302481d919b4
ms.openlocfilehash: 17756d4e641c10c0522f7a849634ae67630b363b


---


# Quels problèmes Azure RMS résout-il ?

*S’applique à : Azure Rights Management, Office 365*

Utilisez le tableau suivant pour identifier les besoins ou problèmes métier auxquels votre entreprise peut être confrontée, et savoir de quelle façon Azure RMS peut y remédier.

|Impératif ou problème|Résolu par Azure RMS|
|--------------------------|-----------------------|
|Protection de tous les types de fichiers|√ Dans la précédente implémentation de Rights Management, seuls les fichiers Office pouvaient être protégés, à l'aide de la protection native. Maintenant, le terme [protection générique](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection) signifie que tous les types de fichiers sont pris en charge.|
|Protection des fichiers en tout lieu|√ Quand un fichier est enregistré à un emplacement ([protection sur place](../rms-client/sharing-app-protect-in-place.md)), il reste protégé, même s’il est copié vers un emplacement de stockage non contrôlé par le service informatique, comme un service de stockage cloud.|
|Partage sécurisé des fichiers envoyés par e-mail|√ Quand un fichier est partagé par e-mail ([Partage protégé](../rms-client/sharing-app-protect-by-email.md)), il est protégé comme pièce jointe à un e-mail, avec des instructions expliquant comment ouvrir la pièce jointe protégée. Dans la mesure où le texte de l’e-mail n’est pas chiffré, son destinataire peut lire ces instructions. En revanche, le document joint est protégé, par conséquent seuls les utilisateurs autorisés peuvent l'ouvrir, même si l’e-mail ou le document est transféré à d'autres personnes.|
|Audit et surveillance|√ Vous pouvez [auditer et surveiller l’utilisation](../deploy-use/log-analyze-usage.md) de vos fichiers protégés, même quand ceux-ci sortent des limites de votre organisation.<br /><br />Par exemple, vous travaillez pour Contoso, Ltd. Vous travaillez sur un projet conjoint avec 3 personnes de Fabrikam, Inc. Vous envoyez par e-mail à ces 3 personnes un document que vous protégez et dont vous restreignez l'accès à la lecture seule. L'audit Azure RMS peut vous fournir les informations suivantes :<br /><br />- Date/heure auxquelles les destinataires de Fabrikam ont ouvert le document, le cas échéant.<br /><br />- Tentative d'ouverture du document (en vain) par d'autres personnes que vous n'avez pas spécifiées, peut-être parce qu'il a été transféré ou enregistré à un emplacement partagé auxquels des tiers ont accès.<br /><br />- Tentative d'impression ou de modification du document (en vain) par une ou plusieurs des personnes spécifiées.|
|Prise en charge des appareils les plus courants, outre les ordinateurs Windows|√ Les [appareils pris en charge](../get-started/requirements-client-devices.md) sont les suivants :<br /><br />- Téléphones et ordinateurs Windows<br /><br />- Ordinateurs Mac<br /><br />- Tablettes et téléphones iOS<br /><br />- Tablettes et téléphones Android|
|Prise en charge pour les collaborations interentreprises|√ Dans la mesure où Azure RMS est un service cloud, il n'est pas nécessaire de configurer explicitement des approbations avec d'autres entreprises pour pouvoir partager du contenu protégé avec elles. Si ces entreprises disposent déjà d'un annuaire Azure AD ou Office 365, la collaboration entre entreprises est automatiquement prise en charge. Si ce n’est pas le cas, les utilisateurs peuvent prendre un abonnement gratuit à [RMS for Individuals](rms-for-individuals.md).|
|Prise en charge des services locaux et d’Office 365|√ Azure RMS fonctionne [de façon transparente avec Office 365](office-apps-services-support.md). Vous pouvez également l’utiliser avec les services locaux suivants quand vous déployez le [connecteur RMS](../deploy-use/deploy-rms-connector.md) :<br /><br />- Exchange Server 2016<br /><br />- SharePoint Server<br /><br />- Windows Server exécutant l’infrastructure de classification des fichiers|
|Facilité d'activation|√ L’[activation du service Rights Management](../deploy-use/activate-service.md) pour les utilisateurs ne nécessite que quelques clics dans le portail Azure Classic.|
|Capacité à évoluer au sein de votre entreprise, conformément à vos besoins|√ Dans la mesure où Azure RMS s’exécute en tant que service cloud et que l’élasticité Azure permet d’évoluer et de monter en puissance, vous n’avez pas à configurer ou déployer des serveurs locaux supplémentaires.|
|Capacité à créer des stratégies simples et flexibles|√ Les [modèles de stratégie de droits personnalisés](../deploy-use/configure-custom-templates.md) permettent aux administrateurs d’appliquer des stratégies rapidement et facilement, et aux utilisateurs d’appliquer le niveau de protection qui convient à chaque document, tout en limitant l’accès au personnel interne de votre organisations.<br /><br />Par exemple, pour partager un document stratégique avec tous les employés de votre entreprise, vous pouvez appliquer une stratégie de lecture seule à tout le personnel interne. Pour un document sensible tel qu'un rapport financier, vous pouvez également limiter l'accès aux cadres de l'entreprise.|
|Prise en charge étendue des applications|√ Azure RMS est étroitement intégré aux applications et services Microsoft Office, mais prend également en charge d'autres applications grâce à l'application de partage RMS.<br /><br />√ Le [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) fournit à vos développeurs internes et aux éditeurs de logiciels les API nécessaires à la création d’applications personnalisées prenant en charge Azure RMS.<br /><br />Pour plus d’informations, consultez [Autres applications prenant en charge les API RMS](api-support.md).|
|Le service informatique doit conserver le contrôle des données|√ Les organisations peuvent choisir de gérer leur propre clé de locataire, d’utiliser la solution « [Bring Your Own Key](../plan-design/plan-implement-tenant-key.md) » (BYOK) et de stocker leur clé de locataire dans des modules de sécurité matériels (HSM).<br /><br />√ Prise en charge de l’audit et de la [journalisation de l’utilisation](../deploy-use/log-analyze-usage.md) pour vous permettre d’analyser les informations de l’entreprise, de détecter des abus et (en cas de fuite d’informations) d’effectuer un audit légal.<br /><br />√ L’accès délégué à l’aide de la [fonctionnalité de super utilisateur](../deploy-use/configure-super-users.md) garantit que le service informatique a toujours accès au contenu protégé, même si celui-ci a été protégé par un employé ne faisant plus partie de l’organisation. En comparaison, les solutions de chiffrement pair à pair présentent un risque de perte d'accès aux données de l'entreprise.<br /><br />√ Synchronisez [uniquement les attributs d’annuaire dont Azure RMS a besoin](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) pour prendre en charge une identité commune pour vos comptes Active Directory locaux, en utilisant un [outil de synchronisation d’annuaire](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison) comme Azure AD Connect.<br /><br />√ Activez l’authentification unique sans réplication des mots de passe dans le cloud, en utilisant AD FS.<br /><br />√ Les organisations ont toujours la possibilité de cesser d'utiliser Azure RMS sans perdre l'accès au contenu précédemment protégé par Azure RMS. Pour plus d’informations sur les options de désaffectation, consultez [Désaffectation et désactivation d’Azure Rights Management](../deploy-use/decommission-deactivate.md). De plus, les organisations ayant déployé Active Directory Rights Management Services (AD RMS) peuvent [migrer vers Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md) sans perdre l’accès aux données précédemment protégées par AD RMS.|
> [!TIP]
> Si vous connaissez bien la version locale de Rights Management, Active Directory Rights Management Services (AD RMS), vous pouvez consulter le tableau de comparaison dans [Comparaison d’Azure Rights Management et d’AD RMS](compare-azure-rms-ad-rms.md).

## Respect des obligations réglementaires, de conformité et de sécurité
Azure RMS respecte les obligations réglementaires, de conformité et de sécurité suivantes :

√ Utilisation du chiffrement standard et prise en charge de la norme FIPS 140-2. Pour plus d’informations, consultez les informations de [Contrôles de chiffrement utilisés par Azure RMS : algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Prise en charge des modules de sécurité matériels (HSM) Thales pour stocker votre clé de locataire dans les centres de données Microsoft Azure. Azure RMS utilise des environnements de sécurité distincts pour ses centres de données d'Amérique du Nord, de la zone EMEA (Europe, Moyen-Orient et Afrique) et d'Asie. Par conséquent, vos clés peuvent uniquement être utilisées dans votre région.

√ Certifié pour ce qui suit :

-   ISO/IEC 27001:2013 (inclut [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Attestations SOC 2 SSAE 16/ISAE 3402

-   Loi HIPAA BAA

-   Clause type de l'UE

-   L'agence FedRAMP, dans le cadre de la certification d'Azure Active Directory dans Office 365, a émis une autorisation d'utilisation par HHS

-   Niveau 1 PCI DSS

Pour plus d'informations sur ces certifications externes, consultez le [Centre de gestion de la confidentialité Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## Étapes suivantes

Pour voir à quoi ressemble Azure RMS pour les administrateurs et les utilisateurs, consultez [Azure RMS en action](what-admins-users-see.md).

Si vous voulez obtenir des informations plus techniques sur le fonctionnement d’Azure RMS, consultez [Fonctionnement d’Azure RMS](how-does-it-work.md). 


<!--HONumber=Jul16_HO3-->


