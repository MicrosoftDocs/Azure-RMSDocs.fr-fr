---
title: Vue d’ensemble de la protection Azure Rights Management d’Azure Information Protection – AIP
description: Informations concernant Azure Rights Management (Azure RMS), la technologie de protection utilisée par Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: aeeebcd7-6646-4405-addf-ee1cc74df5df
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ba44c23b56c2832268f0ed6df122a347c9a8fdf3
ms.sourcegitcommit: 2a1c0882d2b0400f4da6370dbc1830df09867e3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53218457"
---
# <a name="what-is-azure-rights-management"></a>En quoi consiste Azure Rights Management ?

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Rights Management (souvent abrégé en Azure RMS) est la technologie de protection utilisée par [Azure Information Protection](what-is-information-protection.md).

Ce service de protection cloud utilise des stratégies de chiffrement, d’identité et d’autorisation pour sécuriser vos fichiers et e-mails, et fonctionne sur plusieurs appareils tels que des téléphones, tablettes et PC. Des informations peuvent être protégées tant au sein qu'en dehors de votre organisation, car cette protection reste associées aux données, même quand celles-ci quittent les limites de votre organisation.

Par exemple, un employé peut envoyer un document par e-mail à une entreprise partenaire, ou l’enregistrer sur son lecteur cloud. La protection permanente offerte par Azure RMS permet de sécuriser les données de votre entreprise. Elle peut également être nécessaire à des fins de conformité, de communication préalable ou simplement de bonne gestion des informations.

Mais plus important encore, les personnes et services autorisés (recherche et indexation, par exemple) peuvent continuer à lire et inspecter les données protégées. Ceci n’est pas facile à mettre en œuvre avec d’autres solutions de protection des informations qui utilisent le chiffrement pair à pair. Cette fonctionnalité, parfois appelée « reasoning over data », est un élément déterminant pour conserver le contrôle des données de votre entreprise.

L’illustration suivante montre comment ce service fournit une solution de protection pour Office 365, ainsi que pour les serveurs et services locaux. Elle montre également que cette protection est prise en charge par les appareils d’utilisateurs finaux courants qui exécutent Windows, Mac OS, iOS, Android et Windows Phone.


