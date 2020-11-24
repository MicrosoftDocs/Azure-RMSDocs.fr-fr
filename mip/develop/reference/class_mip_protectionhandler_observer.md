---
title: 'classe ProtectionHandler :: observer'
description: 'Documente la classe protectionhandler :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 092448f4af5c27625b8a19f7cfea039e9bcd8071
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567138"
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