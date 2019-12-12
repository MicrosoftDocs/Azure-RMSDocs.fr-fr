---
title: Gérer les données personnelles pour Azure Information Protection
description: Informations sur les données personnelles qui sont utilisées par Azure Information Protection et sur la manière de les afficher, les exporter et les supprimer.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d16e6e7f0667f9ac57bf772de272d23838b793e1
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71966890"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Gérer les données personnelles pour Azure Information Protection

Lorsque vous configurez et utilisez Azure Information Protection, les adresses e-mail et les adresses IP sont stockées et utilisées par le service Azure Information Protection. Ces données personnelles se trouvent dans les éléments suivants :

- Stratégie Azure Information Protection

- Modèles pour le service de protection

- Super utilisateurs et administrateurs délégués pour le service de protection 

- Journaux d’administration pour le service de protection

- Journaux d’utilisation pour le service de protection

- Journaux de suivi des documents

- Journaux d’utilisation pour les clients Azure Information Protection et le client RMS 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Affichage des données personnelles utilisées par Azure Information Protection

À l’aide du portail Azure, un administrateur peut spécifier des adresses e-mail pour les stratégies délimitées et les paramètres de protection dans une configuration d’étiquette. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les étiquettes qui sont configurées pour appliquer la protection à partir du service Azure Rights Management, vous pouvez également trouver l’adresse de messagerie dans modèles de protection, à l’aide des applets de commande PowerShell du [module AIPService](/powershell/module/aipservice). Ce module PowerShell permet également à un administrateur de désigner par adresse e-mail les utilisateurs qui ont le rôle de [super utilisateur](configure-super-users.md) ou d’administrateur pour le service Azure Rights Management. 

Quand Azure Information Protection est utilisé pour classifier et protéger des documents et des e-mails, les adresses e-mail et les adresses IP des utilisateurs peuvent être enregistrées dans des fichiers journaux.


### <a name="protection-templates"></a>Modèles de protection

Exécutez l’applet de commande [obtenir-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) pour obtenir la liste des modèles de protection. Vous pouvez utiliser l’ID de modèle pour obtenir des informations détaillées sur un modèle spécifique. L’objet `RightsDefinitions` affiche les données personnelles, le cas échéant. 

Exemple :
```
PS C:\Users> Get-AipServiceTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


TemplateId              : fcdbbc36-1f48-48ca-887f-265ee1268f51
Names                   : {1033 -> Confidential}
Descriptions            : {1033 -> This data includes sensitive business information. Exposing this data to
                          unauthorized users may cause damage to the business. Examples for Confidential information
                          are employee information, individual customer projects or contracts and sales account data.}
Status                  : Archived
RightsDefinitions       : {admin@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT,
                          REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER,
                          AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@aip500.onmicrosoft.com -> VIEW,
                          VIEWRIGHTSDATA, EDIT, DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT,
                          EDITRIGHTSDATA, OBJMODEL, OWNER, admin2@aip500.onmicrosoft.com -> VIEW, VIEWRIGHTSDATA, EDIT,
                          DOCEDIT, PRINT, EXTRACT, REPLY, REPLYALL, FORWARD, EXPORT, EDITRIGHTSDATA, OBJMODEL, OWNER}
ContentExpirationDate   : 1/1/0001 12:00:00 AM
ContentValidityDuration : 0
ContentExpirationOption : Never
LicenseValidityDuration : 7
ReadOnly                : False
LastModifiedTimeStamp   : 1/26/2018 6:17:00 PM
ScopedIdentities        : {}
EnableInLegacyApps      : False
LabelId                 :
```

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>Super utilisateurs et administrateurs délégués pour le service de protection

Exécutez l’applet de commande [AipServiceSuperUser](/powershell/module/aipservice/get-aipservicesuperuser) et l’applet de commande [aipservicerolebasedadministrator](/powershell/module/aipservice/get-aipservicerolebasedadministrator) pour voir quels utilisateurs ont reçu le rôle de super utilisateur ou d’administrateur général pour le service de protection (Azure Rights Management) à partir de Azure information protection. L’adresse e-mail des utilisateurs ayant reçu l’un de ces rôles est affichée.


### <a name="administration-logs-for-the-protection-service"></a>Journaux d’administration pour le service de protection

Exécutez l’applet de commande [obtenir-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog) pour obtenir un journal des actions d’administration pour le service de protection (Azure Rights Management) à partir de Azure information protection. Ce journal contient des données personnelles sous la forme d’adresses e-mail et d’adresses IP. Le journal est en texte clair et une fois téléchargé, les détails d’un administrateur spécifique peuvent être recherchés hors connexion.

