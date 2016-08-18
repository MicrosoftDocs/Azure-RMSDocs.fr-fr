---
title: "Procédure d’utilisation du suivi de documents | Azure RMS"
description: "L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ca4982cc86d9c006486540055de7c165adca21da
ms.openlocfilehash: 9872317c2d5f5f56f28ed2683d7ebc9743041a37


---

# Procédure : utilisation du suivi des documents

L’utilisation de la fonctionnalité de suivi des documents nécessite une connaissance de base de la gestion des métadonnées associées et de l’inscription auprès du service.

## Gestion des métadonnées de suivi des documents

Chacun des systèmes d’exploitation prenant en charge le suivi des documents a des implémentations similaires. Elles comprennent notamment un ensemble de propriétés qui représentent les métadonnées, un nouveau paramètre ajouté aux méthodes de création de stratégie utilisateur, et une méthode pour inscrire la stratégie afin de la suivre avec le service de suivi des documents.

Du point de vue opérationnel, seules les propriétés **nom du contenu** et **type de notification** sont nécessaires pour le suivi des documents.

La séquence d’étapes que vous utiliserez pour configurer le suivi des documents pour un élément de contenu donné est la suivante :

-   Créer un objet de **métadonnées de licence**.

    Pour plus d’informations, consultez [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc).

-   Définir les propriétés **nom du contenu** et **type de notification**. Ce sont les seules propriétés requises.

    Pour plus d’informations, consultez les méthodes d’accès aux propriétés pour la classe de métadonnées de licence correspondant à la plateforme, [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) ou [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc).

-   Par type de stratégie ; modèle ou ad hoc :

    -   Pour le suivi des document en fonction du modèle, créez un objet **stratégie utilisateur** qui passe les métadonnées de licence en tant que paramètre.

        Pour plus d’informations, consultez [**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) et [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc).

    -   Pour le suivi des document ad hoc, définissez la propriété **métadonnées de licence** sur l’objet **descripteur de stratégie**.

        Pour plus d’informations, consultez [**PolicyDescriptor.getLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java), [**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) et [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc).

    **Remarque**  L’objet de métadonnées de licence n’est directement accessible que pendant le processus de configuration du suivi des documents pour la stratégie d’utilisateur donnée. Une fois l’objet de stratégie utilisateur créé, les métadonnées de licence associées ne sont plus accessibles. Par exemple, la modification des valeurs de métadonnées de licence n’a aucun effet.

     

-   Appeler la méthode d’inscription de plateforme pour le suivi des documents.

    Consultez [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) ou [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc).

 

 



<!--HONumber=Jun16_HO4-->


