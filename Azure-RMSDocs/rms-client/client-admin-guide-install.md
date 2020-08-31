---
title: Installer le client Azure Information Protection pour les utilisateurs
description: Instructions et informations destinées aux administrateurs pour le déploiement du client Azure Information Protection pour Windows sur les réseaux d’entreprise.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/30/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bb2f7d2cacad3623eb590c338a7f19585e9c80d1
ms.sourcegitcommit: dd21de9f06ef019634dc2b5d8baf2670bb8171a2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89176648"
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>Guide de l’administrateur : Installer le client Azure Information Protection pour les utilisateurs

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>
> **Pour déployer le client classique AIP,** ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.

Avant d’installer le client Azure Information Protection sur votre réseau d’entreprise, vérifiez que vos ordinateurs disposent des versions et des applications nécessaires du système d’exploitation pour Azure Information Protection : [Configuration requise pour Azure Information Protection](../requirements.md).

Ensuite, vérifiez les prérequis supplémentaires qui peuvent être nécessaires pour le client Azure Information Protection, comme indiqué dans la section suivante. Tous les prérequis ne sont pas vérifiés par le programme d’installation.

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Prérequis supplémentaires pour le client Azure Information Protection

- Microsoft .NET Framework 4.6.2

    L’installation complète du client Azure Information Protection par défaut nécessite au minimum Microsoft .NET Framework version 4.6.2. Si cette version est manquante, l’Assistant Installation du programme d’installation exécutable tente de télécharger et d’installer ce prérequis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré. Bien que déconseillé, vous pouvez ignorer ce prérequis lorsque vous utilisez l’Assistant Installation en utilisant un [paramètre d’installation personnalisé](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

    Ce prérequis n’est pas installé automatiquement lorsque vous installez le client en mode silencieux à l’aide du programme d’installation exécutable, de Windows Update ou de Windows Installer. Dans ces cas de figure, vous devez installer ce prérequis séparément s’il est nécessaire, faute de quoi l’installation échoue. Vous pouvez télécharger Microsoft .NET Framework 4.6.2 (programme d’installation en mode hors connexion) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53344).

- Microsoft .NET Framework 4.5.2

    Si la visionneuse Azure Information Protection est installée séparément, Microsoft .NET Framework version 4.5.2 minimum est requis. Si cette version est manquante, le programme d’installation exécutable ne procède pas au téléchargement ni à l’installation.

- Version minimale de Windows PowerShell 4,0

    Le module PowerShell pour le client nécessite une version minimale de 4,0 pour Windows PowerShell, qui devra peut-être être installé sur des systèmes d’exploitation plus anciens. Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). Ce programme d’installation ne vérifie pas ou n’installe pas cette condition préalable pour vous. Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne `$PSVersionTable` lors d’une session PowerShell.

- Résolution d’écran supérieure à 800 x 600

    Les résolutions de 800 x 600 et les résolutions inférieures ne peuvent pas afficher entièrement la boîte de dialogue **Classifier et protéger - Azure Information Protection** lorsque vous cliquez avec le bouton droit sur un fichier ou dossier dans l’Explorateur de fichiers.

- Assistant de connexion Microsoft Online Services 7.250.4303.0

    Les ordinateurs qui exécutent Office 2010 nécessitent l’assistant de connexion Microsoft Online Services version 7.250.4303.0. Cette version est incluse dans l’installation du client. Si vous disposez d’une version ultérieure de l’assistant de connexion, désinstallez-la avant d’installer le client Azure Information Protection. Par exemple, vérifiez la version et désinstallez l’Assistant de connexion à l’aide du **panneau de configuration**  >  **programme et fonctionnalités**  >  **désinstaller ou modifier un programme**.

