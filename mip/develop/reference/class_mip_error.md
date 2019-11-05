---
title: mip::Error, classe
description: 'Documente la classe MIP :: Error du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f59a2b394cbf0bfa5deb555e2c4cdd8c427ed7ea
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560295"
---
# <a name="class-miperror"></a>mip::Error, classe 
Classe de base pour toutes les erreurs qui seront signalées (levées ou retournées) à partir du SDK MIP.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Obtenir le message d’erreur.
public std :: shared_ptr\<erreur\> Clone () const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
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

