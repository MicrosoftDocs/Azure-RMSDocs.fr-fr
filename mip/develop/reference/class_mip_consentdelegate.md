---
title: 'MIP :: ConsentDelegate, classe'
description: 'Documente la classe MIP :: consentdelegate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 479ce747334de7e8e73efb84738b6793584c55ab
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74840239"
---
# <a name="class-mipconsentdelegate"></a>MIP :: ConsentDelegate, classe 
Délégué pour les opérations relatives au consentement.
Ce délégué est implémenté par une application cliente pour savoir quand une notification de requête de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Table des matières
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