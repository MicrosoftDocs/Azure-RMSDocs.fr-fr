---
title: mip::FileEngine, classe
description: 'Documente la classe MIP:: fileengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 86437533b2451b613231d668857b1402fc9f4272
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885811"
---
# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std:: Vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  répertorie les types de sensibilité associés au moteur de stratégie.
public const std:: shared_ptr\<étiquette\> GetDefaultSensitivityLabel () const  |  Obtenir l’étiquette de sensibilité par défaut.
public std:: shared_ptr\<label\> GetLabelById (const std:: String & ID) const  |  Obtient l’étiquette en fonction de l’ID fourni.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Retourne une liste d’étiquettes de sensibilité.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public const std:: String & GetPolicyFileId () const  |  Obtient l’ID du fichier de stratégie.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté.
public std:: Chrono:: time_point\<std:: Chrono:: system_clock\> GetLastPolicyFetchTime () const  |  Obtient l’heure de la dernière extraction de la stratégie.
public void CreateFileHandlerAsync (const std:: String & inputFilePath, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<fileHandler:: observer\>& fileHandlerObserver , const std:: shared_ptr\<void\>& contexte, const std:: shared_ptr\<FileExecutionState\>& FileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public void CreateFileHandlerAsync (const std:: shared_ptr\<flux\>& InputStream, const std:: String & actualFilePath, bool isAuditDiscoveryEnabled, const std:: shared_ptr\<fileHandler:: observer \>\<\>\<& fileHandlerObserver, const std:: shared_ptr void & contexte, const std:: shared_ptr FileExecutionState & FileExecutionState) \>  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paramètres personnalisés.
public bool HasClassificationRules () const  |  Obtient si la stratégie a des règles automatiques ou de recommandation.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Retourne les paramètres du moteur.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes fonction)
répertorie les types de sensibilité associés au moteur de stratégie.

  
**Retourne**: Liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled a la valeur false (
  
**Voir aussi**: [FileEngine:: Settings](class_mip_fileengine_settings.md)).
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel fonction)
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne**: Étiquette de sensibilité par défaut si elle existe, nullptr si aucune étiquette par défaut n’est définie.
  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
Obtient l’étiquette en fonction de l’ID fourni.
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne**: URL au format de chaîne.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId fonction)
Obtient l’ID du fichier de stratégie.

  
**Retourne**: Chaîne qui représente l’ID du fichier de stratégie.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté.

  
**Retourne**: True si l’étiquetage est obligatoire, sinon false.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime fonction)
Obtient l’heure de la dernière extraction de la stratégie.

  
**Retourne**: Heure de la dernière extraction de la stratégie
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync fonction)
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **inputFilePath**: Fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **actualFilePath**: Le chemin d’accès du fichier (non temporaire) réel sera utilisé pour l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la détection d’audit est activée ou non. 


* **fileHandlerObserver**: Une classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **contexte**: Contexte client qui sera retourné de manière opaque à l’observateur.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync fonction)
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **InputStream**: Flux contenant les données du fichier. 


* **actualFilePath**: Chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. permet également d’identifier le fichier dans l’audit. 


* **isAuditDiscoveryEnabled**: indiquant si la détection d’audit est activée ou non. 


* **fileHandlerObserver**: Une classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **contexte**: Contexte client qui sera retourné de manière opaque à l’observateur.


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: description du niveau de journalisation: Info/erreur/avertissement 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement


  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: Vecteur de paramètres personnalisés
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules fonction)
Obtient si la stratégie a des règles automatiques ou de recommandation.

  
**Retourne**: Valeur booléenne qui indique s’il existe des règles de recommandation ou automatique dans la stratégie.