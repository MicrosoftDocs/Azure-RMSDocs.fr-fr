---
title: "Actualiser la liste de modèles Azure RMS - AIP"
description: "Quand vous utilisez le service Azure Rights Management, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d’autres étapes si vous apportez des modifications aux modèles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e3f80781c9e998e3d7d0d515ed1b0b13b9656ab4
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="refreshing-templates-for-users"></a>Actualisation des modèles pour les utilisateurs

>*S’applique à : Azure Information Protection, Office 365*

Quand vous utilisez le service Azure Rights Management d’Azure Information Protection, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d'autres étapes si vous apportez des modifications aux modèles :

|Application ou service|Mode d'actualisation des modèles après des modifications|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuration manuelle requise pour actualiser les modèles.<br /><br />Pour connaître les étapes de configuration, consultez la section suivante, [Exchange Online uniquement : Configurer Exchange pour télécharger des modèles personnalisés modifiés](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates).|
|Office 365|Actualisation automatique (aucune étape supplémentaire nécessaire).|
|Office 2016 et Office 2013<br /><br />Application de partage RMS pour Windows|Actualisation automatique (d’après une planification) :<br /><br />Pour ces versions ultérieures d’Office : l’intervalle d’actualisation par défaut est de sept jours.<br /><br />Pour l’application de partage RMS pour Windows : à partir de la version 1.0.1784.0, l’intervalle d’actualisation par défaut est d’une journée. Les versions antérieures ont, par défaut, un intervalle d'actualisation de sept jours.<br /><br />Pour forcer une actualisation avant cette planification, consultez la section suivante, [Office 2016, Office 2013 et application de partage RMS pour Windows : Forcer une actualisation pour un modèle personnalisé modifié](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Actualisation lors de la connexion des utilisateurs.<br /><br />Pour forcer une actualisation, demandez aux utilisateurs de se déconnecter, puis de se reconnecter ou forcez-les à le faire. Ou consultez la section [Office 2010 uniquement : Comment forcer une actualisation d’un modèle personnalisé modifié](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template).|
Pour les appareils mobiles qui utilisent l'application de partage RMS, les modèles sont automatiquement téléchargés (et actualisés au besoin) sans aucune qu'aucune configuration soit requise.

## <a name="exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates"></a>Exchange Online uniquement : Comment configurer Exchange pour télécharger des modèles personnalisés modifiés
Si vous avez déjà configuré la Gestion des droits relatifs à l'information (IRM) pour Exchange Online, les modèles personnalisés ne peuvent pas être téléchargés par les utilisateurs tant que vous n'apportez pas les modifications suivantes à l'aide de Windows PowerShell dans Exchange Online.

