---
title: mip::MetadataAction, classe
description: 'Documente la classe MIP :: metadataaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 405bb153527cb3fde346203d3b11c09c97110f12
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558683"
---
# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Action qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: String\>& GetMetadataToRemove () const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove fonction)
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd fonction)
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne** : Const std::vector<std::pair<std::string, std::string>>& La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.