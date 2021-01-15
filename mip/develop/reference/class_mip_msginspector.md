---
title: MsgInspector de classe
description: 'Documente la classe msginspector :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: aaf9cc6803e0111cd37960f356d8a6bb19fd60a5
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215168"
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
  
**Voir aussi**: [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](https://docs.microsoft.com/windows/win32/intl/code-page-identifiers)
  
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