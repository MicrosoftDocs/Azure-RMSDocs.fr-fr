---
title: mip::PolicyProfile::Observer, classe
description: Décrit la classe mip::policyprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: f9ff2448b3ae09e094189e85b15b2fabad12321e
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184550"
---
# <a name="class-mippolicyprofileobserver"></a>mip::PolicyProfile::Observer, classe 
Interface [Observer](class_mip_policyprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
Toutes les erreurs héritent de [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public OnLoadSuccess void virtuel (const std::shared_ptr\<PolicyProfile\>& profil, const std::shared_ptr\<void\>& contexte)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public OnListEnginesFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public OnUnloadEngineSuccess void virtuel (const std::shared_ptr\<void\>& contexte)  |  Appelé quand le déchargement d’un moteur a réussi.
public OnUnloadEngineFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public OnAddEngineSuccess void virtuel (const std::shared_ptr\<PolicyEngine\>& moteur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  Appelé avant la création de moteur pour décrire ou non les données du moteur de stratégie doivent être extraite à partir du serveur ou si elle peut être créée à partir des données mises en cache localement.
public OnAddEngineFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Appelé lorsque la stratégie a été modifiée pour le moteur avec l’ID spécifié, ou lorsque les Types de sensibilité personnalisé chargé ont changé.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : profil actuel utilisé pour démarrer l’opération. 


* **contexte**: contexte passé à l’opération LoadAsync.


  
### <a name="onloadfailure-function"></a>OnLoadFailure (fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de chargement. 


* **contexte**: contexte passé à l’opération LoadAsync.


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **contexte**: contexte passé à l’opération ListEnginesAsync.


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **contexte**: contexte passé à l’opération ListEnginesAsync.


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess (fonction)
Appelé quand le déchargement d’un moteur a réussi.

Paramètres :  
* **contexte**: contexte passé à l’opération UnloadEngineAsync.


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure (fonction)
Appelé quand le déchargement d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de déchargement du moteur. 


* **contexte**: contexte passé à l’opération UnloadEngineAsync.


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **moteur**: le moteur qui vient d’être ajouté 


* **contexte**: contexte passé à l’opération AddEngineAsync


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting (fonction)
Appelé avant la création de moteur pour décrire ou non les données du moteur de stratégie doivent être extraite à partir du serveur ou si elle peut être créée à partir des données mises en cache localement.

Paramètres :  
* **requiresPolicyFetch**: Décrit si les données de moteur doivent être extraites par le biais de HTTP ou si elle est chargée à partir du cache


Ce rappel facultatif peut être utilisé par une application pour être informé ou non une opération AddEngineAsync nécessitera une opération HTTP (avec son délai associé) pour terminer.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **contexte**: contexte passé à l’opération AddEngineAsync.


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **contexte**: contexte passé à l’opération DeleteEngineAsync.


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **contexte**: contexte passé à l’opération DeleteEngineAsync.


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged (fonction)
Appelé lorsque la stratégie a été modifiée pour le moteur avec l’ID spécifié, ou lorsque les Types de sensibilité personnalisé chargé ont changé.

Paramètres :  
* **engineId** : moteur 


Pour charger la nouvelle stratégie, il est nécessaire de rappeler AddEngineAsync avec l’ID de moteur donné.