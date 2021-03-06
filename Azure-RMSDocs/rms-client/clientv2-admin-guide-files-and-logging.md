---
title: Azure Information Protection les fichiers du client d’étiquetage unifié et la journalisation de l’utilisation
description: Informations sur les fichiers du client et la journalisation de l’utilisation pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 36dae0d339059020b9e95d2671bc64f7a1f77c1f
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560320"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guide de l’administrateur : Azure Information Protection fichiers du client d’étiquetage unifié et journalisation de l’utilisation du client

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Concerne :** [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-files-and-logging.md). *

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

- [Personnalisations](clientv2-admin-guide-customizations.md)

- [Types de fichiers pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

