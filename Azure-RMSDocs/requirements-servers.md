---
title: Prise en charge des serveurs pour la protection des données Azure RMS - AIP
description: Identifiez les produits de serveurs locaux qui peuvent utiliser le service Azure Rights Management d’Azure Information Protection, à l’aide du connecteur Rights Management.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f19ce90a0ac95ae14a8795f1f8c181fb4f3acd49
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136351"
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Serveurs locaux prenant en charge la protection des données Azure Rights Management

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les produits de serveurs locaux suivants sont pris en charge avec Azure Information Protection quand vous utilisez le connecteur Azure Rights Management. Ce connecteur fait office d’interface de communication (relais) entre les serveurs locaux et le service Azure Rights Management utilisé par Azure Information Protection pour protéger les e-mails et les documents Office. 

Pour utiliser ce connecteur, vous devez configurer la synchronisation des annuaires entre vos forêts Active Directory et Azure Active Directory.

-   **Exchange Server** :

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server** :

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **Serveurs de fichiers exécutant Windows Server et utilisant l'infrastructure de classification des fichiers** :

    -   Windows Server 2016

    -   Windows Server 2012 R2

    -   Windows Server 2012


    > 
    > Vous pouvez également utiliser ces applets de commande avec des serveurs exécutant des versions ultérieures de Windows Server, l’avantage étant que ces applets de commande peuvent protéger tous les types de fichiers. Le connecteur RMS protège uniquement les fichiers Office. Pour obtenir des instructions, consultez [Protection RMS avec l’Infrastructure de classification des fichiers &#40;ICF&#41; de Windows Server](./rms-client/configure-fci.md).

Le connecteur Rights Management est pris en charge sur Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012.

Pour plus d’informations sur la configuration du connecteur Rights Management pour ces serveurs locaux, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

## <a name="next-steps"></a>Étapes suivantes
Pour vérifier les autres conditions requises, consultez [Configuration requise pour Azure Information Protection](requirements.md).
