---
title: Détails BYOK-Azure Information Protection
description: Comprenez les détails et les restrictions lorsque vous utilisez des clés gérées par le client (appelées « apportez votre propre clé » ou BYOK) avec Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 11/22/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4a82afdeee9459b460b98a385102147c6c78ff28
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935178"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>BYOK les détails de votre propre clé pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Les organisations qui ont un abonnement incluant Azure Information Protection peuvent configurer leur client Azure Information Protection pour utiliser une clé gérée par le client et [consigner son utilisation](log-analyze-usage.md). La configuration de clé gérée par le client est souvent appelée « mettre votre propre clé », ou BYOK.

Cette clé gérée par le client doit être stockée dans Azure Key Vault, ce qui nécessite un abonnement Azure. Pour utiliser une clé protégée par module HSM, vous devez utiliser le niveau de service Azure Key Vault Premium. L’utilisation d’une clé dans Azure Key Vault entraîne des frais mensuels. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

Quand vous utilisez Azure Key Vault pour votre clé de locataire Azure Information Protection, nous vous recommandons d’utiliser un coffre de clés dédié à cette clé pour garantir qu’il est utilisé seulement par le service Azure Rights Management. Cette configuration permet d’éviter que des appels effectués par d’autres services n’entraînent un dépassement des [limites de service](/azure/key-vault/key-vault-service-limits) pour le coffre de clés, ce qui peut limiter les temps de réponse pour le service Azure Rights Management.  

De plus, étant donné que chaque service qui utilise Azure Key Vault a généralement des exigences différentes pour la gestion des clés, nous vous recommandons d’utiliser un abonnement Azure distinct avec ce coffre de clés afin de limiter les risques de configuration incorrecte. 

Toutefois, si vous souhaitez partager un abonnement Azure avec d’autres services qui utilisent Azure Key Vault, assurez-vous que l’abonnement partage un groupe d’administrateurs commun. De cette façon, les administrateurs qui utilisent cet abonnement ont une bonne compréhension de toutes les clés auxquelles ils ont accès et risquent moins de les configurer incorrectement. 

Par exemple, utilisez un abonnement Azure partagé si les administrateurs de votre clé de locataire Azure Information Protection sont aussi ceux qui gèrent les clés pour la clé de client Office 365 et CRM Online. 

En guise d’alternative, si les administrateurs qui gèrent les clés pour la clé du client ou CRM Online ne sont pas les mêmes que ceux qui administrent votre clé de locataire Azure Information Protection, nous vous recommandons de ne pas partager votre abonnement Azure pour Azure Information Protection.

## <a name="benefits-of-using-azure-key-vault"></a>Avantages de l’utilisation d’Azure Key Vault

Pour des assurances supplémentaires, vous pouvez référencer votre journalisation de l’utilisation de l’Azure Information Protection avec la [journalisation Azure Key Vault](/azure/key-vault/key-vault-logging). Les journaux de Key Vault vous permettent de surveiller indépendamment que seul le service Azure Rights Management utilise votre clé. Si nécessaire, vous pouvez révoquer immédiatement l’accès à la clé en supprimant les autorisations sur le coffre de clés.

Voici d’autres avantages de l’utilisation de Azure Key Vault pour votre clé de locataire Azure Information Protection :

- Azure Key Vault fournit une solution centralisée et cohérente de gestion de clés pour de nombreux services cloud et même locaux utilisant le chiffrement.

- Azure Key Vault prend en charge plusieurs interfaces intégrées pour la gestion de clés, notamment PowerShell, CLI, les API REST et le portail Azure. D’autres outils et services sont intégrés à Azure Key Vault dans le but de fournir des fonctionnalités optimisées pour des tâches spécifiques, comme la surveillance. Par exemple, vous pouvez analyser vos journaux d’utilisation des clés via Log Analytics à partir d’Operations Management Suite, définir des alertes quand des critères spécifiés sont remplis, etc.

- Azure Key Vault offre une séparation des rôles, qui est une bonne pratique reconnue en matière de sécurité. Les administrateurs d’Azure Information Protection peuvent se concentrer sur la gestion de la protection et la classification des données, tandis que les administrateurs d’Azure Key Vault peuvent se concentrer sur la gestion des clés de chiffrement et des stratégies spéciales qui peuvent nécessiter une sécurité ou une conformité.

- Certaines organisations ont des restrictions quant à l’emplacement où doit se trouver leur clé principale. Azure Key Vault offre un niveau élevé de contrôle quant à l’emplacement où la clé principale est stockée car le service est disponible dans de nombreuses régions Azure. Vous pouvez choisir parmi un certain nombre de régions Azure et vous pouvez vous attendre à ce que ce nombre augmente. Pour plus d’informations, consultez la page [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) sur le site Azure.

Outre la gestion des clés, Azure Key Vault offre à vos administrateurs de sécurité la même expérience de gestion pour stocker, utiliser et gérer les certificats et les secrets (comme les mots de passe) pour d’autres services et applications qui utilisent le chiffrement. 

Pour plus d’informations sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](/azure/key-vault/key-vault-whatis) et visitez le [blog de l’équipe Azure Key Vault](https://blogs.technet.microsoft.com/kv/) pour obtenir les informations les plus récentes et découvrir comment d’autres services utilisent cette technologie.

## <a name="byok-support-for-services-and-clients"></a>Prise en charge de BYOK pour les services et les clients

BYOK et la [journalisation de l’utilisation](log-analyze-usage.md) fonctionnent de façon transparente avec chaque application qui s’intègre au service Azure Rights Management utilisé par Azure information protection pour protéger les données. Ceci comprend des services cloud comme SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui utilisent le service Azure Rights Management avec le connecteur RMS, et des applications clientes comme Office 2019, Office 2016 et Office 2013. 

Vous recevez les journaux d’utilisation de la clé, quelle que soit l’application qui envoie des requêtes au service Azure Rights Management.

## <a name="next-steps"></a>Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé locataire Azure Information Protection.

