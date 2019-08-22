---
title: class mip::ApplyLabelAction
description: 'Documente la classe MIP:: applylabelaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7d2067ad030e909d53602fcdb3eefa9b88af56bf
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884528"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
Appliquer les actions de l’étiquette requiert d’appeler l’application pour appliquer une étiquette spécifique.
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<étiquette\>& getLabel () const  |  Obtient l’étiquette requise.
public const std:: Vector\<std:: String\>& GetClassificationIds () const  |  Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.
  
## <a name="members"></a>Membres
  
### <a name="getlabel-function"></a>GetLabel fonction)
Obtient l’étiquette requise.

  
**Retourne**: Étiquette.
  
### <a name="getclassificationids-function"></a>GetClassificationIds fonction)
Obtient les ID de classification qui correspondent et a provoqué l’affichage de cette étiquette.

  
**Retourne**: Const std:: Vector < std:: String > & une liste d’ID de classification ayant provoqué l’affichage de cette étiquette.