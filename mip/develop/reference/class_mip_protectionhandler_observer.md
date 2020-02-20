---
title: class mip::ProtectionHandler::Observer
description: Documente la classe MIP ::p rotectionhandler du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 8f661f3ebf9bc657a4dd6f6356b26cd582d4aa2e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486815"
---
# <a name="class-mipprotectionhandlerobserver"></a>class mip::ProtectionHandler::Observer 
Interface qui reçoit les notifications liées à ProtectionHandler.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnCreateProtectionHandlerSuccess (const std :: shared_ptr\<ProtectionHandler\>& protectionHandler, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque ProtectionHandler a été créé avec succès.
public virtual void OnCreateProtectionHandlerFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lors de l’échec de la création de ProtectionHandler.
  
## <a name="members"></a>Membres
  
### <a name="oncreateprotectionhandlersuccess-function"></a>OnCreateProtectionHandlerSuccess fonction)
Appelé lorsque ProtectionHandler a été créé avec succès.

Paramètres :  
* **protectionHandler**: protectionHandler nouvellement créé


* **Context**: le même contexte qui a été passé à ProtectionEngine :: CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine :: CreateProtectionHandlerFromPublishingLicenseAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine :: CreateProtectionHandlerFromPublishingLicenseAsync, et ce même contexte sera transféré en l’ProtectionEngine :: observer :: OnCreateProtectionHandlerSuccess ou ProtectionEngine :: observer :: OnCreateProtectionHandlerFailure
  
### <a name="oncreateprotectionhandlerfailure-function"></a>OnCreateProtectionHandlerFailure fonction)
Appelé lors de l’échec de la création de ProtectionHandler.

Paramètres :  
* **error** : défaillance qui s’est produite lors de la création 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine :: CreateProtectionHandlerFromPublishingLicenseAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: CreateProtectionHandlerFromDescriptorAsync ou ProtectionEngine :: CreateProtectionHandlerFromPublishingLicenseAsync, et ce même contexte sera transféré en l’ProtectionEngine :: observer :: OnCreateProtectionHandlerSuccess ou ProtectionEngine :: observer :: OnCreateProtectionHandlerFailure