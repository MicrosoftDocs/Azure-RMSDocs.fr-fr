---
title: Conserver votre propre clé de protection (HYOK) pour Azure Information Protection
description: Vue d’ensemble de la protection HYOK (AD RMS) pour Azure Information Protection, et des scénarios pris en charge, limitations, prérequis et recommandations liés à cette protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: c5e401f831cfed9080ae1454c6ee73377591c176
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568193"
---
# <a name="hold-your-own-key-hyok-details-for-azure-information-protection"></a>Conserver les informations de votre propre clé (HYOK) pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Conserver vos propres configurations de clé (HYOK) permet aux clients AIP avec le client classique de protéger du contenu très sensible tout en conservant le contrôle total de leur clé. HYOK utilise une clé supplémentaire, détenue par le client et stockée localement pour le contenu hautement sensible, ainsi que la protection basée sur le Cloud par défaut utilisée pour d’autres contenus. 

Pour plus d’informations sur les clés de racine de locataire par défaut basées sur le Cloud, consultez [planification et implémentation de votre clé de locataire Azure information protection](plan-implement-tenant-key.md).

## <a name="cloud-based-protection-vs-hyok"></a>Protection basée sur le Cloud et HYOK

En règle générale, la protection des documents et e-mails sensibles à l’aide de Azure Information Protection utilise une clé basée sur le Cloud qui est [générée par Microsoft](plan-implement-tenant-key.md#tenant-root-keys-generated-by-microsoft) ou [par le client, à l’aide d’une configuration BYOK](byok-price-restrictions.md). 

Les clés basées sur le Cloud sont gérées dans Azure Key Vault, ce qui offre aux clients les avantages suivants :

- **Aucune configuration requise pour l’infrastructure de serveur.** Les solutions Cloud sont plus rapides et plus économiques à déployer et à entretenir que les solutions locales.

- **L’authentification basée sur le Cloud facilite le** partage avec les partenaires et les utilisateurs d’autres organisations. 

- **Intégration étroite avec d’autres services Azure et Microsoft 365**, tels que la recherche, les visionneuses Web, les vues croisées dynamiques, les logiciels anti-programmes malveillants, EDiscovery et Delve.

- **Suivi** des documents, **révocation** et **notifications par courrier électronique** pour les documents sensibles que vous avez partagés.

Toutefois, certaines organisations peuvent avoir des exigences réglementaires qui nécessitent le chiffrement d’un contenu spécifique à l’aide d’une clé qui est isolée du Cloud. Cette isolation signifie que le contenu chiffré ne peut être lu que par des applications locales et des services locaux.

Avec les configurations HYOK, les locataires client ont une [clé basée](plan-implement-tenant-key.md) sur le Cloud à utiliser avec le contenu qui peut être stocké sur le Cloud, et une clé locale pour le contenu qui doit être protégé localement uniquement.

## <a name="hyok-guidance-and-best-practices"></a>Conseils et bonnes pratiques pour la protection HYOK

Lors de la configuration de HYOK, tenez compte des recommandations suivantes :

- [Contenu adapté à HYOK](#content-suitable-for-hyok)
- [Définir les utilisateurs qui peuvent voir les étiquettes configurées par HYOK](#define-the-users-who-can-see-hyok-configured-labels)
- [HYOK et support électronique](#hyok-and-email-support)

> [!IMPORTANT]
> Une configuration HYOK pour Azure Information Protection n’est pas un remplacement pour un déploiement entièrement AD RMS et Azure Information Protection, ou une alternative à la [migration de AD RMS vers Azure information protection](migrate-from-ad-rms-to-azure-rms.md). 
>
> HYOK est pris en charge uniquement par l’application d’étiquettes, n’offre pas de parité de fonctionnalité avec AD RMS et ne prend pas en charge toutes les configurations de déploiement AD RMS.

### <a name="content-suitable-for-hyok"></a>Contenu adapté à HYOK

La protection HYOK ne fournit pas les avantages de la protection basée sur le Cloud et est souvent au détriment de l’opacité des données, car le contenu est accessible uniquement par les applications et services locaux. Même pour les organisations qui utilisent la protection HYOK, elles ne conviennent généralement que pour un petit nombre de documents. 

Nous vous recommandons d’utiliser HYOK uniquement pour le contenu qui répond aux critères suivants :

- Contenu avec la classification la plus élevée au sein de votre organisation (« top secret »), où l’accès est limité à seulement quelques personnes
- Contenu qui n’est pas partagé à l’extérieur de l’Organisation
- Contenu consommé uniquement sur le réseau interne.

### <a name="define-the-users-who-can-see-hyok-configured-labels"></a>Définir les utilisateurs qui peuvent voir les étiquettes configurées par HYOK

Pour vous assurer que seuls les utilisateurs qui ont besoin d’appliquer la protection HYOK, consultez les étiquettes configurées HYOK, configurez votre stratégie pour ces utilisateurs avec des [stratégies délimitées](configure-policy-scope.md).

### <a name="hyok-and-email-support"></a>HYOK et support électronique

Les services de Microsoft 365 et d’autres services en ligne ne peuvent pas déchiffrer le contenu protégé par HYOK.

Pour les e-mails, cette perte de fonctionnalités comprend des scanneurs de logiciels malveillants, la protection Encrypt-Only, les solutions de prévention de perte de données (DLP), les règles de routage de messagerie, la journalisation, la eDiscovery, les solutions d’archivage et Exchange ActiveSync.

Les utilisateurs peuvent ne pas comprendre pourquoi certains appareils ne peuvent pas ouvrir des e-mails protégés par HYOK, ce qui conduit à des appels supplémentaires à votre support technique. Tenez compte de ces limitations importantes lors de la configuration de la protection HYOK avec les e-mails.

## <a name="supported-applications-for-hyok"></a>Applications prises en charge pour HYOK

Utilisez Azure Information Protection étiquettes pour appliquer des HYOK à des documents et des e-mails spécifiques. HYOK est pris en charge pour les versions d’Office 2013 et ultérieures.

HYOK est une option de configuration d’administrateur pour les étiquettes, et les flux de travail restent les mêmes, que le contenu utilise comme clé basée sur le Cloud ou HYOK.

Les tableaux suivants répertorient les scénarios pris en charge pour la protection et l’utilisation du contenu à l’aide d’étiquettes configurées par HYOK :

- [Prise en charge des applications Windows pour HYOK](#windows-application-support-for-hyok)
- [prise en charge des applications macOS pour HYOK](#macos-application-support-for-hyok)
- [prise en charge des applications iOS pour HYOK](#ios-application-support-for-hyok)
- [Prise en charge des applications Android pour HYOK](#android-application-support-for-hyok)

> [!NOTE]
> Les applications Web et universelles Office ne sont pas prises en charge pour HYOK.

### <a name="windows-application-support-for-hyok"></a>Prise en charge des applications Windows pour HYOK

|Application  |Protection  |Consommation  |
|---------|---------|---------|
|Azure Information Protection client avec Microsoft 365 Apps, Office 2019, Office 2016 et Office 2013 :</br>Word, Excel, PowerPoint, Outlook     | ![Oui](media/yes-icon.png)        | ![Oui](media/yes-icon.png)        |
|Client Azure Information Protection avec l’Explorateur de fichiers     | ![Oui](media/yes-icon.png)        | ![Oui](media/yes-icon.png) |
|Visionneuse Azure Information Protection     |   Non applicable      |  ![Oui](media/yes-icon.png)       |
|Client Azure Information Protection avec les applets de commande d’étiquetage PowerShell     | ![Oui](media/yes-icon.png)        | ![Oui](media/yes-icon.png)        |
|Scanneur Azure Information Protection     |![Oui](media/yes-icon.png)       |   ![Oui](media/yes-icon.png)      |
| | | |

### <a name="macos-application-support-for-hyok"></a>prise en charge des applications macOS pour HYOK

|Application|Protection|Consommation|
|----------------------|----------|-----------|
|Office pour Mac : </br>Word, Excel, PowerPoint, Outlook|![Non](media/no-icon.png)|![Oui](media/yes-icon.png)|
| | | |

### <a name="ios-application-support-for-hyok"></a>prise en charge des applications iOS pour HYOK

|Application|Protection|Consommation|
|----------------------|----------|-----------|
|Office Mobile : </br>Word, Excel, PowerPoint|![Non](media/no-icon.png)| ![Oui](media/yes-icon.png)|
|Office Mobile : </br>Outlook uniquement|![Non](media/no-icon.png)|![Non](media/no-icon.png)|
|Visionneuse Azure Information Protection|Non applicable|![Oui](media/yes-icon.png)|

### <a name="android-application-support-for-hyok"></a>Prise en charge des applications Android pour HYOK

|Application|Protection|Consommation|
|----------------------|----------|-----------|
|Office Mobile : </br>Word, Excel, PowerPoint|![Non](media/no-icon.png)| ![Oui](media/yes-icon.png)|
|Office Mobile : </br>Outlook uniquement|![Non](media/no-icon.png)|![Non](media/no-icon.png)|
|Visionneuse Azure Information Protection|Non applicable| ![Oui](media/yes-icon.png)|


## <a name="implementing-hyok"></a>Implémentation de la protection HYOK

Azure Information Protection prend en charge HYOK lorsque vous avez un services AD RMS (Active Directory Rights Management Services) (AD RMS) qui est conforme à toutes les [exigences listées ci-dessous](#requirements-for-ad-rms-to-support-hyok).

Les stratégies de droits d’utilisation et la clé privée de l’organisation qui protège ces stratégies sont gérées et conservées localement, tandis que la stratégie de Azure Information Protection pour l’étiquetage et la classification reste gérée et stockée dans Azure.

Pour implémenter la protection HYOK :

1. [Vérifier que votre système est conforme à la configuration requise pour la AD RMS](#requirements-for-ad-rms-to-support-hyok)
1. [Localiser les informations que vous souhaitez protéger](#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

Quand vous êtes prêt, passez à [la procédure de configuration d’une étiquette pour la protection de Rights Management](configure-policy-protection.md).

### <a name="requirements-for-ad-rms-to-support-hyok"></a>Prérequis d’un déploiement AD RMS pour prendre en charge HYOK

Un déploiement AD RMS doit remplir les conditions suivantes pour fournir une protection HYOK pour les étiquettes Azure Information Protection :

|Condition requise  |Description  |
|---------|---------|
|**Configuration de AD RMS**     |Votre système de AD RMS doit être configuré de manière spécifique pour prendre en charge HYOK. Pour plus d’informations, voir [ci-dessous](#ad-rms-configuration-requirements).          |
|**Synchronisation de répertoires**     |La synchronisation d’annuaires doit être configurée entre votre Active Directory local et le Azure Active Directory. </br></br>Les utilisateurs qui utiliseront des étiquettes de protection HYOK doivent être configurés pour l’authentification unique.         |
|**Configuration pour les approbations explicitement définies**     |Si vous partagez du contenu protégé par HYOK avec d’autres personnes en dehors de votre organisation, AD RMS devez être configuré pour les approbations explicitement définies dans une relation de point à point directe avec les autres organisations. </br></br>Pour ce faire, utilisez des domaines d’utilisateur approuvé (utilisateurs approuvés) ou des approbations fédérées créées à l’aide de Services ADFS (AD FS).         |
|**Version prise en charge de Microsoft Office**     | Les utilisateurs qui protègent ou consomment du contenu protégé par HYOK doivent disposer des éléments suivants : </br></br>-Une version d’Office qui prend en charge les informations Rights Management (IRM) </br>-Microsoft Office professionnel plus version 2013 ou ultérieure avec Service Pack 1, exécuté sur Windows 7 Service Pack 1 ou version ultérieure. </br>-Pour l’édition Office 2016 Microsoft Installer (. msi), vous devez disposer de la [mise à jour 4018295 pour Microsoft Office 2016 publiée le 2018 6 mars](https://support.microsoft.com/help/4018295/march-6-2018-update-for-office-2016-kb4018295). </br></br>**Remarque :** Office 2010 et Office 2007 ne sont pas pris en charge.        |

> [!IMPORTANT]
> Pour s’assurer de la haute garantie offerte par HYOK protection, nous vous recommandons d’effectuer les opérations suivantes :
> - En localisant vos serveurs AD RMS en dehors de votre DMZ et en vous assurant qu’ils sont utilisés uniquement par les appareils gérés.
>
> - Configurez votre cluster AD RMS avec un module de sécurité matériel (HSM). Cela permet de s’assurer que la clé privée de votre certificat de licence serveur ne peut pas être exposée ou volée si votre déploiement de AD RMS doit être compromis ou compromis.

> [!TIP]
> Pour obtenir des informations et des instructions sur le déploiement pour AD RMS, consultez [Services AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831364(v=ws.11)) dans la bibliothèque Windows Server. 

#### <a name="ad-rms-configuration-requirements"></a>Configuration requise pour la AD RMS

Pour prendre en charge HYOK, assurez-vous que votre système AD RMS possède les configurations suivantes :

|Condition requise  |Description  |
|---------|---------|
|**Version de Windows**     |Au minimum, l’une des versions suivantes de Windows : </br></br>**Environnements de production :** Windows Server 2012 R2</br>**Environnements de test/évaluation**: Windows Server 2008 R2 avec Service Pack 1        |
|**Topologie**     |HYOK requiert l’une des topologies suivantes : </br>-Une seule forêt, avec un seul cluster AD RMS </br>-Plusieurs forêts, avec AD RMS clusters dans chacune d’elles. </br></br>**Licences pour plusieurs forêts**</br> Si vous avez plusieurs forêts, chaque cluster AD RMS partage une URL de licence qui pointe vers le même cluster AD RMS. </br>Sur ce cluster AD RMS, importez tous les certificats de domaine d’utilisateur approuvé à partir de tous les autres clusters AD RMS. </br>Pour plus d’informations sur cette topologie, consultez [Domaine d’utilisateur approuvé](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd983944(v=ws.10)). </br></br>**Étiquettes de stratégie globale pour plusieurs forêts**</br>Quand vous avez plusieurs clusters AD RMS dans des forêts distinctes, supprimez toutes les étiquettes de la stratégie globale qui appliquent la protection HYOK (AD RMS) et qui configurent une [stratégie délimitée](configure-policy-scope.md) pour chaque cluster. <br>Affectez des utilisateurs pour chaque cluster à leur stratégie délimitée, en vous assurant que vous n’utilisez pas de groupes qui aboutissent à l’affectation d’un utilisateur à plusieurs stratégies délimitées.</br>Chaque utilisateur doit avoir des étiquettes pour un seul cluster AD RMS.          |
|**Mode de chiffrement**     | Votre AD RMS doit être configuré avec le [mode de chiffrement 2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh867439(v=ws.10)). </br>Confirmez le mode en activant l’onglet **général** des propriétés du cluster AD RMS.        |
|**Configuration de l’URL de certification**     | Chaque serveur de AD RMS doit être configuré pour l’URL de certification. </br>Pour plus d’informations, voir [ci-dessous](#configuring-ad-rms-servers-to-locate-the-certification-url).        |
|**Points de connexion de service**     | Un point de connexion de service (SCP) n’est pas utilisé lorsque vous utilisez AD RMS protection avec Azure Information Protection. </br></br>**Si vous avez inscrit un SCP pour votre déploiement AD RMS**, supprimez-le pour vous assurer que la [détection du service](./rms-client/client-deployment-notes.md#rms-service-discovery) est réussie pour la protection Azure Rights Management. </br></br>**Si vous installez un nouveau cluster de AD RMS pour hyok**, n’inscrivez pas le SCP lors de la configuration du premier nœud. Pour chaque nœud supplémentaire, assurez-vous que le serveur est configuré pour l’URL de certification avant d’ajouter le rôle AD RMS et de rejoindre le cluster existant.         |
|**SSL/TLS**     |Dans les environnements de production, les serveurs AD RMS doivent être configurés pour utiliser SSL/TLS avec un certificat x. 509 valide qui est approuvé par les clients qui se connectent. </br></br>Cela n’est pas nécessaire à des fins de test ou d’évaluation.         |
|**Modèles de droits**     |Vous devez disposer de modèles de droits configurés pour votre AD RMS.         |
|**IRM Exchange**    |Votre AD RMS ne peut pas être configurée pour Exchange IRM.         |
|**Appareils mobiles/ordinateurs Mac**     | L' [extension d’appareil Mobile services AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)) doit être installée et configurée.        |


#### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configuration de serveurs AD RMS pour localiser l’URL de certification

1. Sur chaque serveur AD RMS dans le cluster, créez l’entrée de registre suivante :

    ```sh
    Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    ```

    Pour le \<string value> , spécifiez l’une des chaînes suivantes :

    |Environnement  |Valeur de chaîne  |
    |---------|---------|
    |**Production** </br>(Clusters AD RMS utilisant SSL/TLS)     | `https://<cluster_name>/_wmcs/certification/certification.asmx`        |
    |**Test/évaluation** </br>(pas de SSL/TLS)     |`http://<cluster_name>/_wmcs/certification/certification.asmx`         |

2. Redémarrez IIS.

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Recherche d’informations pour spécifier la protection AD RMS avec une étiquette Azure Information Protection

La configuration des étiquettes de protection HYOK nécessite que vous spécifiiez l’URL de licence de votre cluster AD RMS. 

En outre, vous devez spécifier un modèle que vous avez configuré avec les autorisations que vous souhaitez accorder aux utilisateurs, ou permettre aux utilisateurs de définir des autorisations et des utilisateurs. 

Procédez comme suit pour rechercher le GUID du modèle et les valeurs de l’URL de licence à partir de la console services AD RMS (Active Directory Rights Management Services) :

#### <a name="locate-a-template-guid"></a>Localiser un GUID de modèle

1. développez le cluster, puis cliquez sur **Modèles de stratégies de droits**. 

1. À partir des informations sur les **modèles de stratégie de droits distribués** , copiez le GUID du modèle que vous souhaitez utiliser. 

Par exemple : **82bf3474-6efe-4fa1-8827-d1bd93339119** 

#### <a name="locate-the-licensing-url"></a>Localiser l’URL de licence

1. Cliquez sur le nom du cluster.
 
1. Dans **Détails du cluster**, copiez la valeur **Gestion des licences** valeur sans la chaîne **/_wmcs/licensing**. 

Par exemple : **https://rmscluster.contoso.com** 
    
> [!NOTE]
> Si vous avez différentes valeurs de licences extranet et intranet, spécifiez la valeur extranet uniquement si vous voulez partager du contenu protégé avec des partenaires. Les partenaires qui partagent du contenu protégé doivent être définis avec des approbations point à point explicites. 
> 
> Si vous ne partagez pas de contenu protégé, utilisez la valeur intranet et assurez-vous que tous les ordinateurs clients qui utilisent AD RMS protection avec Azure Information Protection se connectent via une connexion intranet. Par exemple, les ordinateurs distants doivent utiliser une connexion VPN.
> 

## <a name="next-steps"></a>Étapes suivantes

Lorsque vous avez terminé de configurer votre système pour prendre en charge HYOK, poursuivez la configuration des étiquettes pour la protection HYOK. Pour plus d’informations, consultez [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md).