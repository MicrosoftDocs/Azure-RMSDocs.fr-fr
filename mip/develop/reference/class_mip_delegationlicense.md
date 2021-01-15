---
title: DelegationLicense de classe
description: 'Documente la classe delegationlicense :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: cfb719a68650b2159574dd6f8d92fb3d0c15a2c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224969"
---
# <a name="class-delegationlicense"></a>DelegationLicense de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<uint8_t\>& GetSerializedDelegationJsonLicense ()  |  Obtient la licence de délégation.
public const std :: Vector \<uint8_t\>& GetSerializedUserLicense (ProtectionHandler : format relicenseformat :P)  |  Obtient la licence utilisateur, si elle est demandée.
public const std :: String& GetUser ()  |  Obtient l’utilisateur pour lequel cette licence a été créée.
  
## <a name="members"></a>Membres
  
### <a name="getserializeddelegationjsonlicense-function"></a>GetSerializedDelegationJsonLicense fonction)
Obtient la licence de délégation.

  
**Retourne**: licence sérialisée. cette licence est liée à l’identité de l’utilisateur qui a effectué la demande.
  
### <a name="getserializeduserlicense-function"></a>GetSerializedUserLicense fonction)
Obtient la licence utilisateur, si elle est demandée.

Paramètres :  
* **format**: licence format



  
**Retourne**: licence utilisateur sérialisée si elle est demandée, sinon vide vecteur cette licence est liée à l’utilisateur délégué dans la demande.
  
### <a name="getuser-function"></a>Fonction GetUser
Obtient l’utilisateur pour lequel cette licence a été créée.

  
**Retourne**: l’utilisateur