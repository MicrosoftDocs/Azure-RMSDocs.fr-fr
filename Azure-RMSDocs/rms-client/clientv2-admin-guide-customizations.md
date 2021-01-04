---
title: Configurations personnalisées-Azure Information Protection client d’étiquetage unifié
description: Informations sur la personnalisation de l’Azure Information Protection client d’étiquetage unifié pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/23/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3deab3f361667a79905ab91842361d270b4323d7
ms.sourcegitcommit: b9d7986590382750e63d9059206a40d28fc63eef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97764167"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection

<!-- Notes for contributors: In this file, you can add new settings on at the bottom of the page to simplify the content editing. However, remember to add the xref by setting AND by feature to the reference sections at the top. 

There are two types of reference sections - the legacy table by setting name, and a newer section of reference by feature type. This newer section helps admins understand and configure settings that are relevant to eachother, possibly in a sort of a flow. 

FUTURE task - reorganize this topic by feature type so that admins can read related settings together. NOT recommended to reorganize this page into sub-pages as there are too many xrefs out there to this page and you'll need a lot of redirects. Additionally, users might just search for their setting or text on a single page. It would help to have related settings documented one right after the other to help with scrolling. -->

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP pour Windows et les versions d’Office dans support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Concerne :** [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-customizations.md). *

Utilisez les informations suivantes pour les configurations avancées nécessaires pour des scénarios ou des utilisateurs spécifiques lors de la gestion du client d’étiquetage unifié AIP.

> [!NOTE]
> Ces paramètres requièrent la modification du registre ou la spécification de paramètres avancés. Les paramètres avancés utilisent [Office 365 Security & Compliance Center PowerShell](/powershell/exchange/office-365-scc/office-365-scc-powershell).
> 

## <a name="configuring-advanced-settings-for-the-client-via-powershell"></a>Configuration des paramètres avancés pour le client via PowerShell

Utilisez la Microsoft 365 Security & Compliance Center PowerShell pour configurer des paramètres avancés pour la personnalisation des étiquettes et des stratégies d’étiquette. 

Dans les deux cas, une fois que vous êtes [connecté à Office 365 Security & Compliance Center PowerShell](/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell), spécifiez le paramètre **AdvancedSettings** avec l’identité (nom ou GUID) de la stratégie ou de l’étiquette, avec des paires clé/valeur dans une [table de hachage](/powershell/module/microsoft.powershell.core/about/about_hash_tables). 

Pour supprimer un paramètre avancé, utilisez la même syntaxe de paramètre **AdvancedSettings** , mais spécifiez une valeur de chaîne NULL. 

> [!IMPORTANT]
> N’utilisez pas d’espaces blancs dans vos valeurs de chaîne. Les chaînes blanches dans ces valeurs de chaîne empêcheront l’application de vos étiquettes.

Pour plus d'informations, consultez les pages suivantes :

