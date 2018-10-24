---
title: mip ProtectionHandler Observer, classe
description: Informations de référence pour la classe mip ProtectionHandler Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 7fed286dec42f16d7dfa8e375ec739264bd365ba
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446165"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
Interface qui reçoit les notifications relatives à [ProtectionHandler](class_mip_protectionhandler.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Appelé lorsque [ProtectionHandler](class_mip_protectionhandler.md) a été créé avec succès.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé lorsque la création de [ProtectionHandler](class_mip_protectionhandler.md) a échoué.
  
## <a name="members"></a>Membres
  
### <a name="oncreateprotectionhandlersuccess"></a>OnCreateProtectionHandlerSuccess
Appelé lorsque [ProtectionHandler](class_mip_protectionhandler.md) a été créé avec succès.

Paramètres :  
* **protectionHandler** : [ProtectionHandler](class_mip_protectionhandler.md) nouvellement créé


* **context** : le même contexte que celui transmis à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync), et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure"></a>OnCreateProtectionHandlerFailure
Appelé lorsque la création de [ProtectionHandler](class_mip_protectionhandler.md) a échoué.

Paramètres :  
* **error** : défaillance qui s’est produite lors de la création 


* **context** : le même contexte que celui transmis à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync](class_mip_protectionengine.md#createprotectionhandlerfromdescriptorasync) ou [ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync](class_mip_protectionengine.md#createprotectionhandlerfrompublishinglicenseasync), et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure