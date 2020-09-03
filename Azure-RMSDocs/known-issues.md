---
title: Problèmes connus-Azure Information Protection
description: Recherchez et parcourez les problèmes connus et les limitations de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/30/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 926c24ae3bd7960df21aba508bdf2edc83f29e9f
ms.sourcegitcommit: 11ff3752e45de3d688efc985fe0f327aabee35de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2020
ms.locfileid: "89422379"
---
# <a name="known-issues---azure-information-protection"></a>Problèmes connus-Azure Information Protection

Utilisez les listes et les tableaux ci-dessous pour trouver des informations sur les problèmes connus et les limitations liées aux fonctionnalités de Azure Information Protection.

> [!NOTE]
> Cet article fait référence aux problèmes connus dans les clients d’étiquetage classiques et unifiés. Vous ne connaissez pas trop la différence entre ces clients ? Consultez le [Forum aux questions](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).

## <a name="client-support-for-container-files-such-as-zip-files"></a>Prise en charge des fichiers de conteneur par les clients, tels que les fichiers. zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection. Toutefois, vous pouvez supprimer la protection pour tous les fichiers inclus dans des fichiers conteneurs pris en charge à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

Pour plus d’informations, consultez [le Guide de l’administrateur : types de fichiers pris en charge par le client Azure information protection](rms-client/client-admin-guide-file-types.md).

## <a name="known-issues-for-installing-the-aip-client"></a>Problèmes connus liés à l’installation du client AIP

Le client Azure Information Protection n’est pas pris en charge sur les ordinateurs sur lesquels la [protection contre l’exploitation](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) est activée.

Veillez à désactiver la protection contre les attaques avant d’installer AIP. 

Pour désactiver la protection contre les attaques par le biais de PowerShell, exécutez la commande suivante :

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

Pour plus d’informations, consultez [Azure information Protection Requirements](requirements.md).

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Prise en charge de PowerShell pour le client Azure Information Protection

La version actuelle du module PowerShell **AzureInformationProtection** qui est installée avec le client Azure information protection présente les problèmes connus suivants :

- **Dossiers personnels Outlook (* fichiers. pst *) * *. La protection native des fichiers *. pst* n’est pas prise en charge à l’aide du module **AzureInformationProtection** .

- **Messages électroniques protégés par Outlook *(fichiers. rpmsg* )**. La déprotection des messages électroniques protégés par Outlook est prise en charge par le module **AzureInformationProtection** uniquement s’ils se trouvent dans un dossier personnel Outlook *(fichier. pst* ).

    La déprotection des messages électroniques en dehors d’un fichier *. pst* n’est pas prise en charge.

Pour plus d’informations, consultez [le Guide de l’administrateur : utilisation de PowerShell avec le client Azure information protection](rms-client/client-admin-guide-powershell.md).

## <a name="aip-known-issues-in-office-applications"></a>Problèmes connus liés à AIP dans les applications Office

|Fonctionnalité  |Problèmes connus  |
|---------|---------|
|**Plusieurs versions d’Office**    | Les clients Azure Information Protection, y compris les étiquetages classiques et unifiés, ne prennent pas en charge plusieurs versions d’Office sur le même ordinateur ou n’échangent pas de comptes d’utilisateur dans Office.       |
|**Affichages multiples** |Si vous utilisez plusieurs affichages et que vous avez une application Office ouverte : </br></br>-Vous pouvez rencontrer des problèmes de performances dans vos applications Office.</br>-La barre de Azure Information Protection peut sembler flotter au milieu de l’écran du bureau, sur l’un ou l’autre des écrans </br></br>Pour garantir des performances cohérentes et que la barre reste à l’emplacement approprié, ouvrez la boîte de dialogue **options** de votre application Office et, sous **général,** sélectionnez **optimiser pour la compatibilité** plutôt que **optimiser pour une meilleure apparence.**    |
|**Prise en charge d’IRM dans Office 2016**| Le paramètre de Registre [DRMEncryptProperty](https://docs.microsoft.com/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) , qui contrôle le chiffrement des métadonnées dans Office 2016, n’est pas pris en charge pour les étiquettes de Azure information protection.|
|**Marquages de contenu dans Word**    | Azure Information Protection [marquages](configure-policy-markings.md) de contenu peuvent être masqués dans les pieds de page Microsoft Word, lorsque le pied de page contient également un tableau. Pour plus d’informations, consultez la page [quand des marquages visuels sont appliqués](configure-policy-markings.md#when-visual-markings-are-applied). |
|**Fichiers joints aux courriers électroniques** |En raison d’une limitation dans les mises à jour Windows récentes, lorsque [Microsoft Outlook est protégé par Azure Rights Management](office-apps-services-support.md), les fichiers joints aux courriers électroniques peuvent être verrouillés après l’ouverture du fichier. |
|**Fusion et publipostage**    |  La fonctionnalité de [fusion et](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) publipostage d’Office n’est pas prise en charge avec les fonctionnalités de Azure information protection.       |
| **Courriers électroniques S/MIME** | L’ouverture des e-mails S/MIME dans le volet de lecture d’Outlook peut entraîner des problèmes de performances. </br></br>Pour éviter les problèmes de performances avec les e-mails S/MIME, activez la propriété avancée [**OutlookSkipSmimeOnReadingPaneProperty**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) . </br></br>**Remarque :** L’activation de cette propriété empêche l’affichage de la barre AIP ou de la classification des messages dans le volet de lecture d’Outlook. |
| | |

## <a name="known-issues-in-policies"></a>Problèmes connus dans les stratégies

La publication des stratégies peut prendre jusqu’à 24 heures.

## <a name="known-issues-in-the-aip-client"></a>Problèmes connus dans le client AIP

- **Tailles de fichier maximales. Les fichiers** de plus de 2 Go sont pris en charge pour la protection, mais pas pour le déchiffrement.

- **Visionneuse AIP.** La visionneuse AIP affiche des images en mode portrait, et certaines images larges et de vue paysage peuvent sembler étirées.

    Par exemple, une image d’origine est représentée ci-dessous à gauche, avec une version en mode portrait étirée dans la visionneuse AIP à droite. 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="Image étirée dans la visionneuse cliente":::
    
    Pour plus d'informations, consultez les pages suivantes :

    - [**Client classique**: afficher les fichiers protégés avec la visionneuse de Azure information protection](rms-client/client-view-use-files.md)
    - [**Client d’étiquetage unifié**: afficher les fichiers protégés avec la visionneuse de Azure information protection](rms-client/clientv2-view-use-files.md)

## <a name="more-information"></a>Informations complémentaires

Les articles supplémentaires suivants peuvent être utiles pour répondre à des questions sur les problèmes connus dans Azure Information Protection :

- [Forum aux questions sur Azure Information Protection](faqs.md)
- [Forum aux questions sur la protection des données dans Azure Information Protection](faqs-rms.md)
- [Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection](faqs-infoprotect.md)
- [FAQ pour l’application Microsoft Azure Information Protection pour iOS et Android](rms-client/mobile-app-faq.md)

