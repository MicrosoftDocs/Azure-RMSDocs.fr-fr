---
title: class mip::ClassificationResult
description: 'Documente la classe MIP :: classificationresult du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6f4b1147ef6831ca622d095c0cada67b9f0cf023
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559393"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Obtenir l’ID de la stratégie de classification.
public std::string GetName() const  |  Obtient le nom de la stratégie de classification.
public int GetCount() const  |  Obtenir le nombre d’instances.
public int GetConfidenceLevel() const  |  Obtenir la confiance dans le résultat.
public std :: String GetSensitiveInformationDetections () const  |  Obtient les détections d’informations sensibles.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtenir l’ID de la stratégie de classification.

  
**Retourne** : ID de la stratégie de classification.
  
### <a name="getname-function"></a>Fonction GetName
Obtient le nom de la stratégie de classification.

  
**Retourne**: nom de la stratégie de classification.
  
### <a name="getcount-function"></a>Fonction GetCount
Obtenir le nombre d’instances.

  
**Retourne** : le nombre d’instances.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel fonction)
Obtenir la confiance dans le résultat.
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections fonction)
Obtient les détections d’informations sensibles.

  
**Retourne**: chaîne JSON de toutes les détections d’informations sensibles.