---
# required metadata

title: Tarifs et restrictions BYOK | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Tarifs et restrictions BYOK

*S’applique à : Azure Rights Management, Office 365*


Toute organisation possédant un abonnement Azure géré par informatique peut utiliser la solution BYOK et consigner son utilisation sans frais supplémentaires. Notez que les organisations utilisant RMS for individuals ne peuvent utiliser ni la solution BYOK, ni la journalisation, car elles ne disposent d'aucun administrateur locataire pour configurer ces fonctions.


> [!NOTE]
> Pour plus d’informations sur RMS for individuals, consultez [RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK ne prend pas en charge Exchange Online](../media/RMS_BYOK_noExchange.png)

La solution BYOK et la journalisation fonctionnent de façon transparente, chaque application s'intégrant avec Azure RMS, notamment les services cloud tels que SharePoint Online, les serveurs locaux exécutant Exchange et SharePoint qui fonctionnent avec Azure RMS grâce au connecteur RMS, et les applications clientes telles qu’Office 2013. Vous obtenez des journaux d'utilisation de la clé, quelle que soit l'application effectuant des requêtes Azure RMS.

Il existe une exception : Actuellement, la solution **Azure RMS BYOK**n'est pas compatible avec Exchange Online.  Si vous souhaitez utiliser Exchange Online, nous vous recommandons de déployer Azure RMS maintenant en mode de gestion de clés par défaut dans lequel Microsoft génère et gère votre clé. Vous avez la possibilité de passer à la solution BYOK ultérieurement, par exemple, quand Exchange Online prend en charge Azure RMS BYOK. Toutefois, si vous ne pouvez pas attendre, une autre option consiste à déployer Azure RMS avec la solution BYOK et des fonctionnalités RMS réduites pour Exchange Online (les pièces jointes et messages électroniques non protégés restent entièrement fonctionnels) :

-   Il n'est pas possible d'afficher les pièces jointes ou messages électroniques protégés dans Outlook Web Access.

-   Il n'est pas possible d'afficher les messages électroniques protégés sur des appareils mobiles utilisant l'IRM Exchange ActiveSync.

-   Le déchiffrement du transport (par exemple, pour détecter des logiciels malveillants) et le déchiffrement du journal étant impossibles, les messages électroniques et pièces jointes protégés sont ignorés.

-   Les règles de protection du transport et la protection contre la perte de données (DLP) qui appliquent les stratégies IRM ne sont pas disponibles. La protection RMS ne peut donc pas être appliquée à l'aide de ces méthodes.

-   La recherche basée sur les serveurs de messages électroniques protégés n’est pas disponible. Les messages électroniques protégés sont donc ignorés.

Lorsque vous utilisez la solution BYOK Azure RMS avec des fonctionnalités RMS réduites pour Exchange Online, RMS fonctionne avec les clients de messagerie dans Outlook sur Mac et Windows et sur d'autres clients de messagerie qui n'utilisent pas Exchange ActiveSync IRM.

Si vous effectuez une migration vers Azure RMS à partir d'AD RMS, vous avez peut-être importé votre clé en tant que domaine de publication approuvé (TPD) dans Exchange Online (également appelée BYOK dans la terminologie d'Exchange, qui est distincte de la solution BYOK d'Azure RMS ). Dans ce scénario, vous devez supprimer le domaine de publication approuvé d'Exchange Online afin d'éviter les modèles et stratégies en conflit. Pour plus d’informations, consultez [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) dans la bibliothèque d’applets de commande Exchange Online.

Parfois, l'exception BYOK d'Azure RMS pour Exchange Online n'est pas un problème dans la pratique. Par exemple, les organisations qui souhaitent utiliser la solution BYOK et la journalisation exécutent leurs applications de données (Exchange, SharePoint, Office) en local et utilisent Azure RMS pour les fonctionnalités qui ne sont pas facilement disponibles avec AD RMS en local (par exemple, collaboration avec d'autres sociétés et accès à partir de clients mobiles). La solution BYOK et la journalisation fonctionnent bien dans ce scénario et offrent aux organisations un contrôle total sur leur abonnement Azure RMS.

## Étapes suivantes

Si vous avez décidé de gérer votre propre clé, accédez à [Implémentation de la clé de locataire Azure Rights Management](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key).

Si vous souhaitez que Microsoft gère votre clé de client (configuration par défaut), consultez la section [Étapes suivantes](plan-implement-tenant-key.md#next-steps) de l’article Planification et implémentation de votre clé de client Azure Rights Management.



<!--HONumber=Apr16_HO4-->


