---
title: mip::LabelingOptions, classe
description: Décrit la classe mip::labelingoptions de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 0ef91bb6b27776ec4774be68496bc4eb9240261b
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251254"
---
# <a name="class-miplabelingoptions"></a>mip::LabelingOptions, classe 
Interface pour la configuration des options d’étiquetage des méthodes SetLabel/DeleteLabel.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public LabelingOptions(AssignmentMethod method, ActionSource actionSource)  | _Pas encore documenté._
public AssignmentMethod GetAssignmentMethod() const  | _Pas encore documenté._
public ActionSource GetActionSource() const  | _Pas encore documenté._
public bool IsDowngradeJustified() const  | _Pas encore documenté._
public const std::string& GetJustificationMessage() const  | _Pas encore documenté._
public const std::vector\<std::pair\<std::string, std::string\>\>& GetExtendedProperties() const  | _Pas encore documenté._
public void SetDowngradeJustification(bool isDowngradeJustified, const std::string& justificationMessage)  | _Pas encore documenté._
public SetExtendedProperties void (const std::vector\<std::pair\<std::string, std::string\>\>& extendedProperties)  | _Pas encore documenté._
  
## <a name="members"></a>Membres
  
### <a name="labelingoptions-function"></a>LabelingOptions (fonction)
_Pas encore documenté._

  
### <a name="getassignmentmethod-function"></a>GetAssignmentMethod (fonction)
_Pas encore documenté._

  
### <a name="getactionsource-function"></a>GetActionSource (fonction)
_Pas encore documenté._

  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified (fonction)
_Pas encore documenté._

  
### <a name="getjustificationmessage-function"></a>GetJustificationMessage (fonction)
_Pas encore documenté._

  
### <a name="getextendedproperties-function"></a>GetExtendedProperties (fonction)
_Pas encore documenté._

  
### <a name="setdowngradejustification-function"></a>SetDowngradeJustification (fonction)
_Pas encore documenté._

  
### <a name="setextendedproperties-function"></a>SetExtendedProperties (fonction)
_Pas encore documenté._
