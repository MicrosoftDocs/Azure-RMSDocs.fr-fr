---
title: 'classe FileProfile :: observer'
description: 'Documente la classe fileprofile :: observer du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 4dd3ff426e92fdd28cac211eb6953b8d30eb5ae5
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762749"
---
# <a name="class-fileprofileobserver"></a>classe FileProfile :: observer 
Interface Observer permettant aux clients d’obtenir les notifications des événements liés aux profils.
Toutes les erreurs héritent de mip::Error. Le client ne doit pas rappeler le moteur sur le thread qui appelle l’observateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _Pas encore documenté._
public virtual void OnLoadSuccess (const std :: shared_ptr\<MIP :: FileProfile\>& Profile, const std ::\<shared_ptr\> void& Context)  |  Appelé quand le chargement d’un profil a réussi.
public virtual void OnLoadFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand le chargement d’un profil a provoqué une erreur.
public virtual void OnListEnginesSuccess (const std :: Vector\<std :: String\>& engineIds, const std :: shared_ptr\<void\>& Context)  |  Appelé quand la liste des moteurs a été générée avec succès.
public virtual void OnListEnginesFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand la génération de la liste de moteurs a provoqué une erreur.
public virtuel void OnUnloadEngineSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé quand le déchargement d’un moteur a réussi.
public virtual void OnUnloadEngineFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand le déchargement d’un moteur a provoqué une erreur.
public virtual void OnAddEngineSuccess (const std :: shared_ptr\<MIP :: FileEngine\>& moteur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a réussi.
public virtual void OnAddEngineFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
public virtuel void OnDeleteEngineSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a réussi.
public virtual void OnDeleteEngineFailure (const std :: exception_ptr& erreur, const std :: shared_ptr\<void\>& Context)  |  Appelé quand la suppression d’un moteur a provoqué une erreur.
public virtual void OnPolicyChanged(const std::string& engineId)  |  Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.
public virtual void OnAddPolicyEngineStarting (bool requiresPolicyFetch)  |  Appelée avant la création du moteur pour décrire si les données de stratégie du moteur de stratégie doivent être extraites du serveur ou si elles peuvent être créées à partir de données mises en cache localement.
protected Observer()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="observer-function"></a>~ Fonction observer
_Pas encore documenté._

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess fonction)
Appelé quand le chargement d’un profil a réussi.
  
### <a name="onloadfailure-function"></a>OnLoadFailure fonction)
Appelé quand le chargement d’un profil a provoqué une erreur.
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess fonction)
Appelé quand la liste des moteurs a été générée avec succès.
  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure fonction)
Appelé quand la génération de la liste de moteurs a provoqué une erreur.
  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess fonction)
Appelé quand le déchargement d’un moteur a réussi.
  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure fonction)
Appelé quand le déchargement d’un moteur a provoqué une erreur.
  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess fonction)
Appelé quand l’ajout d’un nouveau moteur a réussi.
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure fonction)
Appelé quand l’ajout d’un nouveau moteur a provoqué une erreur.
  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess fonction)
Appelé quand la suppression d’un moteur a réussi.
  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure fonction)
Appelé quand la suppression d’un moteur a provoqué une erreur.
  
### <a name="onpolicychanged-function"></a>OnPolicyChanged fonction)
Appelé quand la stratégie a été changée pour le moteur avec l’ID spécifié.
  
### <a name="onaddpolicyenginestarting-function"></a>OnAddPolicyEngineStarting fonction)
Appelée avant la création du moteur pour décrire si les données de stratégie du moteur de stratégie doivent être extraites du serveur ou si elles peuvent être créées à partir de données mises en cache localement.

Paramètres :  
* **requiresPolicyFetch**: indique si les données du moteur doivent être récupérées via http ou si elles sont chargées à partir du cache


Ce rappel facultatif peut être utilisé par une application pour être informé qu’une opération AddEngineAsync nécessite ou non une opération HTTP (avec le délai associé) à effectuer.
  
### <a name="observer-function"></a>Fonction observer
_Pas encore documenté._
