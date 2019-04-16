---
title: classe mip::ClassificationRequest
description: Décrit la classe mip::classificationrequest de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 3fddd870b6aebb9f5209fc43160c32d87b1d7129
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573733"
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