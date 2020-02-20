---
title: 'MIP :: ApplicationActionState, classe'
description: 'Documente la classe MIP :: applicationactionstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 70128f67f758145be2b03954d3385a8428d63fe9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490640"
---
# <a name="class-mipapplicationactionstate"></a>MIP :: ApplicationActionState, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Obtient le nouvel état de l’étiquette.
public std :: shared_ptr\<étiquette\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
STD public ::p air\<bool, std :: String\> IsDowngradeJustified () const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std :: Vector\<std ::p air\<std :: String, std :: String\>\> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public bool IsRecommendationEnabled () const  |  Obtient une valeur booléenne qui indique que l’action recommander retourne. par défaut, doit avoir la valeur true, sauf si l’utilisateur spécifie Else.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabelstate-function"></a>GetNewLabelState fonction)
Obtient le nouvel état de l’étiquette.

  
**Retourne**: nouvel état de l’étiquette. 
  
**Voir aussi**: MIP :: LabelState
  
### <a name="getnewlabel-function"></a>GetNewLabel fonction)
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne** : ID de l’étiquette de sensibilité à appliquer au contenu s’il existe ; sinon, valeur vide pour supprimer l’étiquette.
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified fonction)
L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.

  
**Retourne** : True si le passage à une version antérieure est justifié avec le message de justification ; sinon, False 
  
**Voir aussi**: MIP :: JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod fonction)
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne** : la méthode d’affectation STANDARD, PRIVILEGED, AUTO. 
  
**Voir aussi**: [MIP :: assignation](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties fonction)
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne** : propriétés étendues appliquées au contenu.
  
### <a name="getsupportedactions-function"></a>GetSupportedActions fonction)
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne** : énumération masquée qui décrit tous les types d’action pris en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="isrecommendationenabled-function"></a>IsRecommendationEnabled fonction)
Obtient une valeur booléenne qui indique que l’action recommander retourne. par défaut, doit avoir la valeur true, sauf si l’utilisateur spécifie Else.

  
**Retourne**: une valeur booléenne qui indique que l’action recommandée retourne.
ActionType :: RecommendLabel doit être activé pour que ce champ ait un effet.