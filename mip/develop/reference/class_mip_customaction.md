---
title: mip::CustomAction, classe
description: 'Documente la classe MIP :: CustomAction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 9dfbd444684f68b954dd577c9ccdd208f55f9a89
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490193"
---
# <a name="class-mipcustomaction"></a>mip::CustomAction, classe 
CustomAction est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un conteneur de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtenir le nom de l’action.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetProperties () const  |  Obtenir la liste de paires clé/valeur des propriétés.
  
## <a name="members"></a>Membres
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de l’action.

  
**Retourne** : nom de l’action s’il existe ; sinon une chaîne vide.
  
### <a name="getproperties-function"></a>GetProperties, fonction
Obtenir la liste de paires clé/valeur des propriétés.

  
**Retourne** : une liste de paires clé/valeur.