![Fonctionnement d'Azure RMS](./media/AzRMS_elements.png)

Vous pouvez utiliser cette protection avec les abonnements Office 365 et avec les abonnements pour Azure Information Protection. Pour plus d’informations sur les abonnements disponibles et les fonctionnalités qu’ils prennent en charge, visitez le site [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/).

## <a name="business-problems-solved-by-azure-rights-management"></a>Problèmes professionnels résolus par Azure Rights Management

Utilisez le tableau suivant pour identifier les besoins ou problèmes métier auxquels votre entreprise peut être confrontée pour protéger des documents et e-mails, et savoir de quelle façon la technologie Azure Rights Management peut y remédier.


|Impératif ou problème|Résolu par Azure RMS|
|--------------------------|-----------------------|
|Protéger plusieurs types de fichiers|√ Dans les précédentes implémentations de Rights Management, seuls les fichiers Office pouvaient être protégés, à l’aide de la protection Rights Management. La **protection générique** d’abord proposée par l’application de partage Rights Management et désormais offerte par le client Azure Information Protection signifie que davantage de [types de fichiers](./rms-client/client-admin-guide-file-types.md) sont pris en charge.|
|Protection des fichiers en tout lieu|√ Quand un fichier est [protégé](./rms-client/client-classify-protect.md), il reste protégé, même s’il est enregistré ou copié vers un emplacement de stockage non contrôlé par le service informatique, comme un service de stockage cloud.|
|Partager des informations en toute sécurité|√ Lorsqu’un fichier est [protégé](./rms-client/client-classify-protect.md), le partage avec d’autres utilisateurs est sécurisé. Il peut s’agir, par exemple, d’une pièce jointe à un e-mail ou d’un lien vers un site SharePoint. Si un e-mail contient des informations sensibles, vous pouvez le protéger ou simplement utiliser l’option Ne pas transférer dans Outlook. <br /><br />L’avantage de joindre un fichier protégé plutôt que de protéger l’intégralité de l’e-mail est que le texte de ce dernier n’est pas chiffré. Ainsi, si l’e-mail est envoyé à l’extérieur de votre organisation, vous pouvez inclure des instructions pour la première utilisation. Tout le monde peut lire les instructions, mais le document joint est protégé, par conséquent seuls les utilisateurs autorisés peuvent l’ouvrir, même si l’e-mail ou le document est transféré à d’autres personnes.|
|Audit et surveillance|√ Vous pouvez [auditer et surveiller l’utilisation](log-analyze-usage.md) de vos fichiers protégés, même quand ceux-ci sortent des limites de votre organisation.<br /><br />Par exemple, vous travaillez pour Contoso, Ltd. Vous travaillez sur un projet conjoint avec trois personnes de Fabrikam, Inc. Vous envoyez par e-mail à ces trois personnes un document que vous protégez et dont vous restreignez l’accès à la lecture seule. L’audit Azure Rights Management peut fournir les informations suivantes :<br /><br />- Date/heure auxquelles les destinataires de Fabrikam ont ouvert le document, le cas échéant.<br /><br />- Tentative d'ouverture du document (en vain) par d'autres personnes que vous n'avez pas spécifiées, peut-être parce qu'il a été transféré ou enregistré à un emplacement partagé auxquels des tiers ont accès.<br /><br />- Tentative d'impression ou de modification du document (en vain) par une ou plusieurs des personnes spécifiées.<br /><br />En outre, le [site de suivi des documents](./rms-client/client-track-revoke.md) permet aux utilisateurs et aux administrateurs de suivre, et si nécessaire, de révoquer l’accès à des documents protégés.|
|Prise en charge des appareils courants, outre les ordinateurs Windows|√ Les  [appareils pris en charge](./requirements-client-devices.md) sont les suivants :<br /><br />- Téléphones et ordinateurs Windows<br /><br />- Ordinateurs Mac<br /><br />- Tablettes et téléphones iOS<br /><br />- Tablettes et téléphones Android|
|Prise en charge pour les collaborations interentreprises|√ Dans la mesure où Azure Rights Management est un service cloud, il n’est pas nécessaire de configurer explicitement des approbations avec d’autres entreprises pour pouvoir partager du contenu protégé avec elles. Si ces entreprises disposent déjà d'un annuaire Azure AD ou Office 365, la collaboration entre entreprises est automatiquement prise en charge. Dans le cas contraire, les utilisateurs peuvent prendre un abonnement gratuit à [RMS for individuals](rms-for-individuals.md) ou utiliser un compte Microsoft pour [les applications qui prennent en charge ce type d’authentification pour Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|Prise en charge des services locaux et d'Office 365|√ Azure Rights Management fonctionne [de façon transparente avec Office 365](office-apps-services-support.md). Vous pouvez également l’utiliser avec les services locaux suivants quand vous déployez le [connecteur RMS](deploy-rms-connector.md) :<br /><br />- Exchange Server 2016<br /><br />- SharePoint Server<br /><br />- Windows Server exécutant l’infrastructure de classification des fichiers|
|Facilité d'activation|√ Pour les nouveaux abonnements, l’activation est automatique. Pour les abonnements existants, l’[activation du service Rights Management](activate-service.md) ne nécessite que quelques clics dans votre portail de gestion. Si vous préférez le contrôle de ligne de commande, deux commandes PowerShell suffisent.|
|Capacité à évoluer au sein de votre entreprise, conformément à vos besoins|√ Dans la mesure où Azure Rights Management s’exécute en tant que service cloud et que l’élasticité Azure permet d’évoluer et de monter en puissance, vous n’avez pas à configurer ou déployer des serveurs locaux supplémentaires.|
|Capacité à créer des stratégies simples et flexibles|√ Les  [modèles de protection personnalisés](configure-policy-templates.md) permettent aux administrateurs d’appliquer des stratégies rapidement et facilement, et aux utilisateurs d’appliquer le niveau de protection qui convient à chaque document, tout en limitant l’accès au personnel interne de votre organisation.<br /><br />Par exemple, pour partager un document stratégique avec tous les employés de votre entreprise, vous pouvez appliquer une stratégie de lecture seule à tout le personnel interne. Pour un document sensible tel qu'un rapport financier, vous pouvez également limiter l'accès aux cadres de l'entreprise.|
|Prise en charge étendue des applications|√ Azure Rights Management est étroitement intégré aux applications et services Microsoft Office, mais prend également en charge d’autres applications grâce au [client Azure Information Protection](./rms-client/aip-client.md ).<br /><br />√ Les [SDK Azure Information Protection](./develop/developers-guide.md) fournissent à vos développeurs internes et aux fournisseurs de logiciels les API dont ils ont besoin pour écrire des applications personnalisées qui prennent en charge Azure Information Protection.<br /><br />Pour plus d’informations, consultez [Autres applications prenant en charge les API Rights Management ](api-support.md).|
|Le service informatique doit conserver le contrôle des données|√ Les organisations peuvent choisir de gérer leur propre clé de locataire, d’utiliser la solution « [Bring Your Own Key](plan-implement-tenant-key.md) » (BYOK) et de stocker leur clé de locataire dans des modules de sécurité matériels (HSM).<br /><br />√ Prise en charge de l’audit et de la [journalisation de l’utilisation](log-analyze-usage.md) pour vous permettre d’analyser les informations de l’entreprise, de détecter des abus et (en cas de fuite d’informations) d’effectuer un audit légal.<br /><br />√ L’accès délégué à l’aide de la [fonctionnalité de super utilisateur](configure-super-users.md) garantit que le service informatique a toujours accès au contenu protégé, même si celui-ci a été protégé par un employé ne faisant plus partie de l’organisation. En comparaison, les solutions de chiffrement pair à pair présentent un risque de perte d'accès aux données de l'entreprise.<br /><br />√ Synchronisez [uniquement les attributs d’annuaire dont Azure RMS a besoin](/azure/active-directory/hybrid/reference-connect-sync-attributes-synchronized#azure-rms) afin de gérer une identité commune pour vos comptes Active Directory locaux, en utilisant une [solution d’identité hybride](/azure/active-directory/hybrid/) comme Azure AD Connect.<br /><br />√ Activation de l'authentification unique sans réplication des mots de passe dans le cloud, à l'aide d'AD FS.<br /><br />√ Les organisations ont toujours la possibilité de cesser d’utiliser Azure Rights Management sans perdre l’accès au contenu précédemment protégé par Azure Rights Management. Pour plus d’informations sur les options de désaffectation, consultez [Désaffectation et désactivation d’Azure Rights Management](decommission-deactivate.md). De plus, les organisations ayant déployé Active Directory Rights Management Services (AD RMS) peuvent [migrer vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) sans perdre l’accès aux données précédemment protégées par AD RMS.|
> [!TIP]
> Si vous connaissez bien la version locale de Rights Management, Active Directory Rights Management Services (AD RMS), vous pouvez consulter le tableau de comparaison dans [Comparaison d’Azure Rights Management et d’AD RMS](compare-on-premise.md).

## <a name="security-compliance-and-regulatory-requirements"></a>Respect des obligations réglementaires, de conformité et de sécurité
Azure Rights Management respecte les obligations réglementaires, de conformité et de sécurité suivantes :

√ Utilisation du chiffrement standard et prise en charge de la norme FIPS 140-2. Pour plus d’informations, consultez [Contrôles de chiffrement utilisés par Azure RMS : Algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Prise en charge des modules de sécurité matériels (HSM) Thales pour stocker votre clé de locataire dans les centres de données Microsoft Azure. Azure Rights Management utilise des environnements de sécurité distincts pour ses centres de données d’Amérique du Nord, de la zone EMEA (Europe, Moyen-Orient et Afrique) et d’Asie. Par conséquent, vos clés peuvent uniquement être utilisées dans votre région.

√ Certifié pour ce qui suit :

-   ISO/IEC 27001:2013 (./y compris [ISO/IEC 27018](https://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Attestations SOC 2 SSAE 16/ISAE 3402

-   Loi HIPAA BAA

-   Clause type de l'UE

-   L'agence FedRAMP, dans le cadre de la certification d'Azure Active Directory dans Office 365, a émis une autorisation d'utilisation par HHS

-   Niveau 1 PCI DSS

Pour plus d'informations sur ces certifications externes, consultez le [Centre de confidentialité de Azure](https://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir plus d’informations techniques sur le fonctionnement du service Azure Rights Management, consultez [Fonctionnement d’Azure RMS](how-does-it-work.md).

