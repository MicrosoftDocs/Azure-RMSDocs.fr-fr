---
title: class mip::ProtectionEngine::Observer
description: Décrit la classe mip::protectionengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2473e4bc1e64e3e8de498d2976d07b5324346a53
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173136"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OnGetTemplatesSuccess void virtuel (const std::shared_ptr\<std::vector\<std::string\>\>& templateIds, const std::shared_ptr\<void\>& contexte)  |  Appelé lorsque les modèles ont été récupérés.
public OnGetTemplatesFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess(const std::shared_ptr\<std::vector\<std::string\>\>& rights, const std::shared_ptr\<void\>& context)  |  Appelé en cas de récupération réussie des droits.
public OnGetRightsForLabelIdFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess (fonction)
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateIds**: Extrait une référence à la liste des modèles 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure (fonction)
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **Erreur**: [Erreur](class_mip_error.md) qui s’est produite lors de la récupération des modèles 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess (fonction)
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **droits**: Extrait une référence à la liste des droits 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou à [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure function
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **Erreur**: [Erreur](class_mip_error.md) qui s’est produite lors de la récupération des droits 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetRightsForLabelIdAsync](class_mip_protectionengine.md#getrightsforlabelidasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou à [ProtectionEngine::Observer::OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)