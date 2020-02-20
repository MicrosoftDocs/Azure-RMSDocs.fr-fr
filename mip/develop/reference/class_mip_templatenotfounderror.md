---
title: 'MIP :: TemplateNotFoundError, classe'
description: 'Documente la classe MIP :: templatenotfounderror du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: babcf77de224a75b2beec7e0b15c867698b49c15
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489314"
---
# <a name="class-miptemplatenotfounderror"></a>MIP :: TemplateNotFoundError, classe 
L’ID de modèle n’est pas reconnu par le service RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String mMessage  | _Pas encore documenté._
public std :: Map\<std :: String, std :: String\> mDebugInfo  | _Pas encore documenté._
public char const* what() const  |  Obtenir le message d’erreur.
public std :: shared_ptr\<erreur\> Clone () const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public const std :: String & GetErrorName () const  |  Obtenir le nom de l’erreur.
public const std :: String & GetMessage () const  |  Obtenir le message d’erreur.
public void SetMessage (const std :: String & msg)  |  Définir le message d’erreur.
public void AddDebugInfo (const std :: String & clé, const std :: String & value)  |  Ajouter une entrée d’informations de débogage.
public const std :: Map\<std :: String, std :: String\>& GetDebugInfo () const  |  Obtient les informations de débogage.
  
## <a name="members"></a>Membres
  
### <a name="mmessage"></a>mMessage
_Pas encore documenté._

  
### <a name="mdebuginfo"></a>mDebugInfo
_Pas encore documenté._

  
### <a name="what-function"></a>fonction
Obtenir le message d’erreur.

  
**Retourne** : message d’erreur
  
### <a name="clone-function"></a>Cloner une fonction
Cloner l’erreur.

  
**Retourne** : un clone de l’erreur.
  
### <a name="geterrortype-function"></a>GetErrorType fonction)
Obtenir le type de l’erreur.

  
**Retourne** : le type de l’erreur.
  
### <a name="geterrorname-function"></a>GetErrorName fonction)
Obtenir le nom de l’erreur.

  
**Retourne** : le nom de l’erreur.
  
### <a name="getmessage-function"></a>Fonction GetMessage
Obtenir le message d’erreur.

  
**Retourne** : le message d’erreur.
  
### <a name="setmessage-function"></a>SetMessage fonction)
Définir le message d’erreur.

Paramètres :  
* **msg** : le message d’erreur.


  
### <a name="adddebuginfo-function"></a>AddDebugInfo fonction)
Ajouter une entrée d’informations de débogage.

Paramètres :  
* **clé**: clé d’informations de débogage 


* **valeur**: valeur des informations de débogage


  
### <a name="getdebuginfo-function"></a>GetDebugInfo fonction)
Obtient les informations de débogage.

  
**Retourne**: informations de débogage (clés/valeurs)