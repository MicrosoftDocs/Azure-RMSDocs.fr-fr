---
title: "Prise en charge des serveurs locaux pour la protection des données | Azure Information Protection"
description: "Identifiez les produits de serveurs locaux qui peuvent utiliser le service Azure Rights Management d’Azure Information Protection, à l’aide du connecteur Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: e4bf159cea6298e5a5577a2fa4de3dd3beeb47d9


---


# <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>Serveurs locaux prenant en charge la protection des données Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Les produits de serveurs locaux suivants sont pris en charge avec Azure Information Protection quand vous utilisez le connecteur Azure Rights Management. Ce connecteur fait office d’interface de communication (relais) entre les serveurs locaux et le service Azure Rights Management utilisé par Azure Information Protection pour protéger les e-mails et les documents Office. 

Pour utiliser ce connecteur, vous devez configurer la synchronisation des annuaires entre vos forêts Active Directory et Azure Active Directory.

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

    -   Windows Server 2012

    > [!NOTE]
    > Les serveurs de fichiers qui exécutent Windows Server 2008 R2 n’ont pas d’action de tâche de gestion de fichiers intégrée pour appliquer la protection de Rights Management. Par conséquent, vous ne pouvez pas utiliser le connecteur Rights Management pour ce scénario. En revanche, vous pouvez utiliser l’infrastructure de classification des fichiers et Azure RMS sur ces systèmes d’exploitation si vous configurez une tâche de gestion de fichiers personnalisée de sorte qu’elle exécute un exécutable ou un script capable de protéger les fichiers à l’aide d’Azure RMS. Par exemple, un script Windows PowerShell qui utilise les [applets de commande de protection RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > Vous pouvez également utiliser ces applets de commande avec des serveurs exécutant des versions ultérieures de Windows Server, l’avantage étant que ces applets de commande peuvent protéger tous les types de fichiers. Le connecteur RMS protège uniquement les fichiers Office. Pour obtenir des instructions, consultez [Protection RMS avec l’Infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](../rms-client/configure-fci.md).

Le connecteur Rights Management est pris en charge sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.

Pour plus d’informations sur la configuration du connecteur Rights Management pour ces serveurs locaux, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Conditions requises pour Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Nov16_HO2-->


