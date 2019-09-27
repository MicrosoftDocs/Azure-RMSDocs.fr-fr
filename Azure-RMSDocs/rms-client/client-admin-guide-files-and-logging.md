---
title: Fichiers du client Azure Information Protection et journalisation de l’utilisation
description: Informations sur les fichiers du client et la journalisation de l’utilisation du client Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9edd0e3bcfda2d50da70e29bc807745d263f30bb
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314240"
---
# <a name="admin-guide-azure-information-protection-client-files-and-client-usage-logging"></a>Guide de l’administrateur : Fichiers du client Azure Information Protection et journalisation de l’utilisation du client

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Après avoir installé le client Azure Information Protection, vous aurez peut-être besoin de connaître l’emplacement des fichiers et de surveiller l’utilisation du client.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Emplacement des fichiers du client Azure Information Protection

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichier de stratégie actuellement installé :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Journalisation de l’utilisation du client Azure Information Protection

Le client enregistre l’activité de l’utilisateur dans le journal des événements Windows local **Journaux des applications et des services** > **Azure Information Protection**. Les événements incluent les informations suivantes :

- Version du client, ID de stratégie

- Adresses IP de l’utilisateur connecté

- Nom et emplacement de fichier

- Action :

    - Définir l’étiquette : ID d’information 101
    
    - Définir l’étiquette (inférieure) : ID d’information 101
    
    - Définir l’étiquette (supérieure) : ID d’information 101
    
    - Supprimer l’étiquette : ID d’information 104
    
    - Info-bulle de l’étiquette recommandée : Information 105
    
    - Appliquer la protection personnalisée : ID d’information 201
    
    - Supprimer la protection personnalisée : ID d’information 202
    
    - Message d’avertissement Outlook : ID d’information 301
    
    - Message de justification Outlook : ID d’information 302
    
    - Message de blocage Outlook : ID d’information 303
    
    - Connexion (opérationnelle) : ID d’information 902
    
    - Télécharger la stratégie (opérationnelle) : ID d’information 901
    
- Source de l’action :
    
    - Manuel 
    
    - Recommandé
    
    - Automatique  
    
    - Système (pour la stratégie de connexion et de téléchargement)
    
    - Par défaut
    
- Étiquette avant et après l’action 
    
- Protection avant et après l’action
    
- Justification de l’utilisateur (le cas échéant)

- Autorisations personnalisées (le cas échéant) qui incluent les [droits d’utilisation par leur nom d’encodage](../configure-usage-rights.md#usage-rights-and-descriptions) pour les utilisateurs, groupes ou organisations spécifiés

Les événements pour les messages Outlook d’avertissement, de justification et de blocage requièrent des paramètres client avancés. Pour plus d’informations, consultez [Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié tous les fichiers journaux associés au client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

