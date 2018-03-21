---
title: "Conformité et informations relatives à Azure Information Protection"
description: "Informations annexes pour Azure Information Protection qui concernent notamment les mentions légales, la conformité et les contrats de niveau de service."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/12/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2980032c72905ec237dea799e8d6d13e11746df3
ms.sourcegitcommit: 29d3d4760131eb2642e17b0732f852b6d8cfe314
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2018
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Conformité et informations annexes pour Azure Information Protection

Azure Information Protection prend en charge d’autres services et s’appuie également sur d’autres services. Si vous recherchez des informations relatives au service Azure Information Protection qui n’ont pas trait à son utilisation, consultez les ressources suivantes :

## <a name="suitability-for-different-countries"></a>Adaptation aux différents pays

Compte tenu de la diversité des lois et des réglementations dans les pays, des différents cas d’usage et scénarios, et des différentes exigences de chaque secteur d’activité, consultez votre conseiller juridique qui vous aidera à savoir si Azure Information Protection est adapté à votre pays.

Toutefois, certaines informations utiles peuvent aider votre conseiller juridique à se prononcer :

- Azure Information Protection utilise AES 256 et AES 128 pour chiffrer les documents. [Plus d’informations](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Toutes les clés de chiffrement utilisées par Azure Information Protection sont protégées avec une clé racine propre au client qui utilise RSA 2048 bits. RSA 1024 est également pris en charge pour la compatibilité descendante. [Plus d’informations](../understand-explore/how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Les clés racines propres au client sont gérées par Microsoft ou provisionnées par le client dans un module HSM Thales via [BYOK](../plan-design/plan-implement-tenant-key.md) (Bring Your Own Key). Azure Information Protection prend également en charge des fonctionnalités limitées avec une clé locale via [HYOK](../deploy-use/configure-adrms-restrictions.md) (Hold Your Own Key) pour le contenu qui est affecté par les spécifications indiquant qu’il ne doit pas être protégé avec une clé basée sur le cloud.

- Le service Azure Information Protection est hébergé dans les centres de données régionaux du monde entier. Les clés et les stratégies Azure Information Protection restent toujours dans la région dans laquelle elles sont déployées à l’origine.
 
- Azure Information Protection ne transmet pas de contenu de document de clients au service Azure Information Protection. Les opérations de chiffrement et de déchiffrement de contenu sont effectuées sur place sur l’appareil du client. Ou, pour un rendu basé sur un service, ces opérations sont effectuées dans le service qui effectue le rendu du contenu. [Plus d’informations](../understand-explore/how-does-it-work.md)

## <a name="legal-and-privacy"></a>Mentions légales et confidentialité

- Pour plus d'informations sur le contrat Microsoft Azure : [Contrat Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

- Pour plus d'informations sur la confidentialité dans Microsoft Azure : [Déclaration de confidentialité de Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Sécurité, conformité et audit

Consultez la section [Respect des obligations réglementaires, de conformité et de sécurité](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) de l’article [Quels problèmes Azure RMS résout-il ?](../understand-explore/azure-rms-problems-it-solves.md) pour plus d’informations sur les certifications spécifiques au service Azure Rights Management. De plus :

- Pour connaître les certifications externes pour Azure Information Protection : [Centre de confidentialité de Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

- Pour plus d'informations sur FIPS 140 : [Validation FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

Pour obtenir des informations techniques approfondies sur le fonctionnement de la technologie de protection, consultez [Fonctionnement d’Azure RMS](../understand-explore/how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contrats de niveau de service

- [Contrat de niveau de service pour Azure Information Protection](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Contrat de niveau de service pour Azure Active Directory](https://azure.microsoft.com/en-us/support/legal/sla/active-directory/v1_0/)

- [Contrat de niveau de service pour Azure Key Vault](https://azure.microsoft.com/en-us/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>Documentation

- Documentation Azure Active Directory : [Azure Active Directory](/active-directory/)

- Bibliothèque Office 365 : [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
