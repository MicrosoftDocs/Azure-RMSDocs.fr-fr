---
title: mip MetadataAction, classe
description: Informations de référence pour la classe mip MetadataAction
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f7480775a0226c7161c9ad770184e54427a5084
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444617"
---
# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
 public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne** : Const std::vector<std::pair<std::string, std::string>>& La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="actiontype"></a>ActionType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne** : ActionType - le type d’action dérivée vers lequel cette classe de base peut être castée.