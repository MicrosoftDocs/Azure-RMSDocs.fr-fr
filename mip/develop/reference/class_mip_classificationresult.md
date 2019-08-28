---
title: class mip::ClassificationResult
description: 'Documente la classe MIP:: classificationresult du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2744e2d5fe188667ff7c1c93a7f98719f200aecd
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056227"
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