---
title: mip JustificationRequiredError, classe
description: Informations de référence pour la classe mip JustificationRequiredError
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 059d139fc5222fd5f1865c66834519347e23a5a9
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445986"
---
# <a name="class-mipjustificationrequirederror"></a>mip::JustificationRequiredError, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual std::shared_ptr<Error> Clone() const  |  Cloner l’erreur.
 public char const* what() const  |  Obtenir le message d’erreur.
 public virtual ErrorType GetErrorType() const  |  Obtenir le type de l’erreur.
 public virtual const std::string& GetErrorName() const  |  Obtenir le nom de l’erreur.
 public virtual const std::string& GetMessage() const  |  Obtenir le message d’erreur.
 public virtual void SetMessage(const std::string& msg)  |  Définir le message d’erreur.
  
## <a name="members"></a>Membres
  
### <a name="error"></a>Erreur
Cloner l’erreur.

  
**Retourne** : un clone de l’erreur.
  
### <a name="what"></a>what
Obtenir le message d’erreur.

  
**Retourne** : message d’erreur
  
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

