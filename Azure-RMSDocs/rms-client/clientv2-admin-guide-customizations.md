---
title: Configurations personnalisées - Azure Information Protection unifiée étiquetage client
description: Informations sur la personnalisation du client d’étiquetage unifié d’Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: aac8b94bbe1eaa46111dee15ac5f69d05ac730ab
ms.sourcegitcommit: 849c493cef6b2578945c528f4e17373a2ef26287
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563449"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifiée Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations suivantes pour les configurations avancées que vous devrez peut-être pour des scénarios spécifiques ou un sous-ensemble d’utilisateurs lorsque vous gérez le client d’étiquetage unifié Azure Information Protection.

Ces paramètres nécessitent une modification du Registre ou en spécifiant les paramètres avancés. L’utilisation de paramètres avancés [PowerShell du centre de conformité et sécurité Office 365](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps).

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Comment configurer les paramètres avancés pour le client à l’aide de PowerShell du centre de conformité et sécurité Office 365

Lorsque vous utilisez PowerShell du centre de conformité et sécurité Office 365, vous pouvez configurer des paramètres avancés qui prennent en charge des personnalisations pour les étiquettes et les stratégies de l’étiquette. Exemple :

- Le paramètre pour afficher la barre Information Protection dans les applications Office est un ***stratégie paramètre avancé de l’étiquette***.
- Le paramètre pour spécifier une couleur de l’étiquette est un ***étiquette paramètre avancé***.

Dans les deux cas, après avoir [se connecter à Office 365 Security & PowerShell du centre de conformité](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps), spécifiez la *AdvancedSettings* paramètre avec l’identité (nom ou GUID) de la stratégie ou d’une étiquette et spécifiez paires de clé/valeur un [table de hachage](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables). Utilisez la syntaxe suivante :

Pour un paramètre de stratégie étiquette unique comme valeur de chaîne :

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

Pour les paramètres de stratégie étiquette, plusieurs valeurs de chaîne pour la même clé :

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Pour un paramètre d’étiquette unique comme valeur de chaîne :

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

Pour les paramètres de l’étiquette, plusieurs valeurs de chaîne pour la même clé :

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

Pour supprimer un paramètre avancé, utilisent la même syntaxe, mais spécifiez une valeur de chaîne null.


#### <a name="examples-for-setting-advanced-settings"></a>Exemples pour la définition des paramètres avancés

Exemple 1 : Définir une stratégie d’étiquette paramètre avancée pour une valeur de chaîne unique :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

Exemple 2 : Définir une étiquette de paramètre pour une valeur de chaîne unique avancée :

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

Exemple 3 : Définir une étiquette de paramètre avancée pour plusieurs valeurs de chaîne :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

Exemple 4 : Supprimer une stratégie d’étiquette paramètre avancée en spécifiant une valeur de chaîne null :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>Spécification de l’identité pour la stratégie d’étiquette ou une étiquette

En spécifiant le nom de stratégie d’étiquette pour PowerShell *identité* paramètre est simple, car vous ne voyez qu’un seul nom de la stratégie dans le centre d’administration où vous gérez vos stratégies d’étiquette. Toutefois, pour les étiquettes, vous verrez à la fois un **nom** et **nom d’affichage** dans l’administrateur centres. Dans certains cas, la valeur pour les deux sera le même, mais ils peuvent être différents :

- **Nom** est le nom d’origine de l’étiquette et que celui-ci soit unique parmi toutes les étiquettes. Si vous modifiez le nom de votre étiquette après sa création, cette valeur reste la même.

- **Nom d’affichage** est le nom de l’étiquette que les utilisateurs voient et pas nécessairement être unique parmi toutes les étiquettes. Par exemple, les utilisateurs voient une **tous les employés** sublabel pour le **confidentiel** étiquette et l’autre **tous les employés** sublabel pour le **hautement confidentiel**  étiquette. Ces sous-étiquettes affichent le même nom mais ne sont pas la même étiquette et ont des paramètres différents.

Pour configurer votre étiquette les paramètres avancé, utilisez le **nom** valeur. Par exemple, pour identifier l’étiquette dans l’image suivante, vous devez spécifier `-Identity "All Company"`:

![Utilisez « Name » plutôt que « Nom d’affichage » pour identifier une étiquette de sensibilité](../media/labelname_scc.png)

Si vous préférez spécifier le GUID de l’étiquette, cette valeur n’est pas affichée dans le centre d’administration où vous gérez vos étiquettes. Toutefois, vous pouvez utiliser la commande suivante PowerShell du centre de conformité et sécurité Office 365 pour trouver cette valeur :

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>Ordre de priorité - conflit de paramètres sont résolus

À l’aide d’un des centres d’administration où vous gérez vos étiquettes de sensibilité, vous pouvez configurer les paramètres de stratégie d’étiquette suivantes :

- **Appliquer cette étiquette par défaut aux documents et e-mails**

- **Les utilisateurs doivent fournir une justification pour supprimer une étiquette ou une étiquette de classification moins élevée**

- **Demander aux utilisateurs d’appliquer une étiquette à leur e-mail ou un document**

- **Fournir aux utilisateurs avec un lien vers une page d’aide personnalisé**