- [Syntaxe des paramètres avancés de la stratégie d’étiquette](#label-policy-advanced-settings)
- [Syntaxe des paramètres avancés des étiquettes](#label-advanced-settings)
- [Exemples de paramétrage des paramètres avancés](#examples-for-setting-advanced-settings)
- [Spécification de la stratégie d’étiquette ou de l’identité de l’étiquette](#specifying-the-label-policy-or-label-identity)
- [Ordre de priorité-mode de résolution des paramètres en conflit](#order-of-precedence---how-conflicting-settings-are-resolved)
- [Références de paramètres avancés](#advanced-setting-references)
### <a name="label-policy-advanced-settings"></a>Paramètres avancés de la stratégie d’étiquette

Un exemple de paramètre avancé de stratégie d’étiquette est le paramètre permettant d’afficher la barre d’Information Protection dans les applications Office.

**Pour une valeur de chaîne unique**, utilisez la syntaxe suivante :

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}
```

**Pour une valeur de chaîne multiple pour la même clé**, utilisez la syntaxe suivante :

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

### <a name="label-advanced-settings"></a>Paramètres avancés des étiquettes

Un exemple de paramètre avancé d’étiquette est le paramètre permettant de spécifier une couleur d’étiquette.

**Pour une valeur de chaîne unique**, utilisez la syntaxe suivante :

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}
```

**Pour une valeur de chaîne multiple pour la même clé**, utilisez la syntaxe suivante :

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

### <a name="examples-for-setting-advanced-settings"></a>Exemples de paramétrage des paramètres avancés

**Exemple 1 :** Définir un paramètre avancé pour une stratégie d’étiquette pour une valeur de chaîne unique :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

**Exemple 2 :** Définissez un paramètre avancé pour une étiquette pour une valeur de chaîne unique :

```PowerShell
Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}
```

**Exemple 3 :** Définissez un paramètre avancé pour les étiquettes pour plusieurs valeurs de chaîne :

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

**Exemple 4 :** Supprimez un paramètre avancé de stratégie d’étiquette en spécifiant une valeur de chaîne NULL :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}
```

### <a name="specifying-the-label-policy-or-label-identity"></a>Spécification de la stratégie d’étiquette ou de l’identité de l’étiquette

La recherche du nom de la stratégie d’étiquette pour le paramètre d' **identité** PowerShell est simple, car il n’existe qu’un seul nom de stratégie dans le centre d’administration d’étiquetage.

Toutefois, pour les étiquettes, les centres d’administration d’étiquetage affichent un **nom** et une valeur de **nom complet** . Dans certains cas, ces valeurs sont les mêmes, mais elles peuvent être différentes. Pour configurer les paramètres avancés des étiquettes, utilisez la valeur **nom** .

Par exemple, pour identifier l’étiquette dans l’image suivante, utilisez la syntaxe suivante dans votre commande PowerShell : `-Identity "All Company"` :

![Utiliser’name’plutôt que’Display Name’pour identifier une étiquette de sensibilité](../media/labelname_scc.png)

Si vous préférez spécifier le **GUID** de l’étiquette, cette valeur n’est *pas* affichée dans le centre d’administration d’étiquetage. Utilisez la commande [« obtenir une étiquette »](/powershell/module/exchange/get-label) pour rechercher cette valeur, comme suit :

```PowerShell
Get-Label | Format-Table -Property DisplayName, Name, Guid
```

Pour plus d’informations sur les noms d’étiquettes et les noms d’affichage :

- **Nom** est le nom d’origine de l’étiquette et il est unique pour toutes vos étiquettes. 

    Cette valeur reste la même, même si vous avez modifié votre nom d’étiquette par la suite. Pour les étiquettes de sensibilité qui ont été migrées à partir de Azure Information Protection, vous pouvez voir l’ID d’étiquette d’origine à partir du Portail Azure.

- **Nom complet** est le nom actuellement affiché pour les utilisateurs de l’étiquette et n’a pas besoin d’être unique sur toutes vos étiquettes. 

    Par exemple, vous pouvez avoir un nom d’affichage de **tous les employés** pour une sous-étiquette sous l’étiquette **confidentiel** , et un autre nom d’affichage de  **tous les employés** pour une sous-étiquette sous l’étiquette **hautement confidentiel** . Ces sous-étiquettes affichent le même nom, mais elles ne sont pas de la même étiquette et présentent des paramètres différents.

### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordre de priorité-mode de résolution des paramètres en conflit

Vous pouvez utiliser les centres d’administration pour configurer les paramètres de stratégie d’étiquette suivants :

- **Appliquer cette étiquette par défaut aux documents et aux e-mails**

- **Les utilisateurs doivent fournir une justification pour supprimer une étiquette ou une étiquette de classification inférieure**

- **Demander aux utilisateurs d’appliquer une étiquette à leur adresse de messagerie ou à leur document**

- **Fournir aux utilisateurs un lien vers une page d’aide personnalisée**

Lorsque plusieurs stratégies d’étiquette sont configurées pour un utilisateur, chacune avec des paramètres de stratégie potentiellement différents, le dernier paramètre de stratégie est appliqué en fonction de l’ordre des stratégies dans le centre d’administration. Pour plus d’informations, consultez priorité de la [stratégie d’étiquette (ordre important)](/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters) .

Les paramètres avancés de la stratégie d’étiquette sont appliqués à l’aide de la même logique, à l’aide du dernier paramètre de stratégie.

> [!NOTE]
> Dans la version GA actuelle, il existe une exception pour le paramètre de stratégie [OutlookDefaultLabel](#set-a-different-default-label-for-outlook) Advanced label, qui vous permet de définir une étiquette par défaut différente pour Outlook.
> 
> Si vous avez des conflits pour le paramètre [OutlookDefaultLabel](#set-a-different-default-label-for-outlook) , la configuration est effectuée à partir du premier paramètre de stratégie, en fonction de l’ordre de la stratégie dans le centre d’administration. 
>
> Cette exception a été supprimée dans le cadre de la préversion publique [2.9.109.0](unifiedlabelingclient-version-release-history.md#version-291090-public-preview) .

## <a name="advanced-setting-references"></a>Références de paramètres avancés

Les sections suivantes présentent les paramètres avancés disponibles pour les étiquettes et les stratégies d’étiquette :

- [Référence des paramètres avancés par fonctionnalité](#advanced-setting-reference-by-feature)
- [Référence des paramètres avancés de la stratégie d’étiquette](#label-policy-advanced-setting-reference)
- [Référence des paramètres avancés des étiquettes](#label-advanced-setting-reference)
### <a name="advanced-setting-reference-by-feature"></a>Référence des paramètres avancés par fonctionnalité

Les sections suivantes répertorient les paramètres avancés décrits sur cette page par l’intégration de produits et de fonctionnalités :

|Fonctionnalité  |Paramètres avancés  |
|---------|---------|
|**Paramètres Outlook et de messagerie**     | - [Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook) <br> - [Personnaliser les messages de la fenêtre contextuelle Outlook](#customize-outlook-popup-messages) <br>- [Activer la classification recommandée dans Outlook](#enable-recommended-classification-in-outlook)<br> - [Exempter les messages Outlook de l’étiquetage obligatoire](#exempt-outlook-messages-from-mandatory-labeling) <br>- [Pour les courriers électroniques avec pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes.](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)<br>- [Développer les listes de distribution Outlook lors de la recherche de destinataires de courrier électronique](#expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview) <br>- [Implémenter des messages contextuels dans Outlook pour avertir, justifier ou bloquer l’envoi de courriers électroniques](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) <br>- [Empêcher les problèmes de performances d’Outlook avec les e-mails S/MIME](#prevent-outlook-performance-issues-with-smime-emails)   <br>- [Définir une autre étiquette par défaut pour Outlook](#set-a-different-default-label-for-outlook) |
|**Paramètres PowerPoint** | - [Évitez de supprimer des formes de PowerPoint qui contiennent du texte spécifié, et qui ne sont pas des en-têtes et des pieds de page](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers)<br>- [Supprimer explicitement des marquages de contenu externes dans vos dispositions PowerPoint personnalisées](#extend-external-marking-removal-to-custom-layouts)<br>- [Supprimer toutes les formes d’un nom de forme spécifique de vos en-têtes et pieds de page, au lieu de supprimer des formes par du texte à l’intérieur de la forme](#remove-all-shapes-of-a-specific-shape-name)  |
|**Paramètres de l’Explorateur de fichiers**     | - [Toujours afficher les autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) <br>  - [Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer)      |
|**Paramètres d’amélioration des performances**     | - [Limiter la consommation de l’UC](#limit-cpu-consumption) <br>- [Limiter le nombre de threads utilisés par le scanneur](#limit-the-number-of-threads-used-by-the-scanner) <br>- [Empêcher les problèmes de performances d’Outlook avec les e-mails S/MIME](#prevent-outlook-performance-issues-with-smime-emails)        |
|**Paramètres pour les intégrations à d’autres solutions d’étiquetage**     | - [Migrer des étiquettes à partir d’îlots sécurisés et d’autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions) <br> - [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions)    |
|**Paramètres d’analyse AIP**     |   - [Désactiver l’envoi de données d’audit à Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) <br>- [Envoyer les correspondances de type d’informations à Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)      |
|**Paramètres généraux**     | - [Ajouter « signaler un problème » pour les utilisateurs](#add-report-an-issue-for-users) <br>- [Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée](#apply-a-custom-property-when-a-label-is-applied) <br>-  [Modifier le niveau de journalisation locale](#change-the-local-logging-level) <br>- [Changer les types de fichiers à protéger](#change-which-file-types-to-protect)<br>- [Configurer des délais d’attente SharePoint](#configure-sharepoint-timeouts)<br>- [Personnaliser les textes d’invite de justification pour les étiquettes modifiées](#customize-justification-prompt-texts-for-modified-labels)<br>-  [Afficher la barre de Information Protection dans les applications Office](#display-the-information-protection-bar-in-office-apps) <br>- [Activer la suppression de la protection des fichiers compressés](#enable-removal-of-protection-from-compressed-files) <br>-  [Conserver les propriétaires NTFS lors de l’étiquetage (version préliminaire publique)](#preserve-ntfs-owners-during-labeling-public-preview) <br> -  [Supprimer « pas maintenant » pour les documents lorsque vous utilisez l’étiquetage obligatoire](#remove-not-now-for-documents-when-you-use-mandatory-labeling) <br>-  [Ignorer ou ignorer les fichiers lors des analyses en fonction des attributs de fichier](#skip-or-ignore-files-during-scans-depending-on-file-attributes) <br>-  [Spécifier une couleur pour l’étiquette](#specify-a-color-for-the-label)<br>-  [Spécifier une sous-étiquette par défaut pour une étiquette parent](#specify-a-default-sublabel-for-a-parent-label)<br>-  [Prise en charge de la modification \<EXT> . PFILE à P\<EXT>](#additionalpprefixextensions)  <br>-  [Prise en charge des ordinateurs déconnectés](#support-for-disconnected-computers)     <br>-  [Activer la classification pour qu’elle s’exécute en continu en arrière-plan](#turn-on-classification-to-run-continuously-in-the-background) <br>- [Désactiver les fonctionnalités de suivi des documents (préversion publique)](#turn-off-document-tracking-features-public-preview)   |
|     |         |


### <a name="label-policy-advanced-setting-reference"></a>Référence des paramètres avancés de la stratégie d’étiquette

Utilisez le paramètre *AdvancedSettings* avec [New-LabelPolicy](/powershell/module/exchange/policy-and-compliance/new-labelpolicy) et [Set-LabelPolicy](/powershell/module/exchange/policy-and-compliance/set-labelpolicy) pour définir les paramètres suivants :

|Paramètre|Scénario et instructions|
|----------------|---------------|
|**AdditionalPPrefixExtensions**|[Prise en charge de la modification \<EXT> . PFILE à P à \<EXT> l’aide de cette propriété avancée](#additionalpprefixextensions)
|**AttachmentAction**|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|**AttachmentActionTip**|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|**DisableMandatoryInOutlook**|[Exempter les messages Outlook de l’étiquetage obligatoire](#exempt-outlook-messages-from-mandatory-labeling)
|**EnableAudit**|[Désactiver l’envoi de données d’audit à Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|**EnableContainerSupport**|[Activer la suppression de la protection des fichiers PST, rar, 7zip et MSG](#enable-removal-of-protection-from-compressed-files)
|**EnableCustomPermissions**|[Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer)|
|**EnableCustomPermissionsForCustomProtectedFiles**|[Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées aux utilisateurs dans l’Explorateur de fichiers](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|**EnableLabelByMailHeader**|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|**EnableLabelBySharePointProperties**|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
| **EnableOutlookDistributionListExpansion** | [Développer les listes de distribution Outlook lors de la recherche de destinataires de courrier électronique](#expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview) |
| **EnableTrackAndRevoke** | [Désactiver les fonctionnalités de suivi des documents (préversion publique)](#turn-off-document-tracking-features-public-preview) |
|**HideBarByDefault**|[Afficher la barre Information Protection dans les applications Office](#display-the-information-protection-bar-in-office-apps)|
|**JustificationTextForUserText** | [Personnaliser les textes d’invite de justification pour les étiquettes modifiées](#customize-justification-prompt-texts-for-modified-labels) |
|**LogMatchedContent**|[Envoyer les correspondances de type d’informations à Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)|
|**OutlookBlockTrustedDomains**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookBlockUntrustedCollaborationLabel**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookCollaborationRule**| [Personnaliser les messages de la fenêtre contextuelle Outlook](#customize-outlook-popup-messages)|
|**OutlookDefaultLabel**|[Définir une autre étiquette par défaut pour Outlook](#set-a-different-default-label-for-outlook)|
|**OutlookGetEmailAddressesTimeOutMSProperty** | [Modifier le délai d’attente pour le développement d’une liste de distribution dans Outlook lors de l’implémentation de messages de blocage pour les destinataires dans les listes de distribution](#expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview) |
|**OutlookJustifyTrustedDomains**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookJustifyUntrustedCollaborationLabel**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookRecommendationEnabled**|[Activer la classification recommandée dans Outlook](#enable-recommended-classification-in-outlook)|
|**OutlookOverrideUnlabeledCollaborationExtensions**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookSkipSmimeOnReadingPaneEnabled** | [Empêcher les problèmes de performances d’Outlook avec les e-mails S/MIME](#prevent-outlook-performance-issues-with-smime-emails)|
|**OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookWarnTrustedDomains**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**OutlookWarnUntrustedCollaborationLabel**|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|**PFileSupportedExtensions**|[Changer les types de fichiers à protéger](#change-which-file-types-to-protect)|
|**PostponeMandatoryBeforeSave**|[Supprimer « Pas maintenant » pour les documents quand vous utilisez l’étiquetage obligatoire](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
| **PowerPointRemoveAllShapesByShapeName**|[Supprimer toutes les formes d’un nom de forme spécifique de vos en-têtes et pieds de page, au lieu de supprimer des formes par du texte à l’intérieur de la forme](#remove-all-shapes-of-a-specific-shape-name) |
|**PowerPointShapeNameToRemove** |[Évitez de supprimer des formes de PowerPoint qui contiennent du texte spécifié, et qui ne sont pas des en-têtes et des pieds de page](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers) |
|**RemoveExternalContentMarkingInApp**|[Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions)|
|**RemoveExternalMarkingFromCustomLayouts**|[Supprimer explicitement des marquages de contenu externes dans vos dispositions PowerPoint personnalisées](#extend-external-marking-removal-to-custom-layouts) |
|**ReportAnIssueLink**|[Ajouter « Signaler un problème » pour les utilisateurs](#add-report-an-issue-for-users)|
|**RunPolicyInBackground**|[Activer la classification pour qu’elle s’exécute en continu en arrière-plan](#turn-on-classification-to-run-continuously-in-the-background)
|**ScannerMaxCPU** | [Limiter la consommation de l’UC](#limit-cpu-consumption) |
|**ScannerMinCPU** | [Limiter la consommation de l’UC](#limit-cpu-consumption) |
|**ScannerConcurrencyLevel**|[Limiter le nombre de threads utilisés par le scanneur](#limit-the-number-of-threads-used-by-the-scanner)|
|**ScannerFSAttributesToSkip** | [Ignorer ou ignorer les fichiers lors des analyses en fonction des attributs de fichier](#skip-or-ignore-files-during-scans-depending-on-file-attributes)
|**SharepointWebRequestTimeout**| [Configurer des délais d’attente SharePoint](#configure-sharepoint-timeouts)|
|**SharepointFileWebRequestTimeout** |[Configurer des délais d’attente SharePoint](#configure-sharepoint-timeouts)|
|**UseCopyAndPreserveNTFSOwner** | [Conserver les propriétaires NTFS pendant l’étiquetage](#preserve-ntfs-owners-during-labeling-public-preview)
| | |

#### <a name="check-label-policy-settings"></a>Vérifier les paramètres de stratégie d’étiquette
Exemple de commande PowerShell pour vérifier les paramètres de stratégie d’étiquette en vigueur pour une stratégie d’étiquette nommée « global » :

```PowerShell
(Get-LabelPolicy -Identity Global).settings
```

### <a name="label-advanced-setting-reference"></a>Référence des paramètres avancés des étiquettes

Utilisez le paramètre *AdvancedSettings* avec [New-label](/powershell/module/exchange/policy-and-compliance/new-label) et [Set-label](/powershell/module/exchange/policy-and-compliance/set-label).

|Paramètre|Scénario et instructions|
|----------------|---------------|
|**color**|[Spécifier une couleur pour l’étiquette](#specify-a-color-for-the-label)|
|**customPropertiesByLabel**|[Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée](#apply-a-custom-property-when-a-label-is-applied)|
|**DefaultSubLabelId**|[Spécifier une sous-étiquette par défaut pour une étiquette parent](#specify-a-default-sublabel-for-a-parent-label) 
|**labelByCustomProperties**|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|**SMimeEncrypt**|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|**SMimeSign**|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|

#### <a name="check-label-settings"></a>Vérifier les paramètres des étiquettes

Exemple de commande PowerShell pour vérifier les paramètres de votre étiquette en vigueur pour une étiquette nommée « public » :

```PowerShell
(Get-Label -Identity Public).settings
```

## <a name="display-the-information-protection-bar-in-office-apps"></a>Afficher la barre Information Protection dans les applications Office

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, les utilisateurs doivent sélectionner l’option **afficher la barre** à partir du bouton **sensibilité** pour afficher la barre de information protection dans les applications Office. Utilisez la clé **HideBarByDefault** et définissez la valeur sur **false** pour afficher automatiquement cette barre pour les utilisateurs afin qu’ils puissent sélectionner des étiquettes à partir de la barre ou du bouton. 

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **HideBarByDefault**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}
```

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Exempter les messages Outlook de l’étiquetage obligatoire

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, lorsque vous activez le paramètre de stratégie étiquette **tous les documents et e-mails doivent avoir une étiquette**, tous les documents enregistrés et les e-mails envoyés doivent avoir une étiquette appliquée. Quand vous configurez le paramètre avancé suivant, le paramètre de stratégie s’applique uniquement aux documents Office et non aux messages Outlook.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **DisableMandatoryInOutlook**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}
```

## <a name="enable-recommended-classification-in-outlook"></a>Activer la classification recommandée dans Outlook

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous configurez une étiquette pour la classification recommandée, les utilisateurs sont invités à accepter ou ignorer l’étiquette recommandée dans Word, Excel et PowerPoint. Ce paramètre affiche également cette recommandation d’étiquette dans Outlook.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookRecommendationEnabled**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}
```

## <a name="enable-removal-of-protection-from-compressed-files"></a>Activer la suppression de la protection des fichiers compressés

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous configurez ce paramètre, l’applet de commande  [PowerShell](./clientv2-admin-guide-powershell.md) **Set-AIPFileLabel** est activée pour permettre la suppression de la protection des fichiers PST, rar, 7zip et MSG.

- Clé : **EnableContainerSupport**

- Valeur : **true**

Exemple de commande PowerShell dans laquelle votre stratégie est activée :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableContainerSupport="True"}
```

## <a name="set-a-different-default-label-for-outlook"></a>Définir une autre étiquette par défaut pour Outlook

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous configurez ce paramètre, Outlook n’applique pas l’étiquette par défaut qui est configurée en tant que paramètre de stratégie pour l’option **appliquer cette étiquette par défaut aux documents et aux e-mails**. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookDefaultLabel**

- Valeur : \<**label GUID**> ou **aucun**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}
```

## <a name="change-which-file-types-to-protect"></a>Changer les types de fichiers à protéger

Ces configurations utilisent un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, le Azure Information Protection client d’étiquetage unifié protège tous les types de fichiers, et le scanneur du client protège uniquement les types de fichiers Office et les fichiers PDF.

Vous pouvez modifier ce comportement par défaut pour une stratégie d’étiquette sélectionnée, en spécifiant l’un des éléments suivants :

### <a name="pfilesupportedextension"></a>PFileSupportedExtension

- Clé : **PFileSupportedExtensions**

- Ajoutée **\<string value>** 

Utilisez le tableau suivant pour identifier la valeur de chaîne à spécifier :

| Valeur de chaîne| Client| Scanneur|
|-------------|-------|--------|
|\*|Valeur par défaut : appliquer la protection à tous les types de fichiers|Appliquer la protection à tous les types de fichiers|
|ConvertTo-JSON (". jpg", ". png")|En plus des fichiers PDF et des types de fichiers Office, appliquer la protection aux extensions de nom de fichier spécifiées | En plus des fichiers PDF et des types de fichiers Office, appliquer la protection aux extensions de nom de fichier spécifiées
| | | |

**Exemple 1 :**  Commande PowerShell pour que le scanneur protège tous les types de fichiers, où votre stratégie d’étiquette est nommée « scanner » :

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**Exemple 2 :** Commande PowerShell pour le scanneur afin de protéger les fichiers. txt et. csv en plus des fichiers Office et des fichiers PDF, où votre stratégie d’étiquette est nommée « scanner » :

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}
```

Ce paramètre vous permet de modifier les types de fichiers protégés, mais vous ne pouvez pas modifier le niveau de protection par défaut de natif à générique. Par exemple, pour les utilisateurs qui exécutent le client d’étiquetage unifié, vous pouvez modifier le paramètre par défaut afin que seuls les fichiers Office et PDF soient protégés au lieu de tous les types de fichiers. Toutefois, vous ne pouvez pas modifier ces types de fichiers pour qu’ils soient protégés de manière générique avec l’extension de nom de fichier. pfile.

### <a name="additionalpprefixextensions"></a>AdditionalPPrefixExtensions

Le client d’étiquetage unifié prend en charge la modification \<EXT> . PFILE à P à \<EXT> l’aide de la propriété Advanced, **AdditionalPPrefixExtensions**. Cette propriété avancée est prise en charge à partir de l’Explorateur de fichiers, de PowerShell et du scanneur. Toutes les applications ont un comportement similaire.   

- Clé : **AdditionalPPrefixExtensions**

- Ajoutée **\<string value>** 

Utilisez le tableau suivant pour identifier la valeur de chaîne à spécifier :

| Valeur de chaîne| Client et scanneur|
|-------------|---------------|
|\*|Toutes les extensions PFile deviennent P\<EXT>|
|\<null value>| La valeur par défaut se comporte comme la valeur de protection par défaut.|
|ConvertTo-JSON (". DWG", ". zip")|En plus de la liste précédente, « . dwg » et « . zip » deviennent P\<EXT>| 

Avec ce paramètre, les extensions suivantes deviennent toujours **P \<EXT> :** ». txt ",". xml ",". bmp ",". JT ",". jpg ",". jpeg ",". jpe ",". jif ",". JFIF ",". JFI ",". png ",". TIF ",". TIFF ",". gif "). L’exclusion notable est que « PTXT » ne devient pas « txt. pfile ». 

**AdditionalPPrefixExtensions** fonctionne uniquement si la protection de fichiers pfile avec la propriété Advanced- [**PFileSupportedExtension**](#pfilesupportedextension) est activée. 

**Exemple 1 :** Commande PowerShell qui se comporte comme le comportement par défaut où Protect ". DWG" devient ". dwg. pfile" :

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =""}
```

**Exemple 2 :**  Commande PowerShell pour remplacer toutes les extensions PFile de la protection générique (DWG. PFile) par la protection native (. PDWG) lorsque les fichiers sont protégés :

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions ="*"}
```

**Exemple 3 :** Commande PowerShell pour modifier « . dwg » en « . PDWG » lors de l’utilisation de ce service, protéger ce fichier :

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =ConvertTo-Json(".dwg")}
```



## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Supprimer « Pas maintenant » pour les documents quand vous utilisez l’étiquetage obligatoire

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous utilisez le paramètre de stratégie étiquette de **tous les documents et e-mails doit avoir une étiquette**, les utilisateurs sont invités à sélectionner une étiquette lorsqu’ils enregistrent un document Office pour la première fois et lorsqu’ils envoient un message électronique à partir d’Outlook.

