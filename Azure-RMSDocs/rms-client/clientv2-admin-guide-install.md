---
title: Installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs
description: Instructions et informations permettant aux administrateurs de déployer le Azure Information Protection client d’étiquetage unifié pour Windows sur les réseaux d’entreprise.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/07/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 427143c8ee2a93e60be683b3e80b5493c0bab441
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385469"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guide de l’administrateur : installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP pour Windows et les versions d’Office dans support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Instructions pour**: [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-install.md). *

Avant d’installer le client d’étiquetage unifié Azure Information Protection sur votre réseau d’entreprise, vérifiez que les ordinateurs disposent des versions et des applications de système d’exploitation requises pour Azure Information Protection : [Configuration requise pour la Azure information protection](../requirements.md). 

Vérifiez ensuite les prérequis supplémentaires qui peuvent être nécessaires pour le client d’étiquetage unifié Azure Information Protection, comme indiqué dans la section suivante. Tous les prérequis ne sont pas vérifiés par le programme d’installation.

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Conditions préalables supplémentaires pour le client d’étiquetage unifié Azure Information Protection

Les prérequis suivants pour le client d’étiquetage unifié AIP s’ajoutent aux éléments répertoriés dans [Azure information protection exigences](../requirements.md).

|Condition requise  |Description  |
|---------|---------|
|**Microsoft .NET Framework 4.6.2**     | L’installation complète du client d’étiquetage unifié Azure Information Protection par défaut nécessite une version minimale de Microsoft .NET Framework 4.6.2. <br><br>Si ce Framework est absent, l’Assistant Installation du programme d’installation exécutable tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré.       |
|**Microsoft .NET Framework 4.5.2**     | Si la visionneuse de Azure Information Protection est installée séparément, l’application de la visionneuse requiert une version minimale de Microsoft .NET Framework 4.5.2. <br><br>**Important**: si cette infrastructure est manquante pour la visionneuse, le programme d’installation exécutable ne le télécharge *pas* ou l’installe.        |
|**Version minimale de Windows PowerShell 4,0**     |   Le module PowerShell pour le client nécessite une version minimale de Windows PowerShell 4,0, qui peut être nécessaire pour être installé sur des systèmes d’exploitation plus anciens. <br><br>Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). <br><br>**Important**: le programme d’installation ne vérifie pas ou n’installe *pas* ce composant requis pour vous. Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne `$PSVersionTable` lors d’une session PowerShell.      |
|**Résolution d’écran supérieure à 800 x 600**    |     Les résolutions de 800 x 600 et les résolutions inférieures ne peuvent pas afficher entièrement la boîte de dialogue **Classifier et protéger - Azure Information Protection** lorsque vous cliquez avec le bouton droit sur un fichier ou dossier dans l’Explorateur de fichiers.    |
|**Assistant de connexion Microsoft Online Services 7.250.4303.0**     |   Les ordinateurs qui exécutent Office 2010 requièrent l’Assistant de connexion Microsoft Online Services version 7.250.4303.0, qui est inclus dans l’installation du client. <br><br>Si vous disposez d’une version ultérieure de l’Assistant de connexion, désinstallez-la avant d’installer le client d’étiquetage unifié Azure Information Protection. <br><br>Par exemple, vérifiez la version et désinstallez l’Assistant de connexion à l’aide du **panneau de configuration**  >  **programme et fonctionnalités**  >  **désinstaller ou modifier un programme**.      |
|**KB 4482887**     | Pour Windows 10 version 1809 uniquement, pour les builds du système d’exploitation postérieures à 17763.348, installez [1er mars 2019—KB4482887 (Build du système d’exploitation 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) pour que la barre Information Protection s’affiche correctement dans les applications Office. <br><br>Cette mise à jour n’est pas nécessaire si vous avez Office 365 1902 ou ultérieur.        |
|**Autorisations d’administrateur**| L’installation du client d’étiquetage unifié Azure Information Protection requiert des autorisations d’administrateur local.| 
|**Désactiver la protection contre l’exploitation (.NET 2 ou 3 uniquement)**   |Le client AIP n’est pas pris en charge sur les ordinateurs disposant de .NET 2 ou 3 dont la [protection contre l’exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée. Si votre ordinateur dispose de .NET 2 ou 3 en plus d’une version de .NET 4. x indiquée ci-dessus, veillez à [désactiver la protection contre l’exploitation](../known-issues.md#known-issues-for-aip-and-exploit-protection) avant d’installer le client AIP.  |
|||
        
### <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>Configurer votre stratégie de groupe pour empêcher la désactivation d’AIP

Pour les versions d’Office 2013 et ultérieures, nous vous recommandons de configurer votre stratégie de groupe pour vous assurer que le complément **Microsoft Azure information protection** pour les applications Office est toujours activé.  Sans ce complément, les utilisateurs ne peuvent pas étiqueter leurs documents ou messages électroniques dans les applications Office.   

Pour Word, Excel, PowerPoint et Outlook, utilisez la **liste des paramètres de stratégie de groupe des compléments gérés** documentés dans [aucun complément n’est chargé en raison des paramètres de stratégie de groupe pour les programmes Office 2013 et Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off). 

Spécifiez les identificateurs programmatiques (ProgID) suivants pour AIP, puis affectez la valeur 1 à l’option **: le complément est toujours activé**.

|Application  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 

## <a name="applications"></a>Applications

Le client d’étiquetage unifié Azure Information Protection peut étiqueter et protéger des documents et des e-mails à l’aide des applications Office Word, Excel, PowerPoint et Outlook de l’une des éditions Office suivantes :

- Applications Office, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur
- Microsoft 365 Apps for enterprise
- Office Professionnel Plus 2019
- Office Professionnel Plus 2016
- Office Professionnel Plus 2013 avec Service Pack 1
- Office Professionnel Plus 2010 avec Service Pack 2

D’autres éditions (telles que **standard**) d’Office ne peuvent pas protéger des documents et des e-mails à l’aide d’un service Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour l' **étiquetage** uniquement. Par conséquent, les étiquettes qui appliquent la protection ne s’affichent pas pour les utilisateurs sur le bouton ou la barre de sensibilité de Azure Information Protection.

Pour plus d’informations sur les éditions d’Office qui prennent en charge le service de protection, consultez [Applications prenant en charge la protection des données Azure Rights Management](../requirements-applications.md).

### <a name="office-features-and-capabilities-not-supported"></a>Fonctionnalités et caractéristiques Office non prises en charge

Le client d’étiquetage unifié Azure Information Protection ne prend pas en charge plusieurs versions d’Office sur le même ordinateur ou ne bascule pas les comptes d’utilisateur dans Office.

La fonctionnalité Publipostage n’est pas prise en charge avec les fonctionnalités Azure Information Protection.

## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Options d’installation du client d’étiquetage unifié Azure Information Protection pour les utilisateurs

Il existe deux options d’installation du client pour les utilisateurs :

**Exécuter la version exécutable (.exe) du client** : la méthode d’installation recommandée que vous pouvez exécuter en mode interactif ou silencieux. Cette méthode offre la plus grande souplesse et est recommandée, car le programme d’installation vérifie la plupart des composants requis et peut automatiquement installer les composants requis manquants. [Instructions](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Déployer le programme d’installation (.msi) Windows du client** : pris en charge pour les installations en mode silencieux uniquement avec l’utilisation d’un mécanisme de déploiement central, comme une stratégie de groupe, Configuration Manager ou Microsoft Intune. Cette méthode est nécessaire pour les PC Windows 10 qui sont gérés par Intune et la gestion des appareils mobiles (MDM), car pour ces ordinateurs, les fichiers exécutables ne sont pas pris en charge pour l’installation. Toutefois, lorsque vous utilisez cette méthode d’installation, vous devez manuellement vérifier et installer ou désinstaller le logiciel dépendant que le programme d’installation pour le fichier exécutable exécuterait pour chaque ordinateur. [Instructions](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Une fois le client d’étiquetage unifié Azure Information Protection installé, vous pouvez mettre à jour ce client en répétant la méthode d’installation choisie ou en utilisant Windows Update pour que le client soit mis à niveau automatiquement. Pour plus d’informations sur la mise à niveau, consultez la section [Mise à niveau et maintenance du client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>Pour installer le client d’étiquetage unifié Azure Information Protection à l’aide du programme d’installation exécutable

Utilisez les instructions suivantes pour installer le client lorsque vous n’utilisez pas le catalogue Microsoft Update, ou que vous déployez le fichier .msi à l’aide d’une méthode de déploiement central comme Intune.

1. Téléchargez la version exécutable de l’Azure Information Protection client d’étiquetage unifié (nom de fichier de AzInfoProtection_UL) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 

2. Pour une installation par défaut, il vous suffit d’exécuter le fichier exécutable, par exemple, **AzInfoProtection_UL.exe**. Toutefois, pour afficher les options d’installation, commencez par exécuter le fichier exécutable avec **/Help**: `AzInfoProtection_UL.exe /help`

    Exemple pour installer le client en mode silencieux : `AzInfoProtection_UL.exe /quiet`
    
    Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :
    
    - **ServiceLocation** : utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010 et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent un message. [Plus d’informations](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **AllowTelemetry = 0** : Utilisez ce paramètre pour désactiver l’option d’installation **Participer à l’amélioration d’Azure Information Protection en envoyant des statistiques d’utilisation à Microsoft**. 

3. Pour achever l'installation : 

    - Si votre ordinateur exécute Office 2010, redémarrez-le. 
        
        Si le client n’a pas été installé avec le paramètre ServiceLocation, lorsque vous ouvrez pour la première fois l’une des applications Office qui utilisent le client unifié Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le registre pour cette première utilisation. La fonction [Détection du service](client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers. 
        
5. Vous pouvez vérifier que l’installation a réussi en consultant le fichier journal de l’installation, qui est créé par défaut dans le dossier %temp%. Vous pouvez modifier cet emplacement à l’aide du paramètre d’installation **/log**. 
 
    Le nom du fichier a pour format : `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.
    
    Par exemple : **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    Dans ce fichier journal, recherchez la chaîne suivante : **Product : Microsoft Azure information protection--installation terminée**. En cas d’échec de l’installation, ce fichier journal contient des informations pour vous aider à identifier et résoudre les problèmes.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Plus d’informations sur le paramètre d’installation ServiceLocation

Lorsque vous installez le client pour des utilisateurs disposant d’Office 2010 et qu’ils n’ont pas d’autorisations d’administrateur local, spécifiez le paramètre ServiceLocation et l’URL de votre service Azure Rights Management. Ce paramètre et la valeur créent et définissent les clés de registre suivantes :

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Utilisez la procédure suivante pour identifier la valeur à spécifier pour le paramètre ServiceLocation. 

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Pour identifier la valeur à spécifier pour le paramètre ServiceLocation

1. À partir d’une session PowerShell, exécutez d’abord [Connect-AipService](/powershell/module/aipservice/connect-aipservice) et spécifiez vos informations d’identification d’administrateur pour vous connecter au service Azure Rights Management. Exécutez ensuite la [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration). 
 
    Si vous n’avez pas encore installé le module PowerShell pour le service Azure Rights Management, consultez [installation du module PowerShell AIPService](../install-powershell.md).

2. Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

    Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. Supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne restante correspond à la valeur à spécifier pour le paramètre ServiceLocation.

Exemple d’installation du client en mode silencieux pour Office 2010 et Azure RMS : `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>Pour installer le client d’étiquetage unifié Azure Information Protection à l’aide du programme d’installation. msi

Pour le déploiement central, utilisez les informations suivantes, spécifiques à la version d’installation. msi du client d’étiquetage unifié Azure Information Protection. 

Si vous utilisez Intune pour votre méthode de déploiement de logiciels, utilisez ces instructions avec [Ajouter des applications avec Microsoft Intune](/mem/intune/apps/apps-add).

1. Téléchargez la version. msi du Azure Information Protection AzInfoProtection_UL (Unified étiquetage client) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production.

1. Pour chaque ordinateur qui exécute le fichier .msi, vous devez vérifier que les dépendances logicielles suivantes sont établies. Par exemple, empaquetez-les avec la version .msi du client ou déployez-les uniquement sur les ordinateurs qui répondent à ces dépendances :
    
    |Version d’Office|Système d’exploitation|Logiciel|Action|
    |--------------------|--------------|----------------|---------------------|
    |Toutes les versions, à l’exception d’Office 365 1902 ou ultérieur|Windows 10 version 1809 uniquement, builds du système d’exploitation postérieures à 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installer|
    |Office 2016|Toutes les versions prises en charge|64 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Version : 1.0|Installer|
    |Office 2013|Toutes les versions prises en charge|64 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Version : 1.0|Installer|
    |Office 2010|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installer|
    |Office 2010|Windows 8.1 et Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB2843630 ou KB2919355 n’est pas installé|
    |Office 2010|Windows 8 et Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer|
    
   

1. Pour une installation par défaut, exécutez le fichier .msi avec **/quiet/**, par exemple, `AzInfoProtection_UL.msi /quiet`.

    Vous devrez peut-être spécifier des paramètres d’installation supplémentaires. Pour plus d’informations, consultez les [instructions du programme d’installation exécutable](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer).

    > [!NOTE]
    > Par défaut, l’option **aider à améliorer Azure information protection en envoyant des statistiques d’utilisation à** l’installation Microsoft est activée. Pour désactiver cette option, veillez à effectuer l’une des opérations suivantes :
    >
    >- Pendant l’installation, spécifiez **AllowTelemetry = 0**
    >- Après l’installation, mettez à jour la clé de Registre comme suit : **EnableTelemetry = 0**.
    >

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez installé le client d’étiquetage unifié Azure Information Protection, consultez les rubriques suivantes pour plus d’informations sur la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichiers pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)