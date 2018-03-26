---
title: Actualiser la liste de modèles Azure RMS - AIP
description: Quand vous utilisez le service Azure Rights Management, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d’autres étapes si vous apportez des modifications aux modèles.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/16/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0f3c7f45789339aca0186ad2855c2e25f931182f
ms.sourcegitcommit: 758e0cfeb6c05f4c6f5310dc36fbf0c02c256eed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/17/2018
---
# <a name="refreshing-templates-for-users-and-services"></a>Actualisation des modèles pour les utilisateurs et services

>*S’applique à : Azure Information Protection, Office 365*

Quand vous utilisez le service Azure Rights Management d’Azure Information Protection, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d'autres étapes si vous apportez des modifications aux modèles :

|Application ou service|Mode d'actualisation des modèles après des modifications|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />Applicable aux règles de transport et à Outlook Web App |Actualisé automatiquement dans l’heure (aucune étape supplémentaire nécessaire).<br /><br />C’est le cas si vous utilisez le [chiffrement de messages Office 365 avec les nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Si vous avez configuré Exchange Online pour l’utilisation du service Azure Rights Management en important votre domaine de publication approuvé, utilisez le même ensemble d’instructions pour activer les nouvelles fonctionnalités dans Exchange Online.|
|Client Azure Information Protection|Actualisation automatique chaque fois que la stratégie Azure Information Protection est actualisée sur le client :<br /><br /> - Lorsqu’une application Office qui prend en charge la barre Azure Information Protection s’ouvre. <br /><br /> - Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier. <br /><br /> - Lorsque vous exécutez les applets de commande PowerShell pour l’étiquetage et la protection (Get-AIPFileStatus et Set-AIPFileLabel).<br /><br /> - Lorsque le service du scanneur Azure Information Protection démarre et que la stratégie locale remonte à plus d’une heure. De plus, le service du scanneur vérifie les modifications apportées toutes les heures et utilise ces modifications pour le prochain cycle d’analyse.<br /><br /> - Toutes les 24 heures.<br /><br /> En outre, étant donné que le client Azure Information Protection est étroitement intégré à Office, les modèles actualisés pour Office 2016 ou Office 2013 le seront aussi pour le client Azure Information Protection.|
|Office 2016 et Office 2013<br /><br />Application de partage RMS pour Windows|Actualisation automatique (d’après une planification) :<br /><br />- Pour ces versions ultérieures d’Office : l’intervalle d’actualisation par défaut est de sept jours.<br /><br />- Pour l’application de partage RMS pour Windows : à partir de la version 1.0.1784.0, l’intervalle d’actualisation par défaut est d’une journée. Les versions antérieures ont, par défaut, un intervalle d'actualisation de sept jours.<br /><br />Pour forcer une actualisation avant la planification, consultez la section [Office 2016, Office 2013 et application de partage RMS pour Windows : Forcer une actualisation pour un modèle personnalisé modifié](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Actualisation automatique lorsque les utilisateurs se déconnectent de Windows, se reconnectent et attendent jusqu'à une heure.|
|Exchange sur site avec le connecteur Azure Rights Management<br /><br />Applicable aux règles de transport et à Outlook Web App|Actualisation automatique (aucune étape supplémentaire nécessaire). Toutefois, Outlook Web App met l’interface utilisateur en cache pendant un jour.|
|Office 2016 pour Mac|Actualisation automatique (aucune étape supplémentaire nécessaire).|
|Application de partage RMS pour les ordinateurs Mac|Actualisation automatique (aucune étape supplémentaire nécessaire).|

Lorsque les applications client ont besoin de télécharger des modèles (initialement ou actualisés pour des modifications), préparez-vous à attendre pendant jusqu'à 15 minutes avant que le téléchargement soit terminé et que les modèles nouveaux ou mis à jour soient entièrement opérationnels. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration du modèle et la connectivité réseau. 

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

    **Chemin de Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*user_alias*>

    **Type :** REG_SZ

    **Valeur** : LastUpdatedTime

    > [!TIP]
    > Dans le chemin de Registre, *<MicrosoftRMS_FQDN>* fait référence au nom de domaine complet de votre service Microsoft RMS. Si vous souhaitez vérifier cette valeur :

    > Exécutez l’applet de commande [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS. Si vous n’avez pas encore installé le module Windows PowerShell pour Azure RMS, consultez [Installation du module PowerShell AADRM](install-powershell.md).
    >
    > Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.
    >
    > Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 
    > Dans la valeur, supprimez **https://** et **/_wmcs/licensing** de cette chaîne. La valeur restante est votre nom de domaine complet (FQDN) du service Microsoft RMS. Dans notre exemple, le nom de domaine complet (FQDN) du service Microsoft RMS a la valeur suivante :
    >
    >**5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Supprimez le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3.  Redémarrez vos applications Office et les instances de l'Explorateur de fichiers.


## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles dans la stratégie Azure Information Protection](../deploy-use/configure-policy-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
