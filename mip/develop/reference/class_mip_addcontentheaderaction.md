---
title: AddContentHeaderAction de classe
description: 'Documente la classe addcontentheaderaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: e5a2993af705855dde94f5be37e22f1e9ab87c99
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212449"
---
# <a name="class-addcontentheaderaction"></a>AddContentHeaderAction de classe 
Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
  
## <a name="summary"></a>Résumé
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

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient l’en-tête de contenu. Le même nom est retourné dans RemoveContentHeaderAction si l’en-tête de contenu doit être supprimé.
  
### <a name="gettext-function"></a>GetText, fonction
Obtenir le texte devant être placé dans l’en-tête de contenu.

  
**Retourne** : le texte de l’en-tête de contenu.
  
### <a name="getfontname-function"></a>GetFontName fonction)
Obtenir le nom de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne** : le nom de la police. La valeur par défaut est Calibri si rien n’est défini par la stratégie.
  
### <a name="getfontsize-function"></a>GetFontSize fonction)
Obtenir la taille de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne** : la taille de la police sous forme de nombre entier.
  
### <a name="getfontcolor-function"></a>GetFontColor fonction)
Obtenir la couleur de la police utilisée pour afficher l’en-tête de contenu.

  
**Retourne**: la couleur de police sous forme de chaîne (par exemple, #000000»).
  
### <a name="getalignment-function"></a>GetAlignment fonction)
Obtenir l’alignement de l’en-tête.

  
**Retourne**: l’énumérateur CONTENTMARKALIGNMENT : Left | À droite | Gestionnaire. 
  
**Voir aussi** : ContentMarkAlignment
  
### <a name="getmargin-function"></a>GetMargin fonction)
Obtenir la marge de l’en-tête à partir du bas.

  
**Retourne** : marges à partir du bas du document (par exemple, 10 mm).