---
title: Installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs
description: Instructions et informations permettant aux administrateurs de déployer le Azure Information Protection client d’étiquetage unifié pour Windows sur les réseaux d’entreprise.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 016dfba5d945c0411b3c6858922a2e919282e94e
ms.sourcegitcommit: 73befea74644d272e2d8d1d4b95df55c7741ccbe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97762347"
---
# <a name="admin-guide-install-the-azure-information-protection-unified-labeling-client-for-users"></a>Guide de l’administrateur : installer le client d’étiquetage unifié Azure Information Protection pour les utilisateurs

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP pour Windows et les versions d’Office dans support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Instructions pour**: [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-install.md). *

Avant d’installer le client d’étiquetage unifié Azure Information Protection sur votre réseau d’entreprise, vérifiez que les ordinateurs disposent des versions et des applications de système d’exploitation requises pour Azure Information Protection : [Configuration requise pour la Azure information protection](../requirements.md) et [exigences supplémentaires pour l’installation du client d’étiquetage unifié sur les réseaux d’entreprise](reqs-ul-client.md).

## <a name="supported-applications-for-the-unified-labeling-client"></a>Applications prises en charge pour le client d’étiquetage unifié

Le client d’étiquetage unifié Azure Information Protection peut étiqueter et protéger des documents et des e-mails à l’aide des applications Office Word, Excel, PowerPoint et Outlook de l’une des éditions Office suivantes :

- **Applications Office**, pour les versions listées dans le [tableau des versions prises en charge pour Microsoft 365 Apps par le canal de mise à jour](/officeupdates/update-history-microsoft365-apps-by-date), depuis Microsoft 365 Apps for Business ou Microsoft 365 Business Premium, lorsqu’une licence Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur
- **Microsoft 365 Apps for enterprise**
- **Office Professional Plus 2019**
- **Office Professional Plus 2016**
- **Office Professional Plus 2013 avec Service Pack 1**
- **Office Professional Plus 2010 avec Service Pack 2**

D’autres éditions d’Office (comme **standard**) ne peuvent pas protéger des documents et des e-mails à l’aide d’un service de Rights Management. Pour ces éditions, Azure Information Protection est pris en charge pour l' **étiquetage** uniquement. 

Par conséquent, les étiquettes qui appliquent la protection ne s’affichent pas pour les utilisateurs sur le bouton ou la barre de sensibilité de Azure Information Protection.

Pour plus d’informations sur les éditions d’Office qui prennent en charge le service de protection, consultez [Applications prenant en charge la protection des données Azure Rights Management](../requirements-applications.md).

