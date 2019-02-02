---
title: mip::PolicyEngine, classe
description: Décrit la classe mip::policyengine de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 298d9789fb46c2725401425af51a9de8b3436f53
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650967"
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
* **Un**: bool représentant si la découverte de l’audit est activé ou non



  
**Retourne**: Gestionnaire de stratégie.
Application doit conserver l’objet de gestionnaire de stratégie pour la durée de vie du document
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: du niveau de journal : Informations/avertissement/erreur 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml (fonction)
Obtient les données de stratégie XML qui décrit les paramètres, les étiquettes et les règles associées à cette stratégie.

  
**Retourne**: Données de stratégie XML
  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: Un vecteur de paramètres personnalisés