---
title: CustomAction de classe
description: 'Documente la classe CustomAction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc67920b517f3a9f75c395b42350cec9d75b23b3
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567173"
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