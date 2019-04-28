---
title: classe mip::ServiceDisabledError
description: Décrit la classe mip::servicedisablederror de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1373d9ecc03f69267af631216a04d358e8be7af3
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173366"
---
# <a name="class-mipservicedisablederror"></a>classe mip::ServiceDisabledError 
L’utilisateur n’a pas pu obtenir l’accès au contenu en raison d’un service en cours de désactivation.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public GetExtent() étendue const  |  Obtient l’étendue pour laquelle le service est désactivé.
enum étendue  |  Décrit l’étendue pour laquelle le service est désactivé.
public char const* what() const  |  Obtenir le message d’erreur.
public std::shared_ptr\<erreur\> Clone() const  |  Cloner l’erreur.
public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="getextent-function"></a>GetExtent (fonction)
Obtient l’étendue pour laquelle le service est désactivé.

  
**Retourne**: Étendue pour laquelle le service est désactivé
  
### <a name="extent-enum"></a>Enum d’étendue

Décrit l’étendue pour laquelle le service est désactivé.

 Valeurs                         | Descriptions                                
--------------------------------|---------------------------------------------
Utilisateur            | Service est désactivé pour l’utilisateur.
Appareil            | Service est désactivé pour l’appareil.
Plateforme            | Service est désactivé pour la plateforme.
Client            | Service est désactivé pour le locataire.



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