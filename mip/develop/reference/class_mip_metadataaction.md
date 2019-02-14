---
title: mip::MetadataAction, classe
description: Décrit la classe mip::metadataaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 190bccc23ecb5c03faa0ab6748caf8fc206e265f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256989"
---
# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetMetadataToRemove() const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove function
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne**: Un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd (fonction)
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne**: Const std::vector < std::pair < std::string, std::string >> & la suppression de métadonnées doivent être effectuées avant d’ajouter des métadonnées.
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.
