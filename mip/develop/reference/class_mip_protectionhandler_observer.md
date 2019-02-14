---
title: class mip::ProtectionHandler::Observer
description: Décrit la classe mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4dac87e4fba8cf5bbcf6eef98ff1edda28a9947f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255842"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
Interface qui reçoit les notifications relatives à [ProtectionHandler](class_mip_protectionhandler.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OnCreateProtectionHandlerSuccess void virtuel (const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& contexte)  |  Appelé lorsque [ProtectionHandler](class_mip_protectionhandler.md) a été créé avec succès.
public OnCreateProtectionHandlerFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé lorsque la création de [ProtectionHandler](class_mip_protectionhandler.md) a échoué.
  
## <a name="members"></a>Membres
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess (fonction)
Appelé lorsque [ProtectionHandler](class_mip_protectionhandler.md) a été créé avec succès.

Paramètres :  
* **protectionHandler**: Nouvellement créé [ProtectionHandler](class_mip_protectionhandler.md)


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function), et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure (fonction)
Appelé lorsque la création de [ProtectionHandler](class_mip_protectionhandler.md) a échoué.

Paramètres :  
* **Erreur**: Échec s’est produite lors de la création 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync-function) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync-function), et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
