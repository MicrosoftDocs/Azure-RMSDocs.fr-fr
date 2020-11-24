---
title: ComputeEngine de classe
description: 'Documente la classe computeengine :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7371c72cb10e1f08fcacaf286597f9534737996d
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567227"
---
# <a name="class-computeengine"></a>ComputeEngine de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<std::shared_ptr\<Label\> \>& ListSensitivityLabels ()  | _Pas encore documenté._
public std :: shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& contexte, const DocumentState& État)  | _Pas encore documenté._
public std :: Vector \<std::shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& Context, const documentState& DocumentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
STD public ::p air \<std::vector\<std::shared_ptr\<Action\> \> , bool \> ComputeActionsWithRemoteState (ComputeEngineContext& Context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcule les actions lors du choix entre l’État distant et l’état local.
public void NotifyCommittedActions (ComputeEngineContext& Context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
public const std :: shared_ptr \<Label\>& GetDefaultLabel () const  | _Pas encore documenté._
public const std::string& GetMoreInfoUrl() const  | _Pas encore documenté._
public const std :: String& GetUpn () const  | _Pas encore documenté._
public bool IsLabelingRequired() const  | _Pas encore documenté._
public const std :: String& GetFileId () const  | _Pas encore documenté._
public bool HasClassificationRules () const  | _Pas encore documenté._
public bool IsEnhancedClassificationEnabled () const  | _Pas encore documenté._
public std :: shared_ptr \<Label\> GetLabelById (const std :: string& ID) const  | _Pas encore documenté._
public const std :: String& GetTenantId () const  | _Pas encore documenté._
public void SetSensitivityTypesRulePackages (std :: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \> && personnalisé)  | _Pas encore documenté._
public const std :: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& GetSensitivityTypesRulePackages () const  | _Pas encore documenté._
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  | _Pas encore documenté._
uint32_t public GetOpcMetadataVersion () const  | _Pas encore documenté._
public const std :: String& GetUserObjectId () const  | _Pas encore documenté._
virtuel public ~ ComputeEngine ()  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
Pas encore documenté.

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel fonction)
Pas encore documenté.

  
### <a name="computeactions-function"></a>ComputeActions fonction)
Pas encore documenté.

  
### <a name="computeactionswithremotestate-function"></a>ComputeActionsWithRemoteState fonction)
Calcule les actions lors du choix entre l’État distant et l’état local.
L’État est sélectionné à l’aide de cette priorité. Types de protection inconnus (modèle ou ad-hoc absents de la stratégie). L’état de protection est toujours préférable à l’état non protégé. L’état du document avec l’étiquette est préférable à un autre sans. Ordre des étiquettes, la valeur la plus élevée est préférée. Horodatage de l’étiquette, préférer le document étiqueté le plus récent. DocumentState LastModifiedTime éventuellement implémenté, préférer le fichier nouvellement modifié.

Paramètres :  
* **Context**: contexte du moteur de calcul. 


* **localDocumentState**: état du document local. 


* **remoteDocumentState**: état du document distant. 


* **actionState**: état d’action de l’application.



  
**Retourne**: les méthodes retournent une paire. tout d’abord contient une liste de l’action, le second est s’il doit être appliqué sur le local, si des actions fausses doivent être appliquées sur le document distant et que l’état du document doit être utilisé.
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions fonction)
Pas encore documenté.

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel fonction)
Pas encore documenté.

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
Pas encore documenté.

  
### <a name="getupn-function"></a>GetUpn fonction)
Pas encore documenté.

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
Pas encore documenté.

  
### <a name="getfileid-function"></a>GetFileId fonction)
Pas encore documenté.

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules fonction)
Pas encore documenté.

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled fonction)
Pas encore documenté.

  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
Pas encore documenté.

  
### <a name="gettenantid-function"></a>GetTenantId fonction)
Pas encore documenté.

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages fonction)
Pas encore documenté.

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages fonction)
Pas encore documenté.

  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Pas encore documenté.

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion fonction)
Pas encore documenté.

  
### <a name="getuserobjectid-function"></a>GetUserObjectId fonction)
Pas encore documenté.

  
### <a name="computeengine-function"></a>~ ComputeEngine fonction)
Pas encore documenté.
