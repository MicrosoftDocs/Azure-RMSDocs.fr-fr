---
title: 'classe ProtectionHandler :: observer'
description: 'Documente la classe protectionhandler :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd7a2b24b5eb80b3b17c025c43b0e0b31589a00a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214539"
---
# <a name="class-protectionhandlerobserver"></a>classe ProtectionHandler :: observer 
Interface qui reçoit les notifications relatives à ProtectionHandler.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess(const std::shared_ptr\<ProtectionHandler\>& protectionHandler, const std::shared_ptr\<void\>& context)  |  Appelé lorsque ProtectionHandler a été créé avec succès.
public virtual void OnCreateProtectionHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé lorsque la création de ProtectionHandler a échoué.
  
## <a name="members"></a>Membres
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess fonction)
Appelé lorsque ProtectionHandler a été créé avec succès.

Paramètres :  
* **protectionHandler** : ProtectionHandler nouvellement créé


* **context** : le même contexte que celui transmis à ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync, et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure fonction)
Appelé lorsque la création de ProtectionHandler a échoué.

Paramètres :  
* **error** : défaillance qui s’est produite lors de la création 


* **context** : le même contexte que celui transmis à ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync, et ce même contexte sera transféré tel quel à ProtectionEngine::Observer::OnCreateProtectionHandlerSuccess ou ProtectionEngine::Observer::OnCreateProtectionHandlerFailure