Pour les documents, les utilisateurs peuvent sélectionner **Pas maintenant** pour ignorer temporairement l’invite à sélectionner une étiquette et revenir au document. En revanche, ils ne peuvent pas fermer le document enregistré sans l’étiqueter. 

Quand vous configurez le paramètre **PostponeMandatoryBeforeSave** , l’option **Not Now** est supprimée, de sorte que les utilisateurs doivent sélectionner une étiquette lorsque le document est enregistré pour la première fois.

> [!TIP]
> Le paramètre **PostponeMandatoryBeforeSave** garantit également que les documents partagés sont étiquetés avant d’être envoyés par courrier électronique. 
>
>Par défaut, même si **tous les documents et e-mails doivent avoir une étiquette** activée dans votre stratégie, les utilisateurs sont promus uniquement vers des fichiers d’étiquette associés à des courriers électroniques à partir d’Outlook.  
> 
Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **PostponeMandatoryBeforeSave**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}
```

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage

Cette configuration utilise des [Paramètres avancés](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Il existe deux méthodes pour supprimer des classifications d’autres solutions d’étiquetage :

|Paramètre  |Description  |
|---------|---------|
|**WordShapeNameToRemove**     |  Supprime toute forme des documents Word où le nom de la forme correspond au nom défini dans la propriété avancée **WordShapeNameToRemove** .  <br><br>Pour plus d’informations, consultez [utiliser la propriété avancée WordShapeNameToRemove](#use-the-wordshapenametoremove-advanced-property).     |
|**RemoveExternalContentMarkingInApp** <br><br>**ExternalContentMarkingToRemove**   |    Vous permet de supprimer ou de remplacer des en-têtes ou des pieds de page textuels dans des documents Word, Excel et PowerPoint. <br><br>Pour plus d'informations, consultez les pages suivantes : <br>- [Utiliser la propriété avancée RemoveExternalContentMarkingInApp](#use-the-removeexternalcontentmarkinginapp-advanced-property)<br>- [Comment configurer ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove).    |
|     |         |

### <a name="use-the-wordshapenametoremove-advanced-property"></a>Utiliser la propriété avancée WordShapeNameToRemove

*La propriété avancée **WordShapeNameToRemove** est prise en charge à partir de la version 2.6.101.0 et supérieure*

Ce paramètre vous permet de supprimer ou de remplacer des étiquettes basées sur des formes de documents Word lorsque ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, la forme contient le nom d’une ancienne étiquette que vous avez maintenant migrée vers des étiquettes de sensibilité pour utiliser un nouveau nom d’étiquette et sa propre forme.

Pour utiliser cette propriété avancée, vous devez rechercher le nom de la forme dans le document Word, puis les définir dans la liste de propriétés avancées **WordShapeNameToRemove** des formes. Le service supprime toutes les formes dans Word qui commencent par un nom défini dans la liste des formes de cette propriété avancée.

Évitez de supprimer les formes qui contiennent le texte que vous souhaitez ignorer, en définissant le nom de toutes les formes à supprimer et évitez de vérifier le texte dans toutes les formes, ce qui est un processus gourmand en ressources.

> [!NOTE]
> Si vous ne spécifiez pas de formes de mot dans ce paramètre de propriété avancé supplémentaire et que Word est inclus dans la valeur de clé **RemoveExternalContentMarkingInApp** , le texte que vous spécifiez dans la valeur [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) est recherché dans toutes les formes. 
>

**Pour rechercher le nom de la forme que vous utilisez et souhaitez exclure :**

1. Dans Word, affichez le volet de **sélection** : onglet dossier de **démarrage** > groupe **édition** > **Sélectionnez** l’option > **volet sélection**.

2. Sélectionnez la forme sur la page que vous souhaitez marquer pour suppression. Le nom de la forme que vous marquez est maintenant mis en surbrillance dans le volet de **sélection** .

Utilisez le nom de la forme pour spécifier une valeur de chaîne pour la clé * * * * WordShapeNameToRemove * * * *. 

Exemple : le nom de la forme est **DC**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `dc`.

- Clé : **WordShapeNameToRemove**

- Valeur: \<**Word shape name**> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}
```

Lorsque vous avez plusieurs formes de mot à supprimer, spécifiez autant de valeurs que vous avez de formes à supprimer.

### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>Utiliser la propriété avancée RemoveExternalContentMarkingInApp

Ce paramètre vous permet de supprimer ou de remplacer des en-têtes ou des pieds de page textuels dans des documents lorsque ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, l’ancien pied de page contient le nom d’une ancienne étiquette que vous avez maintenant migrée vers des étiquettes de sensibilité pour utiliser un nouveau nom d’étiquette et son propre pied de page.

Lorsque le client d’étiquetage unifié obtient cette configuration dans sa stratégie, les anciens en-têtes et pieds de page sont supprimés ou remplacés lorsque le document est ouvert dans l’application Office et toute étiquette de sensibilité est appliquée au document.

Cette configuration n’est pas prise en charge pour Outlook. Sachez également que quand vous l’utilisez avec Word, Excel et PowerPoint, elle peut affecter négativement les performances de ces applications pour les utilisateurs. La configuration vous permet de définir des paramètres par application, par exemple, rechercher du texte dans les en-têtes et les pieds de page des documents Word, mais pas dans les feuilles de calcul Excel ni dans les présentations PowerPoint.

Étant donné que les critères spéciaux affectent les performances pour les utilisateurs, nous vous recommandons de limiter les types d’applications Office (**W** ORD, E **X** cel, **P** owerPoint) à ceux qui doivent être recherchés.
Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **RemoveExternalContentMarkingInApp**

- Valeur: \<**Office application types WXP**> 

Exemples :

- Pour rechercher dans des documents Word uniquement, spécifiez **W**.

- Pour rechercher dans des documents Word et des présentations PowerPoint, spécifiez **WP**.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}
```

Ensuite, vous avez besoin d’au moins un paramètre client avancé de plus, [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove), pour spécifier le contenu de l’en-tête ou du pied de page et comment les supprimer ou les remplacer.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Comment configurer ExternalContentMarkingToRemove

Lorsque vous spécifiez la valeur de chaîne pour la clé **ExternalContentMarkingToRemove** , vous disposez de trois options qui utilisent des expressions régulières. Pour chacun de ces scénarios, utilisez la syntaxe indiquée dans la colonne **exemple de valeur** dans le tableau suivant :

|Option  |Description de l’exemple |Valeur d'exemple|
|---------|---------|---------|
|**Correspondance partielle pour supprimer tous les éléments dans l’en-tête ou le pied de page**     | Vos en-têtes ou pieds de page contiennent le **texte de chaîne à supprimer** et vous souhaitez supprimer complètement ces en-têtes ou pieds de page.   |`*TEXT*`  | 
|**Terminer la correspondance pour supprimer uniquement des mots spécifiques dans l’en-tête ou le pied de page**     |    Vos en-têtes ou pieds de page contiennent le **texte de chaîne à supprimer**, et vous souhaitez supprimer le **texte** Word uniquement, en laissant la chaîne d’en-tête ou de pied de page comme **à supprimer**.      |`TEXT ` |
|**Terminer la correspondance pour supprimer tous les éléments de l’en-tête ou du pied de page**     |Vos en-têtes ou pieds de page ont le **texte de chaîne à supprimer**. Vous voulez supprimer les en-têtes ou les pieds de page qui ont exactement cette chaîne.         |`^TEXT TO REMOVE$`|
|     |         | |


Les caractères génériques de la chaîne que vous spécifiez sont sensibles à la casse. La longueur de chaîne maximale est de 255 caractères et ne peut pas contenir d’espaces blancs. 

Étant donné que des documents peuvent contenir des caractères invisibles ou différents types d’espaces ou des tabulations, la chaîne que vous spécifiez pour une expression ou une phrase peut ne pas être détectée. Si possible, spécifiez un seul mot distinctif pour la valeur et veillez à tester les résultats avant de procéder au déploiement en production.

Pour la même stratégie d’étiquette, spécifiez les chaînes suivantes :

- Clé : **ExternalContentMarkingToRemove**

- Valeur: \<**string to match, defined as regular expression**> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}
```

Pour plus d'informations, consultez les pages suivantes :

- [En-têtes ou pieds de page multilignes](#multiline-headers-or-footers)
- [Optimisation pour PowerPoint](#optimization-for-powerpoint)

#### <a name="multiline-headers-or-footers"></a>En-têtes ou pieds de page multilignes

Si un texte d’en-tête ou de pied de page prend plus d’une ligne, créez une clé et une valeur pour chaque ligne. Par exemple, si vous avez le pied de page suivant avec deux lignes :

**Le fichier est classé confidentiel**

**Étiquette appliquée manuellement**

Pour supprimer ce pied de page multiligne, vous créez les deux entrées suivantes pour la même stratégie d’étiquette :

- Clé : **ExternalContentMarkingToRemove**

- Valeur de clé 1 : **\* confidentiel***

- Valeur de clé 2 : **\* étiquette appliquée*** 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}
```

#### <a name="optimization-for-powerpoint"></a>Optimisation pour PowerPoint

Les en-têtes et les pieds de page dans PowerPoint sont implémentés en tant que formes. Pour les types de formes **msoTextBox**, **msoTextEffect**, **msoPlaceholder** et **msoAutoShape** , les paramètres avancés suivants fournissent des optimisations supplémentaires :

- [PowerPointShapeNameToRemove](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers)
- [RemoveExternalMarkingFromCustomLayouts](#extend-external-marking-removal-to-custom-layouts)

En outre, le [PowerPointRemoveAllShapesByShapeName](#remove-all-shapes-of-a-specific-shape-name) peut supprimer n’importe quel type de forme, en fonction du nom de la forme.

Pour plus d’informations, consultez [Rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page](#find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer).

##### <a name="avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers"></a>Évitez de supprimer des formes de PowerPoint qui contiennent du texte spécifié, et qui ne sont pas des en-têtes et des pieds de page

Pour éviter de supprimer des formes qui contiennent le texte que vous avez spécifié, mais qui ne sont pas des en-têtes ou des pieds de page, utilisez un paramètre client avancé supplémentaire nommé **PowerPointShapeNameToRemove**. 

Nous recommandons également d’utiliser ce paramètre pour éviter de vérifier le texte dans toutes les formes, qui est un processus gourmand en ressources. 

- Si vous ne spécifiez pas ce paramètre client avancé supplémentaire et si PowerPoint est inclus dans la valeur de la clé [RemoveExternalContentMarkingInApp](#remove-headers-and-footers-from-other-labeling-solutions), toutes les formes sont vérifiées à la recherche du texte que vous spécifiez dans la valeur [ ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove). 

- Si cette valeur est spécifiée, seules les formes qui remplissent les critères de nom de forme et ont également un texte qui correspond à la chaîne fournie avec [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) sera supprimée.

Par exemple :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

##### <a name="extend-external-marking-removal-to-custom-layouts"></a>Étendre la suppression du marquage externe aux dispositions personnalisées

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, la logique utilisée pour supprimer des marquages de contenu externes ignore les dispositions personnalisées configurées dans PowerPoint. Pour étendre cette logique aux dispositions personnalisées, affectez la valeur **true** à la propriété avancée **RemoveExternalMarkingFromCustomLayouts** .

- Clé : **RemoveExternalMarkingFromCustomLayouts**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalMarkingFromCustomLayouts="True"}
```

##### <a name="remove-all-shapes-of-a-specific-shape-name"></a>Supprimer toutes les formes d’un nom de forme spécifique

Si vous utilisez des dispositions personnalisées PowerPoint et souhaitez supprimer toutes les formes d’un nom de forme spécifique de vos en-têtes et pieds de page, utilisez le paramètre avancé **PowerPointRemoveAllShapesByShapeName** , avec le nom de la forme que vous souhaitez supprimer.

L’utilisation du paramètre **PowerPointRemoveAllShapesByShapeName** ignore le texte à l’intérieur de vos formes et utilise à la place le nom de la forme pour identifier les formes que vous souhaitez supprimer.

Par exemple :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointRemoveAllShapesByShapeName="Arrow: Right"}
```

> [!NOTE]
> Pour définir le paramètre **PowerPointRemoveAllShapesByShapeName** , vous devez actuellement définir le paramètre [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) , même si vous n’avez pas besoin de la fonctionnalité fournie par **ExternalContentMarkingToRemove**.
>
> Si vous souhaitez définir **PowerPointRemoveAllShapesByShapeName**, nous vous recommandons de définir [ExternalContentMarkingToRemove](#how-to-configure-externalcontentmarkingtoremove) et [PowerPointShapeNameToRemove](#avoid-removing-shapes-from-powerpoint-that-contain-specified-text-and-are-not-headers--footers) afin d’éviter de supprimer plus de formes que prévu.
>

Pour plus d'informations, consultez les pages suivantes :

- [Rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page](#find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer)
- [Supprimer le marquage de contenu externe des dispositions personnalisées dans PowerPoint](#remove-external-content-marking-from-custom-layouts-in-powerpoint)

##### <a name="find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer"></a>Rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page

1. Dans PowerPoint, affichez le volet **Sélection** : onglet **Mise en forme** > groupe **Organiser** > **volet sélection**.

2. Sélectionnez la forme sur la diapositive qui contient votre en-tête ou votre pied de page. Le nom de la forme sélectionnée est maintenant en surbrillance dans le volet **Sélection**.

Utilisez le nom de la forme afin de spécifier une valeur de chaîne pour la clé **PowerPointShapeNameToRemove**. 

**Exemple**: le nom de la forme est **FC**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `fc`.

- Clé : **PowerPointShapeNameToRemove**

- Valeur: \<**PowerPoint shape name**> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

Lorsque vous avez plusieurs formes PowerPoint à supprimer, spécifiez autant de valeurs que vous le souhaitez pour les formes à supprimer.

Par défaut, seuls les en-têtes et les pieds de page qui se trouvent dans les diapositives principales sont recherchés. Pour étendre cette recherche à toutes les diapositives, processus beaucoup plus gourmand en ressources, utilisez un paramètre client avancé supplémentaire nommé **RemoveExternalContentMarkingInAllSlides**:

- Clé : **RemoveExternalContentMarkingInAllSlides**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}
```

