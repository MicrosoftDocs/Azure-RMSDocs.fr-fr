---
title: 'MIP :: AsyncControl, classe'
description: 'Documente la classe MIP :: AsyncControl du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: afef25cef1363d5275581a774279c97d61239f4b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77492764"
---
# <a name="class-mipasynccontrol"></a>MIP :: AsyncControl, classe 
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