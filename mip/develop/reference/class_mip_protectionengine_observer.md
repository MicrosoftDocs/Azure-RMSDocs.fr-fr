---
title: mip ProtectionEngine Observer, classe
description: Informations de référence pour la classe mip ProtectionEngine Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9999b450d614b4465f151f0b2df80892a83bc143
ms.sourcegitcommit: 4cd90fcf94ac6e2543d8be10e6e29e8218d5fd9d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49651343"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr<std::vector<std::string>>& rights, const std::shared_ptr<void>& context)  |  Appelé en cas de récupération réussie des droits.
public virtual void OnGetRightsForLabelIdFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
public virtual void OnGetGrantingLabelIdsSuccess(const std::shared_ptr<std::vector<std::string>>& labelIds, const std::shared_ptr<void>& context)  |  Appelé en cas de récupération réussie des ID d’étiquettes.
public virtual void OnGetGrantingLabelIdsFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé lors de la récupération des ID d’étiquettes pour l’utilisateur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateIds** : récupère une référence à la liste des modèles 


* **context** : le même contexte que celui transmis à [ProtectionProfile::LoadAsync](class_mip_protectionengine.md#gettemplatesasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **error** : [Erreur](class_mip_error.md) qui s’est produite lors de la récupération de modèles 


* **context** : le même contexte que celui transmis à [ProtectionProfile::LoadAsync](class_mip_protectionengine.md#gettemplatesasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure)
  
### <a name="ongetrightsforlabelidsuccess"></a>OnGetRightsForLabelIdSuccess
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **rights** : référence à la liste des droits récupérés 


* **context** : même contexte que celui qui a été passé à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) ou à [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetrightsforlabelidfailure"></a>OnGetRightsForLabelIdFailure
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **error** : [Erreur](class_mip_error.md) qui s’est produite lors de la récupération de droits 


* **context** : même contexte que celui qui a été passé à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess) ou à [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure)
  
### <a name="ongetgrantinglabelidssuccess"></a>OnGetGrantingLabelIdsSuccess
Appelé en cas de récupération réussie des ID d’étiquettes.

Paramètres :  
* **labelIds** : référence à la liste des ID d’étiquettes récupérés 


* **context** : même contexte que celui qui a été passé à [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) ou à [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)
  
### <a name="ongetgrantinglabelidsfailure"></a>OnGetGrantingLabelIdsFailure
Appelé lors de la récupération des ID d’étiquettes pour l’utilisateur.

Paramètres :  
* **error** : [Erreur](class_mip_error.md) qui s’est produite lors de la récupération d’ID d’étiquettes 


* **context** : même contexte que celui qui a été passé à [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetGrantingLabelIdsAsync](class_mip_protectionengine.md#getgrantinglabelidsasync), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetGrantingLabelIdsSuccess](class_mip_protectionengine_observer.md#ongetgrantinglabelidssuccess) ou à [ProtectionEngine::Observer::OnGetGrantingLabelIdsFailure](class_mip_protectionengine_observer.md#ongetgrantinglabelidsfailure)
