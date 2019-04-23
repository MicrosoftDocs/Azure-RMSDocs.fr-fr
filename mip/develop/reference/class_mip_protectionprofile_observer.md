---
title: mip::ProtectionProfile::Observer, classe
description: Décrit la classe mip::protectionprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 386005f6b3eb8a648a83c60315e12782e8cb7457
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184346"
---
# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications relatives à [ProtectionProfile](class_mip_protectionprofile.md).
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OnLoadSuccess void virtuel (const std::shared_ptr\<ProtectionProfile\>& profil, const std::shared_ptr\<void\>& contexte)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public OnListEnginesFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public OnAddEngineSuccess void virtuel (const std::shared_ptr\<ProtectionEngine\>& moteur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public OnAddEngineFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profil**: Une référence à ce nouveau [ProtectionProfile](class_mip_protectionprofile.md)


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onloadfailure-function"></a>OnLoadFailure (fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **Erreur**: [Erreur](class_mip_error.md) qui s’est produite lors du chargement 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function)


Une application peut passer n’importe quel type de contexte (par exemple, std::promise, std::function) à [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#addengineasync-function), et ce même contexte est transféré tel quel à [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess-function) ou [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure-function)
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::ListEnginesAsync](class_mip_protectionprofile.md#listenginesasync-function)


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **moteur**: Qui vient d’être créé moteur 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::AddEngineAsync](class_mip_protectionprofile.md#addengineasync-function)


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **contexte**: Le même contexte que celui qui a été passé à [ProtectionProfile::DeleteEngineAsync](class_mip_protectionprofile.md#deleteengineasync-function)

