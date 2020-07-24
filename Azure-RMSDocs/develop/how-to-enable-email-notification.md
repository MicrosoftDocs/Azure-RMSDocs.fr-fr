---
title: Activation des notifications par e-mail | Azure RMS
description: Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 3caecdd8d5b5cc173ebe148eaefe3f2202613ab3
ms.sourcegitcommit: 84b45c949d85a7291c088a050d2a66d356fc9af2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87135655"
---
# <a name="how-to-enable-email-notification"></a>Comment : activer les notifications par e-mail

Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.

Pour configurer votre notification par courrier électronique pour une licence donnée, utilisez [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) avec le paramètre de type de propriété *dwPropID*, en tant que [ \_ \_ \_ \_ données spécifiques à l’application IPC Li](https://msdn.microsoft.com/library/hh535287.aspx) et les champs de données d’application sous la forme d’une [liste de \_ valeurs de nom \_ \_ IPC](https://msdn.microsoft.com/library/hh535277.aspx).

**C++**:

```cpp
int numDataPairs = 3;

IPC_NAME_VALUE propertyValuePairs [numDataPairs];

// lcid field set to 0 causes the default lcid to be used

propertyValuePairs[0] = {"MS.Conetent.Name", 0, "FinancialReport.docx"};
propertyValuePairs[1] = {"MS.Notify.Enabled",0 , "true"};
propertyValuePairs[2] = {"MS.Notify.Culture",0 , "en-US"};

IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

result = IpcSetLicenseProperty(licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
```

Le tableau suivant contient les champs de données de l’application (les paires nom/valeur des propriétés) pour les e-mails de notification RMS.


|Nom de la propriété | Type de données | Exemple de valeur | Remarques |
|--------------|-----------|---------------|-------|
|MS.Content.Name|string|« FinancialReport.docx »|Il s’agit d’un identificateur associé au contenu protégé.<br><br> Pour les fichiers protégés, cette valeur doit être le nom du fichier, sans les informations de chemin.<br><br> Pour les autres types de contenu, par exemple, les e-mails, cette valeur peut correspondre à l’objet de l’e-mail ou bien être vide.|
|MS.Notify.Enabled|string|« true » &#124; « false »|Si cette valeur est définie sur « true », un e-mail de notification est envoyé au propriétaire de la licence de publication quand un utilisateur tente d’utiliser sa licence pour obtenir une licence utilisateur final.|
|MS.Notify.Culture|string|« en-US »| **Source** : System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Cette valeur est utilisée pour déterminer la langue localisée de l’e-mail de notification, ainsi que le format de date et d’heure qui doit être utilisé dans l’e-mail.<br><br>Elle doit être définie selon les paramètres utilisateur de l’ordinateur sur lequel est créée la licence de publication, ou selon la culture par défaut du propriétaire de la licence de publication.|
|MS.Notify.TZID|string|« Pacific Standard Time »|**Source** : TimeZoneInfo.Local.Id - ID de fuseau horaire Windows.<br><br>Cette valeur correspond à l’identificateur de fuseau horaire du système d’exploitation Microsoft Windows qui décrit un fuseau horaire particulier et ses caractéristiques.|
|MS.Notify.TZO|string|« -480 »|Il s’agit du décalage horaire du propriétaire de la licence de publication, exprimé en minutes, par rapport à l’heure UTC.<br><br>Si une valeur TZID est fournie, le décalage du fuseau horaire spécifié sera utilisé et cette valeur sera ignorée.<br><br>Cette valeur sera probablement utilisée par les plateformes de publication non Windows qui n’ont pas accès à la liste des valeurs d’ID de fuseau horaire du système d’exploitation Windows.<br><br>Si aucune valeur TZID n’est fournie, cette valeur sera utilisée pour calculer le décalage des messages de notification et la valeur TZSN sera utilisée (quelle que soit la valeur de fuseau horaire) pour indiquer le nom du fuseau horaire. De cette manière, le fuseau horaire reste fixe et n’est pas mis à jour à l’heure d’été.<br><br>Par exemple :<br><br>Si la valeur TXID est vide, et si la valeur TZ0 est définie sur « -420 » et la valeur TZSN définie sur « Pacific Daylight Time », toutes les valeurs indiquées dans l’e-mail de notification seront ajustées à l’heure « Pacific Daylight Time » et le resteront, même si l’heure d’été n’est plus en cours.<br><br>En revanche, si une valeur TZID est fournie, ainsi qu’une valeur TZSN et une valeur TZDN, les heures spécifiées dans l’e-mail de notification seront ajustées et s’afficheront selon le mode d’affichage de date et d’heure défini (Heure d’été ou Standard).|
|MS.Notify.TZSN|string|« Pacific Standard Time »|**Source** : TimeZoneInfo.Local.StandardName - Nom du fuseau horaire.<br><br>Cela doit correspondre au nom localisé du fuseau horaire Standard.|
|MS.Notify.TZDN|string|« Pacific Daylight Time »|**Source** : TimeZoneInfo.Local.DaylightName - Nom du fuseau horaire de l’heure d’été.<br><br>Cela doit correspondre au nom localisé du fuseau horaire de l’heure d’été. Il peut être le même que le nom standard si le fuseau horaire ne prend pas en charge l’heure d’été.|

## <a name="related-topics"></a>Rubriques connexes

- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [\_ \_ \_ données spécifiques de l’application IPC Li \_](https://msdn.microsoft.com/library/hh535287.aspx)
- [IPC \_ \_ \_ liste de valeurs de nom](https://msdn.microsoft.com/library/hh535277.aspx).
