---
title: The client for Azure Information Protection - AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: a5139eed7bccb8a7a57fda0a3b346a1965f7ea50
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474327"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*Applies to: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- The client can be the built-in labeling client for Office, the Azure Information Protection unified labeling client for Windows, the Azure Information Protection client (classic) for Windows, or the Rights Management client.
    
    These clients are often referred to as the **Office built-in labeling client**, the **unified labeling client**, the **classic client**, and the **RMS client**, respectively. Whichever client you use, it integrates with applications that you run on computers and mobile devices.

- The service resides in the cloud or on-premises. The cloud service is Azure Information Protection, which uses the Azure Rights Management service for the data protection. The on-premises service is Active Directory Rights Management Services, more commonly known as AD RMS. 

All these clients integrate with Office applications but the unified labeling client and the classic client must be installed separately and support additional features and components. For example, these clients include support for File Explorer, so you can classify and protect files outside Office. Additional components include a viewer for protected PDF documents and protected images, and a scanner for on-premises data stores.

The RMS client provides protection only. This client is automatically installed with some applications, such as Office applications, the Azure Information Protection clients, and RMS-enlightened applications from software vendors. Toutefois, il peut également être [installé de manière autonome](https://www.microsoft.com/en-us/download/details.aspx?id=38396) pour prendre en charge la [synchronisation des fichiers à partir des bibliothèques protégées par IRM et de OneDrive Entreprise](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668), et pour les développeurs souhaitant intégrer la protection de gestion des droits aux applications métier.

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>Choose which labeling client to use for Windows computers

Where possible, use one of the labeling clients because labels abstract the complexity of applying protection for users, and labels also provide classification so you can track and manage your data.

Your choice of labeling client for your Windows computers might be influenced by which management portal you use:

- The Office built-in labeling client and the Azure Information Protection unified labeling client download labels and policy settings from the following admin centers: 
    - Office 365 Security & Compliance Center
    - Microsoft 365 security center
    - Microsoft 365 compliance center

- The Azure Information Protection client (classic) downloads label and policy settings from the Azure portal.

Because the unified labeling client and the classic client require a separate installation to Office, you must download and install these clients from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Which client should you use?

- Use the **labeling client built in to Office** for your Windows computers when you have Office 365 apps that are a minimum version 1910, you want to use the same labels and policy settings that can also be used by MacOS, iOS, and Android, and you don't need features in your Office apps that require the unified labeling client or classic client. These features include the Information Protection bar under the ribbon for easier label selection and visibility. This client supports switching accounts, and because it doesn't use an Office add-in, it has better performance in Office apps than using either of the Azure Information Protection clients.

- Use the **Azure Information Protection unified labeling client** on Windows computers for labels and policy settings that can also be used by MacOS, iOS, and Android, you want to label files independently from Office 365 apps, and you don’t need features that are only supported by the classic client. These features currently include protecting content with an on-premises key (HYOK) and a general availability version of the scanner for on-premises data stores.

- Install the **Azure Information Protection client (classic)** on Windows computers if you need a version of the client that has features that are not yet available with the unified labeling client. Although this client can use the same labels as those used by MacOS, iOS, and Android, it has different policy settings. So your tradeoff is administration using another management portal and a different user experience for users.

The latest version of the unified labeling client brings it to close parity in features with the classic client. As this gap closes, you can expect new features to be added only to the unified labeling client. For this reason, we recommend you deploy the unified labeling client if its current feature set and functionality meet your business requirements. If not, or if you have configured labels in the Azure portal that you haven't yet [migrated to the unified labeling store](../configure-policy-migrate-labels.md), use the classic client.

You can use different clients in the same environment to support different business requirements, as demonstrated in the following deployment example. In a mixed client environment, we recommend you use unified labels so that clients share the same set of labels for ease of administration. New customers have unified labels by default because their tenants are on the unified labeling platform. For more information, see [How can I determine if my tenant is on the unified labeling platform?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

When you have a Windows computer that runs Office 365 apps that are a minimum version 1910 and one of the Azure Information Protection clients is installed, by default the built-in labeling client is disabled in Office apps. However, you can change this behavior to use the built-in labeling client for just your Office apps. With this configuration, the Azure Information Protection client (classic or unified labeling) remains available for labeling in File Explorer, PowerShell, and the scanner. For instructions to disable the Azure Information Protection client in Office 365 apps, see the section [Can sensitivity labels run alongside the Azure Information Protection client in Office for Windows?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#can-sensitivity-labels-run-alongside-the-azure-information-protection-client-in-office-for-windows) from the Office documentation.

##### <a name="example-deployment-strategy"></a>Example deployment strategy:

- For the majority of users, you deploy the Azure Information Protection unified labeling client because this client meets the business needs for these users. 
    
    For these users, their labeling experience is very similar across Windows, Mac, iOS, and Android because they have the same labels published to them and the same policy settings. As an admin, you manage these labels and policy settings in the same management center.

- You also install the unified labeling client for yourself, to test the preview version of the Azure Information Protection scanner.

- For a subset of users, you deploy the classic client because these users require labels that apply hold your own key (HYOK) protection.
    
    For these users, they have a slightly different labeling experience when they use this client. For example, they see a **Protect** button rather than a **Sensitivity** button in Office apps. As an admin, you need to manage their labels for HYOK settings and policy settings in a different management center to the labels and settings for the other client platforms.

- You have on-premises data stores with documents that need to be scanned for sensitive information, or classified and protected. For production use, you deploy the classic client on servers to run the Azure Information Protection scanner.

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Compare the labeling clients for Windows computers

Use the following table to help compare which features are supported by the three labeling clients for Windows computers.

To compare the Office built-in sensitivity labeling features across different operating system platforms (Windows, MacOS, iOS, and Android) and for the web, see the Office documentation, [What sensitivity label capabilities are supported in Office today?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#what-sensitivity-label-capabilities-are-supported-in-office-today)

|Composant|Classic client|Unified labeling client|Office built-in labeling client|
|:------|:------------:|:---------------------:|:-----------------------------:|
|Manual labeling:| **Oui** | **Oui** |**Oui** |
|Default label:| **Oui** | **Oui** | **Oui** |
|Recommended or automatic labeling:| **Oui** | **Oui** | Non |
|Mandatory labeling:| **Oui** | **Oui** | Non |
|User-defined permissions for a label:<br />- Do Not Forward for emails<br />- Custom permissions for Word, Excel, PowerPoint, File Explorer| **Oui** | **Oui** | Non |
|Multilanguage support for labels:| **Oui** | **Oui** |**Oui** |
|Héritage d’étiquette à partir des pièces jointes aux e-mails :| **Oui** | **Oui**  |Non |
|Customizations that include:<br />- Étiquette par défaut pour e-mail<br />- Pop-up messages in Outlook <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| **Yes** <sup>1</sup> | **Yes** <sup>2</sup> | Non |
|Scanneur pour magasins de données locaux :| **Oui** | **Yes <br />(preview)** | Non |
|Création centralisée de rapports (analytique) :| **Oui** | **Oui** | Non |
|Custom permissions set independently from a label:| **Oui** | **Yes** <sup>3</sup>| Non |
|Barre Information Protection dans les applications Office :| **Oui** | **Oui**| Non |
|Visual markings as a label action (header, footer, watermark):| **Oui** | **Oui** | **Oui**|
|Per app visual markings:| **Oui** | Non | Non |
|Dynamic visual markings with variables:| **Oui** | Non | Non |
|Label with File Explorer:| **Oui** | **Oui** | Non |
|A viewer for protected files (text, images, PDF, .pfile):| **Oui** | **Oui** | Non|
|PPDF support for applying labels:| **Oui** | Non | Non |
|PowerShell labeling cmdlets:| **Oui** | **Yes** <sup>4</sup> | Non |
|Prise en charge hors connexion des actions de protection :| **Oui** | **Yes** <sup>5</sup> | **Oui** |
|Manual policy file management for disconnected computers:| **Oui** |**Yes** <sup>6</sup>| Non |
|Prise en charge de HYOK :| **Oui** | Non | Non |
|Usage logging in Event Viewer:| **Oui** | Non |Non |
|Display the Do Not Forward button in Outlook:| **Oui** | Non | Non |
|Track protected documented:| **Oui** | **Yes** <sup>7</sup> | Non |
|Revoke protected documents:| **Oui** | Non | Non |
|Mode Protection uniquement (pas d’étiquettes) :| **Oui** | Non | Non |
|Support for account switching:| Non | Non | **Oui** |
|Prise en charge des services AD RMS :| **Oui** | No <sup>8</sup> | Non |

Notes de bas de page :

<sup>1</sup> These settings, and many more are supported as [advanced client settings that you configure in the Azure portal](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal).

<sup>2</sup> These settings, and many more are supported as [advanced settings that you configure with PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).

<sup>3</sup> Supported by File Explorer and PowerShell. In Office apps, users can select **File Info** > **Protect Document** > **Restrict Access**.

<sup>4</sup> No support to remove protection from container files (zip, .rar, .7z, .msg, and .pst).

<sup>5</sup> For File Explorer and PowerShell commands, the user must be connected to the internet to protect files.

<sup>6</sup> Supported for labeling with File Explorer, PowerShell, and the scanner. Not supported for labeling in Office apps.

<sup>7</sup> The document tracking site that's supported by the classic client isn't supported by the unified labeling client. However, without the need to first register the document for tracking, administrators can use [central reporting](../reports-aip.md) to identify whether protected documented are accessed from Windows computers, and whether access was granted or denied. 

<sup>8</sup> Labeling and protection actions aren't supported. However, for an AD RMS deployment, the viewer can open protected documents when you use the [Active Directory Rights Management Services Mobile Device Extension](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Detailed comparisons for the Azure Information Protection clients

When the Azure Information Protection client (classic) and the Azure Information Protection unified labeling client both support the same feature, use the following table to help identify some functional differences between the two clients.

|Fonctionnalités |Classic client|Unified labeling client|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurer :| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|Sélection et affichage d’étiquette en cas d’application dans les applications Office :|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|Gérer la barre Information Protection dans les applications Office :|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Protéger** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, par défaut, elle est masquée dans cette application, mais continue de s’afficher automatiquement dans les applications récemment ouvertes. <br /><br /> Pour les administrateurs : <br /><br />- Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre à la première ouverture d’une application, et de contrôler si la barre reste automatiquement masquée pour les applications récemment ouvertes une fois qu’un utilisateur a choisi de masquer la barre|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Critère de diffusion** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, celle-ci est masquée dans cette application et dans les applications récemment ouvertes <br /><br />Pour les administrateurs : <br /><br />- PowerShell setting to manage the bar |
|Couleur d’étiquette : | À configurer dans le portail Azure | Retained after label migration and configurable with [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Labels support different languages:| À configurer dans le portail Azure | Configure by using Office 365 Security & Compliance PowerShell and the *LocaleSettings* parameter for [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) and [Set-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|Mise à jour de la stratégie : | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 24 heures <br /><br />For the scanner: Every hour and when the service starts and the policy is older than one hour| Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 4 heures <br /><br />For the scanner: Every 4 hours|
|Formats pris en charge pour PDF :| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /><br /> - .ppdf <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br /> <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint|
|Generically protected files (.pfile) opened with the viewer:| File opens in the original app where it can then be viewed, modified, and saved without protection | File opens in the original app where it can then be viewed and modified, but not saved|
|Cmdlets prises en charge :| Cmdlets for labeling and cmdlets for protection-only | Cmdlets for labeling:<br /><br /> Set-AIPFileClassification and Set-AIPFileLabel don't support the *Owner* parameter <br /><br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> Set-AIPFileClassification supports the *WhatIf* parameter, so it can be run in discovery mode <br /><br /> La cmdlet Set-AIPFileLabel ne prend pas en charge le paramètre *EnableTracking*. <br /><br /> La cmdlet Get-AIPFileStatus ne retourne aucune information d’étiquette à partir d’autres abonnés et n’affiche pas le paramètre *RMSIssuedTime*.<br /><br />In addition, the *LabelingMethod* parameter for Get-AIPFileStatus displays **Privileged** or **Standard** instead of **Manual** or **Automatic**. Pour plus d’informations, consultez la [documentation en ligne](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Invites de justification (si configurées) par action dans Office : | Frequency: Per file <br /><br /> Diminution du niveau de confidentialité <br /><br /> Suppression d’une étiquette<br /><br /> Suppression de la protection | Frequency: Per session <br /><br /> Diminution du niveau de confidentialité<br /><br /> Suppression d’une étiquette|
|Supprimer les actions de l’étiquette appliquée : | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou l’étiquette automatique (si configurée) n’est pas appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.  <br /><br />| L’utilisateur n’a pas à confirmer la suppression.<br /><br /> L’étiquette par défaut ou l’étiquette automatique (si configurée) est appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.|
|Automatic and recommended labels: | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br /><br />- Nombre de valeurs uniques/non uniques <br /><br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br /><br />- Nombre de valeurs uniques seulement <br /><br />- Nombre de valeurs minimales et maximales <br /><br />- Prise en charge des clauses AND et OR avec les types d’informations <br /><br />- Dictionnaire de mots clés<br /><br />- Niveau de confiance et proximité des caractères personnalisables|
|Customizable policy tip for automatic and recommended labels: | Oui <br /><br />Use the Azure portal to replace the default message to users | Non <br /><br /> Although the admin centers have an option to supply a customized policy tip, this option is not currently supported by the unified labeling client|
|Change the default protection behavior for file types: | You can use [registry edits](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) to override the defaults of native and generic protection | You can use [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) to change which file types get protected|

For a detailed comparison of behavior differences for specific protection settings, see [Comparing the behavior of protection settings for a label](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Features not planned to be in the Azure Information Protection unified labeling client

Although the Azure Information Protection unified labeling client is still under development, the following features and behavior differences from the classic client are not currently planned to be available in future releases for the unified labeling client: 

- Support Office apps for disconnected computers with manual policy file management

- Custom permissions as a separate option that users can select in Office apps: Word, Excel, and PowerPoint

- Suivre et révoquer depuis des applications Office et l’Explorateur de fichiers

- Barre de titre et info-bulle Azure Information Protection

- Protection-only mode (no labels) using templates

- Protéger le document PDF en tant que format .ppdf

- Afficher le bouton Ne pas transférer dans Outlook

- Stratégie de démonstration

- Justification de la suppression de la protection

- Confirmation prompt **Do you want to delete this label?** for users when you don't use the policy setting for justification

- Applets de commande PowerShell distinctes pour la connexion à un service Rights Management


### <a name="parent-labels-and-their-sublabels"></a>Étiquettes parentes et sous-étiquettes associées 

The Azure Information Protection client (classic) doesn't support configurations that specify a parent label that has sublabels. Ces configurations incluent la spécification d’une étiquette par défaut et d’une étiquette pour la classification automatique ou recommandée. Si une étiquette dispose de sous-étiquettes, vous pouvez spécifier l’une d’elles, mais pas l’étiquette parente.

Pour des raisons de parité, le client d’étiquetage unifié Azure Information Protection ne prend pas non plus en charge l’application d’étiquettes parentes comportant des sous-étiquettes, même si elles peuvent être sélectionnées dans les centres d’administration. Dans ce scénario, le client d’étiquetage unifié Azure Information Protection n’applique pas l’étiquette parente.

## <a name="next-steps"></a>Étapes suivantes

To install and configure the Azure Information Protection clients, use the following documentation:

- [Client Azure Information Protection](AIP-client.md)

- [Client d’étiquetage unifié Azure Information Protection](unifiedlabelingclient-version-release-history.md)

For more information about using the built-in labeling client for Office 365 apps, see [Sensitivity labels in Office apps](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps).
