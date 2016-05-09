---
# required metadata

title: Activation des notifications par e-mail | Azure RMS
description: Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: fcaa5643-64a9-4181-b29b-90211fce7ab5

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Activation des notifications par e-mail

Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.

Pour configurer les notifications par e-mail pour une licence donnée, utilisez [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) avec le paramètre de type de propriété *dwPropID* en tant que [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA), et les champs de données de l’application en tant que [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list).

## C++

    ...
    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
    ...    

Le tableau suivant contient les champs de données de l’application (les paires nom/valeur des propriétés) pour les e-mails de notification RMS.


|Nom de la propriété | Type de données | Exemple de valeur | Remarques |
|--------------|-----------|---------------|-------|
|MS.Content.Name|string|« FinancialReport.docx »|Il s’agit d’un identificateur associé au contenu protégé.<br><br> Pour les fichiers protégés, cette valeur doit être le nom du fichier, sans les informations de chemin.<br><br> Pour les autres types de contenu, par exemple, les e-mails, cette valeur peut correspondre à l’objet de l’e-mail ou bien être vide.|
|MS.Notify.Enabled|string|« true » &#124; « false »|Si cette valeur est définie sur « true », un e-mail de notification est envoyé au propriétaire de la licence de publication quand un utilisateur tente d’utiliser sa licence pour obtenir une licence utilisateur final.|
|MS.Notify.Culture|string|« en-US »| **Source** : System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Cette valeur est utilisée pour déterminer la langue localisée de l’e-mail de notification, ainsi que le format de date et d’heure qui doit être utilisé dans l’e-mail.<br><br>Elle doit être définie selon les paramètres utilisateur de l’ordinateur sur lequel est créée la licence de publication, ou selon la culture par défaut du propriétaire de la licence de publication.|
|MS.Notify.TZID|string|« Pacific Standard Time »|**Source** : TimeZoneInfo.Local.Id - ID de fuseau horaire Windows.<br><br>Cette valeur correspond à l’identificateur de fuseau horaire du système d’exploitation Microsoft Windows qui décrit un fuseau horaire particulier et ses caractéristiques.|
|MS.Notify.TZO|string|« -480 »|Il s’agit du décalage horaire du propriétaire de la licence de publication, exprimé en minutes, par rapport à l’heure UTC.<br><br>Si une valeur TZID est fournie, le décalage du fuseau horaire spécifié sera utilisé et cette valeur sera ignorée.<br><br>Cette valeur sera probablement utilisée par les plateformes de publication non Windows qui n’ont pas accès à la liste des valeurs d’ID de fuseau horaire du système d’exploitation Windows.<br><br>Si aucune valeur TZID n’est fournie, cette valeur sera utilisée pour calculer le décalage des messages de notification et la valeur TZSN sera utilisée (quelle que soit la valeur de fuseau horaire) pour indiquer le nom du fuseau horaire. De cette manière, le fuseau horaire reste fixe et n’est pas mis à jour à l’heure d’été.<br><br>Exemple :<br><br>Si la valeur TXID est vide, et si la valeur TZ0 est définie sur « -420 » et la valeur TZSN définie sur « Pacific Daylight Time », toutes les valeurs indiquées dans l’e-mail de notification seront ajustées à l’heure « Pacific Daylight Time » et le resteront, même si l’heure d’été n’est plus en cours.<br><br>En revanche, si une valeur TZID est fournie, ainsi qu’une valeur TZSN et une valeur TZDN, les heures spécifiées dans l’e-mail de notification seront ajustées et s’afficheront selon le mode d’affichage de date et d’heure défini (Heure d’été ou Standard).|
|MS.Notify.TZSN|string|« Pacific Standard Time »|**Source** : TimeZoneInfo.Local.StandardName - Nom du fuseau horaire.<br><br>Cela doit correspondre au nom localisé du fuseau horaire Standard.|
|MS.Notify.TZDN|string|« Pacific Daylight Time »|**Source** : TimeZoneInfo.Local.DaylightName - Nom du fuseau horaire de l’heure d’été.<br><br>Cela doit correspondre au nom localisé du fuseau horaire de l’heure d’été. Il peut être le même que le nom standard si le fuseau horaire ne prend pas en charge l’heure d’été.|

## Rubriques connexes

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 


<!--HONumber=Apr16_HO3-->


