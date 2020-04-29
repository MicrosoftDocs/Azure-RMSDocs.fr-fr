---
title: ClassificationResult de classe
description: 'Documente la classe classificationresult :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: b87db224bdd7a571c22de9e382ff9faf3ce656b8
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763528"
---
# <a name="class-classificationresult"></a>ClassificationResult de classe 
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