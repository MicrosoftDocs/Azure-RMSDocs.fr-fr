---
title: mip::ExecutionState, classe
description: 'Documente la classe MIP :: ExecutionState du kit de développement logiciel (SDK) Microsoft Information Protection (MIP).'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 0087255c3028ed28f6b4729445d6c224344f0dde
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558885"
---
# <a name="class-mipexecutionstate"></a>mip::ExecutionState, classe 
Interface pour tous les états nécessaires à l’exécution du moteur.
Les clients doivent uniquement appeler les méthodes pour obtenir l’état qui est nécessaire. Ainsi, pour des raisons d’efficacité, les clients peuvent implémenter cette interface afin que l’état correspondant soit calculé de façon dynamique plutôt qu’en avance.
  
## <a name="summary"></a>Table des matières
 Membres                        | Descriptions                                
--------------------------------|---------------------------------------------
public std :: shared_ptr\<étiquette\> GetNewLabel () const  |  Obtient l’ID de l’étiquette de sensibilité à appliquer au document.
public std::string GetContentIdentifier() const  |  Obtient la description du contenu qui décrit le document. exemple pour un fichier : [path\filename] exemple pour un e-mail : [Subject : sender].
DataState virtuel public GetDataState () const  |  Obtient l’état du contenu pendant que l’application interagit avec celui-ci.
public std::pair\<bool, std::string\> IsDowngradeJustified() const  |  L’implémentation doit avoir lieu si une justification de passer une étiquette existante à une version antérieure a été fournie.
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  Obtenir la méthode d’assignation de la nouvelle étiquette.
public virtuel std :: Vector\<std ::p air\<std :: String, std :: String\>\> GetNewLabelExtendedProperties () const  |  Retourner les propriétés étendues de la nouvelle étiquette.
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  Obtenir les éléments de métadonnées à partir du contenu.
public std :: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  Obtenir le descripteur de protection.
public ContentFormat GetContentFormat() const  |  Obtient le format du contenu.
public ActionType GetSupportedActions() const  |  Obtient une énumération masquée qui décrit tous les types d’action pris en charge.
public virtuel std :: shared_ptr\<ClassificationResults\> GetClassificationResults (const std :: Vector\<std :: shared_ptr\<ClassificationRequest\>\> &) const  |  Retourne un mappage des résultats de la classification.
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  Retourne une carte de paires clé-valeur d’audit spécifiques à l’application.
  
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
  
**Voir aussi**: [MIP :: assignation](mip-enums-and-structs.md#assignmentmethod-enum)
  
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
  
**Voir aussi**: [MIP :: ContentFormat](mip-enums-and-structs.md#contentformat-enum)
  
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