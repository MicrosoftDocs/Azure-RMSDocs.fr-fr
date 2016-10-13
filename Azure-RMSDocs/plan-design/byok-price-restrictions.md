---
title: "Tarifs et restrictions liés à BYOK | Azure Information Protection"
description: Understand the restrictions when you use customer-managed keys (known as "bring your own key", or BYOK) with Azure RMS.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 36e392d7e9a2fc8cec0419a3e66f92b42137bc72
ms.openlocfilehash: 3ed4f3c770c1c34d2bda7481d8ca405c51d3fe8c


---

# Tarifs et restrictions BYOK

>*S’applique à : Azure Information Protection, Office 365*


Les organisations qui ont un abonnement incluant Azure Rights Management peuvent utiliser des clés gérées par le client (BYOK) dans Azure Key Vault et consigner son utilisation dans un journal sans frais supplémentaires. Cependant, pour utiliser Azure Key Vault, vous devez disposer d’un abonnement Azure qui prend en charge Key Vault avec des clés protégées par HSM. L’utilisation d’une clé dans Azure Key Vault entraîne des frais mensuels. Pour plus d’informations, consultez la [page Tarification d’Azure Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Si vous avez des utilisateurs qui ont souscrit un compte gratuit en utilisant RMS en tant que particuliers, vous ne pouvez pas utiliser BYOK ni la journalisation de l’utilisation car cette configuration n’a pas d’administrateur de locataire pour configurer ces fonctionnalités.


> [!NOTE]
> Pour plus d’informations sur RMS for individuals, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK ne prend pas en charge Exchange Online](../media/RMS_BYOK_noExchange.png)

BYOK et la journalisation de l’utilisation fonctionnent de façon transparente avec chaque application qui s’intègre au service Azure Rights Management (Azure RMS) utilisé par Azure Information Protection. Sont compris : les services cloud, comme SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui fonctionnent avec Azure RMS grâce au connecteur RMS, et les applications clientes comme Office 2016 et Office 2013. Vous obtenez des journaux d'utilisation de la clé, quelle que soit l'application effectuant des requêtes Azure RMS.

Il existe une exception : Actuellement, la solution **Azure RMS BYOK**n'est pas compatible avec Exchange Online. Si vous souhaitez utiliser Exchange Online, nous vous recommandons de déployer Azure RMS maintenant en mode de gestion de clés par défaut dans lequel Microsoft génère et gère votre clé. Vous avez la possibilité de passer à la solution BYOK ultérieurement, par exemple, quand Exchange Online prend en charge Azure RMS BYOK. Toutefois, si vous ne pouvez pas attendre, une autre option consiste à déployer Azure RMS avec la solution BYOK et des fonctionnalités RMS réduites pour Exchange Online (les pièces jointes et messages électroniques non protégés restent entièrement fonctionnels) :

-   Il n'est pas possible d'afficher les pièces jointes ou messages électroniques protégés dans Outlook Web Access.

-   Il n'est pas possible d'afficher les messages électroniques protégés sur des appareils mobiles utilisant l'IRM Exchange ActiveSync.

-   Le déchiffrement du transport (par exemple, pour détecter des logiciels malveillants) et le déchiffrement du journal étant impossibles, les messages électroniques et pièces jointes protégés sont ignorés.

-   Les règles de protection du transport et la protection contre la perte de données (DLP) qui appliquent les stratégies IRM ne sont pas disponibles. La protection RMS ne peut donc pas être appliquée à l'aide de ces méthodes.

-   La recherche basée sur les serveurs de messages électroniques protégés n’est pas disponible. Les messages électroniques protégés sont donc ignorés.

Lorsque vous utilisez la solution BYOK Azure RMS avec des fonctionnalités RMS réduites pour Exchange Online, RMS fonctionne avec les clients de messagerie dans Outlook sur Mac et Windows et sur d'autres clients de messagerie qui n'utilisent pas Exchange ActiveSync IRM.

Si vous effectuez une migration vers Azure RMS depuis AD RMS, vous avez peut-être importé votre clé comme domaine de publication approuvé (TPD) dans Exchange Online (également appelé BYOK dans la terminologie d’Exchange, qui est distincte du BYOK d’Azure Key Vault). Dans ce scénario, vous devez supprimer le domaine de publication approuvé d'Exchange Online afin d'éviter les modèles et stratégies en conflit. Pour plus d’informations, consultez [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) dans la bibliothèque d’applets de commande Exchange Online.

Parfois, l'exception BYOK d'Azure RMS pour Exchange Online n'est pas un problème dans la pratique. Par exemple, les organisations qui souhaitent utiliser la solution BYOK et la journalisation exécutent leurs applications de données (Exchange, SharePoint, Office) en local et utilisent Azure RMS pour les fonctionnalités qui ne sont pas facilement disponibles avec AD RMS en local (par exemple, collaboration avec d'autres sociétés et accès à partir de clients mobiles). La solution BYOK et la journalisation fonctionnent bien dans ce scénario et offrent aux organisations un contrôle total sur leur abonnement Azure RMS.

## Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé de client Azure Rights Management.




<!--HONumber=Sep16_HO4-->


