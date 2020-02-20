---
title: mip::MetadataAction, classe
description: 'Documente la classe MIP :: metadataaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 85d2742d5602dc2e36d9370a33fd04050fbeee9d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487716"
---
# <a name="class-mipmetadataaction"></a>mip::MetadataAction, classe 
Action qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: String\>& GetMetadataToRemove () const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetMetadataToAdd () const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove fonction)
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd fonction)
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne** : Const std::vector<std::pair<std::string, std::string>>& La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.