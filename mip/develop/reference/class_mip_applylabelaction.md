---
title: ApplyLabelAction de classe
description: 'Documente la classe applylabelaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: df208a53f6cd6ec3806e91c28901a3005b801742
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763700"
---
# <a name="class-applylabelaction"></a>ApplyLabelAction de classe 
Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: shared_ptr\<étiquette\>& getLabel () const  |  Obtient l’étiquette requise.
public const std :: Vector\<std :: String\>& GetClassificationIds () const  |  Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’étiquette requise.

  
**Retourne**: l’étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds fonction)
Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.

  
**Retourne**: const std :: Vector<std :: String>& une liste des ID de classification qui ont provoqué l’affichage de cette étiquette.