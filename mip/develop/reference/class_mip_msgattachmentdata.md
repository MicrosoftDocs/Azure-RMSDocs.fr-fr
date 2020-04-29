---
title: MsgAttachmentData de classe
description: 'Documente la classe msgattachmentdata :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cec59e4bea8b62ff16005c02fa7a9516c4fb339d
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761444"
---
# <a name="class-msgattachmentdata"></a>MsgAttachmentData de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<Uint8_t\>& GetBytes ()  |  Obtenir une pièce jointe en tant que vecteur binaire d’octets.
public std :: shared_ptr\<Stream\> GetStream () const  |  Obtenir la pièce jointe en tant que flux binaire.
public const std::string& GetName() const  |  Obtenir le nom de la pièce jointe sous forme de chaîne.
public const std :: String& GetLongName () const  |  Obtenir le nom long de la pièce jointe sous forme de chaîne.
public const std::string& GetPath() const  |  Obtient le nom du chemin d’accès des pièces jointes en tant que chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.
public const std :: String& GetLongPath () const  |  Obtient le nom du chemin d’accès long de la pièce jointe sous forme de chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.
  
## <a name="members"></a>Membres
  
### <a name="getbytes-function"></a>GetBytes, fonction
Obtenir une pièce jointe en tant que vecteur binaire d’octets.
  
### <a name="getstream-function"></a>GetStream, fonction
Obtenir la pièce jointe en tant que flux binaire.
  
### <a name="getname-function"></a>Fonction GetName
Obtenir le nom de la pièce jointe sous forme de chaîne.
  
### <a name="getlongname-function"></a>GetLongName fonction)
Obtenir le nom long de la pièce jointe sous forme de chaîne.
  
### <a name="getpath-function"></a>GetPath fonction)
Obtient le nom du chemin d’accès des pièces jointes en tant que chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.
  
### <a name="getlongpath-function"></a>GetLongPath fonction)
Obtient le nom du chemin d’accès long de la pièce jointe sous forme de chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.