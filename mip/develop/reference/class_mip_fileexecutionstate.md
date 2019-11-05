---
title: 'MIP :: FileExecutionState, classe'
description: 'Documente la classe MIP :: fileexecutionstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 063f1b0227415dc413e0c56d26f60fc39274a817
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560237"
---
# <a name="class-mipfileexecutionstate"></a>MIP :: FileExecutionState, classe 
  
## <a name="summary"></a>Table des matières
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

  
**Retourne**: une liste de métadonnées d’audit spécifiques à l’application clé enregistrée : ID de paires de valeurs expéditeur : ID de courrier électronique pour les destinataires de l’expéditeur : représente un tableau JSON de destinataires pour un e-mail LastModifiedBy : ID de messagerie de l’utilisateur qui a modifié le contenu pour la dernière fois LastModifiedDate &: date de la dernière modification du contenu