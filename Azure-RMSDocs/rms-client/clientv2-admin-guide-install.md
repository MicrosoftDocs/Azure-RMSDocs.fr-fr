---
title: Installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs
description: Instructions et informations permettant aux administrateurs de déployer le Azure Information Protection client d’étiquetage unifié pour Windows sur les réseaux d’entreprise.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 29d08fc8b4b2c2eb73840d8d6dc1f443cd904fcf
ms.sourcegitcommit: d3ac12c51b41bd1ec4ce4009303d124efc95353b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180645"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guide de l’administrateur : Installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Avant d’installer le client d’étiquetage unifié Azure Information Protection sur votre réseau d’entreprise, vérifiez que les ordinateurs disposent des versions et des applications de système d’exploitation requises pour Azure Information Protection: [Configuration requise pour Azure Information Protection](../requirements.md). 

Vérifiez ensuite les prérequis supplémentaires qui peuvent être nécessaires pour le client d’étiquetage unifié Azure Information Protection, comme indiqué dans la section suivante. Tous les prérequis ne sont pas vérifiés par le programme d’installation.

## <a name="additional-prerequisites-for-the-azure-information-protection-unified-labeling-client"></a>Conditions préalables supplémentaires pour le client d’étiquetage unifié Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    L’installation complète du client d’étiquetage unifié Azure Information Protection par défaut, requiert une version minimale de Microsoft .NET Framework 4.6.2 et, si ce n’est pas le cas, l’Assistant Installation du programme d’installation exécutable tente de télécharger et d’installer ce requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré. Bien que déconseillé, vous pouvez ignorer ce prérequis lorsque vous utilisez l’Assistant Installation en utilisant un [paramètre d’installation personnalisé](#more-information-about-the-downgradedotnetrequirement-installation-parameter).
    
    Ce prérequis n’est pas installé automatiquement lorsque vous installez le client en mode silencieux à l’aide du programme d’installation exécutable, de Windows Update ou de Windows Installer. Dans ces cas de figure, vous devez installer ce prérequis séparément s’il est nécessaire, faute de quoi l’installation échoue. Vous pouvez télécharger Microsoft .NET Framework 4.6.2 (programme d’installation en mode hors connexion) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53344).

- Microsoft .NET Framework 4.5.2
    
    Si la visionneuse Azure Information Protection est installée séparément, Microsoft .NET Framework version 4.5.2 minimum est requis. Si cette version est manquante, le programme d’installation exécutable ne procède pas au téléchargement ni à l’installation.

- Windows PowerShell version 4.0
    
    Le module PowerShell pour le client nécessite Windows PowerShell version 4.0, que vous devrez peut-être installer sur les systèmes d’exploitation plus anciens. Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). Ce programme d’installation ne vérifie pas ou n’installe pas cette condition préalable pour vous. Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne `$PSVersionTable` lors d’une session PowerShell.

- Résolution d’écran supérieure à 800 x 600
    
    Les résolutions de 800 x 600 et les résolutions inférieures ne peuvent pas afficher entièrement la boîte de dialogue **Classifier et protéger - Azure Information Protection** lorsque vous cliquez avec le bouton droit sur un fichier ou dossier dans l’Explorateur de fichiers.


- Assistant de connexion Microsoft Online Services 7.250.4303.0
    
    Les ordinateurs qui exécutent Office 2010 nécessitent l’assistant de connexion Microsoft Online Services version 7.250.4303.0. Cette version est incluse dans l’installation du client. Si vous disposez d’une version ultérieure de l’Assistant de connexion, désinstallez-la avant d’installer le client d’étiquetage unifié Azure Information Protection. Par exemple, vérifiez la version et désinstallez de l’assistant de connexion à l’aide du **Panneau de configuration** > **Programmes et fonctionnalités** > **Désinstaller ou modifier un programme**.

