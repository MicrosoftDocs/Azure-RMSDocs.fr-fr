---
title: PolicyEngine de classe
description: 'Documente la classe policyengine :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 10f913029af2be9f0430c55b8296269eb04beb7b
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213434"
---
# <a name="class-policyengine"></a>PolicyEngine de classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Obtenir les Settings du moteur de stratégie.
public const std :: Vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std :: Vector \<std::string\>& contentFormats)  |  Répertoriez les étiquettes de sensibilité associées au moteur de stratégie en fonction du contentFormats fourni.
public const std :: Vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes () const  |  répertorie les types de sensibilité associés au moteur de stratégie.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public bool IsLabelingRequired (const std :: String& contentFormat) const  |  Vérifie si la stratégie indique qu’un contenu doit être étiqueté ou non selon le contentFormat fourni.
public const std :: shared_ptr \<Label\> GetDefaultSensitivityLabel (const std :: string& contentFormat) const  |  Obtient l’étiquette de sensibilité par défaut en fonction du contentFormat fourni.
public std :: shared_ptr \<Label\> GetLabelById (const std :: string& ID) const  |  Obtient l’étiquette en fonction de l’ID fourni.
public std :: shared_ptr \<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled, bool isGetSensitivityLabelAuditDiscoveryEnabled)  |  Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std :: String& GetTenantId () const  |  Obtient l’ID de locataire associé au moteur.
public const std :: String& GetPolicyDataXml () const  |  Obtient des données de stratégie XML qui décrivent les paramètres, les étiquettes et les règles associés à cette stratégie.
public const std :: String& GetSensitivityTypesDataXml () const  |  Obtient les données de types de sensibilité XML qui décrivent les types de sensibilité associés à cette stratégie.
public const std :: Vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  Obtient une liste de paramètres personnalisés.
public const std :: String& GetPolicyFileId () const  |  Obtient l’ID du fichier de stratégie.
public const std :: String& GetSensitivityFileId () const  |  Obtient l’ID du fichier de sensibilité.
public bool HasClassificationRules (const std :: Vector \<std::string\>& contentFormats) const  |  Obtient une valeur si la stratégie a des règles automatiques ou de recommandation selon le contentFormats fourni.
public std :: Chrono :: time_point \<std::chrono::system_clock\> GetLastPolicyFetchTime () const  |  Obtient l’heure de la dernière extraction de la stratégie.
uint32_t public GetWxpMetadataVersion () const  |  Obtient la version de métadonnées WXP (Word, Excel, PowerPoint) recommandée, actuellement 0 pour l’ancienne version 1 pour la version activée pour la co-création.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings fonction)
Obtenir les Settings du moteur de stratégie.

  
**Retourne** : les paramètres du moteur de stratégie. 
  
**Voir aussi**: mip ::P olicyengine :: Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels fonction)
Répertoriez les étiquettes de sensibilité associées au moteur de stratégie en fonction du contentFormats fourni.

Paramètres :  
* **contentFormats**: contentFormats Vector de formats pour filtrer les étiquettes de sensibilité par, par exemple « file », « email », etc. Définissez contentFormats sur un vecteur vide pour filtrer les étiquettes de sensibilité en respectant les formats par défaut.



  
**Retourne** : une liste d’étiquettes de sensibilité.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes fonction)
répertorie les types de sensibilité associés au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled a la valeur false (
  
**Voir aussi**: PolicyEngine :: Settings).
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne** : URL au format de chaîne.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired fonction)
Vérifie si la stratégie indique qu’un contenu doit être étiqueté ou non selon le contentFormat fourni.

Paramètres :  
* **contentFormat**: format à filtrer pour déterminer si une étiquette est obligatoire-exemple : « fichier », « e-mail », etc. Définissez contentFormat sur une chaîne vide pour déterminer si l’étiquetage est requis pour le format par défaut.



  
**Retourne** : True si l’étiquetage est obligatoire ; sinon, False.
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel fonction)
Obtient l’étiquette de sensibilité par défaut en fonction du contentFormat fourni.

Paramètres :  
* **contentFormat**: format à filtrer par lors de la récupération de l’étiquette de sensibilité par défaut-exemple : « fichier », « e-mail », etc. Affectez une chaîne vide à contentFormat pour récupérer l’étiquette de sensibilité par défaut pour le format par défaut.



  
**Retourne** : étiquette de sensibilité par défaut si elle existe, nullptr si aucune étiquette par défaut n’est définie.
  
### <a name="getlabelbyid-function"></a>GetLabelById fonction)
Obtient l’étiquette en fonction de l’ID fourni.

Paramètres :  
* **ID**: identificateur de l’étiquette.



  
**Retourne**: étiquette
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler fonction)
Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.

Paramètres :  
* **isAuditDiscoveryEnabled**: indique si la détection d’audit est activée ou non.



  
**Retourne** : gestionnaire de stratégie.
L’application doit conserver l’objet gestionnaire de stratégie pendant toute la durée de vie du document.
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent fonction)
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **niveau**: au niveau du journal : info/Error/Warning. 


* **eventType**: description du type d’événement. 


* **EventData**: données associées à l’événement.


  
### <a name="gettenantid-function"></a>GetTenantId fonction)
Obtient l’ID de locataire associé au moteur.

  
**Retourne**: ID de locataire
  
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
Obtient une valeur si la stratégie a des règles automatiques ou de recommandation selon le contentFormats fourni.

Paramètres :  
* **contentFormat**: vecteur de formats à prendre en compte pour déterminer si une règle est définie pour tout format fourni. La définition de contentFormats sur un vecteur vide indique que le contentFormats fourni est un format par défaut.



  
**Retourne : valeur** booléenne qui indique s’il existe des règles de recommandation ou automatique dans la stratégie.
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime fonction)
Obtient l’heure de la dernière extraction de la stratégie.

  
**Retourne**: l’heure de la dernière extraction de la stratégie.
  
### <a name="getwxpmetadataversion-function"></a>GetWxpMetadataVersion fonction)
Obtient la version de métadonnées WXP (Word, Excel, PowerPoint) recommandée, actuellement 0 pour l’ancienne version 1 pour la version activée pour la co-création.

  
**Retourne**: Uint32_t int indecating la version des métadonnées que le locataire prend en charge pour les fichiers WXP.