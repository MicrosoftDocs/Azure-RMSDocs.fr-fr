---
title: RecommendLabelAction de classe
description: 'Documente la classe recommendlabelaction :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3990d6de9d78002d9c240e621f96351cd337aabb
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764538"
---
# <a name="class-recommendlabelaction"></a>RecommendLabelAction de classe 
Les actions d’étiquette recommandées sont conçues pour suggérer une étiquette aux utilisateurs. La suppression de cet appel lorsqu’un utilisateur ignore l’étiquette recommandée doit être effectuée via les actions prises en charge sur l’état d’exécution.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std :: shared_ptr\<étiquette\>& getLabel () const  |  Obtient l’étiquette suggérée.
public const std :: Vector\<std :: String\>& GetClassificationIds () const  |  Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’étiquette suggérée.

  
**Retourne**: l’étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds fonction)
Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.

  
**Retourne**: const std :: Vector<std :: String>& une liste des ID de classification qui ont provoqué l’affichage de cette étiquette.