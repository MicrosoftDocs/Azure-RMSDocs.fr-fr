---
title: Comparer Azure Information Protection avec AD RMS – AIP
description: Si vous connaissez ou avez déjà déployé Active Directory Rights Management Services (AD RMS), vous vous demandez peut-être ce qui le différencie d’Azure Information Protection en termes de fonctionnement et de configuration requise.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cbeaa6b8cd46d7e53efd076de16b0f4b2b36dcee
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789603"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Comparaison d’Azure Information Protection avec AD RMS

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si vous connaissez ou avez déjà déployé les services AD RMS (Active Directory Rights Management Services), vous vous demandez peut-être ce qui les différencie d’Azure Information Protection du point de vue du fonctionnement et des prérequis en tant que solution de protection des informations.

Voici quelques-unes des principales différences pour Azure Information Protection :

- **Aucune infrastructure de serveur nécessaire** : Azure Information Protection n’a pas besoin de serveurs et certificats PKI supplémentaires, contrairement à AD RMS, car Microsoft Azure s’en occupe pour vous. Ainsi, cette solution cloud est plus rapide à déployer et plus facile à gérer.

- **Authentification basée sur le cloud** : Azure Information Protection utilise Azure AD pour l’authentification, à la fois pour les utilisateurs internes et pour les utilisateurs d’autres organisations. Cela signifie que vos utilisateurs peuvent être authentifiés même s’ils ne sont pas connectés à votre réseau interne et qu’il est plus facile de partager du contenu protégé avec des utilisateurs d’autres organisations. De nombreuses organisations disposent déjà de comptes d’utilisateur dans Azure AD, car elles exécutent des services Azure ou Office 365. Si ce n’est pas le cas, RMS for individuals permet aux utilisateurs de créer un compte gratuit. Il est également possible d’utiliser un compte Microsoft pour les [applications qui prennent en charge ce type d’authentification pour Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents). Pour partager du contenu protégé AD RMS avec une autre organisation, vous devez configurer des approbations explicites avec chaque organisation.

- **Prise en charge intégrée des appareils mobiles** : Aucune modification du déploiement n’est nécessaire pour Azure Information Protection pour la prise en charge des appareils mobiles et des ordinateurs Mac. Pour prendre en charge ces appareils avec AD RMS, vous devez installer l’extension Appareils mobiles, configurer les services AD FS pour la fédération et créer des enregistrements supplémentaires pour votre service DNS public.

- **Modèles par défaut** : Azure Information Protection crée automatiquement des modèles par défaut qui restreignent l’accès du contenu à votre propre organisation. Ces modèles facilitent le démarrage immédiat de la protection des données sensibles. Il n’existe aucun modèle par défaut pour AD RMS.

- **Modèles départementaux** : également appelés modèles délimités. Azure Information Protection prend en charge les modèles départementaux pour les modèles supplémentaires que vous créez. Cette configuration vous permet de définir un groupe d’utilisateurs autorisés à voir des modèles spécifiques dans leurs applications clientes. Le nombre de modèles rendus visibles étant limité, les utilisateurs peuvent plus facilement sélectionner la stratégie appropriée que vous définissez pour différents groupes d’utilisateurs. AD RMS ne prend pas en charge les modèles départementaux.

- **Suivi et révocation de documents** : Azure Information Protection prend en charge ces fonctionnalités avec le client Azure Information Protection (Classic), contrairement à AD RMS.

- **Classification et étiquetage** : Azure Information Protection prend en charge ces fonctionnalités avec le [client Azure information protection (Classic) et le client d’étiquetage unifié Azure information protection](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use). Ces clients s’intègrent aux applications Office et à l’Explorateur de fichiers, contrairement à AD RMS. De plus, Azure Information Protection étant un service cloud, il peut offrir des correctifs et de nouvelles fonctionnalités plus rapidement qu’une solution de serveur locale. Aucune nouvelle fonctionnalité n’est planifiée pour AD RMS dans Windows Server.