##### <a name="remove-external-content-marking-from-custom-layouts-in-powerpoint"></a>Supprimer le marquage de contenu externe des dispositions personnalisées dans PowerPoint

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, la logique utilisée pour supprimer des marquages de contenu externes ignore les dispositions personnalisées configurées dans PowerPoint. Pour étendre cette logique aux dispositions personnalisées, affectez la valeur **true** à la propriété avancée **RemoveExternalMarkingFromCustomLayouts** .

- Clé : **RemoveExternalMarkingFromCustomLayouts**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalMarkingFromCustomLayouts="True"}
```

## <a name="disable-custom-permissions-in-file-explorer"></a>Désactiver les autorisations personnalisées dans l’Explorateur de fichiers

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, les utilisateurs voient une option nommée **protéger avec des autorisations personnalisées** lorsqu’ils cliquent avec le bouton droit dans l’Explorateur de fichiers et choisissent **classer et protéger**. Cette option permet de définir leurs propres paramètres de protection qui peuvent remplacer tous les paramètres de protection que vous pouvez avoir inclus dans une configuration d’étiquette. Les utilisateurs peuvent voir également une option pour supprimer la protection. Quand vous configurez ce paramètre, les utilisateurs ne voient pas ces options.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableCustomPermissions**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées aux utilisateurs dans l’Explorateur de fichiers

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous configurez le paramètre client avancé pour [Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer), par défaut, les utilisateurs ne sont pas en mesure d’afficher ou de modifier les autorisations personnalisées qui sont déjà définies dans un document protégé.

Toutefois, il existe un autre paramètre de client avancé que vous pouvez spécifier afin que dans ce scénario, les utilisateurs puissent afficher et modifier des autorisations personnalisées pour un document protégé lorsqu’ils utilisent l’Explorateur de fichiers et cliquer avec le bouton droit sur le fichier.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableCustomPermissionsForCustomProtectedFiles**

- Valeur : **true**

Exemple de commande PowerShell :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}
```

## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes

Cette configuration utilise des [Paramètres avancés](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Ce paramètre est destiné aux utilisateurs qui joignent des documents étiquetés à un courrier électronique et n’étiquettent pas le message électronique lui-même. Dans ce scénario, une étiquette est automatiquement sélectionnée pour eux, en fonction des étiquettes de classification appliquées aux pièces jointes. L’étiquette classification la plus élevée est sélectionnée.

La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur Microsoft SharePoint ou OneDrive).

Vous pouvez configurer ce paramètre sur **recommandé**, afin que les utilisateurs soient invités à appliquer l’étiquette sélectionnée à leur message électronique, avec une info-bulle personnalisable. Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Ou bien, vous pouvez configurer ce paramètre sur **automatique**, où l’étiquette sélectionnée est automatiquement appliquée, mais les utilisateurs peuvent supprimer l’étiquette ou sélectionner une autre étiquette avant d’envoyer l’e-mail.

> [!NOTE]
> Lorsque la pièce jointe avec l’étiquette de classification la plus élevée est configurée pour la protection avec le paramètre des autorisations définies par l’utilisateur :
> 
> - Lorsque les autorisations définies par l’utilisateur de l’étiquette sont Outlook (ne pas transférer), cette étiquette est sélectionnée et le fait de ne pas transférer la protection est appliqué à l’e-mail.
> - Lorsque les autorisations définies par l’utilisateur de l’étiquette sont uniquement pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette n’est pas appliquée au message électronique et aucune n’est la protection.
> 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé 1 : **AttachmentAction**

- Valeur de clé 1 : **recommandé** ou **automatique**

- Clé 2 : **AttachmentActionTip**

- Valeur de clé 2 : « \<customized tooltip> »

L’info-bulle personnalisée ne prend en charge qu’une seule langue.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}
```

## <a name="add-report-an-issue-for-users"></a>Ajouter « Signaler un problème » pour les utilisateurs

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous spécifiez le paramètre client avancé suivant, les utilisateurs voient une option **Signaler un problème** qu’ils peuvent sélectionner dans la boîte de dialogue **Aide et commentaires** du client. Spécifiez une chaîne HTTP pour le lien. (par exemple, une page web personnalisée permettant aux utilisateurs de signaler des problèmes, ou une adresse e-mail qui pointe vers votre support technique). 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **ReportAnIssueLink**

- Ajoutée **\<HTTP string>**

Exemple de valeur pour un site web : `https://support.contoso.com`

Exemple de valeur pour une adresse e-mail : `mailto:helpdesk@contoso.com`

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}
```

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails

Cette configuration utilise des [Paramètres avancés](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Quand vous créez et que vous configurez les paramètres client avancés suivants, les utilisateurs voient des messages contextuels dans Outlook qui peuvent les avertir avant d’envoyer un e-mail, leur demander de justifier la raison pour laquelle ils envoient un e-mail ou les empêcher d’envoyer un e-mail pour un des scénarios suivants :

- **Leur e-mail ou la pièce jointe à leur e-mail a une étiquette spécifique** :
    - La pièce jointe peut être n’importe quel type de fichier

- **Leur e-mail ou leur pièce jointe à l’e-mail n’a pas d’étiquette** :
    - La pièce jointe peut être un document Office ou un document PDF

Lorsque ces conditions sont remplies, l’utilisateur voit un message contextuel avec l’une des actions suivantes :

|Type  |Description  |
|---------|---------|
|**Viendra**     | L’utilisateur peut confirmer et envoyer, ou bien annuler.        |
|**Prouver**     |  L’utilisateur est invité à confirmer la justification (options prédéfinies ou formulaire libre) et l’utilisateur peut alors envoyer ou annuler l’e-mail. <br>Le texte de la justification est écrit dans l’en-tête x de l’e-mail, afin qu’il puisse être lu par d’autres systèmes, tels que les services de protection contre la perte de données (DLP).       |
|**Bloquer**     |    L’utilisateur ne peut pas envoyer l’e-mail tant que la condition perdure. <br>Le message contient la raison du blocage de l’e-mail pour que l’utilisateur puisse résoudre le problème, <br>par exemple supprimer des destinataires spécifiques ou appliquer une étiquette à l’e-mail.     |
|     |         | 

Quand les messages contextuels concernent une étiquette spécifique, vous pouvez configurer des exceptions pour les destinataires par nom de domaine.

Pour obtenir un exemple de procédure pas à pas de configuration de ces paramètres, consultez la vidéo [Azure information protection configuration contextuelle Outlook](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) .

> [!TIP]
> Pour garantir l’affichage des fenêtres contextuelles, même lorsque les documents sont partagés à partir d’Outlook **(partage de > de fichiers > joindre une copie)**, configurez également le paramètre avancé [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) .

Pour plus d'informations, consultez les pages suivantes :

- [Pour implémenter les messages contextuels avertir, justifier ou bloquer pour des étiquettes spécifiques](#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels)
- [Pour implémenter les messages contextuels d’avertissement, de justification ou de blocage pour les e-mails ou les pièces jointes qui n’ont pas d’étiquette](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label)

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Pour implémenter les messages contextuels avertir, justifier ou bloquer pour des étiquettes spécifiques

Pour la stratégie sélectionnée, créez un ou plusieurs des paramètres avancés suivants avec les clés suivantes. Pour les valeurs, spécifiez une ou plusieurs étiquettes par leur GUID, chacune séparée par une virgule.

Exemple de valeur pour plusieurs GUID d’étiquette sous la forme d’une chaîne séparée par des virgules : 

```sh
dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f
```

|type de message  |Clé/valeur  |
|---------|---------|
|**Viendra**     |  Clé : **OutlookWarnUntrustedCollaborationLabel** <br><br>Valeur: \<**label GUIDs, comma-separated**>       |
|**Prouver**     |  Clé : **OutlookJustifyUntrustedCollaborationLabel** <br><br>Valeur: \<**label GUIDs, comma-separated**>       |
|**Bloquer**     | Clé : **OutlookBlockUntrustedCollaborationLabel** <br><br>Valeur: \<**label GUIDs, comma-separated**>       |
|     |         |



Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}
```

