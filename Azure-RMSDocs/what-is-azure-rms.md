---
title: Vue d’ensemble de la protection Azure Rights Management - AIP
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
ms.openlocfilehash: e5a9f0039dc21942ac975aa9bf7a80cc957b40e8
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92177851"
---
# <a name="what-is-azure-rights-management"></a>En quoi consiste Azure Rights Management ?

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management (souvent abrégé en Azure RMS) est la technologie de protection utilisée par [Azure Information Protection](what-is-information-protection.md).

Azure RMS est un service de protection cloud qui utilise des stratégies de chiffrement, d’identité et d’autorisation pour aider à sécuriser les fichiers et e-mails sur plusieurs appareils, tels que les téléphones, tablettes et PC. Les paramètres de protection sont conservés avec vos données, même quand elles quittent les limites de votre organisation ; ainsi, votre contenu est protégé à l’intérieur et à l’extérieur de votre organisation.

L’illustration suivante montre comment Azure RMS fournit une protection pour Microsoft 365 ainsi que pour les serveurs et services locaux. La protection est également prise en charge par les appareils d’utilisateurs finaux courants exécutant Windows, macOS, iOS et Android.

![Fonctionnement d'Azure RMS](./media/AzRMS_elements.png)

Utilisez Azure RMS avec des abonnements Microsoft 365 ou des abonnements pour Azure Information Protection. Pour plus d’informations sur les types d’abonnements individuels et les fonctionnalités prises en charge, consultez le site [Tarification Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

### <a name="sample-azure-rms-use-case"></a>Exemple de cas d’usage d’Azure RMS

Un employé peut envoyer un document par e-mail à une entreprise partenaire, ou l’enregistrer sur son lecteur cloud.

L’utilisation de la protection permanente d’Azure RMS permet de sécuriser les données d’entreprise et peut également être légalement requise à des fins de conformité ou de découverte légale, ou en guise de bonnes pratiques pour la gestion des informations.

Azure RMS garantit que les personnes et services autorisés, par exemple la recherche et l’indexation, peuvent continuer à lire et à inspecter les données protégées.

La garantie de l’accès permanent pour les personnes et les services autorisés, également appelée « raisonnement concernant les données », est un élément essentiel dans le maintien du contrôle des données de votre organisation. Ceci peut être délicat à mettre en œuvre avec d’autres solutions de protection des informations qui utilisent le chiffrement pair à pair. 

## <a name="business-problems-solved-by-azure-rights-management"></a>Problèmes professionnels résolus par Azure Rights Management

Utilisez les listes et tableaux suivants pour identifier les besoins ou problèmes métier auxquels votre entreprise peut être confrontée pour protéger des documents et e-mails, et savoir de quelle façon la technologie Azure Rights Management peut y remédier.

- [Fonctionnalités de protection](#protection-features)
- [Fonctionnalités de collaboration](#collaboration-features)
- [Fonctionnalités de prise en charge de plateforme](#platform-support-features)
- [Fonctionnalités d’infrastructure](#infrastructure-features)

> [!TIP]
> Si vous connaissez bien la version locale de Rights Management, Active Directory Rights Management Services (AD RMS), vous pouvez consulter le tableau de comparaison dans [Comparaison d’Azure Rights Management et d’AD RMS](compare-on-premise.md).

### <a name="protection-features"></a>Fonctionnalités de protection

|Fonctionnalité  |Description  |
|---------|---------|
|**Protéger plusieurs types de fichiers**     | Dans les précédentes implémentations de Rights Management, seuls les fichiers Office pouvaient être protégés, à l’aide de la protection Rights Management native. </br></br>La protection générique initialement proposée par l’application de partage Rights Management, et désormais offerte par le client Azure Information Protection, signifie aujourd’hui que davantage de [types de fichiers](./rms-client/client-admin-guide-file-types.md) sont pris en charge.        |
|**Protection des fichiers en tout lieu** . | Quand un fichier est [protégé](./rms-client/client-classify-protect.md), il reste protégé même s’il est enregistré ou copié vers un emplacement de stockage non contrôlé par le service informatique, comme un service de stockage cloud.|
|     |         |


### <a name="collaboration-features"></a>Fonctionnalités de collaboration

|Fonctionnalité  |Description  |
|---------|---------|
|**Partager des informations en toute sécurité**     |  Les [fichiers protégés](./rms-client/client-classify-protect.md) peuvent être partagés sans risque avec d’autres personnes, par exemple en tant que pièce jointe à un e-mail ou un lien vers un site SharePoint. </br></br> Si un e-mail contient des informations sensibles, protégez-le ou utilisez l’option **Ne pas transférer** dans Outlook.       |
|**Prise en charge pour les collaborations interentreprises**     |  Dans la mesure où Azure Rights Management est un service cloud, il n’est pas nécessaire de configurer explicitement des approbations avec d’autres entreprises pour pouvoir partager du contenu protégé avec elles. </br></br>La collaboration avec d’autres organisations qui disposent déjà de Microsoft 365 ou d’un annuaire Azure AD est prise en charge automatiquement. </br></br>Pour les organisations sans Microsoft 365 ou sans annuaire Azure AD, les utilisateurs peuvent souscrire un abonnement gratuit [RMS for individuals](rms-for-individuals.md) ou utiliser une compte Microsoft pour les [applications prises en charge](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).       |
| | |

> [!TIP]
> Le fait de joindre des fichiers protégés, plutôt que de protéger l’intégralité d’un e-mail, vous permet de maintenir le texte de l’e-mail non chiffré. 
>
> Par exemple, vous souhaiterez peut-être inclure des instructions pour une première utilisation si l’e-mail est envoyé en dehors de votre organisation. Si vous joignez un fichier protégé, les instructions de base peuvent être lues par n’importe qui, mais seuls les utilisateurs autorisés pourront ouvrir le document, même si l’e-mail ou le document est transféré à d’autres personnes.

### <a name="platform-support-features"></a>Fonctionnalités de prise en charge de plateforme

Azure RMS prend en charge un large éventail de plateformes et d’applications, notamment :

|Fonctionnalité  |Description  |
|---------|---------|
|**Appareils couramment utilisés** </br>pas seulement les ordinateurs Windows     | Les [appareils clients](requirements.md#client-devices) incluent : </br></br>- Téléphones et ordinateurs Windows </br>- Ordinateurs Mac </br>- Tablettes et téléphones iOS </br>- Tablettes et téléphones Android        |
|**Services locaux**     | Azure Rights Management fonctionne [de façon transparente avec Office 365](office-apps-services-support.md). Vous pouvez également l’utiliser avec les services locaux suivants quand vous déployez le [connecteur RMS](deploy-rms-connector.md) : </br></br>- Exchange Server 2016 </br>- SharePoint Server </br>- Windows Server exécutant l’infrastructure de classification des fichiers        |
|**Extensibilité des applications**     |Azure Rights Management est étroitement intégré aux applications et services Microsoft Office, mais prend également en charge d’autres applications grâce au [client Azure Information Protection](./rms-client/aip-client.md ). </br></br>Les [SDK Azure Information Protection](./develop/developers-guide.md) fournissent à vos développeurs internes et aux éditeurs de logiciels les API dont ils ont besoin pour écrire des applications personnalisées qui prennent en charge Azure Information Protection. </br></br>Pour plus d’informations, consultez [Autres applications prenant en charge les API Rights Management ](api-support.md).         |
| | |

### <a name="infrastructure-features"></a>Fonctionnalités d’infrastructure

Azure RMS fournit les fonctionnalités suivantes pour soutenir les services informatiques et les organisations d’infrastructure :

- **Création de stratégies simples et flexibles** . Les [modèles de protection personnalisés](configure-policy-templates.md) permettent aux administrateurs d’appliquer des stratégies rapidement et facilement, et aux utilisateurs d’appliquer le niveau de protection qui convient à chaque document, tout en limitant l’accès au personnel interne de votre organisation. Exemple :

    - Pour partager un document stratégique avec tous les employés de votre entreprise, appliquez une stratégie de lecture seule à tout le personnel interne. 
    - Pour un document sensible tel qu’un rapport financier, limitez l’accès aux cadres de l’entreprise.

- **Activation simplifiée** . Pour les nouveaux abonnements, l’activation est automatique. Pour les abonnements existants, l’[activation du service Rights Management](activate-service.md) ne nécessite que quelques clics dans votre portail de gestion, ou deux commandes PowerShell.

- **Services d’audit et de supervision** . [Auditez et supervisez l’utilisation](log-analyze-usage.md) de vos fichiers protégés, même quand ceux-ci sortent des limites de votre organisation. 

    Par exemple, si un employé de Contoso, Ltd travaille sur un projet commun avec trois personnes de Fabrikam, Inc, il peut envoyer à ses partenaires Fabrikam un document protégé et limité en *lecture seule* . 

    L'audit Azure RMS peut vous fournir les informations suivantes :

    - Si les partenaires Fabrikam ont ouvert le document et quand. 
    - Si d’autres personnes, qui n’ont pas été spécifiées, ont tenté sans succès d’ouvrir le document. Cela peut se produire si l’e-mail a été transféré ou enregistré à un emplacement partagé.

    En outre, le [site de suivi des documents](./rms-client/client-track-revoke.md) permet aux utilisateurs et aux administrateurs de suivre, et si nécessaire, de révoquer l’accès à des documents protégés.

- **Capacité à évoluer au sein de votre entreprise** Dans la mesure où Azure Rights Management s’exécute en tant que service cloud et que l’élasticité Azure permet d’effectuer un scale-up et un scale-out, vous n’avez pas à configurer ou déployer des serveurs locaux supplémentaires.

- **Conservation du contrôle informatique sur les données** . Les organisations peuvent tirer parti de fonctionnalités de contrôle informatique telles que les suivantes :

    |Fonctionnalité  |Description  |
    |---------|---------|
    |Gestion des clés de locataire    |   Gérez votre propre clé de locataire à l’aide de la solution « [Bring Your Own Key](plan-implement-tenant-key.md) » (BYOK), qui stocke votre clé de locataire dans des modules de sécurité matériels (HSM).      |
    |Audit et journalisation de l’utilisation    |   Utilisez les fonctionnalités d’audit et de [journalisation de l’utilisation](log-analyze-usage.md) pour analyser les insights métier, détecter les abus et effectuer une analyse d’investigation en cas de fuite d’informations.      |
    |Délégation de l’accès     |  L’accès délégué à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md) garantit que le service informatique a toujours accès au contenu protégé, même si celui-ci a été protégé par un employé ne faisant plus partie de l’organisation. </br> En comparaison, les solutions de chiffrement pair à pair présentent un risque de perte d'accès aux données de l'entreprise.       |
    |Synchronisation Active Directory     |   Synchronisez [uniquement les attributs d’annuaire dont Azure RMS a besoin](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) afin de prendre en charge une identité commune pour vos comptes Active Directory locaux, en utilisant une [solution d’identité hybride](/azure/active-directory/hybrid/) comme Azure AD Connect.      |
    |Authentification unique     | Activez l’authentification unique sans réplication des mots de passe dans le cloud à l’aide d’AD FS.        |
    |Migration à partir d’AD RMS |Si vous avez déployé les services AD RMS (Active Directory Rights Management Services), [migrez vers le service Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) sans perdre l’accès aux données précédemment protégées par AD RMS. |
    | | |


> [!NOTE]
> Les organisations ont toujours la possibilité de cesser d’utiliser le service Azure Rights Management sans perdre l’accès au contenu précédemment protégé par Azure Rights Management. 
> 
> Pour plus d’informations, consultez [Désaffectation et désactivation d’Azure Rights Management](decommission-deactivate.md). 
> 



## <a name="security-compliance-and-regulatory-requirements"></a>Respect des obligations réglementaires, de conformité et de sécurité
Azure Rights Management respecte les obligations réglementaires, de conformité et de sécurité suivantes :

- **Utilisation du chiffrement standard et prise en charge de la norme FIPS 140-2.** Pour plus d’informations, consultez les informations de [Contrôles de chiffrement utilisés par Azure RMS : algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

- **Prise en charge du module de sécurité matériel (HSM) nCipher nShield** pour stocker votre clé de locataire dans les centres de données Microsoft Azure. 

    Azure Rights Management utilise des environnements de sécurité distincts pour ses centres de données d’Amérique du Nord, de la zone EMEA (Europe, Moyen-Orient et Afrique) et d’Asie. Par conséquent, vos clés peuvent uniquement être utilisées dans votre région.

- **Certification pour les normes suivantes :**

    -   ISO/IEC 27001:2013 (./y compris [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))
    -   Attestations SOC 2 SSAE 16/ISAE 3402
    -   HIPAA BAA
    -   Clause type de l'UE
    -   L'agence FedRAMP, dans le cadre de la certification d'Azure Active Directory dans Office 365, a émis une autorisation d'utilisation par HHS
    -   PCI DSS Level 1

Pour plus d'informations sur ces certifications externes, consultez le [Centre de confidentialité de Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir plus d’informations techniques sur le fonctionnement du service Azure Rights Management, consultez [Fonctionnement d’Azure RMS](how-does-it-work.md).
