---
title: mip::AddContentHeaderAction, classe
description: Décrit la classe mip::addcontentheaderaction de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8cd04bc610944bbbdf00873267161b06a9c09038
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650933"
---
# <a name="class-mipaddcontentheaderaction"></a>mip::AddContentHeaderAction, classe 
Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément d’en-tête de contenu.
public const std::string& GetText() const  |  Obtenir le texte devant être placé dans l’en-tête de contenu.
public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.
public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.
public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.
public ContentMarkAlignment GetAlignment() const  |  Obtenir l’alignement de l’en-tête.
public int GetMargin() const  |  Obtenir la marge de l’en-tête à partir du bas.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName (fonction)
API utilisée pour marquer l’élément d’en-tête de contenu.

  
**Retourne**: Le nom doit être utilisé pour l’élément d’interface qui contient l’en-tête de contenu. Le même nom est retourné dans [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) si l’en-tête de contenu doit être supprimé.
  
### <a name="gettext-function"></a>GetText (fonction)
Obtenir le texte devant être placé dans l’en-tête de contenu.

  
**Retourne**: Texte d’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName (fonction)
Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize (fonction)
Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Taille de police en tant qu’entier.
  
### <a name="getfontcolor-function"></a>GetFontColor (fonction)
Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Couleur de police sous forme de chaîne (par exemple, #000000 »).
  
### <a name="getalignment-function"></a>GetAlignment (fonction)
Obtenir l’alignement de l’en-tête.

  
**Retourne**: L’énumérateur ContentMarkAlignment : GAUCHE | DROITE | CENTER. 
  
**Voir aussi**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin (fonction)
Obtenir la marge de l’en-tête à partir du bas.

  
**Retourne**: Les marges à partir du bas du document (par exemple, 10 mm).
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.