---
title: mip::ContentLabel, classe
description: Décrit la classe mip::contentlabel de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d608ca9229a9b8c4ef0bec3c0d2fe37b51b71f61
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651732"
---
# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetCreationTime() const  |  Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetExtendedProperties() const  |  Obtient les propriétés étendues.
public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std::shared_ptr\<Label\> GetLabel() const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime-function"></a>GetCreationTime (fonction)
Obtenir l’heure de création de l’étiquette.

  
**Retourne**: Heure de création sous forme de chaîne GMT.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (fonction)
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne**: Méthode d’assignation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi**: [mip::AssignmentMethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties (fonction)
Obtient les propriétés étendues.

  
**Retourne**: Propriétés étendues.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel (fonction)
Indique si la protection a été appliquée par l’étiquette ou non.

  
**Retourne**: True si la protection du modèle et il a été par cette étiquette, sinon false.
  
### <a name="getlabel-function"></a>GetLabel (fonction)
Obtient l’objet d’étiquette réel appliqué au contenu.

  
**Retourne**: L’objet d’étiquette appliqué au contenu. 
  
**Voir aussi** : [mip::Label](class_mip_label.md)