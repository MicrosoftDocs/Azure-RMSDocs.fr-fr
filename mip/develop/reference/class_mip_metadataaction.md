---
title: MetadataAction de classe
description: 'Documente la classe metadataaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d36a97130fd8a04f8053b6c272cea9af050cb89c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761618"
---
# <a name="class-metadataaction"></a>MetadataAction de classe 
Une Action qui ajoute des informations de métadonnées au contenu.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<std :: String\>& GetMetadataToRemove () const  |  Obtenir la liste des noms des métadonnées à supprimer du contenu.
public const std :: Vector\<MetadataEntry\>& GetMetadataToAdd () const  |  Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.
  
## <a name="members"></a>Membres
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove fonction)
Obtenir la liste des noms des métadonnées à supprimer du contenu.

  
**Retourne** : un vecteur de chaînes à supprimer. La suppression de métadonnées doit être effectuée avant l’ajout de métadonnées.
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd fonction)
Obtenir les paires nom/valeur des métadonnées à ajouter au contenu.

  
**Retourne**: const std :: Vector<MetadataEntry>& la suppression des métadonnées doit être effectuée avant l’ajout de métadonnées.