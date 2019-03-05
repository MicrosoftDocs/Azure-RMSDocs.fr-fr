---
title: classe mip::FileExecutionState
description: Décrit la classe mip::fileexecutionstate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 9433ca2f47496e0d28d46c68b3100b53cd25c3f3
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333681"
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
