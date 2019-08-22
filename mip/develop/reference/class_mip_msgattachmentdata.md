---
title: 'MIP:: MsgAttachmentData, classe'
description: 'Documente la classe MIP:: msgattachmentdata du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 963968008e1098209270d990e9c6b1ab273b0971
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893308"
---
# <a name="class-mipmsgattachmentdata"></a>MIP:: MsgAttachmentData, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std:: Vector\<uint8_t\>& GetBytes ()  |  Obtenir une pièce jointe en tant que vecteur binaire d’octets.
public std:: shared_ptr\<Stream\> GetStream () const  |  Obtenir la pièce jointe en tant que flux binaire.
public const std::string& GetName() const  |  Obtenir le nom de la pièce jointe sous forme de chaîne.
public const std:: String & GetLongName () const  |  Obtenir le nom long de la pièce jointe sous forme de chaîne.
public const std::string& GetPath() const  |  Obtient le nom du chemin d’accès des pièces jointes en tant que chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.
public const std:: String & GetLongPath () const  |  Obtient le nom du chemin d’accès long de la pièce jointe sous forme de chaîne. Si le chemin d’accès n’est pas vide, référencez la pièce jointe.
  
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