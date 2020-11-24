---
title: MetadataVersion de classe
description: 'Documente la classe metadataversion :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 05154ec7777fb94478c2065f6e637dea47d58d28
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565672"
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