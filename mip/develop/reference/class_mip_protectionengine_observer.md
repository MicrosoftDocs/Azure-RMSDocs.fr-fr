---
title: 'classe ProtectionEngine :: observer'
description: 'Documente la classe protectionengine :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: ca1f9c3251df30166b123ae31c8e3c5fceef67fc
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764608"
---
# <a name="class-protectionengineobserver"></a>classe ProtectionEngine :: observer 
Interface qui reçoit les notifications relatives à ProtectionEngine.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std :: Vector\<std :: shared_ptr\<TemplateDescriptor\> \>& templateDescriptors, const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess (const std :: shared_ptr\<std :: Vector\<std :: String\> \>& droits, const std :: shared_ptr\<void\>& Context)  |  Appelé en cas de récupération réussie des droits.
public virtual void OnGetRightsForLabelIdFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
public virtuel void OnLoadUserCertSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque le certificat de l’utilisateur a été chargé avec succès.
public virtual void OnLoadUserCertFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé en cas d’échec du chargement du certificat de l’utilisateur.
public virtuel void OnRegisterContentForTrackingAndRevocationSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque l’inscription du contenu pour le suivi & révocation est réussie.
public virtual void OnRegisterContentForTrackingAndRevocationFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque l’inscription du contenu pour le suivi & révocation échoue.
public virtuel void OnRevokeContentSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé en cas de réussite de la révocation de.
public virtual void OnRevokeContentFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé en cas d’échec de la révocation du contenu.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess fonction)
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateDescriptors**: référence à la liste des descripteurs de modèles 


* **context** : le même contexte que celui transmis à [ProtectionProfile::LoadAsync](class_mip_protectionengine.md)


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetTemplatesAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetTemplatesSuccess ou ProtectionEngine :: observer :: OnGetTemplatesFailure.
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure fonction)
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des modèles 


* **context** : le même contexte que celui transmis à ProtectionProfile::LoadAsync


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionEngine::GetTemplatesAsync, et ce même contexte est transféré tel quel à ProtectionEngine::Observer::OnGetTemplatesSuccess ou à ProtectionEngine::Observer::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess fonction)
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **rights** : référence à la liste des droits récupérés 


* **Context**: le même contexte qui a été passé à [ProtectionEngine :: GetRightsForLabelIdAsync](class_mip_protectionengine.md).


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure.
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure fonction)
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des droits 


* **context** : même contexte que celui qui a été passé à ProtectionEngine::GetRightsForLabelIdAsync


Une application peut transmettre n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionEngine::GetRightsForLabelIdAsync, et ce même contexte est transféré tel quel à ProtectionEngine::Observer::OnGetRightsForLabelIdSuccess ou à ProtectionEngine::Observer::OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess fonction)
Appelé lorsque le certificat de l’utilisateur a été chargé avec succès.

Paramètres :  
* **Context**: le même contexte qui a été passé à ProtectionEngine :: LoadUserCert.


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à [ProtectionEngine :: LoadUserCertAsync et ce même contexte sera transféré en l’État à [ProtectionEngine :: observer :: OnLoadUserCertSuccess](class_mip_protectionengine_observer.md) ou [ProtectionEngine :: observer :: OnLoadUserCertFailure](class_mip_protectionengine_observer.md)
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure fonction)
Appelé en cas d’échec du chargement du certificat de l’utilisateur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des droits 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: LoadUserCert


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: LoadUserCertAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnLoadUserCertSuccess ou ProtectionEngine :: observer :: OnLoadUserCertFailure
  
### <a name="onregistercontentfortrackingandrevocationsuccess-function"></a>OnRegisterContentForTrackingAndRevocationSuccess fonction)
Appelé lorsque l’inscription du contenu pour le suivi & révocation est réussie.

Paramètres :  
* **Context**: le même contexte qui a été passé à ProtectionEngine :: RegisterContentForTrackingAndRevocationAsync.


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: RegisterContentForTrackingAndRevocationAsync et ce même contexte sera transféré en l’État à [ProtectionEngine :: observer :: OnRegisterContentForTrackingAndRevocationSuccess](class_mip_protectionengine_observer.md) ou [ProtectionEngine :: observer :: OnRegisterContentForTrackingAndRevocationFailure](class_mip_protectionengine_observer.md)
  
### <a name="onregistercontentfortrackingandrevocationfailure-function"></a>OnRegisterContentForTrackingAndRevocationFailure fonction)
Appelé lorsque l’inscription du contenu pour le suivi & révocation échoue.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de l’inscription du contenu 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: RegisterContentForTrackingAndRevocationAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: RegisterContentForTrackingAndRevocationAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnRegisterContentForTrackingAndRevocationSuccess ou ProtectionEngine :: observer :: OnRegisterContentForTrackingAndRevocationFailure
  
### <a name="onrevokecontentsuccess-function"></a>OnRevokeContentSuccess fonction)
Appelé en cas de réussite de la révocation de.

Paramètres :  
* **Context**: le même contexte qui a été passé à ProtectionEngine :: RevokeContentAsync.


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: RevokeContentAsync et ce même contexte sera transféré en l’État à [ProtectionEngine :: observer :: OnRevokeContentSuccess](class_mip_protectionengine_observer.md) ou [ProtectionEngine :: observer :: OnRevokeContentFailure](class_mip_protectionengine_observer.md)
  
### <a name="onrevokecontentfailure-function"></a>OnRevokeContentFailure fonction)
Appelé en cas d’échec de la révocation du contenu.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la révocation du contenu 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: RevokeContentAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: RevokeContentAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnRevokeContentSuccess ou ProtectionEngine :: observer :: OnRevokeContentFailure