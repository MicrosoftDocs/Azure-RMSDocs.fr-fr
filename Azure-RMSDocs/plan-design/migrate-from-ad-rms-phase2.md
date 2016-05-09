---
# required metadata

title: Migration d’AD RMS vers Azure Rights Management - Phase 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Phase de migration 2 - Configuration côté client
Utilisez les informations suivantes pour la Phase 2 de la migration d’AD RMS vers Azure Rights Management (Azure RMS). Ces procédures couvrent l’étape 5 de [Migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Étape 5. Reconfigurer les clients pour utiliser Azure RMS
Pour des clients Windows :

1.  [Téléchargez les scripts de migration](http://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Ces scripts réinitialisent la configuration sur des ordinateurs Windows afin qu'ils utilisent le service RMS Azure plutôt qu'AD RMS.

2.  Suivez les instructions du script de redirection (Redirect_OnPrem.cmd) pour modifier celui-ci pour qu’il pointe vers votre nouveau locataire Azure RMS.

3.  Sur les ordinateurs Windows, exécutez ces scripts avec des privilèges élevés dans le contexte de l'utilisateur.

Pour des clients appareils mobiles et des ordinateurs Mac :

-   Supprimez les enregistrements SRV DNS que vous avez créés lors du déploiement de l’ [extension d'appareil mobile AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### Modifications apportées par les scripts de migration
Cette section décrit les modifications apportées par les scripts de migration. Vous pouvez utiliser ces informations uniquement à des fins de référence ou de dépannage, ou si vous voulez apporter personnellement ces modifications.

CleanUpRMS_RUN_Elevated.cmd :

-   Supprimez le contenu des dossiers %userprofile%\AppData\Local\Microsoft\DRM et %userprofile%\AppData\Local\Microsoft\MSIPC, y compris les sous-dossiers et fichiers portant un nom long.

-   Supprimez le contenu des clés de Registre suivantes :

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   Supprimez les valeurs de Registre suivantes :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd :

-   Créez les valeurs de Registre suivantes pour chaque URL fournie en tant que paramètre sous chacun des emplacements suivants :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Chaque entrée a une valeur REG_SZ **https://OldRMSserverURL/_wmcs/licensing**, dont les données sont au format suivant : **https://&lt;URL_votre_locataire&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;URL_votre_locataire&gt;* a le format suivant : **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Par exemple : 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Vous pouvez trouver cette valeur en identifiant la valeur **RightsManagementServiceId** lorsque vous exécutez l'applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS.


## Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 3 : Configuration des services de prise en charge](migrate-from-ad-rms-phase3.md).

<!--HONumber=Apr16_HO3-->


