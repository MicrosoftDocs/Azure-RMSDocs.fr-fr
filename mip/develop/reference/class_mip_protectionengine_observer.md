---
title: class mip::ProtectionEngine::Observer
description: Documente la classe MIP ::p rotectionengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 688bc59b992e885b2b9724111c19f69f860badd9
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489671"
---
# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
Interface qui reçoit les notifications liées à ProtectionEngine.
Cette interface doit être implémentée par les applications utilisant le SDK de protection
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess (const std :: Vector\<std :: shared_ptr\<TemplateDescriptor\>\>& templateDescriptors, const std :: shared_ptr\<void\>& contexte)  |  Appelé lorsque les modèles ont été récupérés.
public virtual void OnGetTemplatesFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lorsque la récupération de modèles a généré une erreur.
public virtual void OnGetRightsForLabelIdSuccess (const std :: shared_ptr\<std :: Vector\<std :: String\>\>& droits, const std :: shared_ptr\<void\>& contexte)  |  Appelé en cas de récupération réussie des droits.
public virtual void OnGetRightsForLabelIdFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.
public virtual void OnLoadUserCertSuccess (const std :: shared_ptr\<void\>& Context)  |  Appelé lorsque le certificat de l’utilisateur a été chargé avec succès.
public virtual void OnLoadUserCertFailure (const std :: exception_ptr & erreur, const std :: shared_ptr\<void\>contexte &)  |  Appelé en cas d’échec du chargement du certificat de l’utilisateur.
  
## <a name="members"></a>Membres
  
### <a name="ongettemplatessuccess-function"></a>OnGetTemplatesSuccess fonction)
Appelé lorsque les modèles ont été récupérés.

Paramètres :  
* **templateDescriptors**: référence à la liste des descripteurs de modèles 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetTemplatesAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetTemplatesAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetTemplatesSuccess ou ProtectionEngine :: O bserver::OnGetTemplatesFailure
  
### <a name="ongettemplatesfailure-function"></a>OnGetTemplatesFailure fonction)
Appelé lorsque la récupération de modèles a généré une erreur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des modèles 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetTemplatesAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetTemplatesAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetTemplatesSuccess ou ProtectionEngine :: O bserver::OnGetTemplatesFailure
  
### <a name="ongetrightsforlabelidsuccess-function"></a>OnGetRightsForLabelIdSuccess fonction)
Appelé en cas de récupération réussie des droits.

Paramètres :  
* **rights** : référence à la liste des droits récupérés 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetRightsForLabelIdAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure
  
### <a name="ongetrightsforlabelidfailure-function"></a>OnGetRightsForLabelIdFailure fonction)
Appelé lors de la récupération des droits pour un ID d’étiquette pour l’utilisateur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des droits 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: GetRightsForLabelIdAsync


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: GetRightsForLabelIdAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnGetRightsForLabelIdSuccess ou ProtectionEngine :: observer :: OnGetRightsForLabelIdFailure
  
### <a name="onloadusercertsuccess-function"></a>OnLoadUserCertSuccess fonction)
Appelé lorsque le certificat de l’utilisateur a été chargé avec succès.

Paramètres :  
* **Context**: le même contexte qui a été passé à ProtectionEngine :: LoadUserCert


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: LoadUserCertAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnLoadUserCertSuccess ou ProtectionEngine :: O bserver::OnLoadUserCertFailure
  
### <a name="onloadusercertfailure-function"></a>OnLoadUserCertFailure fonction)
Appelé en cas d’échec du chargement du certificat de l’utilisateur.

Paramètres :  
* **erreur**: erreur qui s’est produite lors de la récupération des droits 


* **Context**: le même contexte qui a été passé à ProtectionEngine :: LoadUserCert


Une application peut passer n’importe quel type de contexte (par exemple, std ::p romise, std :: Function) à ProtectionEngine :: LoadUserCertAsync et ce même contexte sera transféré en l’État à ProtectionEngine :: observer :: OnLoadUserCertSuccess ou ProtectionEngine :: O bserver::OnLoadUserCertFailure