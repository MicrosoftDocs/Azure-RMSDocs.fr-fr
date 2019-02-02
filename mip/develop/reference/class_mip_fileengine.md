---
title: mip::FileEngine, classe
description: Décrit la classe mip::fileengine de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4bcdd08cb7ced9e2eea8fa09d9364064a8d198df
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651460"
---
# <a name="class-mipfileengine"></a>mip::FileEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  Retourne les paramètres du moteur.
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  Répertorie les types de sensibilité associées au moteur de stratégie.
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  Retourne une liste d’étiquettes de sensibilité.
public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté.
public CreateFileHandlerAsync void (const std::string & inputFilePath, isAuditDiscoveryEnabled de bool const std::string & contentIdentifier, const ContentState contentState, const std::shared_ptr\<FileHandler::Observer\>& fileHandlerObserver, const std::shared_ptr\<void\>& contexte, const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.
public CreateFileHandlerAsync void (const std::shared_ptr\<Stream\>& inputStream, const std::string & inputFilePath, const std::string & contentIdentifier, const mip::ContentState contentState, bool isAuditDiscoveryEnabled, const std::shared_ptr\<FileHandler::Observer\>& fileHandlerObserver, const std::shared_ptr\<void\>& contexte, const std::shared_ptr\< FileExecutionState\>& fileExecutionState)  |  Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  Obtient une liste de paramètres personnalisés.
  
## <a name="members"></a>Membres
  
### <a name="getsettings-function"></a>GetSettings (fonction)
Retourne les paramètres du moteur.
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes (fonction)
Répertorie les types de sensibilité associées au moteur de stratégie.

  
**Retourne**: Une liste d’étiquettes de sensibilité. vide si LoadSensitivityTypesEnabled était faux)
  
**Voir aussi**: [FileEngine::Settings](class_mip_fileengine_settings.md)).
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels (fonction)
Retourne une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl (fonction)
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne**: Une url au format de chaîne.
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired (fonction)
Vérifie si la stratégie détermine qu’un document doit être étiqueté.

  
**Retourne**: True si l’étiquetage est obligatoire ; sinon, false.
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (fonction)
Commence à créer un gestionnaire de fichiers pour le chemin de fichier donné.

Paramètres :  
* **inputFilePath**: Fichier à ouvrir. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **contentIdentifier**: un identificateur contrôlable de visu pour le contenu. exemple d’un fichier : Exemple de « C:\mip-sdk-for-cpp\files\audit.docx » [chemin] pour un message électronique : « RE : Audit design:user1@contoso.com« [sujet : expéditeur] 


* **contentState**: L’état du contenu lors de l’application interagit avec lui. 


* **isAuditDiscoveryEnabled**: indiquant si la découverte de l’audit est activé ou non. 


* **fileHandlerObserver**: Une classe qui implémente l’interface [FileHandler::Observer](class_mip_filehandler_observer.md). 


* **contexte**: Contexte de client qui sera transmis de manière opaque à l’Observateur.


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync (fonction)
Commence à créer un gestionnaire de fichiers pour le flux de fichier donné.

Paramètres :  
* **inputStream**: Un flux contenant les données de fichier. 


* **inputFilePath**: Chemin du fichier. Le chemin doit inclure le nom de fichier et l’extension de nom de fichier éventuelle. 


* **contentIdentifier**: un identificateur contrôlable de visu pour le contenu. exemple d’un fichier : Exemple de « C:\mip-sdk-for-cpp\files\audit.docx » [chemin] pour un message électronique : « RE : Audit design:user1@contoso.com« [sujet : expéditeur] 


* **contentState**: L’état du contenu lors de l’application interagit avec lui. 


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