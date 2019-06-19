---
title: Tarifs et restrictions liés à BYOK - Azure Information Protection
description: Découvrez les restrictions imposées quand vous utilisez des clés gérées par le client (BYOK, Bring Your Own Key) avec Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 11d3370e67ae643e870000fbaba3349d725a4428
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156335"
---
# <a name="byok-pricing-and-restrictions"></a>Tarifs et restrictions BYOK

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Les organisations qui ont un abonnement incluant Azure Information Protection peuvent configurer leur locataire Azure Information Protection pour utiliser une clé gérée par le client (BYOK) et [consigner son utilisation](./log-analyze-usage.md). 

La clé doit être stockée dans Azure Key Vault, ce qui nécessite un abonnement Azure. Pour utiliser une clé protégée par module HSM, vous devez utiliser le niveau de service Azure Key Vault Premium. L’utilisation d’une clé dans Azure Key Vault entraîne des frais mensuels. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

Quand vous utilisez Azure Key Vault pour votre clé de locataire Azure Information Protection, nous vous recommandons d’utiliser un coffre de clés dédié à cette clé pour garantir qu’il est utilisé seulement par le service Azure Rights Management. Cette configuration permet d’éviter que des appels effectués par d’autres services n’entraînent un dépassement des [limites de service](/azure/key-vault/key-vault-service-limits) pour le coffre de clés, ce qui peut limiter les temps de réponse pour le service Azure Rights Management.  

De plus, étant donné que chaque service qui utilise Azure Key Vault a généralement des exigences différentes pour la gestion des clés, nous vous recommandons d’utiliser un abonnement Azure distinct avec ce coffre de clés afin de limiter les risques de configuration incorrecte. 

Toutefois, si vous souhaitez partager un abonnement Azure avec d’autres services qui utilisent Azure Key Vault, assurez-vous que l’abonnement partage un groupe d’administrateurs commun. De cette façon, les administrateurs qui utilisent cet abonnement ont une bonne compréhension de toutes les clés auxquelles ils ont accès et risquent moins de les configurer incorrectement. Par exemple, utilisez un abonnement Azure partagé si les administrateurs de votre clé de locataire Azure Information Protection sont aussi ceux qui gèrent les clés pour la clé de client Office 365 et CRM Online. En revanche, si les administrateurs qui gèrent les clés pour la clé de client ou CRM Online ne sont pas ceux qui administrent votre clé de locataire Azure Information Protection, nous vous recommandons de ne pas partager votre abonnement Azure pour Azure Information Protection.

## <a name="benefits-of-using-azure-key-vault"></a>Avantages de l’utilisation d’Azure Key Vault

En plus de la journalisation de l’utilisation d’Azure Information Protection, vous pouvez doubler avec la [journalisation d’Azure Key Vault](/azure/key-vault/key-vault-logging) pour surveiller de façon indépendante que seul le service Azure Rights Management utilise cette clé. Si nécessaire, vous pouvez révoquer immédiatement l’accès à la clé en supprimant les autorisations sur le coffre de clés.

Voici d’autres avantages de l’utilisation d’Azure Key Vault pour votre clé de locataire Azure Information Protection :

- Azure Key Vault fournit une solution centralisée et cohérente de gestion de clés pour de nombreux services cloud et même locaux utilisant le chiffrement.

- Azure Key Vault prend en charge plusieurs interfaces intégrées pour la gestion de clés, notamment PowerShell, CLI, les API REST et le portail Azure. D’autres outils et services sont intégrés à Azure Key Vault dans le but de fournir des fonctionnalités optimisées pour des tâches spécifiques, comme la surveillance. Par exemple, vous pouvez analyser vos journaux d’utilisation des clés via Log Analytics à partir d’Operations Management Suite, définir des alertes quand des critères spécifiés sont remplis, etc.

- Azure Key Vault offre une séparation des rôles, qui est une bonne pratique reconnue en matière de sécurité. Les administrateurs d’Azure Information Protection peuvent se concentrer sur la gestion de la protection et la classification des données, tandis que les administrateurs d’Azure Key Vault peuvent se concentrer sur la gestion des clés de chiffrement et des stratégies spéciales qui peuvent nécessiter une sécurité ou une conformité.

- Certaines organisations ont des restrictions quant à l’emplacement où doit se trouver leur clé principale. Azure Key Vault offre un niveau élevé de contrôle quant à l’emplacement où la clé principale est stockée car le service est disponible dans de nombreuses régions Azure. Actuellement, vous pouvez choisir parmi 28 régions Azure, ce nombre étant appelé à augmenter. Pour plus d’informations, consultez la page [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) sur le site Azure.

Outre la gestion des clés, Azure Key Vault offre à vos administrateurs de sécurité la même expérience de gestion pour stocker, utiliser et gérer les certificats et les secrets (comme les mots de passe) pour d’autres services et applications qui utilisent le chiffrement. 

Pour plus d’informations sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](/azure/key-vault/key-vault-whatis) et visitez le [blog de l’équipe Azure Key Vault](https://blogs.technet.microsoft.com/kv/) pour obtenir les informations les plus récentes et découvrir comment d’autres services utilisent cette technologie.

## <a name="restrictions-when-using-byok"></a>Restrictions lors de l’utilisation de BYOK

BYOK et la journalisation de l’utilisation fonctionnent de façon homogène avec chaque application qui s’intègre au service Azure Rights Management utilisé par Azure Information Protection. Ceci comprend des services cloud comme SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui utilisent le service Azure Rights Management avec le connecteur RMS, et des applications clientes comme Office 2019, Office 2016 et Office 2013. Vous obtenez des journaux d’utilisation de la clé, quelle que soit l’application effectuant des demandes au service Azure Rights Management.

Si vous avez activé Exchange Online IRM en important votre domaine de publication approuvé à partir d’Azure RMS, suivez les instructions dans [Configurer de nouvelles fonctionnalités de chiffrement de messages Office 365 reposant sur Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) pour activer les nouvelles fonctionnalités dans Exchange Online qui prennent en charge BYOK pour Azure Information Protection.

## <a name="next-steps"></a>Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé locataire Azure Information Protection.

