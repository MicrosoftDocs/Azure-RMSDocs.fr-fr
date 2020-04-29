---
title: 'classe ProtectionHandler :: observer'
description: 'Documente la classe protectionhandler :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 66453d343505cc57427e177eac258b83a2663eb0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764438"
---
# <a name="class-protectionhandlerobserver"></a>classe ProtectionHandler :: observer 
Interface qui reçoit les notifications relatives à ProtectionHandler.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std :: shared_ptr\<protectionHandler\>& ProtectionHandler, const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque ProtectionHandler a été créé avec succès.
public virtual void OnCreateProtectionHandlerFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque la création de ProtectionHandler a échoué.
  
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