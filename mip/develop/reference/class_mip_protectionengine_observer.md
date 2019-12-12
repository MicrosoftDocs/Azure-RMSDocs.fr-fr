---
title: class mip::ProtectionEngine::Observer
description: Documente la classe MIP ::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e5196535dc474d2649c084b55c55a80c3af349b9
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560758"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications liées à ProtectionEngine.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std :: shared_ptr\<std :: Vector\<std :: String\>\>& templateIds, const std :: shared_ptr\<void\>& contexte)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess (const std :: shared_ptr\<std :: Vector\<std :: String\>\>& droits, const std :: shared_ptr\<void\>& contexte)  |  Appelé en cas de récupération réussie des droits.
public virtual void OnGetRightsForLabelIdFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess fonction)
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateIds** : récupère une référence à la liste des modèles 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetTemplatesAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetTemplatesAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetTemplatesSuccess ou ProtectionEngine :: O bserver::OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure fonction)
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des modèles 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetTemplatesAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetTemplatesAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetTemplatesSuccess ou ProtectionEngine :: O bserver::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess fonction)
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **rights** : référence à la liste des droits récupérés 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetRightsForLabelIdAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure fonction)
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des droits 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetRightsForLabelIdAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure