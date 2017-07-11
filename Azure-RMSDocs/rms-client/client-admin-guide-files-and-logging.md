---
title: "Fichiers du client Azure Information Protection et journalisation de l’utilisation"
description: "Informations sur les fichiers du client et la journalisation de l’utilisation du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: bf695772d545daca602903e156903da2aadaae7a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="azure-information-protection-client-files-and-client-usage-logging" class="xliff"></a>

# Fichiers du client Azure Information Protection et journalisation de l’utilisation du client

>*S’applique à : Services Active Directory Rights Management, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

Après avoir installé le client Azure Information Protection, vous aurez peut-être besoin de connaître l’emplacement des fichiers et de surveiller l’utilisation du client.

<a id="file-locations-for-the-azure-information-protection-client" class="xliff"></a>

## Emplacement des fichiers du client Azure Information Protection

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichier de stratégie actuellement installé :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**

<a id="usage-logging-for-the-azure-information-protection-client" class="xliff"></a>

## Journalisation de l’utilisation du client Azure Information Protection

Le client enregistre l’activité de l’utilisateur dans le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Les événements incluent les informations suivantes :

- Date, version du client, ID de stratégie

- Nom d’utilisateur, nom d’ordinateur connectés

- Nom et emplacement de fichier

- Action :

    - Définir l’étiquette : ID d’informations 101
    
    - Définir l’étiquette (inférieure) : ID d’informations 102
    
    - Définir l’étiquette (supérieure) : ID d’informations 103
    
    - Supprimer l’étiquette : ID d’informations 104
   
    - Astuce recommandée : ID d’informations 105
    
    - Appliquer la protection personnalisée : ID d’informations 201
    
    - Supprimer la protection personnalisée : ID d’informations 202
    
    - Connexion (opérationnelle) : ID d’informations 902
    
    - Télécharger la stratégie (opérationnelle) : ID d’informations 901
    
- Source de l’action :
    
    - Manuel 
    
    - Recommandé
    
    - Automatique  
    
    - Système (pour la stratégie de connexion et de téléchargement)
    
- Étiquette avant et après l’action 
    
- Protection avant et après l’action
    
- Justification de l’utilisateur (le cas échéant)
    

Pour des informations sur la journalisation de l’utilisation pour le service Azure Rights Management, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](../deploy-use/log-analyze-usage.md)



<a id="next-steps" class="xliff"></a>

## Étapes suivantes
Maintenant que vous avez identifié tous les fichiers journaux associés au client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
