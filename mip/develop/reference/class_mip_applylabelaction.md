---
title: class mip::ApplyLabelAction
description: 'Documente la classe MIP:: applylabelaction du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 3e5ba734400000b1b1a324520e9595828c2f6ff9
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056316"
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