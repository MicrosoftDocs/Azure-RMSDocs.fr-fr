---
title: Client d’étiquetage unifié Azure Information Protection - Informations sur les versions
description: Consultez les informations de version pour le client d’étiquetage unifié Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 699e2807c700b90b98bbc855dd8792aa607696f3
ms.sourcegitcommit: 8ba63c0f4cd7d2ad7614af4ea9cfe8aec7fac4c0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56956251"
---
# <a name="azure-information-protection-unified-labeling-client-version-release-information"></a>Client d’étiquetage unifié Azure Information Protection : Informations sur la version

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

> [!NOTE]
> Ce client est en préversion et susceptible d’être modifié. Il utilise le magasin d’étiquetage unifié et télécharge une stratégie avec des étiquettes à partir du Centre de sécurité et conformité Office 365. [Plus d’informations](/Office365/SecurityCompliance/sensitivity-labels)

Vous pouvez télécharger la dernière préversion du client d’étiquetage unifié Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

### <a name="release-information"></a>Informations de version

Utilisez les informations suivantes pour voir les éléments pris en charge pour la dernière préversion du client d’étiquetage unifié Azure Information Protection.

Ce client installe un module complémentaire Office pour les ordinateurs Windows, une extension pour l’Explorateur de fichiers et un module PowerShell. Ce client a les mêmes [prérequis](../requirements.md) que le client Azure Information Protection qui télécharge une stratégie à partir d’Azure.

Pour comparer les fonctionnalités avec le client Azure Information Protection, voir [Comparaison des fonctionnalités des clients](use-client.md#feature-comparisons-for-the-clients).

## <a name="current-preview-version"></a>Préversion actuelle

**Date de publication** : 25/02/2019

Cette préversion du client d’étiquetage unifié Azure Information Protection pour Windows prend en charge les fonctionnalités suivantes : 

- Mise à niveau à partir du client Azure Information Protection.

- Étiquetage manuel, automatique et recommandé : utilisez **Étiquetage automatique** à partir du Centre de sécurité et conformité Office 365 pour configurer l’étiquetage automatique et recommandé. Pour plus d’informations, voir [Appliquer automatiquement une étiquette sensibilité au contenu](/Office365/SecurityCompliance/apply_sensitivity_label_automatically).

- Dans l’Explorateur de fichiers, actions déclenchées par clic droit pour classifier et protéger des fichiers, supprimer la protection et appliquer des autorisations personnalisées.

- Visionneuse pour les fichiers texte et image protégés, les fichiers PDF protégés ainsi que les fichiers faisant l’objet d’une protection générique.

- Commandes PowerShell pour effectuer les actions suivantes :
    - [Définir ou supprimer une étiquette dans un document](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [Étiqueter un document après en avoir examiné le contenu](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [Lire les informations d’étiquette appliquées à un document](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [S’authentifier pour prendre en charge les sessions PowerShell sans assistance](/powershell/module/azureinformationprotection/set-aipauthentication)

- Prise en charge de la création centralisée de rapports à l’aide de [l’analytique Azure Information Protection](../reports-aip.md).

- Paramètres d’étiquette et de stratégie suivants :
    - Marquage visuel (en-têtes, pieds de page, filigranes)
    - Étiquetage par défaut
    - Étiquettes qui appliquent Ne pas transférer et s’affichent uniquement dans Outlook
    - Invites de justification si les utilisateurs baissent le niveau de classification ou suppriment une étiquette
    - Couleurs des étiquettes

- Actualisation de la stratégie à partir du Centre de sécurité et de conformité :
    - à chaque démarrage d’une application Office et toutes les 4 heures ;
    - lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier ;
    - lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection.

- Boîte de dialogue Aide et commentaires, qui inclut des paramètres de réinitialisation et des journaux d’exportation.

### <a name="features-that-do-not-work-in-this-preview-version-or-are-not-available"></a>Fonctionnalités qui ne fonctionnent pas dans cette préversion ou qui ne sont pas disponibles

Inclut :

- Le scanneur permettant de détecter, étiqueter et protéger les fichiers dans les magasins de données locaux n’est pas disponible.

- Les étiquettes migrées à partir du portail Azure et configurées pour la protection HYOK s’affichent dans le client lorsqu’elles sont publiées, mais n’appliquent pas la protection.

- L’ensemble complet des cmdlets du module AzureInformationProtection n’est pas disponible, notamment les cmdlets qui se connectent directement à un service de protection. Exemple : Unprotect-RMSFile pour ôter la protection des fichiers en bloc.

Pour plus d’informations, consultez les [tableaux de comparaison](use-client.md#feature-comparisons-for-the-clients).

## <a name="instructions"></a>Instructions

1. Installez le client à l'aide des instructions suivantes : [Guide de l’utilisateur : Télécharger et installer le client Azure Information Protection (préversion)](install-unifiedlabelingclient-app.md) 

2. Utilisez le client comme vous le feriez pour le client Azure Information Protection, avec les exceptions suivantes pour les applications Office :
    - Le bouton du ruban Office est nommé **Critère de diffusion** et non **Protéger**.
    - Par défaut, les administrateurs ne peuvent pas afficher la barre Information Protection, contrairement aux utilisateurs qui peuvent l’afficher en sélectionnant **Afficher la barre** à partir du bouton **Critère de diffusion**. 
    - Les autorisations personnalisées ne sont pas disponibles.
    - L’action Suivre et révoquer n’est pas disponible.
    
    Pour les instructions destinées à l’utilisateur :
    
    - [Classifier un fichier ou un e-mail](client-classify.md) 
    
    - [Classifier et protéger un fichier ou un e-mail](client-classify-protect.md)

3. Partagez votre expérience : 
    
    - Pour fournir des commentaires ou poser des questions sur ce client en préversion, utilisez le [site Yammer pour Azure Information Protection](https://www.yammer.com/AskIPTeam).
