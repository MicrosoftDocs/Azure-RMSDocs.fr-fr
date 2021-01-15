---
title: 'classe ProtectionProfile :: observer'
description: 'Documente la classe protectionprofile :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 38f578991ed9409aed6ea87622d8db79dcd78b06
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214437"
---
# <a name="class-protectionprofileobserver"></a>classe ProtectionProfile :: observer 
Interface qui reçoit les notifications relatives à ProtectionProfile.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr\<ProtectionProfile\>& profile, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std :: Vector \<std::string\>& engineIds, const std :: shared_ptr \<void\>& Context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnAddEngineSuccess(const std::shared_ptr\<ProtectionEngine\>& engine, const std::shared_ptr\<void\>& context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : référence au ProtectionProfile nouvellement créé


* **context** : le même contexte que celui qui a été passé à ProtectionProfile::LoadAsync


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionProfile::LoadAsync, et ce même contexte est transféré tel quel à ProtectionProfile::Observer::OnLoadSuccess ou ProtectionProfile::Observer::OnLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors du chargement 


* **context** : le même contexte que celui qui a été passé à ProtectionProfile::LoadAsync


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à ProtectionProfile::LoadAsync, et ce même contexte est transféré tel quel à ProtectionProfile::Observer::OnLoadSuccess ou ProtectionProfile::Observer::OnLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **context** : même contexte que celui qui a été passé à ProtectionProfile::ListEnginesAsync


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **context** : même contexte que celui qui a été passé à ProtectionProfile::ListEnginesAsync


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **engine** : moteur nouvellement créé 


* **context** : même contexte que celui qui a été passé à ProtectionProfile::AddEngineAsync


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **context** : même contexte que celui qui a été passé à ProtectionProfile::AddEngineAsync


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **context** : même contexte que celui qui a été passé à ProtectionProfile::DeleteEngineAsync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **context** : même contexte que celui qui a été passé à ProtectionProfile::DeleteEngineAsync

