---
title: 'MIP:: ApplicationActionState, classe'
description: 'Documente la classe MIP:: applicationactionstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a75ade6fcbb87e24b778b4368eb65080e767c130
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055516"
---
# <a name="class-mipapplicationactionstate"></a>MIP:: ApplicationActionState, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Obtient le nouvel état de l’étiquette.
public std:: shared_ptr\<label\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std:: Vector\<std::p air\<std:: String, std:: String\> \> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public bool IsRecommendationEnabled () const  |  Obtient une valeur booléenne qui indique que l’action recommander retourne. par défaut, doit avoir la valeur true, sauf si l’utilisateur spécifie Else.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState fonction)
Obtient le nouvel état de l’étiquette.

  
**Retourne**: Nouvel état de l’étiquette. 
  
**Voir aussi**: MIP:: LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel fonction)
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne**: ID d’étiquette de sensibilité à appliquer au contenu si Exists ou vide pour supprimer l’étiquette.
  
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
  
### <a name="getsupportedactions-function"></a>GetSupportedActions fonction)
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne**: Enum masqué décrivant tous les types d’action pris en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled fonction)
Obtient une valeur booléenne qui indique que l’action recommander retourne. par défaut, doit avoir la valeur true, sauf si l’utilisateur spécifie Else.

  
**Retourne**: Valeur booléenne qui indique que l’action recommander retourne.
ActionType:: RecommendLabel doit être activé pour que ce champ ait un effet.