---
title: ClassificationRequest de classe
description: 'Documente la classe classificationrequest :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2e509950bad2d219843c2d45ebd3922a19bef7f4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567234"
---
# <a name="class-classificationrequest"></a>ClassificationRequest de classe 
Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
  
## <a name="summary"></a>Résumé
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