Pour une personnalisation plus poussée, vous pouvez également [exempter les noms de domaine pour les messages contextuels configurés pour des étiquettes spécifiques](#to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels).

> [!NOTE]
> Les paramètres avancés de cette section (**OutlookWarnUntrustedCollaborationLabel**, **OutlookJustifyUntrustedCollaborationLabel** et **OutlookBlockUntrustedCollaborationLabel**) concernent le moment où une étiquette *spécifique* est en cours d’utilisation.
> 
> Pour implémenter des messages contextuels par défaut pour le contenu *unlabled* , utilisez le paramètre avancé **[OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label)** . Pour personnaliser vos messages contextuels pour un contenu sans étiquette, utilisez un fichier **. JSON** pour définir vos paramètres avancés. 
>
>Pour plus d’informations, consultez [personnaliser les messages de la fenêtre contextuelle Outlook](#customize-outlook-popup-messages).
> 
> [!TIP]
> Pour vous assurer que vos messages de bloc s’affichent en fonction des besoins, même pour un destinataire situé dans une liste de distribution Outlook, veillez à ajouter le paramètre avancé [EnableOutlookDistributionListExpansion](#expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview) .
>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Pour exempter les noms de domaine pour les messages contextuels configurés pour des étiquettes spécifiques

Pour les étiquettes que vous avez spécifiées avec ces messages contextuels, vous pouvez exempter des noms de domaine spécifiques afin que les utilisateurs ne voient pas les messages pour les destinataires qui ont ce nom de domaine inclus dans leur adresse de messagerie. Dans ce cas, les e-mails sont envoyés sans qu’un message interrompe le processus. Pour spécifier plusieurs domaines, ajoutez-les sous la forme d’une seule chaîne, en les séparant par des virgules.

Une configuration typique consiste à afficher les messages contextuels seulement pour les destinataires qui sont externes à votre organisation ou qui ne sont pas des partenaires autorisés de votre organisation. Dans ce cas, vous spécifiez tous les domaines de messagerie utilisés par votre organisation et par vos partenaires.

Pour la même stratégie d’étiquette, créez les paramètres client avancés suivants et, pour la valeur, spécifiez un ou plusieurs domaines, chacun étant séparé par une virgule.

Exemple de valeur pour plusieurs domaines sous forme de chaîne séparée par des virgules : `contoso.com,fabrikam.com,litware.com`

|type de message  |Clé/valeur  |
|---------|---------|
|**Viendra**     |  Clé : **OutlookWarnTrustedDomains** <br><br>Ajoutée **\<**domain names, comma separated**>**     |
|**Prouver**     | Clé : **OutlookJustifyTrustedDomains** <br><br>Ajoutée **\<**domain names, comma separated**>**       |
|**Bloquer**     | Clé : **OutlookBlockTrustedDomains** <br><br>Ajoutée **\<**domain names, comma separated**>**      |
|     |         |


Par exemple, supposons que vous avez spécifié le paramètre client avancé **OutlookBlockUntrustedCollaborationLabel** pour l’étiquette **confidentiel \ tous les employés** . 

Vous spécifiez maintenant le paramètre de client avancé supplémentaire **OutlookBlockTrustedDomains** avec **contoso.com**. Par conséquent, un utilisateur peut envoyer un e-mail à `john@sales.contoso.com` lorsqu’il est étiqueté **confidentiel \ tous les employés**, mais qu’il ne pourra pas envoyer un e-mail avec la même étiquette à un compte gmail.

Exemples de commandes PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="contoso.com"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}
```

> [!NOTE]
> Pour vous assurer que vos messages de bloc s’affichent en fonction des besoins, même pour un destinataire situé dans une liste de distribution Outlook, veillez à ajouter le paramètre avancé [EnableOutlookDistributionListExpansion](#expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview) .
>

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Pour implémenter les messages contextuels d’avertissement, de justification ou de blocage pour les e-mails ou les pièces jointes qui n’ont pas d’étiquette

Pour la même stratégie d’étiquette, créez le paramètre de client avancé suivant avec l’une des valeurs suivantes :

|type de message  |Clé/valeur  |
|---------|---------|
|**Viendra**     |  Clé : **OutlookUnlabeledCollaborationAction** <br><br>Valeur : **avertir**     |
|**Prouver**     |Clé : **OutlookUnlabeledCollaborationAction**<br><br>Valeur : **justifier**       |
|**Bloquer**     | Clé : **OutlookUnlabeledCollaborationAction** <br><br>Valeur : **bloquer**      |
|  **Désactiver ces messages**   |   Clé : **OutlookUnlabeledCollaborationAction** <br><br>Valeur : **désactivé**      |
| | |


Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}
```

Pour plus de personnalisation, consultez :

- [Pour définir des extensions de nom de fichier spécifiques pour les messages contextuels avertir, justifier ou bloquer pour les pièces jointes qui n’ont pas d’étiquette](#to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label)
- [Pour spécifier une action différente pour les messages électroniques sans pièces jointes](#to-specify-a-different-action-for-email-messages-without-attachments)
- [Personnaliser les messages de la fenêtre contextuelle Outlook](#customize-outlook-popup-messages)

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Pour définir des extensions de nom de fichier spécifiques pour les messages contextuels avertir, justifier ou bloquer pour les pièces jointes qui n’ont pas d’étiquette

Par défaut, les messages contextuels avertir, justifier ou bloquer s’appliquent à tous les documents Office et documents PDF. Vous pouvez affiner cette liste en spécifiant les extensions de nom de fichier qui doivent afficher les messages d’avertissement, justifier ou bloquer avec un paramètre avancé supplémentaire et une liste séparée par des virgules des extensions de nom de fichier.

Exemple de valeur pour plusieurs extensions de nom de fichier à définir en tant que chaîne séparée par des virgules : `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

Dans cet exemple, un document PDF sans étiquette n’a pas pour effet d’avertir, de justifier ou de bloquer les messages contextuels.

Pour la même stratégie d’étiquette, entrez les chaînes suivantes : 


- Clé : **OutlookOverrideUnlabeledCollaborationExtensions**

- Ajoutée **\<**file name extensions to display messages, comma separated**>**


Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}
```

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Pour spécifier une action différente pour les messages électroniques sans pièces jointes

Par défaut, la valeur que vous spécifiez pour [OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label) pour avertir, justifier ou bloquer les messages contextuels s’applique aux e-mails ou pièces jointes qui n’ont pas d’étiquette. 

Vous pouvez affiner cette configuration en spécifiant un autre paramètre avancé pour les messages électroniques qui n’ont pas de pièces jointes.

Créez le paramètre client avancé suivant avec une des valeurs suivantes :

|type de message  |Clé/valeur  |
|---------|---------|
|**Viendra**     | Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valeur : **avertir**
     |
|**Prouver**     |Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valeur : **justifier**      |
|**Bloquer**     | Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valeur : **bloquer**     |
|  **Désactiver ces messages**   |    Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior** <br><br>Valeur : **désactivé**    |
| | |


Si vous ne spécifiez pas ce paramètre client, la valeur que vous spécifiez pour [OutlookUnlabeledCollaborationAction](#to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label) est utilisée pour les messages électroniques sans étiquette, et les messages électroniques sans étiquette avec pièces jointes.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}
```

## <a name="expand-outlook-distribution-lists-when-searching-for-email-recipients-public-preview"></a>Développer les listes de distribution Outlook lors de la recherche de destinataires de courrier électronique (version préliminaire publique)

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Pour étendre la prise en charge d’autres paramètres avancés aux destinataires dans les listes de distribution Outlook, définissez le paramètre avancé **EnableOutlookDistributionListExpansion** sur **true**.

- Clé : **EnableOutlookDistributionListExpansion**
- Valeur : **true**

Par exemple, si vous avez configuré les paramètres [OutlookBlockTrustedDomains](#to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels), [OutlookBlockUntrustedCollaborationLabel](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent) Advanced, et que vous configurez également le paramètre **EnableOutlookDistributionListExpansion** , Outlook est activé pour étendre la liste de distribution afin de s’assurer qu’un message de blocage s’affiche si nécessaire.

Le délai d’expiration par défaut pour le développement de la liste de distribution est de **2000** millisecondes.

Pour modifier ce délai d’attente, créez le paramètre avancé suivant pour la stratégie sélectionnée :

- Clé : **OutlookGetEmailAddressesTimeOutMSProperty**
- Valeur : *entier, en millisecondes*

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableOutlookDistributionListExpansion="true"} @{OutlookGetEmailAddressesTimeOutMSProperty="3000"}
```

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Désactiver l’envoi de données d’audit à Azure Information Protection Analytics

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Le client d’étiquetage unifié Azure Information Protection prend en charge la création de rapports centraux et, par défaut, envoie ses données d’audit à [Azure information protection Analytics](../reports-aip.md). Pour plus d’informations sur les informations qui sont envoyées et stockées, consultez la section [informations recueillies et envoyées à Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft) dans la documentation du centre de création de rapports.

Pour modifier ce comportement afin que ces informations ne soient pas envoyées par le client d’étiquetage unifié, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableAudit**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}
```

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>Envoyer les correspondances de type d’informations à Azure Information Protection Analytics
 
Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, le client d’étiquetage unifié n’envoie pas de correspondances de contenu pour les types d’informations sensibles à [Azure information protection Analytics](../reports-aip.md). Pour plus d’informations sur ces informations supplémentaires qui peuvent être envoyées, consultez la section [correspondances de contenu pour une analyse plus poussée](../reports-aip.md#content-matches-for-deeper-analysis) dans la documentation du centre de création de rapports.

Pour envoyer des correspondances de contenu lors de l’envoi de types d’informations sensibles, créez le paramètre de client avancé suivant dans une stratégie d’étiquette : 

- Clé : **LogMatchedContent**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}
```

## <a name="limit-cpu-consumption"></a>Limiter la consommation de l’UC

Le scanneur d’étiquetage unifié AIP limite la consommation des ressources pour s’assurer que le processeur de l’ordinateur ne dépasse jamais 85 pour cent. 

Depuis la version 2.7. x. x du scanner, nous vous recommandons de limiter la consommation de l’UC à l’aide de la méthode de paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU** suivante. 

> [!IMPORTANT]
> Lorsque la stratégie de limitation de threads suivante est utilisée, les paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU** sont ignorés. Pour limiter la consommation de l’UC à l’aide des paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU** , annulez l’utilisation des stratégies qui limitent le nombre de threads. 

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Pour limiter la consommation de l’UC sur l’ordinateur du scanneur, il est gérable en créant deux paramètres avancés : 

- **ScannerMaxCPU**: 

    Défini sur **100** par défaut, ce qui signifie qu’il n’y a pas de limite de consommation maximale de l’UC. Dans ce cas, le processus du scanneur essaiera d’utiliser tout le temps processeur disponible pour optimiser les taux d’analyse. 

    Si vous affectez à **ScannerMaxCPU** une valeur inférieure à 100, le scanneur surveille la consommation du processeur au cours des 30 dernières minutes, et si le processeur Max franchit la limite que vous avez définie, il commence à réduire le nombre de threads alloués pour les nouveaux fichiers. 

    La limite du nombre de threads se poursuit tant que la consommation du processeur est supérieure à la limite définie pour **ScannerMaxCPU**.

- **ScannerMinCPU**:

    Activé uniquement si **ScannerMaxCPU** n’est pas égal à 100 et ne peut pas être défini sur un nombre supérieur à la valeur  **ScannerMaxCPU** .  Nous vous recommandons de laisser **ScannerMinCPU** définir au moins 15 points inférieurs à la valeur de  **ScannerMaxCPU**.    
    
    Défini sur **50** par défaut, ce qui signifie que si la consommation du processeur au cours des 30 dernières minutes est inférieure à cette valeur, le scanneur commence à ajouter de nouveaux threads pour analyser plus de fichiers en parallèle, jusqu’à ce que la consommation du processeur atteigne le niveau que vous avez défini pour **ScannerMaxCPU**-15. 


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limiter le nombre de threads utilisés par le scanneur

> [!IMPORTANT]
> Lorsque la stratégie de limitation de threads suivante est utilisée, les paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU** sont ignorés. Pour limiter la consommation de l’UC à l’aide des paramètres avancés **ScannerMaxCPU** et **ScannerMinCPU** , annulez l’utilisation des stratégies qui limitent le nombre de threads. 

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, le scanneur utilise toutes les ressources du processeur disponibles sur l’ordinateur exécutant le service du scanneur. Si vous devez limiter la consommation du processeur pendant l’analyse de ce service, créez le paramètre avancé suivant dans une stratégie d’étiquette. 

Pour la valeur, spécifiez le nombre de threads simultanés que le scanneur peut exécuter en parallèle. Comme le scanneur utilise un thread distinct pour chaque fichier qu’il analyse, cette configuration de limitation définit donc le nombre de fichiers pouvant être analysés en parallèle. 

Lorsque vous configurez tout d’abord la valeur pour le test, nous vous recommandons de spécifier 2 par cœur, puis de surveiller les résultats. Par exemple, si vous exécutez le scanneur sur un ordinateur disposant de 4 cœurs, définissez tout d’abord la valeur 8. Si nécessaire, augmentez ou diminuez ce nombre, selon les performances qui vous sont nécessaires pour l’ordinateur du scanneur et votre fréquence d’analyse. 

- Clé : **ScannerConcurrencyLevel**

- Ajoutée **\<number of concurrent threads>**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « scanner » :

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}
```

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migrer des étiquettes de Secure Islands et d’autres solutions d’étiquetage

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) pour les étiquettes que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Cette configuration n’est pas compatible avec les fichiers PDF protégés qui ont une extension de nom de fichier. ppdf. Ces fichiers ne peuvent pas être ouverts par le client à l’aide de l’Explorateur de fichiers ou de PowerShell.

Pour les documents Office étiquetés par des îlots sécurisés, vous pouvez réétiqueter ces documents avec une étiquette de sensibilité à l’aide d’un mappage que vous définissez. Cette méthode permet également de réutiliser les étiquettes d’autres solutions qui se trouvent sur des documents Office. 

À la suite de cette option de configuration, la nouvelle étiquette de sensibilité est appliquée par le client d’étiquetage unifié Azure Information Protection comme suit :

- **Pour les documents Office :** Lorsque le document est ouvert dans l’application de bureau, la nouvelle étiquette de sensibilité est indiquée comme définie et appliquée lorsque le document est enregistré.

- **Pour PowerShell :** [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) peuvent appliquer la nouvelle étiquette de sensibilité.

- **Pour l’Explorateur de fichiers :** Dans la boîte de dialogue Azure Information Protection, la nouvelle étiquette de sensibilité est affichée, mais n’est pas définie.

Cette configuration nécessite que vous spécifiiez un paramètre avancé nommé **labelByCustomProperties** pour chaque étiquette de sensibilité que vous souhaitez mapper à l’ancienne étiquette. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

```PowerShell
[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]
```

Spécifiez votre choix d’un nom de règle de migration. Utilisez un nom descriptif qui vous aide à identifier la manière dont une ou plusieurs étiquettes de votre solution d’étiquetage précédente doivent être mappées à l’étiquette de sensibilité.

Notez que ce paramètre ne supprime pas l’étiquette d’origine du document ni les marquages visuels du document que l’étiquette d’origine a éventuellement appliqués. Pour supprimer des en-têtes et des pieds de page, consultez [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions).

Exemples :

- [Exemple 1 : mappage du même nom d’étiquette](#example-1-one-to-one-mapping-of-the-same-label-name)
- [Exemple 2 : un mappage pour un autre nom d’étiquette](#example-2-one-to-one-mapping-for-a-different-label-name)
- [Exemple 3 : mappage de plusieurs noms d’étiquettes en un](#example-3-many-to-one-mapping-of-label-names)
- [Exemple 4 : plusieurs règles pour la même étiquette](#example-4-multiple-rules-for-the-same-label)

Pour une personnalisation supplémentaire, consultez :

- [Étendre vos règles de migration d’étiquette aux e-mails](#extend-your-label-migration-rules-to-emails)
- [Étendre vos règles de migration d’étiquette à des propriétés SharePoint](#extend-your-label-migration-rules-to-sharepoint-properties)

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Exemple 1 : mappage du même nom d’étiquette

Exigence : les documents qui ont une étiquette des îlots sécurisés « confidentiel » doivent être réétiquetés comme « confidentiels » par Azure Information Protection.

Dans cet exemple :

- L’étiquette Secure Islands s’appelle **Confidentiel** et est stockée dans la propriété personnalisée nommée **Classification**.

Paramètre avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés est confidentielle, classification, confidentiel**

Exemple de commande PowerShell, où votre étiquette est nommée « Confidential » :

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}
```

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Exemple 2 : un mappage pour un autre nom d’étiquette

Exigence : les documents intitulés « sensibles » par les îles sécurisées doivent être renommés comme « hautement confidentiels » par Azure Information Protection.

Dans cet exemple :

- L’étiquette Secure Islands s’appelle **Sensible** et est stockée dans la propriété personnalisée nommée **Classification**.

Paramètre avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés est sensible, classification, sensible**

Exemple de commande PowerShell, où votre étiquette est nommée « hautement confidentiel » :

```PowerShell
Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}
```

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Exemple 3 : mappage de plusieurs noms d’étiquettes en un

Exigence : vous avez deux étiquettes de îles sécurisées qui incluent le mot « Internal » et vous souhaitez que les documents qui ont l’une de ces étiquettes des îlots sécurisés soient réétiquetés comme « général » par le client d’étiquetage unifié Azure Information Protection.

Dans cet exemple :

- L’étiquette Secure Islands inclut le mot **Interne** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés contient Internal, classification. \* Interne. \***

Exemple de commande PowerShell, où votre étiquette est nommée « général » :

```PowerShell
Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}
```

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Exemple 4 : plusieurs règles pour la même étiquette

Lorsque vous avez besoin de plusieurs règles pour la même étiquette, définissez plusieurs valeurs de chaîne pour la même clé. 

Dans cet exemple, les étiquettes des îles sécurisées nommées « confidentiel » et « secret » sont stockées dans la propriété personnalisée nommée **classification** et vous souhaitez que le Azure information protection client d’étiquetage unifié applique l’étiquette de sensibilité nommée « confidentiel » :

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

### <a name="extend-your-label-migration-rules-to-emails"></a>Étendre vos règles de migration d’étiquette aux e-mails

Vous pouvez utiliser la configuration que vous avez définie avec le paramètre avancé [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) pour les courriers électroniques Outlook, en plus des documents Office, en spécifiant un paramètre avancé de stratégie d’étiquette supplémentaire. 

Toutefois, ce paramètre a un impact négatif connu sur les performances d’Outlook. par conséquent, configurez ce paramètre supplémentaire uniquement si vous avez une forte exigence pour l’entreprise et n’oubliez pas de le définir sur une valeur de chaîne NULL lorsque vous avez terminé la migration à partir de l’autre solution d’étiquetage.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableLabelByMailHeader**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}
```

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>Étendre vos règles de migration d’étiquette à des propriétés SharePoint

Vous pouvez utiliser la configuration que vous avez définie avec le paramètre avancé [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) pour les propriétés SharePoint que vous pouvez exposer en tant que colonnes aux utilisateurs en spécifiant un paramètre avancé de stratégie d’étiquette supplémentaire.

Ce paramètre est pris en charge lorsque vous utilisez Word, Excel et PowerPoint.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableLabelBySharePointProperties**

- Valeur : **true**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}
```

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) pour les étiquettes que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Il peut y avoir des scénarios lorsque vous souhaitez appliquer une ou plusieurs propriétés personnalisées à un document ou à un message électronique en plus des métadonnées appliquées par une étiquette de sensibilité.

Par exemple :

- Vous êtes en train de [migrer à partir d’une autre solution d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions), telle que des îlots sécurisés. Pour l’interopérabilité au cours de la migration, vous souhaitez que les étiquettes de sensibilité appliquent également une propriété personnalisée utilisée par l’autre solution d’étiquetage.

- Pour votre système de gestion de contenu (par exemple, SharePoint ou une solution de gestion de documents d’un autre fournisseur), vous souhaitez utiliser un nom de propriété personnalisée cohérent avec des valeurs différentes pour les étiquettes et des noms conviviaux au lieu du GUID de l’étiquette.

Pour les documents Office et les e-mails Outlook libellés par les utilisateurs à l’aide du client d’étiquetage unifié Azure Information Protection, vous pouvez ajouter une ou plusieurs propriétés personnalisées que vous définissez. Vous pouvez également utiliser cette méthode pour le client d’étiquetage unifié pour afficher une propriété personnalisée sous la forme d’une étiquette à partir d’autres solutions pour le contenu qui n’est pas encore étiqueté par le client d’étiquetage unifié.

À la suite de cette option de configuration, toutes les propriétés personnalisées supplémentaires sont appliquées par le client d’étiquetage unifié Azure Information Protection, comme suit :

|Environnement  | Description  |
|---------|---------|
|**Documents Office**    | Lorsque le document est étiqueté dans l’application de bureau, les propriétés personnalisées supplémentaires sont appliquées lors de l’enregistrement du document.        |
|**Courriers électroniques Outlook**     |    Lorsque le message électronique est étiqueté dans Outlook, les propriétés supplémentaires sont appliquées à l’en-tête x lors de l’envoi de l’e-mail.     |
|**PowerShell**     |  [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) appliquent les propriétés personnalisées supplémentaires lorsque le document est étiqueté et enregistré. <br><br>La fonction [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) affiche les propriétés personnalisées en tant qu’étiquette mappée si une étiquette de sensibilité n’est pas appliquée.  |
|**Explorateur de fichiers**     |     Quand l’utilisateur clique avec le bouton droit sur le fichier et applique l’étiquette, les propriétés personnalisées sont appliquées.     |
|     |         |


Cette configuration nécessite que vous spécifiiez un paramètre avancé nommé **customPropertiesByLabel** pour chaque étiquette de sensibilité à laquelle vous souhaitez appliquer les propriétés personnalisées supplémentaires. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

```sh
[custom property name],[custom property value]
```

> [!IMPORTANT]
> L’utilisation d’espaces blancs dans la chaîne empêche l’application des étiquettes.

Par exemple :

- [Exemple 1 : ajouter une seule propriété personnalisée pour une étiquette](#example-1-add-a-single-custom-property-for-a-label)
- [Exemple 2 : ajouter plusieurs propriétés personnalisées pour une étiquette](#example-2-add-multiple-custom-properties-for-a-label)
#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Exemple 1 : ajouter une seule propriété personnalisée pour une étiquette

Exigence : les documents étiquetés comme étant « confidentiels » par le client d’étiquetage unifié Azure Information Protection doivent avoir la propriété personnalisée supplémentaire nommée « classification » avec la valeur « secret ».

Dans cet exemple :

- L’étiquette sensibilité est nommée **confidentiel** et crée une propriété personnalisée nommée **classification** avec la valeur **secret**.

Paramètre avancé :

- Clé : **customPropertiesByLabel**

- Valeur : **classification, secret**

Exemple de commande PowerShell, où votre étiquette est nommée « Confidential » :

```PowerShell
    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}
```

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Exemple 2 : ajouter plusieurs propriétés personnalisées pour une étiquette

Pour ajouter plusieurs propriétés personnalisées pour la même étiquette, vous devez définir plusieurs valeurs de chaîne pour la même clé.

Exemple de commande PowerShell, où votre étiquette est nommée « General » et que vous souhaitez ajouter une propriété personnalisée nommée **classification** avec la valeur **General** et une deuxième propriété personnalisée nommée **Sensitivity** avec la valeur **Internal**:

```PowerShell
Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}
```

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurer une étiquette pour appliquer la protection S/MIME dans Outlook

Cette configuration utilise des [Paramètres avancés](#configuring-advanced-settings-for-the-client-via-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Utilisez ces paramètres uniquement lorsque vous disposez d’un [déploiement S/MIME](/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) opérationnel et que vous souhaitez qu’une étiquette applique automatiquement cette méthode de protection pour les e-mails plutôt que Rights Management protection à partir de Azure information protection. La protection qui en résulte est la même que lorsque l’utilisateur sélectionne manuellement les options S/MIME dans Outlook.

|Configuration  |Clé/valeur  |
|---------|---------|
|**Signature numérique S/MIME**     |   Pour configurer un paramètre avancé pour une signature numérique S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée : <br><br>-Clé : **SMimeSign** <br><br>-Valeur : **true**      |
|**Chiffrement S/MIME**     |   Pour configurer un paramètre avancé pour le chiffrement S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée :<br><br>-Clé : **SMimeEncrypt**<br><br>-Valeur : **true**      |
|     |         |

Si l’étiquette que vous spécifiez est configurée pour le chiffrement, pour le client d’étiquetage unifié Azure Information Protection, la protection S/MIME remplace la protection Rights Management uniquement dans Outlook. Le client continue d’utiliser les paramètres de chiffrement spécifiés pour l’étiquette dans le centre d’administration. 

Pour les applications Office avec étiquetage intégré, celles-ci n’appliquent pas la protection S/MIME mais appliquent la protection **ne pas transférer** .

Si vous souhaitez que l’étiquette soit visible dans Outlook uniquement, configurez l’étiquette pour appliquer le chiffrement **uniquement aux messages électroniques dans Outlook**.

Exemples de commandes PowerShell, où votre étiquette est nommée « destinataires uniquement » :

```PowerShell
Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}
```

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Spécifier une sous-étiquette par défaut pour une étiquette parent

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) pour les étiquettes que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Lorsque vous ajoutez une sous-étiquette à une étiquette, les utilisateurs ne peuvent plus appliquer l’étiquette parent à un document ou à un e-mail. Par défaut, les utilisateurs sélectionnent l’étiquette parente pour afficher les sous-étiquettes qu’elles peuvent appliquer, puis sélectionnent l’une de ces sous-étiquettes. Si vous configurez ce paramètre avancé, lorsque les utilisateurs sélectionnent l’étiquette parent, une sous-étiquette est automatiquement sélectionnée et appliquée : 

- Clé : **DefaultSubLabelId**

- Ajoutée **\<sublabel GUID>**

Exemple de commande PowerShell, où votre étiquette parente est nommée « Confidential » et la sous-étiquette « all employees » a le GUID 8faca7b8-8d20-48A3-8ea2-0f96310a848e :

```PowerShell
Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
```

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>Activer la classification pour qu’elle s’exécute en continu en arrière-plan

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) pour les étiquettes que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell. 

Quand vous configurez ce paramètre, il modifie le comportement par défaut de la façon dont le Azure Information Protection client d’étiquetage unifié applique les étiquettes automatiques et recommandées aux documents :

Pour Word, Excel et PowerPoint, la classification automatique s’exécute en continu en arrière-plan.

Le comportement ne change pas pour Outlook.

Lorsque le Azure Information Protection client d’étiquetage unifié vérifie régulièrement les règles de condition que vous spécifiez, ce comportement active la classification et la protection automatiques et recommandées pour les documents Office stockés dans SharePoint ou OneDrive, tant que l’enregistrement automatique est activé. Les fichiers volumineux sont également enregistrés plus rapidement, car les règles de condition ont déjà été exécutées.

Les règles des conditions ne s’exécutent pas en temps réel pendant la saisie de l’utilisateur. Elles s’exécutent plutôt à intervalles réguliers sous la forme d’une tâche en arrière-plan si le document est modifié.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **RunPolicyInBackground**
- Valeur : **true**

Exemple de commande PowerShell : 

```PowerShell
Set-LabelPolicy -Identity PolicyName -AdvancedSettings @{RunPolicyInBackground = "true"}
```

> [!NOTE]
> Cette fonctionnalité est actuellement en PRÉVERSION. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 
> 

## <a name="specify-a-color-for-the-label"></a>Spécifier une couleur pour l’étiquette

Cette configuration utilise des [Paramètres avancés](#configuring-advanced-settings-for-the-client-via-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Utilisez ce paramètre avancé pour définir la couleur d’une étiquette. Pour spécifier la couleur, entrez un code d’triplement hexadécimal pour les composants rouge, vert et bleu (RVB) de la couleur. Par exemple, #40e0d0 est la valeur hexadécimale RVB pour turquoise.

Si vous avez besoin d’une référence pour ces codes, vous trouverez une table utile à partir de la [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) page des documents Web MSDN. Vous trouverez également ces codes dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

Pour configurer le paramètre avancé pour la couleur d’un contrôle Label, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **couleur**

- Ajoutée **\<RGB hex value>**

Exemple de commande PowerShell, où votre étiquette est nommée « public » :

```PowerShell
Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}
```

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

La connexion avec plusieurs utilisateurs n’est pas prise en charge par AIP en production. Cette procédure décrit comment se connecter en tant qu’utilisateur différent à des fins de test uniquement.

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure information protection** : Ouvrez une application Office et, sous l’onglet dossier de **démarrage** , cliquez sur le bouton **sensibilité** , puis sélectionnez **aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Un symptôme de l’utilisation d’un compte incorrect comprend l’échec du téléchargement des étiquettes ou l’affichage des étiquettes ou du comportement que vous attendez.

**Pour vous connecter en tant qu’autre utilisateur**:

1. Accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si vous ne voyez pas d’invite dans votre application Office pour vous connecter au service Azure Information Protection, revenez à la boîte de dialogue **Microsoft Azure information protection** et sélectionnez **se connecter** à partir de la section **État du client** mis à jour.

De plus :

|Scénario  |Description  |
|---------|---------|
|**Toujours connecté à l’ancien compte**     |  Si le client d’étiquetage unifié Azure Information Protection est toujours connecté avec l’ancien compte après avoir effectué ces étapes, supprimez tous les cookies d’Internet Explorer, puis répétez les étapes 1 et 2.       |
|**Utilisation de l’authentification unique**    |    Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir supprimé le fichier de jeton. <br><br>Le Azure Information Protection client d’étiquetage unifié s’authentifie ensuite automatiquement à l’aide de votre compte d’utilisateur actuellement connecté.     |
|**Différents locataires**     |  Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. <br><br>Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.       |
|**Réinitialiser les paramètres**     | Vous pouvez utiliser l’option **Réinitialiser les paramètres** dans **aide et commentaires** pour vous déconnecter et supprimer les étiquettes et les paramètres de stratégie actuellement téléchargés à partir du centre de conformité d’Office 365 Security &, du centre de sécurité Microsoft 365 ou du centre de conformité Microsoft 365.        |
|     |         |

## <a name="support-for-disconnected-computers"></a>Prise en charge des ordinateurs déconnectés

> [!IMPORTANT]
> Les ordinateurs déconnectés sont pris en charge pour les scénarios d’étiquetage suivants : Explorateur de fichiers, PowerShell, vos applications Office et le scanneur.

Par défaut, le Azure Information Protection client d’étiquetage unifié tente automatiquement de se connecter à Internet pour télécharger les étiquettes et les paramètres de stratégie d’étiquette à partir de votre centre de gestion des étiquettes (le centre de conformité de la sécurité des & Office 365, le centre de sécurité Microsoft 365 ou le Microsoft 365 Compliance Center). 

Si vous avez des ordinateurs qui ne peuvent pas se connecter à Internet pendant un certain temps, vous pouvez exporter et copier des fichiers qui gèrent manuellement la stratégie du client d’étiquetage unifié.

**Pour prendre en charge les ordinateurs déconnectés du client d’étiquetage unifié :**

1. Choisissez ou créez un compte d’utilisateur dans Azure AD que vous allez utiliser pour télécharger des étiquettes et des paramètres de stratégie que vous souhaitez utiliser sur votre ordinateur déconnecté.

2. En tant que paramètre de stratégie d’étiquette supplémentaire pour ce compte, [désactivez l’envoi de données d’audit à Azure information protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) à l’aide du paramètre avancé **EnableAudit** .
    
    Nous vous recommandons d’effectuer cette étape, car si l’ordinateur déconnecté dispose d’une connectivité Internet périodique, il envoie les informations de journalisation à Azure Information Protection Analytics qui comprend le nom d’utilisateur de l’étape 1. Ce compte d’utilisateur peut être différent du compte local que vous utilisez sur l’ordinateur déconnecté.

3. À partir d’un ordinateur connecté à Internet et sur lequel le client d’étiquetage unifié est installé et connecté avec le compte d’utilisateur de l’étape 1, téléchargez les étiquettes et les paramètres de stratégie.

4. À partir de cet ordinateur, exportez les fichiers journaux.
    
    Par exemple, exécutez l’applet de commande [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) ou utilisez l’option **Exporter les journaux** de la boîte de dialogue [aide et commentaires](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client) du client. 
    
    Les fichiers journaux sont exportés sous la forme d’un fichier compressé unique.

5.  Ouvrez le fichier compressé et, à partir du dossier MSIP, copiez tous les fichiers qui ont une extension de nom de fichier. Xml.

6. Collez ces fichiers dans le dossier **%LocalAppData%\Microsoft\MSIP** sur l’ordinateur déconnecté.

7. Si le compte d’utilisateur choisi est un compte qui se connecte généralement à Internet, activez à nouveau l’envoi des données d’audit en affectant à la valeur **EnableAudit** la valeur **true**.

N’oubliez pas que si un utilisateur de cet ordinateur sélectionne l’option **Réinitialiser les paramètres** dans [aide et commentaires](clientv2-admin-guide.md#help-and-feedback-section), cette action supprime les fichiers de stratégie et rend le client inopérant tant que vous n’avez pas remplacé manuellement les fichiers ou que le client ne se connecte pas à Internet et télécharge les fichiers.

Si votre ordinateur déconnecté exécute le scanneur Azure Information Protection, vous devez effectuer des étapes de configuration supplémentaires. Pour plus d’informations, voir [restriction : le serveur du scanneur ne peut pas disposer d’une connexion Internet](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) à partir des instructions de déploiement de l’analyseur.

## <a name="change-the-local-logging-level"></a>Modifier le niveau de journalisation local

Par défaut, le Azure Information Protection client d’étiquetage unifié écrit les fichiers journaux du client dans le dossier **%LocalAppData%\Microsoft\MSIP** . Ces fichiers servent à la résolution des problèmes par le Support Microsoft.
 
Pour modifier le niveau de journalisation de ces fichiers, localisez le nom de la valeur suivante dans le registre et définissez les données de la valeur sur le niveau de journalisation requis :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Définissez le niveau de journalisation sur l'une des valeurs suivantes :

- **Off**: aucune journalisation locale.

- **Erreur**: erreurs uniquement.

- **WARN**: erreurs et avertissements.

- **Info**: journalisation minimale, qui n’indique aucun ID d’événement (paramètre par défaut pour le scanneur).

- **Débogage**: informations complètes.

- **Trace**: journalisation détaillée (paramètre par défaut pour les clients).

Ce paramètre de registre ne modifie pas les informations qui sont envoyées à Azure Information Protection pour la [création de rapports centraux](../reports-aip.md).

## <a name="skip-or-ignore-files-during-scans-depending-on-file-attributes"></a>Ignorer ou ignorer les fichiers lors des analyses en fonction des attributs de fichier

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, le Azure Information Protection scanneur d’étiquetage unifié analyse tous les fichiers appropriés. Toutefois, vous pouvez définir des fichiers spécifiques à ignorer, par exemple pour les fichiers archivés ou les fichiers qui ont été déplacés. 

Activez le scanneur pour ignorer des fichiers spécifiques en fonction de leurs attributs de fichier à l’aide du paramètre avancé **ScannerFSAttributesToSkip** . Dans la valeur de paramètre, répertoriez les attributs de fichier qui permettront d’ignorer le fichier lorsqu’ils sont tous définis sur **true**. Cette liste d’attributs de fichier utilise la logique et.

Les exemples de commandes PowerShell suivants illustrent l’utilisation de ce paramètre avancé avec une étiquette nommée « global ».

**Ignorer les fichiers qui sont en lecture seule et archivés**

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY, FILE_ATTRIBUTE_ARCHIVE"}
```

**Ignorer les fichiers qui sont en lecture seule ou archivés**

Pour utiliser une logique ou, exécutez la même propriété plusieurs fois. Par exemple :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY"}
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_ARCHIVE"}
```

> [!TIP]
> Nous vous recommandons d’activer le scanneur pour qu’il ignore les fichiers avec les attributs suivants :
> * FILE_ATTRIBUTE_SYSTEM
> * FILE_ATTRIBUTE_HIDDEN
> * FILE_ATTRIBUTE_DEVICE
> * FILE_ATTRIBUTE_OFFLINE
> * FILE_ATTRIBUTE_RECALL_ON_DATA_ACCESS
> * FILE_ATTRIBUTE_RECALL_ON_OPEN
> * FILE_ATTRIBUTE_TEMPORARY

Pour obtenir la liste de tous les attributs de fichier qui peuvent être définis dans le paramètre avancé **ScannerFSAttributesToSkip** , consultez [constantes d’attribut de fichier Win32](/windows/win32/fileio/file-attribute-constants) .

## <a name="preserve-ntfs-owners-during-labeling-public-preview"></a>Conserver les propriétaires NTFS lors de l’étiquetage (version préliminaire publique)

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

Par défaut, les étiquettes scanner, PowerShell et de l’extension de l’Explorateur de fichiers ne conservent pas le propriétaire NTFS qui a été défini avant l’étiquetage. 

Pour vous assurer que la valeur de propriétaire NTFS est préservée, affectez la valeur **true** au paramètre avancé **UseCopyAndPreserveNTFSOwner** pour la stratégie d’étiquette sélectionnée.

> [!CAUTION]
> Définissez ce paramètre avancé uniquement lorsque vous pouvez garantir une connexion réseau fiable et à faible latence entre le scanneur et le référentiel analysé. Une défaillance du réseau pendant le processus d’étiquetage automatique peut entraîner la perte du fichier.

Exemple de commande PowerShell, lorsque votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ UseCopyAndPreserveNTFSOwner ="true"}
```

> [!NOTE]
> Cette fonctionnalité est actuellement en PRÉVERSION. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 
> 

## <a name="customize-justification-prompt-texts-for-modified-labels"></a>Personnaliser les textes d’invite de justification pour les étiquettes modifiées

Personnaliser les invites de justification qui s’affichent à la fois dans Office et le client AIP, lorsque les utilisateurs finaux modifient les étiquettes de classification sur les documents et les e-mails.

Par exemple, en tant qu’administrateur, il se peut que vous souhaitiez rappeler à vos utilisateurs de ne pas ajouter les informations d’identification du client dans ce champ :

:::image type="content" source="../media/justification-office.png" alt-text="Texte d’invite de justification personnalisé":::

Pour modifier **le texte par** défaut affiché, utilisez la propriété avancée **JustificationTextForUserText** avec l’applet de commande [Set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) . Définissez la valeur sur le texte que vous souhaitez utiliser à la place.

Exemple de commande PowerShell, lorsque votre stratégie d’étiquette est nommée « global » :

``` PowerShell

[Set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
```

## <a name="customize-outlook-popup-messages"></a>Personnaliser les messages de la fenêtre contextuelle Outlook

Les administrateurs AIP peuvent personnaliser les messages contextuels qui s’affichent pour les utilisateurs finaux dans Outlook, par exemple :

- Messages pour les e-mails bloqués
- Messages d’avertissement invitant les utilisateurs à vérifier le contenu qu’ils envoient
- Messages de justification qui demandent aux utilisateurs de justifier le contenu qu’ils envoient

> [!IMPORTANT]
> Cette procédure remplacera tous les paramètres que vous avez déjà définis à l’aide de la propriété avancée [OutlookUnlabeledCollaborationAction](#to-specify-a-different-action-for-email-messages-without-attachments) .
>
> En production, nous vous recommandons d’éviter les complications *en utilisant* la propriété avancée [OutlookUnlabeledCollaborationAction](#to-specify-a-different-action-for-email-messages-without-attachments) pour définir vos règles, *ou* en définissant des règles complexes avec un fichier **JSON** tel que défini ci-dessous, mais pas les deux.
>

**Pour personnaliser vos messages Outlook**:

1. Créez des fichiers **. JSON** , chacun avec une règle qui configure la façon dont Outlook affiche les messages contextuels à vos utilisateurs. Pour plus d’informations, consultez Syntaxe de la [règle. JSON](#rule-value-json-syntax) et [exemple de personnalisation contextuelle. code JSON](#sample-popup-customization-json-code).

1. Utilisez PowerShell pour définir des paramètres avancés qui contrôlent les messages contextuels que vous configurez. Exécutez un ensemble de commandes distinct pour chaque règle que vous souhaitez configurer.

    Chaque ensemble de commandes PowerShell doit inclure le nom de la stratégie que vous configurez, ainsi que la clé et la valeur qui définissent votre règle.

    Utilisez la syntaxe suivante :

    ```PowerShell
    $filedata = Get-Content "<Path to json file>”
    Set-LabelPolicy -Identity <Policy name> -AdvancedSettings @{<Key> ="$filedata"}
    ```
    Où : 

    - `<Path to json file>` est le chemin d’accès au fichier JSON que vous avez créé. Par exemple : **C:\Users\msanchez\Desktop\ \dlp\OutlookCollaborationRule_1.json**.
    - `<Policy name>` nom de la stratégie que vous souhaitez configurer. 
    - `<Key>` est le nom de votre règle. Utilisez la syntaxe suivante, où **<#>** est le numéro de série de votre règle : 
    
        `OutlookCollaborationRule_<x>` 

    Pour plus d’informations, consultez [classement des règles de personnalisation Outlook](#ordering-your-outlook-customization-rules) et [syntaxe JSON](#rule-value-json-syntax)de la valeur de règle.

   
> [!TIP]
> Pour une organisation supplémentaire, nommez votre fichier avec la même chaîne que la clé utilisée dans votre commande PowerShell. Par exemple, nommez votre fichier **OutlookCollaborationRule_1.jssur**, puis utilisez également **OutlookCollaborationRule_1** comme clé.
>
> Pour garantir l’affichage des fenêtres contextuelles, même lorsque les documents sont partagés à partir d’Outlook **(partage de > de fichiers > joindre une copie)**, configurez également le paramètre avancé [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) .
> 

### <a name="ordering-your-outlook-customization-rules"></a>Classement des règles de personnalisation d’Outlook

AIP utilise le numéro de série de la clé que vous entrez pour déterminer l’ordre de traitement des règles. Lors de la définition des clés utilisées pour chaque règle, définissez vos règles plus restrictives avec des nombres inférieurs, suivies de règles moins restrictives avec des nombres plus élevés.

Une fois qu’une correspondance de règle spécifique a été trouvée, AIP arrête le traitement des règles et effectue l’action associée à la règle de correspondance. (Logique **de sortie de la première correspondance >** )
    
**Exemple** :

Imaginons que vous souhaitiez configurer tous les courriers électroniques **internes** avec un message d' **Avertissement** spécifique, mais que vous ne souhaitez généralement pas les bloquer. Toutefois, vous souhaitez empêcher les utilisateurs d’envoyer des pièces jointes classées comme **secrets**, même en tant qu’e-mails **internes** . 

Dans ce scénario, classez votre clé de règle de **secret de bloc** , qui est la règle la plus spécifique, avant d’obtenir une clé **de règle d’avertissement en interne** plus générique :
- Pour le message de **blocage** : **OutlookCollaborationRule_1**
- Pour le message d' **Avertissement** : **OutlookCollaborationRule_2**

### <a name="rule-value-json-syntax"></a>Syntaxe de la valeur de la règle. JSON

Définissez la syntaxe JSON de votre règle comme suit :

``` JSON
"type" : "And",
"nodes" : []
```

Vous devez avoir au moins deux nœuds, le premier représentant la condition de la règle et le dernier représentant l’action de la règle. Pour plus d'informations, consultez les pages suivantes :

- [Syntaxe de condition de règle](#rule-condition-syntax)
- [Syntaxe de l’action de règle](#rule-action-syntax)

##### <a name="rule-condition-syntax"></a>Syntaxe de condition de règle

Les nœuds de condition de règle doivent inclure le type de nœud, puis les conditions elles-mêmes. 

Les types de nœuds pris en charge sont les suivants :

|Type de nœud  |Description  |
|---------|---------|
| **And**   | Effectue *et* sur tous les nœuds enfants     |
| **Ou**    |Effectue *ou* sur tous les nœuds enfants       |
| **Not**   | *N’effectue pas* pour son propre enfant      |
| **Except**    | Retourne la valeur *not* pour son propre enfant, provoquant son comportement comme **All**        |
| **SentTo**, suivi des **domaines : listOfDomains**    |Vérifie l’un des éléments suivants : <br>-Si le parent est **except**, vérifie si **tous** les destinataires se trouvent dans l’un des domaines.<br>-Si le parent est autre que, **à l’exception** de, **vérifie si l’un des** destinataires est dans l’un des domaines.   |
| **EMailLabel**, suivi de l’étiquette | Celui-ci peut avoir l'une des valeurs suivantes :  <br>-ID d’étiquette <br>-NULL, s’il n’est pas étiqueté             |
| **AttachmentLabel**, suivi par l' **étiquette** et les **Extensions** prises en charge   | Celui-ci peut avoir l'une des valeurs suivantes :  <br><br>**:** <br>-Si le parent est **except**, vérifie si **toutes** les pièces jointes avec une extension prise en charge existent dans l’étiquette<br>-Si le parent est autre que, **à l’exception** de, vérifie si l' **une** des pièces jointes avec une extension prise en charge existe dans l’étiquette <br>-S’il n’est pas étiqueté et **étiquette = null** <br><br> **false :** Pour tous les autres cas <br><br>**Remarque**: si la propriété **Extensions** est vide ou manquante, tous les types de fichiers pris en charge (extensions) sont inclus dans la règle.
| | |

#### <a name="rule-action-syntax"></a>Syntaxe de l’action de règle

Les actions de règle peuvent être l’une des suivantes :

|Action  |Syntaxe  |Exemple de message  |
|---------|---------|---------|
|**Bloquer**     |    `Block (List<language, [title, body]>)`     |    **_E-mail bloqué_* _<br /><br />  _You êtes sur le paragraphe de l’envoi d’un contenu classifié comme **secret** à un ou plusieurs destinataires non approuvés : *<br />* `rsinclair@contoso.com` *<br /><br />* la stratégie de votre organisation n’autorise pas cette action. Envisagez de supprimer ces destinataires ou de remplacer le contenu. *|
|**Viendra**     | `Warn (List<language,[title,body]>)`        |  **_Confirmation obligatoire_* _<br /><br />_You êtes sur le paragraphe de l’envoi d’un contenu classifié comme **général** à un ou plusieurs destinataires non approuvés : *<br />* `rsinclair@contoso.com` *<br /><br />* la stratégie de votre organisation nécessite une confirmation pour l’envoi de ce contenu. *       |
|**Prouver**     | `Justify (numOfOptions, hasFreeTextOption, List<language, [Title, body, options1,options2….]> )` <br /><br />Y compris jusqu’à trois options.        |  **_Justification obligatoire_* _ <br /><br />_Your stratégie d’organisation nécessite une justification pour envoyer le contenu classé comme **général** à des destinataires non approuvés. *<br /><br />* -Je confirme que les destinataires sont approuvés pour partager ce contenu *<br />* -mon responsable a approuvé le partage de ce contenu *<br />* -autre, comme expliqué * |
| | | |

##### <a name="action-parameters"></a>Paramètres d’action

Si aucun paramètre n’est fourni pour une action, les fenêtres contextuelles comporteront le texte par défaut. 

Tous les textes prennent en charge les paramètres dynamiques suivants : 

|Paramètre  |Description  |
|---------|---------|
| `${MatchedRecipientsList}`  | La dernière correspondance pour les conditions **SentTo**       |
| `${MatchedLabelName}`      | **Étiquette** de messagerie/pièce jointe, avec le nom localisé de la stratégie               |
| `${MatchedAttachmentName}` | Nom de la pièce jointe à partir de la dernière correspondance pour la condition **AttachmentLabel** |
| | |

> [!NOTE]
> Tous les messages incluent l’option en **savoir plus** , ainsi que les boîtes de dialogue **aide** et **Commentaires** .
>
> La **langue** est le **cultureName** pour le nom des paramètres régionaux, par exemple : **anglais**  =  `en-us` ; **Espagnol** = `es-es`
>
> Les noms de langue parent uniquement sont également pris en charge, par exemple `en` uniquement.
> 

### <a name="sample-popup-customization-json-code"></a>Exemple de personnalisation de la fenêtre contextuelle. code JSON

Les jeux de code **. JSON** suivants montrent comment vous pouvez définir une série de règles qui contrôlent la façon dont Outlook affiche les messages contextuels pour vos utilisateurs.

- [**Exemple 1**: bloquer les e-mails internes ou les pièces jointes](#example-1-block-internal-emails-or-attachments)
- [**Exemple 2**: bloquer les pièces jointes Office non classifiées](#example-2-block-unclassified-office-attachments)
- [**Exemple 3**: demander à l’utilisateur d’accepter l’envoi d’un e-mail ou d’une pièce jointe confidentiel](#example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment)
- [**Exemple 4**: signaler un message sans étiquette, et une pièce jointe avec une étiquette spécifique](#example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label)
- [**Exemple 5**: demander une justification, avec deux options prédéfinies et une option de texte libre supplémentaire](#example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option)

#### <a name="example-1-block-internal-emails-or-attachments"></a>Exemple 1 : bloquer les e-mails internes ou les pièces jointes

Le code **. JSON** suivant bloque les messages électroniques ou les pièces jointes qui sont classés comme **internes** , de la définition de destinataires externes.

Dans cet exemple, **89a453df-5df4-4976-8191-259d0cf9560a** est l’ID de l’étiquette **interne** , et les domaines internes incluent **contoso.com** et **Microsoft.com**.

Dans la mesure où aucune extension spécifique n’est spécifiée, tous les types de fichiers pris en charge sont inclus.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
              "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"              
                }
            ]
        },      
        {           
            "type" : "Block",           
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "The email or at least one of the attachments is classified as <Bold>${MatchedLabelName}</Bold>. Documents classified as <Bold> ${MatchedLabelName}</Bold> cannot be sent to external recipients (${MatchedRecipientsList}).<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance with classification requirements as per Contoso’s policies."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "El correo electrónico o al menos uno de los archivos adjuntos se clasifica como <Bold> ${MatchedLabelName}</Bold>."                
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-2-block-unclassified-office-attachments"></a>Exemple 2 : bloquer les pièces jointes Office non classifiées

Le code **. JSON** suivant bloque l’envoi de pièces jointes Office ou de messages électroniques non classifiés à des destinataires externes.

Dans l’exemple suivant, la liste des pièces jointes qui requiert un étiquetage est : **. doc,. docm,. docx,. dot,. dotm,. dotx,. potm,. potx,. PPS,. PPSM,. ppsx,. ppt,. pptm,. pptx,. vdw,. VSD,. VSDM,. vsdx,. VSS,. VSSM,. VST,. vstm,. vssx** ,. vstx,.,. xlsb,. xlt,. xltm,. xltx

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".doc",
                                    ".docm",
                                    ".docx",
                                    ".dot",
                                    ".dotm",
                                    ".dotx",
                                    ".potm",
                                    ".potx",
                                    ".pps",
                                    ".ppsm",
                                    ".ppsx",
                                    ".ppt",
                                    ".pptm",
                                    ".pptx",
                                    ".vdw",
                                    ".vsd",
                                    ".vsdm",
                                    ".vsdx",
                                    ".vss",
                                    ".vssm",
                                    ".vst",
                                    ".vstm",
                                    ".vssx",
                                    ".vstx",
                                    ".xls",
                                    ".xlsb",
                                    ".xlt",
                                    ".xlsm",
                                    ".xlsx",
                                    ".xltm",
                                    ".xltx"
                                 ]
                    
                },{                     
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Emailed Blocked",                   
                    "Body": "Classification is necessary for attachments to be sent to external recipients.<br><br>List of attachments that are not classified:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>For MS Office documents, classify and send again.<br><br>For PDF files, classify the document or classify the email (using the most restrictive classification level of any single attachment or the email content) and send again."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "La clasificación es necesaria para que los archivos adjuntos se envíen a destinatarios externos."              
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment"></a>Exemple 3 : demander à l’utilisateur d’accepter l’envoi d’un e-mail ou d’une pièce jointe confidentiel

L’exemple suivant fait en sorte qu’Outlook affiche un message qui avertit l’utilisateur qu’il envoie **un courrier électronique** ou une pièce jointe à des destinataires externes, et qu’il exige que l’utilisateur sélectionne **J’accepte**. 

Ce type de message d’avertissement est techniquement considéré comme une justification, car l’utilisateur doit sélectionner **J’accepte**.

Dans la mesure où aucune extension spécifique n’est spécifiée, tous les types de fichiers pris en charge sont inclus.

``` PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"              
                }
            ]
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Warning",                   
                    "Body": "You are sending a document that is classified as <Bold>${MatchedLabelName}</Bold> to at least one external recipient. Please make sure that the content is correctly classified and that the recipients are entitled to receive this document.<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><Bold>List of external email addresses:</Bold><br>${MatchedRecipientsList})<br><br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br><Bold>Acknowledgement</Bold><br>By clicking <Bold>I accept<\Bold> below, you confirm that the recipient is entitled to receive the content and the communication complies with CS Policies and Standards",
                    "Options": [                        
                        "I accept"              
                    ] 
                },              
                "es-es": {                
                    "Title": "Advertencia",                   
                    "Body": "Está enviando un documento clasificado como <Bold>${MatchedLabelName}</Bold> a al menos un destinatario externo. Asegúrese de que el contenido esté correctamente clasificado y que los destinatarios tengan derecho a recibir este documento.",
                    "Options": [                        
                        "Acepto"                    
                    ]                   
                }           
            },          
            "HasFreeTextOption":"false",            
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label"></a>Exemple 4 : signaler un message sans étiquette, et une pièce jointe avec une étiquette spécifique

Le **code. JSON** suivant fait en sorte qu’Outlook avertisse l’utilisateur lorsqu’il envoie un e-mail interne sans étiquette, avec une pièce jointe qui a une étiquette spécifique. 

Dans cet exemple, **bcbef25a-c4db-446b-9496-1b558d9edd0e** est l’ID de l’étiquette de la pièce jointe, et la règle s’applique aux fichiers. docx,. xlsx et. pptx.

Par défaut, les e-mails qui ont des pièces jointes étiquetées ne reçoivent pas automatiquement la même étiquette.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "EmailLabel",
                     "LabelId" : null           
        },
        {
          "type": "AttachmentLabel",
          "LabelId": "bcbef25a-c4db-446b-9496-1b558d9edd0e",
          "Extensions": [
                ".docx",
                ".xlsx",
                ".pptx"
             ]
        },
    {           
            "type" : "SentTo",              
            "Domains" : [               
                "contoso.com",              
            ]           
        },      
        {           
            "type" : "Warn" 
        }   
    ] 
}
```

#### <a name="example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option"></a>Exemple 5 : demander une justification, avec deux options prédéfinies et une option de texte libre supplémentaire

Le code **. JSON** suivant fait en sorte qu’Outlook invite l’utilisateur à justifier son action. Le texte de la justification comprend deux options prédéfinies, ainsi qu’une troisième option de texte libre.

Dans la mesure où aucune extension spécifique n’est spécifiée, tous les types de fichiers pris en charge sont inclus.

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                                  
                ]               
            }       
        },      
        {           
            "type" : "EmailLabel",          
            "LabelId" : "34b8beec-40df-4219-9dd4-553e1c8904c1"      
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                  
                    "Title": "Justification Required",                  
                    "Body": "Your organization policy requires justification for you to send content classified as <Bold> ${MatchedLabelName}</Bold>,to untrusted recipients:<br>Recipients are: ${MatchedRecipientsList}",                     
                    "Options": [                        
                        "I confirm the recipients are approved for sharing this content",                   
                        "My manager approved sharing of this content",                      
                        "Other, as explained"                   
                    ]               
                },              
                "es-es": {                  
                    "Title": "Justificación necesaria",                     
                    "Body": "La política de su organización requiere una justificación para que envíe contenido clasificado como <Bold> ${MatchedLabelName}</Bold> a destinatarios que no sean de confianza.",                  
                    "Options": [                        
                        "Confirmo que los destinatarios están aprobados para compartir este contenido.",
                        "Mi gerente aprobó compartir este contenido",
                        "Otro, como se explicó"                     
                    ]               
                }           
            },          
            "HasFreeTextOption":"true",             
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

## <a name="configure-sharepoint-timeouts"></a>Configurer des délais d’attente SharePoint

Par défaut, le délai d’attente pour les interactions SharePoint est de deux minutes, après quoi l’opération de tentative d’AIP échoue.

À partir de la [version 2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850), les administrateurs AIP peuvent contrôler ce délai d’attente à l’aide des propriétés avancées suivantes, à l’aide d’une syntaxe **hh : mm : SS** pour définir les délais d’attente :

- **SharepointWebRequestTimeout**. Détermine le délai d’expiration de toutes les requêtes Web AIP sur SharePoint. Valeur par défaut = 2 minutes.

    Par exemple, si votre stratégie est nommée **Global**, l’exemple de commande PowerShell suivant met à jour le délai d’expiration de la demande Web à 5 minutes.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointWebRequestTimeout="00:05:00"}
    ```

