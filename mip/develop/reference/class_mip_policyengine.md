---
title: mip PolicyEngine, classe
description: Informations de référence pour la classe mip PolicyEngine
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 57dd325e9c00a3cb2a4056f7ef0b522efef5d0c4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446037"
---
# <a name="class-mippolicyengine"></a>mip::PolicyEngine, classe 
Cette classe fournit une interface pour toutes les fonctions de moteur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  répertorier les étiquettes de sensibilité associées au moteur de stratégie.
 public const std::string& GetMoreInfoUrl() const  |  Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.
 public bool IsLabelingRequired() const  |  Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  Obtenir l’étiquette de sensibilité par défaut.
public std::shared_ptr<PolicyHandler> CreatePolicyHandler(const std::string& contentIdentifier)  |  Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  Consigne un événement spécifique à l’application dans le pipeline d’audit.
  
## <a name="members"></a>Membres
  
### <a name="settings"></a>Paramètres
Obtenir les [Settings](class_mip_policyengine_settings.md) du moteur de stratégie.

  
**Retourne** : les paramètres du moteur de stratégie. 
  
**Voir aussi** : [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Étiquette
répertorier les étiquettes de sensibilité associées au moteur de stratégie.

  
**Retourne** : une liste d’étiquettes de sensibilité.
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
Fournir une URL pour la recherche d’autres informations sur la stratégie/les étiquettes.

  
**Retourne** : URL au format de chaîne.
  
### <a name="islabelingrequired"></a>IsLabelingRequired
Vérifie si la stratégie détermine qu’un document doit être étiqueté ou non.

  
**Retourne** : True si l’étiquetage est obligatoire ; sinon, False.
  
### <a name="label"></a>Étiquette
Obtenir l’étiquette de sensibilité par défaut.

  
**Retourne** : étiquette de sensibilité par défaut si elle existe, nullptr si aucune étiquette par défaut n’est définie.
  
### <a name="policyhandler"></a>PolicyHandler
Créer un gestionnaire de stratégie pour exécuter des fonctions liées à la stratégie sur l’état d’exécution d’un fichier.

Paramètres :  
* **contentIdentifier** : identificateur explicite pour le contenu. Exemple pour un fichier : « C:\mip-sdk-for-cpp\files\audit.docx » [chemin], exemple pour un e-mail : « RE : Audit design:user1@contoso.com » [objet : expéditeur]



  
**Retourne** : gestionnaire de stratégie.
  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
Consigne un événement spécifique à l’application dans le pipeline d’audit.

Paramètres :  
* **description** : du niveau de journalisation : Info/Erreur/Avertissement 


* **eventType** : description du type d’événement 


* **eventData** : données associées à l’événement

