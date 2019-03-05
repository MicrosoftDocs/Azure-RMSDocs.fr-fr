---
title: mip::AddContentFooterAction, classe
description: Décrit la classe mip::addcontentfooteraction de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: dd803c734c099e11b46db1b7d446b03b2eaa8a1e
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332274"
---
# <a name="class-mipaddcontentfooteraction"></a>mip::AddContentFooterAction, classe 
Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément de pied de page de contenu.
public const std::string& GetText() const  |  Obtenir le texte devant être placé dans le pied de page de contenu.
public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.
public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.
public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.
public ContentMarkAlignment GetAlignment() const  |  Obtenir l’alignement du pied de page.
public int GetMargin() const  |  Obtenir la marge du pied de page à partir du bas.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName (fonction)
API utilisée pour marquer l’élément de pied de page de contenu.

  
**Retourne**: Le nom doit être utilisé pour l’élément d’interface utilisateur qui contient le pied de page de contenu. Le même nom est retourné dans [RemoveContentFooterAction](class_mip_removecontentfooteraction.md) si le pied de page de contenu doit être supprimé.
  
### <a name="gettext-function"></a>GetText (fonction)
Obtenir le texte devant être placé dans le pied de page de contenu.

  
**Retourne**: Texte de pied de page de contenu.
  
### <a name="getfontname-function"></a>GetFontName (fonction)
Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne**: Nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize (fonction)
Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne**: Taille de police en tant qu’entier.
  
### <a name="getfontcolor-function"></a>GetFontColor (fonction)
Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne**: Couleur de police sous forme de chaîne (par exemple, « #000000 »).
  
### <a name="getalignment-function"></a>GetAlignment (fonction)
Obtenir l’alignement du pied de page.

  
**Retourne**: L’énumérateur ContentMarkAlignment : GAUCHE | DROITE | CENTER. 
  
**Voir aussi**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin (fonction)
Obtenir la marge du pied de page à partir du bas.

  
**Retourne**: Les marges à partir du bas du document (par exemple, 10 mm).
  
### <a name="gettype-function"></a>Fonction GetType
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.
