---
title: mip::AddContentFooterAction, classe
description: 'Documente la classe MIP :: addcontentfooteraction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 83452da929250dac907dd53868733c77eb26b877
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560396"
---
# <a name="class-mipaddcontentfooteraction"></a>mip::AddContentFooterAction, classe 
Classe d’action qui spécifie l’ajout d’un pied de page de contenu au document.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetUIElementName()  |  API utilisée pour marquer l’élément de pied de page de contenu.
public const std::string& GetText() const  |  Obtenir le texte devant être placé dans le pied de page de contenu.
public const std::string& GetFontName() const  |  Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.
public int GetFontSize() const  |  Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.
public const std::string& GetFontColor() const  |  Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.
public ContentMarkAlignment GetAlignment() const  |  Obtenir l’alignement du pied de page.
public int GetMargin() const  |  Obtenir la marge du pied de page à partir du bas.
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName fonction)
API utilisée pour marquer l’élément de pied de page de contenu.

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient le pied de page de contenu. Le même nom sera retourné dans RemoveContentFooterAction si le pied de page de contenu doit être supprimé.
  
### <a name="gettext-function"></a>GetText, fonction
Obtenir le texte devant être placé dans le pied de page de contenu.

  
**Retourne** : le texte du pied de page de contenu.
  
### <a name="getfontname-function"></a>GetFontName fonction)
Obtenir le nom de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : le nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize fonction)
Obtenir la taille de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor-function"></a>GetFontColor fonction)
Obtenir la couleur de la police utilisée pour afficher le pied de page de contenu.

  
**Retourne** : couleur de la police sous forme de chaîne (par exemple, #000000).
  
### <a name="getalignment-function"></a>GetAlignment fonction)
Obtenir l’alignement du pied de page.

  
**Retourne** : l’énumérateur ContentMarkAlignment : LEFT|RIGHT|CENTER. 
  
**Voir aussi**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin fonction)
Obtenir la marge du pied de page à partir du bas.

  
**Retourne** : marges à partir du bas du document (par exemple, 10 mm).