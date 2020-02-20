---
title: class mip::ClassificationResult
description: 'Documente la classe MIP :: classificationresult du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a245cd4d9505de8adbf3cc1a2de6d2fa20369ce7
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490402"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
  
## <a name="summary"></a>Résumé
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

  
**Retourne**: chaîne JSON de toutes les détections d’informations sensibles. Si la variable n’est pas vide, doit être un format JSON valide.