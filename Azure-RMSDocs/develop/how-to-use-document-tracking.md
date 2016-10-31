---
title: "Procédure d’utilisation du suivi de documents | Azure RMS"
description: "L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 04234755fabb10794f5be7c4fc658573bebf6e70
ms.openlocfilehash: 616d5dd088665abf6e7d435978b021b10c5ac3f5


---

# Procédure : utilisation du suivi des documents

L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service.

## Gestion des métadonnées de suivi des documents

Chacun des systèmes d’exploitation prenant en charge le suivi des documents a des implémentations similaires. Elles comprennent notamment un ensemble de propriétés qui représentent les métadonnées, un nouveau paramètre ajouté aux méthodes de création de stratégie utilisateur, et une méthode pour inscrire la stratégie afin de la suivre avec le service de suivi des documents.

Du point de vue opérationnel, seules les propriétés **nom du contenu** et **type de notification** sont nécessaires pour le suivi des documents.

La séquence d’étapes que vous utiliserez pour configurer le suivi des documents pour un élément de contenu donné est la suivante :

-   Créez un objet de **métadonnées de licence**, puis définissez le **nom du contenu** et le **type de notification**. Ce sont les seules propriétés requises.
   - Android - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
   -  iOS - [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

Choisissez un type de stratégie, modèle ou ad hoc :
- Pour le suivi des document en fonction du modèle, créez un objet **stratégie utilisateur** qui passe les métadonnées de licence en tant que paramètre.
  - Android - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- Pour le suivi des document ad hoc, définissez la propriété **métadonnées de licence** sur l’objet **descripteur de stratégie**.
  - Android - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS - [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx).

    **Remarque**  L’objet de métadonnées de licence n’est directement accessible que pendant le processus de configuration du suivi des documents pour la stratégie d’utilisateur donnée. Une fois l’objet de stratégie utilisateur créé, les métadonnées de licence associées ne sont plus accessibles. Par conséquent, la modification des valeurs des métadonnées de licence n’aura aucun effet.

     

-   Enfin, appelez la méthode d’inscription de plateforme pour le suivi des documents.
  - Android - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) ou [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)

 

 



<!--HONumber=Oct16_HO3-->


