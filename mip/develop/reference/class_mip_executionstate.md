---
title: ExecutionState de classe
description: 'Documente la classe ExecutionState :: non définie du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: f73c3e366f1be0647d2c9a7de78f37b6a9a95549
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566990"
---
# <a name="class-executionstate"></a>ExecutionState de classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Résumé
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr \<Label\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
STD public ::p air \<bool, std::string\> IsDowngradeJustified () const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std :: Vector \<std::pair\<std::string, std::string\> \> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std :: Vector \<MetadataEntry\> GetContentMetadata (const std :: vector \<std::string\>& Names, const std :: Vector \<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
MetadataVersion virtuel public GetContentMetadataVersion () const  |  Obtient la version de métadonnées la plus élevée prise en charge par l’application pour le locataire.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public virtuel std :: shared_ptr \<ClassificationResults\> GetClassificationResults (const std :: vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  Retourne un mappage des résultats de la classification.
public virtuel std :: map \<std::string, std::string\> GetAuditMetadata () const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
## <a name="members"></a>Membres
  
### <a name="getnewlabel-function"></a>GetNewLabel fonction)
Obtient l’ID de l’étiquette de sensibilité à appliquer au document.

  
**Retourne** : ID de l’étiquette de sensibilité à appliquer au contenu s’il existe ; sinon, valeur vide pour supprimer l’étiquette.
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier fonction)
Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].

  
**Retourne**: description du contenu à appliquer au contenu.
Cette valeur est utilisée par l’audit comme une description explicite du contenu
  
### <a name="getdatastate-function"></a>GetDataState fonction)
Obtient l’état du contenu pendant que l’application interagit avec celui-ci.

  
**Retourne** : état des données de contenu
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified fonction)
L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.

  
**Retourne** : True si le passage à une version antérieure est justifié avec le message de justification ; sinon, False 
  
**Voir aussi**: MIP :: JustifyAction
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod fonction)
Obtenir la méthode d’assignation de la nouvelle étiquette.

  
**Retourne** : la méthode d’affectation STANDARD, PRIVILEGED, AUTO. 
  
**Voir aussi** : mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties fonction)
Retourner les propriétés étendues de la nouvelle étiquette.

  
**Retourne** : propriétés étendues appliquées au contenu.
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata fonction)
Obtenir les éléments de métadonnées à partir du contenu.

  
**Retourne** : métadonnées appliquées au contenu. Chaque élément de métadonnées est une paire nom/valeur.
  
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
  
### <a name="getsupportedactions-function"></a>GetSupportedActions fonction)
Obtient une énumération masquée qui décrit tous les types d’action pris en charge.

  
**Retourne** : énumération masquée qui décrit tous les types d’action pris en charge.
ActionType::Justify doit être pris en charge. Quand la modification d’une stratégie et d’une étiquette nécessite une justification, une action de la justification est toujours retournée.
  
### <a name="getclassificationresults-function"></a>GetClassificationResults fonction)
Retourne un mappage des résultats de la classification.

Paramètres :  
* **classificationIds**: liste d’ID de classification. 



  
**Retourne**: une liste de résultats de classification. retourne nullptr si aucun cycle de classification n’est exécuté.
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata fonction)
Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.

  
**Retourne**: une liste de métadonnées d’audit spécifiques à l’application clé enregistrée : ID de paires de valeurs expéditeur : ID de messagerie pour les destinataires de l’expéditeur : représente un tableau JSON de destinataires pour un e-mail LastModifiedBy : ID de l’utilisateur qui a modifié le contenu LastModifiedDate &: date de la dernière modification du contenu