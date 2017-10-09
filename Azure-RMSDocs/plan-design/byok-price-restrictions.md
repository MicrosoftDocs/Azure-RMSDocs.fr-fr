---
title: "Tarifs et restrictions liés à BYOK - Azure Information Protection"
description: "Découvrez les restrictions imposées quand vous utilisez des clés gérées par le client (BYOK, Bring Your Own Key) avec Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: afc25e638cff4bddc342ed29dee7fab304d67bd7
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="byok-pricing-and-restrictions"></a>Tarifs et restrictions BYOK

>*S’applique à : Azure Information Protection, Office 365*


Les organisations qui ont un abonnement incluant Azure Information Protection peuvent configurer leur locataire Azure Information Protection pour utiliser une clé gérée par le client (BYOK) et [consigner son utilisation](../deploy-use/log-analyze-usage.md) dans un journal sans frais supplémentaires. 

La clé doit être stockée dans Azure Key Vault, ce qui nécessite un abonnement Azure. Pour utiliser une clé protégée par module HSM, vous devez utiliser le niveau de service Azure Key Vault Premium. L’utilisation d’une clé dans Azure Key Vault entraîne des frais mensuels. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Quand vous utilisez Azure Key Vault pour votre clé de locataire Azure Information Protection, nous vous recommandons d’utiliser un coffre de clés dédié à cette clé, avec un abonnement dédié. Cette configuration permet de garantir qu’elle est utilisée seulement par le service Azure Rights Management. 

## <a name="benefits-of-using-azure-key-vault"></a>Avantages de l’utilisation d’Azure Key Vault

En plus de la journalisation de l’utilisation d’Azure Information Protection, vous pouvez doubler avec la [journalisation d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-logging/) pour surveiller de façon indépendante que seul le service Azure Rights Management utilise cette clé. Si nécessaire, vous pouvez révoquer immédiatement l’accès à la clé en supprimant les autorisations sur le coffre de clés.

Voici d’autres avantages de l’utilisation d’Azure Key Vault pour votre clé de locataire Azure Information Protection :

- Azure Key Vault fournit une solution centralisée et cohérente de gestion de clés pour de nombreux services cloud et même locaux utilisant le chiffrement.

- Azure Key Vault prend en charge plusieurs interfaces intégrées pour la gestion de clés, notamment PowerShell, CLI, les API REST et le portail Azure. D’autres outils et services sont intégrés à Azure Key Vault dans le but de fournir des fonctionnalités optimisées pour des tâches spécifiques, comme la surveillance. Par exemple, vous pouvez analyser vos journaux d’utilisation des clés via Log Analytics à partir d’Operations Management Suite, définir des alertes quand des critères spécifiés sont remplis, etc.

- Azure Key Vault offre une séparation des rôles, qui est une bonne pratique reconnue en matière de sécurité. Les administrateurs d’Azure Information Protection peuvent se concentrer sur la gestion de la protection et la classification des données, tandis que les administrateurs d’Azure Key Vault peuvent se concentrer sur la gestion des clés de chiffrement et des stratégies spéciales qui peuvent nécessiter une sécurité ou une conformité.

- Certaines organisations ont des restrictions quant à l’emplacement où doit se trouver leur clé principale. Azure Key Vault offre un niveau élevé de contrôle quant à l’emplacement où la clé principale est stockée car le service est disponible dans de nombreuses régions Azure. Actuellement, vous pouvez choisir parmi 28 régions Azure. Attendez-vous à ce que ce nombre augmente. Pour plus d’informations, consultez la page [Disponibilité des produits par région] (https://azure.microsoft.com/regions/services/) sur le site Azure.

Outre la gestion des clés, Azure Key Vault offre à vos administrateurs de sécurité la même expérience de gestion pour stocker, utiliser et gérer les certificats et les secrets (comme les mots de passe) pour d’autres services et applications qui utilisent le chiffrement. 

Pour plus d’informations sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](/azure/key-vault/key-vault-whatis) et visitez le [blog de l’équipe Azure Key Vault](https://blogs.technet.microsoft.com/kv/) pour obtenir les informations les plus récentes et découvrir comment d’autres services utilisent cette technologie.

## <a name="restrictions-when-using-byok"></a>Restrictions lors de l’utilisation de BYOK

BYOK et la journalisation de l’utilisation fonctionnent de façon homogène avec chaque application qui s’intègre au service Azure Rights Management utilisé par Azure Information Protection. Ceci comprend des services cloud comme SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui utilisent le service Azure Rights Management avec le connecteur RMS, et des applications clientes comme Office 2016 et Office 2013. Vous obtenez des journaux d’utilisation de la clé, quelle que soit l’application effectuant des demandes au service Azure Rights Management.

Si vous avez activé Exchange Online IRM en important votre domaine de publication approuvé à partir d’Azure RMS, suivez les instructions dans [Configurer de nouvelles fonctionnalités de chiffrement de messages Office 365 reposant sur Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) pour activer les nouvelles fonctionnalités dans Exchange Online qui prennent en charge BYOK pour Azure Information Protection.

## <a name="next-steps"></a>Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé de client Azure Rights Management.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
