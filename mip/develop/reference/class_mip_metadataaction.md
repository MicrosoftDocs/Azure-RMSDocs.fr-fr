---
title: mip::MetadataAction, classe
description: 'Documente la classe MIP:: metadataaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 26a189d714001f4145ce328c163a052313923136
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885415"
---
# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Une [Action](class_mip_action.md) qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std:: Vector\<std:: String\>& GetMetadataToRemove () const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove fonction)
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne**: Vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd fonction)
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne**: Const std:: Vector < std::p air < std:: String, std:: String > > & la suppression des métadonnées doit être effectuée avant l’ajout de métadonnées.