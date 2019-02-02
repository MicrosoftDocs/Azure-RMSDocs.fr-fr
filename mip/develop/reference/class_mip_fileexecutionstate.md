---
title: classe mip::FileExecutionState
description: Décrit la classe mip::fileexecutionstate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 08a9064645f0ffb3ffbaa72f00db26c5b29d3643
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652334"
---
# <a name="class-mipfileexecutionstate"></a>classe mip::FileExecutionState 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
std::map virtuel public\<std::string, std::shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std::shared_ptr\<FileHandler\> &, const std :: vecteur\<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::vector\<uint8_t\> GetSerializedProtectionInfo() const  |  Retourner une mémoire tampon avec le plan sérialisée
  
## <a name="members"></a>Membres
  
### <a name="getclassificationresults-function"></a>GetClassificationResults function
Retourne un mappage des résultats de la classification.

Paramètres :  
* **Gestionnaire de fichiers**:-le Gestionnaire de fichier du fichier utilisé 


* **classificationIds**: une liste des ID de classification. 



  
**Retourne**: Liste des résultats de la classification.
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Retourner une mémoire tampon avec le plan sérialisée

  
**Retourne**: Une mémoire tampon avec le plan sérialisée