Exemple :
```
PS C:\Users> Get-AipServiceAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-protection-service"></a>Journaux d’utilisation pour le service de protection
Exécutez l’applet de commande [obtenir-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog) pour récupérer un journal des actions de l’utilisateur final qui utilisent le service de protection à partir de Azure information protection. Le journal peut inclure des données personnelles sous la forme d’adresses e-mail et d’adresses IP. Le journal est en texte clair et une fois téléchargé, les détails d’un administrateur spécifique peuvent être recherchés hors connexion.

Exemple :
```
PS C:\Users> Get-AipServiceUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
Acquiring access to your user log…
Downloading the log for 2018-04-01.
Downloading the log for 2018-04-03.
Downloading the log for 2018-04-06.
Downloading the log for 2018-04-09.
Downloading the log for 2018-04-10.
Downloaded the log for 2018-04-01. The log is available at .\Desktop\rmslog-2018-04-01.log.
Downloaded the log for 2018-04-03. The log is available at .\Desktop\rmslog-2018-04-03.log.
Downloaded the log for 2018-04-06. The log is available at .\Desktop\rmslog-2018-04-06.log.
Downloaded the log for 2018-04-09. The log is available at .\Desktop\rmslog-2018-04-09.log.
Downloaded the log for 2018-04-10. The log is available at .\Desktop\rmslog-2018-04-10.log.
Downloading the log for 2018-04-12.
Downloading the log for 2018-04-13.
Downloading the log for 2018-04-14.
Downloading the log for 2018-04-16.
Downloading the log for 2018-04-18.
Downloaded the log for 2018-04-12. The log is available at .\Desktop\rmslog-2018-04-12.log.
Downloaded the log for 2018-04-13. The log is available at .\Desktop\rmslog-2018-04-13.log.
Downloaded the log for 2018-04-14. The log is available at .\Desktop\rmslog-2018-04-14.log.
Downloaded the log for 2018-04-16. The log is available at .\Desktop\rmslog-2018-04-16.log.
Downloaded the log for 2018-04-18. The log is available at .\Desktop\rmslog-2018-04-18.log.
Downloading the log for 2018-04-24.
Downloaded the log for 2018-04-24. The log is available at .\Desktop\rmslog-2018-04-24.log.
```   

### <a name="document-tracking-logs"></a>Journaux de suivi des documents

Exécutez l’applet de commande [AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog) pour récupérer des informations à partir du site de suivi des documents sur un utilisateur spécifique. Pour accéder aux informations de suivi associées aux journaux de document, utilisez l’applet de commande [AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog?view=azureipps) .

Exemple :
```
PS C:\Users> Get-AipServiceDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


ContentId             : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer                : admin@aip500.onmicrosoft.com
Owner                 : admin@aip500.onmicrosoft.com
ContentName           :
CreatedTime           : 3/6/2018 10:24:00 PM
Recipients            : {
                        PrimaryEmail: johndoe@contoso.com
                        DisplayName: JOHNDOE@CONTOSO.COM
                        UserType: External,
                        PrimaryEmail: alice@contoso0110.onmicrosoft.com
                        DisplayName: ALICE@CONTOSO0110.ONMICROSOFT.COM
                        UserType: External
                        }
TemplateId            :
PolicyExpires         :
EULDuration           :
SendRegistrationEmail : True
NotificationInfo      : Enabled: False
                        DeniedOnly: False
                        Culture:
                        TimeZoneId:
                        TimeZoneOffset: 0
                        TimeZoneDaylightName:
                        TimeZoneStandardName:

RevocationInfo        : Revoked: False
                        RevokedTime:
                        RevokedBy:


PS C:\Users> Get-AipServiceTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

ContentId            : 6326fcb2-c465-4c24-a7f6-1cace7a9cb6f
Issuer               : admin@aip500.onmicrosoft.com
RequestTime          : 3/6/2018 10:45:57 PM
RequesterType        : External
RequesterEmail       : johndoe@contoso.com
RequesterDisplayName : johndoe@contoso.com
RequesterLocation    : IP: 167.220.1.54
                       Country: US
                       City: redmond
                       Position: 47.6812453974602,-122.120736471666

