---
title: mip::ExecutionState, classe
description: 'Documente la classe MIP:: ExecutionState du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 02e72dc55c12b3800ff76356da1fb7c3adf08fdd
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884356"
---
# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<label\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier: [path\filename] exemple pour un e-mail: [Subject: sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std:: Vector\<std::p air\<std:: String, std:: String\> \> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public virtuel std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: Vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabel-function"></a>GetNewLabel fonction)
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne**: ID d’étiquette de sensibilité à appliquer au contenu si Exists ou vide pour supprimer l’étiquette.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier fonction)
Obtient la description du contenu qui décrit le document. exemple pour un fichier: [path\filename] exemple pour un e-mail: [Subject: sender].

  
**Retourne**: Description du contenu à appliquer au contenu.
Cette valeur est utilisée par l’audit comme une description explicite du contenu
  
### <a name="getdatastate-function"></a>GetDataState fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne**: État des données de contenu
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified fonction)
L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.

  
**Retourne**: True si la rétrogradation est justifiedalong avec la justification messageelse false 
  
**Voir aussi** : [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod fonction)
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne**: La méthode d’affectation STANDARD, PRIVILEGEd, AUTO. 
  
**Voir aussi**: [MIP:: assignation](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties fonction)
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne**: Propriétés étendues appliquées au contenu.
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata fonction)
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne**: Métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
Obtenir le descripteur de protection.

  
**Retourne**: Descripteur de protection
  
### <a name="getcontentformat-function"></a>GetContentFormat fonction)
Obtient le format du contenu.

  
**Retourne**: PAR DÉFAUT, E-MAIL 
  
**Voir aussi**: [MIP:: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions fonction)
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne**: Enum masqué décrivant tous les types d’action pris en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults fonction)
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationIds**: liste d’ID de classification. 



  
**Retourne**: Liste des résultats de la classification. retourne nullptr si aucun cycle de classification n’est exécuté.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata fonction)
Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.

  
**Retourne**: Liste des métadonnées d’audit spécifiques à l’application clé inscrite: expéditeur des paires de valeurs: ID d’e-mail pour les destinataires de l’expéditeur: Représente un tableau JSON de destinataires pour un LastModifiedBy de messagerie: ID de messagerie de l’utilisateur qui a modifié le contenu LastModifiedDate &: Date de dernière modification du contenu