Lorsque plusieurs stratégies de l’étiquette est configurée pour un utilisateur, chacun ayant potentiellement différents paramètres de stratégie, le dernier paramètre de stratégie est appliqué selon l’ordre des stratégies dans le centre d’administration. Pour plus d’informations, consultez [étiqueter la priorité des stratégies (questions d’ordre)](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels#label-policy-priority-order-matters)

Étiquette paramètres avancé suivent la même logique pour la priorité de : Lorsqu’une étiquette est en plusieurs stratégies d’étiquette et cette étiquette a des paramètres avancés, le dernier paramètre avancé est appliqué selon l’ordre des stratégies dans le centre d’administration.

Paramètres de stratégie avancés sont appliqués dans l’ordre inverse de l’étiquette : À une exception près, les paramètres avancés de la première stratégie sont appliqués, en fonction de l’ordre des stratégies dans le centre d’administration. L’exception est le paramètre avancé *OutlookDefaultLabel*, qui définit une autre étiquette par défaut pour Outlook. Pour cette stratégie étiquette paramètre avancé uniquement, le dernier paramètre est appliqué selon l’ordre des stratégies dans le centre d’administration.

#### <a name="available-advanced-settings-for-label-policies"></a>Disponible des paramètres avancé pour les stratégies d’étiquette

|Paramètre|Scénario et instructions|
|----------------|---------------|
|AttachmentAction|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[Pour les e-mails avec pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|EnableCustomPermissions|[Désactiver les autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées pour les utilisateurs dans l’Explorateur de fichiers](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|labelByCustomProperties|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LogMatchedContent|[Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Définir une autre étiquette par défaut pour Outlook](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Activer la classification recommandée dans Outlook](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[Supprimer « Pas maintenant » pour les documents quand l’étiquetage obligatoire est utilisé](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[Ajouter « Signaler un problème » pour les utilisateurs](#add-report-an-issue-for-users)|
|RunAuditInformationTypeDiscovery|[Désactiver l’envoi des informations sensibles découvertes dans les documents à l’analytique d’Azure Information Protection](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|

Exemple de commande PowerShell pour vérifier vos paramètres de stratégie d’étiquette en vigueur pour une stratégie d’étiquette nommé « Global » :

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>Paramètres avancés disponibles pour les étiquettes

|Paramètre|Scénario et instructions|
|----------------|---------------|
|Couleur|[Spécifiez une couleur pour l’étiquette](#specify-a-color-for-the-label)|
|customPropertyByLabel|[Migrer des étiquettes de Secure Islands et autres solutions d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|DefaultSubLabelId|[Spécifier une sous-étiquette par défaut pour une étiquette parent](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Appliquer une propriété personnalisée, quand une étiquette est appliquée.](#apply-a-custom-property-when-a-label-is-applied)|
|SMimeEncrypt|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](#configure-a-label-to-apply-smime-protection-in-outlook)|

Exemple de commande PowerShell pour vérifier vos paramètres d’étiquette en vigueur pour une étiquette nommée « Public » :

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Afficher la barre Information Protection dans les applications Office

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Par défaut, les utilisateurs doivent sélectionner la **afficher la barre** option à partir de la **sensibilité** bouton pour afficher la barre Information Protection dans les applications Office. Utilisez le **HideBarByDefault** de clé et définissez la valeur sur **False** pour afficher automatiquement cette barre pour les utilisateurs afin qu’ils peuvent sélectionner des étiquettes à partir de la barre ou le bouton. 

Pour la stratégie de l’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **HideBarByDefault**

- Value : **False**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="enable-recommended-classification-in-outlook"></a>Activer la classification recommandée dans Outlook

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Quand vous configurez une étiquette pour la classification recommandée, les utilisateurs sont invités à accepter ou ignorer l’étiquette recommandée dans Word, Excel et PowerPoint. Ce paramètre affiche également cette recommandation d’étiquette dans Outlook.

Pour la stratégie de l’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookRecommendationEnabled**

- Value : **True**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Définir une autre étiquette par défaut pour Outlook

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque vous configurez ce paramètre, Outlook n’applique pas l’étiquette par défaut qui est configuré comme un paramètre de stratégie pour l’option **appliquer cette étiquette par défaut aux documents et e-mails**. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer.

Pour la stratégie de l’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **OutlookDefaultLabel**

- Valeur : \< **GUID de l’étiquette**> ou **None**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}


## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>Supprimer « Pas maintenant » pour les documents quand vous utilisez l’étiquetage obligatoire

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque vous utilisez le paramètre de stratégie d’étiquette de **tous les documents et e-mails doivent avoir une étiquette**, les utilisateurs sont invités à sélectionner une étiquette au premier enregistrement d’un document Office et lorsqu’ils envoient un message électronique. Pour les documents, les utilisateurs peuvent sélectionner **Pas maintenant** pour ignorer temporairement l’invite à sélectionner une étiquette et revenir au document. En revanche, ils ne peuvent pas fermer le document enregistré sans l’étiqueter. 

Quand vous configurez ce paramètre, l’option **Pas maintenant** n’est pas proposée, et les utilisateurs sont obligés de sélectionner une étiquette au premier enregistrement du document.

Pour la stratégie de l’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **PostponeMandatoryBeforeSave**

- Value : **False**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>Supprimer les en-têtes et les pieds de page d’autres solutions d’étiquetage

Cette configuration utilise la stratégie [paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Les paramètres permettent de supprimer ou de remplacer des en-têtes ou des pieds de page textuels de documents quand ces marquages visuels ont été appliqués par une autre solution d’étiquetage. Par exemple, le pied de page ancien contient le nom d’une ancienne étiquette que vous avez maintenant migré vers étiquettes de sensibilité à utiliser un nouveau nom d’étiquette et sa propre pied de page.

Lorsque le client d’étiquetage unifié obtient cette configuration dans sa stratégie, ancien en-têtes et pieds de page sont supprimées ou remplacées lorsque le document est ouvert dans l’application Office et une étiquette de sensibilité est appliquée au document.

Cette configuration n’est pas prise en charge pour Outlook. Sachez également que quand vous l’utilisez avec Word, Excel et PowerPoint, elle peut affecter négativement les performances de ces applications pour les utilisateurs. La configuration vous permet de définir des paramètres par application, par exemple, rechercher du texte dans les en-têtes et les pieds de page des documents Word, mais pas dans les feuilles de calcul Excel ni dans les présentations PowerPoint.

Étant donné que la correspondance de modèle affecte les performances pour les utilisateurs, nous vous recommandons de limiter les types d’applications Office (**W**ord, **E**xcel, **P**PowerPoint) à celles qui doivent être recherchés.

Pour la stratégie de l’étiquette sélectionnée, spécifiez les chaînes suivantes :

- Clé : **RemoveExternalContentMarkingInApp**

- Value : \<**Types d’application Office WXP**> 

Exemples :

- Pour rechercher dans des documents Word uniquement, spécifiez **W**.

- Pour rechercher dans des documents Word et des présentations PowerPoint, spécifiez **WP**.

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

Ensuite, vous avez besoin d’au moins un paramètre client avancé de plus, **ExternalContentMarkingToRemove**, pour spécifier le contenu de l’en-tête ou du pied de page et comment les supprimer ou les remplacer.

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>Comment configurer ExternalContentMarkingToRemove

Lorsque vous spécifiez la valeur de chaîne pour la clé **ExternalContentMarkingToRemove**, vous disposez de trois options qui utilisent des expressions régulières :

- Correspondance partielle pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXT TO REMOVE** (TEXTE À SUPPRIMER). Vous souhaitez entièrement supprimer ces en-têtes ou pieds de page. Spécifiez la valeur : `*TEXT*`.

- Correspondance totale pour juste supprimer des mots spécifiques dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXT TO REMOVE** (TEXTE À SUPPRIMER). Vous souhaitez supprimer le mot **TEXTE** uniquement, ce qui laisse la chaîne d’en-tête ou de pied de page avec **À SUPPRIMER**. Spécifiez la valeur : `TEXT `.

- Correspondance totale pour tout supprimer dans l’en-tête ou le pied de page.
    
    Exemple : Les en-têtes ou les pieds de page contiennent la chaîne **TEXT TO REMOVE** (TEXTE À SUPPRIMER). Vous voulez supprimer les en-têtes ou les pieds de page qui ont exactement cette chaîne. Spécifiez la valeur : `^TEXT TO REMOVE$`.
    

Les caractères génériques de la chaîne que vous spécifiez sont sensibles à la casse. La longueur maximale de la chaîne est de 255 caractères.

Étant donné que des documents peuvent contenir des caractères invisibles ou différents types d’espaces ou des tabulations, la chaîne que vous spécifiez pour une expression ou une phrase peut ne pas être détectée. Si possible, spécifiez un seul mot distinctif pour la valeur et veillez à tester les résultats avant de procéder au déploiement en production.

Pour la même stratégie de l’étiquette, spécifiez les chaînes suivantes :

- Clé : **ExternalContentMarkingToRemove**

- Valeur : \< **chaîne à trouver, définie comme expression régulière**> 

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>En-têtes ou pieds de page multilignes

Si un texte d’en-tête ou de pied de page prend plus d’une ligne, créez une clé et une valeur pour chaque ligne. Par exemple, vous avez le pied de page suivant sur deux lignes :

**Le fichier est classé confidentiel**

**Étiquette appliquée manuellement**

Pour supprimer ce pied de page multiligne, vous créez les deux entrées suivantes pour la même stratégie d’étiquette :

- Clé : **ExternalContentMarkingToRemove**

- Valeur de la clé 1 : **\*Confidentiel***

- Valeur de la clé 2 : **\*Étiquette appliquée*** 

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>Optimisation pour PowerPoint

Les pieds de page dans PowerPoint sont implémentés en tant que formes. Pour éviter de supprimer les formes qui contiennent le texte que vous avez spécifié, mais qui ne sont ni des en-têtes ni des pieds de page, utilisez un paramètre client avancé supplémentaire nommé **PowerPointShapeNameToRemove**. Nous recommandons également d’utiliser ce paramètre pour éviter de vérifier le texte dans toutes les formes, qui est un processus gourmand en ressources.

Si vous ne spécifiez pas ce paramètre client avancé supplémentaire et si PowerPoint est inclus dans la valeur de la clé **RemoveExternalContentMarkingInApp**, toutes les formes sont vérifiées à la recherche du texte que vous spécifiez dans la valeur  **ExternalContentMarkingToRemove**. 

Pour rechercher le nom de la forme que vous utilisez comme en-tête ou pied de page :

1. Dans PowerPoint, affichez le volet **Sélection** : Onglet **Format** > Groupe **Organiser** > Volet **Sélection**.

2. Sélectionnez la forme sur la diapositive qui contient votre en-tête ou votre pied de page. Le nom de la forme sélectionnée est maintenant en surbrillance dans le volet **Sélection**.

Utilisez le nom de la forme afin de spécifier une valeur de chaîne pour la clé **PowerPointShapeNameToRemove**. 

Exemple : Le nom de la forme est **fc**. Pour supprimer la forme portant ce nom, spécifiez la valeur : `fc`.

- Clé : **PowerPointShapeNameToRemove**

- Value : \<**Nom de la forme PowerPoint**> 

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

Lorsque vous avez plusieurs formes de PowerPoint à supprimer, spécifiez toutes les valeurs que vous avez des formes à supprimer.

Par défaut, seuls les en-têtes et les pieds de page qui se trouvent dans les diapositives principales sont recherchés. Pour étendre cette recherche à toutes les diapositives, processus beaucoup plus gourmand en ressources, utilisez un paramètre client avancé supplémentaire nommé **RemoveExternalContentMarkingInAllSlides**:

- Clé : **RemoveExternalContentMarkingInAllSlides**

- Value : **True**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>Désactiver les autorisations personnalisées dans l’Explorateur de fichiers

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Par défaut, les utilisateurs voient une option nommée **protéger avec des autorisations personnalisées** lorsqu’elles avec le bouton droit dans l’Explorateur de fichiers et choisissez **classifier et protéger**. Cette option vous permet de les définir leurs propres paramètres de protection qui peuvent remplacer les paramètres de protection que vous avez peut-être inclus avec une configuration d’étiquette. Les utilisateurs peuvent voir également une option pour supprimer la protection. Lorsque vous configurez ce paramètre, les utilisateurs ne voient pas ces options.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé : **EnableCustomPermissions**

- Value : **False**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>Pour les fichiers protégés avec des autorisations personnalisées, toujours afficher des autorisations personnalisées aux utilisateurs dans l’Explorateur de fichiers

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque vous configurez le paramètre client avancé [désactiver des autorisations personnalisées dans l’Explorateur de fichiers](#disable-custom-permissions-in-file-explorer), par défaut, les utilisateurs ne sont pas en mesure de voir ou modifier des autorisations personnalisées qui sont déjà définies dans un document protégé.

Toutefois, il existe une autre avancé paramètre client que vous pouvez spécifier afin que dans ce scénario, les utilisateurs peuvent voir et modifier des autorisations personnalisées pour un document protégé lorsqu’ils utilisent l’Explorateur de fichiers et cliquez sur le fichier.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé : **EnableCustomPermissionsForCustomProtectedFiles**

- Value : **True**

Exemple de commande PowerShell :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes

Cette configuration utilise la stratégie [paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque les utilisateurs joignez des documents étiquetées à un e-mail et effectuez l’étiquette pas le message électronique proprement dit, ce paramètre est destiné. Dans ce scénario, une étiquette est automatiquement sélectionnée pour eux, basée sur les étiquettes de classification qui sont appliquées aux pièces jointes. L’étiquette de classification la plus élevée est sélectionnée.

La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur SharePoint ou OneDrive Entreprise).

Vous pouvez configurer ce paramètre pour **recommandé**, de sorte que les utilisateurs sont invités à appliquer l’étiquette sélectionnée à leur e-mail, avec une info-bulle personnalisable. Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Ou, vous pouvez configurer ce paramètre pour **automatique**, où l’étiquette sélectionnée est appliquée automatiquement, mais les utilisateurs peuvent supprimer l’étiquette ou sélectionnez une autre étiquette avant d’envoyer l’e-mail.

Remarque : Quand la pièce jointe avec l’étiquette de classification la plus élevée est configurée pour la protection avec le paramètre d’autorisations définies par l’utilisateur :

- Lorsque l’étiquette-défini par l’utilisateur les autorisations incluent Outlook (ne pas transférer), que label est sélectionné et la protection de ne pas transférer est appliquée à l’adresse e-mail. 
- Lorsque les autorisations définies par l’utilisateur de l’étiquette sont simplement pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette n’est pas appliquée au message électronique, et n’est pas une protection.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé 1 : **AttachmentAction**

- Valeur de la clé 1 : **Recommandé** ou **automatique**

- Clé 2 : **AttachmentActionTip**

- Valeur de la clé 2 : «\<personnalisé d’info-bulle > »


Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>Ajouter « Signaler un problème » pour les utilisateurs

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Quand vous spécifiez le paramètre client avancé suivant, les utilisateurs voient une option **Signaler un problème** qu’ils peuvent sélectionner dans la boîte de dialogue **Aide et commentaires** du client. Spécifiez une chaîne HTTP pour le lien. (par exemple, une page web personnalisée permettant aux utilisateurs de signaler des problèmes, ou une adresse e-mail qui pointe vers votre support technique). 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé : **ReportAnIssueLink**

- Value : **\<Chaîne HTTP>**

Exemple de valeur pour un site web : `https://support.contoso.com`

Exemple de valeur pour une adresse e-mail : `mailto:helpdesk@contoso.com`

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Implémenter des messages contextuels dans Outlook qui avertissent, demandent une justification ou bloquent l’envoi des e-mails

Cette configuration utilise la stratégie [paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Quand vous créez et que vous configurez les paramètres client avancés suivants, les utilisateurs voient des messages contextuels dans Outlook qui peuvent les avertir avant d’envoyer un e-mail, leur demander de justifier la raison pour laquelle ils envoient un e-mail ou les empêcher d’envoyer un e-mail pour un des scénarios suivants :

- **Leur e-mail ou la pièce jointe à leur e-mail a une étiquette spécifique** :
    - La pièce jointe peut être n’importe quel type de fichier

- **Leur e-mail ou leur pièce jointe à l’e-mail n’a pas d’étiquette** :
    - La pièce jointe peut être un document Office ou un document PDF

Lorsque ces conditions sont remplies et adresse de messagerie du destinataire n’est pas inclus dans une liste autorisée des noms de domaine que vous avez spécifié, l’utilisateur voit un message contextuel avec l’une des actions suivantes :

- **Avertir** : L’utilisateur peut confirmer et envoyer, ou bien annuler.

- **Justifier** : L’utilisateur est invité à entrer une justification (selon des options prédéfinies ou sous forme libre).  L’utilisateur peut ensuite envoyer ou annuler l’e-mail. Le texte de la justification est écrit dans l’en-tête X de l’e-mail afin qu’il puisse être lu par d’autres systèmes, par exemple des services de protection contre la perte de données.

- **Bloquer** : L’utilisateur ne peut pas envoyer l’e-mail tant que la condition perdure. Le message contient la raison du blocage de l’e-mail pour que l’utilisateur puisse résoudre le problème, par exemple supprimer des destinataires spécifiques ou appliquer une étiquette à l’e-mail. 


> [!TIP]
> Bien que le didacticiel est pour le client Azure Information Protection plutôt que le client d’étiquetage unifié, vous pouvez voir ces paramètres dans l’action par vous-même avec avancés [didacticiel : Configurez Azure Information Protection pour contrôler oversharing des informations à l’aide de Outlook](../infoprotect-oversharing-tutorial.md).

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>Pour implémenter des messages d’avertissement, de justification ou de blocage pour des étiquettes spécifiques :

Pour la stratégie sélectionnée, créez un ou plusieurs des paramètres avancés suivants avec les clés suivantes. Pour les valeurs, spécifier une ou plusieurs étiquettes par leur GUID, chacun d’eux séparé par une virgule.

Exemple de valeur d’étiquette plusieurs GUID sous forme de chaîne séparée par des virgules : `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- Messages d’avertissement :
    
    - Clé : **OutlookWarnUntrustedCollaborationLabel**
    
    - Valeur : \< **GUID, séparées par des virgules de l’étiquette**>

- Messages de justification :
    
    - Clé : **OutlookJustifyUntrustedCollaborationLabel**
    
    - Valeur : \< **GUID, séparées par des virgules de l’étiquette**>

- Messages de blocage :
    
    - Clé : **OutlookBlockUntrustedCollaborationLabel**
    
    - Valeur : \< **GUID, séparées par des virgules de l’étiquette**>


Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}


### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>Pour implémenter des messages contextuels d’avertissement, de justification ou de blocage pour des e-mails ou des pièces jointes qui n’ont pas d’étiquette :

Pour la même stratégie de l’étiquette, créer les éléments suivants avancé du client avec l’une des valeurs suivantes :

- Messages d’avertissement :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Value : **Warn**

- Messages de justification :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Value : **Justify**

- Messages de blocage :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Value : **Bloquer**

- Désactiver ces messages :
    
    - Clé : **OutlookUnlabeledCollaborationAction**
    
    - Value : **Off**


Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>Pour définir des extensions de nom de fichier spécifique pour l’avertir, justifier ou bloquer des messages contextuels pour les pièces jointes qui n’ont pas une étiquette

Par défaut, l’avertissement, justifier ou de bloquer des messages contextuels s’appliquent à tous les documents Office et PDF. Vous pouvez affiner cette liste en spécifiant les extensions de nom de fichier doit afficher l’avertissement, justifier ou bloquer les messages avec un autre paramètre et avancées une liste séparée par des virgules du fichier des extensions de nom.

Exemple de valeur pour plusieurs extensions de nom de fichier définir sous forme de chaîne séparée par des virgules : `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

Dans cet exemple, un document PDF sans étiquette n’entraîne pas avertir, justifier ou bloquer des messages contextuels.

Pour la même stratégie de l’étiquette, entrez les chaînes suivantes : 


- Clé : **OutlookOverrideUnlabeledCollaborationExtensions**

- Valeur : **\<** pour afficher les messages, séparés par des virgules des extensions de nom de fichier **>**


Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

### <a name="to-specify-the-allowed-domain-names-for-recipients-exempt-from-the-pop-up-messages"></a>Pour spécifier les noms de domaine autorisés pour des destinataires exemptés des messages contextuels

Lorsque vous spécifiez des noms de domaine dans un paramètre client avancé supplémentaire, les utilisateurs ne voient pas les messages contextuels pour les destinataires qui disposent de ce nom de domaine inclus dans leur adresse de messagerie. Dans ce cas, les e-mails sont envoyés sans qu’un message interrompe le processus. Pour spécifier plusieurs domaines, ajoutez-les sous la forme d’une seule chaîne, en les séparant par des virgules.

Une configuration typique consiste à afficher les messages contextuels seulement pour les destinataires qui sont externes à votre organisation ou qui ne sont pas des partenaires autorisés de votre organisation. Dans ce cas, vous spécifiez tous les domaines de messagerie utilisés par votre organisation et par vos partenaires.

Pour la même stratégie de l’étiquette, créez les éléments suivants client paramètres avancés et pour la valeur, spécifiez un ou plusieurs domaines, chacun d’eux séparés par une virgule.

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

Par exemple, spécifiez le client avancé pour bloquer les messages envoyés aux utilisateurs qui ont une adresse de messagerie contoso.com jamais, paramètre de **OutlookBlockTrustedDomains** et **contoso.com**. Par conséquent, les utilisateurs ne voient pas les messages d’avertissement de la fenêtre contextuelle dans Outlook lorsqu’ils envoient un e-mail à john@sales.contoso.com.

Exemples de commandes PowerShell, dans lequel votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>Désactiver l’envoi des informations sensibles découvertes dans les documents à l’analytique d’Azure Information Protection

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

[Analytique de Protection des informations Azure](../reports-aip.md) peut détecter et signaler les documents enregistrés par les clients Azure Information Protection quand ce contenu contient des informations sensibles. Par défaut, cette information est envoyée par le client d’étiquetage unifié Azure Information Protection pour l’analytique d’Azure Information Protection.

Pour modifier ce comportement afin que ces informations ne sont pas envoyées par le client d’étiquetage unifié, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé : **RunAuditInformationTypeDiscovery**

- Value : **False**

Si vous définissez ce paramètre client avancé, les résultats d’audit sont toujours envoyés à partir du client d’étiquetage unifié, mais que les informations sont limitées à la création de rapports lorsqu’un utilisateur a accédé intitulé contenu.

Exemple :

- Avec ce paramètre, vous pouvez voir qu’un utilisateur a accédé Financial.docx étiqueté **confidentiel \ Sales**.

- Sans ce paramètre, vous pouvez voir que Financial.docx contient 6 numéros de carte de crédit.
    
    - Si vous activez également [Correspondances de contenu pour approfondir l’analyse](../reports-aip.md#content-matches-for-deeper-analysis), vous pourrez en plus voir quels sont ces numéros de carte de crédit.

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypeDiscovery="False"}

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>Désactiver l’envoi de correspondances de types d’informations pour un sous-ensemble d’utilisateurs

Cette configuration utilise une stratégie [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque la case [Analytique Azure Information Protection](../reports-aip.md) (qui collecte les correspondances de contenu des types d’informations sensibles ou des conditions personnalisées) est cochée, ces informations sont par défaut envoyées par tous les utilisateurs. Si vous avez des utilisateurs qui ne doivent pas envoyer ces données, créez les avancées de paramètre dans une stratégie d’étiquette pour ces utilisateurs client suivantes : 

- Clé : **LogMatchedContent**

- Value : **False**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="Disable"}

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Migrer des étiquettes de Secure Islands et d’autres solutions d’étiquetage

Cette configuration utilise une étiquette [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Cette configuration n’est pas compatible avec les fichiers PDF protégés qui ont une extension de nom de fichier .ppdf. Ces fichiers ne peut pas être ouvert par l’Explorateur de fichiers, de PowerShell ou l’analyseur.

Pour les documents Office qui sont étiquetés par Secure Islands, vous pouvez également réétiqueter ces documents avec une étiquette de sensibilité à l’aide d’un mappage que vous définissez. Cette méthode permet également de réutiliser les étiquettes d’autres solutions qui se trouvent sur des documents Office. 

À la suite de cette option de configuration, la nouvelle étiquette de sensibilité est appliquée par le client d’étiquetage unifié Azure Information Protection comme suit :

- Pour les documents Office : Lorsque le document est ouvert dans l’application de bureau, la nouvelle étiquette de sensibilité est affichée comme définie et est appliquée lorsque le document est enregistré.

- Pour PowerShell : [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) peut appliquer la nouvelle étiquette de sensibilité.

- Pour l’Explorateur de fichiers : Dans la boîte de dialogue Azure Information Protection, la nouvelle étiquette de sensibilité est indiquée mais n’est pas définie.

Cette configuration, vous devez spécifier un paramètre avancé nommé **labelByCustomProperties** pour chaque étiquette de sensibilité que vous souhaitez mapper à l’ancienne étiquette. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Spécifiez votre choix d’un nom de règle de migration. Utilisez un nom descriptif qui vous aide à identifier la façon dont une ou plusieurs étiquettes à partir de votre solution d’étiquetage précédente doit être mappée à l’étiquette de sensibilité. Le nom s’affiche dans les rapports d’analyse et dans l’observateur d’événements.

Notez que ce paramètre ne supprime pas l’étiquette d’origine du document ni les marquages visuels du document que l’étiquette d’origine a éventuellement appliqués. Pour supprimer les en-têtes et pieds de page, consultez la section précédente, [supprimer des en-têtes et pieds de page à partir d’autres solutions d’étiquetage](#remove-headers-and-footers-from-other-labeling-solutions).

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>Exemple 1 : Mappage un-à-un du même nom d’étiquette

Configuration requise : Les documents qui ont une étiquette Secure Islands « Confidentiel » doivent être à nouveau libellées « Confidentiel » par Azure Information Protection.

Exemple :

- L’étiquette Secure Islands s’appelle **Confidentiel** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre avancé :

- Clé : **labelByCustomProperties**

- Value : **Sécurisé étiquette Islands est confidentiel, Classification, confidentiel**

Exemple PowerShell de commande, où votre étiquette est nommé « Confidentiel » :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>Exemple 2 : Mappage un-à-un pour un autre nom d’étiquette

Configuration requise : Les documents qui ont une étiquette « Sensible » chez Secure Islands doivent être à nouveau libellés « Hautement confidentiel » par Azure Information Protection.

Exemple :

- L’étiquette Secure Islands s’appelle **Sensible** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre avancé :

- Clé : **labelByCustomProperties**

- Value : **Sécurisé étiquette Islands est sensible, Classification, sensible**

Exemple PowerShell de commande, où votre étiquette est nommé « Hautement confidentiel » :

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>Exemple 3 : Mappage plusieurs-à-un de noms d’étiquettes

Configuration requise : Vous avez deux étiquettes Secure Islands qui contiennent le mot « Interne » et vous souhaitez que les documents qui ont une de ces étiquettes Secure Islands pour être à nouveau libellées « Général » par le client d’étiquetage unifié Azure Information Protection.

Exemple :

- L’étiquette Secure Islands inclut le mot **Interne** et est stockée dans la propriété personnalisée nommée **Classification**.

Le paramètre client avancé :

- Clé : **labelByCustomProperties**

- Value : **Sécurisé étiquette Islands contient interne, Classification. \*Interne.\***

Exemple PowerShell de commande, où votre étiquette est nommé « Général » :

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>Exemple 4 : Plusieurs règles pour la même étiquette

Lorsque vous avez besoin de plusieurs règles pour la même étiquette, définir plusieurs valeurs de chaîne pour la même clé. 

Exemple :

- Le Secure Islands étiquettes nommée « confidentiel » et « Secret » est stocké dans la propriété personnalisée nommée ** Classification et vous souhaitez que le client étiquetage unifié d’Azure Information Protection pour appliquer l’étiquette de sensibilité nommée « Confidentiel » :

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>Étendre votre étiquette aux e-mails, les règles de migration

Vous pouvez utiliser votre labelByCustomProperties avancé des paramètres avec des courriers électroniques Outlook en plus de documents Office en spécifiant un paramètre de stratégie avancée supplémentaire de l’étiquette. Toutefois, ce paramètre a connu un impact négatif sur les performances d’Outlook, donc configurer ce paramètre supplémentaire uniquement lorsque vous avez une exigence métier solide pour elle et n’oubliez pas de définir une valeur de chaîne null lorsque vous avez terminé la migration à partir de la autre solution d’étiquetage.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes pour la stratégie de l’étiquette sélectionnée :

- Clé : **EnableLabelByMailHeader**

- Value : **Mar**

Exemple PowerShell de commande, où votre stratégie de l’étiquette est nommé « Global » :

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>Appliquer une propriété personnalisée, quand une étiquette est appliquée.

Cette configuration utilise une étiquette [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Il peut y avoir certains scénarios lorsque vous souhaitez appliquer une ou plusieurs propriétés personnalisées à un document ou un message électronique en plus des métadonnées qui sont appliquée par une étiquette de sensibilité.

Exemple :

- Vous êtes en cours de [migration à partir d’une autre solution d’étiquetage](#migrate-labels-from-secure-islands-and-other-labeling-solutions), tels que Secure Islands. Pour une interopérabilité lors de la migration, vous souhaitez que les étiquettes de sensibilité à appliquer également une propriété personnalisée qui est utilisée par l’autre solution d’étiquetage.

- Pour votre système de gestion de contenu (par exemple, SharePoint ou une solution de gestion de documents à partir d’un autre fournisseur) que vous souhaitez utiliser un nom de propriété personnalisé cohérent avec des valeurs différentes pour les étiquettes et noms conviviaux au lieu de l’étiquette GUID.

Pour les documents Office et des e-mails Outlook cette étiquette aux utilisateurs en utilisant le client d’étiquetage Azure Information Protection unifié, vous pouvez ajouter un ou plusieurs des propriétés personnalisées que vous définissez. Vous pouvez également utiliser cette méthode pour le client d’étiquetage unifiée pour afficher une propriété personnalisée en tant qu’étiquette à partir d’autres solutions pour le contenu qui n’est pas encore été étiqueté par le client d’étiquetage unifié.

À la suite de cette option de configuration, toutes les propriétés personnalisées supplémentaires sont appliquées par le client d’étiquetage unifié Azure Information Protection comme suit :

- Pour les documents Office : Lorsque le document est étiqueté dans l’application de bureau, les propriétés personnalisées supplémentaires sont appliquées lorsque le document est enregistré.

- Pour les e-mails Outlook : Lorsque le message électronique est étiqueté dans Outlook, les propriétés supplémentaires sont appliquées à l’en-tête x-lors de l’e-mail est envoyé.

- Pour PowerShell : [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) applique les propriétés personnalisées supplémentaires lorsque le document est étiqueté et enregistré. [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) affiche les propriétés personnalisées en tant que l’étiquette mappé si une étiquette de sensibilité n’est pas appliquée.

- Pour l’Explorateur de fichiers : Lorsque l’utilisateur clique sur le fichier et applique l’étiquette, les propriétés personnalisées sont appliquées.

Cette configuration, vous devez spécifier un paramètre avancé nommé **customPropertyByLabel** pour chaque étiquette de sensibilité à appliquer les propriétés personnalisées supplémentaires. Ensuite, définissez la valeur à utiliserpour chaque entrée avec la syntaxe suivante :

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>Exemple 1 : Ajouter une propriété personnalisée unique pour une étiquette

Configuration requise : Les documents qui sont étiquetés comme « Confidentiel » par le client d’étiquetage unifié Azure Information Protection doivent avoir la propriété personnalisée supplémentaire nommée « Classification » avec la valeur de « Secret ».

Exemple :

- L’étiquette de sensibilité est nommé **confidentiel** et crée une propriété personnalisée nommée **Classification** avec la valeur de **Secret**.

Le paramètre avancé :

- Clé : **customPropertyByLabel**

- Value : **Classification, Secret**

Exemple PowerShell de commande, où votre étiquette est nommé « Confidentiel » :

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertyByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>Exemple 2 : Ajouter plusieurs des propriétés personnalisées pour une étiquette

Pour ajouter plus d’une propriété personnalisée pour la même étiquette, vous devez définir plusieurs valeurs de chaîne pour la même clé.

Exemple de commande PowerShell, où votre étiquette est nommée « Général » et que vous souhaitez ajouter une propriété personnalisée nommée **Classification** avec la valeur de **général** et une deuxième propriété personnalisée nommée **Sensibilité** avec la valeur de **interne**:

    Set-Label -Identity General -AdvancedSettings @{customPropertyByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>Configurer une étiquette pour appliquer la protection S/MIME dans Outlook

Cette configuration utilise l’étiquette [paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Utilisez ces paramètres uniquement lorsque vous avez une [déploiement de S/MIME](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption) et souhaitez une étiquette pour appliquer automatiquement cette méthode de protection pour des messages électroniques au lieu de protection de Rights Management d’Azure Information Protection. La protection qui en résulte est la même que lorsque l’utilisateur sélectionne manuellement les options S/MIME dans Outlook.

Pour configurer un paramètre avancé pour des signatures numériques S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **SMimeSign**

- Value : **True**

Pour configurer un paramètre avancé pour le chiffrement S/MIME, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **SMimeEncrypt**

- Value : **True**

Si l’étiquette que vous spécifiez est configuré pour le chiffrement, pour la version préliminaire de Azure Information Protection unifiée étiquetage client, la protection de S/MIME remplace la protection Rights Management uniquement dans Outlook. La version disponibilité générale du client unifiée étiquetage continue à utiliser les paramètres de chiffrement spécifiés pour l’étiquette dans le centre d’administration. Pour les applications Office avec l’étiquetage intégrées, celles-ci ne s’appliquent pas la protection de S/MIME, mais au lieu de cela, appliquent ne pas transférer protection.

Si vous souhaitez que l’étiquette soit visible dans Outlook uniquement, configurez l’étiquette pour appliquer le chiffrement à **uniquement aux e-mails dans Outlook**.

Exemples de commandes PowerShell, dans lequel votre étiquette est nommé « Destinataires uniquement » :

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>Spécifier une sous-étiquette par défaut pour une étiquette parent

Cette configuration utilise une étiquette [paramètre avancé](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365. Il est pris en charge par la version préliminaire d’unifiée étiquetage uniquement le client.

Lorsque vous ajoutez une sous-étiquette à une étiquette, les utilisateurs peuvent appliquer n’est plus l’étiquette parent à un document ou l’e-mail. Par défaut, les utilisateurs sélectionner l’étiquette parent pour afficher les sous-étiquettes qu’ils peuvent s’appliquent, puis sélectionnez une de ces sous-étiquettes. Si vous configurez ce paramètre, Avancé, lorsque les utilisateurs sélectionnent l’étiquette parent, une sous-étiquette est automatiquement sélectionnée et appliquée pour eux : 

- Clé : **DefaultSubLabelId**

- Valeur : \<sublabel GUID >

Exemple de commande PowerShell, dans lequel votre étiquette parent est nommé « Confidentiel » et la sous-étiquette « Tous les employés » a un GUID de 8faca7b8 - 8d-20-48a3-8ea2-0f96310a848e :

    Set-Label -Identity "Confidential" -AdvancedSettings @{defaultsublabels="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}

## <a name="specify-a-color-for-the-label"></a>Spécifiez une couleur pour l’étiquette

Cette configuration utilise l’étiquette [paramètres avancés](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) que vous devez configurer à l’aide de PowerShell du centre de conformité et sécurité Office 365.

Utilisez ce paramètre avancé pour définir une couleur pour une étiquette. Pour spécifier la couleur, entrez un code hexadécimal pour les composants (RVB) rouges, vert et bleus de la couleur. Par exemple, #40e0d0 est la valeur RVB pour turquoise.

Si vous avez besoin d’une référence pour ces codes, vous trouverez une table utile à partir de la [ \<couleur >](https://developer.mozilla.org/docs/Web/CSS/color_value) page à partir de la documentation web MSDN. Ces codes sont utilisés dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

Pour configurer le paramètre avancé pour les couleurs d’une étiquette, entrez les chaînes suivantes pour l’étiquette sélectionnée :

- Clé : **couleur**

- Value : \<Valeur RVB >

Exemple PowerShell de commande, où votre étiquette est nommé « Public » :

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs n’aurait pas généralement obligé de vous connecter comme un autre utilisateur lorsqu’ils utilisent Azure Information Protection unifiée étiquetage client. Toutefois, en tant qu’administrateur, vous devrez peut-être vous connecter sous un autre nom d’utilisateur pendant une phase de test. 

Vous pouvez vérifier sous quel compte vous êtes actuellement connecté en utilisant la boîte de dialogue **Microsoft Azure Information Protection** : Ouvrez une application Office et sur le **accueil** onglet, sélectionnez le **sensibilité** bouton, puis sélectionnez **aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Un symptôme d’à l’aide de compte incorrect inclut ne parvient pas à télécharger les étiquettes, ou vous ne voyez ne pas les étiquettes ou le comportement que vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. Accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si vous ne voyez pas une invite de commandes dans votre application Office pour vous connecter au service Azure Information Protection, revenez à la **Microsoft Azure Information Protection** boîte de dialogue et sélectionnez **connectez-vous** à partir de la mise à jour **d’état du Client** section.

En outre :

- Si le client d’étiquetage unifié Azure Information Protection est toujours connecté avec l’ancien compte après avoir effectué ces étapes, supprimer tous les cookies à partir d’Internet Explorer et répétez les étapes 1 et 2.

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir supprimé le fichier de jeton. Client Azure Information Protection unifié étiquetage alors vous authentifier automatiquement à l’aide de votre actuellement connecté dans le compte d’utilisateur.

- Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.

- Vous pouvez utiliser la **réinitialiser les paramètres** option à partir de **aide et commentaires** pour vous déconnecter et supprimer les étiquettes actuellement téléchargés et les paramètres de stratégie à partir de la sécurité et Office 365 centre de conformité, le Microsoft 365 Security center, ou le centre de conformité de Microsoft 365.


## <a name="change-the-local-logging-level"></a>Modifier le niveau de journalisation local

Par défaut, Azure Information Protection unifiée étiquetage écritures client fichiers journaux du client pour le **%localappdata%\Microsoft\MSIP** dossier. Ces fichiers servent à la résolution des problèmes par le Support Microsoft.
 
Pour modifier le niveau de journalisation pour ces fichiers, recherchez le nom de valeur suivant dans le Registre et définir les données de valeur pour le niveau de journalisation requis :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

Définissez le niveau de journalisation sur l'une des valeurs suivantes :

- **Désactivé** : aucune journalisation locale.

- **Erreur** : erreurs uniquement.

- **Info** : journalisation minimale, qui n’inclut aucun ID d’événement.

- **Debug** : Informations complètes.

- **Trace** : Journalisation détaillée (paramètre par défaut pour les clients).

Ce paramètre de Registre ne modifie pas les informations qui sont envoyées vers Azure Information Protection pour [centrale reporting](../reports-aip.md).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez personnalisé le client étiquetage d’Azure Information Protection unifié, consultez les ressources suivantes pour plus d’informations que vous devrez peut-être prendre en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)
