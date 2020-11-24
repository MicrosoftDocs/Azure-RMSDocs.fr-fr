---
title: DocumentState de classe
description: 'Documente la classe documentstate :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: ad1c99a76c3078c86ec80a4ec6e1cc7d244cbbeb
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567006"
---
# <a name="class-documentstate"></a>DocumentState de classe 
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std :: Vector \<MetadataEntry\> GetContentMetadata (const std :: vector \<std::string\>& Names, const std :: Vector \<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
MetadataVersion virtuel public GetContentMetadataVersion () const  |  Obtient la version de métadonnées la plus élevée prise en charge par l’application pour le locataire.
public virtuel std :: shared_ptr \<ClassificationResults\> GetClassificationResults (const std :: vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Retourne un mappage des résultats de la classification.
public virtuel std :: map \<std::string, std::string\> GetAuditMetadata () const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
public virtuel std :: Chrono :: time_point \<std::chrono::system_clock\> GetLastModifiedTime () const  |  Retourne un point d’heure au dernier moment où le document a été modifié.
  
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

  
**Retourne** : métadonnées appliquées au contenu. 
  
**Voir aussi**: MIP :: MetadataEntry.
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor fonction)
Obtenir le descripteur de protection.

  
**Retourne** : descripteur de protection
  
### <a name="getcontentformat-function"></a>GetContentFormat fonction)
Obtient le format du contenu.

  
**Retourne** : DEFAULT, EMAIL 
  
**Voir aussi** : mip::ContentFormat
  
### <a name="getcontentmetadataversion-function"></a>GetContentMetadataVersion fonction)
Obtient la version de métadonnées la plus élevée prise en charge par l’application pour le locataire.

  
**Retourne**: version des métadonnées de contenu. Si la valeur est 0, les métadonnées n’ont pas de version. Si un format de fichier prend en charge plusieurs versions des métadonnées, cela permet à MIP de comprendre toutes les métadonnées et de signaler les modifications des métadonnées granulaires à chaque version.
  
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