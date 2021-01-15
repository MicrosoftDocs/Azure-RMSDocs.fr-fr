---
title: 'classe PolicyProfile :: observer'
description: 'Documente la classe policyprofile :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 978597bcc90386a53ca35271cb862b9f0f0465a7
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215066"
---
# <a name="class-policyprofileobserver"></a>classe PolicyProfile :: observer 
Interface Observer permettant aux clients d’obtenir les notifications des événements liés aux profils.
Toutes les erreurs héritent de mip::Error. Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr\<PolicyProfile\>& profile, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std :: Vector \<std::string\>& engineIds, const std :: shared_ptr \<void\>& Context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtual void OnUnloadEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand le déchargement d’un moteur a réussi.
public virtual void OnUnloadEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public virtual void OnAddEngineSuccess(const std::shared_ptr\<PolicyEngine\>& engine, const std::shared_ptr\<void\>& context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineStarting (bool requiresPolicyFetch)  |  Appelée avant la création du moteur pour décrire si les données de stratégie du moteur doivent être extraites du serveur ou si elles peuvent être créées à partir de données mises en cache localement.
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
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
* **requiresPolicyFetch**: indique si les données du moteur doivent être récupérées via http ou si elles sont chargées à partir du cache


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