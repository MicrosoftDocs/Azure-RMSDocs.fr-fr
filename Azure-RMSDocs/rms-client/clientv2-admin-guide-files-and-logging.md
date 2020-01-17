---
title: Azure Information Protection les fichiers du client d’étiquetage unifié et la journalisation de l’utilisation
description: Informations sur les fichiers du client et la journalisation de l’utilisation pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2983f346ba29bed30d1ceb2b055e4cdd1e152d4e
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117542"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guide de l’administrateur : Azure Information Protection fichiers du client d’étiquetage unifié et journalisation de l’utilisation du client

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Après avoir installé le client d’étiquetage unifié Azure Information Protection, vous devrez peut-être savoir où se trouvent les fichiers et surveiller la façon dont le client est utilisé.

## <a name="file-locations-for-the-azure-information-protection-unified-labeling-client"></a>Emplacements des fichiers pour le client d’étiquetage unifié Azure Information Protection

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichiers de stratégie actuellement installés :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**


## <a name="usage-logging-for-the-azure-information-protection-unified-labeling-client"></a>Journalisation de l’utilisation pour le client d’étiquetage unifié Azure Information Protection

Le client d’étiquetage unifié n’enregistre pas l’activité des utilisateurs dans le journal des événements Windows local. Utilisez plutôt la fonctionnalité de [création de rapports centralisée](../reports-aip.md) de Azure information protection. 


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié tous les fichiers journaux associés à l’Azure Information Protection client d’étiquetage unifié, consultez les éléments suivants pour plus d’informations sur la prise en charge de ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

