---
title: mip::PolicyEngine, classe
description: Décrit la classe mip::policyengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ce8ef7df12cdc9823a62234b5dadaaacdb7fed37
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173638"
---
# <a name="class-mippolicyengine"></a>mip::PolicyEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  répertorier les étiquettes de sensibilité associées au moteur de stratégie.
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Répertorie les types de sensibilité associées au moteur de stratégie.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.
public std::shared_ptr\<Label\> GetDefaultSensitivityLabel()  |  Obtenir l’étiquette de sensibilité par défaut.
public std::shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std::string& GetPolicyDataXml() const  |  Obtient les données de stratégie XML qui décrit les paramètres, les étiquettes et les règles associées à cette stratégie.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paramètres personnalisés.
public const std::string& GetPolicyId() const  |  Obtient l’ID de stratégie.
public bool HasClassificationRules() const  |  Obtient si la stratégie a des règles automatiques ou de recommandation.
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  Obtient l’heure lors de la dernière extraction de la stratégie.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.

  
**Retourne**: Paramètres du moteur de stratégie. 
  
**Voir aussi** : [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (fonction)
répertorier les étiquettes de sensibilité associées au moteur de stratégie.

  
**Retourne**: Une liste d’étiquettes de sensibilité.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (fonction)
Répertorie les types de sensibilité associées au moteur de stratégie.

  
**Retourne**: Une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled était faux)
  
**Voir aussi**: [PolicyEngine::Settings](class_mip_policyengine_settings.md)).
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne**: Une url au format de chaîne.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.

  
**Retourne**: True si l’étiquetage est obligatoire ; sinon, false.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (fonction)
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne**: À défaut d’étiquette de sensibilité existe, nullptr si aucun jeu d’étiquette par défaut.
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler (fonction)
Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.

Paramètres :  
* **Un**: bool représentant si la découverte de l’audit est activé ou non.



  
**Retourne**: Gestionnaire de stratégie.
Application doit conserver l’objet de gestionnaire de stratégie pour la durée de vie du document.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: du niveau de journal : Informations/avertissement/erreur. 


* **eventType**: une description du type d’événement. 


* **eventData**: les données associées à l’événement.


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml (fonction)
Obtient les données de stratégie XML qui décrit les paramètres, les étiquettes et les règles associées à cette stratégie.

  
**Retourne**: Données XML de la stratégie.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: Un vecteur de paramètres personnalisés.
  
### <a name="getpolicyid-function"></a>GetPolicyId (fonction)
Obtient l’ID de stratégie.

  
**Retourne**: Chaîne qui représente l’ID de stratégie
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (fonction)
Obtient si la stratégie a des règles automatiques ou de recommandation.

  
**Retourne**: Une valeur booléenne qui indique si il automatique ni recommandation règles dans la stratégie
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (fonction)
Obtient l’heure lors de la dernière extraction de la stratégie.

  
**Retourne**: Le temps lors de la dernière extraction de la stratégie