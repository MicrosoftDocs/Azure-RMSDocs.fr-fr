---
title: MIP de classe ::D ocumentState
description: Documente la classe MIP ::d ocumentstate du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a49683730f120b3d43e2c8f9381a86f0df1a400d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490130"
---
# <a name="class-mipdocumentstate"></a>MIP de classe ::D ocumentState 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std :: Vector\<std ::p air\<std :: String, std :: String\>\> GetContentMetadata (const std :: Vector\<std :: String\>& Names, const std :: Vector\<std :: String\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std :: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
public virtuel std :: shared_ptr\<ClassificationResults\> GetClassificationResults (const std :: Vector\<std :: shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtuel std :: Map\<std :: String, std :: String\> GetAuditMetadata () const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
public virtuel std :: Chrono :: time_point\<std :: Chrono :: system_clock\> GetLastModifiedTime () const  |  Retourne un point d’heure au dernier moment où le document a été modifié.
  
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
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime fonction)
Retourne un point d’heure au dernier moment où le document a été modifié.

  
**Retourne**: heure de la dernière modification du point d’heure des documents.