---
title: Conformité et informations relatives à Azure Information Protection
description: Informations annexes pour Azure Information Protection qui concernent notamment les mentions légales, la conformité et les contrats de niveau de service.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3d311a1055dc0973dee4b4e0f6b10c4ffcd0e537
ms.sourcegitcommit: 319c0691509748e04aecf839adaeb3b5cac2d2cf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71684250"
---
# <a name="compliance-and-supporting-information-for-azureinformation-protection"></a>Conformité et informations annexes pour Azure Information Protection

Azure Information Protection prend en charge d’autres services et s’appuie également sur d’autres services. Si vous recherchez des informations relatives au service Azure Information Protection qui n’ont pas trait à son utilisation, consultez les ressources suivantes :

## <a name="suitability-for-different-countries"></a>Adaptation aux différents pays

Compte tenu de la diversité des lois et des réglementations dans les pays, des différents cas d’usage et scénarios, et des différentes exigences de chaque secteur d’activité, consultez votre conseiller juridique qui vous aidera à savoir si Azure Information Protection est adapté à votre pays.

Toutefois, certaines informations utiles peuvent aider votre conseiller juridique à se prononcer :

- Azure Information Protection utilise AES 256 et AES 128 pour chiffrer les documents. [Plus d’informations](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Toutes les clés de chiffrement utilisées par Azure Information Protection sont protégées avec une clé racine propre au client qui utilise RSA 2048 bits. RSA 1024 bits est également pris en charge pour la compatibilité descendante. [Plus d’informations](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Les clés racines spécifiques au client sont gérées par Microsoft ou approvisionnées par le client dans un HSM nCipher à l’aide de la «mise en place[de votre propre clé](plan-implement-tenant-key.md)» (BYOK). Azure Information Protection prend également en charge des fonctionnalités limitées avec une clé locale via [HYOK](configure-adrms-restrictions.md) (Hold Your Own Key) pour le contenu qui est affecté par les spécifications indiquant qu’il ne doit pas être protégé avec une clé basée sur le cloud.

- Le service Azure Information Protection est hébergé dans les centres de données régionaux du monde entier. Les clés et les stratégies Azure Information Protection restent toujours dans la région dans laquelle elles sont déployées à l’origine.
 
- Azure Information Protection ne transmet pas de contenu de document de clients au service Azure Information Protection. Les opérations de chiffrement et de déchiffrement de contenu sont effectuées sur place sur l’appareil du client. Ou, pour un rendu basé sur un service, ces opérations sont effectuées dans le service qui effectue le rendu du contenu. [Plus d’informations](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>Mentions légales et confidentialité

- Pour Microsoft Azure d’informations sur les contrats: [Contrat Microsoft Azure](https://azure.microsoft.com/support/legal/subscription-agreement/)

- Pour plus d’Microsoft Azure informations de confidentialité: [Déclaration de confidentialité de Microsoft Azure](https://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Sécurité, conformité et audit

Consultez la section [Respect des obligations réglementaires, de conformité et de sécurité](./what-is-azure-rms.md#security-compliance-and-regulatory-requirements) de l’article [Quels problèmes Azure RMS résout-il ?](./azure-rms-problems-it-solves.md) pour plus d’informations sur les certifications spécifiques au service Azure Rights Management. De plus :

- Pour connaître les certifications externes pour Azure Information Protection : [Centre de confidentialité Microsoft Azure](https://azure.microsoft.com/support/trust-center/)

- Pour obtenir des informations sur FIPS 140: [Validation FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

Pour obtenir des informations techniques approfondies sur le fonctionnement de la technologie de protection, consultez [Fonctionnement d’Azure RMS](./how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contrats de niveau de service

- [Contrat de niveau de service pour Azure Information Protection](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Contrat de niveau de service pour Azure Active Directory](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Contrat de niveau de service pour Azure Key Vault](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>Documentation

- Documentation Azure Active Directory : [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)

- Documentation Office 365 Entreprise : [Office 365](https://docs.microsoft.com/en-us/Office365/Enterprise/)

