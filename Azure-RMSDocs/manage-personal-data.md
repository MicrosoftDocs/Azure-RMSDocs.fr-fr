---
title: Gérer les données personnelles pour Azure Information Protection
description: Informations sur les données personnelles qui sont utilisées par Azure Information Protection et sur la manière de les afficher, les exporter et les supprimer.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 99a51862-83e9-4a1e-873a-a84ae1465f07
ms.reviewer: aashishr
ms.suite: ems
ms.openlocfilehash: 08ae5875437a1e443247a5a57b1bb621b6627ce3
ms.sourcegitcommit: cf52083dde756ad3620c05fc74f012d8a7abacf3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898781"
---
# <a name="manage-personal-data-for-azure-information-protection"></a>Gérer les données personnelles pour Azure Information Protection

Lorsque vous configurez et utilisez Azure Information Protection, les adresses e-mail et les adresses IP sont stockées et utilisées par le service Azure Information Protection. Ces données personnelles se trouvent dans les éléments suivants :

- Stratégie Azure Information Protection

- Modèles de protection du service Azure Rights Management

- Super utilisateurs et administrateurs délégués du service Azure Rights Management 

- Journaux d’administration du service Azure Rights Management

- Journaux d’utilisation du service Azure Rights Management

- Journaux de suivi des documents

- Journaux d’utilisation du client Azure Information Protection et du client RMS 


[!INCLUDE [GDPR-related guidance](./includes/gdpr-intro-sentence.md)]


## <a name="viewing-personal-data-that-azure-information-protection-uses"></a>Affichage des données personnelles utilisées par Azure Information Protection

À l’aide du portail Azure, un administrateur peut spécifier des adresses e-mail pour les stratégies délimitées et les paramètres de protection dans une configuration d’étiquette. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les étiquettes configurées de sorte à appliquer une protection à partir du service Azure Rights Management, il est aussi possible de trouver les adresses e-mail dans les modèles de protection à l’aide des applets de commande PowerShell du [module AADRM](/powershell/module/aadrm). Ce module PowerShell permet également à un administrateur de désigner par adresse e-mail les utilisateurs qui ont le rôle de [super utilisateur](configure-super-users.md) ou d’administrateur pour le service Azure Rights Management. 

Quand Azure Information Protection est utilisé pour classifier et protéger des documents et des e-mails, les adresses e-mail et les adresses IP des utilisateurs peuvent être enregistrées dans des fichiers journaux.


### <a name="protection-templates"></a>Modèles de protection

Exécutez l’applet de commande [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) pour obtenir une liste des modèles de protection. Vous pouvez utiliser l’ID de modèle pour obtenir des informations détaillées sur un modèle spécifique. L’objet `RightsDefinitions` affiche les données personnelles, le cas échéant. 

Exemple :
```
PS C:\Users> Get-AadrmTemplate -TemplateId fcdbbc36-1f48-48ca-887f-265ee1268f51 | select *


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

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Super utilisateurs et administrateurs délégués du service Azure Rights Management

Exécutez les applets de commande [Get-AadrmSuperUser](/powershell/module/aadrm/get-aadrmsuperuser) et [Get-AadrmRoleBasedAdministrator](/powershell/module/aadrm/get-aadrmrolebasedadministrator) pour voir quels utilisateurs ont reçu le rôle de super utilisateur ou d’administrateur général pour le service Azure Rights Management. L’adresse e-mail des utilisateurs ayant reçu l’un de ces rôles est affichée.


### <a name="administration-logs-for-the-azure-rights-management-service"></a>Journaux d’administration du service Azure Rights Management

Exécutez l’applet de commande [Get-AadrmAdminLog](/powershell/module/aadrm/get-aadrmadminlog) afin d’obtenir un journal des actions d’administration pour le service Azure Rights Management, lequel protège les données pour Azure Information Protection. Ce journal contient des données personnelles sous la forme d’adresses e-mail et d’adresses IP. Le journal est en texte clair et une fois téléchargé, les détails d’un administrateur spécifique peuvent être recherchés hors connexion.

Par exemple :
```
PS C:\Users> Get-AadrmAdminLog -Path '.\Desktop\admin.log' -FromTime 4/1/2018 -ToTime 4/30/2018 -Verbose
The Rights Management administration log was successfully generated and can be found at .\Desktop\admin.log.
```

### <a name="usage-logs-for-the-azure-rights-management-service"></a>Journaux d’utilisation du service Azure Rights Management
Exécutez l’applet de commande [Get-AadrmUserLog](/powershell/module/aadrm/get-aadrmuserlog) pour récupérer un journal des actions de l’utilisateur final qui utilisent le service Azure Rights Management. Ce service protège les données pour Azure Information Protection. Le journal peut inclure des données personnelles sous la forme d’adresses e-mail et d’adresses IP. Le journal est en texte clair et une fois téléchargé, les détails d’un administrateur spécifique peuvent être recherchés hors connexion.

Par exemple :
```
PS C:\Users> Get-AadrmUserLog -Path '.\Desktop\' -FromDate 4/1/2018 -ToDate 4/30/2018 -NumberOfThreads 10
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

