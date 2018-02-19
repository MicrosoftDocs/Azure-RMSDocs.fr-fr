---
title: Installer le client Azure Information Protection pour les utilisateurs
description: "Instructions et informations destinées aux administrateurs pour le déploiement du client Azure Information Protection pour Windows sur les réseaux d’entreprise."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea3ec965-3720-4614-8564-3ecfe60bc175
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 92e4f6c05378b36165db0628f14941b0ccd26cb7
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="admin-guide-install-the-azure-information-protection-client-for-users"></a>Guide de l’administrateur : Installer le client Azure Information Protection pour les utilisateurs

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Avant d’installer le client Azure Information Protection sur votre réseau d’entreprise, vérifiez que vos ordinateurs disposent des versions et des applications nécessaires du système d’exploitation pour Azure Information Protection : [Configuration requise pour Azure Information Protection](../get-started/requirements-azure-rms.md). 

Ensuite, vérifiez les prérequis supplémentaires qui peuvent être nécessaires pour le client Azure Information Protection, comme indiqué dans la section suivante. Tous les prérequis ne sont pas vérifiés par le programme d’installation.

## <a name="additional-prerequisites-for-the-azure-information-protection-client"></a>Prérequis supplémentaires pour le client Azure Information Protection

- Microsoft .NET Framework 4.6.2
    
    L’installation complète du client Azure Information Protection par défaut requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré. Bien que cela ne soit pas conseillé, vous pouvez ignorer cette condition à l’aide d’un [paramètre d’installation personnalisé](#more-information-about-the-downgradedotnetrequirement-installation-parameter).

- Microsoft .NET Framework 4.5.2
    
    Si la visionneuse Azure Information Protection est installée séparément, une version minimale de Microsoft .NET Framework 4.5.2 est requise. Si cette version est manquante, le programme d’installation ne procède pas au téléchargement ni à l’installation.

- Windows PowerShell version 4.0
    
    Le module PowerShell pour le client nécessite Windows PowerShell version 4.0, que vous devrez peut-être installer sur les systèmes d’exploitation plus anciens. Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). Ce programme d’installation ne vérifie pas ou n’installe pas cette condition préalable pour vous. Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne `$PSVersionTable` lors d’une session PowerShell.

- Assistant de connexion Microsoft Online Services 7.250.4303.0
    
    Les ordinateurs qui exécutent Office 2010 nécessitent l’assistant de connexion Microsoft Online Services version 7.250.4303.0. Cette version est incluse dans l’installation du client. Si vous disposez d’une version ultérieure de l’assistant de connexion, désinstallez-la avant d’installer le client Azure Information Protection. Par exemple, vérifiez la version et désinstallez de l’assistant de connexion à l’aide du **Panneau de configuration** > **Programmes et fonctionnalités** > **Désinstaller ou modifier un programme**.

