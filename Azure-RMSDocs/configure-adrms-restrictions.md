---
title: Protection HYOK pour Azure Information Protection
description: Vue d’ensemble de la protection HYOK (AD RMS) pour Azure Information Protection, et des scénarios pris en charge, limitations, prérequis et recommandations liés à cette protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: 83fc8228b664acc067c6a604f3d438f39669a49a
ms.sourcegitcommit: 005307a9a2d51f230f65a902325bac0a7eff29fb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80375626"
---
# <a name="hold-your-own-key-hyok-protection-for-azure-information-protection"></a>Protection HYOK (Hold your own key) pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Prenez connaissance des informations suivantes pour comprendre le lien entre la protection HYOK (Hold Your Own Key) et Azure Information Protection, et en quoi cette protection diffère de la protection cloud par défaut. Avant d’appliquer une protection HYOK, assurez-vous de bien comprendre les cas d’usage appropriés, les scénarios pris en charge, les limitations et les prérequis. 

## <a name="cloud-based-protection-vs-hyok"></a>Protection basée sur le Cloud et HYOK

Pour protéger vos documents et e-mails les plus sensibles avec Azure Information Protection, vous appliquez généralement une clé cloud qui utilise la protection Azure Rights Management (Azure RMS). Les avantages de cette méthode sont les suivants :

- Aucune infrastructure serveur n’est exigée, ce qui rend la solution plus rapide et plus économique à déployer et à gérer qu’une solution locale.

- Simplification du partage avec les partenaires et les utilisateurs d’autres organisations à l’aide de l’authentification basée sur le cloud.

- Intégration étroite aux services Office 365 et Azure, notamment la recherche, les visionneuses web, les vues croisées dynamiques, les logiciels anti-programme malveillant, eDiscovery et Delve.

- Suivi et révocation des documents, et notification par e-mail en cas de partage de documents sensibles.

Une clé cloud protège les documents et e-mails de votre organisation à l’aide d’une clé privée qui est gérée par Microsoft (scénario par défaut) ou par vous-même (scénario BYOK, « Bring Your Own Key »). Pour plus d’informations sur les options de clé de locataire, consultez [Planification et implémentation de la clé de locataire Azure Rights Management](plan-implement-tenant-key.md).

Vous pouvez stocker vos documents et e-mails protégés dans le cloud ou localement. Pour plus d’informations sur le processus de protection avec cette clé cloud, consultez [En quoi consiste Azure Rights Management ?](what-is-azure-rms.md )

Les services Office 365 et les applications cloud de votre locataire peuvent être intégrés avec Azure Information Protection. De cette façon, les fonctions essentielles pour l’organisation, comme les services de recherche, d’indexation, d’archivage et anti-programme malveillant, continuent de s’exécuter sans interruption sur le contenu qui est protégé par Azure Information Protection. Cette capacité à lire le contenu chiffré dans ces scénarios est souvent appelée « raisonnement sur les données » (reasoning over data). Par exemple, cela permet à Exchange Online de déchiffrer les e-mails lors de la détection de programmes malveillants et d’appliquer des règles de prévention contre la perte de données (DLP) aux e-mails chiffrés.

Toutefois, pour respecter des obligations réglementaires, certaines organisations sont parfois obligées de chiffrer le contenu à l’aide d’une clé qui est isolée du cloud. Cette isolation signifie que le contenu chiffré peut être lu uniquement par les applications et services locaux. Cette option de gestion des clés correspond à la protection HYOK (Hold Your Own Key) qui est prise en charge par Azure Information Protection. Quand vous utilisez Azure Information Protection avec HYOK, votre locataire a deux clés : une clé stockée dans le cloud et une clé locale.

## <a name="hyok-guidance-and-best-practices"></a>Conseils et bonnes pratiques pour la protection HYOK

Utilisez la protection HYOK uniquement pour les documents et e-mails pour lesquels la clé de chiffrement doit être isolée du cloud. La protection HYOK n’offre pas tous les avantages offerts par la protection à l’aide d’une clé cloud. Son utilisation entraîne souvent une certaine « opacité des données ». En d’autres termes, seuls les applications et services locaux peuvent accéder aux données protégées par HYOK ; les applications et services cloud ne peuvent pas raisonner sur des données protégées par HYOK.

Même dans les organisations qui l’utilisent, la protection HYOK convient généralement pour protéger un petit nombre de documents. Nous vous conseillons de l’utiliser uniquement pour des documents qui remplissent tous les critères suivants :

- Le contenu a le niveau de classification le plus élevé au sein de votre organisation (« Top Secret ») et l’accès est limité à seulement quelques personnes

