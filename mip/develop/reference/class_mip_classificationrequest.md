---
title: classe mip::ClassificationRequest
description: Décrit la classe mip::classificationrequest de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 61846ef3b8273169e9cf38eaa173eac3ba18dae6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330514"
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
