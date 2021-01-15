---
title: MsgAttachmentData de classe
description: 'Documente la classe msgattachmentdata :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 6082b96649e32e282c544ac5ec46773e7b4be901
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213621"
---
# <a name="class-msgattachmentdata"></a>MsgAttachmentData de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<uint8_t\>& GetBytes ()  |  Obtenir une pièce jointe en tant que vecteur binaire d’octets.
public std :: shared_ptr \<Stream\> GetStream () const  |  Obtenir la pièce jointe en tant que flux binaire.
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