---
title: mip::HttpResponse, classe
description: 'Documente la classe MIP:: HttpResponse du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 4d7711f755f4ffde923eb7d913abdb5bd2a905db
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884124"
---
# <a name="class-miphttpresponse"></a>mip::HttpResponse, classe 
Interface qui décrit une seule réponse HTTP, implémentée par l’application cliente lors du remplacement de [HttpDelegate](class_mip_httpdelegate.md).
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  Obtient l’ID de réponse.
public int32_t GetStatusCode() const  |  Obtenir le code d’état de la réponse.
public const std:: Vector\<uint8_t\>& GetBody () const  |  Obtenir le corps de la requête.
public const std:: map\<std:: String, std:: String, CaseInsensitiveComparator\>& GetHeaders () const  |  Obtenir les en-têtes de requête.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtient l’ID de réponse.

  
**Retourne**: ID de réponse les HttpRequest correspondants auront le même ID
  
### <a name="getstatuscode-function"></a>GetStatusCode fonction)
Obtenir le code d’état de la réponse.

  
**Retourne**: Code d’état
  
### <a name="getbody-function"></a>GetBody fonction)
Obtenir le corps de la requête.

  
**Retourne**: Corps de la demande
  
### <a name="getheaders-function"></a>GetHeaders fonction)
Obtenir les en-têtes de requête.

  
**Retourne**: En-têtes de requête