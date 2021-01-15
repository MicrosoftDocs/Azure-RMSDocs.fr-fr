---
title: MetadataVersion de classe
description: 'Documente la classe metadataversion :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 35ed3ef28cd4a1a822c11f64b422a474edcd4b53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213604"
---
# <a name="class-metadataversion"></a>MetadataVersion de classe 
Interface pour un MetadataVersion. MetadataVersion détermine les métadonnées actives et leur mode de traitement.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public MetadataVersion (version uint32_t, indicateurs MetadataVersionFormat)  |  Constructeur MetadataVersion.
const uint32_t virtuelle public GetValue ()  |  Obtient la version numérique.
public virtuel bool HasFlag (indicateur MetadataVersionFormat) const  |  Obtient une valeur indiquant si un indicateur spécifique est défini.
MetadataVersionFormat-const virtuelle public  |  Obtient les indicateurs qui définissent le mode de traitement des métadonnées pour une version donnée.
  
## <a name="members"></a>Membres
  
### <a name="metadataversion-function"></a>MetadataVersion fonction)
Constructeur MetadataVersion.

Paramètres :  
* **version**: version numérique à utiliser pour les actions de métadonnées 


* **Flags**: indicateurs pour spécifier comment la version est utilisée pour calculer des actions de métadonnées


  
### <a name="getvalue-function"></a>GetValue, fonction
Obtient la version numérique.

  
**Retourne**: la version numérique.
  
### <a name="hasflag-function"></a>HasFlag fonction)
Obtient une valeur indiquant si un indicateur spécifique est défini.

  
**Retourne**: true si l’indicateur est défini.
  
### <a name="getflags-function"></a>GetFlags, fonction
Obtient les indicateurs qui définissent le mode de traitement des métadonnées pour une version donnée.

  
**Retourne**: les indicateurs qui spécifient le mode de traitement des métadonnées.