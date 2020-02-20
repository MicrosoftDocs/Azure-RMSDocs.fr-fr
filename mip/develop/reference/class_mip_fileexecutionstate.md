---
title: 'MIP :: FileExecutionState, classe'
description: 'Documente la classe MIP :: fileexecutionstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a55ad7b5d28a3115ea4f17f36a846011e82d7827
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490045"
---
# <a name="class-mipfileexecutionstate"></a>MIP :: FileExecutionState, classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public virtuel std :: shared_ptr\<ClassificationResults\> GetClassificationResults (const std :: shared_ptr\<FileHandler\> &, const std :: Vector\<std :: shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtuel std :: Map\<std :: String, std :: String\> GetAuditMetadata () const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
## <a name="members"></a>Membres
  
### <a name="getdatastate-function"></a>GetDataState fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne** : état des données de contenu
  
### <a name="getclassificationresults-function"></a>GetClassificationResults fonction)
Retourne un mappage des résultats de la classification.

Paramètres :  
* **fileHandler**: le gestionnaire de fichiers du fichier utilisé 


* **classificationIds**: liste d’ID de classification. 



  
**Retourne**: une liste de résultats de classification.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata fonction)
Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.

  
**Retourne**: une liste de métadonnées d’audit spécifiques à l’application clé enregistrée : ID de paires de valeurs expéditeur : ID de messagerie pour les destinataires de l’expéditeur : représente un tableau JSON de destinataires pour un e-mail LastModifiedBy : ID de l’utilisateur qui a modifié le contenu LastModifiedDate &: date de la dernière modification du contenu