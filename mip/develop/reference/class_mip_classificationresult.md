---
title: mip ClassificationResult, classe
description: Informations de référence pour la classe mip ClassificationResult
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: ea312330c656b6daefbc1bcba690f53ebfbf419f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446292"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
 public std::string GetId() const  |  Obtenir l’ID de la stratégie de classification.
 public int GetCount() const  |  Obtenir le nombre d’instances.
 public int GetConfidenceLevel() const  |  Obtenir la confiance dans le résultat.
  
## <a name="members"></a>Membres
  
### <a name="getid"></a>GetId
Obtenir l’ID de la stratégie de classification.

  
**Retourne** : ID de la stratégie de classification.
  
### <a name="getcount"></a>GetCount
Obtenir le nombre d’instances.

  
**Retourne** : le nombre d’instances.
  
### <a name="getconfidencelevel"></a>GetConfidenceLevel
Obtenir la confiance dans le résultat.