---
title: 'MIP:: MsgInspector, classe'
description: 'Documente la classe MIP:: msginspector du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: cb0b85b0de42eae46d6cd7c9c6d6e18680b2e545
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69892747"
---
# <a name="class-mipmsginspector"></a>MIP:: MsgInspector, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std:: Vector\<uint8_t\>& GetBody ()  |  Obtient le corps du message. si TXT/HTML est au format UTF8.
public BodyType GetBodyType () const  |  Obtient le type de corps.
public const std:: Vector\<std:: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.
public InspectorType GetInspectorType () const  |  Obtient les types de fichiers,.
public std:: shared_ptr\<Stream\> GetFileStream () const  |  Obtient le flux de fichier.
  
## <a name="members"></a>Membres
  
### <a name="getbody-function"></a>GetBody fonction)
Obtient le corps du message. si TXT/HTML est au format UTF8.

  
**Retourne**: Vecteur d’octets.
  
### <a name="getbodytype-function"></a>GetBodyType fonction)
Obtient le type de corps.

  
**Retourne**: Type du corps du message.
  
### <a name="getattachments-function"></a>GetAttachments fonction)
Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.

  
**Retourne**: Vecteur de std:: unique_ptr<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType fonction)
Obtient les types de fichiers,.

  
**Retourne**: InspectorType.
  
### <a name="getfilestream-function"></a>GetFileStream fonction)
Obtient le flux de fichier.

  
**Retourne**: Ptr partagé dans le flux de fichier.