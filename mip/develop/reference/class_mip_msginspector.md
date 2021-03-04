---
title: MsgInspector de classe
description: 'Documente la classe msginspector :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: b9a1f4e96b4a8a80280007353d578391f6a02e50
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844249"
---
# <a name="class-msginspector"></a>MsgInspector de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<uint8_t\>& GetBody () const  |  Obtient le corps du message. si TXT/HTML est au format UTF8.
unsigned int GetCodePage () const non signé  |  Obtient la page de codes d’encodage du corps, pertinente pour les formats txt et de corps HTML.
public BodyType GetBodyType () const  |  Obtient le type de corps.
public const std :: Vector \<std::shared_ptr\<MsgAttachmentData\> \>& GetAttachments () const  |  Obtient une liste de pièces jointes sous forme d’objets de données de pièce jointe MSG.
public InspectorType GetInspectorType () const  |  Obtient les types de fichiers,.
public std :: shared_ptr \<Stream\> GetFileStream () const  |  Obtient le flux de fichier.
  
## <a name="members"></a>Membres
  
### <a name="getbody-function"></a>GetBody fonction)
Obtient le corps du message. si TXT/HTML est au format UTF8.

  
**Retourne**: un vecteur d’octets.
  
### <a name="getcodepage-function"></a>GetCodePage fonction)
Obtient la page de codes d’encodage du corps, pertinente pour les formats txt et de corps HTML.

  
**Retourne**: une page de codes non signée. 
  
**Voir aussi**: [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](/windows/win32/intl/code-page-identifiers)
  
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