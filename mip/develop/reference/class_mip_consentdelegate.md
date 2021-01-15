---
title: classe ConsentDelegate
description: 'Documente la classe consentdelegate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 62ea631159a2658432a1b62ff47c635c05f63fcf
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215491"
---
# <a name="class-consentdelegate"></a>classe ConsentDelegate 
Délégué pour les opérations relatives au consentement.
Ce délégué est implémenté par une application cliente pour savoir quand une notification de requête de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.
  
## <a name="members"></a>Membres
  
### <a name="getuserconsent-function"></a>GetUserConsent fonction)
Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.

Paramètres :  
* **url** : URL pour laquelle le Kit SDK nécessite le consentement de l’utilisateur



  
**Retourne** : énum de consentement avec la décision de l’utilisateur.
Lorsque le Kit SDK requiert le consentement de l’utilisateur avec cette méthode, l’application cliente doit présenter l’URL à l’utilisateur. Les applications clientes doivent fournir un moyen d’obtenir le consentement de l’utilisateur et retourner l’énum de consentement appropriée qui correspond à la décision de l’utilisateur.