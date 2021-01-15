---
title: CustomAction de classe
description: 'Documente la classe CustomAction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1fb231d76ba2b5f076d42bbeeff95618c7386f3
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211700"
---
# <a name="class-customaction"></a>CustomAction de classe 
CustomAction est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un conteneur de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtenir le nom de l’action.
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetProperties () const  |  Obtenir la liste de paires clé/valeur des propriétés.
  
## <a name="members"></a>Membres
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de l’action.

  
**Retourne** : nom de l’action s’il existe ; sinon une chaîne vide.
  
### <a name="getproperties-function"></a>GetProperties, fonction
Obtenir la liste de paires clé/valeur des propriétés.

  
**Retourne** : une liste de paires clé/valeur.