---
title: mip::TransientNetworkError, classe
description: 'Documente la classe MIP:: transientnetworkerror du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5787c5742edc2daefee00a3c5a9b2bf826b81529
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882901"
---
# <a name="class-miptransientnetworkerror"></a>mip::TransientNetworkError, classe 
Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Obtenir le message d’erreur.
public std:: shared_ptr\<Error\> Clone () const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="what-function"></a>fonction
Obtenir le message d’erreur.

  
**Retourne**: Message d’erreur
  
### <a name="clone-function"></a>Cloner une fonction
Cloner l’erreur.

  
**Retourne**: Un clone de l’erreur.
  
### <a name="geterrortype-function"></a>GetErrorType fonction)
Obtenir le type de l’erreur.

  
**Retourne**: Type d’erreur.
  
### <a name="geterrorname-function"></a>GetErrorName fonction)
Obtenir le nom de l’erreur.

  
**Retourne**: Nom de l’erreur.
  
### <a name="getmessage-function"></a>Fonction GetMessage
Obtenir le message d’erreur.

  
**Retourne**: Message d’erreur.
  
### <a name="setmessage-function"></a>SetMessage fonction)
Définir le message d’erreur.

Paramètres :  
* **msg** : le message d’erreur.

