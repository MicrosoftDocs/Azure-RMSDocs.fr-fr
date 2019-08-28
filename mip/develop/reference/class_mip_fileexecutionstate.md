---
title: 'MIP:: FileExecutionState, classe'
description: 'Documente la classe MIP:: fileexecutionstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d6159bf22bf1c887ed74232472163f74440c2051
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056052"
---
# <a name="class-mipfileexecutionstate"></a>MIP:: FileExecutionState, classe 
  
## <a name="summary"></a>Récapitulatif
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public virtuel std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<fileHandler\> &, const std:: Vector\<std:: shared_ptr\<ClassificationRequest\>&)const \>  |  Retourne un mappage des résultats de la classification.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
## <a name="members"></a>Membres
  
### <a name="getdatastate-function"></a>GetDataState fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne**: État des données de contenu
  
### <a name="getclassificationresults-function"></a>GetClassificationResults fonction)
Retourne un mappage des résultats de la classification.

Paramètres :  
* **fileHandler**: le gestionnaire de fichiers du fichier utilisé 


* **classificationIds**: liste d’ID de classification. 



  
**Retourne**: Liste des résultats de la classification.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata fonction)
Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.

  
**Retourne**: Liste des métadonnées d’audit spécifiques à l’application clé inscrite: expéditeur des paires de valeurs: ID d’e-mail pour les destinataires de l’expéditeur: Représente un tableau JSON de destinataires pour un LastModifiedBy de messagerie: ID de messagerie de l’utilisateur qui a modifié le contenu LastModifiedDate &: Date de dernière modification du contenu