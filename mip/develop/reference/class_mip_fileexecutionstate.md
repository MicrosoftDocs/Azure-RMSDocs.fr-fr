---
title: classe mip::FileExecutionState
description: Décrit la classe mip::fileexecutionstate de Microsoft Information Protection (MIP) SDK.
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bdf0814e56d64bd16918a6f4d269a057620f92f5
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184669"
---
# <a name="class-mipfileexecutionstate"></a>classe mip::FileExecutionState 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
DataState GetDataState() virtuel public const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public virtual std::shared_ptr\<ClassificationResults\> GetClassificationResults(const std::shared_ptr\<FileHandler\> &, const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::vector\<uint8_t\> GetSerializedProtectionInfo() const  |  Retourner une mémoire tampon avec le plan sérialisée
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourner un mappage des paires clé-valeur l’application d’audit spécifique.
  
## <a name="members"></a>Membres
  
### <a name="getdatastate-function"></a>GetDataState (fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne**: État des données du contenu
  
### <a name="getclassificationresults-function"></a>GetClassificationResults function
Retourne un mappage des résultats de la classification.

Paramètres :  
* **Gestionnaire de fichiers**:-le Gestionnaire de fichier du fichier utilisé 


* **classificationIds**: une liste des ID de classification. 



  
**Retourne**: Liste des résultats de la classification.
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo function
Retourner une mémoire tampon avec le plan sérialisée

  
**Retourne**: Une mémoire tampon avec le plan sérialisée
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata function
Retourner un mappage des paires clé-valeur l’application d’audit spécifique.

  
**Retourne**: Une liste d’expéditeur les paires clé-valeur inscrit de métadonnées d’audit spécifique application : Id d’e-mail pour l’expéditeur, destinataires : Représente un tableau JSON de destinataires pour un message électronique LastModifiedBy : Id d’e-mail pour l’utilisateur qui a modifié dernièrement le LastModifiedDate & gt ; contenu : Date de que dernière modification du contenu