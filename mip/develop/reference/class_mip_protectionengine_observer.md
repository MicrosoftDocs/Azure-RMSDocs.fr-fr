---
title: class mip::ProtectionEngine::Observer
description: Documente la classe MIP::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8985b5646849338213855017da042538a27c935b
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057635"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications relatives à [ProtectionEngine](class_mip_protectionengine.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& templateIds, const std:: shared_ptr\<void\>& Context)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess (const std:: shared_ptr\<std:: Vector\<std:: String\>\>& droits, const std:: shared_ptr\<void\>& Context)  |  Appelé en cas de récupération réussie des droits.
public virtual void OnGetRightsForLabelIdFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess fonction)
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateIds**: Référence à la liste des modèles récupérés 


* **contexte**: Le même contexte qui a été passé à [ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure fonction)
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **erreur**: [Erreur](class_mip_error.md) qui s’est produite lors de la récupération des modèles 


* **contexte**: Le même contexte qui a été passé à [ProtectionEngine:: GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function)


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync-function), et ce même contexte est transféré tel quel à [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess-function) ou à [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure-function)
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess fonction)
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **droits**: Référence à la liste des droits récupérés 


* **contexte**: Le même contexte qui a été passé à ProtectionEngine:: GetRightsForLabelIdAsync.


Une application peut passer n’importe quel type de contexte (par exemple, std::p romise, std:: Function) à ProtectionEngine:: GetRightsForLabelIdAsync. ce même contexte sera transféré en l' [ProtectionEngine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou [ProtectionEngine:: observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure fonction)
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **erreur**: [Erreur](class_mip_error.md) qui s’est produite lors de la récupération des droits 


* **contexte**: Le même contexte qui a été passé à ProtectionEngine:: GetRightsForLabelIdAsync.


Une application peut passer n’importe quel type de contexte (par exemple, std::p romise, std:: Function) à ProtectionEngine:: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à [ProtectionEngine:: observer:: OnGetRightsForLabelIdSuccess](class_mip_protectionengine_observer.md#ongetrightsforlabelidsuccess-function) ou [ProtectionEngine:: observer:: OnGetRightsForLabelIdFailure](class_mip_protectionengine_observer.md#ongetrightsforlabelidfailure-function)