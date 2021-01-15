---
title: ComputeEngine de classe
description: 'Documente la classe computeengine :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd3f287022b567ba2531108f9f24f614a3bb6b01
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211904"
---
# <a name="class-computeengine"></a>ComputeEngine de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: Vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std :: Vector \<std::string\>& contentFormats)  | _Pas encore documenté._
public std :: shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& contexte, const DocumentState& État)  | _Pas encore documenté._
public std :: Vector \<std::shared_ptr\<Action\> \> ComputeActions (ComputeEngineContext& Context, const documentState& DocumentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
STD public ::p air \<std::vector\<std::shared_ptr\<Action\> \> , bool \> ComputeActionsWithRemoteState (ComputeEngineContext& Context, const DocumentState& localDocumentState, const DocumentState& remoteDocumentState, const ApplicationActionState& actionState)  |  Calcule les actions lors du choix entre l’État distant et l’état local.
public void NotifyCommittedActions (ComputeEngineContext& Context, const DocumentState& documentState, const ApplicationActionState& actionState)  | _Pas encore documenté._
public const std :: shared_ptr \<Label\> GetDefaultLabel (const std :: string& contentFormat) const  | _Pas encore documenté._
public const std::string& GetMoreInfoUrl() const  | _Pas encore documenté._
public const std :: String& GetUpn () const  | _Pas encore documenté._
public bool IsLabelingRequired (const std :: String& contentFormat) const  | _Pas encore documenté._
public const std :: String& GetFileId () const  | _Pas encore documenté._
public bool HasClassificationRules (const std :: Vector \<std::string\>& contentFormats) const  | _Pas encore documenté._
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
_Pas encore documenté._

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel fonction)
_Pas encore documenté._

  
### <a name="computeactions-function"></a>ComputeActions fonction)
_Pas encore documenté._

  
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
_Pas encore documenté._

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel fonction)
_Pas encore documenté._

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
_Pas encore documenté._

  
### <a name="getupn-function"></a>GetUpn fonction)
_Pas encore documenté._

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
_Pas encore documenté._

  
### <a name="getfileid-function"></a>GetFileId fonction)
_Pas encore documenté._

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules fonction)
_Pas encore documenté._

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled fonction)
_Pas encore documenté._

  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
_Pas encore documenté._

  
### <a name="gettenantid-function"></a>GetTenantId fonction)
_Pas encore documenté._

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages fonction)
_Pas encore documenté._

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages fonction)
_Pas encore documenté._

  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
_Pas encore documenté._

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion fonction)
_Pas encore documenté._

  
### <a name="getuserobjectid-function"></a>GetUserObjectId fonction)
_Pas encore documenté._

  
### <a name="computeengine-function"></a>~ ComputeEngine fonction)
_Pas encore documenté._
