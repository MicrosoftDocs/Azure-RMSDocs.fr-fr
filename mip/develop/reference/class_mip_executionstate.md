---
title: mip::ExecutionState, classe
description: Décrit la classe mip::executionstate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d4e06495df39565971b29427d05a56ebe852c3df
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332818"
---
# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId() const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public ActionSource GetNewLabelActionSource() const  |  Obtient la source pour une nouvelle action d’étiquette.
public std::string GetContentIdentifier() const  |  Obtient l’identificateur de contenu qui décrit le document. exemple d’un fichier : exemple [chemin] pour un message électronique : [expéditeur : objet].
public ContentState GetContentState() const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public std::vector\<std::pair\<std::string, std::string\>\> GetNewLabelExtendedProperties() const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public virtual std::map\<std::string, std::shared_ptr\<ClassificationResult\>\> GetClassificationResults(const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourner un mappage des paires clé-valeur l’application d’audit spécifique.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabelid-function"></a>GetNewLabelId function
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne**: ID d’étiquette de sensibilité à appliquer au contenu si a été défini vide pour supprimer l’étiquette.
  
### <a name="getnewlabelactionsource-function"></a>GetNewLabelActionSource function
Obtient la source pour une nouvelle action d’étiquette.

  
**Retourne**: Source de l’action.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier (fonction)
Obtient l’identificateur de contenu qui décrit le document. exemple d’un fichier : exemple [chemin] pour un message électronique : [expéditeur : objet].

  
**Retourne**: Identificateur de contenu à appliquer au contenu.
Cette valeur est utilisée par l’audit comme une description explicite du contenu
  
### <a name="getcontentstate-function"></a>GetContentState (fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne**: État des données du contenu
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified (fonction)
L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.

  
**Retourne**: True si la rétrogradation est justifiedalong avec la valeur false messageelse de justification 
  
**Voir aussi** : [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod function
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne**: La méthode d’assignation STANDARD, PRIVILEGED, AUTO. 
  
**Voir aussi**: [mip::AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties (fonction)
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne**: Les propriétés étendues appliquées au contenu.
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata function
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne**: Les métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor (fonction)
Obtenir le descripteur de protection.

  
**Retourne**: Le descripteur de Protection
  
### <a name="getcontentformat-function"></a>GetContentFormat (fonction)
Obtient le format du contenu.

  
**Retourne**: PAR DÉFAUT, LE COURRIER ÉLECTRONIQUE 
  
**Voir aussi**: [mip::ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions (fonction)
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne**: Un enum masqué qui décrit tous les types d’action prise en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults function
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationId** : liste des ID de classification. 



  
**Retourne**: Liste des résultats de la classification.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata function
Retourner un mappage des paires clé-valeur l’application d’audit spécifique.

  
**Retourne**: Une liste d’expéditeur les paires clé-valeur inscrit de métadonnées d’audit spécifique application : Id d’e-mail pour l’expéditeur, destinataires : Représente un tableau JSON de destinataires pour un message électronique LastModifiedBy : Id d’e-mail pour l’utilisateur qui a modifié dernièrement le LastModifiedDate & gt ; contenu : Date de que dernière modification du contenu
