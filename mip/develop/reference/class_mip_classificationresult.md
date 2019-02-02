---
title: class mip::ClassificationResult
description: Décrit la classe mip::classificationresult de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 28b174fe65de5980fb1922cfb4c3e5cee7cab1d8
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650746"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Obtenir l’ID de la stratégie de classification.
public int GetCount() const  |  Obtenir le nombre d’instances.
public int GetConfidenceLevel() const  |  Obtenir la confiance dans le résultat.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId (fonction)
Obtenir l’ID de la stratégie de classification.

  
**Retourne**: ID de la stratégie de classification.
  
### <a name="getcount-function"></a>GetCount (fonction)
Obtenir le nombre d’instances.

  
**Retourne**: Le nombre d’instances.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel (fonction)
Obtenir la confiance dans le résultat.