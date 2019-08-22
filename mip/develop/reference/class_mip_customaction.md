---
title: mip::CustomAction, classe
description: 'Documente la classe MIP:: CustomAction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: e71adc9c791f71b73c9386955d6b9606f2554f83
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884391"
---
# <a name="class-mipcustomaction"></a>mip::CustomAction, classe 
[CustomAction](class_mip_customaction.md) est une classe d’action générique qui capture toutes les sous-propriétés de l’action sous la forme d’un jeu de propriétés. Il appartient à l’appelant de comprendre la signification de l’action.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  Obtenir le nom de l’action.
public const std:: Vector\<std::p air\<std:: String, std:: String\>\>& GetProperties () const  |  Obtenir la liste de paires clé/valeur des propriétés.
  
## <a name="members"></a>Membres
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de l’action.

  
**Retourne**: Nom de l’action, le cas échéant, une chaîne vide.
  
### <a name="getproperties-function"></a>GetProperties, fonction
Obtenir la liste de paires clé/valeur des propriétés.

  
**Retourne**: Liste de paires clé-valeur.