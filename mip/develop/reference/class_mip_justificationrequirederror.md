---
title: mip::JustificationRequiredError, classe
description: Décrit la classe mip::justificationrequirederror de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 721037296ecc7d92fae6747a408ce84bfda4b34a
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650916"
---
# <a name="class-mipjustificationrequirederror"></a>mip::JustificationRequiredError, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::shared_ptr virtuel\<erreur\> Clone() const  |  Cloner l’erreur.
public char const* what() const  |  Obtenir le message d’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="clone-function"></a>Clone, fonction
Cloner l’erreur.

  
**Retourne**: Un clone de l’erreur.
  
### <a name="what-function"></a>Quelle est la fonction
Obtenir le message d’erreur.

  
**Retourne**: Le message d’erreur
  
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

