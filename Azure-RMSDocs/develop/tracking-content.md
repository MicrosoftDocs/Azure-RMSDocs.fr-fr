---
title: Procédure d’activation du suivi et de la révocation de documents | Azure RMS
description: Instructions de base pour implémenter le suivi des documents pour le contenu ainsi qu’un exemple de code pour les mises à jour de métadonnées et un bouton Suivre l’utilisation pour votre application.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: e632e99f42947afa10223bb1b11fcc18cdec6f7a
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
ms.locfileid: "27765423"
---
# <a name="how-to-enable-document-tracking-and-revocation"></a>Comment : activer le suivi et la révocation de documents

Cette rubrique décrit les instructions de base pour implémenter le suivi des documents pour le contenu ainsi que l’exemple de code pour les mises à jour de métadonnées et la création d’un **bouton Suivre l'utilisation** pour votre application.

## <a name="steps-to-implement-document-tracking"></a>Étapes pour implémenter le suivi des documents

Les étapes 1 et 2 permettent au document d’être suivi. L’étape 3 permet aux utilisateurs de votre application d’atteindre le site de suivi des documents pour suivre et révoquer vos documents protégés.

1. Ajouter des métadonnées de suivi des documents
2. Inscrire le document auprès du service RMS
3. Ajouter un bouton Suivre l’utilisation à votre application

Les détails de l’implémentation de ces étapes suivent.

## <a name="1-add-document-tracking-metadata"></a>1. Ajouter des métadonnées de suivi des documents

Le suivi de documents est une fonctionnalité du système Rights Management. En ajoutant des métadonnées spécifiques pendant le processus de protection d’un document, vous pouvez inscrire le document auprès d’un portail de services offrant différentes options de suivi.

Utilisez ces API pour ajouter/mettre à jour une licence de contenu avec les métadonnées de suivi des documents.


Du point de vue opérationnel, seules les propriétés **nom du contenu** et **type de notification** sont nécessaires pour le suivi des documents.


- [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
- [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)

  Vous définirez sans doute toutes les propriétés des métadonnées. Celles-ci, classées par type, sont répertoriées ci-dessous.

  Pour plus d’informations, consultez [Types de propriétés des métadonnées de licence](https://msdn.microsoft.com/library/dn974062.aspx).

  - **IPC_MD_CONTENT_PATH**

    Permet d’identifier le document faisant l’objet d’un suivi. S’il est impossible de fournir un chemin complet, indiquez simplement le nom du fichier.

  - **IPC_MD_CONTENT_NAME**

    Permet d’identifier le nom du document faisant l’objet d’un suivi.

  - **IPC_MD_NOTIFICATION_TYPE**

    Permet d’indiquer quand la notification est envoyée. Pour plus d’informations, consultez Type de notification.

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    Permet d’indiquer le type de notification. Pour plus d’informations, consultez Préférence de notification.

  - **IPC_MD_DATE_MODIFIED**

    Nous vous suggérons de définir cette date chaque fois que l’utilisateur clique sur Enregistrer.

  - **IPC_MD_DATE_CREATED**

    Permet de définir la date de création du fichier.

- [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)

Utilisez l’API appropriée parmi celles-ci pour ajouter les métadonnées à votre fichier ou flux.

- [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
- [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)

Enfin, utilisez cette API pour inscrire votre document faisant l’objet d’un suivi auprès du système de suivi.

- [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


## <a name="2-register-the-document-with-the-rms-service"></a>2. Inscrire le document auprès du service RMS

Voici un exemple d’extrait de code illustrant la définition des métadonnées de suivi de document et l’appel utilisé pour inscrire le document auprès du système de suivi.

      C++
      HRESULT hr = S_OK;
      LPCWSTR wszOutputFile = NULL;
      wstring wszWorkingFile;
      IPC_LICENSE_METADATA md = {0};

      md.cbSize = sizeof(IPC_LICENSE_METADATA);
      md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
      md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
      //file origination date, current time for this example
      md.ftDateCreated = GetCurrentTime();
      md.ftDateModified = GetCurrentTime();

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

     /* This will contain the serialized license */
     PIPC_BUFFER pSerializedLicense;

     /* the context to use for the call */
     PCIPC_PROMPT_CTX pContext;

     wstring wstrContentName(“MyDocument.txt”);
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);

## <a name="add-a-track-usage-button-to-your-app"></a>Ajouter un bouton **Suivre l’utilisation** à votre application

Ajouter un élément d’interface utilisateur **Suivre l’utilisation** à votre application est aussi simple qu’utiliser l’un des formats d’URL suivants :

- Utilisation de l’ID de contenu
  - Obtenez l’ID de contenu à l’aide de [IpcGetLicenseProperty](https://msdn.microsoft.com/library/hh535265.aspx) ou [IpcGetSerializedLicenseProperty](https://msdn.microsoft.com/library/hh995038.aspx) si la licence est sérialisée et utilisez la propriété de licence **IPC_LI_CONTENT_ID**. Pour plus d’informations, consultez [Types de propriété de licence](https://msdn.microsoft.com/library/hh535287.aspx).
  - Avec les métadonnées **ContentId** et **Issuer**, utilisez le format suivant : `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    Exemple : `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- Si vous n’avez pas accès à ces métadonnées (par exemple, si vous examinez la version non protégée du document), vous pouvez utiliser **Content_Name** au format suivant : `https://track.azurerms.com/#/?q={ContentName}`

  Exemple : https://track.azurerms.com/#/?q=Secret!.txt

Le client doit simplement ouvrir un navigateur avec l’URL appropriée. Le portail de suivi des documents RMS gère l’authentification et toute redirection requise.

## <a name="related-topics"></a>Rubriques connexes

* [Types de propriétés des métadonnées de licence](https://msdn.microsoft.com/library/dn974062.aspx)
* [Préférence de notification](https://msdn.microsoft.com/library/dn974063.aspx)
* [Type de notification](https://msdn.microsoft.com/library/dn974064.aspx)
* [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
* [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)
* [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)
* [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
* [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)
* [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]