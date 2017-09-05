---
title: "Tarifs et restrictions liés à BYOK - Azure Information Protection"
description: "Découvrez les restrictions imposées quand vous utilisez des clés gérées par le client (BYOK, Bring Your Own Key) avec Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3c8fb56d33c1aa745975254dc9a2134db857b352
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="byok-pricing-and-restrictions"></a>Tarifs et restrictions BYOK

>*S’applique à : Azure Information Protection, Office 365*


Les organisations qui ont un abonnement incluant Azure Information Protection peuvent configurer leur locataire Azure Information Protection pour utiliser une clé gérée par le client (BYOK) et [consigner son utilisation](../deploy-use/log-analyze-usage.md) dans un journal sans frais supplémentaires. 

La clé doit être stockée dans Azure Key Vault, qui nécessite un abonnement Azure payant (ou d’évaluation), et vous devez utiliser le niveau de service Premium d’Azure Key Vault pour prendre en charge les clés protégées par HSM. L’utilisation d’une clé protégée par HSM dans Azure Key Vault entraîne des frais mensuels. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Quand vous utilisez Azure Key Vault pour votre clé de locataire Azure Information Protection, nous vous recommandons d’utiliser un coffre de clés dédié à cette clé avec un abonnement dédié, pour garantir qu’il est utilisé seulement par le service Azure Rights Management. 

## <a name="benefits-of-using-azure-key-vault"></a>Avantages de l’utilisation d’Azure Key Vault

En plus de la journalisation de l’utilisation d’Azure Information Protection, vous pouvez doubler avec la [journalisation d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-logging/) pour surveiller de façon indépendante que seul le service Azure Rights Management utilise cette clé. Si nécessaire, vous pouvez révoquer immédiatement l’accès à la clé en supprimant les autorisations sur le coffre de clés.

Voici d’autres avantages de l’utilisation d’Azure Key Vault pour votre clé de locataire Azure Information Protection :

- Azure Key Vault fournit une solution centralisée et cohérente de gestion de clés pour de nombreux services cloud et même locaux utilisant le chiffrement.

- Azure Key Vault prend en charge plusieurs interfaces intégrées pour la gestion de clés, notamment PowerShell, CLI, les API REST et le portail Azure. D’autres outils et services sont intégrés à Azure Key Vault dans le but de fournir des fonctionnalités optimisées pour des tâches spécifiques, comme la surveillance. Par exemple, vous pouvez analyser vos journaux d’utilisation des clés via Log Analytics à partir d’Operations Management Suite, définir des alertes quand des critères spécifiés sont remplis, etc.

- Azure Key Vault offre une séparation des rôles, qui est une bonne pratique reconnue en matière de sécurité. Les administrateurs d’Azure Information Protection peuvent se concentrer sur la gestion de la protection et la classification des données, tandis que les administrateurs d’Azure Key Vault peuvent se concentrer sur la gestion des clés de chiffrement et des stratégies spéciales qui peuvent nécessiter une sécurité ou une conformité.

