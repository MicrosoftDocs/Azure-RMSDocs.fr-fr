---
title: "Migrer un déploiement AD RMS vers Azure Information Protection - Phase 2"
description: "Phase 2 de la migration d’AD RMS vers Azure Information Protection, couvrant l’étape 5 de la migration d’AD RMS vers Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6e3f0bf46886c27620f8b7c836d0c67aafb61d37
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-2---client-side-configuration"></a>Phase de migration 2 - Configuration côté client

>*S’applique à : Services AD RMS, Azure Information Protection, Office 365*

Utilisez les informations suivantes pour la Phase 2 de la migration d’AD RMS vers Azure Information Protection. Ces procédures couvrent l’étape 5 de la rubrique [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-5-reconfigure-clients-to-use-azure-information-protection"></a>Étape 5. Reconfigurer les clients pour utiliser Azure Information Protection
Pour des clients Windows :

1.  [Téléchargez les scripts de migration](https://go.microsoft.com/fwlink/?LinkId=524619) :

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    Ces scripts réinitialisent la configuration sur des ordinateurs Windows afin qu’ils utilisent le service Azure Information Protection plutôt qu’AD RMS.

2.  Suivez les instructions du script de redirection (Redirect_OnPrem.cmd) pour modifier celui-ci pour qu’il pointe vers votre nouveau locataire Azure Information Protection.

    > [!IMPORTANT]
    > Les instructions incluent le remplacement des exemples d’adresses **adrms** et **adrms.contoso.com** par les adresses de vos propres serveurs AD RMS. Quand vous effectuez cette opération, vérifiez qu’il n’y a pas d’espaces supplémentaires avant ou après vos adresses ; ces derniers engendreraient une interruption du script de migration et il serait très difficile de les identifier comme étant à l’origine du problème. Certains outils d’édition ajoutent automatiquement un espace après le collage du texte.
    >
    > De plus, si vos serveurs AD RMS utilisent des certificats de serveur SSL/TLS, vérifiez si les valeurs des URL de licence incluent le numéro de port **443** dans la chaîne. Par exemple : https:// rms.treyresearch.net:443/_wmcs/licensing. Ces informations sont disponibles dans la console Active Directory Rights Management Services quand vous cliquez sur le nom du cluster et que vous consultez les informations **Détails du cluster**. Si vous voyez le numéro de port 443 dans l’URL, incluez cette valeur quand vous modifiez le script. Par exemple, https://rms.treyresearch.net**:443**.

3. Si les utilisateurs disposent d’Office 2016 : Les scripts ne sont pas encore mis à jour pour inclure la configuration pour Office 2016 ; donc, si les utilisateurs disposent de cette version d’Office, vous devez manuellement mettre à jour les scripts :

    - Pour **CleanUpRMS.cmd** : recherchez la ligne `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` et immédiatement en dessous, ajoutez la ligne suivante :

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - Pour **Redirect_Onprem.cmd** : recherchez la ligne `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F` et immédiatement en dessous, ajoutez les deux lignes suivantes :

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    Facultatif : Les scripts ne référencent pas Office 2016 dans les commentaires. Si vous souhaitez mettre à jour les commentaires pour refléter ces ajouts pour Office 2016, apportez les modifications suivantes à **Redirect_Onprem.cmd** :

    - Recherchez `::     or MSIPC (Office 2013) with on-premises AD RMS` et remplacez-le par le code suivant :
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - Recherchez `echo Redirect SCP for Office 2013` et remplacez-le par le code suivant :
    
            echo Redirect SCP for Office versions based on MSIPC

    - Recherchez `echo Redirect MSIPC for Office 2013` et remplacez-le par le code suivant :
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  Sur les Ordinateurs Windows :

    - Exécutez ces scripts avec des privilèges élevés dans le contexte de l'utilisateur.

    Pour des clients appareils mobiles et des ordinateurs Mac :

    -  Supprimez les enregistrements SRV DNS que vous avez créés lors du déploiement de l’ [extension d'appareil mobile AD RMS](http://technet.microsoft.com/library/dn673574.aspx).

#### <a name="changes-made-by-the-migration-scripts"></a>Modifications apportées par les scripts de migration
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

-   Ajoutez les valeurs de Registre suivantes :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd :

-   Créez les valeurs de Registre suivantes pour chaque URL fournie en tant que paramètre sous chacun des emplacements suivants :

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    Chaque entrée a une valeur REG_SZ **https://URL_ancien_serveur_RMS/_wmcs/licensing**, dont les données sont au format suivant : **https://&lt;URL_votre_client&gt;/_wmcs/licensing**.

    > [!NOTE]
    > *&lt;URL_votre_client&gt;* a le format suivant : **{GUID}.rms.[Region].aadrm.com**.
    > 
    > Par exemple : 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Vous pouvez trouver cette valeur en identifiant la valeur **RightsManagementServiceId** lorsque vous exécutez l'applet de commande [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS.


## <a name="next-steps"></a>Étapes suivantes
Pour poursuivre la migration, passez à la [Phase 3 : Configuration des services de prise en charge](migrate-from-ad-rms-phase3.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]