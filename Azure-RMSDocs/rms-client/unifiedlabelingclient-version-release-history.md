---
title: Client d’étiquetage unifié Azure Information Protection - Informations sur les versions
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: a1544e0fa3c6d09328d1801a75ffbccd496e3482
ms.sourcegitcommit: b275c1f82bf9176fe3fb36016c6f8692b8418295
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951837"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Client d’étiquetage unifié Azure Information Protection : informations sur les versions

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

> [!NOTE]
> Ce client est en préversion et susceptible d’être modifié. Il utilise le magasin d’étiquetage unifié et télécharge une stratégie avec des étiquettes à partir du Centre de sécurité et conformité Office 365. [Plus d’informations](/Office365/SecurityCompliance/sensitivity-labels)

Vous pouvez télécharger la dernière préversion du client d’étiquetage unifié Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour voir les éléments pris en charge pour la dernière préversion du client d’étiquetage unifié Azure Information Protection. 

Ce client est installé comme un module complémentaire Office pour les ordinateurs Windows et a les mêmes [prérequis](../requirements.md) que le client Azure Information Protection qui télécharge une stratégie à partir d’Azure.

## <a name="current-preview-version"></a>Préversion actuelle

**Date de publication** : 16/10/2018

Cette préversion du client d’étiquetage unifié Azure Information Protection pour Windows prend en charge les fonctionnalités suivantes : 

- Mise à niveau à partir du client Azure Information Protection

- Étiquetage manuel qui applique la classification et la protection pour Word, Excel, PowerPoint et Outlook.

- Marquage visuel (en-têtes, pieds de page, filigranes)

- Étiquetage par défaut 

- Étiquettes qui appliquent Ne pas transférer

- Demandes de justification si les utilisateurs abaissent le niveau de confidentialité

- Boîte de dialogue Aide et commentaires, qui inclut la réinitialisation des paramètres et l’exportation des journaux

- Actualisation de la stratégie à partir du Centre de sécurité et de conformité toutes les 4 heures, par l’application Office.

Les fonctionnalités suivantes ne fonctionnent pas dans cette préversion :

- Classification automatique et recommandée

- Autorisations personnalisées

- Visionneuse pour les fichiers texte et image protégés, les fichiers PDF protégés et les fichiers faisant l’objet d’une protection générique

- Explorateur de fichiers, actions accessibles par un clic droit pour classifier et protéger des fichiers

- Commandes PowerShell pour classifier et protéger des fichiers à partir de la ligne de commande

- Scanneur pour détecter, étiqueter et protéger des fichiers dans les banques de données locales

- Prise en charge des langues autres que l’anglais

## <a name="instructions"></a>Instructions

1. Installez le client en respectant les instructions suivantes : [Guide de l’utilisateur : Télécharger et installer le client Azure Information Protection (préversion)](install-unifiedlabelingclient-app.md) 

2. Utilisez le client dans les applications Office comme vous le feriez pour le client Azure Information Protection, à ceci près que le bouton du ruban Office est nommé **Sensibilité** plutôt que **Protéger** :
    
    - [Classifier un fichier ou un e-mail](client-classify.md) 
    
    - [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md)

3. Partagez votre expérience : 
    
    - Pour fournir des commentaires ou poser des questions sur ce client en préversion, utilisez le [site Yammer pour Azure Information Protection](https://www.yammer.com/AskIPTeam).
    
    - Pour signaler des problèmes avec ce client en préversion, utilisez l’option **Aide et commentaires** du bouton **Sensibilité** sur le ruban. À partir de la boîte de dialogue, exportez vos journaux et joignez ces fichiers journaux à l’e-mail qui est créé avec l’option **Signaler un problème**. 