Exécutez l’applet de commande [Get-AadrmDocumentLog](/powershell/module/aadrm/get-aadrmdocumentlog) pour récupérer des informations sur un utilisateur spécifique à partir du site de suivi de document. Pour obtenir les informations de suivi associées aux journaux de documents, utilisez l’applet de commande [Get-AadrmTrackingLog](/powershell/module/aadrm/get-aadrmtrackinglog?view=azureipps).

Par exemple :
```
PS C:\Users> Get-AadrmDocumentLog -UserEmail "admin@aip500.onmicrosoft.com"


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


PS C:\Users> Get-AadrmTrackingLog -UserEmail "admin@aip500.onmicrosoft.com"

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

### <a name="usage-logs-for-the-azure-information-protection-client-and-rms-client"></a>Journaux d’utilisation du client Azure Information Protection et du client RMS

Lorsque des étiquettes et la protection sont appliquées à des documents et des e-mails, les adresses e-mail et les adresses IP peuvent être stockées dans les fichiers journaux sur l’ordinateur d’un utilisateur aux emplacements suivants :

- Pour le client Azure Information Protection : %localappdata%\Microsoft\MSIP\Logs

- Pour le client RMS : %localappdata%\Microsoft\MSIPC\msip\Logs

Par ailleurs, le client Azure Information Protection journalise ces données personnelles dans le journal des événements Windows local **Journaux des applications et des services** > **Azure Information Protection**.

Lorsque le client Azure Information Protection exécute le scanneur, les données personnelles sont enregistrées dans %localappdata%\Microsoft\MSIP\Scanner\Reports sur l’ordinateur Windows Server qui exécute le scanneur.

Pour désactiver la journalisation des informations pour le scanneur et le client Azure Information Protection, utilisez les configurations suivantes :

- Pour le client Azure Information Protection : créez un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#change-the-local-logging-level) qui configure **LogLevel** sur **Désactivé**.

- Pour le scanneur Azure Information Protection : utilisez la cmdlet [Set-AIPScannerConfiguration](/azureinformationprotection/set-aipscannerconfiguration) pour définir le paramètre *ReportLevel* sur **Désactivé**.

[!INCLUDE [GDPR-related guidance](./includes/gdpr-hybrid-note.md)]

## <a name="securing-and-controlling-access-to-personal-information"></a>Sécurisation et contrôle d’accès aux informations personnelles
Les données personnelles que vous affichez et spécifiez dans le portail Azure sont accessibles uniquement par les utilisateurs ayant reçu l’un des [rôles d’administrateur suivants par Azure Active Directory](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) :
    
- **Administrateur Information Protection**

- **Administrateur de sécurité**

- **Administrateur général/administrateur de la société**

Les données personnelles que vous affichez et spécifiez à l’aide du module AADRM sont accessibles uniquement par les utilisateurs ayant reçu le rôle **administrateur Information Protection** ou les rôles **Administrateur général/administrateur de la société** par Azure Active Directory, ou le rôle d’administrateur global pour le service Azure Rights Management.  

## <a name="updating-personal-data"></a>Mise à jour des données personnelles

Vous pouvez mettre à jour les adresses e-mail pour les stratégies délimitées et les paramètres de protection dans la stratégie Azure Information Protection. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les paramètres de protection, vous pouvez mettre à jour ces mêmes informations à l’aide des applets de commande PowerShell du [module AADRM](/powershell/module/aadrm).

Vous ne pouvez pas mettre à jour les adresses e-mail pour les super utilisateurs et les administrateurs délégués. Vous devez supprimer le compte d’utilisateur spécifié et ajouter le compte d’utilisateur avec l’adresse e-mail mise à jour. 

### <a name="protection-templates"></a>Modèles de protection

Exécutez l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) pour mettre à jour le modèle de protection. Les données personnelles se trouvant dans la propriété `RightsDefinitions`, vous devez également utiliser l’applet de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) pour créer un objet RightsDefinitions avec les informations mises à jour et utiliser l’objet RightsDefinitions avec l’applet de commande `Set-AadrmTemplateProperty`.

### <a name="super-users-and-delegated-administrators-for-the-azure-rights-management-service"></a>Super utilisateurs et administrateurs délégués du service Azure Rights Management

Lorsque vous avez besoin de mettre à jour une adresse e-mail pour un super utilisateur :

1. Utilisez [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) pour supprimer l’utilisateur et l’ancienne adresse e-mail.

2. Utilisez [Add-AadrmSuperUser](/powershell/module/aadrm/Add-AadrmSuperUser) pour ajouter l’utilisateur et la nouvelle adresse e-mail.

Lorsque vous avez besoin de mettre à jour une adresse e-mail pour un administrateur délégué :

1. Utilisez [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator) pour supprimer l’utilisateur et l’ancienne adresse e-mail.

2. Utilisez [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Add-AadrmRoleBasedAdministrator) pour ajouter l’utilisateur et la nouvelle adresse e-mail.

## <a name="deleting-personal-data"></a>Suppression des données personnelles
Vous pouvez supprimer les adresses e-mail pour les stratégies délimitées et les paramètres de protection dans la stratégie Azure Information Protection. Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md) et [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md). 

Pour les paramètres de protection, vous pouvez supprimer ces mêmes informations à l’aide des applets de commande PowerShell du [module AADRM](/powershell/module/aadrm).

Pour supprimer des adresses e-mail pour les super utilisateurs et les administrateurs délégués, supprimez ces utilisateurs à l’aide des applets de commande [Remove-AadrmSuperUser](/powershell/module/aadrm/Remove-AadrmSuperUser) et [Remove-AadrmRoleBasedAdministrator](/powershell/module/aadrm/Remove-AadrmRoleBasedAdministrator). 

Pour supprimer des données personnelles dans les journaux de suivi des documents, les journaux d’administration ou les journaux d’utilisation du service Azure Rights Management, utilisez la section suivante pour formuler une demande auprès du support Microsoft.

Pour supprimer des données personnelles dans les fichiers journaux du client et les journaux du scanneur stockés sur des ordinateurs, utilisez les outils Windows standard afin de supprimer les fichiers ou les données personnelles dans les fichiers. 

### <a name="to-delete-personal-data-with-microsoft-support"></a>Pour supprimer des données personnelles avec l’aide du support Microsoft

Utilisez les trois étapes suivantes pour demander à Microsoft de supprimer des données personnelles dans les journaux de suivi des documents, les journaux d’administration ou les journaux d’utilisation du service Azure Rights Management. 

**Étape 1 : Lancer la demande de suppression**
[Contactez le Support Microsoft](information-support.md#to-contact-microsoft-support) afin qu’il ouvre un dossier de support Azure Information Protection en vue de la suppression de données de votre locataire. Vous devez prouver que vous êtes administrateur de votre locataire Azure Information Protection et comprendre que la confirmation de ce processus prend plusieurs jours. Lors de l’envoi de votre demande, vous devrez fournir des informations supplémentaires en fonction des données qui doivent être supprimées.

- Pour supprimer le journal d’administration, fournissez la **date de fin**. Tous les journaux d’administration jusqu'à cette date de fin seront supprimés.
- Pour supprimer les journaux d’utilisation, fournissez la **date de fin**. Tous les journaux d’utilisation jusqu'à cette date de fin seront supprimés.
- Pour supprimer les journaux de suivi des documents, fournissez l’**e-mail de l’utilisateur** (UserEmail). Toutes les informations de suivi des documents relatives à cet e-mail utilisateur seront supprimées.

La suppression de ces données est irréversible. Il n’existe aucun moyen de récupérer les données après le traitement d’une demande de suppression. Il est recommandé aux administrateurs d’exporter les données requises avant de soumettre une demande de suppression.

**Étape 2 : Attendre la vérification** Microsoft doit vérifier que votre demande de suppression d’un ou plusieurs journaux est légitime. Cela peut prendre jusqu’à cinq jours ouvrés.

**Étape 3 : Obtenir la confirmation de la suppression** Les services de support technique Microsoft vous enverront un e-mail de confirmation de la suppression des données. 

## <a name="exporting-personal-data"></a>Exportation des données personnelles
Lorsque vous utilisez les applets de commande PowerShell du module AADRM, les données personnelles sont disponibles pour la recherche et l’exportation en tant qu’objet PowerShell. L’objet PowerShell peut être converti en objet JSON et être enregistré à l’aide de l’applet de commande `ConvertTo-Json`.

## <a name="restricting-the-use-of-personal-data-for-profiling-or-marketing-without-consent"></a>Restriction de l’utilisation des données personnelles pour le profilage et le marketing sans consentement
Azure Information Protection suit la [déclaration de confidentialité](https://privacy.microsoft.com/privacystatement) Microsoft pour le profilage ou le marketing reposant sur les données personnelles.

## <a name="auditing-and-reporting"></a>Audit et rapports
Seuls les utilisateurs ayant reçu des [autorisations d’administrateur](#securing-and-controlling-access-to-personal-information) peuvent utiliser le module AADRM pour la recherche et l’exportation de données personnelles. Ces opérations sont enregistrées dans le journal d’administration, qui peut ensuite être téléchargé.

Pour les actions de suppression, la demande de support sert de piste d’audit et de création de rapports pour les actions réalisées par Microsoft. Une fois supprimées, les données ne sont plus disponibles pour la recherche et l’exportation, ce qui peut-être vérifié par l’administrateur à l’aide des applets de commande Get du module AADRM.

