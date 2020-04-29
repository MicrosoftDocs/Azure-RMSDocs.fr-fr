---
title: ContentLabel de classe
description: 'Documente la classe contentlabel :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e69a4a8146eb7e7251645ef83a8db0926d383166
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763401"
---
# <a name="class-contentlabel"></a>ContentLabel de classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetCreationTime () const  |  Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std :: Vector\<MetadataEntry\>& GetExtendedProperties () const  |  Obtient les propriétés étendues.
public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std :: shared_ptr\<label\> getLabel () const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getcreationtime-function"></a>GetCreationTime fonction)
Obtenir l’heure de création de l’étiquette.

  
**Retourne**: heure de création.
  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod fonction)
Obtenir la méthode d’assignation de l’étiquette.

  
**Retourne** : Méthode d’affectation STANDARD | PRIVILEGED | AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
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