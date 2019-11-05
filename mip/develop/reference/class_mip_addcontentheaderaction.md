---
title: mip::AddContentHeaderAction, classe
description: 'Documente la classe MIP :: addcontentheaderaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 40e9b648799008bcc75b48ae9379f7a3010bd7bd
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559047"
---
# <a name="class-mipaddcontentheaderaction"></a>mip::AddContentHeaderAction, classe 
Classe d’action qui spécifie l’ajout d’un en-tête de contenu.
  
## <a name="summary"></a>Table des matières
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

  
**Retourne** : le nom à utiliser pour l’élément d’interface utilisateur qui contient l’en-tête de contenu. Le même nom sera retourné dans RemoveContentHeaderAction si l’en-tête de contenu doit être supprimé.
  
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

  
**Retourne** : couleur de la police sous forme de chaîne (par exemple, #000000).
  
### <a name="getalignment-function"></a>GetAlignment fonction)
Obtenir l’alignement de l’en-tête.

  
**Retourne** : l’énumérateur ContentMarkAlignment : LEFT|RIGHT|CENTER. 
  
**Voir aussi**: [ContentMarkAlignment](mip-enums-and-structs.md#contentmarkalignment-enum)
  
### <a name="getmargin-function"></a>GetMargin fonction)
Obtenir la marge de l’en-tête à partir du bas.

  
**Retourne** : marges à partir du bas du document (par exemple, 10 mm).