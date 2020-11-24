---
title: Comparer Azure Information Protection avec AD RMS – AIP
description: Si vous connaissez ou avez déjà déployé Active Directory Rights Management Services (AD RMS), vous vous demandez peut-être ce qui le différencie d’Azure Information Protection en termes de fonctionnement et de configuration requise.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: dad175a5dad6218bf0380a7804a7a85c528c47ed
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567851"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Comparaison d’Azure Information Protection avec AD RMS

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si vous connaissez ou avez déjà déployé les services AD RMS (Active Directory Rights Management Services), vous vous demandez peut-être ce qui les différencie d’Azure Information Protection du point de vue du fonctionnement et des prérequis en tant que solution de protection des informations.

Voici quelques-unes des principales différences pour Azure Information Protection :

- **Aucune infrastructure serveur nécessaire** : Azure Information Protection n’a pas besoin de serveurs et de certificats PKI supplémentaires, contrairement à AD RMS, car Microsoft Azure s’en occupe pour vous. Ainsi, cette solution cloud est plus rapide à déployer et plus facile à gérer.

- **Authentification basée sur le cloud** : Azure Information Protection utilise Azure AD pour l’authentification, à la fois pour les utilisateurs internes et les utilisateurs d’autres organisations. Cela signifie que vos utilisateurs peuvent être authentifiés même s’ils ne sont pas connectés à votre réseau interne et qu’il est plus facile de partager du contenu protégé avec des utilisateurs d’autres organisations. De nombreuses organisations disposent déjà de comptes d’utilisateur dans Azure AD, car ils exécutent des services Azure ou ont Microsoft 365. Si ce n’est pas le cas, RMS for individuals permet aux utilisateurs de créer un compte gratuit. Il est également possible d’utiliser un compte Microsoft pour les [applications qui prennent en charge ce type d’authentification pour Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents). En comparaison, pour partager AD RMS contenu protégé avec une autre organisation, vous devez configurer des approbations explicites avec chaque organisation.

- **Prise en charge intégrée des appareils mobiles**: aucune modification du déploiement n’est nécessaire pour Azure information protection pour la prise en charge des appareils mobiles et des ordinateurs Mac. Pour prendre en charge ces appareils avec AD RMS, vous devez installer l’extension Appareils mobiles, configurer les services AD FS pour la fédération et créer des enregistrements supplémentaires pour votre service DNS public.

- **Modèles par défaut**: Azure information protection crée automatiquement des modèles par défaut qui restreignent l’accès du contenu à votre propre organisation. Ces modèles facilitent le démarrage immédiat de la protection des données sensibles. Il n’existe aucun modèle par défaut pour AD RMS.

- **Modèles départementaux**: également appelés modèles délimités. Azure Information Protection prend en charge les modèles départementaux pour les modèles supplémentaires que vous créez. Cette configuration vous permet de définir un groupe d’utilisateurs autorisés à voir des modèles spécifiques dans leurs applications clientes. Le nombre de modèles rendus visibles étant limité, les utilisateurs peuvent plus facilement sélectionner la stratégie appropriée que vous définissez pour différents groupes d’utilisateurs. AD RMS ne prend pas en charge les modèles départementaux.

- **Suivi et révocation des documents**: Azure information protection prend en charge ces fonctionnalités avec le client Azure information protection (Classic), contrairement à AD RMS.

- **Classification et étiquetage**: Azure information protection prend en charge les étiquettes qui appliquent la classification et éventuellement la protection. Ces fonctionnalités sont fournies avec le [client Azure information protection (Classic) et le client d’étiquetage unifié Azure information protection](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers). À l’aide de ces clients, la classification et l’étiquetage peuvent être intégrés aux applications Office, à l’Explorateur de fichiers, à PowerShell et à un scanneur pour les magasins de données locaux. AD RMS ne prend pas en charge ces fonctionnalités de classification et d’étiquetage.

De plus, Azure Information Protection étant un service cloud, il peut offrir des correctifs et de nouvelles fonctionnalités plus rapidement qu’une solution de serveur locale. Aucune nouvelle fonctionnalité n’est planifiée pour AD RMS dans Windows Server.

