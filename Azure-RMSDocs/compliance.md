---
title: Conformité et informations relatives à Azure Information Protection
description: Informations annexes pour Azure Information Protection qui concernent notamment les mentions légales, la conformité et les contrats de niveau de service.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b3a7127b-6d24-4439-bc4e-2a0a325e8ea3
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 708d39a5f69182225a1eea23c625b4a53a7172cd
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102414750"
---
# <a name="compliance-and-supporting-information-for-azure-information-protection"></a>Conformité et informations annexes pour Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Azure Information Protection prend en charge d’autres services et s’appuie également sur d’autres services. Si vous recherchez des informations relatives au service Azure Information Protection qui n’ont pas trait à son utilisation, consultez les ressources suivantes :

## <a name="suitability-for-different-countries"></a>Adaptation aux différents pays

Compte tenu de la diversité des lois et des réglementations dans les pays, des différents cas d’usage et scénarios, et des différentes exigences de chaque secteur d’activité, consultez votre conseiller juridique qui vous aidera à savoir si Azure Information Protection est adapté à votre pays.

Toutefois, certaines informations utiles peuvent aider votre conseiller juridique à se prononcer :

- Azure Information Protection utilise AES 256 et AES 128 pour chiffrer les documents. [Plus d’informations](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Toutes les clés de chiffrement utilisées par Azure Information Protection sont protégées avec une clé racine propre au client qui utilise RSA 2048 bits. RSA 1024 bits est également pris en charge pour la compatibilité descendante. [Plus d’informations](./how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)

- Les clés racines spécifiques au client sont gérées par Microsoft ou approvisionnées par le client dans un HSM nCipher à l’aide de la « mise en place de votre propre clé » (BYOK). Azure Information Protection prend également en charge les fonctionnalités pour la protection locale, pour le contenu qui ne peut pas être protégé par une clé basée sur le Cloud. Pour plus d’informations, consultez [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

- Le service Azure Information Protection est hébergé dans les centres de données régionaux du monde entier. Les clés et les stratégies Azure Information Protection restent toujours dans la région dans laquelle elles sont déployées à l’origine.

    > [!NOTE]
    > Les stratégies de Azure Information Protection sont pertinentes pour le client standard AIP uniquement.
    >
  
- Azure Information Protection ne transmet pas de contenu de document de clients au service Azure Information Protection. Les opérations de chiffrement et de déchiffrement de contenu sont effectuées sur place sur l’appareil du client. Ou, pour un rendu basé sur un service, ces opérations sont effectuées dans le service qui effectue le rendu du contenu. [Plus d’informations](./how-does-it-work.md)

## <a name="legal-and-privacy"></a>Mentions légales et confidentialité

- Pour plus d'informations sur le contrat Microsoft Azure : [Contrat Microsoft Azure](https://azure.microsoft.com/support/legal/subscription-agreement/)

- Pour plus d'informations sur la confidentialité dans Microsoft Azure : [Déclaration de confidentialité de Microsoft Azure](https://azure.microsoft.com/support/legal/privacy-statement/)

## <a name="security-compliance-and-auditing"></a>Sécurité, conformité et audit

Consultez la section relative à la [sécurité, à la conformité et aux exigences réglementaires](./what-is-azure-rms.md#security-compliance-and-regulatory-requirements) dans l’article [qu’est-ce que Azure RMS ?](./what-is-azure-rms.md) pour plus d’informations sur les certifications spécifiques au service Azure Rights Management. De plus :

- Pour connaître les certifications externes pour Azure Information Protection : [Centre de confidentialité de Microsoft Azure](https://azure.microsoft.com/support/trust-center/)

- Pour plus d'informations sur FIPS 140 : [Validation FIPS 140](/windows/security/threat-protection/fips-140-validation)

Pour obtenir des informations techniques approfondies sur le fonctionnement de la technologie de protection, consultez [Fonctionnement d’Azure RMS](./how-does-it-work.md) 

## <a name="service-level-agreements"></a>Contrats de niveau de service

- [Contrat de niveau de service pour Azure Information Protection](https://azure.microsoft.com/support/legal/sla/information-protection/v1_0/)

- [Contrat de niveau de service pour Azure Active Directory](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/)

- [Contrat de niveau de service pour Azure Key Vault](https://azure.microsoft.com/support/legal/sla/key-vault/v1_0/)

## <a name="documentation"></a>Documentation

- Documentation Azure Active Directory : [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis)

- Documentation Microsoft 365 : [Microsoft 365 pour la documentation et les ressources d’entreprise](/Office365/Enterprise/)

