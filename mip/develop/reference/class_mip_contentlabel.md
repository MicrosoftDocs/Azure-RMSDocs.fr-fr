---
title: ContentLabel de classe
description: 'Documente la classe contentlabel :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a60244b9db9b3087dde71cbdbcf63ba170cb06c3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567197"
---
# <a name="class-contentlabel"></a>ContentLabel de classe 
Abstraction d’une étiquette Microsoft Information Protection appliquée à un élément de contenu, généralement un document.
Elle contient également des propriétés pour une instance d’étiquette appliquée spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: Chrono :: time_point \<std::chrono::system_clock\> GetCreationTime () const  |  Obtenir l’heure de création de l’étiquette.
public AssignmentMethod GetAssignmentMethod() const  |  Obtenir la méthode d’assignation de l’étiquette.
public const std :: Vector \<MetadataEntry\>& GetExtendedProperties () const  |  Obtient les propriétés étendues.
public bool IsProtectionAppliedFromLabel() const  |  Indique si la protection a été appliquée par l’étiquette ou non.
public std::shared_ptr\<Label\> GetLabel() const  |  Obtient l’objet d’étiquette réel appliqué au contenu.
  
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