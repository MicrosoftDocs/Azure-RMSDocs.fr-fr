---
title: classe mip::ConsentDelegate
description: Décrit la classe mip::consentdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 3eed60a06d2dda22f3ed037b1f30e3c5a0f2c699
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651858"
---
# <a name="class-mipconsentdelegate"></a>classe mip::ConsentDelegate 
Délégué pour les opérations relatives au consentement.
Ce délégué est implémenté par une application cliente pour savoir quand une notification de requête de consentement doit être présentée à l’utilisateur.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.
  
## <a name="members"></a>Membres
  
### <a name="getuserconsent-function"></a>GetUserConsent (fonction)
Appelé lorsque le Kit SDK nécessite le consentement de l’utilisateur pour se connecter à un point de terminaison de service.

Paramètres :  
* **URL**: L’URL pour laquelle le Kit de développement logiciel nécessite le consentement de l’utilisateur



  
**Retourne**: Un enum consentement à la décision de l’utilisateur.
Lorsque le Kit SDK requiert le consentement de l’utilisateur avec cette méthode, l’application cliente doit présenter l’URL à l’utilisateur. Les applications clientes doivent fournir un moyen d’obtenir le consentement de l’utilisateur et retourner l’énum de consentement appropriée qui correspond à la décision de l’utilisateur.