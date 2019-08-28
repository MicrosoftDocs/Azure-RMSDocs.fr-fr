---
title: mip::ProtectionProfile::Observer, classe
description: Documente la classe MIP::p rotectionprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: e7e260f879fb1e48b19d43f13a451a3a91ee1a39
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057469"
---
# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std:: shared_ptr\<ProtectionProfile\>& Profile, const std::\<shared_ptr\>void & Context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std:: Vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<ProtectionEngine\>& moteur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtuel void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **Profil**: Référence au [ProtectionProfile](class_mip_protectionprofile.md) nouvellement créé


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>OnLoadFailure fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **erreur**: [Erreur](class_mip_error.md) qui s’est produite lors du chargement 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **moteur**: Moteur nouvellement créé 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile:: AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **contexte**: Le même contexte qui a été passé à [ProtectionProfile::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **contexte**: Le même contexte qui a été passé à [ProtectionProfile::D eleteengineasync](class_mip_protectionprofile.md#deleteengineasync-function)

