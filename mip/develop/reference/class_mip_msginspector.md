---
title: 'MIP:: MsgInspector, classe'
description: 'Documente la classe MIP:: msginspector du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 274ada562bae46add2429a2f87442bb77528ea05
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054269"
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