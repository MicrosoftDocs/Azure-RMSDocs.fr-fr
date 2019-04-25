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
ms.openlocfilehash: 334b4aed3e24a64e553429587eea4b0bf4c7948a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178367"
---
# <a name="how-to-use-document-tracking"></a>Procédure : utiliser le suivi des documents

L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service.

## <a name="managing-document-tracking-metadata"></a>Gestion des métadonnées de suivi des documents

Chacun des systèmes d’exploitation prenant en charge le suivi des documents a des implémentations similaires. Elles comprennent notamment un ensemble de propriétés qui représentent les métadonnées, un nouveau paramètre ajouté aux méthodes de création de stratégie utilisateur, et une méthode pour inscrire la stratégie afin de la suivre avec le service de suivi des documents.

Du point de vue opérationnel, seules les propriétés **nom du contenu** et **type de notification** sont nécessaires pour le suivi des documents.

La séquence d’étapes que vous utiliserez pour configurer le suivi des documents pour un élément de contenu donné est la suivante :

- Créez un objet de **métadonnées de licence**, puis définissez le **nom du contenu** et le **type de notification**. Ce sont les seules propriétés requises.
  - Android - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
  -  iOS - [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

Choisissez un type de stratégie, modèle ou ad hoc :
- Pour le suivi des document en fonction du modèle, créez un objet **stratégie utilisateur** qui passe les métadonnées de licence en tant que paramètre.
  - Android - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- Pour le suivi des document ad hoc, définissez la propriété **métadonnées de licence** sur l’objet **descripteur de stratégie**.
  - Android - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS - [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx).

    **Remarque**  L’objet de métadonnées de licence n’est directement accessible que pendant le processus de configuration du suivi des documents pour la stratégie d’utilisateur donnée. Une fois l’objet de stratégie utilisateur créé, les métadonnées de licence associées ne sont plus accessibles. Par conséquent, la modification des valeurs des métadonnées de licence n’aura aucun effet.

     

- Enfin, appelez la méthode d’inscription de plateforme pour le suivi des documents.
  - Android - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) ou [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)
