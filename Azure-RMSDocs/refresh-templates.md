---
title: Actualiser la liste de modèles Azure RMS - AIP
description: Quand vous utilisez le service Azure Rights Management, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d’autres étapes si vous apportez des modifications aux modèles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5939869dd421899a4b929b262e8a18790debaf5c
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535075"
---
# <a name="refreshing-templates-for-users-and-services"></a>Actualisation des modèles pour les utilisateurs et services

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Quand vous utilisez le service Azure Rights Management d’Azure Information Protection, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner à partir de leurs applications. En revanche, vous devrez peut-être effectuer d'autres étapes si vous apportez des modifications aux modèles :

|Application ou service|Mode d'actualisation des modèles après des modifications|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />Applicable aux règles de transport et à Outlook Web App |Actualisé automatiquement dans l’heure (aucune étape supplémentaire nécessaire).<br /><br />C’est le cas si vous utilisez le [chiffrement de messages Office 365 avec les nouvelles fonctionnalités](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Si vous avez configuré Exchange Online pour l’utilisation du service Azure Rights Management en important votre domaine de publication approuvé, utilisez le même ensemble d’instructions pour activer les nouvelles fonctionnalités dans Exchange Online.|
|Client Azure Information Protection|Actualisation automatique chaque fois que la stratégie Azure Information Protection est actualisée sur le client :<br /><br /> - Lorsqu’une application Office qui prend en charge la barre Azure Information Protection s’ouvre. <br /><br /> - Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier. <br /><br /> - Lorsque vous exécutez les applets de commande PowerShell pour l’étiquetage et la protection (Get-AIPFileStatus et Set-AIPFileLabel).<br /><br /> - Lorsque le service du scanneur Azure Information Protection démarre et que la stratégie locale remonte à plus d’une heure. De plus, le service du scanneur vérifie les modifications apportées toutes les heures et utilise ces modifications pour le prochain cycle d’analyse.<br /><br /> - Toutes les 24 heures.<br /><br /> De plus, étant donné que ce client est étroitement intégré à Office, les modèles actualisés pour les applications Office 365 ou pour Office 2019, Office 2016 ou Office 2013 le seront aussi pour le client Azure Information Protection.|
|Client d’étiquetage unifié Azure Information Protection|Actualisé automatiquement toutes les 4 heures par l’application Office.<br /><br /> De plus, étant donné que ce client est étroitement intégré à Office, les modèles actualisés pour les applications Office 365 ou pour Office 2019, Office 2016 ou Office 2013 le seront aussi pour le client d’étiquetage unifié Azure Information Protection.|
|Applications Office 365, Office 2019, Office 2016 et Office 2013|Actualisation automatique (d’après une planification) :<br /><br />- Pour ces versions ultérieures d’Office : L’intervalle d’actualisation par défaut est de sept jours.<br /><br />Pour forcer une actualisation avant la planification, consultez la section [Applications Office 365, Office 2019, Office 2016 et Office 2013 : Forcer une actualisation pour un modèle personnalisé modifié](#office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Actualisation automatique lorsque les utilisateurs se déconnectent de Windows, se reconnectent et attendent jusqu'à une heure.|
|Exchange sur site avec le connecteur Azure Rights Management<br /><br />Applicable aux règles de transport et à Outlook Web App|Actualisation automatique (aucune étape supplémentaire nécessaire). Toutefois, Outlook Web App met l’interface utilisateur en cache pendant un jour.|
|Office 2019 pour Mac et Office 2016 pour Mac|Actualisation automatique (aucune étape supplémentaire nécessaire).|
|Application de partage RMS pour les ordinateurs Mac|Actualisation automatique (aucune étape supplémentaire nécessaire).|
|Applications Office qui [prennent en charge la fonctionnalité Niveau de confidentialité](https://support.office.com/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US&ui=en-US&rs=en-US#bkmk_whereavailable)|Ces clients ne téléchargent pas les modèles mais y accèdent en ligne, donc aucune étape supplémentaire n’est nécessaire.|

Lorsque les applications client ont besoin de télécharger des modèles (initialement ou actualisés pour des modifications), préparez-vous à attendre pendant jusqu'à 15 minutes avant que le téléchargement soit terminé et que les modèles nouveaux ou mis à jour soient entièrement opérationnels. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration du modèle et la connectivité réseau. 

## <a name="office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-a-changed-custom-template"></a>Applications Office 365, Office 2019, Office 2016 et Office 2013 : Comment forcer une actualisation pour un modèle personnalisé modifié
En modifiant le Registre sur les ordinateurs exécutant les applications Office 365, Office 2019, Office 2016 ou Office 2013, vous pouvez changer la planification automatique afin que les modèles modifiés soient actualisés sur les ordinateurs à une fréquence supérieure à la fréquence par défaut. Vous pouvez également forcer une actualisation immédiate en supprimant les données existantes dans une valeur de Registre.

> [!WARNING]
> Si vous n'utilisez pas l'Éditeur du Registre correctement, vous risquez de provoquer de sérieux problèmes pouvant vous amener à devoir réinstaller le système d'exploitation. Microsoft ne peut pas garantir la résolution des problèmes engendrés par une utilisation incorrecte de l'Éditeur du Registre. Utilisez l’Éditeur du Registre à vos propres risques.

### <a name="to-change-the-automatic-schedule"></a>Pour modifier la planification automatique

1.  Dans l’un Éditeur du Registre, créez et définissez l’une des valeurs de Registre suivantes :
    
    - Pour définir une fréquence de mise à jour en jours (au moins 1 jour) :  Créez une valeur de Registre nommée **TemplateUpdateFrequency** et définissez une valeur entière pour les données, spécifiant la fréquence (en jours) de téléchargement des modifications d’un modèle téléchargé. Utilisez les informations suivantes pour rechercher le chemin du Registre pour créer cette nouvelle valeur de Registre.

        **Chemin du Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type :** REG_DWORD

        **Valeur :** TemplateUpdateFrequency

    - Pour définir une fréquence de mise à jour en secondes (au moins 1 seconde) :  Créez une valeur de Registre nommée **TemplateUpdateFrequencyInSeconds** et définissez une valeur entière pour les données, spécifiant la fréquence (en secondes) de téléchargement des modifications d’un modèle téléchargé. Utilisez les informations suivantes pour rechercher le chemin du Registre pour créer cette nouvelle valeur de Registre.

        **Chemin du Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type :** REG_DWORD

        **Valeur :** TemplateUpdateFrequencyInSeconds

    Assurez-vous que vous créez et définissez l’une de ces valeurs de Registre, pas les deux. Si les deux sont présentes, **TemplateUpdateFrequency** est ignoré.

2.  Si vous souhaitez forcer une actualisation immédiate des modèles, passez à la procédure suivante. Dans le cas contraire, redémarrez maintenant vos applications et instances Office de l'Explorateur de fichiers.

### <a name="to-force-an-immediate-refresh"></a>Pour forcer une actualisation immédiate

1. À l’aide d’un éditeur du Registre, supprimez les données de la valeur **LastUpdatedTime**. Par exemple, les données peuvent afficher **2015-04-20T15:52**. Supprimez 2015-04-20T15:52 pour qu’aucune donnée ne s’affiche. Utilisez les informations suivantes pour rechercher le chemin de Registre et supprimer ces données de valeur de Registre.

   **Chemin du Registre :** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*alias_utilisateur*>

   **Type :** REG_SZ

   **Valeur :** LastUpdatedTime

   > [!TIP]
   > Dans le chemin de Registre, *<MicrosoftRMS_FQDN>* fait référence au nom de domaine complet de votre service Microsoft RMS. Si vous souhaitez vérifier cette valeur :
   > 
   > Exécutez le [Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) applet de commande pour Azure Information Protection. Si vous n’avez pas déjà installé le module PowerShell de AIPService, consultez [installation du module PowerShell de AIPService](install-powershell.md).
   > 
   > Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.
   > 
   > Exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > Dans la valeur, supprimez **https://** et **/_wmcs/licensing** de cette chaîne. La valeur restante est votre nom de domaine complet (FQDN) du service Microsoft RMS. Dans notre exemple, le nom de domaine complet (FQDN) du service Microsoft RMS a la valeur suivante :
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. Supprimez le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3. Redémarrez vos applications Office et les instances de l’Explorateur de fichiers.

## <a name="see-also"></a>Voir aussi
[Configuration et gestion des modèles dans la stratégie Azure Information Protection](configure-policy-templates.md)

