---
title: 'MIP:: ClassificationRequest, classe'
description: 'Documente la classe MIP:: classificationrequest du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 1966123c8a0975ea42aa119883cabd47db594bc4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884485"
---
# <a name="class-mipclassificationrequest"></a>MIP:: ClassificationRequest, classe 
Classe qui contient la demande d’un appel de classification sur l’état d’exécution.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std:: String GetClassificationId () const  |  Obtenir l’ID de la stratégie de classification.
public std:: String GetRulePackageId () const  |  Obtient l’ID du package de règles.
  
## <a name="members"></a>Membres
  
### <a name="getclassificationid-function"></a>GetClassificationId fonction)
Obtenir l’ID de la stratégie de classification.

  
**Retourne**: ID de la stratégie de classification.
  
### <a name="getrulepackageid-function"></a>GetRulePackageId fonction)
Obtient l’ID du package de règles.

  
**Retourne**: ID du package de règles. les classifications prédéfinies seront définies sur un GUID vide.