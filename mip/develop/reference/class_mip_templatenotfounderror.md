---
title: TemplateNotFoundError de classe
description: 'Documente la classe templatenotfounderror :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 48182ae5d821aeed65e8c28b086dce0349b9af03
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212856"
---
# <a name="class-templatenotfounderror"></a>TemplateNotFoundError de classe 
L’ID de modèle n’est pas reconnu par le service RMS.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String mMessage  | _Pas encore documenté._
public std :: map \<std::string, std::string\> mDebugInfo  | _Pas encore documenté._
public std :: String mName  | _Pas encore documenté._
public ErrorCode GetErrorCode, () const  |  Obtient le errorCode de l’entrée incorrecte.
public char const* what() const  |  Obtenir le message d’erreur.
public std::shared_ptr\<Error\> Clone() const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public const std :: String& GetErrorName () const  |  Obtenir le nom de l’erreur.
public const std :: String& GetMessage () const  |  Obtenir le message d’erreur.
public void SetMessage (const std :: String& MSG)  |  Définir le message d’erreur.
public void AddDebugInfo (const std :: String& clé, const std :: String& value)  |  Ajouter une entrée d’informations de débogage.
public const std :: map \<std::string, std::string\>& GetDebugInfo () const  |  Obtient les informations de débogage.
énumération ErrorCode  |  Code d’erreur de l’erreur d’entrée incorrecte.
  
## <a name="members"></a>Membres
  
### <a name="mmessage"></a>mMessage
_Pas encore documenté._

  
### <a name="mdebuginfo"></a>mDebugInfo
_Pas encore documenté._

  
### <a name="mname"></a>mName
_Pas encore documenté._

  
### <a name="geterrorcode-function"></a>GetErrorCode, fonction)
Obtient le errorCode de l’entrée incorrecte.

  
**Retourne**: ErrorCode d’une erreur d’entrée incorrecte
  
### <a name="what-function"></a>fonction
Obtenir le message d’erreur.

  
**Retourne**: le message d’erreur
  
### <a name="clone-function"></a>Clone, fonction
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

  
**Retourne**: le message d’erreur.
  
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
  
### <a name="errorcode-enum"></a>ErrorCode (énumération)

Code d’erreur de l’erreur d’entrée incorrecte.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Général            | Erreur d’entrée générale incorrecte
FileIsTooLargeForProtection            | Le fichier est trop volumineux pour la protection
