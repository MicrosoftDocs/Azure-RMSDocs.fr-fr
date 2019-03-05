---
title: mip::AddWatermarkAction, classe
description: Décrit la classe mip::addwatermarkaction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 8121763106c9f46022264a7eea3bc16e363e523c
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330472"
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
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName (fonction)
API utilisée pour marquer l’élément de filigrane.

  
**Retourne**: Le nom doit être utilisé pour l’élément d’interface utilisateur qui contient le filigrane. Le même nom est retourné dans RemoveWatermarkingAction si le filigrane doit être supprimé.
  
### <a name="getlayout-function"></a>GetLayout (fonction)
API utilisée pour obtenir la disposition du filigrane.

  
**Retourne**: WatermarkLayout : disposition du filigrane sous forme d’enum HORIZONTAL|DIAGONAL. ,
  
### <a name="gettext-function"></a>GetText (fonction)
Obtenir le texte devant être placé dans le filigrane.

  
**Retourne**: Texte d’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName (fonction)
Obtenir le nom de la police utilisée pour afficher le filigrane.

  
**Retourne**: Nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize (fonction)
Obtenir la taille de la police utilisée pour afficher le filigrane.

  
**Retourne**: Taille de police en tant qu’entier.
  
### <a name="getfontcolor-function"></a>GetFontColor (fonction)
Obtenir la couleur de la police utilisée pour afficher le filigrane.

  
**Retourne**: Couleur de police sous forme de chaîne (par exemple, « #000000 »).
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.
