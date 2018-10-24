---
title: mip ExecutionState, classe
description: Informations de référence pour la classe mip ExecutionState
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 976bca60f3f494a0fbf196e6512b00bdcdd63992
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446309"
---
# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
 public ActionSource GetNewLabelActionSource() const  |  Obtient la source pour une nouvelle action d’étiquette.
 public std::string GetContentIdentifier() const  |  Obtient l’identificateur de contenu qui décrit le document. Exemple pour un fichier : [chemin], exemple pour un e-mail : [objet : expéditeur].
 public ContentState GetContentState() const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std::pair<bool, std::string> IsDowngradeJustified() const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor() const  |  Obtenir le descripteur de protection.
 public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
 public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  Retourne un mappage des résultats de la classification.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabelid"></a>GetNewLabelId
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne** : ID de l’étiquette de sensibilité à appliquer au contenu s’il existe ; sinon, valeur vide pour supprimer l’étiquette.
  
### <a name="getnewlabelactionsource"></a>GetNewLabelActionSource
Obtient la source pour une nouvelle action d’étiquette.

  
**Retourne** : source de l’action.
  
### <a name="getcontentidentifier"></a>GetContentIdentifier
Obtient l’identificateur de contenu qui décrit le document. Exemple pour un fichier : [chemin], exemple pour un e-mail : [objet : expéditeur].

  
**Retourne** : identificateur de contenu à appliquer au contenu.
Cette valeur est utilisée par l’audit comme une description explicite du contenu
  
### <a name="getcontentstate"></a>GetContentState
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne** : état des données de contenu
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.

  
**Retourne** : True si le passage à une version antérieure est justifié avec le message de justification ; sinon, False 
  
**Voir aussi** : [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne** : la méthode d’affectation STANDARD, PRIVILEGED, AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne** : propriétés étendues appliquées au contenu.
  
### <a name="getcontentmetadata"></a>GetContentMetadata
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne** : métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
Obtenir le descripteur de protection.

  
**Retourne** : descripteur de protection
  
### <a name="getcontentformat"></a>GetContentFormat
Obtient le format du contenu.

  
**Retourne** : DEFAULT, EMAIL 
  
**Voir aussi** : mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne** : énumération masquée qui décrit tous les types d’action pris en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="classificationresult"></a>ClassificationResult
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationId** : liste des ID de classification. 



  
**Retourne** : une liste des résultats de la classification.