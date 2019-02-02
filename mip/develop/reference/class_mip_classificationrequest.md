---
title: classe mip::ClassificationRequest
description: Décrit la classe mip::classificationrequest de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: a7350961af4c2e5d63211840382ee7a0b701f1c4
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652028"
---
# <a name="class-mipclassificationrequest"></a>classe mip::ClassificationRequest 
Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetClassificationId() const  |  Obtenir l’ID de la stratégie de classification.
public std::string GetRulePackageId() const  |  Obtenir l’ID du package de règle.
  
## <a name="members"></a>Membres
  
### <a name="getclassificationid-function"></a>GetClassificationId function
Obtenir l’ID de la stratégie de classification.

  
**Retourne**: ID de la stratégie de classification.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId (fonction)
Obtenir l’ID du package de règle.

  
**Retourne**: ID du package de la règle. classifications prédéfinies seront définies à un guid vide.