Pour les autres différences, utilisez le tableau suivant pour une comparaison côte à côte. Si vous avez des questions spécifiques concernant la sécurité, consultez la section [Contrôles de chiffrement pour la signature et le chiffrement](#cryptographic-controls-for-signing-and-encryption) dans cet article.

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Prend en charge les fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Microsoft Online Services et les produits serveur Microsoft locaux.|Prend en charge les fonctionnalités de gestion des droits relatifs à l’information (IRM) pour les produits serveur Microsoft locaux et Exchange Online.|
|Active automatiquement la collaboration sécurisée sur les documents de toutes les organisations qui utilisent aussi Azure AD pour l’authentification.|La collaboration sécurisée sur les documents externes à l’organisation exige que des approbations d’authentification soient explicitement définies dans une relation point à point directe entre deux organisations. Vous devez configurer des domaines d’utilisateurs approuvés ou des approbations fédérées créées avec les services AD FS (Active Directory Federation Services).|
|Envoyez un e-mail protégé (avec éventuellement des documents Office en pièce jointe qui sont automatiquement protégés) aux utilisateurs quand aucune relation d’approbation d’authentification n’existe. Ce scénario est possible en utilisant la fédération avec les fournisseurs de réseaux sociaux ou un code secret à usage unique, ainsi qu’un navigateur web pour l’affichage.|Ne prend pas en charge pas l’envoi d’e-mails protégés quand aucune relation d’approbation d’authentification n’existe.|
|Prend en charge le client Azure Information Protection (Classic) et le client d’étiquetage unifié Azure Information Protection.|Prend en charge le client Azure Information Protection (Classic) et la prise en charge de la consommation uniquement pour le client d’étiquetage unifié Azure Information Protection quand vous installez également l' [services AD RMS (Active Directory Rights Management Services) extension de périphérique mobile]
|Prend en charge l'authentification multifacteur (Multi-Factor Authentication, MFA) pour les ordinateurs et les appareils mobiles.<br /><br />Pour plus d’informations, consultez [Multi-Factor Authentication (MFA) et Azure Information Protection](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Prend en charge l'authentification par carte à puce si IIS est configuré pour demander des certificats.|
|Prend en charge le mode de chiffrement 2 par défaut pour fournir un niveau de sécurité recommandé pour les longueurs de clés et les algorithmes de chiffrement.|Prend en charge le mode de chiffrement 1 par défaut et requiert une configuration supplémentaire pour prendre en charge le mode de chiffrement 2 pour un niveau de sécurité recommandé.<br /><br />Pour plus d’informations, consultez [AD RMS modes](https://go.microsoft.com/fwlink/?LinkId=266659)de chiffrement.|
|Requiert une licence Azure Information Protection ou Azure Rights Management avec Office 365 pour protéger le contenu. Aucune licence n’est nécessaire pour utiliser du contenu protégé par Azure Information Protection (y compris si les utilisateurs appartiennent à une autre organisation).<br /><br />Pour plus d’informations, consultez la [liste des fonctionnalités](https://www.microsoft.com/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection.|Nécessite une licence RMS pour protéger du contenu et utiliser du contenu protégé par AD RMS.<br /><br />Pour plus d'informations sur les licences pour AD RMS, voir [Licences d'administration (ML) et licences d'accès client (CAL)](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) , mais contacter votre partenaire Microsoft ou un représentant de Microsoft pour des informations spécifiques.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Contrôles de chiffrement pour la signature et le chiffrement
Par défaut, Azure Information Protection utilise la norme RSA 2048 pour tout le chiffrement à clé publique et la norme SHA 256 pour les opérations de signature. Par comparaison, AD RMS prend en charge les normes RSA 1024 et RSA 2048, ainsi que les normes SHA 1 ou SHA 256 pour les opérations de signature.

Azure Information Protection et AD RMS utilisent la norme AES 128 pour le chiffrement symétrique.

Azure Information Protection est conforme à la norme FIPS 140-2 lorsque la taille de votre clé de locataire est de 2 048 bits, ce qui correspond à la taille par défaut quand le service Azure Rights Management est activé. 

Pour plus d’informations sur les contrôles de chiffrement, consultez [Contrôles de chiffrement utilisés par Azure RMS : Algorithmes et longueurs de clé](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la configuration requise pour utiliser Azure Information Protection, comme la prise en charge des appareils et les versions minimales, consultez [Configuration requise pour les Azure information protection](requirements.md).

Si vous envisagez de migrer de AD RMS vers Azure Information Protection, consultez [migration de AD RMS vers Azure information protection](migrate-from-ad-rms-to-azure-rms.md).

Les forums aux questions suivants peuvent vous intéresser:
- [Quelle est la différence entre Azure Information Protection et Microsoft Information Protection?](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)
- [Quelle est la différence entre Azure Information Protection et Azure Rights Management?](faqs.md#whats-the-difference-between-azure-information-protection-and-azure-rights-management)

