---
title: mip::PolicyEngine, classe
description: Documente la classe MIP ::p olicyengine du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 114b8dedb46a0e86eb73ff1f6fa58de81927b60e
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489824"
---
# <a name="class-mippolicyengine"></a>mip::PolicyEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtient les paramètres du moteur de stratégie.
public const std :: Vector\<std :: shared_ptr\<étiquette\>\>& ListSensitivityLabels ()  |  répertorier les étiquettes de sensibilité associées au moteur de stratégie.
public const std :: Vector\<std :: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  répertorie les types de sensibilité associés au moteur de stratégie.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.
public std :: shared_ptr\<étiquette\> GetDefaultSensitivityLabel ()  |  Obtenir l’étiquette de sensibilité par défaut.
public std :: shared_ptr\<étiquette\> GetLabelById (const std :: String & ID) const  |  Obtient l’étiquette en fonction de l’ID fourni.
public std :: shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std :: String & GetPolicyDataXml () const  |  Obtient des données de stratégie XML qui décrivent les paramètres, les étiquettes et les règles associés à cette stratégie.
public const std :: String & GetSensitivityTypesDataXml () const  |  Obtient les données de types de sensibilité XML qui décrivent les types de sensibilité associés à cette stratégie.
public const std :: Vector\<std ::p air\<std :: String, std :: String\>\>& GetCustomSettings () const  |  Obtient une liste de paramètres personnalisés.
public const std :: String & GetPolicyFileId () const  |  Obtient l’ID du fichier de stratégie.
public const std :: String & GetSensitivityFileId () const  |  Obtient l’ID du fichier de sensibilité.
public bool HasClassificationRules () const  |  Obtient si la stratégie a des règles automatiques ou de recommandation.
public std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetLastPolicyFetchTime () const  |  Obtient l’heure de la dernière extraction de la stratégie.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtient les paramètres du moteur de stratégie.

  
**Retourne** : les paramètres du moteur de stratégie. 
  
**Voir aussi**: mip ::P olicyengine :: Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
répertorier les étiquettes de sensibilité associées au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes fonction)
répertorie les types de sensibilité associés au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled a la valeur false (
  
**Voir aussi**: PolicyEngine :: Settings).
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne** : URL au format de chaîne.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.

  
**Retourne** : True si l’étiquetage est obligatoire ; sinon, False.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel fonction)
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne** : étiquette de sensibilité par défaut si elle existe, nullptr si aucune étiquette par défaut n’est définie.
  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
Obtient l’étiquette en fonction de l’ID fourni.
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler fonction)
Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.

Paramètres :  
* **A**: valeur booléenne indiquant si la détection d’audit est activée ou non.



  
**Retourne** : gestionnaire de stratégie.
L’application doit conserver l’objet gestionnaire de stratégie pendant toute la durée de vie du document.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: au niveau du journal : info/Error/Warning. 


* **eventType**: description du type d’événement. 


* **EventData**: données associées à l’événement.


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml fonction)
Obtient des données de stratégie XML qui décrivent les paramètres, les étiquettes et les règles associés à cette stratégie.

  
**Retourne**: données de stratégie XML.
  
### <a name="getsensitivitytypesdataxml-function"></a>GetSensitivityTypesDataXml fonction)
Obtient les données de types de sensibilité XML qui décrivent les types de sensibilité associés à cette stratégie.

  
**Retourne**: données de type de sensibilité XML.
  
### <a name="getcustomsettings-function"></a>GetCustomSettings fonction)
Obtient une liste de paramètres personnalisés.

  
**Retourne**: un vecteur de paramètres personnalisés.
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId fonction)
Obtient l’ID du fichier de stratégie.

  
**Retourne**: une chaîne qui représente l’ID du fichier de stratégie.
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId fonction)
Obtient l’ID du fichier de sensibilité.

  
**Retourne**: une chaîne qui représente l’ID du fichier de stratégie.
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules fonction)
Obtient si la stratégie a des règles automatiques ou de recommandation.

  
**Retourne : valeur**booléenne qui indique s’il existe des règles de recommandation ou automatique dans la stratégie.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime fonction)
Obtient l’heure de la dernière extraction de la stratégie.

  
**Retourne**: l’heure de la dernière extraction de la stratégie.