- Le contenu n’est pas partagé en dehors de l’organisation

- Le contenu est utilisé uniquement sur le réseau interne

Étant donné que la protection HYOK est une option de configuration administrateur pour les étiquettes, les flux de travail utilisateur restent inchangés, indépendamment de la protection appliquée (HYOK ou avec une clé cloud).

Les [stratégies délimitées](configure-policy-scope.md) constituent un bon moyen de vous assurer que les utilisateurs qui ont besoin d’appliquer la protection HYOK sont les seuls à voir les étiquettes configurées pour cette protection. 

## <a name="supported-scenarios-for-hyok"></a>Scénarios de protection HYOK pris en charge

Pour appliquer une protection HYOK, utilisez les étiquettes Azure Information Protection. 

Le tableau suivant liste les scénarios qui prennent en charge la protection du contenu à l’aide d’étiquettes configurées avec HYOK, ainsi que l’ouverture (l’utilisation) du contenu protégé par HYOK.

|Plateforme|Application|Pris en charge|
|----------------------|----------|-----------|
|Windows|Client Azure Information Protection avec applications Office 365, Office 2019, Office 2016 et Office 2013 <br /><br />- Word, Excel, PowerPoint|Protection : oui<br /><br />Utilisation : oui|
|Windows|Client Azure Information Protection avec applications Office 365, Office 2019, Office 2016 et Office 2013 <br /><br />- Outlook|Protection : oui<br /><br />Utilisation : oui|
|Windows|Client Azure Information Protection avec l’Explorateur de fichiers|Protection : oui <br /><br />Utilisation : oui|
|Windows|Visionneuse Azure Information Protection|Protection : non applicable<br /><br />Utilisation : oui|
|Windows|Client Azure Information Protection avec les applets de commande d’étiquetage PowerShell|Protection : oui<br /><br />Utilisation : oui|
|Windows|Scanneur Azure Information Protection|Protection : oui<br /><br />Utilisation : oui|
|Windows|Application de partage Rights Management|Protection : non<br /><br />Utilisation : oui|
|MacOS|Office pour Mac <br /><br /> - Word, Excel, PowerPoint|Protection : non<br /><br />Utilisation : oui|
|MacOS|Office pour Mac<br /><br />- Outlook|Protection : non<br /><br />Utilisation : oui|
|MacOS|Application de partage Rights Management|Protection : non<br /><br />Utilisation : oui|
|iOS|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protection : non<br /><br />Utilisation : oui|
|iOS|Office Mobile <br /><br />\- Outlook|Protection : non<br /><br />Utilisation : non|
|iOS|Visionneuse Azure Information Protection|Protection : non applicable<br /><br />Utilisation : oui|
|Android|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protection : non<br /><br />Utilisation : oui|
|Android|Office Mobile <br /><br />- Outlook|Protection : non<br /><br />Utilisation : non|
|Android|Visionneuse Azure Information Protection|Protection : non applicable<br /><br />Utilisation : oui|
|Internet|Outlook sur le web|Protection : non<br /><br />Utilisation : non|
|Internet|Office pour le Web<br /><br />- Word, Excel, PowerPoint|Protection : non<br /><br />Utilisation : non|
|Universal|Applications Office Universal<br /><br />- Word, Excel, PowerPoint|Protection : non<br /><br />Utilisation : non|


## <a name="additional-limitations-when-using-hyok"></a>Limitations supplémentaires lors de l’utilisation de la solution HYOK

L’utilisation de la protection HYOK avec des étiquettes Azure Information Protection présente les autres limitations suivantes :

- Ne prend pas en charge les versions d’Office antérieures à Office 2013.

- Les services Office 365 et autres services en ligne ne peuvent pas déchiffrer les documents et e-mails protégés par HYOK pour inspecter leur contenu et effectuer les actions nécessaires. Cette limitation s’étend aux documents et e-mails protégés par HYOK et auxquels s’applique une protection du connecteur Rights Management. 
    
    Cette perte de fonctionnalités pour les e-mails protégés par HYOK inclut les scanneurs anti-programme malveillant, les solutions de prévention contre la perte de données (DLP), les règles de routage des e-mails, la journalisation, eDiscovery, les solutions d’archivage et Exchange ActiveSync. De plus, les utilisateurs risquent de ne pas comprendre pourquoi certains appareils ne peuvent pas ouvrir leurs e-mails protégés par HYOK, et vont appeler votre support technique pour obtenir de l’aide. En raison de toutes ces limitations, nous vous déconseillons d’appliquer une protection HYOK aux e-mails.

