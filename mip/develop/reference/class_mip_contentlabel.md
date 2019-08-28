---
title: mip::ContentLabel, classe
description: 'Documente la classe MIP:: contentlabel du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8c3849f2614e8209c355dac3a49d44d64a622b15
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055186"
---
# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetCreationTime () const  |  Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std:: Vector\<std::p air\<std:: String, std:: String\>\>& GetExtendedProperties () const  |  Obtient les propriétés étendues.
public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std:: shared_ptr\<label\> getLabel () const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime-function"></a>GetCreationTime fonction)
Obtenir l’heure de création de l’étiquette.

  
**Retourne**: Heure de création.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod fonction)
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne**: Méthode d’assignation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi**: [MIP:: assignation](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties fonction)
Obtient les propriétés étendues.

  
**Retourne**: Propriétés étendues.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel fonction)
Indique si la protection a été appliquée par l’étiquette ou non.

  
**Retourne**: True s’il existe une protection de modèle et qu’elle se trouvait sur cette étiquette, sinon false.
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’objet d’étiquette réel appliqué au contenu.

  
**Retourne**: Objet d’étiquette appliqué au contenu. 
  
**Voir aussi** : [mip::Label](class_mip_label.md)