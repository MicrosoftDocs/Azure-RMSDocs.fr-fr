---
title: AddWatermarkAction de classe
description: 'Documente la classe addwatermarkaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8b5767999b666e6cd8a2b9f42d9d86e690000681
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212363"
---
# <a name="class-addwatermarkaction"></a>AddWatermarkAction de classe 
Classe d’action qui spécifie l’ajout d’un filigrane.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément de filigrane.
public WatermarkLayout GetLayout() const  |  API utilisée pour obtenir la disposition du filigrane.
public const std::string& GetText() const  |  Obtenir le texte devant être placé dans le filigrane.
public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher le filigrane.
public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher le filigrane.
public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher le filigrane.
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName fonction)
API utilisée pour marquer l’élément de filigrane.

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient le filigrane. Le même nom est retourné dans RemoveWatermarkingAction si le filigrane doit être supprimé.
  
### <a name="getlayout-function"></a>GetLayout fonction)
API utilisée pour obtenir la disposition du filigrane.

  
**Retourne** : WatermarkLayout - la disposition du filigrane sous forme d’enum HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>GetText, fonction
Obtenir le texte devant être placé dans le filigrane.

  
**Retourne** : le texte de l’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName fonction)
Obtenir le nom de la police utilisée pour afficher le filigrane.

  
**Retourne** : le nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize fonction)
Obtenir la taille de la police utilisée pour afficher le filigrane.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor-function"></a>GetFontColor fonction)
Obtenir la couleur de la police utilisée pour afficher le filigrane.

  
**Retourne** : couleur de la police sous forme de chaîne (par exemple, #000000).