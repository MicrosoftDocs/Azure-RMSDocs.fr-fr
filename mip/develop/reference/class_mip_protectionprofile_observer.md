---
title: mip::ProtectionProfile::Observer, classe
description: Documente la classe MIP ::p rotectionprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a9138e497655dfa939a9ac9b15d7ed228331e9e0
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560698"
---
# <a name="class-mipprotectionprofileobserver"></a>mip::ProtectionProfile::Observer, classe 
Interface qui reçoit les notifications liées à ProtectionProfile.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std :: shared_ptr\<ProtectionProfile\>& profil, const std :: shared_ptr\<void\>& contexte)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std :: Vector\<std :: String\>& engineIds, const std :: shared_ptr\<void\>& contexte)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnAddEngineSuccess (const std :: shared_ptr\<ProtectionEngine\>& moteur, const std :: shared_ptr\<void\>& contexte)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess (const std :: shared_ptr\<void\>contexte &)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **Profil**: référence au ProtectionProfile nouvellement créé.


* **context** : le même contexte que celui qui a été passé à ProtectionProfile::LoadAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionProfile :: LoadAsync, et ce même contexte sera transféré tel quel à ProtectionProfile :: observer :: OnLoadSuccess ou ProtectionProfile :: observer :: O nLoadFailure
  
### <a name="onloadfailure-function"></a>OnLoadFailure fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors du chargement 


* **context** : le même contexte que celui qui a été passé à ProtectionProfile::LoadAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionProfile :: LoadAsync, et ce même contexte sera transféré tel quel à ProtectionProfile :: observer :: OnLoadSuccess ou ProtectionProfile :: observer :: O nLoadFailure
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **Context**: le même contexte qui a été passé à ProtectionProfile :: ListEnginesAsync


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **Context**: le même contexte qui a été passé à ProtectionProfile :: ListEnginesAsync


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **engine** : moteur nouvellement créé 


* **Context**: le même contexte qui a été passé à ProtectionProfile :: AddEngineAsync


  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **Context**: le même contexte qui a été passé à ProtectionProfile :: AddEngineAsync


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **Context**: le même contexte qui a été passé à ProtectionProfile ::D eleteengineasync


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **Context**: le même contexte qui a été passé à ProtectionProfile ::D eleteengineasync

