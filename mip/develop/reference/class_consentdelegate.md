---
title: classe ConsentDelegate
description: Informations de référence pour la classe ConsentDelegate
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 841049b1e6b369eb2f6a34d9701ed34eca028af6
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446360"
---
# <a name="class-consentdelegate"></a>classe ConsentDelegate 
Délégué pour les opérations relatives au consentement.
Ce délégué est implémenté par une application cliente pour savoir quand une notification de requête de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.
  
## <a name="members"></a>Membres
  
### <a name="consent"></a>Consent
Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.

Paramètres :  
* **url** : URL pour laquelle le Kit SDK nécessite le consentement de l’utilisateur



  
**Retourne** : énum de consentement avec la décision de l’utilisateur.
Lorsque le Kit SDK requiert le consentement de l’utilisateur avec cette méthode, l’application cliente doit présenter l’URL à l’utilisateur. Les applications clientes doivent fournir un moyen d’obtenir le consentement de l’utilisateur et retourner l’énum de consentement appropriée qui correspond à la décision de l’utilisateur.