Pour plus d’informations, consultez [problèmes connus des AIP dans les applications Office](../known-issues.md#aip-known-issues-in-office-applications).

## <a name="unified-labeling-client-installation-options"></a>Options d’installation du client d’étiquetage unifié

Il existe deux options d’installation du client pour les utilisateurs :

|Option  |Description  | I
|---------|---------|
|**Exécuter la version exécutable (. exe) du client**     |   La méthode d’installation recommandée que vous pouvez exécuter en mode interactif ou silencieux. <br><br>Cette méthode offre la plus grande souplesse et est recommandée, car le programme d’installation vérifie la plupart des composants requis et peut automatiquement installer les composants requis manquants. <br><br>Pour plus d’informations, consultez [installer le client d’étiquetage unifié AIP à l’aide du programme d’installation exécutable](#install-the-aip-unified-labeling-client-using-the-executable-installer).|
|**Déployer la version Windows Installer (. msi) du client**     |     Pris en charge pour les installations en mode silencieux uniquement avec l’utilisation d’un mécanisme de déploiement central, comme une stratégie de groupe, Configuration Manager ou Microsoft Intune. <br><br>Cette méthode est nécessaire pour les PC Windows 10 qui sont gérés par Intune et la gestion des appareils mobiles (MDM), car pour ces ordinateurs, les fichiers exécutables ne sont pas pris en charge pour l’installation. <br><br> Toutefois, lorsque vous utilisez cette méthode d’installation, vous devez manuellement vérifier et installer ou désinstaller le logiciel dépendant que le programme d’installation pour le fichier exécutable exécuterait pour chaque ordinateur. <br><br>Pour plus d’informations, consultez [installer le client d’étiquetage unifié à l’aide du programme d’installation. msi](#install-the-unified-labeling-client-using-the-msi-installer). |
|     |         |


Une fois le client d’étiquetage unifié Azure Information Protection installé, vous pouvez mettre à jour ce client en répétant la méthode d’installation choisie ou en utilisant Windows Update pour que le client soit mis à niveau automatiquement. 

Pour plus d’informations sur la mise à niveau, consultez la section [Mise à niveau et maintenance du client Azure Information Protection](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client).

## <a name="install-the-aip-unified-labeling-client-using-the-executable-installer"></a>Installer le client d’étiquetage unifié AIP à l’aide du programme d’installation exécutable

Utilisez les instructions suivantes pour installer le client lorsque vous *n’utilisez pas* le catalogue Microsoft Update ou si vous [déployez le fichier **. msi**](#install-the-unified-labeling-client-using-the-msi-installer) à l’aide d’une méthode de déploiement centralisée telle qu’Intune.

**Pour installer le client d’étiquetage unifié à l’aide du fichier. exe**:

1. Téléchargez la version exécutable de l’Azure Information Protection client d’étiquetage unifié (nom de fichier de **AzInfoProtection_UL**) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    > [!IMPORTANT]
    > Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 
    >
 
1. Pour une installation par défaut, il vous suffit d’exécuter le fichier exécutable, par exemple, **AzInfoProtection_UL.exe**. 

    Pour afficher toutes les options d’installation, commencez par exécuter le fichier exécutable avec **/Help**: `AzInfoProtection_UL.exe /help`

    Par exemple : 
    - Pour installer le client en mode silencieux : `AzInfoProtection_UL.exe /quiet`
    
    - Pour installer en mode silencieux uniquement les applets de commande PowerShell : `AzInfoProtection_UL.exe  PowerShellOnly=true /quiet`
    
    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :
        
    |Paramètre  |Description  |
    |---------|---------|
    |**AllowTelemetry = 0**     |    Utilisez ce paramètre pour désactiver l’option d’installation **Participer à l’amélioration d’Azure Information Protection en envoyant des statistiques d’utilisation à Microsoft**.     |
    |**ServiceLocation**     |  Utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010, et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent d’invites. <br><br>Pour plus d'informations, consultez les pages suivantes : <br>- [Plus d’informations sur le paramètre d’installation **ServiceLocation**](#more-information-about-the-servicelocation-installation-parameter) <br> - [AIP pour Windows et les versions d’Office dans le support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)      |

    | | |

1. Pour achever l'installation : 

    - **Si votre ordinateur exécute [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)**, redémarrez votre ordinateur. 
        
        Si le client n’a pas été installé avec le paramètre **ServiceLocation** , lorsque vous ouvrez pour la première fois l’une des applications Office qui utilisent le client unifié Azure information protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le registre pour cette première utilisation. 

        La fonction [Détection du service](client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - **Pour les autres versions d’Office**, redémarrez toutes les applications Office et toutes les instances de l’Explorateur de fichiers. 
        
1. Vérifiez que l’installation a réussi en consultant le fichier journal d’installation, qui est créé par défaut dans le dossier **% temp%** . 

    Le format de nom du fichier journal d’installation est le suivant : `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    Par exemple : **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    Dans ce fichier journal, recherchez la chaîne suivante : **Product : Microsoft Azure information protection--installation terminée**. En cas d’échec de l’installation, ce fichier journal contient des informations pour vous aider à identifier et résoudre les problèmes.

    > [!TIP]
    > Vous pouvez modifier l’emplacement du fichier journal d’installation avec le paramètre d’installation **/log** . 
    >  
### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Plus d’informations sur le paramètre d’installation ServiceLocation

Quand vous installez le client pour les utilisateurs qui disposent d' [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support) et qu’ils ne disposent pas d’autorisations d’administrateur local, spécifiez le paramètre **SERVICELOCATION** et l’URL de votre service Azure Rights Management. 

Ce paramètre et la valeur créent et définissent les clés de registre suivantes :

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation`

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing`

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation`


**Pour identifier la valeur à spécifier pour le paramètre ServiceLocation :**

1. À partir d’une session PowerShell, exécutez d’abord [Connect-AipService](/powershell/module/aipservice/connect-aipservice) et spécifiez vos informations d’identification d’administrateur pour vous connecter au service Azure Rights Management. Exécutez ensuite la [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration). 
 
    Si vous n’avez pas encore installé le module PowerShell pour le service Azure Rights Management, consultez [installation du module PowerShell AIPService](../install-powershell.md).

2. Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

    Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. Supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne restante correspond à la valeur à spécifier pour le paramètre ServiceLocation.

Par exemple, pour installer le client en mode silencieux pour [Office 2010](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support) et Azure RMS :

```powershell
AzInfoProtection_UL.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
```


## <a name="install-the-unified-labeling-client-using-the-msi-installer"></a>Installer le client d’étiquetage unifié à l’aide du programme d’installation. msi

Pour le déploiement central, utilisez les informations suivantes, spécifiques à la version d’installation **. msi** du client d’étiquetage unifié Azure information protection. 

Si vous utilisez Intune pour votre méthode de déploiement de logiciels, utilisez ces instructions avec [Ajouter des applications avec Microsoft Intune](/mem/intune/apps/apps-add).

**Pour installer le client d’étiquetage unifié avec le fichier. msi**

1. Téléchargez la version **. msi** du Azure information protection **AzInfoProtection_UL**(Unified étiquetage client) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018). 
    
    > [!IMPORTANT]
    > Si une préversion est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production.
    > 

1. Pour chaque ordinateur qui exécute le fichier **. msi** , vous devez vous assurer que les dépendances logicielles suivantes sont en place. 

    Par exemple, empaquetez-les avec la version **. msi** du client ou déployez uniquement sur les ordinateurs qui répondent à ces dépendances :
    
    |Version d’Office|Système d’exploitation|Logiciel|Action|
    |--------------------|--------------|----------------|---------------------|
    |**Toutes les versions, à l’exception d’Office 365 1902 ou ultérieur**|Windows 10 version 1809 uniquement, builds du système d’exploitation postérieures à 17763.348|[KB 4482887](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887)|Installer|
    |**Office 2016**|Toutes les versions prises en charge|64 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=55007)<br /><br />32 bits : [KB3178666](https://www.microsoft.com/download/details.aspx?id=54999)<br /><br /> Version : 1.0|Installer|
    |**Office 2013**|Toutes les versions prises en charge|64 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54992)<br /><br /> 32 bits : [KB3172523](https://www.microsoft.com/download/details.aspx?id=54979) <br /><br />Version : 1.0|Installer|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Toutes les versions prises en charge|[Assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)<br /><br /> Version : 2.1|Installer|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Windows 8.1 et Windows Server 2012 R2|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer si KB2843630 ou KB2919355 n’est pas installé|
    |[**Office 2010**](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)|Windows 8 et Windows Server 2012|[KB2843630](https://www.microsoft.com/download/details.aspx?id=41708)<br /><br /> Numéro de version inclus dans le nom de fichier : v3|Installer|
    | | | | |

1. Pour une installation par défaut, exécutez le fichier .msi avec **/quiet/**, par exemple, `AzInfoProtection_UL.msi /quiet`.

    Vous devrez peut-être spécifier des paramètres d’installation supplémentaires. Pour plus d’informations, consultez les [instructions du programme d’installation exécutable](#install-the-aip-unified-labeling-client-using-the-executable-installer).

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