> [!NOTE]
> Pour plus d’informations sur l’utilisation de Windows PowerShell dans Exchange Online, consultez [Utilisation de PowerShell avec Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Vous devez suivre cette procédure chaque fois que vous modifiez un modèle.

### <a name="to-update-templates-for-exchange-online"></a>Pour mettre à jour des modèles pour Exchange Online

1.  À l’aide de Windows PowerShell dans Exchange Online, connectez-vous au service :

    1.  Indiquez vos nom d’utilisateur et mot de passe Office 365 :

        ```
        $UserCredential = Get-Credential
        ```

    2.  Connectez-vous au service Exchange Online en exécutant les deux commandes suivantes :

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Utilisez l’applet de commande [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) pour réimporter votre domaine de publication approuvé (TPD) à partir d’Azure RMS :

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Par exemple, si le nom de votre TPD est **RMS Online - 1** (nom par défaut pour de nombreuses organisations), entrez : **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Pour vérifier le nom de votre TPD, vous pouvez utiliser l’applet de commande [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx).

3.  Pour vérifier que les modèles ont été importés correctement, patientez quelques minutes, puis exécutez l’applet de commande [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) et définissez le Type sur All. Exemple :

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Il est utile de conserver une copie de la sortie afin de pouvoir facilement copier les noms ou GUID de modèles si vous archivez un modèle ultérieurement.

4.  Si vous voulez qu’un modèle importé soit disponible dans Outlook Web App, vous devez utiliser l’applet de commande [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) et définir le Type sur Distributed :

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Outlook Web Access mettant en cache l’interface utilisateur pendant 24 heures, il se peut que les utilisateurs ne voient pas le nouveau modèle avant un jour.

De plus, si vous archivez un modèle (personnalisé ou par défaut) et utilisez Exchange Online avec Office 365, les utilisateurs vont continuer de voir les modèles archivés s'ils utilisent Outlook Web App ou des appareils mobiles qui utilisent le protocole Exchange ActiveSync.

Pour que les utilisateurs ne voient plus ces modèles, connectez-vous au service à l’aide de Windows PowerShell dans Exchange Online, puis utilisez l’applet de commande [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) en exécutant la commande suivante :

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

## <a name="office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template"></a>Office 2016, Office 2013 et application de partage RMS pour Windows : Forcer une actualisation pour un modèle personnalisé modifié
En modifiant le Registre sur les ordinateurs exécutant Office 2016, Office 2013 ou l'application de partage Rights Management (RMS) pour Windows, vous pouvez modifier la planification automatique afin que les modèles modifiés soient actualisés sur les ordinateurs à une fréquence supérieure à la fréquence par défaut. Vous pouvez également forcer une actualisation immédiate en supprimant les données existantes dans une valeur de registre.

> [!WARNING]
> Si vous n'utilisez pas l'Éditeur du Registre correctement, vous risquez de provoquer de sérieux problèmes pouvant vous amener à devoir réinstaller le système d'exploitation. Microsoft ne peut pas garantir la résolution des problèmes engendrés par une utilisation incorrecte de l'Éditeur du Registre. Utilisez l’Éditeur du Registre à vos propres risques.

### <a name="to-change-the-automatic-schedule"></a>Pour modifier la planification automatique

1.  Dans l'un Éditeur du Registre, créez et définissez l'une des valeurs de Registre suivantes :

    - Pour définir une fréquence de mise à jour en jours (au moins 1 jour) :  créez une valeur de Registre nommée **TemplateUpdateFrequency**, et définissez une valeur entière pour les données, spécifiant la fréquence en jours de téléchargement des modifications dans un modèle téléchargé. Utilisez les informations suivantes pour rechercher le chemin du Registre pour créer cette nouvelle valeur de Registre.

        **Chemin de Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type :** REG_DWORD

        **Valeur** : TemplateUpdateFrequency

    - Pour définir une fréquence de mise à jour en secondes (au moins 1 seconde) :  créez une valeur de Registre nommée **TemplateUpdateFrequencyInSeconds**, et définissez une valeur entière pour les données, spécifiant la fréquence en secondes de téléchargement des modifications dans un modèle téléchargé. Utilisez les informations suivantes pour rechercher le chemin du Registre pour créer cette nouvelle valeur de Registre.

        **Chemin de Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type :** REG_DWORD

        **Valeur :** TemplateUpdateFrequencyInSeconds

    Assurez-vous que vous créez et définissez l'une de ces valeurs de Registre, pas les deux. Si les deux sont présentes, **TemplateUpdateFrequency** est ignoré.

2.  Si vous souhaitez forcer une actualisation immédiate des modèles, passez à la procédure suivante. Dans le cas contraire, redémarrez maintenant vos applications et instances Office de l'Explorateur de fichiers.

### <a name="to-force-an-immediate-refresh"></a>Pour forcer une actualisation immédiate

1.  À l’aide d’un éditeur du Registre, supprimez les données de la valeur **LastUpdatedTime**. Par exemple, les données peuvent afficher **2015-04-20T15:52**. Supprimez 2015-04-20T15:52 pour qu’aucune donnée ne s’affiche. Utilisez les informations suivantes pour rechercher le chemin de Registre et supprimer ces données de valeur de Registre.

    **Chemin de Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **Type :** REG_SZ

    **Valeur** : LastUpdatedTime

    > [!TIP]
        > Dans le chemin de Registre, *<MicrosoftRMS_FQDN>* fait référence au nom de domaine complet de votre service Microsoft RMS. Si vous souhaitez vérifier cette valeur :

    > 1.  Exécutez l’applet de commande [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS. Si vous n’avez pas encore installé le module Windows PowerShell pour Azure RMS, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).
    > 2.  Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.
    > 
    >     Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  Dans la valeur, supprimez **https://** et **/_wmcs/licensing** de cette chaîne. La valeur restante est votre nom de domaine complet (FQDN) du service Microsoft RMS. Dans notre exemple, le nom de domaine complet (FQDN) du service Microsoft RMS a la valeur suivante :
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Supprimez le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3.  Redémarrez vos applications Office et les instances de l'Explorateur de fichiers.

## <a name="office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template"></a>Office 2010 uniquement : Forcer une actualisation pour un modèle personnalisé modifié
En modifiant le Registre sur les ordinateurs qui exécutent Office 2010, vous pouvez définir une valeur de façon à ce que les modèles modifiés soient actualisés sur les ordinateurs sans attendre que les utilisateurs se déconnectent, puis se reconnectent. Vous pouvez également forcer une actualisation immédiate en supprimant les données existantes dans une valeur de registre.

> [!WARNING]
> Si vous n'utilisez pas l'Éditeur du Registre correctement, vous risquez de provoquer de sérieux problèmes pouvant vous amener à devoir réinstaller le système d'exploitation. Microsoft ne peut pas garantir la résolution des problèmes engendrés par une utilisation incorrecte de l'Éditeur du Registre. Utilisez l’Éditeur du Registre à vos propres risques.

### <a name="to-change-the-update-frequency"></a>Pour modifier la fréquence de mise à jour

1.  À l'aide d'un éditeur du Registre, créez une nouvelle valeur de Registre nommée **UpdateFrequency** et définir une valeur entière pour les données, qui spécifiant la fréquence en jours pour télécharger les modifications dans un modèle téléchargé. Utilisez le tableau suivant pour rechercher le chemin d'accès du Registre afin de créer cette nouvelle valeur de Registre.

    **Chemin de Registre :** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Type :** REG_DWORD

    **Valeur** : UpdateFrequency

2.  Si vous souhaitez forcer une actualisation immédiate des modèles, passez à la procédure suivante. Dans le cas contraire, redémarrez vos applications Office.

### <a name="to-force-an-immediate-refresh"></a>Pour forcer une actualisation immédiate

1.  À l’aide d’un éditeur du Registre, supprimez les données de la valeur **LastUpdatedTime**. Par exemple, les données peuvent afficher **2015-04-20T15:52**. Supprimez 2015-04-20T15:52 pour qu’aucune donnée ne s’affiche. Utilisez le tableau suivant pour rechercher le chemin d’accès du registre pour supprimer cette valeur de registre.

    **Chemin de Registre :** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **Type :** REG_SZ

    **Valeur** : LastUpdatedTime


2.  Supprimez le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3.  Redémarrez vos applications Office.

## <a name="see-also"></a>Voir aussi
[Configurer des modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]