- KB 4482887
    
    Pour Windows 10 version 1809 uniquement, pour les builds du système d’exploitation postérieures à 17763.348, installez [1er mars 2019—KB4482887 (Build du système d’exploitation 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) pour que la barre Information Protection s’affiche correctement dans les applications Office. Cette mise à jour n’est pas nécessaire si vous avez Office 365 1902 ou ultérieur.

- KB 2533623
    
    Les ordinateurs exécutant Windows 7 SP1 requièrent KB 2533623. Pour plus d’informations sur cette mise à jour, consultez [Avis de sécurité Microsoft : Le chargement non sécurisé de bibliothèque peut permettre l’exécution de code à distance](https://support.microsoft.com/en-us/kb/2533623). Vous pouvez peut-être installer cette mise à jour directement, ou elle peut être remplacée par une autre qui l’installe pour vous.
    
    Si cette mise à jour est requise, mais qu’elle n’est pas installée, l’installation du client vous avertit qu’elle doit l’être. Cette mise à jour peut être installée après l’installation du client, mais certaines actions seront bloquées et le message s’affichera à nouveau.  

- Visual C++ Redistributable pour Visual Studio 2015 (version 32 bits)
    
    Pour les ordinateurs qui exécutent Windows 7 Service Pack 1, installez **vc_redist.x86.exe** depuis la page de téléchargement : [Visual C++ Redistributable pour Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    L’installation du client ne vérifie pas la configuration requise, mais elle est nécessaire pour que le client d’étiquetage unifié Azure Information Protection pour classifier et protéger les fichiers PDF.

- Configurer la stratégie de groupe pour empêcher la désactivation du complément Azure Information Protection
    
    Pour Office 2013 et versions ultérieures, configurez la stratégie de groupe pour vous assurer que le complément **Microsoft Azure Information Protection** pour les applications Office est toujours activé. Sans cette configuration, le complément Microsoft Azure Information Protection peut être désactivé et les utilisateurs ne seront pas en mesure d’étiqueter leurs documents et e-mails dans leur application Office.
    
    - Pour Outlook: Utilisez le paramètre de stratégie de groupe documenté dans [Contrôle de l’administrateur système sur les compléments](https://docs.microsoft.com/office/vba/outlook/concepts/getting-started/support-for-keeping-add-ins-enabled#system-administrator-control-over-add-ins) de la documentation Office.
    
    - Pour Word, Excel et PowerPoint : Utilisez le paramètre de stratégie de groupe **Liste des compléments gérés** documenté dans l’article du support [Aucun complément chargé en raison des paramètres de stratégie de groupe pour les programmes Office 2013 et Office 2016](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off). 
        
        Spécifiez les identificateurs programmatiques (ProgID) suivants pour Azure Information Protection et définissez l’option sur **1 : Le complément est toujours activé**.
        
        Pour Word : `MSIP.WordAddin`
        
        Pour Excel : `MSIP.ExcelAddin`
        
        Pour PowerPoint : `MSIP.PowerPointAddin`

> [!IMPORTANT]
> L’installation du client d’étiquetage unifié Azure Information Protection requiert des autorisations d’administrateur local.


## <a name="options-to-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Options d’installation du client d’étiquetage unifié Azure Information Protection pour les utilisateurs

Il existe deux options d’installation du client pour les utilisateurs :

**Exécuter la version exécutable (.exe) du client** : La méthode d’installation recommandée que vous pouvez exécuter en mode interactif ou silencieux. Cette méthode offre la plus grande souplesse et est recommandée, car le programme d’installation vérifie la plupart des composants requis et peut automatiquement installer les composants requis manquants. [Instructions](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer)

**Déployer la version du programme d’installation (.msi) Windows du client** : Pris en charge pour les installations en mode silencieux uniquement avec l’utilisation d’un mécanisme de déploiement central, comme une stratégie de groupe, Configuration Manager ou Microsoft Intune. Cette méthode est nécessaire pour les PC Windows 10 qui sont gérés par Intune et la gestion des appareils mobiles (MDM), car pour ces ordinateurs, les fichiers exécutables ne sont pas pris en charge pour l’installation. Toutefois, lorsque vous utilisez cette méthode d’installation, vous devez manuellement vérifier et installer ou désinstaller le logiciel dépendant que le programme d’installation pour le fichier exécutable exécuterait pour chaque ordinateur. [Instructions](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer)

Une fois le client d’étiquetage unifié Azure Information Protection installé, vous pouvez mettre à jour ce client en répétant la méthode d’installation choisie ou en utilisant Windows Update pour que le client soit mis à niveau automatiquement. Pour plus d’informations sur la mise à niveau, consultez la section [Mise à niveau et maintenance du client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer"></a>Pour installer le client d’étiquetage unifié Azure Information Protection à l’aide du programme d’installation exécutable

Utilisez les instructions suivantes pour installer le client lorsque vous n’utilisez pas le catalogue Microsoft Update, ou que vous déployez le fichier .msi à l’aide d’une méthode de déploiement central comme Intune.

1. Téléchargez la version exécutable du client d’étiquetage unifié Azure Information Protection (nom de fichier AzInfoProtection_UL) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 

2. Pour une installation par défaut, exécutez simplement le fichier exécutable, par exemple, **AzInfoProtection_UL. exe**. Toutefois, pour afficher les options d’installation, commencez par exécuter le fichier exécutable avec **/Help** : `AzInfoProtection_UL.exe /help`

    Exemple pour installer le client en mode silencieux : `AzInfoProtection_UL.exe /quiet`
    
    Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :
    
    - **ServiceLocation** : Utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010, et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent d’invites. [Plus d’informations](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement** : Utilisez ce paramètre pour éviter d’exiger Microsoft Framework .NET version 4.6.2. [Plus d’informations](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry=0** : Utilisez ce paramètre pour désactiver l’option d’installation **Participer à l’amélioration d’Azure Information Protection en envoyant des statistiques d’utilisation à Microsoft**. 

3. Pour achever l'installation : 

    - Si votre ordinateur exécute Office 2010, redémarrez-le. 
        
        Si le client n’a pas été installé avec le paramètre ServiceLocation, lorsque vous ouvrez pour la première fois l’une des applications Office qui utilisent le client unifié Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le registre pour cette première utilisation. La fonction [Détection du service](client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers. 
        
5. Vous pouvez vérifier que l’installation a réussi en consultant le fichier journal de l’installation, qui est créé par défaut dans le dossier %temp%. Vous pouvez modifier cet emplacement à l’aide du paramètre d’installation **/log**. 
 
    Le nom du fichier a pour format : `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.
    
    Par exemple :  **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    Dans ce fichier journal, recherchez la chaîne suivante : **Produit : Microsoft Azure Information Protection--Installation effectuée.** En cas d’échec de l’installation, ce fichier journal contient des informations pour vous aider à identifier et résoudre les problèmes.

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

    Par exemple :  **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. À partir de la valeur, supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne restante correspond à la valeur à spécifier pour le paramètre ServiceLocation.

Exemple d’installation du client en mode silencieux pour Office 2010 et Azure RMS : `AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Plus d’informations sur le paramètre d’installation DowngradeDotNetRequirement

Pour prendre en charge les mises à niveau automatiques à l’aide d’Windows Update et pour une intégration fiable avec les applications Office, le client d’étiquetage Azure Information Protection unifié utilise Microsoft .NET Framework version 4.6.2. Par défaut, l’installation interactive à partir de l’exécutable vérifie que cette version est installée et essaie de l’installer si elle est manquante. L’installation nécessite le redémarrage de l’ordinateur.

Si l’installation de cette version de Microsoft .NET Framework ne vous arrange pas, vous pouvez installer le client en indiquant le paramètre et la valeur suivants **DowngradeDotNetRequirement=True**, ce qui permet de contourner cette exigence si la version 4.5.1 de Microsoft .NET Framework est installée.

Par exemple : `AzInfoProtection_UL.exe DowngradeDotNetRequirement=True`

Nous vous recommandons d’utiliser ce paramètre avec précaution et de savoir qu’il existe des problèmes avec les applications Office qui se sont débloquées lorsque le client d’étiquetage unifié Azure Information Protection est utilisé avec cette version antérieure du Microsoft .NET Framework. Si vous rencontrez des problèmes de blocage, installez la version recommandée avant d’essayer d’autres solutions de dépannage. 

Rappelez-vous également que si vous utilisez Windows Update pour que le Azure Information Protection client d’étiquetage unifié soit mis à jour, vous devez disposer d’un autre mécanisme de déploiement de logiciels pour mettre à niveau le client vers des versions ultérieures.

### <a name="to-install-the-azure-information-protection-unified-labeling-client-by-using-the-msi-installer"></a>Pour installer le client d’étiquetage unifié Azure Information Protection à l’aide du programme d’installation. msi

Pour le déploiement central, utilisez les informations suivantes, spécifiques à la version d’installation. msi du client d’étiquetage unifié Azure Information Protection. 

Si vous utilisez Intune pour votre méthode de déploiement de logiciels, utilisez ces instructions avec [Ajouter des applications avec Microsoft Intune](/intune/deploy-use/add-apps).

1. Téléchargez la version. msi du Azure Information Protection AzInfoProtection_UL (Unified étiquetage client) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production.

2. Pour chaque ordinateur qui exécute le fichier .msi, vous devez vérifier que les dépendances logicielles suivantes sont établies. Par exemple, empaquetez-les avec la version .msi du client ou déployez-les uniquement sur les ordinateurs qui répondent à ces dépendances :
    
    |Version d’Office|Système d’exploitation|Logiciels|Action|
    |--------------------|--------------|----------------|---------------------|
    |Toutes les versions, à l’exception d’Office 365 1902 ou ultérieur|Windows 10 version 1809 uniquement, builds du système d’exploitation postérieures à 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installation|
    |Office 2016|Toutes les versions prises en charge|64 bits: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 bits: [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> Version : 1.0|Installation|
    |Office 2013|Toutes les versions prises en charge|64 bits: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 bits: [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />Version : 1.0|Installation|
    |Office 2010|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installation|
    |Office 2010|Windows 8.1 et Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB2843630 ou KB2919355 n’est pas installé|
    |Office 2010|Windows 8 et Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installation|
    |Office 2010|Windows 7 et Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB3125574 n’est pas installé|
    |Non applicable|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|Installation|
    |Non applicable|Windows 7|KB2627273 <br /><br /> Numéro de version inclus dans le nom de fichier : v4|Désinstaller l’interface|

3. Pour une installation par défaut, exécutez le fichier .msi avec **/quiet/** , par exemple, `AzInfoProtection_UL.msi /quiet`. Toutefois, vous devrez peut-être spécifier des paramètres d’installation supplémentaires qui sont documentés dans les [instructions du programme d’installation exécutable](#to-install-the-azure-information-protection-unified-labeling-client-by-using-the-executable-installer).  


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez installé le client d’étiquetage unifié Azure Information Protection, consultez les rubriques suivantes pour plus d’informations sur la prise en charge de ce client:

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

