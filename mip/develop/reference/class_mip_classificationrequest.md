---
title: 'MIP:: ClassificationRequest, classe'
description: 'Documente la classe MIP:: classificationrequest du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 39fde4fa5fb0fe6f91545c9cffa36ed976a4b8b1
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055319"
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