---
title: mip::FileEngine, classe
description: Décrit la classe mip::fileengine de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 15ce90a80430f50854580f6c7a2993d92db0a744
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573987"
---
# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Répertorie les types de sensibilité associées au moteur de stratégie.
public const std::shared_ptr\<Label\> GetDefaultSensitivityLabel() const  |  Obtenir l’étiquette de sensibilité par défaut.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Retourne une liste d’étiquettes de sensibilité.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public const std::string& GetPolicyId() const  |  Obtient l’ID de stratégie.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté.
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  Obtient l’heure lors de la dernière extraction de la stratégie.
public CreateFileHandlerAsync void (const std::string & inputFilePath, const std::string & actualFilePath, bool isAuditDiscoveryEnabled, const std::shared_ptr\<FileHandler::Observer\>& fileHandlerObserver const std::shared_ptr\<void\>& contexte, const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public CreateFileHandlerAsync void (const std::shared_ptr\<Stream\>& inputStream, const std::string & actualFilePath, bool isAuditDiscoveryEnabled, const std::shared_ptr\<FileHandler::Observer \>& fileHandlerObserver, const std::shared_ptr\<void\>& contexte, const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paramètres personnalisés.
public bool HasClassificationRules() const  |  Obtient si la stratégie a des règles automatiques ou de recommandation.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Retourne les paramètres du moteur.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (fonction)
Répertorie les types de sensibilité associées au moteur de stratégie.

  
**Retourne**: Une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled était faux)
  
**Voir aussi**: [FileEngine::Settings](class_mip_fileengine_settings.md)).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel (fonction)
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne**: À défaut d’étiquette de sensibilité existe, nullptr si aucun jeu d’étiquette par défaut.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (fonction)
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne**: Une url au format de chaîne.
  
### <a name="getpolicyid-function"></a>GetPolicyId (fonction)
Obtient l’ID de stratégie.

  
**Retourne**: Chaîne qui représente l’ID de stratégie
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté.

  
**Retourne**: True si l’étiquetage est obligatoire ; sinon, false.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime (fonction)
Obtient l’heure lors de la dernière extraction de la stratégie.

  
**Retourne**: Le temps lors de la dernière extraction de la stratégie
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (fonction)
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **inputFilePath**: Fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **actualFilePath**: Le chemin d’accès de fichier (non temporaires) réelle, sera utilisé pour l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la découverte de l’audit est activé ou non. 


* **fileHandlerObserver**: Une classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **contexte**: Contexte de client qui sera transmis de manière opaque à l’Observateur.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (fonction)
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **inputStream**: Un flux contenant les données de fichier. 


* **actualFilePath**: Chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. utilisera également pour identifier le fichier dans l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la découverte de l’audit est activé ou non. 


* **fileHandlerObserver**: Une classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **contexte**: Contexte de client qui sera transmis de manière opaque à l’Observateur.


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent (fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: une description du niveau de journal : Informations/avertissement/erreur 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement


  
### <a name="getcustomsettings-function"></a>GetCustomSettings (fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: Un vecteur de paramètres personnalisés
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules (fonction)
Obtient si la stratégie a des règles automatiques ou de recommandation.

  
**Retourne**: Une valeur booléenne qui indique si il automatique ni recommandation règles dans la stratégie