Rights               : {VIEW,OBJMODEL}
Successful           : False
IsHiddenInfo         : False
```

Il n’est pas possible d’effectuer des recherches par ObjectID. Toutefois, vous n’êtes pas limité par le paramètre `-UserEmail` et il n’est pas nécessaire que l’adresse e-mail que vous fournissez fasse partie de votre locataire. Si l’adresse e-mail fournie est stockée n’importe où dans les journaux de suivi des documents, l’entrée de suivi de document est retournée dans la sortie de l’applet de commande.

### <a name="usage-logs-for-the-azure-information-protection-clients-and-rms-client"></a>Journaux d’utilisation pour les clients Azure Information Protection et le client RMS

Lorsque des étiquettes et la protection sont appliquées à des documents et des e-mails, les adresses e-mail et les adresses IP peuvent être stockées dans les fichiers journaux sur l’ordinateur d’un utilisateur aux emplacements suivants :

- Pour le client d’étiquetage unifié Azure Information Protection et le client Azure Information Protection :%localappdata%\Microsoft\MSIP\Logs

- Pour le client RMS : %localappdata%\Microsoft\MSIPC\msip\Logs

Par ailleurs, le client Azure Information Protection journalise ces données personnelles dans le journal des événements Windows local **Journaux des applications et des services** > **Azure Information Protection**.

Lorsque le client Azure Information Protection exécute le scanneur, les données personnelles sont enregistrées dans %localappdata%\Microsoft\MSIP\Scanner\Reports sur l’ordinateur Windows Server qui exécute le scanneur.

Pour désactiver la journalisation des informations pour le scanneur et le client Azure Information Protection, utilisez les configurations suivantes :

- Pour le client Azure Information Protection : créez un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#change-the-local-logging-level) qui configure **LogLevel** sur **off**.

- Pour le scanneur Azure Information Protection : utilisez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/set-aipscannerconfiguration) pour définir le paramètre *ReportLevel* sur **off**.

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>Sécurisation et contrôle d’accès aux informations personnelles
Les données personnelles que vous affichez et spécifiez dans le portail Azure sont accessibles uniquement par les utilisateurs ayant reçu l’un des [rôles d’administrateur suivants par Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) :
    
- **Administrateur Azure Information Protection**

- **Administrateur de conformité**

- **Administrateur des données de conformité**

- **Administrateur de sécurité**

- **Lecteur Sécurité**

- **Administrateur général**

- **Lecteur global**

Les données personnelles que vous affichez et spécifiez à l’aide du module AIPService (ou de l’ancien module, AADRM) sont accessibles uniquement aux utilisateurs qui ont reçu les rôles administrateur **Azure information protection**, administrateur de **conformité**, administrateur des **données de conformité**ou administrateur **général** de Azure Active Directory ou le rôle d’administrateur général pour le service de protection.

## <a name="updating-personal-data"></a>Mise à jour des données personnelles

Vous pouvez mettre à jour les adresses e-mail pour les stratégies délimitées et les paramètres de protection dans la stratégie Azure Information Protection. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les paramètres de protection, vous pouvez mettre à jour les mêmes informations à l’aide des applets de commande PowerShell à partir du [module AIPService](/powershell/module/aipservice).

Vous ne pouvez pas mettre à jour les adresses e-mail pour les super utilisateurs et les administrateurs délégués. Vous devez supprimer le compte d’utilisateur spécifié et ajouter le compte d’utilisateur avec l’adresse e-mail mise à jour. 

### <a name="protection-templates"></a>Modèles de protection

Exécutez l’applet de commande [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) pour mettre à jour le modèle de protection. Étant donné que les données personnelles se trouvent dans la propriété `RightsDefinitions`, vous devez également utiliser l’applet de commande [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) pour créer un objet de définitions de droits avec les informations mises à jour, et utiliser l’objet de définitions de droits avec l’applet de commande `Set-AipServiceTemplateProperty`.

### <a name="super-users-and-delegated-administrators-for-the-protection-service"></a>Super utilisateurs et administrateurs délégués pour le service de protection

Lorsque vous avez besoin de mettre à jour une adresse e-mail pour un super utilisateur :

1. Utilisez [Remove-AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser) pour supprimer l’utilisateur et l’ancienne adresse e-mail.

2. Utilisez [Add-AipServiceSuperUser](/powershell/module/aipservice/Add-AipServiceSuperUser) pour ajouter l’utilisateur et une nouvelle adresse e-mail.

Lorsque vous avez besoin de mettre à jour une adresse e-mail pour un administrateur délégué :

1. Utilisez [Remove-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator) pour supprimer l’utilisateur et l’ancienne adresse e-mail.

2. Utilisez [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Add-AipServiceRoleBasedAdministrator) pour ajouter l’utilisateur et une nouvelle adresse e-mail.

## <a name="deleting-personal-data"></a>Suppression des données personnelles
Vous pouvez supprimer les adresses e-mail pour les stratégies délimitées et les paramètres de protection dans la stratégie Azure Information Protection. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les paramètres de protection, vous pouvez supprimer les mêmes informations à l’aide des applets de commande PowerShell du [module AIPService](/powershell/module/aipservice).

Pour supprimer des adresses de messagerie pour les super utilisateurs et les administrateurs délégués, supprimez ces utilisateurs à l’aide de l’applet de commande [Remove-AipServiceSuperUser](/powershell/module/aipservice/Remove-AipServiceSuperUser) et [Remove-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/Remove-AipServiceRoleBasedAdministrator). 

Pour supprimer des données personnelles dans les journaux de suivi des documents, les journaux d’administration ou les journaux d’utilisation pour le service de protection, utilisez la section suivante pour déclencher une demande avec Support Microsoft.

Pour supprimer des données personnelles dans les fichiers journaux du client et les journaux du scanneur stockés sur des ordinateurs, utilisez les outils Windows standard afin de supprimer les fichiers ou les données personnelles dans les fichiers. 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Pour supprimer des données personnelles avec l’aide du support Microsoft

Utilisez les trois étapes suivantes pour demander à Microsoft de supprimer les données personnelles dans les journaux de suivi de document, les journaux d’administration ou les journaux d’utilisation pour le service de protection. 

**Étape 1 : Lancer la demande de suppression**
[Contactez le Support Microsoft](information-support.md#to-contact-microsoft-support) afin qu’il ouvre un dossier de support Azure Information Protection en vue de la suppression de données de votre locataire. Vous devez prouver que vous êtes administrateur de votre locataire Azure Information Protection et comprendre que la confirmation de ce processus prend plusieurs jours. Lors de l’envoi de votre demande, vous devrez fournir des informations supplémentaires en fonction des données qui doivent être supprimées.

- Pour supprimer le journal d’administration, fournissez la **date de fin**. Tous les journaux d’administration jusqu'à cette date de fin seront supprimés.
- Pour supprimer les journaux d’utilisation, fournissez la **date de fin**. Tous les journaux d’utilisation jusqu'à cette date de fin seront supprimés.
- Pour supprimer les journaux de suivi des documents, fournissez l’**e-mail de l’utilisateur** (UserEmail). Toutes les informations de suivi des documents relatives à cet e-mail utilisateur seront supprimées.

La suppression de ces données est irréversible. Il n’existe aucun moyen de récupérer les données après le traitement d’une demande de suppression. Il est recommandé aux administrateurs d’exporter les données requises avant de soumettre une demande de suppression.

**Étape 2 : Attendre la vérification** Microsoft doit vérifier que votre demande de suppression d’un ou plusieurs journaux est légitime. Cela peut prendre jusqu’à cinq jours ouvrés.

**Étape 3 : Obtenir la confirmation de la suppression** Les services de support technique Microsoft (CSS) vous enverront un e-mail de confirmation de la suppression des données. 

## <a name="exporting-personal-data"></a>Exportation des données personnelles
Lorsque vous utilisez les applets de commande PowerShell AIPService ou AADRM, les données personnelles sont rendues disponibles pour la recherche et l’exportation sous la forme d’un objet PowerShell. L’objet PowerShell peut être converti en objet JSON et être enregistré à l’aide de l’applet de commande `ConvertTo-Json`.

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>Restriction de l’utilisation des données personnelles pour le profilage et le marketing sans consentement
Azure Information Protection suit la [déclaration de confidentialité](https://privacy.microsoft.com/privacystatement) Microsoft pour le profilage ou le marketing reposant sur les données personnelles.

## <a name="auditing-and-reporting"></a>Audit et rapports
Seuls les utilisateurs qui ont reçu des [autorisations d’administrateur](#securing-and-controlling-access-to-personal-information) peuvent utiliser le module AIPSERVICE ou addr pour la recherche et l’exportation de données personnelles. Ces opérations sont enregistrées dans le journal d’administration, qui peut ensuite être téléchargé.

Pour les actions de suppression, la demande de support sert de piste d’audit et de création de rapports pour les actions réalisées par Microsoft. Après la suppression, les données supprimées ne sont pas disponibles pour la recherche et l’exportation, et l’administrateur peut vérifier cela à l’aide des applets de commande obtenir du module AIPService.
