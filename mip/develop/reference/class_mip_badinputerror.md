---
title: mip BadInputError, classe
description: Informations de référence pour la classe mip BadInputError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 1ee772499e55f413d8c7f4aa0d926cf2b579106d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446168"
---
# <a name="class-mipbadinputerror"></a>mip::BadInputError, classe 
Erreur d’entrée incorrecte, levée quand l’entrée dans une API SDK n’est pas valide.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public char const* what() const  |  Obtenir le message d’erreur.
public std::shared_ptr<Error> Clone() const  |  Cloner l’erreur.
 public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
 public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
 public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
 public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="what"></a>what
Obtenir le message d’erreur.

  
**Retourne** : message d’erreur
  
### <a name="error"></a>Erreur
Cloner l’erreur.

  
**Retourne** : un clone de l’erreur.
  
### <a name="errortype"></a>ErrorType
Obtenir le type de l’erreur.

  
**Retourne** : le type de l’erreur.
  
### <a name="geterrorname"></a>GetErrorName
Obtenir le nom de l’erreur.

  
**Retourne** : le nom de l’erreur.
  
### <a name="getmessage"></a>GetMessage
Obtenir le message d’erreur.

  
**Retourne** : le message d’erreur.
  
### <a name="setmessage"></a>SetMessage
Définir le message d’erreur.

Paramètres :  
* **msg** : le message d’erreur.

