---
title: Migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée-AIP
description: Migrez Azure Information Protection étiquettes vers des étiquettes de sensibilité unifiée pour les clients et les services qui prennent en charge Microsoft Information Protection Framework.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e505ef4153732fe68b1475112cb2ab97d520433e
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383225"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>Comment migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée

> **S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> **Concerne les** [clients Azure information protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Migrez Azure Information Protection étiquettes vers la plateforme d’étiquetage unifiée pour pouvoir les utiliser en tant qu’étiquettes de sensibilité par [les clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling).

> [!NOTE]
> Si votre abonnement Azure Information Protection est relativement nouveau, vous n’aurez peut-être pas besoin de migrer des étiquettes, car votre locataire est déjà sur la plateforme d’étiquetage unifiée. Pour plus d’informations, consultez [Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Après avoir migré vos étiquettes, vous ne verrez aucune différence avec le client Azure Information Protection Classic, car ce client continue de télécharger les étiquettes avec la stratégie de Azure Information Protection à partir du Portail Azure. Toutefois, vous pouvez maintenant utiliser les étiquettes avec le client d’étiquetage unifié Azure Information Protection et d’autres clients et services qui utilisent des étiquettes de sensibilité.

Avant de lire les instructions pour migrer vos étiquettes, vous trouverez peut-être les questions fréquemment posées suivantes :

- [Quelle est la différence entre les étiquettes dans Microsoft 365 et les étiquettes dans Azure Information Protection ?](faqs.md#whats-the-difference-between-labels-in-microsoft-365-and-labels-in-azure-information-protection)

- [Quand est-il approprié de migrer mes étiquettes ?](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Rôles d’administration qui prennent en charge la plateforme d’étiquetage unifiée

Si vous utilisez des rôles d’administrateur pour l’administration déléguée dans votre organisation, vous devrez peut-être effectuer certaines modifications pour la plateforme d’étiquetage unifiée :

Le [rôle Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) de **Azure information protection administrateur** (anciennement **information protection administrateur**) n’est pas pris en charge par la plateforme d’étiquetage unifiée. Si ce rôle d’administration est utilisé dans votre organisation pour gérer Azure Information Protection, ajoutez les utilisateurs qui possèdent ce rôle aux rôles Azure AD de l’administrateur de la **conformité**, à l’administrateur des **données de conformité** ou à l’administrateur de la **sécurité**. Si vous avez besoin d’aide pour cette étape, consultez [accorder aux utilisateurs l’accès au centre de conformité Microsoft 365 Security &](/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center). Vous pouvez également attribuer ces rôles dans le portail Azure AD, le centre de sécurité Microsoft 365 et le centre de conformité Microsoft 365.

Au lieu d’utiliser des rôles, dans les centres d’administration, vous pouvez créer un nouveau groupe de rôles pour ces utilisateurs et ajoutez les rôles **Administrateur d’étiquette de sensibilité** ou **Configuration de l’organisation** à ce groupe.

Si vous ne donnez pas accès aux centres d’administration à ces utilisateurs suivant l’une de ces configurations, ils ne pourront pas configurer Azure Information Protection dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux de votre locataire pourront continuer à gérer les étiquettes et les stratégies sur le Portail Azure et dans les centres d’administration une fois vos étiquettes migrées.

## <a name="before-you-begin"></a>Avant de commencer

La migration des étiquettes présente de nombreux avantages, mais est irréversible. Avant de procéder à la migration, assurez-vous que vous avez pris connaissance des modifications et considérations suivantes :

- [Prise en charge des clients pour l’étiquetage unifié](#client-support-for-unified-labeling)
- [Configuration de la stratégie](#policy-configuration)
- [Modèles de protection](#protection-templates)
- [Noms complets](#display-names)
- [Chaînes localisées dans les étiquettes](#localized-strings-in-labels)
- [Modification des étiquettes migrées dans les centres d’administration](#editing-migrated-labels-in-the-admin-centers)
- [Paramètres d’étiquette non pris en charge dans les centres d’administration](#label-settings-that-are-not-supported-in-the-admin-centers)
- [Comparaison du comportement des paramètres de protection pour une étiquette](#comparing-the-behavior-of-protection-settings-for-a-label)

### <a name="client-support-for-unified-labeling"></a>Prise en charge des clients pour l’étiquetage unifié

Assurez-vous que vous avez des [clients qui prennent en charge des étiquettes unifiées](#clients-and-services-that-support-unified-labeling) et, si nécessaire, préparez-vous à l’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et les centres d’administration (pour le client qui prennent en charge les étiquettes unifiées).

### <a name="policy-configuration"></a>Configuration de la stratégie

Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Les options de configuration de ces paramètres après la migration de votre étiquette sont les suivantes :

- Votre centre d’administration pour les étiquettes de sensibilité.
- [Office 365 Security & Compliance PowerShell](/powershell/exchange/office-365-scc/office-365-scc-powershell), que vous devez utiliser pour configurer les [Paramètres avancés du client](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    
> [!IMPORTANT]
> Les paramètres d’une étiquette migrée ne sont pas tous pris en charge par les centres d’administration. Suivez le tableau de la section [Paramètres d’étiquette non pris en charge dans les centres d’administration](#label-settings-that-are-not-supported-in-the-admin-centers) pour identifier ces paramètres et la procédure recommandée.
> 

### <a name="protection-templates"></a>Modèles de protection

- Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
- Si vous avez des étiquettes configurées pour un modèle prédéfini, modifiez ces étiquettes et sélectionnez l’option **Définir les autorisations** pour configurer les mêmes paramètres de protection que ceux de votre modèle. Les étiquettes comportant des modèles prédéfinis ne bloquent pas la migration des étiquettes, mais cette configuration n’est pas prise en charge dans les centres d’administration.
        
    > [!TIP]
    > Pour vous aider à reconfigurer ces étiquettes, il peut être utile de disposer de deux fenêtres de navigateur : une fenêtre dans laquelle vous sélectionnez le bouton **modifier le modèle** pour l’étiquette afin d’afficher les paramètres de protection, et l’autre fenêtre pour configurer les mêmes paramètres lorsque vous sélectionnez **définir les autorisations**.
    
- Après la migration d’une étiquette avec des paramètres de protection basés sur le Cloud, l’étendue résultante du modèle de protection est définie dans l’étendue définie dans le Portail Azure (ou à l’aide du module PowerShell AIPService) et l’étendue définie dans les centres d’administration. 

### <a name="display-names"></a>Noms complets

Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Les utilisateurs voient ce nom d’étiquette dans leurs applications. 

Les centres d’administration indiquent à la fois ce nom d’affichage et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous spécifiez lorsque l’étiquette est créée pour la première fois et cette propriété est utilisée par le service principal à des fins d’identification. Lorsque vous migrez vos étiquettes, le nom d’affichage reste le même et le nom de l’étiquette est renommé avec l’ID d’étiquette du Portail Azure.

#### <a name="conflicting-display-names"></a>Noms d’affichage en conflit

Avant de procéder à la migration, assurez-vous de ne pas avoir de noms d’affichage conflictuels une fois la migration terminée. Les noms d’affichage au même emplacement dans la hiérarchie d’étiquetage doivent être uniques. 

Par exemple, considérez la liste d’étiquettes suivante :

- **Public**
- **Général**
- **Confidentiel**
    - **Confidential\HR**
    - **Confidential\Finance**
- **Secret**
    - **Secret\HR**
    - **Secret\Finance**
    
Dans cette liste, **public**, **General**, **Confidential** et **secret** sont toutes des étiquettes parentes et ne peuvent pas avoir de noms en double. En outre, **Confidential\HR** et **Confidential\Finance** sont au même emplacement dans la hiérarchie et ne peuvent pas avoir de noms en double.

Toutefois, les sous-étiquettes sur différents parents, telles que **Confidential\HR** et **Secret\HR** , ne sont pas au même emplacement dans la hiérarchie, et peuvent donc avoir les mêmes noms individuels. 

### <a name="localized-strings-in-labels"></a>Chaînes localisées dans les étiquettes

Aucune chaîne localisée pour les étiquettes n’est migrée. Définissez de nouvelles chaînes localisées pour les étiquettes migrées à l’aide d’Office 365 Security & Compliance PowerShell et du paramètre *LocaleSettings* pour [Set-label](/powershell/module/exchange/policy-and-compliance/set-label).

### <a name="editing-migrated-labels-in-the-admin-centers"></a>Modification des étiquettes migrées dans les centres d’administration

Après la migration, tout modification d’une étiquette migrée sur le Portail Azure est automatiquement répercutée dans les centres d’administration. 

Toutefois, lorsque vous modifiez une étiquette migrée dans l’un des centres d’administration, vous devez revenir au volet Portail Azure, **Azure information protection-Unified étiquetage** , puis sélectionner **publier**. 

Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection (Classic) récupèrent les modifications apportées aux étiquettes.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Paramètres d’étiquette non pris en charge dans les centres d’administration

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée non pris en charge par le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. Si vous avez des étiquettes avec ces paramètres, une fois la migration terminée, utilisez les conseils d’administration de la dernière colonne avant de publier vos étiquettes dans l’un des centres d’administration référencés.

Si vous n’êtes pas sûr de la façon dont vos étiquettes sont configurées, affichez leurs paramètres dans le portail Azure. Si vous avez besoin d’aide, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Les clients Azure Information Protection (Classic) peuvent utiliser tous les paramètres d’étiquette indiqués sans aucun problème, car ils continuent de télécharger les étiquettes à partir du Portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié| Aide pour les centres d’administration|
|-------------------|---------------------------------------------|-------------------------|
|**État activé ou désactivé**<br /><br />Cet État n’est pas synchronisé avec les centres d’administration |Non applicable|L’équivalent est si l’étiquette est publiée ou non. |
|**Couleur d’étiquette que vous sélectionnez dans la liste ou que vous spécifiez avec un code RVB** |Oui|Aucune option de configuration pour les couleurs des étiquettes. Au lieu de cela, vous pouvez configurer les couleurs des étiquettes dans le Portail Azure ou utiliser [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|**Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini** |No|Aucune option de configuration pour les modèles prédéfinis. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|**Protection cloud avec des autorisations définies par l’utilisateur pour Word, Excel et PowerPoint** |Oui|Les centres d’administration disposent désormais d’une option de configuration pour les autorisations définies par l’utilisateur. <br /><br /> Si vous publiez une étiquette avec cette configuration, vérifiez les résultats de l’application de l’étiquette à partir du [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|**Protection basée sur hyok à l’aide des autorisations définies par l’utilisateur pour Outlook** (ne pas transférer) |No|Aucune option de configuration pour HYOK. Nous vous déconseillons de publier une étiquette avec cette configuration. Si vous le faites néanmoins, prenez connaissance des résultats de l’application de l’étiquette listés dans le [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|**Nom de police personnalisé, taille et couleur de police personnalisée par code RVB pour les marquages visuels** (en-tête, pied de page, filigrane)  |Oui|La configuration pour les marquages visuels est limitée à une liste de couleurs et de tailles de police. Vous pouvez publier cette étiquette sans rien changer, même si les valeurs configurées n’apparaissent pas dans les centres d’administration. <br /><br />Pour modifier ces options, utilisez l’applet [**de commande New-label**](/powershell/module/exchange/new-label) Office 365 Security & Compliance Center. Pour faciliter l’administration, envisagez de modifier la couleur de l’une des options listées dans les centres d’administration. <br /><br />**Remarque**: le centre d’administration de la conformité du centre de sécurité & prend en charge une liste prédéfinie de définitions de polices. Les polices et les couleurs personnalisées sont prises en charge uniquement par le biais de l’applet [**de commande New-label**](/powershell/module/exchange/new-label) Office 365 Security & Compliance Center. <br><br>Si vous travaillez avec le client classique, apportez ces modifications à votre étiquette dans la Portail Azure.|
|**Variables dans les marquages visuels** (en-tête, pied de page) |Oui|Cette configuration d’étiquette est prise en charge par les clients AIP et l’étiquetage Office intégré pour les applications Select. <br /><br />Si vous utilisez l’étiquetage intégré à l’aide d’une application qui ne prend pas en charge cette configuration et publiez cette étiquette sans modification, les variables s’affichent sous forme de texte sur les clients, au lieu d’afficher la valeur dynamique.<br /><br />Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables). |
|**Marquages visuels par application**|Oui|Cette configuration d’étiquette est prise en charge uniquement par les clients AIP, et non par l’étiquetage intégré d’Office. <br /><br />Si vous utilisez l’étiquetage intégré et que vous publiez cette étiquette sans modification, la configuration du marquage visuel s’affiche sous forme de texte de variable au lieu des marquages visuels que vous avez configurés pour s’afficher dans chaque application.  |
|**Protection « uniquement pour moi »**|Oui|Les centres d’administration ne vous permettent pas d’enregistrer les paramètres de chiffrement que vous appliquez maintenant, sans spécifier d’utilisateurs. Dans le Portail Azure, cette configuration génère une étiquette qui applique la [protection « juste pour moi »](configure-policy-protection.md#example-6-label-that-applies-just-for-me-protection). <br /><br /> Vous pouvez également créer une étiquette qui applique le chiffrement et spécifier un utilisateur avec des autorisations, puis modifier le modèle de protection associé à l’aide de PowerShell. Tout d’abord, utilisez l’applet [de commande New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) (Voir l’exemple 3), puis [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty#examples) avec le paramètre *RightsDefinitions* .|
|**Conditions et paramètres associés** <br /><br /> Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Non applicable|Reconfigurez vos conditions en utilisant l’étiquetage d’automatique comme configuration distincte des paramètres d’étiquette.|
| | | |

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Comparaison du comportement des paramètres de protection pour une étiquette

Utilisez le tableau suivant pour identifier la façon dont le même paramètre de protection pour une étiquette se comporte différemment, selon qu’elle est utilisée par le client Azure Information Protection Classic, le client d’étiquetage unifié Azure Information Protection ou par les applications Office qui ont des étiquettes intégrées (également appelées « étiquetage Office natif »). Les différences de comportement des étiquettes peuvent modifier votre décision de publier les étiquettes, en particulier lorsque vous avez un mélange de clients dans votre organisation.

Si vous n’êtes pas sûr de la façon dont vos paramètres de protection sont configurés, affichez leurs paramètres dans le volet **protection** , dans la portail Azure. Si vous avez besoin d’aide, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Les paramètres de protection qui se comportent de la même façon n’apparaissent pas dans le tableau, à ces exceptions près :
- Dans le cas d’applications Office avec étiquetage intégré, les étiquettes ne sont pas visibles dans l’Explorateur de fichiers à moins d’installer également le client d’étiquetage unifié Azure Information Protection.
- Dans le cas d’applications Office avec étiquetage intégré, si une protection a déjà été appliquée indépendamment d’une étiquette, elle est conservée[[1]](#footnote-1).

|Paramètre de protection pour une étiquette |Client Azure Information Protection Classic |Client d’étiquetage unifié Azure Information Protection| Applications Office avec étiquetage intégré
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|HYOK (AD RMS) avec un modèle :| Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection HYOK est appliquée aux documents et aux e-mails | Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers  <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |Visible dans Word, Excel, PowerPoint et Outlook <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1) |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée :<br /><br /> - La protection HYOK est appliquée aux documents et aux e-mails| Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Outlook :|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- « Ne pas transférer » avec la protection HYOK est appliqué aux e-mails|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br /> - La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|

###### <a name="footnote-1"></a>Note 1

Dans Outlook, la protection est conservée avec une exception : lorsqu’un e-mail a été protégé avec l’option Encrypt-Only, cette protection est supprimée.


###### <a name="footnote-2"></a>Note 2

La protection est supprimée si l’utilisateur a un droit d’utilisation ou un rôle qui prend en charge cette action :
- Le [droit d’utilisation](configure-usage-rights.md#usage-rights-and-descriptions) Exporter ou Contrôle total.
- Le rôle de [Émetteur Rights Management ou Propriétaire Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou de [super utilisateur](configure-super-users.md).

Si l’utilisateur n’a pas un de ces droits d’utilisation ou un de ces rôles, l’étiquette n’est pas appliquée et la protection d’origine est conservée.


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

Utilisez les instructions suivantes pour migrer vos étiquettes de locataire et de Azure Information Protection pour utiliser le magasin d’étiquetage unifié.

Vous devez être administrateur de la conformité, administrateur des données de conformité, administrateur de la sécurité ou administrateur général pour migrer vos étiquettes.

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. Dans l’option de menu **gérer** , sélectionnez **étiquetage unifié**.

3. Dans le volet d' **étiquetage Azure information protection-Unified** , sélectionnez **activer** et suivez les instructions en ligne.
    
    Si l’option d’activation n’est pas disponible, vérifiez l' **État d’étiquetage unifié**: Si vous voyez **activé**, votre locataire utilise déjà le magasin d’étiquetage unifié et il n’est pas nécessaire de migrer vos étiquettes.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Toutefois, vous devez d’abord [publier ces étiquettes](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy) dans l’un des centres d’administration : Office 365 Security & Compliance center, Microsoft 365 Security center ou Microsoft 365 Compliance Center.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors de la Portail Azure, pour les clients Azure Information Protection (Classic), revenez à ce volet d' **étiquetage Azure information protection-Unified** , puis sélectionnez **publier**.

### <a name="copy-policies"></a>Copier les stratégies

Une fois que vous avez migré vos étiquettes, vous pouvez sélectionner une option pour copier les stratégies. Si vous sélectionnez cette option, une copie unique de vos stratégies avec les paramètres de [stratégie](configure-policy-settings.md) et les [Paramètres client avancés](./rms-client/client-admin-guide-customizations.md#available-advanced-classic-client-settings) est envoyée au centre d’administration où vous gérez vos étiquettes : Office 365 Security & Compliance Center, Microsoft 365 Security Center, Microsoft 365 Compliance Center. 

Les stratégies ont été correctement copiées avec leurs paramètres et les étiquettes sont ensuite automatiquement publiées sur les utilisateurs et les groupes qui ont été affectés aux stratégies dans la Portail Azure. Notez que, pour la stratégie globale, il s’agit de tous les utilisateurs. Si vous n’êtes pas prêt à publier les étiquettes migrées dans les stratégies copiées, une fois les stratégies copiées, vous pouvez supprimer les étiquettes des stratégies d’étiquette dans le centre d’étiquetage de votre administrateur.

Avant de sélectionner l’option **copier les stratégies (version préliminaire)** dans le volet d' **étiquetage Azure information protection-Unified** , tenez compte des points suivants :

- L’option **copier les stratégies (** préversion) n’est pas disponible tant que l’étiquetage unifié n’est pas activé pour votre locataire.

- Vous ne pouvez pas sélectionner de manière sélective les stratégies et les paramètres à copier. Toutes les stratégies (stratégie **globale** et stratégies délimitées) sont automatiquement sélectionnées pour être copiées, et tous les paramètres pris en charge en tant que paramètres de stratégie d’étiquette sont copiés. Si vous disposez déjà d’une stratégie d’étiquette portant le même nom, elle sera remplacée par les paramètres de stratégie de la Portail Azure.

- Certains paramètres client avancés ne sont pas copiés, car pour le client d’étiquetage unifié Azure Information Protection, ils sont pris en charge en tant que *Paramètres avancés d’étiquette* plutôt qu’en tant que paramètres de stratégie. Vous pouvez configurer ces paramètres avancés des étiquettes avec [Microsoft 365 Security & Compliance Center PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). Les paramètres avancés du client qui ne sont pas copiés sont les suivants :
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Contrairement à la migration des étiquettes où les modifications ultérieures apportées aux étiquettes sont synchronisées, l’action **copier les stratégies** ne synchronise pas les modifications ultérieures apportées à vos stratégies ou paramètres de stratégie. Vous pouvez répéter l’action copier la stratégie après avoir apporté des modifications au Portail Azure, et les stratégies existantes et leurs paramètres seront à nouveau remplacés. Ou utilisez les applets de commande Set-LabelPolicy ou Set-Label avec le paramètre *AdvancedSettings* d’Office 365 Security & Compliance Center PowerShell.

- L’action **copier les stratégies** vérifie les éléments suivants pour chaque stratégie avant de la copier :
    
    - Les utilisateurs et les groupes attribués à la stratégie sont actuellement dans Azure AD. Si un ou plusieurs comptes sont absents, la stratégie n’est pas copiée. L’appartenance au groupe n’est pas vérifiée.
    
    - La stratégie globale contient au moins une étiquette. Étant donné que les centres d’étiquetage des administrateurs ne prennent pas en charge les stratégies d’étiquette sans étiquette, une stratégie globale sans étiquette n’est pas copiée.

- Si vous copiez des stratégies, puis que vous les supprimez de votre centre d’étiquetage des administrateurs, attendez au moins deux heures avant d’utiliser l’action **copier les stratégies** pour garantir un temps suffisant pour la réplication de la suppression.

- Les stratégies copiées à partir de Azure Information Protection n’ont pas le même nom, mais elles sont nommées avec un préfixe de **AIP_**. Les noms de stratégie ne peuvent pas être modifiés par la suite. 

Pour plus d’informations sur la configuration des paramètres de stratégie, des paramètres client avancés et des paramètres d’étiquette pour le client d’étiquetage unifié Azure Information Protection, consultez [configurations personnalisées pour le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-customizations.md) à partir du Guide de l’administrateur.

> [!NOTE]
> Azure Information Protection la prise en charge de la copie des stratégies est actuellement disponible en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 

### <a name="clients-and-services-that-support-unified-labeling"></a>Clients et services prenant en charge l’étiquetage unifié

Pour vérifier si les clients et les services que vous utilisez prennent en charge l’étiquetage unifié, reportez-vous à leur documentation pour vérifier s’ils peuvent utiliser des étiquettes de sensibilité publiées à partir de l’un des centres d’administration : Office 365 Security & Compliance Center, Microsoft 365 Security Center ou Microsoft 365 Compliance Center. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>Les clients qui prennent en charge l’étiquetage unifié sont :

- **Le [client d’étiquetage unifié Azure information protection pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md)** 

    Pour obtenir une comparaison entre ce client et le client Azure Information Protection Classic, consultez [comparer les solutions d’étiquetage pour les ordinateurs Windows](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers).

- **Applications d’Office qui se trouvent dans des étapes de disponibilité différentes** 

    Pour plus d’informations, consultez [prise en charge des fonctionnalités d’étiquette de sensibilité dans les applications](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps) de la documentation de conformité Microsoft 365.
    
- **Applications de fournisseurs de logiciels et de développeurs** qui utilisent le [Kit de développement logiciel (SDK) Microsoft information protection](/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>Les services qui prennent en charge l’étiquetage unifié sont :

- **[Power BI](/power-bi/admin/service-security-data-protection-overview)**

- **Office Online et Outlook sur le Web**

    Pour plus d’informations, consultez [activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

- **Microsoft SharePoint, OneDrive entreprise ou scolaire, OneDrive pour la famille, les équipes et les groupes de Microsoft 365**
    
    Pour plus d’informations, consultez [utiliser des étiquettes de sensibilité pour protéger du contenu dans Microsoft Teams, les groupes de Microsoft 365 et les sites SharePoint](/microsoft-365/compliance/sensitivity-labels-teams-groups-sites).

- **Microsoft Defender - Protection avancée contre les menaces**

- **Microsoft Cloud App Security**
    
    Ce service prend en charge les étiquettes avant la migration vers le magasin d’étiquetage unifié et après la migration, selon la logique suivante :
    
    - Si les centres d’administration ont des étiquettes de sensibilité, ces étiquettes sont récupérées à partir des centres d’administration. Pour que ces étiquettes puissent être sélectionnées dans Cloud App Security, au moins une étiquette doit être publiée sur au moins un utilisateur.
    
    - Si les centres d’administration n’ont pas d’étiquette de sensibilité, Azure Information Protection étiquettes sont récupérées à partir du Portail Azure.

- **Services des éditeurs de logiciels et des développeurs** qui utilisent le [Kit de développement logiciel (SDK) Microsoft information protection](/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes

**Conseils et astuces de notre équipe de l’expérience utilisateur**:

- Billet de blog : [comprendre la migration unifiée d’étiquetage](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)

- Webinaire : [enregistrement d’étiquettes, de jeux et de FAQ unifiés](https://github.com/nihendle/MIP-Comp/tree/master/MIP/Webinars/Unified%20Labeling%20Migration)


**À propos des étiquettes de sensibilité**:
- [En savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels)
- [Créez et configurez des étiquettes de sensibilité et leurs stratégies](/microsoft-365/compliance/create-sensitivity-labels).

**Déployez le client d’étiquetage unifié AIP**:

Si vous ne l’avez pas déjà fait, installez le client d’étiquetage unifié Azure Information Protection. 

Pour plus d'informations, consultez les pages suivantes :

- [Azure Information Protection l’historique des versions et la stratégie de support du client d’étiquetage unifié](rms-client/unifiedlabelingclient-version-release-history.md)
- [Guide de l’administrateur du client d’étiquetage unifié Azure Information Protection](rms-client/clientv2-admin-guide.md)
- [Guide de l’utilisateur d’étiquetage unifié Azure Information Protection](rms-client/clientv2-user-guide.md)