Pour les autres différences, utilisez le tableau suivant pour une comparaison côte à côte. Si vous avez des questions spécifiques concernant la sécurité, consultez la section [Contrôles de chiffrement pour la signature et le chiffrement](#cryptographic-controls-for-signing-and-encryption) dans cet article.

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Prend en charge les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Microsoft Online Services et les produits serveur Microsoft locaux.|Prend en charge les fonctionnalités de gestion des droits relatifs à l’information (IRM) pour les produits serveur Microsoft locaux et Exchange Online.|
|Active automatiquement la collaboration sécurisée sur les documents de toutes les organisations qui utilisent aussi Azure AD pour l’authentification.|La collaboration sécurisée sur les documents externes à l’organisation exige que des approbations d’authentification soient explicitement définies dans une relation point à point directe entre deux organisations. Vous devez configurer des domaines d’utilisateurs approuvés ou des approbations fédérées créées avec les services AD FS (Active Directory Federation Services).|
|Envoyez un e-mail protégé (avec éventuellement des documents Office en pièce jointe qui sont automatiquement protégés) aux utilisateurs quand aucune relation d’approbation d’authentification n’existe. Ce scénario est possible en utilisant la fédération avec les fournisseurs de réseaux sociaux ou un code secret à usage unique, ainsi qu’un navigateur web pour l’affichage.|Ne prend pas en charge pas l’envoi d’e-mails protégés quand aucune relation d’approbation d’authentification n’existe.|
|Prend en charge le client Azure Information Protection (Classic) et le client d’étiquetage unifié Azure Information Protection pour les activités de protection et de consommation.|Prend en charge le client Azure Information Protection (Classic) pour les activités de protection et de consommation. <br /><br />Prend en charge le client d’étiquetage unifié Azure Information Protection à des fins de consommation uniquement et vous devez installer l' [extension d’appareil Mobile services AD RMS (Active Directory Rights Management Services)](./active-directory-rights-manage-mobile-device.md).
|Prend en charge l'authentification multifacteur (Multi-Factor Authentication, MFA) pour les ordinateurs et les appareils mobiles.<br /><br />Pour plus d’informations, consultez [Multi-Factor Authentication (MFA) et Azure Information Protection](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Prend en charge l'authentification par carte à puce si IIS est configuré pour demander des certificats.|
|Prend en charge le mode de chiffrement 2 par défaut pour fournir un niveau de sécurité recommandé pour les longueurs de clés et les algorithmes de chiffrement.|Prend en charge le mode de chiffrement 1 par défaut et requiert une configuration supplémentaire pour prendre en charge le mode de chiffrement 2 pour un niveau de sécurité recommandé.<br /><br />Pour plus d’informations, consultez [Modes de chiffrement d’AD RMS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh867439(v=ws.10)).|
|Requiert une licence Azure Information Protection ou une licence Azure Rights Management avec Microsoft 365 pour protéger du contenu. <br /><br />Aucune licence n’est nécessaire pour utiliser du contenu protégé par Azure Information Protection (y compris si les utilisateurs appartiennent à une autre organisation).<br /><br />Pour plus d’informations sur les licences, y compris les différences entre une licence P1 et P2, consultez la [liste des fonctionnalités](https://www.microsoft.com/cloud-platform/azure-information-protection-features) du site Azure information protection.|Nécessite une licence RMS pour protéger du contenu et utiliser du contenu protégé par AD RMS.<br /><br />Pour plus d’informations sur les licences, consultez [licences d’accès client et licences de gestion](https://www.microsoft.com/Licensing/product-licensing/client-access-license.aspx) pour obtenir des informations générales, mais contactez votre partenaire Microsoft ou un représentant Microsoft pour obtenir des informations spécifiques.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Contrôles de chiffrement pour la signature et le chiffrement
Par défaut, Azure Information Protection utilise la norme RSA 2048 pour tout le chiffrement à clé publique et la norme SHA 256 pour les opérations de signature. Par comparaison, AD RMS prend en charge les normes RSA 1024 et RSA 2048, ainsi que les normes SHA 1 ou SHA 256 pour les opérations de signature.

Azure Information Protection et AD RMS utilisent la norme AES 128 pour le chiffrement symétrique.

Azure Information Protection est conforme à la norme FIPS 140-2 lorsque la taille de votre clé de locataire est de 2 048 bits, ce qui correspond à la taille par défaut quand le service Azure Rights Management est activé. 

Pour plus d’informations sur les contrôles de chiffrement, consultez [Contrôles de chiffrement utilisés par Azure RMS : algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la configuration requise pour utiliser Azure Information Protection, comme la prise en charge des appareils et les versions minimales, consultez [Configuration requise pour les Azure information protection](requirements.md).

Si vous envisagez de migrer de AD RMS vers Azure Information Protection, consultez [migration de AD RMS vers Azure information protection](migrate-from-ad-rms-to-azure-rms.md).

Prise en main de [services AD RMS (Active Directory Rights Management Services) extension d’appareil mobile](./active-directory-rights-manage-mobile-device.md). 

Les forums aux questions suivants peuvent vous intéresser :
- [Quelle est la différence entre Azure Information Protection et Microsoft Information Protection ?](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Quelle est la différence entre Information Protection et Azure Rights Management ?](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)