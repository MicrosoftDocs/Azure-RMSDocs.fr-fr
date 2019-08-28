---
title: mip::PolicyProfile::Observer, classe
description: Documente la classe MIP::p olicyprofile du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 1315f4c1289c63184b8fa029b3668b363b88b143
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054192"
---
# <a name="class-mippolicyprofileobserver"></a>mip::PolicyProfile::Observer, classe 
Interface [Observer](class_mip_policyprofile_observer.md) permettant aux clients d’obtenir les notifications des événements liés aux profils.
Toutes les erreurs héritent de [mip::Error](class_mip_error.md). Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess (const std:: shared_ptr\<PolicyProfile\>& Profile, const std::\<shared_ptr\>void & Context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std:: Vector\<std:: String\>& engineIds, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtuel void OnUnloadEngineSuccess (const std:: shared_ptr\<void\>& Context)  |  Appelé quand le déchargement d’un moteur a réussi.
public virtual void OnUnloadEngineFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public virtual void OnAddEngineSuccess (const std:: shared_ptr\<PolicyEngine\>& moteur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  Appelée avant la création du moteur pour décrire si les données de stratégie du moteur doivent être extraites du serveur ou si elles peuvent être créées à partir de données mises en cache localement.
public virtual void OnAddEngineFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtuel void OnDeleteEngineSuccess (const std:: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure (const std:: exception_ptr & erreur, const std:: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Appelé lorsque la stratégie a été modifiée pour le moteur avec l’ID donné, ou lorsque les types de sensibilité personnalisée chargés ont été modifiés.
  
## <a name="members"></a>Membres
  
### <a name="onloadsuccess-function"></a>OnLoadSuccess fonction)
Appelé quand le chargement d’un profil a réussi.

Paramètres :  
* **profile** : profil actuel utilisé pour démarrer l’opération. 


* **Context**: contexte passé à l’opération LoadAsync.


  
### <a name="onloadfailure-function"></a>OnLoadFailure fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de chargement. 


* **Context**: contexte passé à l’opération LoadAsync.


  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess fonction)
Appelé quand la liste des moteurs a été générée avec succès.

Paramètres :  
* **engineIds** : liste des ID des moteurs disponibles. 


* **Context**: contexte passé à l’opération ListEnginesAsync.


  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de génération de la liste des moteurs. 


* **Context**: contexte passé à l’opération ListEnginesAsync.


  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess fonction)
Appelé quand le déchargement d’un moteur a réussi.

Paramètres :  
* **Context**: contexte passé à l’opération UnloadEngineAsync.


  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure fonction)
Appelé quand le déchargement d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de déchargement du moteur. 


* **Context**: contexte passé à l’opération UnloadEngineAsync.


  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.

Paramètres :  
* **moteur**: moteur récemment ajouté 


* **Context**: contexte passé à l’opération AddEngineAsync


  
### <a name="onaddenginestarting-function"></a>OnAddEngineStarting fonction)
Appelée avant la création du moteur pour décrire si les données de stratégie du moteur doivent être extraites du serveur ou si elles peuvent être créées à partir de données mises en cache localement.

Paramètres :  
* **requiresPolicyFetch**: Indique si les données du moteur doivent être récupérées via HTTP ou si elles sont chargées à partir du cache


Ce rappel facultatif peut être utilisé par une application pour être informé qu’une opération AddEngineAsync nécessite ou non une opération HTTP (avec le délai associé) à effectuer.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération d’ajout du moteur. 


* **Context**: contexte passé à l’opération AddEngineAsync.


  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess fonction)
Appelé quand la suppression d’un moteur a réussi.

Paramètres :  
* **Context**: contexte passé à l’opération DeleteEngineAsync.


  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.

Paramètres :  
* **error** : erreur ayant provoqué l’échec de l’opération de suppression du moteur. 


* **Context**: contexte passé à l’opération DeleteEngineAsync.


  
### <a name="onpolicychanged-function"></a>OnPolicyChanged fonction)
Appelé lorsque la stratégie a été modifiée pour le moteur avec l’ID donné, ou lorsque les types de sensibilité personnalisée chargés ont été modifiés.

Paramètres :  
* **engineId** : moteur 


Pour charger la nouvelle stratégie, il est nécessaire de rappeler AddEngineAsync avec l’ID de moteur donné.