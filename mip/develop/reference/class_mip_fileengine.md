---
title: mip::FileEngine, classe
description: 'Documente la classe MIP :: fileengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 60be23f1cda4403936ba1e334ae437f6d82d3e20
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490062"
---
# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std :: Vector\<std :: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  répertorie les types de sensibilité associés au moteur de stratégie.
public const std :: shared_ptr\<étiquette\> GetDefaultSensitivityLabel () const  |  Obtenir l’étiquette de sensibilité par défaut.
public std :: shared_ptr\<étiquette\> GetLabelById (const std :: String & ID) const  |  Obtient l’étiquette en fonction de l’ID fourni.
public const std :: Vector\<std :: shared_ptr\<étiquette\>\>& ListSensitivityLabels ()  |  Retourne une liste d’étiquettes de sensibilité.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public const std :: String & GetPolicyFileId () const  |  Obtient l’ID du fichier de stratégie.
public const std :: String & GetSensitivityFileId () const  |  Obtient l’ID du fichier de sensibilité.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté.
public std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetLastPolicyFetchTime () const  |  Obtient l’heure de la dernière extraction de la stratégie.
public const std :: String & GetPolicyDataXml () const  |  Obtient des données de stratégie XML qui décrivent les paramètres, les étiquettes et les règles associés à cette stratégie.
public std :: shared_ptr\<AsyncControl\> CreateFileHandlerAsync (const std :: String & inputFilePath, const std :: String & actualFilePath, bool isAuditDiscoveryEnabled, const std :: shared_ptr\<FileHandler :: observer\>& fileHandlerObserver, const std :: shared_ptr\<void\>& contexte, const std :: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public std :: shared_ptr\<AsyncControl\> CreateFileHandlerAsync (const std :: shared_ptr\<flux\>& inputStream, const std :: String & actualFilePath, bool isAuditDiscoveryEnabled, const std :: shared_ptr\<FileHandler :: observer\>& fileHandlerObserver, const std :: shared_ptr\<void\>& contexte, const std :: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetCustomSettings () const  |  Obtient une liste de paramètres personnalisés.
public bool HasClassificationRules () const  |  Obtient si la stratégie a des règles automatiques ou de recommandation.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres du moteur.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes fonction)
répertorie les types de sensibilité associés au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled a la valeur false (
  
**Voir aussi**: FileEngine :: Settings).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel fonction)
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne** : étiquette de sensibilité par défaut si elle existe, nullptr si aucune étiquette par défaut n’est définie.
  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
Obtient l’étiquette en fonction de l’ID fourni.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne** : URL au format de chaîne.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId fonction)
Obtient l’ID du fichier de stratégie.

  
**Retourne**: une chaîne qui représente l’ID du fichier de stratégie.
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId fonction)
Obtient l’ID du fichier de sensibilité.

  
**Retourne**: une chaîne qui représente l’ID du fichier de stratégie.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté.

  
**Retourne** : True si l’étiquetage est obligatoire ; sinon, False.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime fonction)
Obtient l’heure de la dernière extraction de la stratégie.

  
**Retourne**: l’heure de la dernière extraction de la stratégie.
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml fonction)
Obtient des données de stratégie XML qui décrivent les paramètres, les étiquettes et les règles associés à cette stratégie.

  
**Retourne**: données de stratégie XML.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync fonction)
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **inputFilePath**: fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **actualFilePath**: le chemin d’accès du fichier réel (non temporaire) sera utilisé pour l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la détection d’audit est activée ou non. 


* **fileHandlerObserver**: classe implémentant l’interface fileHandler :: observer. 


* **context** : contexte client qui est repassé de façon opaque à l’observateur. 



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync fonction)
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **inputStream** : flux contenant les données de fichier. 


* **actualFilePath**: chemin d’accès au fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. permet également d’identifier le fichier dans l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la détection d’audit est activée ou non. 


* **fileHandlerObserver**: classe implémentant l’interface fileHandler :: observer. 


* **context** : contexte client qui est repassé de façon opaque à l’observateur. 



  
**Retourne**: objet de contrôle asynchrone.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **level** : description du niveau de journalisation : Info/Erreur/Avertissement 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: un vecteur de paramètres personnalisés
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules fonction)
Obtient si la stratégie a des règles automatiques ou de recommandation.

  
**Retourne : valeur**booléenne qui indique s’il existe des règles de recommandation ou automatique dans la stratégie.