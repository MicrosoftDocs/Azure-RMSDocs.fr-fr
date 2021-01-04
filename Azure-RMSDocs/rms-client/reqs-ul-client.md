---
title: Conditions supplémentaires requises pour l’installation du client d’étiquetage unifié Azure Information Protection
description: Informations destinées aux administrateurs qui doivent comprendre la configuration système supplémentaire requise pour l’installation du client d’étiquetage unifié sur les réseaux d’entreprise.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c93b0a338f25b058e517c4c2bb746ccaa6e41a69
ms.sourcegitcommit: 0ac52ea741f205692406f0f82c74c65c23ee3467
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792311"
---
# <a name="additional-requirements-for-installing-the-unified-labeling-client-on-enterprise-networks"></a>Conditions supplémentaires requises pour l’installation du client d’étiquetage unifié sur les réseaux d’entreprise

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP pour Windows et les versions d’Office dans support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Instructions pour**: [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-install.md). *

Avant d’installer le client d’étiquetage unifié Azure Information Protection sur votre réseau d’entreprise, vérifiez que les ordinateurs disposent des versions et des applications de système d’exploitation requises pour Azure Information Protection : [Configuration requise pour la Azure information protection](../requirements.md). 

Ensuite, vérifiez que vous disposez des éléments supplémentaires requis pour installer le client d’étiquetage unifié Azure Information Protection.

> [!NOTE]
> Toutes ces exigences ne sont pas vérifiées par le logiciel d’installation.
>

## <a name="microsoft-net-framework-requirements"></a>Configuration requise pour Microsoft .NET Framework

L’installation complète du client d’étiquetage unifié Azure Information Protection par défaut nécessite une version minimale de Microsoft .NET Framework 4.6.2. 

Si ce Framework est absent, l’Assistant Installation du programme d’installation exécutable tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré.  

Si vous installez le [Azure information protection Viewer](clientv2-view-use-files.md) seul, vous devez disposer d’une version minimale de Microsoft .NET Framework 4.5.2. 

> [!IMPORTANT]
> Si une version minimale de Microsoft .NET Framework 4.5.2 est manquante pour l’installation de la visionneuse, le logiciel d’installation ne la télécharge pas ou ne l’installe *pas* .
> 

### <a name="disable-exploit-protection-net-2-or-3-only"></a>Désactiver la protection contre l’exploitation (.NET 2 ou 3 uniquement)

Le client AIP n’est pas pris en charge sur les ordinateurs disposant de .NET 2 ou 3 dont la [protection contre l’exploit](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée. 

Dans ce cas, nous vous recommandons de mettre à niveau votre version .NET. 

Si vous devez conserver votre .NET version 2 ou 3, veillez à [désactiver la protection contre les attaques](../known-issues.md#known-issues-for-aip-and-exploit-protection) avant d’installer le client AIP.

## <a name="windows-powershell-minimum-requirements"></a>Configuration minimale requise pour Windows PowerShell

Le module PowerShell pour le client nécessite une version minimale de Windows PowerShell 4,0.

Si vous travaillez sur un système d’exploitation plus ancien, vous devrez peut-être Insall PowerShell manuellement. Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). 

> [!IMPORTANT]
> Le programme d’installation ne vérifie pas ou n’installe *pas* ce composant requis pour vous. 
>
> Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne `$PSVersionTable` lors d’une session PowerShell.  
> 


## <a name="screen-resolution-requirements"></a>Exigences en matière de résolution d’écran

Les ordinateurs clients avec des résolutions de **800x600** et inférieures ne peuvent pas afficher entièrement la boîte de dialogue **classer et protéger-Azure information protection** lorsque vous cliquez avec le bouton droit sur un fichier ou un dossier dans l’Explorateur de fichiers.   

## <a name="admin-permissions"></a>Autorisations d’administrateur

Pour installer le client d’étiquetage unifié Azure Information Protection, vous devez disposer d’autorisations d’administrateur local sur l’ordinateur client.
        
## <a name="windows-10-requirements"></a>Exigences de Windows 10

Les ordinateurs qui exécutent Office 2010 requièrent l' **Assistant de connexion Microsoft Online Services version 7.250.4303.0**, qui est inclus dans l’installation du client. 

Si vous disposez d’une version ultérieure de l’Assistant de connexion, désinstallez-la avant d’installer le client d’étiquetage unifié Azure Information Protection. 

Par exemple, vérifiez la version et désinstallez l’Assistant de connexion à l’aide du **panneau de configuration**  >  **programme et fonctionnalités**  >  **désinstaller ou modifier un programme**. 

Pour Windows 10 version 1809 uniquement, pour les builds du système d’exploitation postérieures à 17763.348, installez [1er mars 2019—KB4482887 (Build du système d’exploitation 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) pour que la barre Information Protection s’affiche correctement dans les applications Office. Cette mise à jour n’est pas nécessaire si vous avez Office 365 1902 ou ultérieur.    

## <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>Configurer votre stratégie de groupe pour empêcher la désactivation d’AIP

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
    

## <a name="next-steps"></a>Étapes suivantes

Poursuivez avec  [le Guide d’administration : installer le client d’étiquetage unifié Azure information protection pour les utilisateurs](clientv2-admin-guide-install.md).

Pour plus d'informations, consultez les pages suivantes :

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichiers pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)