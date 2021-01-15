---
title: ApplicationActionState de classe
description: 'Documente la classe applicationactionstate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ef62674d4586b967a822ccfb25612a491d157bf4
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212278"
---
# <a name="class-applicationactionstate"></a>ApplicationActionState de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public LabelState GetNewLabelState () const  |  Obtient le nouvel état de l’étiquette.
public std :: shared_ptr \<Label\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
STD public ::p air \<bool, std::string\> IsDowngradeJustified () const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std :: Vector \<std::pair\<std::string, std::string\> \> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
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
  
**Voir aussi** : mip::AssignmentMethod
  
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