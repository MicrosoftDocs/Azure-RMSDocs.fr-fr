---
title: MsgInspector de classe
description: 'Documente la classe msginspector :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 79a044099c09d799d77f4af11eb0b80ecc21d6d6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761480"
---
# <a name="class-msginspector"></a>MsgInspector de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector\<Uint8_t\>& GetBody ()  |  Obtient le corps du message. si TXT/HTML est au format UTF8.
public BodyType GetBodyType () const  |  Obtient le type de corps.
public const std :: Vector\<std :: shared_ptr\<MsgAttachmentData\> \>& GetAttachments () const  |  Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.
public InspectorType GetInspectorType () const  |  Obtient les types de fichiers,.
public std :: shared_ptr\<Stream\> GetFileStream () const  |  Obtient le flux de fichier.
  
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