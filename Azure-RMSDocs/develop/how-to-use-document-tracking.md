---
title: Procédure d’utilisation du suivi de documents | Azure RMS
description: L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: dfcb4c616be2f5891b242a918a06abf2708c12cc
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568199"
---
# <a name="how-to-use-document-tracking"></a>Comment : utiliser le suivi de documents

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service.

## <a name="managing-document-tracking-metadata"></a>Gestion des métadonnées de suivi des documents

Chacun des systèmes d’exploitation prenant en charge le suivi des documents a des implémentations similaires. Elles comprennent notamment un ensemble de propriétés qui représentent les métadonnées, un nouveau paramètre ajouté aux méthodes de création de stratégie utilisateur, et une méthode pour inscrire la stratégie afin de la suivre avec le service de suivi des documents.

Du point de vue opérationnel, seules les propriétés **nom du contenu** et **type de notification** sont nécessaires pour le suivi des documents.

La séquence d’étapes que vous utiliserez pour configurer le suivi des documents pour un élément de contenu donné est la suivante :

- Créez un objet de **métadonnées de licence**, puis définissez le **nom du contenu** et le **type de notification**. Ce sont les seules propriétés requises.
  - Android - [LicenseMetadata](/previous-versions/windows/desktop/msipcthin2/licensemetadata-interface-java)
  -  iOS - [MSLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/mslicensemetadata-class-objc)

Choisissez un type de stratégie, modèle ou ad hoc :
- Pour le suivi des document en fonction du modèle, créez un objet **stratégie utilisateur** qui passe les métadonnées de licence en tant que paramètre.
  - Android - [UserPolicy.create](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-templatedescriptor-property-objc)

- Pour le suivi des document ad hoc, définissez la propriété **métadonnées de licence** sur l’objet **descripteur de stratégie**.
  - Android - [PolicyDescriptor.setLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/policydescriptor-setlicensemetadata-java)
  - iOS - [MSPolicyDescriptor.licenseMetadata](/previous-versions/windows/desktop/msipcthin2/mspolicydescriptor-licensemetadata-property-objc).

    **Remarque**    L’objet de métadonnées de licence n’est accessible directement qu’au cours du processus de configuration du suivi des documents pour la stratégie d’utilisateur donnée. Une fois l’objet de stratégie utilisateur créé, les métadonnées de licence associées ne sont plus accessibles. Par conséquent, la modification des valeurs des métadonnées de licence n’aura aucun effet.

     

- Enfin, appelez la méthode d’inscription de plateforme pour le suivi des documents.
  - Android - [UserPolicy.registerForDocTracking asynchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-boolean--sting--authenticationcallback--creationcallback--java) ou [UserPolicy.registerForDocTracking synchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-synchronous-method-java)
  - iOS - [MSUserPolicy.registerForDocTracking](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-registerfordoctracking-userid-authenticationcallback-completionblock-method-objc)