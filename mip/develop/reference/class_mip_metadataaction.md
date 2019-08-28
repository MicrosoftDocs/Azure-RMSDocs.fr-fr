---
title: mip::MetadataAction, classe
description: 'Documente la classe MIP:: metadataaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 9175fc9278f012b3f3247cab6a09650c55713ac3
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055916"
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