---
title: class mip::ClassificationResult
description: Décrit la classe mip::classificationresult de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: ecdd8b357aa1e266e92d8a5b4d03408488f3f332
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258485"
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
