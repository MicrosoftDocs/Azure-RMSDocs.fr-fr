---
title: Configurations personnalisées-Azure Information Protection client d’étiquetage unifié
description: Informations sur la personnalisation de l’Azure Information Protection client d’étiquetage unifié pour Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b18beab3c6a2dd3b01991fdb9755b943ec62fe5a
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117695"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations suivantes pour les configurations avancées dont vous pouvez avoir besoin pour des scénarios spécifiques ou un sous-ensemble d’utilisateurs lorsque vous gérez le client d’étiquetage unifié Azure Information Protection.

Ces paramètres requièrent la modification du registre ou la spécification de paramètres avancés. Les paramètres avancés utilisent [Office 365 Centre de sécurité et de conformité PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps).

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Comment configurer des paramètres avancés pour le client à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell

Quand vous utilisez Office 365 Centre de sécurité et de conformité PowerShell, vous pouvez configurer des paramètres avancés qui prennent en charge les personnalisations des étiquettes et des stratégies d’étiquette. Exemple :

- Le paramètre permettant d’afficher la barre d’Information Protection dans les applications Office est un ***paramètre avancé***de la stratégie d’étiquette.
- Le paramètre permettant de spécifier une couleur d’étiquette est un ***paramètre avancé d’étiquette***.

Dans les deux cas, une fois que vous êtes [connecté à Office 365 Centre de sécurité et de conformité PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps), spécifiez le paramètre *AdvancedSettings* avec l’identité (nom ou GUID) de la stratégie ou de l’étiquette, et spécifiez des paires clé/valeur dans une [table de hachage](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables). Utilisez la syntaxe suivante :

Pour un paramètre de stratégie étiquette, valeur de chaîne unique :

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

Pour les paramètres de stratégie d’étiquette, plusieurs valeurs de chaîne pour la même clé :

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Pour un paramètre d’étiquette, valeur de chaîne unique :

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

Pour les paramètres d’étiquette, plusieurs valeurs de chaîne pour la même clé :

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Pour supprimer un paramètre avancé, utilisez la même syntaxe, mais spécifiez une valeur de chaîne NULL.


#### <a name="examples-for-setting-advanced-settings"></a>Exemples de paramétrage des paramètres avancés

Exemple 1 : définir une stratégie d’étiquette paramètre avancé pour une valeur de chaîne unique :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

Exemple 2 : définir un paramètre avancé pour une étiquette pour une valeur de chaîne unique :

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

Exemple 3 : définir un paramètre avancé pour les étiquettes pour plusieurs valeurs de chaîne :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

Exemple 4 : supprimer un paramètre avancé de stratégie d’étiquette en spécifiant une valeur de chaîne NULL :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>Spécification de l’identité de la stratégie ou de l’étiquette de l’étiquette

La spécification du nom de la stratégie d’étiquette pour le paramètre d' *identité* PowerShell est simple, car vous ne voyez qu’un seul nom de stratégie dans le centre d’administration où vous gérez vos stratégies d’étiquette. Toutefois, pour les étiquettes, vous voyez un **nom** et un **nom d’affichage** dans les centres d’administration. Dans certains cas, la valeur est la même, mais elle peut être différente :

- **Nom** est le nom d’origine de l’étiquette et il est unique pour toutes vos étiquettes. Si vous modifiez le nom de votre étiquette après sa création, cette valeur reste la même. Pour les étiquettes qui ont été migrées à partir de Azure Information Protection, vous pouvez voir l’ID d’étiquette de l’étiquette à partir du Portail Azure.

- **Nom complet** est le nom de l’étiquette que les utilisateurs voient, et il n’est pas nécessaire qu’il soit unique sur toutes vos étiquettes. Par exemple, les utilisateurs voient une sous-étiquette **tous les employés** pour l’étiquette **confidentiel** et une autre sous-étiquette **tous les employés** pour l’étiquette **hautement confidentiel** . Ces sous-étiquettes affichent le même nom, mais elles ne sont pas de la même étiquette et présentent des paramètres différents.

Pour configurer les paramètres avancés des étiquettes, utilisez la valeur **nom** . Par exemple, pour identifier l’étiquette dans l’image suivante, vous devez spécifier `-Identity "All Company"`:

![Utiliser’name’plutôt que’Display Name’pour identifier une étiquette de sensibilité](../media/labelname_scc.png)

Si vous préférez spécifier le GUID de l’étiquette, cette valeur n’est pas affichée dans le centre d’administration où vous gérez vos étiquettes. Toutefois, vous pouvez utiliser la commande Office 365 Centre de sécurité et de conformité PowerShell suivante pour rechercher cette valeur :

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordre de priorité-mode de résolution des paramètres en conflit

À l’aide de l’un des centres d’administration où vous gérez vos étiquettes de sensibilité, vous pouvez configurer les paramètres de stratégie d’étiquette suivants :

- **Appliquer cette étiquette par défaut aux documents et aux e-mails**

- **Les utilisateurs doivent fournir une justification pour supprimer une étiquette ou une étiquette de classification inférieure**

- **Demander aux utilisateurs d’appliquer une étiquette à leur adresse de messagerie ou à leur document**

- **Fournir aux utilisateurs un lien vers une page d’aide personnalisée**

Lorsque plusieurs stratégies d’étiquette sont configurées pour un utilisateur, chacune avec des paramètres de stratégie potentiellement différents, le dernier paramètre de stratégie est appliqué en fonction de l’ordre des stratégies dans le centre d’administration. Pour plus d’informations, consultez priorité de la [stratégie d’étiquette (ordre important)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters) .

Les paramètres avancés des étiquettes suivent la même logique pour la précédence : lorsqu’une étiquette est dans plusieurs stratégies d’étiquette et que cette étiquette a des paramètres avancés, le dernier paramètre avancé est appliqué en fonction de l’ordre des stratégies dans le centre d’administration.

Les paramètres avancés de la stratégie d’étiquette sont appliqués dans l’ordre inverse : à une exception près, les paramètres avancés de la première stratégie sont appliqués, en fonction de l’ordre des stratégies dans le centre d’administration. L’exception est le paramètre avancé *OutlookDefaultLabel*, qui définit une autre étiquette par défaut pour Outlook. Pour ce paramètre avancé de stratégie d’étiquette uniquement, le dernier paramètre est appliqué en fonction de l’ordre des stratégies dans le centre d’administration.

#### <a name="available-advanced-settings-for-label-policies"></a>Paramètres avancés disponibles pour les stratégies d’étiquette

Utilisez le paramètre *AdvancedSettings* avec [New-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-labelpolicy?view=exchange-ps) et [Set-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps).