## <a name="implementing-hyok"></a>Implémentation de la protection HYOK

La protection HYOK est prise en charge par Azure Information Protection quand vous avez un déploiement Active Directory Rights Management Services (AD RMS) opérationnel qui remplit les exigences décrites dans la section suivante. Dans ce scénario, les stratégies de droits d’utilisation et la clé privée de l’organisation qui protège ces stratégies sont gérées et conservées en local, tandis que la stratégie Azure Information Protection pour l’étiquetage et la classification est gérée et stockée dans Azure. 

L’utilisation de la protection HYOK pour Azure Information Protection ne doit pas être confondue avec l’utilisation d’un déploiement complet d’AD RMS et d’Azure Information Protection, et ne remplace pas non plus une migration d’AD RMS vers Azure Information Protection. La protection HYOK est uniquement prise en charge avec l’étiquetage, elle n’offre pas de parité de fonctionnalités avec AD RMS et elle ne prend pas en charge toutes les configurations de déploiement d’AD RMS :

- Pour plus d’informations sur les scénarios que HYOK prend en charge pour protéger du contenu et utiliser le contenu protégé, consultez la section [Scénarios de protection HYOK pris en charge](#supported-scenarios-for-hyok).

- Pour obtenir des instructions sur la migration à partir d’AD RMS, consultez [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

- Pour plus d’informations sur les prérequis d’un déploiement AD RMS, consultez la section suivante.

### <a name="requirements-for-ad-rms-to-support-hyok"></a>Prérequis d’un déploiement AD RMS pour prendre en charge HYOK

Un déploiement AD RMS doit remplir les prérequis suivants pour prendre en charge la protection HYOK avec les étiquettes Azure Information Protection.

- Configuration d’AD RMS :
    
  - Version minimale de Windows Server 2012 R2 : obligatoire pour les environnements de production, mais à des fins de test ou d’évaluation, vous pouvez utiliser une version minimale de Windows Server 2008 R2 avec Service Pack 1.
    
  - Une des topologies suivantes :
        
    - Forêt unique avec un seul cluster racine AD RMS. 
        
    - Plusieurs forêts avec des clusters racines AD RMS indépendants, les utilisateurs n’ayant pas accès au contenu protégé par les utilisateurs des autres forêts.
        
    - Plusieurs forêts avec des clusters AD RMS dans chacune d’elles. Chaque cluster AD RMS partage une URL de licence qui pointe vers le même cluster AD RMS. Sur ce cluster AD RMS, vous devez importer tous les certificats de domaine utilisateur approuvé à partir de tous les autres clusters AD RMS. Pour plus d’informations sur cette topologie, consultez [Domaine d’utilisateur approuvé](https://technet.microsoft.com/library/dd983944(v=ws.10).aspx).
        
    Quand vous avez plusieurs clusters AD RMS dans des forêts distinctes, supprimez toutes les étiquettes de la stratégie globale qui appliquent la protection HYOK (AD RMS) et qui configurent une [stratégie délimitée](configure-policy-scope.md) pour chaque cluster. Affectez ensuite les utilisateurs de chaque cluster à leur stratégie délimitée, en vous assurant que vous n’utilisez pas des groupes qui entraîneraient l’affectation d’un utilisateur à plusieurs stratégies délimitées. Chaque utilisateur doit avoir des étiquettes pour un seul cluster AD RMS. 
    
  - [Mode de chiffrement 2](https://technet.microsoft.com/library/hh867439.aspx): vous pouvez confirmer le mode en vérifiant les propriétés du cluster AD RMS, onglet **Général**.
    
  - Chaque serveur AD RMS est configuré pour l’URL de certification. [Instructions](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
  - Un point de connexion de service (SCP) n’est pas inscrit dans Active Directory : aucun SCP n’est utilisé quand vous appliquez la protection AD RMS avec Azure Information Protection. 
    
      - Si vous avez inscrit un SCP pour votre déploiement AD RMS, vous devez le supprimer pour que la [découverte du service](./rms-client/client-deployment-notes.md#rms-service-discovery) fonctionne pour la protection Azure Rights Management. 
        
      - Si vous installez un nouveau cluster AD RMS pour HYOK, ignorez l’étape qui consiste à inscrire le SCP lors de la configuration du premier nœud. Pour chaque nœud supplémentaire, assurez-vous que le serveur est configuré pour l’URL de certification avant d’ajouter le rôle AD RMS et de rejoindre le cluster existant.
    
  - Les serveurs AD RMS sont configurés pour utiliser SSL/TLS avec un certificat x.509 valide qui est approuvé par les clients qui se connectent : obligatoire pour les environnements de production, mais non obligatoire à des fins de test ou d’évaluation.
    
  - Modèles de droits configurés.
    
  - Pas de configuration pour Exchange IRM.
    
  - Pour les appareils mobiles et les ordinateurs Mac : [Active Directory Rights Management Services Mobile Device Extension](https://technet.microsoft.com/library/dn673574.aspx) est installé et configuré.

- La synchronisation d’annuaires est configurée entre votre annuaire Active Directory local et votre annuaire Azure Active Directory, et les utilisateurs qui utilisent la protection HYOK sont configurés pour l’authentification unique.

- Si vous partagez des documents ou des e-mails protégés par HYOK avec des personnes extérieures à votre organisation : AD RMS est configuré pour des approbations définies explicitement dans une relation de point à point directe avec les autres organisations à l’aide de domaines d’utilisateurs approuvés ou d’approbations fédérées créés au moyen des services de fédération Active Directory (AD FS).

- Les utilisateurs exécutent une version d’Office qui prend en charge la Gestion des droits relatifs à l’information (IRM) et au moins Office Professionnel Plus 2013 avec Service Pack 1 exécuté sur Windows 7 Service Pack 1 ou ultérieur. Notez qu’Office 2010 et Office 2007 ne sont pas pris en charge dans ce scénario.
    
    - Pour l’édition Office 2016, Microsoft Installer (. msi) : vous avez installé la [mise à jour 4018295 pour Microsoft Office 2016 publiée le 2018 6 mars](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295).

> [!IMPORTANT]
> Pour garantir un niveau de protection HYOK maximal, placez si possible vos serveurs AD RMS à l’extérieur de votre réseau de périmètre et limitez leur accès uniquement à des appareils gérés. 
> 
> Nous recommandons également que votre cluster AD RMS utilise un HSM, pour que la clé privée de votre certificat de licence serveur ne puisse pas être exposée ou volée en cas de violation ou de compromission de la sécurité de votre déploiement AD RMS. 

Pour obtenir des informations et des instructions sur le déploiement pour AD RMS, consultez [Services AD RMS (Active Directory Rights Management Services)](https://technet.microsoft.com/library/hh831364.aspx) dans la bibliothèque Windows Server. 


### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configuration de serveurs AD RMS pour localiser l’URL de certification

1. Sur chaque serveur AD RMS dans le cluster, créez l’entrée de registre suivante :

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    Pour la \<valeur de chaîne>, spécifiez l’une des valeurs suivantes :
    
    - Pour les clusters AD RMS utilisant SSL/TLS :

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - Pour les clusters AD RMS qui n’utilisent pas SSL/TLS (test des réseaux uniquement) :
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. Redémarrez IIS.

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection

Quand vous configurez une étiquette pour la protection **HYOK (AD RMS)** , vous devez spécifier l’URL de licence de votre cluster AD RMS. Par ailleurs, vous devez spécifier un modèle que vous avez configuré pour les autorisations à accorder aux utilisateurs ou permettre aux utilisateurs de définir les autorisations et les utilisateurs. 

Les valeurs du GUID de modèle et de l’URL de licence sont disponibles dans la console des services AD RMS (Active Directory Rights Management Services) :

- Pour rechercher le GUID du modèle : développez le cluster, puis cliquez sur **Modèles de stratégies de droits**. Vous pouvez ensuite copier le GUID des informations **Modèles de stratégies de droits distribués** à partir du modèle à utiliser. Par exemple : 82bf3474-6efe-4fa1-8827-d1bd93339119

- Pour trouver l’URL de licence : cliquez sur le nom du cluster. Dans **Détails du cluster**, copiez la valeur **Gestion des licences** valeur sans la chaîne **/_wmcs/licensing**. Exemple : `https://rmscluster.contoso.com`. 
    
    Si vous disposez d’une valeur de licence extranet et d’une valeur de licence intranet différentes : spécifiez la valeur extranet uniquement si vous voulez partager des documents ou des e-mails protégés avec des partenaires qui ont été définis avec des approbations point à point explicites. Sinon, utilisez la valeur intranet et vérifiez que tous les ordinateurs clients qui utilisent la protection AD RMS avec Azure Information Protection se connectent au moyen d’une connexion intranet (par exemple, les ordinateurs distants utilisent une connexion VPN).


## <a name="next-steps"></a>Étapes suivantes :

Pour savoir comment configurer une étiquette pour la protection HYOK, consultez [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md). 