- KB 4482887

    Pour Windows 10 version 1809 uniquement, pour les builds du système d’exploitation postérieures à 17763.348, installez [1er mars 2019—KB4482887 (Build du système d’exploitation 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) pour que la barre Information Protection s’affiche correctement dans les applications Office. Cette mise à jour n’est pas nécessaire si vous avez Office 365 1902 ou ultérieur.

- Configurer la stratégie de groupe pour empêcher la désactivation du complément Azure Information Protection

    Pour Office 2013 et versions ultérieures, configurez la stratégie de groupe pour vous assurer que le complément **Microsoft Azure Information Protection** pour les applications Office est toujours activé. Sans cette configuration, le complément Microsoft Azure Information Protection peut être désactivé et les utilisateurs ne seront pas en mesure d’étiqueter leurs documents et e-mails dans leur application Office.

    - Pour Outlook : utilisez le paramètre de stratégie de groupe documenté dans [Contrôle de l’administrateur système sur les compléments](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins) dans la documentation Office.

    - Pour Word, Excel et PowerPoint : utilisez le paramètre de stratégie de groupe **liste des compléments gérés** documenté dans l’article du support [Aucun complément chargé en raison des paramètres de stratégie de groupe pour les programmes Office 2013 et Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off).

        Indiquez les identificateurs programmatiques (ProgID) suivants pour Azure Information Protection et définissez l’option sur **1 : le complément est toujours activé**.

        Pour Word : `MSIP.WordAddin`

        Pour Excel : `MSIP.ExcelAddin`

        Pour PowerPoint : `MSIP.PowerPointAddin`

- Le client AIP n’est pas pris en charge sur les ordinateurs sur lesquels la [protection contre l’exploitation](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée. Veillez à [désactiver la protection contre l’exploitation](../known-issues.md#known-issues-for-installing-the-aip-client) avant d’installer le client AIP.  

> [!IMPORTANT]
> L’installation du client Azure Information Protection nécessite les autorisations d’administrateur local.

## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Options d’installation du client Azure Information Protection pour les utilisateurs

Utilisez l’une des options suivantes pour installer le client pour les utilisateurs :

|Option d’installation  |Description  |
|---------|---------|
|**Exécuter l’exécutable client (. exe)**  </br></br> [Instructions](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)      | Nous vous recommandons d’exécuter la version. exe du client pour exécuter l’installation de manière interactive ou silencieuse.</br></br> L’exécution du fichier. exe offre la plus grande souplesse et est recommandée car elle vérifie également la plupart des conditions préalables et peut également installer les composants requis manquants. |
|**Déployer le programme d’installation Windows (. msi) du client** </br></br> [Instructions](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)    | Le programme d’installation de Windows Azure Information Protection client est pris en charge uniquement pour les installations sans assistance qui utilisent un mécanisme de déploiement central.</br></br> Par exemple, utilisez le fichier. msi lors du déploiement avec une stratégie de groupe, Configuration Manager et Microsoft Intune.</br></br> Vous devez utiliser la méthode tis pour les PC Windows 10 gérés par Intune et la gestion des appareils mobiles (MDM), car les fichiers. exe ne sont pas pris en charge pour ces ordinateurs.</br></br>**Remarque :** Lorsque vous utilisez l’installation. msi, vous devez vérifier manuellement la configuration requise et installer ou désinstaller tous les logiciels dépendants requis. |

Après avoir installé le client, effectuez les mises à jour en répétant la même procédure d’installation, ou utilisez Windows Update pour que le client reste automatiquement mis à jour. Vous n’êtes pas obligé de désinstaller les versions héritées du client avant d’installer une nouvelle version.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!NOTE]
> Pour désinstaller le client, utilisez l’option Windows **Ajouter ou supprimer des programmes** , par exemple, [dans le panneau de configuration Windows](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs).

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Pour installer le client Azure Information Protection en utilisant le programme d’installation exécutable

Utilisez les instructions suivantes pour installer le client lorsque vous n’utilisez pas le catalogue Microsoft Update, ou que vous déployez le fichier .msi à l’aide d’une méthode de déploiement central comme Intune.

1. Pour une installation par défaut, exécutez simplement le fichier exécutable, par exemple **AzInfoProtection.exe**. 

    Pour afficher d’autres options d’installation, exécutez d’abord le fichier exécutable avec **/Help**: `AzInfoProtection.exe /help`

    Exemple pour installer le client en mode silencieux : `AzInfoProtection.exe /quiet`

    Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection.exe  PowerShellOnly=true /quiet`

    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :

    - **ServiceLocation** : utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010 et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent un message. [Plus d’informations](#more-information-about-the-servicelocation-installation-parameter)

    - **DowngradeDotNetRequirement** : utilisez ce paramètre pour éviter d’avoir à disposer de Microsoft Framework .NET version 4.6.2. [Plus d’informations](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

    - **AllowTelemetry = 0** : Utilisez ce paramètre pour désactiver l’option d’installation **Participer à l’amélioration d’Azure Information Protection en envoyant des statistiques d’utilisation à Microsoft**.

1. En cas d’installation interactive, sélectionnez l’option d’installation d’une **stratégie de démonstration** si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.

1. Pour achever l'installation :

    - Si votre ordinateur exécute Office 2010, redémarrez-le.

        Si le client n’était pas installé avec le paramètre ServiceLocation, lorsque vous commencez par ouvrir l’une des applications Office qui utilise la barre Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le Registre pour cette première utilisation. La fonction [Détection du service](client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre.

    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers.

1. Vous pouvez vérifier que l’installation a réussi en consultant le fichier journal de l’installation, qui est créé par défaut dans le dossier %temp%. Vous pouvez modifier cet emplacement à l’aide du paramètre d’installation **/log**.

    Le nom du fichier a pour format : `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.

    Par exemple : **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**

    Dans ce fichier journal, recherchez la chaîne suivante : **Produit : Microsoft Azure Information Protection -- Installation effectuée.** En cas d’échec de l’installation, ce fichier journal contient des informations pour vous aider à identifier et résoudre les problèmes.

#### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Plus d’informations sur le paramètre d’installation ServiceLocation

Lorsque vous installez le client pour des utilisateurs disposant d’Office 2010 et qu’ils n’ont pas d’autorisations d’administrateur local, spécifiez le paramètre ServiceLocation et l’URL de votre service Azure Rights Management. Ce paramètre et la valeur créent et définissent les clés de registre suivantes :

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Utilisez la procédure suivante pour identifier la valeur à spécifier pour le paramètre ServiceLocation.

##### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Pour identifier la valeur à spécifier pour le paramètre ServiceLocation

1. À partir d’une session PowerShell, exécutez d’abord [Connect-AipService](https://docs.microsoft.com/powershell/module/aipservice/connect-aipservice) et spécifiez vos informations d’identification d’administrateur pour vous connecter au service Azure Rights Management. Exécutez ensuite la [AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration).

    Si vous n’avez pas encore installé le module PowerShell pour le service Azure Rights Management, consultez [installation du module PowerShell AIPService](../install-powershell.md).

2. Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

    Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. Supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne remainin’est la valeur à spécifier pour votre paramètre ServiceLocation.

Exemple d’installation du client en mode silencieux pour Office 2010 et Azure RMS : `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`

#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Plus d’informations sur le paramètre d’installation DowngradeDotNetRequirement

Pour prendre en charge les mises à jour automatiques via Windows Update et pour s’intégrer de façon fiable avec les applications Office, le client Azure Information Protection utilise Microsoft .NET Framework version 4.6.2. Par défaut, l’installation interactive à partir de l’exécutable vérifie que cette version est installée et essaie de l’installer si elle est manquante. L’installation nécessite le redémarrage de l’ordinateur.

Si l’installation de cette version de Microsoft .NET Framework ne vous arrange pas, vous pouvez installer le client en indiquant le paramètre et la valeur suivants **DowngradeDotNetRequirement=True**, ce qui permet de contourner cette exigence si la version 4.5.1 de Microsoft .NET Framework est installée.

Exemple : `AzInfoProtection.exe DowngradeDotNetRequirement=True`.

Nous vous recommandons d’utiliser ce paramètre avec précaution, car des problèmes ont été signalés avec les applications Office. Il arrive que celles-ci se bloquent lorsque le client Azure Information Protection est utilisé avec cette ancienne version de Microsoft .NET Framework. Si vous rencontrez des problèmes de blocage, installez la version recommandée avant d’essayer d’autres solutions de dépannage. 

N’oubliez pas que si vous utilisez Windows Update pour mettre à jour le client Azure Information Protection, vous devez utiliser un autre mécanisme de déploiement de logiciels pour mettre à niveau le client vers des versions ultérieures.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Pour installer le client Azure Information Protection en utilisant le programme d’installation .msi

Pour le déploiement central, utilisez les informations suivantes qui sont spécifiques à la version .msi du client Azure Information Protection. 

Si vous utilisez Intune pour votre méthode de déploiement de logiciels, utilisez ces instructions avec [Ajouter des applications avec Microsoft Intune](/intune/deploy-use/add-apps).

1. Pour chaque ordinateur qui exécute le fichier .msi, vous devez vérifier que les dépendances logicielles suivantes sont établies. Par exemple, empaquetez-les avec la version .msi du client ou déployez-les uniquement sur les ordinateurs qui répondent à ces dépendances :
    
    |Version d’Office|Système d’exploitation|Logiciel|Action|
    |--------------------|--------------|----------------|---------------------|
    |Toutes les versions, à l’exception d’Office 365 1902 ou ultérieur|Windows 10 version 1809 uniquement, builds du système d’exploitation postérieures à 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installer|
    |Office 2013|Toutes les versions prises en charge|64 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Version : 1.0|Installer|
    |Office 2010|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installer|
    |Office 2016|Toutes les versions prises en charge|64 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Version : 1.0|Installer|
    |Office 2010|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installer|
    |Office 2010|Windows 8.1 et Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB2843630 ou KB2919355 n’est pas installé|
    |Office 2010|Windows 8 et Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer|

1. Pour une installation par défaut, exécutez le fichier .msi avec **/quiet/**, par exemple, `AzInfoProtection.msi /quiet`. Toutefois, vous devrez peut-être spécifier des paramètres d’installation supplémentaires qui sont documentés dans les [instructions du programme d’installation exécutable](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).

    > [!NOTE]
    > Par défaut, l’option **aider à améliorer Azure information protection en envoyant des statistiques d’utilisation à** l’installation Microsoft est activée. Pour désactiver cette option, veillez à effectuer l’une des opérations suivantes :
    >
    >- Pendant l’installation, spécifiez **AllowTelemetry = 0**
    >- Après l’installation, mettez à jour la clé de Registre comme suit : **EnableTelemetry = 0**.
    >

## <a name="how-to-install-the-azure-information-protection-scanner"></a>Guide pratique pour installer le scanneur Azure Information Protection

Le module PowerShell inclus avec le client Azure Information Protection fournit des applets de commande permettant d’installer et de configurer le scanneur. Toutefois, pour utiliser le scanneur, vous devez installer la version complète du client et non pas uniquement le module PowerShell.

Pour installer le client pour le scanneur, suivez les mêmes instructions que dans les sections précédentes. Vous êtes alors prêt à configurer et à installer le scanneur. Pour plus d’informations, consultez [qu’est-ce que le Azure information protection scanneur classique ?](../deploy-aip-scanner-classic.md).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez installé le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Personnalisations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichiers pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)
