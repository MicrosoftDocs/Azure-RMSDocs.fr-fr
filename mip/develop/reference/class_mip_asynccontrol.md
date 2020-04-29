---
title: AsyncControl de classe
description: 'Documente la classe AsyncControl :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d032abf9fe7192cfe6ccfd5890d6585aaa2ba645
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763654"
---
# <a name="class-asynccontrol"></a>AsyncControl de classe 
Classe utilisée pour annuler l’opération asynchrone.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public bool Cancel ()  |  L’appel d’Cancel entraîne une tentative d’annulation de la tâche, en cas de réussite, le rappel onFailure approprié sera appelé avec MIP :: OperationCancelledError. Cette fonctionnalité est dépendante du délégué de répartiteur de tâches (.
  
## <a name="members"></a>Membres
  
### <a name="cancel-function"></a>Fonction Cancel
L’appel d’Cancel entraîne une tentative d’annulation de la tâche, en cas de réussite, le rappel onFailure approprié sera appelé avec MIP :: OperationCancelledError. Cette fonctionnalité est dépendante du délégué de répartiteur de tâches (.
  
**Voir aussi**: MIP :: TaskDispatcherDelegate),

  
**Retourne**: false si le signal d’annulation ne peut pas être distribué, true dans le cas contraire.
Ne conservez pas une référence forte à un objet AsyncControl dans un bloc d’achèvement de tâche.