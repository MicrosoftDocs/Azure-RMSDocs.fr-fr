---
title: class mip::ClassificationResult
description: 'Documente la classe MIP:: classificationresult du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 83856362e0d0a347f660cb60a64a82e24062c247
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885857"
---
# <a name="class-mipclassificationresult"></a>class mip::ClassificationResult 
Classe qui contient le résultat d’un appel de classification sur l’État d’exécution.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetId() const  |  Obtenir l’ID de la stratégie de classification.
public int GetCount() const  |  Obtenir le nombre d’instances.
public int GetConfidenceLevel() const  |  Obtenir la confiance dans le résultat.
public std:: String GetSensitiveInformationDetections () const  |  Obtient les détections d’informations sensibles.
  
## <a name="members"></a>Membres
  
### <a name="getid-function"></a>GetId, fonction
Obtenir l’ID de la stratégie de classification.

  
**Retourne**: ID de la stratégie de classification.
  
### <a name="getcount-function"></a>Fonction GetCount
Obtenir le nombre d’instances.

  
**Retourne**: Nombre d’instances.
  
### <a name="getconfidencelevel-function"></a>GetConfidenceLevel fonction)
Obtenir la confiance dans le résultat.
  
### <a name="getsensitiveinformationdetections-function"></a>GetSensitiveInformationDetections fonction)
Obtient les détections d’informations sensibles.

  
**Retourne**: Chaîne JSON de toutes les détections d’informations sensibles.