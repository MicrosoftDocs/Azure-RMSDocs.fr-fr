---
title: mip ProtectionProfile Observer, classe
description: Informations de référence pour la classe mip ProtectionProfile Observer
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3678e6c1e1659f28b2f1dcc36f61295a8d29393e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446428"
---
# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess(const std::vector<std::string>& engineIds, const std::shared_ptr<void>& context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnAddEngineSuccess(const std::shared_ptr<ProtectionEngine>& engine, const std::shared_ptr<void>& context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr<void>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess"></a>OnLoadSuccess
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : référence au [ProtectionProfile](class_mip_protectionprofile.md) nouvellement créé


* **context** : le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onloadfailure"></a>OnLoadFailure
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **error** : [erreur](class_mip_error.md) qui s’est produite lors du chargement 


* **context** : le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure)
  
### <a name="onlistenginessuccess"></a>OnListEnginesSuccess
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **context** : même contexte que celui qui a été passé à [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onlistenginesfailure"></a>OnListEnginesFailure
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **context** : même contexte que celui qui a été passé à [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync)


  
### <a name="onaddenginesuccess"></a>OnAddEngineSuccess
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **engine** : moteur nouvellement créé 


* **context** : même contexte que celui qui a été passé à [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="onaddenginefailure"></a>OnAddEngineFailure
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **context** : même contexte que celui qui a été passé à [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync)


  
### <a name="ondeleteenginesuccess"></a>OnDeleteEngineSuccess
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **context** : même contexte que celui qui a été passé à [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)


  
### <a name="ondeleteenginefailure"></a>OnDeleteEngineFailure
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **context** : même contexte que celui qui a été passé à [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync)