|Paramètre|Scénario et instructions|
|----------------|---------------|
|AttachmentAction|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[Exempter les messages Outlook de l’étiquetage obligatoire](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[Désactiver l’envoi de données d’audit à Azure Information Protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableCustomPermissions|[Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault|[Afficher la barre Information Protection dans les applications Office](#display-the-information-protection-bar-in-office-apps)|
|LogMatchedContent|[Envoyer les correspondances de type d’informations à Azure Information Protection Analytics](#send-information-type-matches-to-azure-information-protection-analytics)|
|OutlookBlockTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Définir une autre étiquette par défaut pour Outlook](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Activer la classification recommandée dans Outlook](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PFileSupportedExtensions|[Changer les types de fichiers à protéger](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[Supprimer « Pas maintenant » pour les documents quand l’étiquetage obligatoire est utilisé](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Ajouter « Signaler un problème » pour les utilisateurs](#add-report-an-issue-for-users)|
|RunAuditInformationTypesDiscovery|[Désactiver l’envoi d’informations sensibles découvertes dans des documents à Azure Information Protection Analytics](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|ScannerConcurrencyLevel|[Limiter le nombre de threads utilisés par le scanneur](#limit-the-number-of-threads-used-by-the-scanner)|

Exemple de commande PowerShell pour vérifier les paramètres de stratégie d’étiquette en vigueur pour une stratégie d’étiquette nommée « global » :

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>Paramètres avancés disponibles pour les étiquettes

Utilisez le paramètre *AdvancedSettings* avec [New-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) et [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

|Paramètre|Scénario et instructions|
|----------------|---------------|
|couleur|[Spécifier une couleur pour l’étiquette](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[Spécifier une sous-étiquette par défaut pour une étiquette parent](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|

Exemple de commande PowerShell pour vérifier les paramètres de votre étiquette en vigueur pour une étiquette nommée « public » :

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Afficher la barre Information Protection dans les applications Office

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, les utilisateurs doivent sélectionner l’option **afficher la barre** à partir du bouton **sensibilité** pour afficher la barre de information protection dans les applications Office. Utilisez la clé **HideBarByDefault** et définissez la valeur sur **false** pour afficher automatiquement cette barre pour les utilisateurs afin qu’ils puissent sélectionner des étiquettes à partir de la barre ou du bouton. 

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **HideBarByDefault**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>Exempter les messages Outlook de l’étiquetage obligatoire

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, lorsque vous activez le paramètre de stratégie étiquette **tous les documents et e-mails doivent avoir une étiquette**, tous les documents enregistrés et les e-mails envoyés doivent avoir une étiquette appliquée. Quand vous configurez le paramètre avancé suivant, le paramètre de stratégie s’applique uniquement aux documents Office et non aux messages Outlook.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **DisableMandatoryInOutlook**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}

## <a name="enable-recommended-classification-in-outlook"></a>Activer la classification recommandée dans Outlook

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous configurez une étiquette pour la classification recommandée, les utilisateurs sont invités à accepter ou ignorer l’étiquette recommandée dans Word, Excel et PowerPoint. Ce paramètre affiche également cette recommandation d’étiquette dans Outlook.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookRecommendationEnabled**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Définir une autre étiquette par défaut pour Outlook

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous configurez ce paramètre, Outlook n’applique pas l’étiquette par défaut qui est configurée en tant que paramètre de stratégie pour l’option **appliquer cette étiquette par défaut aux documents et aux e-mails**. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookDefaultLabel**

- Valeur : \<**GUID**de l’étiquette > ou **aucun**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}

## <a name="change-which-file-types-to-protect"></a>Changer les types de fichiers à protéger

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, le Azure Information Protection client d’étiquetage unifié protège tous les types de fichiers, et le scanneur du client protège uniquement les types de fichiers Office et les fichiers PDF.

Vous pouvez modifier ce comportement par défaut pour une stratégie d’étiquette sélectionnée, en spécifiant les éléments suivants :

- Clé : **PFileSupportedExtensions**

- Valeur : **<string value>** 

Utilisez le tableau suivant pour identifier la valeur de chaîne à spécifier :

| Valeur chaîne| Client| Scanner|
|-------------|-------|--------|
|\*|Valeur par défaut : appliquer la protection à tous les types de fichiers|Appliquer la protection à tous les types de fichiers|
|\<valeur null >| Appliquer la protection aux types de fichiers Office et aux fichiers PDF| Valeur par défaut : appliquer la protection aux types de fichiers Office et aux fichiers PDF|
|ConvertTo-JSON (". jpg", ". png")|En plus des fichiers PDF et des types de fichiers Office, appliquer la protection aux extensions de nom de fichier spécifiées | En plus des fichiers PDF et des types de fichiers Office, appliquer la protection aux extensions de nom de fichier spécifiées

Exemple 1 : commande PowerShell pour le client unifié pour protéger uniquement les types de fichiers Office et les fichiers PDF, où votre stratégie d’étiquette est nommée « client » :

    Set-LabelPolicy -Identity Client -AdvancedSettings @{PFileSupportedExtensions=""}

Exemple 2 : commande PowerShell pour le scanneur afin de protéger tous les types de fichiers, où votre stratégie d’étiquette est nommée « scanner » :

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

Exemple 3 : commande PowerShell pour le scanneur afin de protéger les fichiers. txt et. csv en plus des fichiers Office et des fichiers PDF, où votre stratégie d’étiquette est nommée « scanner » :

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}

Ce paramètre vous permet de modifier les types de fichiers protégés, mais vous ne pouvez pas modifier le niveau de protection par défaut de natif à générique. Par exemple, pour les utilisateurs qui exécutent le client d’étiquetage unifié, vous pouvez modifier le paramètre par défaut afin que seuls les fichiers Office et PDF soient protégés au lieu de tous les types de fichiers. Toutefois, vous ne pouvez pas modifier ces types de fichiers pour qu’ils soient protégés de manière générique avec l’extension de nom de fichier. pfile.

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Supprimer « Pas maintenant » pour les documents quand vous utilisez l’étiquetage obligatoire

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous utilisez le paramètre de stratégie étiquette de **tous les documents et e-mails doit avoir une étiquette**, les utilisateurs sont invités à sélectionner une étiquette lorsqu’ils enregistrent un document Office pour la première fois et lorsqu’ils envoient un message électronique. Pour les documents, les utilisateurs peuvent sélectionner **Pas maintenant** pour ignorer temporairement l’invite à sélectionner une étiquette et revenir au document. En revanche, ils ne peuvent pas fermer le document enregistré sans l’étiqueter. 

Quand vous configurez ce paramètre, l’option **Pas maintenant** n’est pas proposée, et les utilisateurs sont obligés de sélectionner une étiquette au premier enregistrement du document.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **PostponeMandatoryBeforeSave**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage

Cette configuration utilise des [Paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Il existe deux méthodes qui peuvent être utilisées pour supprimer des classifications d’autres solutions d’étiquetage. La première méthode supprime toute forme de documents Word où le nom de forme correspond au nom défini dans la propriété avancée **WordShapeNameToRemove**, la deuxième méthode vous permet de supprimer ou de remplacer des en-têtes ou des pieds de page textuels à partir de documents Word, Excel et PowerPoint, comme défini dans la propriété avancée **RemoveExternalContentMarkingInApp** . 

### <a name="use-the-wordshapenametoremove-advanced-property-preview"></a>Utiliser la propriété avancée WordShapeNameToRemove (version préliminaire)

*La propriété avancée **WordShapeNameToRemove** est prise en charge à partir de la version 2.6.101.0 et supérieure*

Ce paramètre vous permet de supprimer ou de remplacer des étiquettes basées sur des formes de documents Word lorsque ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, la forme contient le nom d’une ancienne étiquette que vous avez maintenant migrée vers des étiquettes de sensibilité pour utiliser un nouveau nom d’étiquette et sa propre forme.

Pour utiliser cette propriété avancée, vous devez rechercher le nom de la forme dans le document Word, puis les définir dans la liste de propriétés avancées **WordShapeNameToRemove** des formes. Le service supprime toutes les formes dans Word qui commencent par un nom défini dans la liste des formes de cette propriété avancée.

Évitez de supprimer les formes qui contiennent le texte que vous souhaitez ignorer, en définissant le nom de toutes les formes à supprimer et évitez de vérifier le texte dans toutes les formes, ce qui est un processus gourmand en ressources.

Si vous ne spécifiez pas de formes de mot dans ce paramètre de propriété avancé supplémentaire et que Word est inclus dans la valeur de clé **RemoveExternalContentMarkingInApp** , le texte que vous spécifiez dans la valeur **ExternalContentMarkingToRemove** est recherché dans toutes les formes. 

Pour rechercher le nom de la forme que vous utilisez et souhaitez exclure :

1. Dans Word, affichez le volet de **sélection** : onglet dossier de **démarrage** > groupe **édition** > **Sélectionnez** l’option > **volet sélection**.

2. Sélectionnez la forme sur la page que vous souhaitez marquer pour suppression. Le nom de la forme que vous marquez est maintenant mis en surbrillance dans le volet de **sélection** .

Utilisez le nom de la forme pour spécifier une valeur de chaîne pour la clé * * * * WordShapeNameToRemove * * * *. 

Exemple : le nom de la forme est **DC**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `dc`.

- Clé : **WordShapeNameToRemove**

- Valeur : \<**nom** de la forme de mot> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}

Lorsque vous avez plusieurs formes de mot à supprimer, spécifiez autant de valeurs que vous avez de formes à supprimer.


### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>Utiliser la propriété avancée RemoveExternalContentMarkingInApp
Ce paramètre vous permet de supprimer ou de remplacer des en-têtes ou des pieds de page textuels dans des documents lorsque ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, l’ancien pied de page contient le nom d’une ancienne étiquette que vous avez maintenant migrée vers des étiquettes de sensibilité pour utiliser un nouveau nom d’étiquette et son propre pied de page.

Lorsque le client d’étiquetage unifié obtient cette configuration dans sa stratégie, les anciens en-têtes et pieds de page sont supprimés ou remplacés lorsque le document est ouvert dans l’application Office et toute étiquette de sensibilité est appliquée au document.

Cette configuration n’est pas prise en charge pour Outlook. Sachez également que quand vous l’utilisez avec Word, Excel et PowerPoint, elle peut affecter négativement les performances de ces applications pour les utilisateurs. La configuration vous permet de définir des paramètres par application, par exemple, rechercher du texte dans les en-têtes et les pieds de page des documents Word, mais pas dans les feuilles de calcul Excel ni dans les présentations PowerPoint.

Étant donné que les critères spéciaux affectent les performances pour les utilisateurs, nous vous recommandons de limiter les types d’applications Office (**W**ORD, E**X**cel, **P**owerPoint) à ceux qui doivent être recherchés.

Pour la stratégie d’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **RemoveExternalContentMarkingInApp**

- Valeur : \<**Types d’application Office WXP**> 

Exemples :

- Pour rechercher dans des documents Word uniquement, spécifiez **W**.

- Pour rechercher dans des documents Word et des présentations PowerPoint, spécifiez **WP**.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

Ensuite, vous avez besoin d’au moins un paramètre client avancé de plus, **ExternalContentMarkingToRemove**, pour spécifier le contenu de l’en-tête ou du pied de page et comment les supprimer ou les remplacer.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Comment configurer ExternalContentMarkingToRemove

Lorsque vous spécifiez la valeur de chaîne pour la clé **ExternalContentMarkingToRemove**, vous disposez de trois options qui utilisent des expressions régulières :

- Correspondance partielle pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXTE À SUPPRIMER**. Vous souhaitez entièrement supprimer ces en-têtes ou pieds de page. Spécifiez la valeur : `*TEXT*`.

- Correspondance totale pour juste supprimer des mots spécifiques dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXTE À SUPPRIMER**. Vous souhaitez supprimer le mot **TEXTE** uniquement, ce qui laisse la chaîne d’en-tête ou de pied de page avec **À SUPPRIMER**. Spécifiez la valeur : `TEXT `.

- Correspondance totale pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page ont la chaîne **TEXTE À SUPPRIMER**. Vous voulez supprimer les en-têtes ou les pieds de page qui ont exactement cette chaîne. Spécifiez la valeur : `^TEXT TO REMOVE$`.
    

Les caractères génériques de la chaîne que vous spécifiez sont sensibles à la casse. La longueur maximale de la chaîne est de 255 caractères.

Étant donné que des documents peuvent contenir des caractères invisibles ou différents types d’espaces ou des tabulations, la chaîne que vous spécifiez pour une expression ou une phrase peut ne pas être détectée. Si possible, spécifiez un seul mot distinctif pour la valeur et veillez à tester les résultats avant de procéder au déploiement en production.

Pour la même stratégie d’étiquette, spécifiez les chaînes suivantes :

- Clé : **ExternalContentMarkingToRemove**

- Valeur : \<**chaîne à trouver, définie comme expression régulière**> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>En-têtes ou pieds de page multilignes

Si un texte d’en-tête ou de pied de page prend plus d’une ligne, créez une clé et une valeur pour chaque ligne. Par exemple, vous avez le pied de page suivant sur deux lignes :

**Le fichier est classé confidentiel**

**Étiquette appliquée manuellement**

Pour supprimer ce pied de page multiligne, vous créez les deux entrées suivantes pour la même stratégie d’étiquette :

- Clé : **ExternalContentMarkingToRemove**

- Valeur de la clé 1 : **\*Confidentiel***

- Valeur de la clé 2 : **\*Étiquette appliquée*** 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>Optimisation pour PowerPoint

Les pieds de page dans PowerPoint sont implémentés en tant que formes. Pour éviter de supprimer les formes qui contiennent le texte que vous avez spécifié, mais qui ne sont ni des en-têtes ni des pieds de page, utilisez un paramètre client avancé supplémentaire nommé **PowerPointShapeNameToRemove**. Nous recommandons également d’utiliser ce paramètre pour éviter de vérifier le texte dans toutes les formes, qui est un processus gourmand en ressources.

Si vous ne spécifiez pas ce paramètre client avancé supplémentaire et si PowerPoint est inclus dans la valeur de la clé **RemoveExternalContentMarkingInApp**, toutes les formes sont vérifiées à la recherche du texte que vous spécifiez dans la valeur  **ExternalContentMarkingToRemove**. 

Pour rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page :

1. Dans PowerPoint, affichez le volet **Sélection** : onglet **Mise en forme** > groupe **Organiser** > **volet sélection**.

2. Sélectionnez la forme sur la diapositive qui contient votre en-tête ou votre pied de page. Le nom de la forme sélectionnée est maintenant en surbrillance dans le volet **Sélection**.

Utilisez le nom de la forme afin de spécifier une valeur de chaîne pour la clé **PowerPointShapeNameToRemove**. 

Exemple : Le nom de la forme est **fc**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `fc`.

- Clé : **PowerPointShapeNameToRemove**

- Valeur : \<**Nom de la forme PowerPoint**> 

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

Lorsque vous avez plusieurs formes PowerPoint à supprimer, spécifiez autant de valeurs que vous le souhaitez pour les formes à supprimer.

Par défaut, seuls les en-têtes et les pieds de page qui se trouvent dans les diapositives principales sont recherchés. Pour étendre cette recherche à toutes les diapositives, processus beaucoup plus gourmand en ressources, utilisez un paramètre client avancé supplémentaire nommé **RemoveExternalContentMarkingInAllSlides**:

- Clé : **RemoveExternalContentMarkingInAllSlides**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>Désactiver les autorisations personnalisées dans l’Explorateur de fichiers

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, les utilisateurs voient une option nommée **protéger avec des autorisations personnalisées** lorsqu’ils cliquent avec le bouton droit dans l’Explorateur de fichiers et choisissent **classer et protéger**. Cette option permet de définir leurs propres paramètres de protection qui peuvent remplacer tous les paramètres de protection que vous pouvez avoir inclus dans une configuration d’étiquette. Les utilisateurs peuvent voir également une option pour supprimer la protection. Quand vous configurez ce paramètre, les utilisateurs ne voient pas ces options.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableCustomPermissions**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées aux utilisateurs dans l’Explorateur de fichiers

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous configurez le paramètre client avancé pour [Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer), par défaut, les utilisateurs ne sont pas en mesure d’afficher ou de modifier les autorisations personnalisées qui sont déjà définies dans un document protégé.

Toutefois, il existe un autre paramètre de client avancé que vous pouvez spécifier afin que dans ce scénario, les utilisateurs puissent afficher et modifier des autorisations personnalisées pour un document protégé lorsqu’ils utilisent l’Explorateur de fichiers et cliquer avec le bouton droit sur le fichier.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableCustomPermissionsForCustomProtectedFiles**

- Valeur : **True**

Exemple de commande PowerShell :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes

Cette configuration utilise des [Paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Ce paramètre est destiné aux utilisateurs qui joignent des documents étiquetés à un courrier électronique et n’étiquettent pas le message électronique lui-même. Dans ce scénario, une étiquette est automatiquement sélectionnée pour eux, en fonction des étiquettes de classification appliquées aux pièces jointes. L’étiquette classification la plus élevée est sélectionnée.

La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur SharePoint ou OneDrive Entreprise).

Vous pouvez configurer ce paramètre sur **recommandé**, afin que les utilisateurs soient invités à appliquer l’étiquette sélectionnée à leur message électronique, avec une info-bulle personnalisable. Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Ou bien, vous pouvez configurer ce paramètre sur **automatique**, où l’étiquette sélectionnée est automatiquement appliquée, mais les utilisateurs peuvent supprimer l’étiquette ou sélectionner une autre étiquette avant d’envoyer l’e-mail.

Remarque : lorsque la pièce jointe avec l’étiquette de classification la plus élevée est configurée pour la protection avec le paramètre des autorisations définies par l’utilisateur :

- Lorsque les autorisations définies par l’utilisateur de l’étiquette sont Outlook (ne pas transférer), cette étiquette est sélectionnée et le fait de ne pas transférer la protection est appliqué à l’e-mail.
- Lorsque les autorisations définies par l’utilisateur de l’étiquette sont uniquement pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette n’est pas appliquée au message électronique et aucune n’est la protection.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé 1 : **AttachmentAction**

- Valeur de clé 1 : **recommandé** ou **automatique**

- Clé 2 : **AttachmentActionTip**

- Valeur de clé 2 : «\<info-bulle personnalisée > »

L’info-bulle personnalisée ne prend en charge qu’une seule langue.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>Ajouter « Signaler un problème » pour les utilisateurs

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous spécifiez le paramètre client avancé suivant, les utilisateurs voient une option **Signaler un problème** qu’ils peuvent sélectionner dans la boîte de dialogue **Aide et commentaires** du client. Spécifiez une chaîne HTTP pour le lien. (par exemple, une page web personnalisée permettant aux utilisateurs de signaler des problèmes, ou une adresse e-mail qui pointe vers votre support technique). 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **ReportAnIssueLink**

- Valeur : **\<chaîne HTTP >**

Exemple de valeur pour un site web : `https://support.contoso.com`

Exemple de valeur pour une adresse e-mail : `mailto:helpdesk@contoso.com`

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails

Cette configuration utilise des [Paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Quand vous créez et que vous configurez les paramètres client avancés suivants, les utilisateurs voient des messages contextuels dans Outlook qui peuvent les avertir avant d’envoyer un e-mail, leur demander de justifier la raison pour laquelle ils envoient un e-mail ou les empêcher d’envoyer un e-mail pour un des scénarios suivants :

- **Leur e-mail ou la pièce jointe à leur e-mail a une étiquette spécifique** :
    - La pièce jointe peut être n’importe quel type de fichier

- **Leur e-mail ou leur pièce jointe à l’e-mail n’a pas d’étiquette** :
    - La pièce jointe peut être un document Office ou un document PDF

Lorsque ces conditions sont remplies, l’utilisateur voit un message contextuel avec l’une des actions suivantes :

- **WARN**: l’utilisateur peut confirmer et envoyer, ou annuler.

- **Justify**: l’utilisateur est invité à fournir une justification (options prédéfinies ou forme libre).  L’utilisateur peut ensuite envoyer ou annuler l’e-mail. Le texte de la justification est écrit dans l’en-tête X de l’e-mail afin qu’il puisse être lu par d’autres systèmes, par exemple des services de protection contre la perte de données.

- **Bloquer**: l’utilisateur ne peut pas envoyer l’e-mail tant que la condition est conservée. Le message contient la raison du blocage de l’e-mail pour que l’utilisateur puisse résoudre le problème, par exemple supprimer des destinataires spécifiques ou appliquer une étiquette à l’e-mail. 

Quand les messages contextuels concernent une étiquette spécifique, vous pouvez configurer des exceptions pour les destinataires par nom de domaine.

> [!TIP]
> Pour obtenir un exemple de procédure pas à pas de configuration de ces paramètres, consultez la vidéo [Azure information protection configuration contextuelle Outlook](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) .

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Pour implémenter des messages d’avertissement, de justification ou de blocage pour des étiquettes spécifiques :

Pour la stratégie sélectionnée, créez un ou plusieurs des paramètres avancés suivants avec les clés suivantes. Pour les valeurs, spécifiez une ou plusieurs étiquettes par leur GUID, chacune séparée par une virgule.

Exemple de valeur pour plusieurs GUID d’étiquette sous la forme d’une chaîne séparée par des virgules : `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messages d’avertissement :
    
    - Clé : **OutlookWarnUntrustedCollaborationLabel**
    
    - Valeur : \<**GUID des étiquettes, séparés par des virgules**>

- Messages de justification :
    
    - Clé : **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valeur : \<**GUID des étiquettes, séparés par des virgules**>

- Messages de blocage :
    
    - Clé : **OutlookBlockUntrustedCollaborationLabel**
    
    - Valeur : \<**GUID des étiquettes, séparés par des virgules**>


Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>Pour exempter les noms de domaine pour les messages contextuels configurés pour des étiquettes spécifiques

Pour les étiquettes que vous avez spécifiées avec ces messages contextuels, vous pouvez exempter des noms de domaine spécifiques afin que les utilisateurs ne voient pas les messages pour les destinataires qui ont ce nom de domaine inclus dans leur adresse de messagerie. Dans ce cas, les e-mails sont envoyés sans qu’un message interrompe le processus. Pour spécifier plusieurs domaines, ajoutez-les sous la forme d’une seule chaîne, en les séparant par des virgules.

Une configuration typique consiste à afficher les messages contextuels seulement pour les destinataires qui sont externes à votre organisation ou qui ne sont pas des partenaires autorisés de votre organisation. Dans ce cas, vous spécifiez tous les domaines de messagerie utilisés par votre organisation et par vos partenaires.

Pour la même stratégie d’étiquette, créez les paramètres client avancés suivants et, pour la valeur, spécifiez un ou plusieurs domaines, chacun étant séparé par une virgule.

Exemple de valeur pour plusieurs domaines sous forme de chaîne séparée par des virgules : `contoso.com,fabrikam.com,litware.com`

- Messages d’avertissement :
    
    - Clé : **OutlookWarnTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

- Messages de justification :
    
    - Clé : **OutlookJustifyTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

- Messages de blocage :
    
    - Clé : **OutlookBlockTrustedDomains**
    
    - Valeur : **\<** noms de domaine, séparés par des virgules **>**

Par exemple, vous avez spécifié le paramètre client avancé **OutlookBlockUntrustedCollaborationLabel** pour l’étiquette **confidentiel \ tous les employés** . Vous spécifiez maintenant le paramètre de client avancé supplémentaire **OutlookJustifyTrustedDomains** et **contoso.com**. Par conséquent, un utilisateur peut envoyer un e-mail à john@sales.contoso.com lorsqu’il est étiqueté **confidentiel \ tous les employés** , mais qu’il ne peut pas envoyer un e-mail avec la même étiquette à un compte gmail.

Exemples de commandes PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Pour implémenter des messages contextuels d’avertissement, de justification ou de blocage pour des e-mails ou des pièces jointes qui n’ont pas d’étiquette :

Pour la même stratégie d’étiquette, créez le paramètre de client avancé suivant avec l’une des valeurs suivantes :

- Messages d’avertissement :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **avertir**

- Messages de justification :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **justifier**

- Messages de blocage :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **bloquer**

- Désactiver ces messages :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Valeur : **désactivé**


Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Pour définir des extensions de nom de fichier spécifiques pour les messages contextuels avertir, justifier ou bloquer pour les pièces jointes qui n’ont pas d’étiquette

Par défaut, les messages contextuels avertir, justifier ou bloquer s’appliquent à tous les documents Office et documents PDF. Vous pouvez affiner cette liste en spécifiant les extensions de nom de fichier qui doivent afficher les messages d’avertissement, justifier ou bloquer avec un paramètre avancé supplémentaire et une liste séparée par des virgules des extensions de nom de fichier.

Exemple de valeur pour plusieurs extensions de nom de fichier à définir en tant que chaîne séparée par des virgules : `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

Dans cet exemple, un document PDF sans étiquette n’a pas pour effet d’avertir, de justifier ou de bloquer les messages contextuels.

Pour la même stratégie d’étiquette, entrez les chaînes suivantes : 


- Clé : **OutlookOverrideUnlabeledCollaborationExtensions**

- Valeur : **\<** des extensions de nom de fichier pour afficher des messages, séparés par des virgules **>**


Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>Pour spécifier une action différente pour les messages électroniques sans pièces jointes

Par défaut, la valeur que vous spécifiez pour OutlookUnlabeledCollaborationAction pour avertir, justifier ou bloquer les messages contextuels s’applique aux e-mails ou pièces jointes qui n’ont pas d’étiquette. Vous pouvez affiner cette configuration en spécifiant un autre paramètre avancé pour les messages électroniques qui n’ont pas de pièces jointes.

Créez le paramètre client avancé suivant avec une des valeurs suivantes :

- Messages d’avertissement :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **avertir**

- Messages de justification :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **justifier**

- Messages de blocage :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **bloquer**

- Désactiver ces messages :
    
    - Clé : **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - Valeur : **désactivé**

Si vous ne spécifiez pas ce paramètre client, la valeur que vous spécifiez pour OutlookUnlabeledCollaborationAction est utilisée pour les messages électroniques sans étiquette, et les messages électroniques sans étiquette avec pièces jointes.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Désactiver l’envoi de données d’audit à Azure Information Protection Analytics

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Le client d’étiquetage unifié Azure Information Protection prend en charge la création de rapports centraux et, par défaut, envoie ses données d’audit à [Azure information protection Analytics](../reports-aip.md). Pour plus d’informations sur les informations qui sont envoyées et stockées, consultez la section [informations recueillies et envoyées à Microsoft](../reports-aip.md#information-collected-and-sent-to-microsoft) dans la documentation du centre de création de rapports.

Pour modifier ce comportement afin que ces informations ne soient pas envoyées par le client d’étiquetage unifié, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableAudit**

- Valeur : **False**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}


## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Désactiver l’envoi d’informations sensibles découvertes dans des documents à Azure Information Protection Analytics

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Lorsque le client d’étiquetage unifié Azure Information Protection est utilisé dans les applications Office, il recherche des informations sensibles dans les documents lorsqu’ils sont enregistrés pour la première fois. Si le paramètre avancé [EnableAudit](#disable-sending-audit-data-to-azure-information-protection-analytics) n’est pas défini sur **false**, tous les types d’informations sensibles prédéfinis et personnalisés détectés sont ensuite envoyés à [Azure information protection Analytics](../reports-aip.md).

Pour modifier ce comportement afin que les types d’informations sensibles détectés par le client d’étiquetage unifié ne soient pas envoyés, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **RunAuditInformationTypesDiscovery**

- Valeur : **False**

Si vous définissez ce paramètre de client avancé, les informations d’audit peuvent toujours être envoyées à partir du client, mais les informations sont limitées à la création de rapports lorsqu’un utilisateur a accédé au contenu étiqueté.

Exemple :

- Avec ce paramètre, vous pouvez voir qu’un utilisateur a accédé à Financial. docx qui est étiqueté **confidentiel \ Sales**.

- Sans ce paramètre, vous pouvez voir que Financial. docx contient 6 numéros de carte de crédit.
    
    - Si vous activez également [Correspondances de contenu pour approfondir l’analyse](../reports-aip.md#content-matches-for-deeper-analysis), vous pourrez en plus voir quels sont ces numéros de carte de crédit.

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypesDiscovery="False"}

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>Envoyer les correspondances de type d’informations à Azure Information Protection Analytics
 
Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, le client d’étiquetage unifié n’envoie pas de correspondances de contenu pour les types d’informations sensibles à [Azure information protection Analytics](../reports-aip.md). Pour plus d’informations sur ces informations supplémentaires qui peuvent être envoyées, consultez la section [correspondances de contenu pour une analyse plus poussée](../reports-aip.md#content-matches-for-deeper-analysis) dans la documentation du centre de création de rapports.

Pour envoyer des correspondances de contenu lors de l’envoi de types d’informations sensibles, créez le paramètre de client avancé suivant dans une stratégie d’étiquette : 

- Clé : **LogMatchedContent**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>Limiter le nombre de threads utilisés par le scanneur

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) de stratégie que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Par défaut, le scanneur utilise toutes les ressources du processeur disponibles sur l’ordinateur exécutant le service du scanneur. Si vous devez limiter la consommation du processeur pendant l’analyse de ce service, créez le paramètre avancé suivant dans une stratégie d’étiquette. 

Pour la valeur, spécifiez le nombre de threads simultanés que le scanneur peut exécuter en parallèle. Comme le scanneur utilise un thread distinct pour chaque fichier qu’il analyse, cette configuration de limitation définit donc le nombre de fichiers pouvant être analysés en parallèle. 

Lorsque vous configurez tout d’abord la valeur pour le test, nous vous recommandons de spécifier 2 par cœur, puis de surveiller les résultats. Par exemple, si vous exécutez le scanneur sur un ordinateur disposant de 4 cœurs, définissez tout d’abord la valeur 8. Si nécessaire, augmentez ou diminuez ce nombre, selon les performances qui vous sont nécessaires pour l’ordinateur du scanneur et votre fréquence d’analyse. 

- Clé : **ScannerConcurrencyLevel**

- Valeur : **\<nombre maximal de threads simultanés**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « scanner » :

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}


## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migrer des étiquettes de Secure Islands et d’autres solutions d’étiquetage

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Cette configuration n’est pas compatible avec les fichiers PDF protégés qui ont une extension de nom de fichier. ppdf. Ces fichiers ne peuvent pas être ouverts par le client à l’aide de l’Explorateur de fichiers ou de PowerShell.

Pour les documents Office étiquetés par des îlots sécurisés, vous pouvez réétiqueter ces documents avec une étiquette de sensibilité à l’aide d’un mappage que vous définissez. Cette méthode permet également de réutiliser les étiquettes d’autres solutions qui se trouvent sur des documents Office. 

À la suite de cette option de configuration, la nouvelle étiquette de sensibilité est appliquée par le client d’étiquetage unifié Azure Information Protection comme suit :

- Pour les documents Office : lorsque le document est ouvert dans l’application de bureau, la nouvelle étiquette de sensibilité est indiquée comme définie et appliquée lorsque le document est enregistré.

- Pour PowerShell : [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) peuvent appliquer la nouvelle étiquette de sensibilité.

- Pour l’Explorateur de fichiers : dans la boîte de dialogue Azure Information Protection, la nouvelle étiquette de sensibilité est affichée, mais n’est pas définie.

Cette configuration nécessite que vous spécifiiez un paramètre avancé nommé **labelByCustomProperties** pour chaque étiquette de sensibilité que vous souhaitez mapper à l’ancienne étiquette. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Spécifiez votre choix d’un nom de règle de migration. Utilisez un nom descriptif qui vous aide à identifier la manière dont une ou plusieurs étiquettes de votre solution d’étiquetage précédente doivent être mappées à l’étiquette de sensibilité.

Notez que ce paramètre ne supprime pas l’étiquette d’origine du document ni les marquages visuels du document que l’étiquette d’origine a éventuellement appliqués. Pour supprimer des en-têtes et des pieds de page, consultez la section précédente, [Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions).

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Exemple 1 : mappage du même nom d’étiquette

Exigence : les documents qui ont une étiquette des îlots sécurisés « confidentiel » doivent être réétiquetés comme « confidentiels » par Azure Information Protection.

Exemple :

- L’étiquette Secure Islands s’appelle **Confidentiel** et est stockée dans la propriété personnalisée nommée **Classification**.

Paramètre avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés est confidentielle, classification, confidentiel**

Exemple de commande PowerShell, où votre étiquette est nommée « Confidential » :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Exemple 2 : un mappage pour un autre nom d’étiquette

Exigence : les documents intitulés « sensibles » par les îles sécurisées doivent être renommés comme « hautement confidentiels » par Azure Information Protection.

Exemple :

- L’étiquette Secure Islands s’appelle **Sensible** et est stockée dans la propriété personnalisée nommée **Classification**.

Paramètre avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés est sensible, classification, sensible**

Exemple de commande PowerShell, où votre étiquette est nommée « hautement confidentiel » :

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Exemple 3 : mappage de plusieurs noms d’étiquettes en un

Exigence : vous avez deux étiquettes de îles sécurisées qui incluent le mot « Internal » et vous souhaitez que les documents qui ont l’une de ces étiquettes des îlots sécurisés soient réétiquetés comme « général » par le client d’étiquetage unifié Azure Information Protection.

Exemple :

- L’étiquette Secure Islands inclut le mot **Interne** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

- Clé : **labelByCustomProperties**

- Valeur : l' **étiquette des îlots sécurisés contient Internal, classification,.\*Internal.\***

Exemple de commande PowerShell, où votre étiquette est nommée « général » :

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Exemple 4 : plusieurs règles pour la même étiquette

Lorsque vous avez besoin de plusieurs règles pour la même étiquette, définissez plusieurs valeurs de chaîne pour la même clé. 

Dans cet exemple, les étiquettes des îles sécurisées nommées « confidentiel » et « secret » sont stockées dans la propriété personnalisée nommée **classification**et vous souhaitez que le Azure information protection client d’étiquetage unifié applique l’étiquette de sensibilité nommée « confidentiel » :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>Étendre vos règles de migration d’étiquette aux e-mails

Vous pouvez utiliser vos paramètres avancés labelByCustomProperties avec les courriers électroniques Outlook en plus des documents Office en spécifiant un paramètre avancé de stratégie d’étiquette supplémentaire. Toutefois, ce paramètre a un impact négatif connu sur les performances d’Outlook. par conséquent, configurez ce paramètre supplémentaire uniquement lorsque vous avez une forte exigence pour l’entreprise et n’oubliez pas de le définir sur une valeur de chaîne NULL lorsque vous avez terminé la migration à partir de la autre solution d’étiquetage.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableLabelByMailHeader**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>Étendre vos règles de migration d’étiquette à des propriétés SharePoint

Vous pouvez utiliser vos paramètres avancés labelByCustomProperties avec des propriétés SharePoint que vous pouvez exposer en tant que colonnes aux utilisateurs.

Ce paramètre est pris en charge lorsque vous utilisez Word, Excel et PowerPoint.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie d’étiquette sélectionnée :

- Clé : **EnableLabelBySharePointProperties**

- Valeur : **True**

Exemple de commande PowerShell, où votre stratégie d’étiquette est nommée « global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Appliquer une propriété personnalisée lorsqu’une étiquette est appliquée

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Il peut y avoir des scénarios lorsque vous souhaitez appliquer une ou plusieurs propriétés personnalisées à un document ou à un message électronique en plus des métadonnées appliquées par une étiquette de sensibilité.

Exemple :

- Vous êtes en train de [migrer à partir d’une autre solution d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions), telle que des îlots sécurisés. Pour l’interopérabilité au cours de la migration, vous souhaitez que les étiquettes de sensibilité appliquent également une propriété personnalisée utilisée par l’autre solution d’étiquetage.

- Pour votre système de gestion de contenu (par exemple, SharePoint ou une solution de gestion de documents d’un autre fournisseur), vous souhaitez utiliser un nom de propriété personnalisée cohérent avec des valeurs différentes pour les étiquettes et des noms conviviaux au lieu du GUID de l’étiquette.

Pour les documents Office et les e-mails Outlook libellés par les utilisateurs à l’aide du client d’étiquetage unifié Azure Information Protection, vous pouvez ajouter une ou plusieurs propriétés personnalisées que vous définissez. Vous pouvez également utiliser cette méthode pour le client d’étiquetage unifié pour afficher une propriété personnalisée sous la forme d’une étiquette à partir d’autres solutions pour le contenu qui n’est pas encore étiqueté par le client d’étiquetage unifié.

À la suite de cette option de configuration, toutes les propriétés personnalisées supplémentaires sont appliquées par le client d’étiquetage unifié Azure Information Protection, comme suit :

- Pour les documents Office : lorsque le document est étiqueté dans l’application de bureau, les propriétés personnalisées supplémentaires sont appliquées lors de l’enregistrement du document.

- Pour les e-mails Outlook : lorsque le message électronique est étiqueté dans Outlook, les propriétés supplémentaires sont appliquées à l’en-tête x lors de l’envoi de l’e-mail.

- Pour PowerShell : [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) appliquent les propriétés personnalisées supplémentaires lorsque le document est étiqueté et enregistré. La fonction [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) affiche les propriétés personnalisées en tant qu’étiquette mappée si une étiquette de sensibilité n’est pas appliquée.

- Pour l’Explorateur de fichiers : quand l’utilisateur clique avec le bouton droit sur le fichier et applique l’étiquette, les propriétés personnalisées sont appliquées.

Cette configuration nécessite que vous spécifiiez un paramètre avancé nommé **customPropertiesByLabel** pour chaque étiquette de sensibilité à laquelle vous souhaitez appliquer les propriétés personnalisées supplémentaires. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Exemple 1 : ajouter une seule propriété personnalisée pour une étiquette

Exigence : les documents étiquetés comme étant « confidentiels » par le client d’étiquetage unifié Azure Information Protection doivent avoir la propriété personnalisée supplémentaire nommée « classification » avec la valeur « secret ».

Exemple :

- L’étiquette sensibilité est nommée **confidentiel** et crée une propriété personnalisée nommée **classification** avec la valeur **secret**.

Paramètre avancé :

- Clé : **customPropertiesByLabel**

- Valeur : **classification, secret**

Exemple de commande PowerShell, où votre étiquette est nommée « Confidential » :

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Exemple 2 : ajouter plusieurs propriétés personnalisées pour une étiquette

Pour ajouter plusieurs propriétés personnalisées pour la même étiquette, vous devez définir plusieurs valeurs de chaîne pour la même clé.

Exemple de commande PowerShell, où votre étiquette est nommée « General » et que vous souhaitez ajouter une propriété personnalisée nommée **classification** avec la valeur **General** et une deuxième propriété personnalisée nommée **Sensitivity** avec la valeur **Internal**:

    Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurer une étiquette pour appliquer la protection S/MIME dans Outlook

Cette configuration utilise des [Paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Utilisez ces paramètres uniquement lorsque vous disposez d’un [déploiement S/MIME](https://docs.microsoft.com/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) opérationnel et que vous souhaitez qu’une étiquette applique automatiquement cette méthode de protection pour les e-mails plutôt que Rights Management protection à partir de Azure information protection. La protection qui en résulte est la même que lorsque l’utilisateur sélectionne manuellement les options S/MIME dans Outlook.

Pour configurer un paramètre avancé pour une signature numérique S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **SMimeSign**

- Valeur : **True**

Pour configurer un paramètre avancé pour le chiffrement S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **SMimeEncrypt**

- Valeur : **True**

Si l’étiquette que vous spécifiez est configurée pour le chiffrement, pour le client d’étiquetage unifié Azure Information Protection, la protection S/MIME remplace la protection Rights Management uniquement dans Outlook. La version de disponibilité générale du client d’étiquetage unifié continue à utiliser les paramètres de chiffrement spécifiés pour l’étiquette dans le centre d’administration. Pour les applications Office avec étiquetage intégré, celles-ci n’appliquent pas la protection S/MIME mais appliquent la protection ne pas transférer.

Si vous souhaitez que l’étiquette soit visible dans Outlook uniquement, configurez l’étiquette pour appliquer le chiffrement **uniquement aux messages électroniques dans Outlook**.

Exemples de commandes PowerShell, où votre étiquette est nommée « destinataires uniquement » :

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Spécifier une sous-étiquette par défaut pour une étiquette parent

Cette configuration utilise un [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Lorsque vous ajoutez une sous-étiquette à une étiquette, les utilisateurs ne peuvent plus appliquer l’étiquette parent à un document ou à un e-mail. Par défaut, les utilisateurs sélectionnent l’étiquette parente pour afficher les sous-étiquettes qu’elles peuvent appliquer, puis sélectionnent l’une de ces sous-étiquettes. Si vous configurez ce paramètre avancé, lorsque les utilisateurs sélectionnent l’étiquette parent, une sous-étiquette est automatiquement sélectionnée et appliquée : 

- Clé : **DefaultSubLabelId**

- Valeur : GUID de la sous-étiquette \<

Exemple de commande PowerShell, où votre étiquette parente est nommée « Confidential » et la sous-étiquette « all employees » a le GUID 8faca7b8-8d20-48A3-8ea2-0f96310a848e :

    Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}


## <a name="specify-a-color-for-the-label"></a>Spécifier une couleur pour l’étiquette

Cette configuration utilise des [Paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) d’étiquette que vous devez configurer à l’aide d’Office 365 Centre de sécurité et de conformité PowerShell.

Utilisez ce paramètre avancé pour définir la couleur d’une étiquette. Pour spécifier la couleur, entrez un code d’triplement hexadécimal pour les composants rouge, vert et bleu (RVB) de la couleur. Par exemple, #40e0d0 est la valeur hexadécimale RVB pour turquoise.

Si vous avez besoin d’une référence pour ces codes, vous trouverez une table utile à partir de la page de [> de couleur\<](https://developer.mozilla.org/docs/Web/CSS/color_value) dans les documents Web MSDN. Vous trouverez également ces codes dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

Pour configurer le paramètre avancé pour la couleur d’un contrôle Label, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **couleur**

- Valeur : \<valeur hexadécimale RVB >

Exemple de commande PowerShell, où votre étiquette est nommée « public » :

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs n’ont généralement pas besoin de se connecter en tant qu’utilisateur différent lorsqu’ils utilisent le client d’étiquetage unifié Azure Information Protection. Toutefois, en tant qu’administrateur, vous devrez peut-être vous connecter sous un autre nom d’utilisateur pendant une phase de test. 

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure information protection** : Ouvrez une application Office et, sous l’onglet dossier de **démarrage** , cliquez sur le bouton **sensibilité** , puis sélectionnez **aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Un symptôme de l’utilisation d’un compte incorrect comprend l’échec du téléchargement des étiquettes ou l’affichage des étiquettes ou du comportement que vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. Accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si vous ne voyez pas d’invite dans votre application Office pour vous connecter au service Azure Information Protection, revenez à la boîte de dialogue **Microsoft Azure information protection** et sélectionnez **se connecter** à partir de la section **État du client** mis à jour.

En outre :

- Si le client d’étiquetage unifié Azure Information Protection est toujours connecté avec l’ancien compte après avoir effectué ces étapes, supprimez tous les cookies d’Internet Explorer, puis répétez les étapes 1 et 2.

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir supprimé le fichier de jeton. Le Azure Information Protection client d’étiquetage unifié s’authentifie ensuite automatiquement à l’aide de votre compte d’utilisateur actuellement connecté.

- Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.

- Vous pouvez utiliser l’option **Réinitialiser les paramètres** dans **aide et commentaires** pour vous déconnecter et supprimer les étiquettes et les paramètres de stratégie actuellement téléchargés à partir du centre de sécurité et de conformité Office 365, du centre de sécurité Microsoft 365 ou du centre de conformité des Microsoft 365.


## <a name="support-for-disconnected-computers"></a>Prise en charge des ordinateurs déconnectés

> [!IMPORTANT]
> Les ordinateurs déconnectés sont pris en charge pour les scénarios d’étiquetage suivants : Explorateur de fichiers, PowerShell, vos applications Office et le scanneur.

Par défaut, le Azure Information Protection client d’étiquetage unifié tente automatiquement de se connecter à Internet pour télécharger les étiquettes et les paramètres de stratégie d’étiquette à partir du centre de gestion des étiquettes : le Centre de sécurité et de conformité Office 365, le Microsoft 365 Security Center ou le centre de conformité des Microsoft 365. Si vous avez des ordinateurs qui ne peuvent pas se connecter à Internet pendant un certain temps, vous pouvez exporter et copier des fichiers qui gèrent manuellement la stratégie du client d’étiquetage unifié.

Instructions :

1. Choisissez ou créez un compte d’utilisateur dans Azure AD que vous allez utiliser pour télécharger des étiquettes et des paramètres de stratégie que vous souhaitez utiliser sur votre ordinateur déconnecté.

2. En tant que paramètre de stratégie d’étiquette supplémentaire pour ce compte, [désactivez l’envoi de données d’audit à Azure information protection Analytics](#disable-sending-audit-data-to-azure-information-protection-analytics) à l’aide du paramètre avancé **EnableAudit** .
    
    Nous vous recommandons d’effectuer cette étape, car si l’ordinateur déconnecté dispose d’une connectivité Internet périodique, il envoie les informations de journalisation à Azure Information Protection Analytics qui comprend le nom d’utilisateur de l’étape 1. Ce compte d’utilisateur peut être différent du compte local que vous utilisez sur l’ordinateur déconnecté.

3. À partir d’un ordinateur connecté à Internet et sur lequel le client d’étiquetage unifié est installé et connecté avec le compte d’utilisateur de l’étape 1, téléchargez les étiquettes et les paramètres de stratégie.

4. À partir de cet ordinateur, exportez les fichiers journaux.
    
    Par exemple, exécutez l’applet de commande [Export-AIPLogs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs) ou utilisez l’option **Exporter les journaux** de la boîte de dialogue [aide et commentaires](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client) du client. 
    
    Les fichiers journaux sont exportés sous la forme d’un fichier compressé unique.

5.  Ouvrez le fichier compressé et, à partir du dossier MSIP, copiez tous les fichiers qui ont une extension de nom de fichier. Xml.

6. Collez ces fichiers dans le dossier **%LocalAppData%\Microsoft\MSIP** sur l’ordinateur déconnecté.

7. Si le compte d’utilisateur choisi est un compte qui se connecte généralement à Internet, activez à nouveau l’envoi des données d’audit en affectant à la valeur **EnableAudit** la valeur **true**.

8. Pour que l’ordinateur déconnecté protège des fichiers, reprotégez les fichiers, supprimez la protection des fichiers ou Inspectez les fichiers protégés : sur l’ordinateur déconnecté, exécutez l’applet de commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec le paramètre *DelegatedUser* et spécifiez le compte d’utilisateur de l’étape 1 pour définir le contexte de l’utilisateur. Exemple :
    
        Set-AIPAuthentication -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser offlineuser@contoso.com

N’oubliez pas que si un utilisateur de cet ordinateur sélectionne l’option **Réinitialiser les paramètres** dans [aide et commentaires](clientv2-admin-guide.md#help-and-feedback-section), cette action supprime les fichiers de stratégie et rend le client inopérant tant que vous n’avez pas remplacé manuellement les fichiers ou que le client ne se connecte pas à Internet et télécharge les fichiers.

Si votre ordinateur déconnecté exécute le scanneur Azure Information Protection, vous devez effectuer des étapes de configuration supplémentaires. Pour plus d’informations, voir [restriction : le serveur du scanneur ne peut pas disposer d’une connexion Internet](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity) à partir des instructions de déploiement de l’analyseur.

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez personnalisé le client d’étiquetage unifié Azure Information Protection, consultez les ressources suivantes pour obtenir des informations supplémentaires dont vous pouvez avoir besoin pour prendre en charge ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)
