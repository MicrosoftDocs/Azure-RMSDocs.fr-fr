---
title: 'MIP :: MsgInspector, classe'
description: 'Documente la classe MIP :: msginspector du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1234168e4ce3996077b705e904f5765b761ec4c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558605"
---
# <a name="class-mipmsginspector"></a>MIP :: MsgInspector, classe 
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<uint8_t\>& GetBody ()  |  Obtient le corps du message. si TXT/HTML est au format UTF8.
public BodyType GetBodyType () const  |  Obtient le type de corps.
public const std :: Vector\<std :: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.
  
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