- KB 2533623
    
    Les ordinateurs exécutant Windows 7 SP1 requièrent KB 2533623. Pour plus d’informations, consultez [Avis de sécurité Microsoft : le chargement non sécurisé de bibliothèque peut permettre l’exécution de code à distance](https://support.microsoft.com/en-us/kb/2533623). Vous pouvez peut-être installer cette mise à jour directement, ou elle peut être remplacée par une autre qui l’installe pour vous.
    
    Si cette mise à jour est requise, mais qu’elle n’est pas installée, l’installation du client vous avertit qu’elle doit l’être. Cette mise à jour peut être installée après l’installation du client, mais certaines actions seront bloquées et le message s’affichera à nouveau.  

- Visual C++ Redistributable pour Visual Studio 2015 (version 32 bits)
    
    Pour les ordinateurs qui exécutent Windows 7 Service Pack 1, installez **vc_redist.x86.exe** depuis la page de téléchargement : [Visual C++ Redistributable pour Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
    
    L’installation du client ne recherche pas ce prérequis, mais il est nécessaire au client Azure Information Protection pour classifier et protéger les fichiers PDF.

- Ne désactivez pas le complément **Microsoft Azure Information Protection** pour les applications Office
    
    Si vous avez configuré le paramètre de stratégie de groupe **Liste des compléments gérés**, ajoutez le complément Microsoft Azure Information Protection pour les applications Office en spécifiant les identificateurs programmatiques (ProgID) suivants pour Azure Information Protection et définissez l’option sur **1 : le complément est toujours activé**.
    
    - Pour Outlook : `MSIP.OutlookAddin`
    
    - Pour Word : `MSIP.WordAddin`
    
    - Pour Excel : `MSIP.ExcelAddin`
    
    - Pour PowerPoint : `MSIP.PowerPointAddin`
    
    Même si vous n’avez pas configuré ce paramètre de stratégie de groupe **Liste des compléments gérés**, vous devrez peut-être le configurer si vous recevez des rapports signalant que le complément Microsoft Azure Information Protection est désactivé. Quand ce complément est désactivé, les utilisateurs ne voient pas la barre Azure Information Protection dans l’application Office.
    
    Pour plus d’informations sur ce paramètre de stratégie de groupe, consultez [No Add-ins loaded due to group policy settings for Office 2013 and Office 2016 programs](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off) (Aucun complément n’est chargé à cause des paramètres de stratégie de groupe pour les programmes Office 2013 et Office 2016).

- Pour les versions d’Office 16.0.8628.2010 et ultérieures (Démarrer en un clic) : activer la prise en charge héritée pour les moniteurs
    
    Remarque : ce prérequis n’est pas nécessaire pour la préversion actuelle du client Azure Information Protection. 
    
    Pour empêcher que la barre Azure Information Protection ne s’affiche en dehors des logiciels Office de ces versions Office, vous devrez peut-être activer la prise en charge héritée pour les écrans. Lorsque la barre ne s’affiche pas correctement dans ce scénario, vous risquez de la voir sous la forme **AdxTaskPane**. 
    
    Pour configurer les applications Office afin de remplir cette condition : **Fichier** > **Options** > **Général** > **Options de l’interface utilisateur** :
    
    - Si vous voyez que l’option **Lors de l’utilisation de plusieurs écrans** est définie avec **Ajuster afin d’obtenir la meilleure apparence**, sélectionnez plutôt **Optimiser pour la compatibilité (redémarrage obligatoire du logiciel)**. 
        
    - Si vous voyez que l’option **Utiliser les meilleurs paramètres pour mon écran** est sélectionnée, supprimez cette sélection.
    
    - Si vous ne voyez aucune de ces options, aucune configuration supplémentaire n’est nécessaire.

> [!IMPORTANT]
> L’installation du client Azure Information Protection nécessite les autorisations d’administrateur local.


## <a name="options-to-install-the-azure-information-protection-client-for-users"></a>Options d’installation du client Azure Information Protection pour les utilisateurs

Il existe trois options d’installation du client pour les utilisateurs :

**Windows Update** : Le client Azure Information Protection est inclus dans le catalogue Microsoft Update, ce qui vous permet d’installer et de mettre à jour le client à l’aide de n’importe quel service de mise à jour de logiciel utilisant le catalogue.

**Exécuter la version exécutable (.exe) du client** : la méthode d’installation recommandée que vous pouvez exécuter en mode interactif ou silencieux. Cette méthode offre la plus grande souplesse et est recommandée, car le programme d’installation vérifie la plupart des composants requis et peut automatiquement installer les composants requis manquants. [Instructions](#to-install-the-azure-information-protection-client-by-using-the-executable-installer)

**Déployer le programme d’installation (.msi) Windows du client** : pris en charge pour les installations en mode silencieux uniquement avec l’utilisation d’un mécanisme de déploiement central, comme une stratégie de groupe, Configuration Manager ou Microsoft Intune. Cette méthode est nécessaire pour les PC Windows 10 qui sont gérés par Intune et la gestion des appareils mobiles (MDM), car pour ces ordinateurs, les fichiers exécutables ne sont pas pris en charge pour l’installation. Toutefois, lorsque vous utilisez cette méthode d’installation, vous devez manuellement vérifier et installer ou désinstaller le logiciel dépendant que le programme d’installation pour le fichier exécutable exécuterait pour chaque ordinateur. [Instructions](#to-install-the-azure-information-protection-client-by-using-the-msi-installer)

### <a name="to-install-the-azure-information-protection-client-by-using-the-executable-installer"></a>Pour installer le client Azure Information Protection en utilisant le programme d’installation exécutable

Utilisez les instructions suivantes pour installer le client lorsque vous n’utilisez pas le catalogue Microsoft Update, ou que vous déployez le fichier .msi à l’aide d’une méthode de déploiement central comme Intune.

1. Téléchargez la version exécutable du client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 

2. Pour une installation par défaut, exécutez simplement le fichier exécutable, par exemple **AzInfoProtection.exe**. Toutefois, pour afficher les options d’installation, commencez par exécuter le fichier exécutable avec **/Help** : `AzInfoProtection.exe /help`

    Exemple pour installer le client en mode silencieux : `AzInfoProtection.exe /quiet`
    
    Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :
    
    - **ServiceLocation** : utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010 et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent un message. [Plus d’informations](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement** : utilisez ce paramètre pour éviter d’avoir à disposer de Microsoft Framework .NET version 4.6.2. [Plus d’informations](#more-information-about-the-downgradedotnetrequirement-installation-parameter)
    
    - **AllowTelemetry = 0** : Utilisez ce paramètre pour désactiver l’option d’installation **Participer à l’amélioration d’Azure Information Protection en envoyant des statistiques d’utilisation à Microsoft**. 
    
3. En cas d’installation interactive, sélectionnez l’option d’installation d’une **stratégie de démonstration** si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.
    
4. Pour achever l'installation : 

    - Si votre ordinateur exécute Office 2010, redémarrez-le. 
        
        Si le client n’était pas installé avec le paramètre ServiceLocation, lorsque vous commencez par ouvrir l’une des applications Office qui utilise la barre Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le Registre pour cette première utilisation. La fonction [Détection du service](../rms-client/client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers. 
        
5. Vous pouvez vérifier que l’installation a réussi en consultant le fichier journal de l’installation, qui est créé par défaut dans le dossier %temp%. Vous pouvez modifier cet emplacement à l’aide du paramètre d’installation **/log**. 
 
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

1. À partir d’une session PowerShell, exécutez d’abord [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) et spécifiez vos informations d’identification d’administrateur pour vous connecter au service Azure Rights Management. Exécutez [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Si vous n’avez pas encore installé le module PowerShell pour le service Azure Rights Management, consultez la section [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

    Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. À partir de la valeur, supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne restante correspond à la valeur à spécifier pour le paramètre ServiceLocation.

Exemple d’installation du client en mode silencieux pour Office 2010 et Azure RMS : `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


#### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Plus d’informations sur le paramètre d’installation DowngradeDotNetRequirement

Pour prendre en charge les mises à jour automatiques via Windows Update et pour s’intégrer de façon fiable avec les applications Office, le client Azure Information Protection utilise Microsoft .NET Framework version 4.6.2. Par défaut, l’installation vérifie que cette version est installée et essaie de l’installer si elle est manquante. L’installation nécessite le redémarrage de l’ordinateur.

Si l’installation de cette version de Microsoft .NET Framework ne vous arrange pas, vous pouvez installer le client en indiquant le paramètre et la valeur suivants **DowngradeDotNetRequirement=True**, ce qui permet de contourner cette exigence si la version 4.5.1 de Microsoft .NET Framework est installée.

Par exemple : `AzInfoProtection.exe DowngradeDotNetRequirement=True`

Nous vous recommandons d’utiliser ce paramètre avec précaution, car des problèmes ont été signalés avec les applications Office. Il arrive que celles-ci se bloquent lorsque le client Azure Information Protection est utilisé avec cette ancienne version de Microsoft .NET Framework. Si vous rencontrez des problèmes de blocage, installez la version recommandée avant d’essayer d’autres solutions de dépannage. 

N’oubliez pas que si vous utilisez Windows Update pour mettre à jour le client Azure Information Protection, vous devez utiliser un autre mécanisme de déploiement de logiciels pour mettre à niveau le client vers des versions ultérieures.

### <a name="to-install-the-azure-information-protection-client-by-using-the-msi-installer"></a>Pour installer le client Azure Information Protection en utilisant le programme d’installation .msi

Pour le déploiement central, utilisez les informations suivantes qui sont spécifiques à la version .msi du client Azure Information Protection. 

Si vous utilisez Intune pour votre méthode de déploiement de logiciels, utilisez ces instructions avec [Ajouter des applications avec Microsoft Intune](/intune/deploy-use/add-apps).

1. Téléchargez la version .msi du client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 

2. Pour chaque ordinateur qui exécute le fichier .msi, vous devez vérifier que les dépendances logicielles suivantes sont établies. Par exemple, empaquetez-les avec la version .msi du client ou déployez-les uniquement sur les ordinateurs qui répondent à ces dépendances :
    
    |Version d’Office|Système d'exploitation|Logiciels|Action|
    |--------------------|--------------|----------------|---------------------|
    |Office 2016|Toutes les versions prises en charge|64 bits : [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=55007)<br /><br />32 bits : [KB3178666](https://www.microsoft.com/en-us/download/details.aspx?id=54999)<br /><br /> Version : 1.0|Installer|
    |Office 2013|Toutes les versions prises en charge|64 bits : [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54992)<br /><br /> 32 bits : [KB3172523](https://www.microsoft.com/en-us/download/details.aspx?id=54979) <br /><br />Version : 1.0|Installer|
    |Office 2010|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/en-us/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installer|
    |Office 2010|Windows 8.1 et Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB2843630 ou KB2919355 n’est pas installé|
    |Office 2010|Windows 8 et Windows Server 2012|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer|
    |Office 2010|Windows 7 et Windows Server 2008 R2|[KB2843630](https://www.microsoft.com/en-us/download/details.aspx?id=41709)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB3125574 n’est pas installé|
    |Non applicable|Windows 7|[vc_redist.x86.exe](https://www.microsoft.com/en-us/download/details.aspx?id=48145)|Installer|
    |Non applicable|Windows 7|KB2627273 <br /><br /> Numéro de version inclus dans le nom de fichier : v4|Désinstaller|

3. Pour une installation par défaut, exécutez le fichier .msi avec **/quiet/**, par exemple, `AzInfoProtection.msi /quiet`. Toutefois, vous devrez peut-être spécifier des paramètres d’installation supplémentaires qui sont documentés dans les [instructions du programme d’installation exécutable](#to-install-the-azure-information-protection-client-by-using-the-executable-installer).  


## <a name="how-to-install-the-azure-information-protection-scanner"></a>Guide pratique pour installer le scanneur Azure Information Protection

Actuellement, la version de disponibilité générale du scanneur Azure Information Protection est disponible en téléchargement séparé (**AzInfoProtectionScanner.exe**) dans le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Les versions ultérieures du scanneur seront incluses dans le client Azure Information Protection.

La préversion actuelle du client Azure Information Protection comprend également le scanneur Azure Information Protection. 

Le module PowerShell inclus avec le scanneur et la préversion du client a des applets de commande pour installer et configurer le scanneur.

Pour installer le client pour le scanneur, suivez les mêmes instructions que dans les sections précédentes. Notez que si vous n’avez pas besoin de tous les composants du client, comme le complément et la visionneuse Office, vous pouvez installer uniquement le module PowerShell. Par exemple, vous pouvez exécuter le fichier exécutable avec `PowerShellOnly=true /quiet`.

Une fois que vous avez installé le client, vous être prêt à installer le scanneur. Pour obtenir des instructions, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](../deploy-use/deploy-aip-scanner.md).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez installé le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
