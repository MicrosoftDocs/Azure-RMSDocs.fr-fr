---
title: mip::CustomAction, classe
description: 'Documente la classe MIP :: CustomAction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 450ae0e455f74c6cb9b1f6b0b6d8aded9b30b2bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558904"
---
# <a name="class-mipcustomaction"></a>mip::CustomAction, classe 
CustomAction est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un conteneur de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Table des matières
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