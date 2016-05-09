---
# required metadata

title: Suivi du contenu | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ca08e01f-690d-46f4-ae0f-a880cc29dabc

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Suivi du contenu

\[Certaines informations se rapportent à la version préliminaire du produit qui peut encore faire l’objet de modifications significatives avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.\]

Cette rubrique propose des conseils de base pour implémenter le suivi de documents sur du contenu protégé à l’aide de Rights Management Services SDK 2.1.

Le suivi de documents est une fonctionnalité du système Rights Management. En ajoutant des métadonnées spécifiques pendant le processus de protection d’un document, vous pouvez inscrire le document auprès d’un portail de services offrant différentes options de suivi.

Utilisez ces API pour ajouter/mettre à jour une licence de contenu avec les métadonnées de suivi des documents.

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    Vous définirez sans doute toutes les propriétés des métadonnées. Celles-ci, classées par type, sont répertoriées ci-dessous.

    Pour plus d’informations, consultez [**Types de propriétés des métadonnées de licence**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types).

    -   **IPC\_MD\_CONTENT\_PATH**

        Permet d’identifier le document faisant l’objet d’un suivi. S’il est impossible de fournir un chemin complet, indiquez simplement le nom du fichier.

    -   **IPC\_MD\_CONTENT\_NAME**

        Permet d’identifier le nom du document faisant l’objet d’un suivi.

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        Permet d’indiquer quand la notification est envoyée. Pour plus d’informations, consultez [**Type de notification**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type).

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        Permet d’indiquer le type de notification. Pour plus d’informations, consultez [**Préférence de notification**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference).

    -   **IPC\_MD\_DATE\_MODIFIED**

        Nous vous suggérons de définir cette date chaque fois que l’utilisateur clique sur **Enregistrer**.

    -   **IPC\_MD\_DATE\_CREATED**

        Date de création du fichier.

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

Utilisez l’API appropriée parmi celles-ci pour ajouter les métadonnées à votre fichier ou flux.

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

Enfin, utilisez cette API pour inscrire votre document faisant l’objet d’un suivi auprès du système de suivi.

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

Voici un exemple d’extrait de code illustrant la définition des métadonnées de suivi de document et l’appel utilisé pour inscrire le document auprès du système de suivi.



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

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

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


### Rubriques connexes


* [**Types de propriétés des métadonnées de licence**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**Préférence de notification**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**Type de notification**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Apr16_HO3-->