- Certaines organisations ont des restrictions quant à l’emplacement où doit se trouver leur clé principale. Azure Key Vault offre un niveau élevé de contrôle quant à l’emplacement où la clé principale est stockée car le service est disponible dans de nombreuses régions Azure. Actuellement, vous pouvez choisir parmi 28 régions Azure. Attendez-vous à ce que ce nombre augmente. Pour plus d’informations, consultez la page [Disponibilité des produits par région] (https://azure.microsoft.com/regions/services/) sur le site Azure.

Outre la gestion des clés, Azure Key Vault offre à vos administrateurs de sécurité la même expérience de gestion pour stocker, utiliser et gérer les certificats et les secrets (comme les mots de passe) pour d’autres services et applications qui utilisent le chiffrement. 

Pour plus d’informations sur Azure Key Vault, consultez [Qu’est-ce qu’Azure Key Vault ?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) et visitez le [blog de l’équipe Azure Key Vault](https://blogs.technet.microsoft.com/kv/) pour obtenir les informations les plus récentes et découvrir comment d’autres services utilisent cette technologie.


## <a name="restrictions-when-using-byok"></a>Restrictions lors de l’utilisation de BYOK

BYOK et la journalisation de l’utilisation fonctionnent de façon transparente avec chaque application qui s’intègre au service Azure Rights Management (Azure RMS) utilisé par Azure Information Protection. Sont compris : les services cloud, comme SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui fonctionnent avec Azure RMS grâce au connecteur RMS, et les applications clientes comme Office 2016 et Office 2013. Vous obtenez des journaux d'utilisation de la clé, quelle que soit l'application effectuant des requêtes Azure RMS.

Il existe une exception : Actuellement, la solution **Azure RMS BYOK n'est pas compatible avec Exchange Online** :

![BYOK ne prend pas en charge Exchange Online](../media/RMS_BYOK_noExchange.png)

Si vous souhaitez utiliser Exchange Online, nous vous recommandons de déployer Azure RMS maintenant en mode de gestion de clés par défaut dans lequel Microsoft génère et gère votre clé. Vous avez la possibilité de passer à la solution BYOK ultérieurement, par exemple, quand Exchange Online prend en charge Azure RMS BYOK. Toutefois, si vous ne pouvez pas attendre, une autre option consiste à déployer Azure RMS avec la solution BYOK et des fonctionnalités RMS réduites pour Exchange Online (les pièces jointes et messages électroniques non protégés restent entièrement fonctionnels) :

-   Il n'est pas possible d'afficher les pièces jointes ou messages électroniques protégés dans Outlook Web Access.

-   Il n'est pas possible d'afficher les messages électroniques protégés sur des appareils mobiles utilisant l'IRM Exchange ActiveSync.

-   Le déchiffrement du transport (par exemple, pour détecter des logiciels malveillants) et le déchiffrement du journal étant impossibles, les messages électroniques et pièces jointes protégés sont ignorés.

-   Les règles de protection du transport et la protection contre la perte de données (DLP) qui appliquent les stratégies IRM ne sont pas disponibles. La protection RMS ne peut donc pas être appliquée à l'aide de ces méthodes.

-   La recherche basée sur les serveurs de messages électroniques protégés n’est pas disponible. Les messages électroniques protégés sont donc ignorés.

Lorsque vous utilisez la solution BYOK Azure RMS avec des fonctionnalités RMS réduites pour Exchange Online, RMS fonctionne avec les clients de messagerie dans Outlook sur Mac et Windows et sur d'autres clients de messagerie qui n'utilisent pas Exchange ActiveSync IRM.

Si vous effectuez une migration vers Azure RMS depuis AD RMS, vous avez peut-être importé votre clé comme domaine de publication approuvé (TPD) dans Exchange Online (également appelé BYOK dans la terminologie d’Exchange, qui est distincte du BYOK d’Azure Key Vault). Dans ce scénario, vous devez supprimer le domaine de publication approuvé d'Exchange Online afin d'éviter les modèles et stratégies en conflit. Pour plus d’informations, consultez [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) dans la bibliothèque d’applets de commande Exchange Online.

Parfois, l'exception BYOK d'Azure RMS pour Exchange Online n'est pas un problème dans la pratique. Par exemple, les organisations qui souhaitent utiliser la solution BYOK et la journalisation exécutent leurs applications de données (Exchange, SharePoint, Office) en local et utilisent Azure RMS pour les fonctionnalités qui ne sont pas facilement disponibles avec AD RMS en local (par exemple, collaboration avec d'autres sociétés et accès à partir de clients mobiles). La solution BYOK et la journalisation fonctionnent bien dans ce scénario et offrent aux organisations un contrôle total sur leur abonnement Azure RMS.

## <a name="next-steps"></a>Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé de client Azure Rights Management.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
