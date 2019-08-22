---
title: mip::ContentLabel, classe
description: 'Documente la classe MIP:: contentlabel du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 27f8adba3e65647a3804256e0b429e1457003085
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884394"
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