---
title: Azure Information Protection les fichiers du client d’étiquetage unifié et la journalisation de l’utilisation
description: Informations sur les fichiers du client et la journalisation de l’utilisation pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1f568c3bf2a2e6cd9b94b0a7a8bd9a49b35c4958
ms.sourcegitcommit: ef57eb7896cf0aeb592f5e8ab37452f1e95aa20d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542356"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>Guide de l’administrateur : Azure Information Protection fichiers du client d’étiquetage unifié et journalisation de l’utilisation du client

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Après avoir installé le client d’étiquetage unifié Azure Information Protection, vous devrez peut-être savoir où se trouvent les fichiers et surveiller la façon dont le client est utilisé.

## <a name="file-locations-for-the-azure-information-protection-unified-labeling-client"></a>Emplacements des fichiers pour le client d’étiquetage unifié Azure Information Protection

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%LocalAppData%\Microsoft\MSIP\Logs**


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié tous les fichiers journaux associés à l’Azure Information Protection client d’étiquetage unifié, consultez les éléments suivants pour plus d’informations sur la prise en charge de ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

