---
title: classe mip::NoPermissionsError
description: Décrit la classe mip::nopermissionserror de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ac10820e1fa167888b857043219711a485632c00
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184584"
---
# <a name="class-mipnopermissionserror"></a>classe mip::NoPermissionsError 
L’utilisateur n’a pas pu obtenir l’accès au contenu. Par exemple, aucune autorisation, contenu révoqué.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  Obtient le contact en cas de droits manquants au document.
public std::string GetOwner() const  | _Pas encore documenté._
public char const* what() const  |  Obtenir le message d’erreur.
public std::shared_ptr\<erreur\> Clone() const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres

### <a name="getreferrer-function"></a>GetReferrer (fonction)
Obtient le contact en cas de droits manquants au document.

  
**Retourne**: Le contact en cas de droits manquants au document.
  
### <a name="getowner-function"></a>GetOwner (fonction)
_Pas encore documenté._

### <a name="what-function"></a>Quelle est la fonction
Obtenir le message d’erreur.

  
**Retourne**: Le message d’erreur
  
### <a name="clone-function"></a>Clone, fonction
Cloner l’erreur.

  
**Retourne**: Un clone de l’erreur.
  
### <a name="geterrortype-function"></a>GetErrorType (fonction)
Obtenir le type de l’erreur.

  
**Retourne**: Le type d’erreur.
  
### <a name="geterrorname-function"></a>GetErrorName (fonction)
Obtenir le nom de l’erreur.

  
**Retourne**: Le nom de l’erreur.
  
### <a name="getmessage-function"></a>Fonction GetMessage
Obtenir le message d’erreur.

  
**Retourne**: Le message d’erreur.
  
### <a name="setmessage-function"></a>SetMessage (fonction)
Définir le message d’erreur.

Paramètres :  
* **msg** : le message d’erreur.