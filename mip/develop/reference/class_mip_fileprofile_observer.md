---
title: mip::FileProfile::Observer, classe
description: Décrit la classe mip::fileprofile de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7b9c3440d577e9ba2e08bdba6ed890d3a480c783
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174097"
---
# <a name="class-mipfileprofileobserver"></a>mip::FileProfile::Observer, classe 
Interface [Observer](class_mip_fileprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
Toutes les erreurs héritent de [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _Pas encore documenté._
public OnLoadSuccess void virtuel (const std::shared_ptr\<mip::FileProfile\>& profil, const std::shared_ptr\<void\>& contexte)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess(const std::vector\<std::string\>& engineIds, const std::shared_ptr\<void\>& context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public OnListEnginesFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public OnUnloadEngineSuccess void virtuel (const std::shared_ptr\<void\>& contexte)  |  Appelé quand le déchargement d’un moteur a réussi.
public OnUnloadEngineFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public OnAddEngineSuccess void virtuel (const std::shared_ptr\<mip::FileEngine\>& moteur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public OnAddEngineFailure void virtuel (std::exception_ptr const & erreur, const std::shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.
public virtual void OnAddPolicyEngineStarting (bool requiresPolicyFetch)  |  Appelé avant la création de moteur pour décrire ou non les données de la stratégie du moteur de stratégie doivent être extraite à partir du serveur ou si elle peut être créée à partir des données mises en cache localement.
protected Observer()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="observer-function"></a>~ Fonction observateur
_Pas encore documenté._

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess (fonction)
Appelé quand le chargement d’un profil a réussi.
  
### <a name="onloadfailure-function"></a>OnLoadFailure (fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess (fonction)
Appelé quand la liste des moteurs a été générée avec succès.
  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure (fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.
  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess (fonction)
Appelé quand le déchargement d’un moteur a réussi.
  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure (fonction)
Appelé quand le déchargement d’un moteur a provoqué une erreur.
  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess (fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure (fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess (fonction)
Appelé quand la suppression d’un moteur a réussi.
  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure (fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.
  
### <a name="onpolicychanged-function"></a>OnPolicyChanged (fonction)
Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.
  
### <a name="onaddpolicyenginestarting-function"></a>OnAddPolicyEngineStarting (fonction)
Appelé avant la création de moteur pour décrire ou non les données de la stratégie du moteur de stratégie doivent être extraite à partir du serveur ou si elle peut être créée à partir des données mises en cache localement.

Paramètres :  
* **requiresPolicyFetch**: Décrit si les données de moteur doivent être extraites par le biais de HTTP ou si elle est chargée à partir du cache


Ce rappel facultatif peut être utilisé par une application pour être informé ou non une opération AddEngineAsync nécessitera une opération HTTP (avec son délai associé) pour terminer.
  
### <a name="observer-function"></a>Fonction d’observateur
_Pas encore documenté._