- **SharepointFileWebRequestTimeout**. Détermine le délai d’expiration spécifiquement pour les fichiers SharePoint par le biais de requêtes Web AIP. Valeur par défaut = 15 minutes

    Par exemple, si votre stratégie est nommée **Global**, l’exemple de commande PowerShell suivant met à jour le délai d’expiration de la demande Web de fichier à 10 minutes.

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointFileWebRequestTimeout="00:10:00"}
    ```

### <a name="avoid-scanner-timeouts-in-sharepoint"></a>Éviter les délais d’attente du scanneur dans SharePoint

Si vous avez des chemins d’accès de fichiers longs dans SharePoint version 2013 ou ultérieure, assurez-vous que la valeur [httpRuntime. maxUrlLength](/dotnet/api/system.web.configuration.httpruntimesection.maxurllength) de votre serveur SharePoint est supérieure aux 260 de caractères par défaut.

Cette valeur est définie dans la classe **HttpRuntimeSection** de la `ASP.NET` Configuration. 

**Pour mettre à jour la classe HttpRuntimeSection** : * *

1. Sauvegardez votre configuration de **web.config** . 

1. Mettez à jour la valeur **maxUrlLength** en fonction des besoins. Par exemple :

    ```c#
    <httpRuntime maxRequestLength="51200" requestValidationMode="2.0" maxUrlLength="5000"  />
    ```

1. Redémarrez votre serveur Web SharePoint et vérifiez qu’il se charge correctement. 

    Par exemple, dans le gestionnaire Windows Internet Information Server (IIS), sélectionnez votre site, puis sous **gérer le site Web**, sélectionnez **redémarrer**. 

## <a name="prevent-outlook-performance-issues-with-smime-emails"></a>Empêcher les problèmes de performances d’Outlook avec les e-mails S/MIME

Des problèmes de performances peuvent se produire dans Outlook lorsque les courriers électroniques S/MIME sont ouverts dans le volet de lecture. Pour éviter ces problèmes, activez la propriété avancée **OutlookSkipSmimeOnReadingPaneEnabled** . 

L’activation de cette propriété empêche l’affichage de la barre AIP et des classifications de courrier électronique dans le volet de lecture.

Par exemple, si votre stratégie est nommée **Global**, l’exemple de commande PowerShell suivant active la propriété **OutlookSkipSmimeOnReadingPaneEnabled** :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookSkipSmimeOnReadingPaneEnabled="true"}
```

