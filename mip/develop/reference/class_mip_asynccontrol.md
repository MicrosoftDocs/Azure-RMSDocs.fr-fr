---
title: AsyncControl de classe
description: 'Documente la classe AsyncControl :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7058ccdcac0133bc708a81d5e7342f61c48994f9
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567275"
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