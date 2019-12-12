---
title: MIP de classe ::D ocumentState
description: Documente la classe MIP ::d ocumentstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 5cdcf04a68269581dc032f753247ba88e9f118d7
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558868"
---
# <a name="class-mipdocumentstate"></a>MIP de classe ::D ocumentState 
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std :: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
public virtuel std :: shared_ptr\<ClassificationResults\> GetClassificationResults (const std :: Vector\<std :: shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
## <a name="members"></a>Membres
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier fonction)
Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].

  
**Retourne**: description du contenu à appliquer au contenu.
Cette valeur est utilisée par l’audit comme une description explicite du contenu
  
### <a name="getdatastate-function"></a>GetDataState fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne** : état des données de contenu
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata fonction)
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne** : métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
Obtenir le descripteur de protection.

  
**Retourne** : descripteur de protection
  
### <a name="getcontentformat-function"></a>GetContentFormat fonction)
Obtient le format du contenu.

  
**Retourne** : DEFAULT, EMAIL 
  
**Voir aussi**: [MIP :: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getclassificationresults-function"></a>GetClassificationResults fonction)
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationIds**: liste d’ID de classification. 



  
**Retourne**: une liste de résultats de classification. retourne nullptr si aucun cycle de classification n’est exécuté.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata fonction)
Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.

  
**Retourne**: une liste de métadonnées d’audit spécifiques à l’application clé enregistrée : ID de paires de valeurs expéditeur : ID de messagerie pour les destinataires de l’expéditeur : représente un tableau JSON de destinataires pour un e-mail LastModifiedBy : ID de l’utilisateur qui a modifié le contenu LastModifiedDate &: date de la dernière modification du contenu