---
title: mip::AddWatermarkAction, classe
description: 'Documente la classe MIP:: addwatermarkaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2b6a50385e5d891b8893949a8761e7f38f591f17
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056338"
---
# <a name="class-mipaddwatermarkaction"></a>mip::AddWatermarkAction, classe 
Classe d’action qui spécifie l’ajout d’un filigrane.
  
## <a name="summary"></a>Récapitulatif
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

  
**Retourne**: Nom à utiliser pour l’élément d’interface utilisateur qui contient le filigrane. Le même nom est retourné dans RemoveWatermarkingAction si le filigrane doit être supprimé.
  
### <a name="getlayout-function"></a>GetLayout fonction)
API utilisée pour obtenir la disposition du filigrane.

  
**Retourne**: WatermarkLayout : disposition du filigrane sous forme d’enum HORIZONTAL|DIAGONAL. .
  
### <a name="gettext-function"></a>GetText, fonction
Obtenir le texte devant être placé dans le filigrane.

  
**Retourne**: Texte d’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName fonction)
Obtenir le nom de la police utilisée pour afficher le filigrane.

  
**Retourne**: Nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize fonction)
Obtenir la taille de la police utilisée pour afficher le filigrane.

  
**Retourne**: Taille de police sous la forme d’un entier.
  
### <a name="getfontcolor-function"></a>GetFontColor fonction)
Obtenir la couleur de la police utilisée pour afficher le filigrane.

  
**Retourne**: Couleur de police sous forme de chaîne (par exemple, «#000000»).