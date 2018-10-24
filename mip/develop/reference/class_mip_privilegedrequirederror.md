---
title: mip PrivilegedRequiredError, classe
description: Informations de référence pour la classe mip PrivilegedRequiredError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e55228cb48ff779e271695d4f6461be115d05b2f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445748"
---
# <a name="class-mipprivilegedrequirederror"></a>mip::PrivilegedRequiredError, classe 
L’étiquette actuelle a été affectée en tant qu’opération avec des privilèges (l’équivalent d’une opération administrateur), par conséquent, elle ne peut pas être remplacée.
  
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

