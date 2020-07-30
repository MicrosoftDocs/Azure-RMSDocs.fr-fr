---
title: Présentation d’Azure Rights Management protection-AIP
description: Informations concernant Azure Rights Management (Azure RMS), la technologie de protection utilisée par Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 1a239e489dee616ba13050a9fa6614d85bee1429
ms.sourcegitcommit: d1f6f10c9cb95de535d8121e90b211f421825caf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87297865"
---
# <a name="what-is-azure-rights-management"></a>En quoi consiste Azure Rights Management ?

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management (souvent abrégé en Azure RMS) est la technologie de protection utilisée par [Azure Information Protection](what-is-information-protection.md).

Azure RMS est un service de protection Cloud qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour sécuriser les fichiers et les e-mails sur plusieurs appareils, y compris les téléphones, les tablettes et les PC. Les paramètres de protection sont conservés avec vos données, même quand ils quittent les limites de votre organisation, ce qui empêche la protection de votre contenu à l’intérieur et à l’extérieur de votre organisation.

L’illustration suivante montre comment Azure RMS fournit la protection d’Office 365, ainsi que les serveurs et services locaux. La protection est également prise en charge par les appareils d’utilisateurs finaux populaires exécutant Windows, macOS, iOS et Android.

![Fonctionnement d'Azure RMS](./media/AzRMS_elements.png)

Utilisez Azure RMS avec les abonnements Office 365 ou les abonnements pour Azure Information Protection. Pour plus d’informations sur les types d’abonnements individuels et les fonctionnalités prises en charge, consultez le site de [tarification Azure information protection](https://azure.microsoft.com/pricing/details/information-protection/) .

### <a name="sample-azure-rms-use-case"></a>Exemple de cas d’usage Azure RMS

Les employés peuvent envoyer par courrier électronique un document à une société partenaire ou enregistrer un document sur leur lecteur Cloud.

L’utilisation de la protection permanente de Azure RMS permet de sécuriser les données d’entreprise et peut également être légalement requise pour la conformité, les exigences de découverte légale ou les meilleures pratiques pour la gestion des informations.

Azure RMS garantit que les personnes et services autorisés (recherche et indexation, par exemple) peuvent continuer à lire et inspecter les données protégées.

Garantir un accès permanent pour les personnes et les services autorisés, également appelé « raisonnement sur les données », est un élément essentiel dans le maintien du contrôle des données de votre organisation. Cette fonctionnalité peut ne pas être facilement réalisable avec d’autres solutions de protection des informations qui utilisent le chiffrement pair à pair. 

## <a name="business-problems-solved-by-azure-rights-management"></a>Problèmes professionnels résolus par Azure Rights Management

Utilisez les listes et les tables suivantes pour identifier les besoins de l’entreprise ou les problèmes que votre organisation peut avoir dans la protection des documents et des e-mails, ainsi que la façon dont la technologie Azure Rights Management peut répondre à vos besoins.

- [Fonctionnalités de protection](#protection-features)
- [Fonctionnalités de collaboration](#collaboration-features)
- [Fonctionnalités de prise en charge de plateforme](#platform-support-features)
- [Fonctionnalités de l’infrastructure](#infrastructure-features)

> [!TIP]
> Si vous êtes familiarisé avec la version locale de Rights Management, services AD RMS (Active Directory Rights Management Services) (AD RMS), vous pouvez être intéressé par le tableau de comparaison en [comparant les Rights Management Azure et les AD RMS](compare-on-premise.md).

### <a name="protection-features"></a>Fonctionnalités de protection

|Caractéristique  |Description  |
|---------|---------|
|**Protéger plusieurs types de fichiers**     | Dans les premières implémentations de Rights Management, seuls les fichiers Office pouvaient être protégés, à l’aide de la protection Native Rights Management. </br></br>À présent, la protection générique qui a été fournie par l’application de partage Rights Management, et désormais offerte par le client Azure Information Protection, signifie que davantage de [types de fichiers](./rms-client/client-admin-guide-file-types.md) sont pris en charge.        |
|**Protégez vos fichiers n’importe où**. | Lorsqu’un fichier est [protégé](./rms-client/client-classify-protect.md), la protection reste avec le fichier, même s’il est enregistré ou copié dans un stockage qui n’est pas sous le contrôle de celui-ci, tel qu’un service de stockage cloud.|
|     |         |


### <a name="collaboration-features"></a>Fonctionnalités de collaboration

|Caractéristique  |Description  |
|---------|---------|
|**Partager des informations en toute sécurité**     |  Les [fichiers protégés](./rms-client/client-classify-protect.md) peuvent être partagés avec d’autres personnes, par exemple, une pièce jointe à un message électronique ou un lien vers un site SharePoint. </br></br> Si les informations sensibles se trouvent dans un message électronique, Protégez l’e-mail ou utilisez l’option **ne pas transférer** d’Outlook.       |
|**Prise en charge pour les collaborations interentreprises**     |  Étant donné qu’Azure Rights Management est un service Cloud, il n’est pas nécessaire de configurer explicitement des approbations avec d’autres organisations avant de pouvoir partager du contenu protégé avec eux. </br></br>La collaboration avec d’autres organisations qui disposent déjà d’un annuaire Office 365 ou Azure AD est prise en charge automatiquement. </br></br>Pour les organisations sans Office 365 ou un répertoire Azure AD, les utilisateurs peuvent s’inscrire à l’abonnement gratuit [RMS for Individuals](rms-for-individuals.md) , ou utiliser une compte Microsoft pour les [applications prises en charge](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).       |
| | |

> [!TIP]
> L’attachement de fichiers protégés, plutôt que la protection de l’intégralité d’un message électronique, vous permet de garder le texte de l’e-mail non chiffré. 
>
> Par exemple, vous souhaiterez peut-être inclure des instructions pour une première utilisation si le courrier électronique est envoyé en dehors de votre organisation. Si vous attachez un fichier protégé, les instructions de base peuvent être lues par n’importe qui, mais seuls les utilisateurs autorisés pourront ouvrir le document, même si l’e-mail ou le document est transféré à d’autres personnes.

### <a name="platform-support-features"></a>Fonctionnalités de prise en charge de plateforme

Azure RMS prend en charge un large éventail de plates-formes et d’applications, notamment :

|Caractéristique  |Description  |
|---------|---------|
|**Appareils couramment utilisés** </br>pas seulement les ordinateurs Windows     | Les [périphériques clients](requirements.md#client-devices) sont les suivants : </br></br>- Téléphones et ordinateurs Windows </br>- Ordinateurs Mac </br>- Tablettes et téléphones iOS </br>- Tablettes et téléphones Android        |
|**Services locaux**     | En plus de travailler en [toute transparence avec Office 365](office-apps-services-support.md), utilisez Azure Rights Management avec les services locaux suivants lorsque vous déployez le [connecteur RMS](deploy-rms-connector.md): </br></br>- Exchange Server 2016 </br>- SharePoint Server </br>- Windows Server exécutant l’infrastructure de classification des fichiers        |
|**Extensibilité des applications**     |Azure Rights Management offre une intégration étroite avec les applications et les services Microsoft Office, et étend la prise en charge d’autres applications à l’aide du [client Azure information protection](./rms-client/aip-client.md ). </br></br>Les [Kits de développement](./develop/developers-guide.md) logiciel (sdk) Azure information protection fournissent à vos développeurs internes et aux éditeurs de logiciels des API pour écrire des applications personnalisées qui prennent en charge Azure information protection. </br></br>Pour plus d’informations, consultez [Autres applications prenant en charge les API Rights Management ](api-support.md).         |
| | |

### <a name="infrastructure-features"></a>Fonctionnalités de l’infrastructure

Azure RMS fournit les fonctionnalités suivantes pour prendre en charge les services informatiques et les organisations d’infrastructure :

- **Créez des stratégies simples et flexibles**. Les [modèles de protection personnalisés](configure-policy-templates.md) offrent une solution simple et rapide permettant aux administrateurs d’appliquer des stratégies, et aux utilisateurs d’appliquer le niveau de protection approprié pour chaque document et de restreindre l’accès aux personnes au sein de votre organisation. Par exemple :

    - Pour qu’un document de stratégie à l’ensemble de l’entreprise soit partagé avec tous les employés, appliquez une stratégie en lecture seule à tous les employés internes. 
    - Pour un document plus sensible, tel qu’un rapport financier, limitez l’accès aux cadres uniquement.

- **Activation simple**. Pour les nouveaux abonnements, l’activation est automatique. Pour les abonnements existants, [l’activation du service Rights Management](activate-service.md) ne nécessite que quelques clics dans votre portail de gestion, ou deux commandes PowerShell.

- **Services d’audit et de surveillance**. [Auditez et surveillez l’utilisation](log-analyze-usage.md) de vos fichiers protégés, même après que ces fichiers ont quitté les limites de votre organisation. 

    Par exemple, si un employé contoso, Ltd travaille sur un projet joint avec trois personnes de Fabrikam, Inc, il peut envoyer à ses partenaires Fabrikam un document protégé et limité en *lecture seule*. 

    L'audit Azure RMS peut vous fournir les informations suivantes :

    - Si les partenaires Fabrikam ont ouvert le document et quand. 
    - Si d’autres personnes, qui n’ont pas été spécifiées, ont tentées et n’ont pas pu ouvrir le document. Cela peut se produire si l’e-mail a été transféré ou enregistré dans un emplacement partagé.

    En outre, le [site de suivi des documents](./rms-client/client-track-revoke.md) permet aux utilisateurs et aux administrateurs de suivre, et si nécessaire, de révoquer l’accès à des documents protégés.

- **Possibilité de mettre à l’échelle au sein de votre organisation**. Dans la mesure où Azure Rights Management s’exécute en tant que service Cloud avec l’élasticité Azure pour évoluer, vous n’avez pas besoin d’approvisionner ou de déployer des serveurs locaux supplémentaires.

- **Maintenez le contrôle informatique sur les données**. Les organisations peuvent tirer parti des fonctionnalités de contrôle informatique, telles que :

    |Caractéristique  |Description  |
    |---------|---------|
    |Gestion des clés de locataire    |   Gérez votre propre clé de locataire à l’aide de la solution «[Bring Your Own Key](plan-implement-tenant-key.md)» (BYOK), qui stocke votre clé de locataire dans des modules de sécurité matériels (HSM).      |
    |Audit et journalisation de l’utilisation    |   Utilisez les fonctionnalités d’audit et de [journalisation de l’utilisation](log-analyze-usage.md) pour analyser les informations métier, surveiller les abus et effectuer une analyse d’investigation pour les fuites d’informations.      |
    |Délégation d’accès     |  Déléguez l’accès à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md), en veillant à ce qu’il puisse toujours accéder au contenu protégé, même si un document a été protégé par un employé qui quitte ensuite l’organisation. </br> En comparaison, les solutions de chiffrement pair à pair présentent un risque de perte d'accès aux données de l'entreprise.       |
    |Synchronisation Active Directory     |   Synchronisez [uniquement les attributs d’annuaire dont Azure RMS a besoin](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) pour prendre en charge une identité commune pour vos comptes de Active Directory locaux, à l’aide d' [une solution d’identité hybride](/azure/active-directory/hybrid/), telle que Azure ad Connect.      |
    |Authentification unique     | Activez l’authentification unique sans répliquer les mots de passe dans le Cloud, à l’aide de AD FS.        |
    |Migration à partir de AD RMS |Si vous avez déployé services AD RMS (Active Directory Rights Management Services) (AD RMS), [migrez vers le service Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) sans perdre l’accès aux données précédemment protégées par AD RMS. |
    | | |


> [!NOTE]
> Les organisations ont toujours la possibilité de cesser d’utiliser le service Azure Rights Management sans perdre l’accès au contenu précédemment protégé par Azure Rights Management. 
> 
> Pour plus d’informations, consultez [désaffectation et désactivation d’Azure Rights Management](decommission-deactivate.md). 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>Respect des obligations réglementaires, de conformité et de sécurité
Azure Rights Management prend en charge les exigences réglementaires, de conformité et de sécurité suivantes :

- **L’utilisation du chiffrement standard et prend en charge FIPS 140-2.** Pour plus d’informations, consultez les informations de [Contrôles de chiffrement utilisés par Azure RMS : algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

- **Prise en charge du module de sécurité matériel (HSM) NCipher nshield** pour stocker votre clé de locataire dans Microsoft Azure centres de données. 

    Azure Rights Management utilise des environnements de sécurité distincts pour ses centres de données d’Amérique du Nord, de la zone EMEA (Europe, Moyen-Orient et Afrique) et d’Asie. Par conséquent, vos clés peuvent uniquement être utilisées dans votre région.

- **Certification pour les normes suivantes :**

    -   ISO/IEC 27001:2013 (./includes [ISO/iec 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))
    -   Attestations SOC 2 SSAE 16/ISAE 3402
    -   HIPAA BAA
    -   Clause type de l'UE
    -   L'agence FedRAMP, dans le cadre de la certification d'Azure Active Directory dans Office 365, a émis une autorisation d'utilisation par HHS
    -   PCI DSS Level 1

Pour plus d’informations sur ces certifications externes, consultez le [Centre de confidentialité Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir plus d’informations techniques sur le fonctionnement du service Azure Rights Management, consultez [Fonctionnement d’Azure RMS](how-does-it-work.md).