## <a name="turn-off-document-tracking-features-public-preview"></a>Désactiver les fonctionnalités de suivi des documents (préversion publique)

Par défaut, les fonctionnalités de suivi des documents sont activées pour votre locataire. Pour les désactiver, par exemple pour les exigences de confidentialité dans votre organisation ou région, affectez la valeur **false** à **EnableTrackAndRevoke** .

Une fois désactivé, les données de suivi de document ne sont plus disponibles dans votre organisation et les utilisateurs ne voient plus l’option de menu [**révoquer**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) dans leurs applications Office.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **EnableTrackAndRevoke**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableTrackAndRevoke="False"}
```

Une fois cette valeur définie sur **false**, le suivi et la révocation sont désactivés comme suit : 

- L’ouverture de documents protégés avec le client d’étiquetage unifié AIP n’enregistre plus les documents pour le suivi et la révocation.
- Les utilisateurs finaux ne voient plus l’option de menu [**révoquer**](revoke-access-user.md#revoke-access-from-microsoft-office-apps) dans leurs applications Office.

Toutefois, les documents protégés qui sont déjà enregistrés pour le suivi continueront d’être suivis, et les administrateurs pourront tout de même révoquer l’accès à partir de PowerShell. Pour désactiver les fonctionnalités de suivi et de révocation complètes, exécutez également l’applet [de commande Disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) .

Cette configuration utilise un [paramètre avancé](#configuring-advanced-settings-for-the-client-via-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Security & Compliance Center PowerShell.

> [!NOTE]
> Pour activer le suivi et la révocation, affectez la valeur **true** à **EnableTrackAndRevoke** et exécutez également l’applet de commande [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature) .
>
## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez personnalisé le client d’étiquetage unifié Azure Information Protection, consultez les ressources suivantes pour obtenir des informations supplémentaires dont vous pouvez avoir besoin pour prendre en charge ce client :

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichiers pris en charge](clientv2-admin-guide-file-types.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)