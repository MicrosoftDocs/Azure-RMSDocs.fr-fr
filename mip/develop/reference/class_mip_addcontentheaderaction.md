---
title: mip::AddContentHeaderAction, classe
description: 'Documente la classe MIP:: addcontentheaderaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 131d2902efc988a75e7aee262d09e8a71e655bcc
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056416"
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
  
## <a name="members"></a>Membres
  
### <a name="getuielementname-function"></a>GetUIElementName fonction)
API utilisée pour marquer l’élément d’en-tête de contenu.

  
**Retourne**: Nom à utiliser pour l’élément d’interface utilisateur qui contient l’en-tête de contenu. Le même nom est retourné dans [RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) si l’en-tête de contenu doit être supprimé.
  
### <a name="gettext-function"></a>GetText, fonction
Obtenir le texte devant être placé dans l’en-tête de contenu.

  
**Retourne**: Texte d’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName fonction)
Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize fonction)
Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Taille de police sous la forme d’un entier.
  
### <a name="getfontcolor-function"></a>GetFontColor fonction)
Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: Couleur de police sous forme de chaîne (par exemple, #000000»).
  
### <a name="getalignment-function"></a>GetAlignment fonction)
Obtenir l’alignement de l’en-tête.

  
**Retourne**: Énumérateur ContentMarkAlignment: À GAUCHE | À DROITE | GESTIONNAIRE. 
  
**Voir aussi**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin fonction)
Obtenir la marge de l’en-tête à partir du bas.

  
**Retourne**: Marges à partir du bas du document (par exemple, 10 mm).