---
title: mip::TransientNetworkError, classe
description: Décrit la classe mip::transientnetworkerror de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ff9aa768559b56f897289ec30ade9b7c408c92d4
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60185009"
---
# <a name="class-miptransientnetworkerror"></a>mip::TransientNetworkError, classe 
Erreur de mise en réseau temporaire. Causée par un comportement inattendu lors d’appels réseau aux points de terminaison du service. L’opération peut être retentée, car cette erreur est une erreur temporaire.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public char const* what() const  |  Obtenir le message d’erreur.
public std::shared_ptr\<erreur\> Clone() const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
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

