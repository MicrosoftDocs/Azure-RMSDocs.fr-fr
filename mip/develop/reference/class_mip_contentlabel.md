---
title: mip::ContentLabel, classe
description: 'Documente la classe MIP :: contentlabel du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a29ea5be05d928f25b9a4255416d93acedcb1c0b
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74840273"
---
# <a name="class-mipcontentlabel"></a>mip::ContentLabel, classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetCreationTime () const  |  Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetExtendedProperties () const  |  Obtient les propriétés étendues.
public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std :: shared_ptr\<étiquette\> GetLabel () const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime-function"></a>GetCreationTime fonction)
Obtenir l’heure de création de l’étiquette.

  
**Retourne**: heure de création.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod fonction)
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne** : Méthode d’affectation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi**: [MIP :: assignation](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getextendedproperties-function"></a>GetExtendedProperties fonction)
Obtient les propriétés étendues.

  
**Retourne** : propriétés étendues.
  
### <a name="isprotectionappliedfromlabel-function"></a>IsProtectionAppliedFromLabel fonction)
Indique si la protection a été appliquée par l’étiquette ou non.

  
**Retourne** : True s’il existe une protection du modèle et qu’elle a été appliquée par cette étiquette ; sinon False.
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’objet d’étiquette réel appliqué au contenu.

  
**Retourne** : l’objet d’étiquette appliqué au contenu. 
  
**Voir aussi**: MIP :: label