---
title: "Conditions requises pour Azure RMS #58; serveurs locaux qui prennent en charge Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ed50d87138c428fadfd22cd5b3ef3c7f7e421848
ms.openlocfilehash: 7e718d8178dd7c4b18ea7a19eb3165ee06dc4b36


---


# Conditions requises pour Azure RMS : serveurs locaux qui prennent en charge Azure RMS

*S’applique à : Azure Rights Management, Office 365*

Les produits de serveurs locaux suivants sont acceptés avec le connecteur Azure RMS, qui agit en tant qu’interface de communication (relais) entre les serveurs locaux et Azure RMS. De plus, cette configuration implique de configurer la synchronisation des annuaires entre vos forêts Active Directory et Azure Active Directory.

-   **Exchange Server** :

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server** :

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Serveurs de fichiers qui exécutent Windows Server et utilisent l’infrastructure de classification des fichiers (ICF)** :

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Les serveurs de fichiers qui exécutent Windows Server 2008 R2 n’ont pas d’action de tâche de gestion de fichiers intégrée pour appliquer une protection RMS. Par conséquent, vous ne pouvez pas utiliser le connecteur RMS pour ce scénario. En revanche, vous pouvez utiliser l’infrastructure de classification des fichiers et Azure RMS sur ces systèmes d’exploitation si vous configurez une tâche de gestion de fichiers personnalisée de sorte qu’elle exécute un exécutable ou un script capable de protéger les fichiers à l’aide d’Azure RMS. Par exemple, un script Windows PowerShell qui utilise les [applets de commande de protection RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Vous pouvez également utiliser ces applets de commande avec des serveurs exécutant des versions ultérieures de Windows Server, l’avantage étant que ces applets de commande peuvent protéger tous les types de fichiers. Le connecteur RMS protège uniquement les fichiers Office. Pour obtenir des instructions, consultez [Protection RMS avec l’Infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](../rms-client/configure-fci.md).

Le connecteur RMS est pris en charge sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.

Pour plus d’informations sur la configuration du connecteur RMS pour ces serveurs locaux, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Conditions requises pour Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Jun16_HO4-->


