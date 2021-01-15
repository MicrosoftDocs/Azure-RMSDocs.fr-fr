---
title: AsyncControl de classe
description: 'Documente la classe AsyncControl :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7d21002c9bf90014a57eeb9b666f706e2b41f68d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212210"
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