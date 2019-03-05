---
title: class mip::ProtectionHandler::Observer
description: Décrit la classe mip::protectionhandler de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 00d74069374850a562547cd161ad4c5f15927b0a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333719"
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
