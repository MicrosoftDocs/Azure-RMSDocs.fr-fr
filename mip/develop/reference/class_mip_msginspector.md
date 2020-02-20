---
title: 'MIP :: MsgInspector, classe'
description: 'Documente la classe MIP :: msginspector du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d2c4f85989e5d9d77ebb540b0b4adfd64b8334c1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489892"
---
# <a name="class-mipmsginspector"></a>MIP :: MsgInspector, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<uint8_t\>& GetBody ()  |  Obtient le corps du message. si TXT/HTML est au format UTF8.
public BodyType GetBodyType () const  |  Obtient le type de corps.
public const std :: Vector\<std :: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.
public InspectorType GetInspectorType () const  |  Obtient les types de fichiers,.
public std :: shared_ptr\<flux\> GetFileStream () const  |  Obtient le flux de fichier.
  
## <a name="members"></a>Membres
  
### <a name="getbody-function"></a>GetBody fonction)
Obtient le corps du message. si TXT/HTML est au format UTF8.

  
**Retourne**: un vecteur d’octets.
  
### <a name="getbodytype-function"></a>GetBodyType fonction)
Obtient le type de corps.

  
**Retourne**: le type de corps du message.
  
### <a name="getattachments-function"></a>GetAttachments fonction)
Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.

  
**Retourne**: un vecteur de std :: unique_ptr<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType fonction)
Obtient les types de fichiers,.

  
**Retourne**: InspectorType.
  
### <a name="getfilestream-function"></a>GetFileStream fonction)
Obtient le flux de fichier.

  
**Retourne**: PTR partagé dans le flux de fichier.