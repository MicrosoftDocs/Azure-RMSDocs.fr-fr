---
title: ClassificationRequest de classe
description: 'Documente la classe classificationrequest :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 0d4b8d3ed5e12698c0044975516b017d1c9376b0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763542"
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