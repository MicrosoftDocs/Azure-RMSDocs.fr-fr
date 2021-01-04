---
title: Azure Information Protection les fichiers du client Classic et la journalisation de l’utilisation
description: Informations sur les fichiers du client Classic et la journalisation de l’utilisation pour le client Azure Information Protection Classic pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d314c7554b993f328428962a9947b725365969e0
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807380"
---
# <a name="admin-guide-azure-information-protection-classic-client-files-and-client-usage-logging"></a>Guide de l’administrateur : Azure Information Protection fichiers du client Classic et journalisation de l’utilisation du client

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Concerne** : [Client classique Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Une fois que vous avez installé le client Azure Information Protection Classic, vous devrez peut-être savoir où se trouvent les fichiers et surveiller la façon dont le client est utilisé.

## <a name="file-locations-for-the-azure-information-protection-client"></a>Emplacement des fichiers du client Azure Information Protection

Fichiers du client :    

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichier de stratégie actuellement installé :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-classic-client"></a>Journalisation de l’utilisation pour le client Azure Information Protection Classic

Le client enregistre l’activité de l’utilisateur dans le journal des événements Windows local **journaux des applications et des services**  >  **Azure information protection**. Les événements incluent les informations suivantes :

- Version du client, ID de stratégie

- Adresses IP de l’utilisateur connecté

- Nom et emplacement de fichier

- Action :

    - Définir l’étiquette : ID d’informations 101
    
    - Définir l’étiquette (inférieure) : ID d’informations 102
    
    - Définir l’étiquette (plus élevée) : ID d’informations 103
    
    - Supprimer l’étiquette : ID d’informations 104
    
    - Info-bulle de l’étiquette recommandée : information 105
    
    - Appliquer la protection personnalisée : ID d’informations 201
    
    - Supprimer la protection personnalisée : ID d’informations 202
    
    - Message Outlook Warn : information ID 301
    
    - Outlook justifier le message : ID d’informations 302
    
    - Message de blocage Outlook : ID d’informations 303
    
    - Connexion (opérationnelle) : ID d’informations 902
    
    - Télécharger la stratégie (opérationnelle) : ID d’informations 901
    
- Source de l’action :
    
    - Manuel 
    
    - Recommandé
    
    - Automatique  
    
    - Système (pour la stratégie de connexion et de téléchargement)
    
    - Default
    
- Étiquette avant et après l’action 
    
- Protection avant et après l’action
    
- Justification de l’utilisateur (le cas échéant)

- Autorisations personnalisées (le cas échéant) qui incluent les [droits d’utilisation par leur nom d’encodage](../configure-usage-rights.md#usage-rights-and-descriptions) pour les utilisateurs, groupes ou organisations spécifiés

Les événements pour les messages Outlook d’avertissement, de justification et de blocage requièrent des paramètres client avancés. Pour plus d’informations, consultez [Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié tous les fichiers journaux associés au client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Personnalisations](client-admin-guide-customizations.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichiers pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

