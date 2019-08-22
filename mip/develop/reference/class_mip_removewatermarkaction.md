---
title: mip::RemoveWatermarkAction, classe
description: 'Documente la classe MIP:: removewatermarkaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 9d67dc7839183e148cb2792482e1fc186858ce7e
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883146"
---
# <a name="class-mipremovewatermarkaction"></a>mip::RemoveWatermarkAction, classe 
Classe d’action qui spécifie la suppression du filigrane du document.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetUIElementNames()  |  Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.
public ActionType GetType() const  |  Obtenir le type de [Action](class_mip_action.md).
  
## <a name="members"></a>Membres
  
### <a name="getuielementnames-function"></a>GetUIElementNames fonction)
Obtient une liste de noms à utiliser pour rechercher les éléments d’interface utilisateur qui doivent être supprimés.

  
**Retourne**: Liste des noms d’éléments d’interface utilisateur.
  
### <a name="gettype-function"></a>GetType, fonction
Obtenir le type de [Action](class_mip_action.md).

  
**Retourne**: ActionType : type d’action dérivée vers lequel cette classe de base peut être castée.