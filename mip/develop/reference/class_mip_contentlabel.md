---
title: mip ContentLabel, classe
description: Informations de référence pour la classe mip ContentLabel
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: c105f620ed2cd3d6f1427f2543784ea66ce2c4d7
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446020"
---
# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  Obtenir l’heure de création de l’étiquette.
 public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std::vector<std::pair<std::string, std::string>>& GetExtendedProperties() const  |  Obtient les propriétés étendues.
 public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std::shared_ptr<Label> GetLabel() const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime"></a>GetCreationTime
Obtenir l’heure de création de l’étiquette.

  
**Retourne** : heure de création sous forme de chaîne GMT.
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne** : Méthode d’affectation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
### <a name="getextendedproperties"></a>GetExtendedProperties
Obtient les propriétés étendues.

  
**Retourne** : propriétés étendues.
  
### <a name="isprotectionappliedfromlabel"></a>IsProtectionAppliedFromLabel
Indique si la protection a été appliquée par l’étiquette ou non.

  
**Retourne** : True s’il existe une protection du modèle et qu’elle a été appliquée par cette étiquette ; sinon False.
  
### <a name="label"></a>Étiquette
Obtient l’objet d’étiquette réel appliqué au contenu.

  
**Retourne** : l’objet d’étiquette appliqué au contenu. 
  
**Voir aussi** : [mip::Label](class_mip_label.md)