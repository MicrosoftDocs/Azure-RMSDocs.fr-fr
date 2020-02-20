---
title: class mip::ApplyLabelAction
description: 'Documente la classe MIP :: applylabelaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e1551adddec611c6f9a0982c5a267fad39c436c4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490674"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: shared_ptr\<étiquette\>& GetLabel () const  |  Obtient l’étiquette requise.
public const std :: Vector\<std :: String\>& GetClassificationIds () const  |  Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’étiquette requise.

  
**Retourne**: l’étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds fonction)
Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.

  
**Retourne**: const std :: Vector < std :: string > & une liste d’ID de classification qui a provoqué l’affichage de cette étiquette.