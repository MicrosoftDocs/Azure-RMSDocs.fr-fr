---
title: 'MIP :: ClassificationRequest, classe'
description: 'Documente la classe MIP :: classificationrequest du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 62b600a377d195c693c94dff7a0472305b53b3f2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74840307"
---
# <a name="class-mipclassificationrequest"></a>MIP :: ClassificationRequest, classe 
Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: String GetClassificationId () const  |  Obtenir l’ID de la stratégie de classification.
public std :: String GetRulePackageId () const  |  Obtient l’ID du package de règles.
  
## <a name="members"></a>Membres
  
### <a name="getclassificationid-function"></a>GetClassificationId fonction)
Obtenir l’ID de la stratégie de classification.

  
**Retourne** : ID de la stratégie de classification.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId fonction)
Obtient l’ID du package de règles.

  
**Retourne**: ID du package de règles. les classifications prédéfinies seront définies sur un GUID vide.