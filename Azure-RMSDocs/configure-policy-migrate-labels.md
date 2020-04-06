---
title: Migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée-AIP
description: Migrez Azure Information Protection étiquettes vers des étiquettes de sensibilité unifiée pour les clients et les services qui prennent en charge Microsoft Information Protection Framework.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ffb0d3b468940cb0497b0d7081520e06942bc096
ms.sourcegitcommit: c0fd00b057d155d6f2ed3a3ef5942d593b5be5c9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/05/2020
ms.locfileid: "80670194"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>Comment migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Migrez Azure Information Protection étiquettes vers la plateforme d’étiquetage unifiée pour pouvoir les utiliser en tant qu’étiquettes de sensibilité par [les clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling).

> [!NOTE]
> Si votre abonnement Azure Information Protection est relativement nouveau, vous n’aurez peut-être pas besoin de migrer des étiquettes, car votre locataire est déjà sur la plateforme d’étiquetage unifiée. Pour plus d’informations, consultez [Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Après avoir migré vos étiquettes, vous ne verrez aucune différence avec le client Azure Information Protection (Classic), car ce client continue de télécharger les étiquettes avec la stratégie de Azure Information Protection à partir du Portail Azure. Toutefois, vous pouvez maintenant utiliser les étiquettes avec le client d’étiquetage unifié Azure Information Protection et d’autres clients et services qui utilisent des étiquettes de sensibilité.

Avant de lire les instructions pour migrer vos étiquettes, vous trouverez peut-être les questions fréquemment posées suivantes :

- [Quelle est la différence entre les étiquettes dans Azure Information Protection et les étiquettes dans Office 365 ?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Quand est-il approprié de migrer mes étiquettes ?](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Rôles d’administration qui prennent en charge la plateforme d’étiquetage unifiée

Si vous utilisez des rôles d’administrateur pour l’administration déléguée dans votre organisation, vous devrez peut-être effectuer certaines modifications pour la plateforme d’étiquetage unifiée :

Le [rôle Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) de **Azure information protection administrateur** (anciennement **information protection administrateur**) n’est pas pris en charge par la plateforme d’étiquetage unifiée. Si ce rôle d’administration est utilisé dans votre organisation pour gérer Azure Information Protection, ajoutez les utilisateurs qui possèdent ce rôle aux rôles Azure AD de l’administrateur de la **conformité**, à l’administrateur des **données de conformité**ou à l’administrateur de la **sécurité**. Si vous avez besoin d’aide, consultez [Donner aux utilisateurs accès au Centre de sécurité et de conformité Office 365](https://docs.microsoft.com/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center). Vous pouvez également attribuer ces rôles dans le portail Azure AD, le centre de sécurité Microsoft 365 et le centre de conformité Microsoft 365.

Au lieu d’utiliser des rôles, dans les centres d’administration, vous pouvez créer un nouveau groupe de rôles pour ces utilisateurs et ajoutez les rôles **Administrateur d’étiquette de sensibilité** ou **Configuration de l’organisation** à ce groupe.

Si vous ne donnez pas accès aux centres d’administration à ces utilisateurs suivant l’une de ces configurations, ils ne pourront pas configurer Azure Information Protection dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux de votre locataire pourront continuer à gérer les étiquettes et les stratégies sur le Portail Azure et dans les centres d’administration une fois vos étiquettes migrées.

## <a name="before-you-begin"></a>Avant de commencer

La migration des étiquettes présente de nombreux avantages, mais est irréversible. Assurez-vous que vous avez pris connaissance des modifications et des considérations suivantes :

- Assurez-vous que vous avez des [clients qui prennent en charge des étiquettes unifiées](#clients-and-services-that-support-unified-labeling) et, si nécessaire, préparez-vous à l’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et les centres d’administration (pour le client qui prennent en charge les étiquettes unifiées).

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Les options de configuration de ces paramètres après la migration de votre étiquette sont les suivantes :
    - Votre centre d’administration pour les étiquettes de sensibilité.
    - [Office 365 Security & Compliance PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), que vous devez utiliser pour configurer les [Paramètres avancés du client](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    

- Les paramètres d’une étiquette migrée ne sont pas tous pris en charge par les centres d’administration. Suivez le tableau de la section [Paramètres d’étiquette non pris en charge dans les centres d’administration](#label-settings-that-are-not-supported-in-the-admin-centers) pour identifier ces paramètres et la procédure recommandée.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Si vous avez des étiquettes configurées pour un modèle prédéfini, modifiez ces étiquettes et sélectionnez l’option **Définir les autorisations** pour configurer les mêmes paramètres de protection que ceux de votre modèle. Les étiquettes comportant des modèles prédéfinis ne bloquent pas la migration des étiquettes, mais cette configuration n’est pas prise en charge dans les centres d’administration.
        
        Conseil : pour vous aider à reconfigurer ces étiquettes, il peut être utile de disposer de deux fenêtres de navigateur : une fenêtre dans laquelle vous sélectionnez le bouton **modifier le modèle** pour l’étiquette afin d’afficher les paramètres de protection, et l’autre fenêtre pour configurer les mêmes paramètres lorsque vous sélectionnez **définir les autorisations**.
    
    - Après la migration d’une étiquette avec des paramètres de protection basés sur le Cloud, l’étendue résultante du modèle de protection est définie dans l’étendue définie dans le Portail Azure (ou à l’aide du module PowerShell AIPService) et l’étendue définie dans les centres d’administration. 

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Les utilisateurs voient ce nom d’étiquette dans leurs applications. Les centres d’administration indiquent à la fois ce nom d’affichage et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous spécifiez lorsque l’étiquette est créée pour la première fois et cette propriété est utilisée par le service principal à des fins d’identification. Lorsque vous migrez vos étiquettes, le nom d’affichage reste le même et le nom de l’étiquette est renommé avec l’ID d’étiquette du Portail Azure.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Définissez de nouvelles chaînes localisées pour les étiquettes migrées à l’aide d’Office 365 Security & Compliance PowerShell et du paramètre *LocaleSettings* pour [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- Après la migration, tout modification d’une étiquette migrée sur le Portail Azure est automatiquement répercutée dans les centres d’administration. Toutefois, lorsque vous modifiez une étiquette migrée dans l’un des centres d’administration, vous devez revenir au volet Portail Azure, **Azure information protection-Unified étiquetage** , puis sélectionner **publier**. Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection (Classic) récupèrent les modifications apportées aux étiquettes.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Paramètres d’étiquette non pris en charge dans les centres d’administration

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée non pris en charge par le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. Si vous avez des étiquettes avec ces paramètres, une fois la migration terminée, utilisez les conseils d’administration de la dernière colonne avant de publier vos étiquettes dans l’un des centres d’administration référencés.

Si vous n’êtes pas sûr de la façon dont vos étiquettes sont configurées, affichez leurs paramètres dans le portail Azure. Si vous avez besoin d’aide, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Les clients Azure Information Protection (Classic) peuvent utiliser tous les paramètres d’étiquette indiqués sans aucun problème, car ils continuent de télécharger les étiquettes à partir du Portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié| Aide pour les centres d’administration|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Cet État n’est pas synchronisé avec les centres d’administration |Not applicable|L’équivalent est si l’étiquette est publiée ou non. |
|Couleur d’étiquette que vous sélectionnez dans la liste ou que vous spécifiez avec un code RVB |Oui|Aucune option de configuration pour les couleurs des étiquettes. Au lieu de cela, vous pouvez configurer les couleurs des étiquettes dans le Portail Azure ou utiliser [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Aucune option de configuration pour les modèles prédéfinis. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Protection cloud avec des autorisations définies par l’utilisateur pour Word, Excel et PowerPoint |Oui|Les centres d’administration disposent désormais d’une option de configuration pour les autorisations définies par l’utilisateur. <br /><br /> Si vous publiez une étiquette avec cette configuration, vérifiez les résultats de l’application de l’étiquette à partir du [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protection HYOK avec des autorisations définies par l’utilisateur dans Outlook (Ne pas transférer) |Non|Aucune option de configuration pour HYOK. Nous vous déconseillons de publier une étiquette avec cette configuration. Si vous le faites néanmoins, prenez connaissance des résultats de l’application de l’étiquette listés dans le [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Taille de police personnalisée et couleur de police personnalisée par code RVB pour les marquages visuels (en-tête, pied de page, filigrane)  |Oui|La configuration pour les marquages visuels est limitée à une liste de couleurs et de tailles de police. Vous pouvez publier cette étiquette sans rien changer, même si les valeurs configurées n’apparaissent pas dans les centres d’administration. <br /><br />Pour changer ces options, vous pouvez utiliser le portail Azure. Cependant, pour des raisons de simplicité d’administration, vous pouvez remplacer la couleur par l’une des options listées dans les centres d’administration. <br /><br /> Le type de police **personnalisé** (Arial, Courier et autres) n’est pas pris en charge par le client d’étiquetage unifié|
|Variables dans les marquages visuels (en-tête, pied de page)|Oui|Si vous publiez cette étiquette sans changement, les variables s’affichent sous forme de texte sur les clients au lieu d’afficher les valeurs dynamiques. Avant de publier l’étiquette, modifiez les chaînes pour supprimer les variables.|
|Marquages visuels par application|Oui|Si vous publiez cette étiquette sans changement, les variables d’application s’affichent sous forme de texte sur les clients dans toutes les applications, au lieu d’afficher vos chaînes de texte sur les applications choisies. Publiez cette étiquette seulement si elle convient pour toutes les applications, et modifiez les chaînes pour supprimer les variables d’application.|
|Protection « uniquement pour moi » |Oui|Les centres d’administration ne vous permettent pas d’enregistrer les paramètres de chiffrement que vous appliquez maintenant, sans spécifier d’utilisateurs. Dans le Portail Azure, cette configuration génère une étiquette qui applique la [protection « juste pour moi »](configure-policy-protection.md#example-6-label-that-applies-just-for-me-protection). <br /><br /> Vous pouvez également créer une étiquette qui applique le chiffrement et spécifier un utilisateur avec des autorisations, puis modifier le modèle de protection associé à l’aide de PowerShell. Tout d’abord, utilisez l’applet [de commande New-AipServiceRightsDefinition](https://docs.microsoft.com/powershell/module/aipservice/new-aipservicerightsdefinition) (Voir l’exemple 3), puis [Set-AipServiceTemplateProperty](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicetemplateproperty?view=azureipps#examples) avec le paramètre *RightsDefinitions* .|
|Conditions et paramètres associés <br /><br /> Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Not applicable|Reconfigurez vos conditions en utilisant l’étiquetage d’automatique comme configuration distincte des paramètres d’étiquette.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Comparaison du comportement des paramètres de protection pour une étiquette

Utilisez le tableau suivant pour identifier le comportement du même paramètre de protection pour une étiquette, selon qu’elle est utilisée par le client Azure Information Protection (Classic), le Azure Information Protection client d’étiquetage unifié ou par les applications Office qui ont des étiquettes intégrées (également appelées « étiquetage Office natif »). Les différences de comportement des étiquettes peuvent modifier votre décision de publier les étiquettes, en particulier lorsque vous avez un mélange de clients dans votre organisation.

Si vous n’êtes pas sûr de la façon dont vos paramètres de protection sont configurés, affichez leurs paramètres dans le volet **protection** , dans la portail Azure. Si vous avez besoin d’aide, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Les paramètres de protection qui se comportent de la même façon n’apparaissent pas dans le tableau, à ces exceptions près :
- Dans le cas d’applications Office avec étiquetage intégré, les étiquettes ne sont pas visibles dans l’Explorateur de fichiers à moins d’installer également le client d’étiquetage unifié Azure Information Protection.
- Dans le cas d’applications Office avec étiquetage intégré, si une protection a déjà été appliquée indépendamment d’une étiquette, elle est conservée[[1]](#footnote-1).

|Paramètre de protection pour une étiquette |Client Azure Information Protection (classique) |Client d’étiquetage unifié Azure Information Protection| Applications Office avec étiquetage intégré
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (clé cloud) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs sont invités à définir des autorisations personnalisées qui sont ensuite appliquées comme protection avec une clé cloud| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs sont invités à définir des autorisations personnalisées qui sont ensuite appliquées comme protection avec une clé cloud|Visible dans Word, Excel, PowerPoint et Outlook : <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs ne sont pas invités à définir des autorisations personnalisées et aucune protection n’est appliquée. <br /><br /> - Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|
|HYOK (AD RMS) avec un modèle :| Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection HYOK est appliquée aux documents et aux e-mails | Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers  <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |Visible dans Word, Excel, PowerPoint et Outlook <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1) |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée :<br /><br /> - La protection HYOK est appliquée aux documents et aux e-mails| Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Outlook :|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- « Ne pas transférer » avec la protection HYOK est appliqué aux e-mails|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br /> - La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|

###### <a name="footnote-1"></a>Note de bas de page 1

Dans Outlook, la protection est conservée avec une exception : lorsqu’un e-mail a été protégé avec l’option de chiffrement seul, cette protection est supprimée.


###### <a name="footnote-2"></a>Note 2

La protection est supprimée si l’utilisateur a un droit d’utilisation ou un rôle qui prend en charge cette action :
- Le [droit d’utilisation](configure-usage-rights.md#usage-rights-and-descriptions) Exporter ou Contrôle total.
- Le rôle de [Émetteur Rights Management ou Propriétaire Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou de [super utilisateur](configure-super-users.md).

Si l’utilisateur n’a pas un de ces droits d’utilisation ou un de ces rôles, l’étiquette n’est pas appliquée et la protection d’origine est conservée.


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

Utilisez les instructions suivantes pour migrer vos étiquettes de locataire et de Azure Information Protection pour utiliser le magasin d’étiquetage unifié.

Vous devez être administrateur de la conformité, administrateur des données de conformité, administrateur de la sécurité ou administrateur général pour migrer vos étiquettes.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. Dans l’option de menu **gérer** , sélectionnez **étiquetage unifié**.

3. Dans le volet d' **étiquetage Azure information protection-Unified** , sélectionnez **activer** et suivez les instructions en ligne.
    
    Si l’option d’activation n’est pas disponible, vérifiez l' **État d’étiquetage unifié**: Si vous voyez **activé**, votre locataire utilise déjà le magasin d’étiquetage unifié et il n’est pas nécessaire de migrer vos étiquettes.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Toutefois, vous devez d’abord [publier ces étiquettes](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy) dans l’un des centres d’administration : Office 365 Centre de sécurité et de conformité, Microsoft 365 Security center ou Microsoft 365 Center Compliance Center.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors de la Portail Azure, pour les clients Azure Information Protection (Classic), revenez à ce volet d' **étiquetage Azure information protection-Unified** , puis sélectionnez **publier**.

### <a name="copy-policies"></a>Copier les stratégies

> [!NOTE]
> Cette option est en version préliminaire et sujette à modification.

Une fois que vous avez migré vos étiquettes, vous pouvez sélectionner une option pour copier les stratégies. Si vous sélectionnez cette option, une copie unique de vos stratégies avec les paramètres de [stratégie](configure-policy-settings.md) et les [Paramètres client avancés](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings) est envoyée au centre d’administration où vous gérez vos étiquettes : Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center, Microsoft 365 Compliance Center. 

Les stratégies ont été correctement copiées avec leurs paramètres et les étiquettes sont ensuite automatiquement publiées sur les utilisateurs et les groupes qui ont été affectés aux stratégies dans la Portail Azure. Notez que, pour la stratégie globale, il s’agit de tous les utilisateurs. Si vous n’êtes pas prêt à publier les étiquettes migrées dans les stratégies copiées, une fois les stratégies copiées, vous pouvez supprimer les étiquettes des stratégies d’étiquette dans le centre d’étiquetage de votre administrateur.

Avant de sélectionner l’option **copier les stratégies (version préliminaire)** dans le volet d' **étiquetage Azure information protection-Unified** , tenez compte des points suivants :

- L’option **copier les stratégies (** préversion) n’est pas disponible tant que l’étiquetage unifié n’est pas activé pour votre locataire.

- Vous ne pouvez pas sélectionner de manière sélective les stratégies et les paramètres à copier. Toutes les stratégies (stratégie **globale** et stratégies délimitées) sont automatiquement sélectionnées pour être copiées, et tous les paramètres pris en charge en tant que paramètres de stratégie d’étiquette sont copiés. Si vous disposez déjà d’une stratégie d’étiquette portant le même nom, elle sera remplacée par les paramètres de stratégie de la Portail Azure.

- Certains paramètres client avancés ne sont pas copiés, car pour le client d’étiquetage unifié Azure Information Protection, ils sont pris en charge en tant que *Paramètres avancés d’étiquette* plutôt qu’en tant que paramètres de stratégie. Vous pouvez configurer ces paramètres avancés d’étiquette avec [Office 365 Centre de sécurité et de conformité PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). Les paramètres avancés du client qui ne sont pas copiés sont les suivants :
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Contrairement à la migration des étiquettes où les modifications ultérieures apportées aux étiquettes sont synchronisées, l’action **copier les stratégies** ne synchronise pas les modifications ultérieures apportées à vos stratégies ou paramètres de stratégie. Vous pouvez répéter l’action copier la stratégie après avoir apporté des modifications au Portail Azure, et les stratégies existantes et leurs paramètres seront à nouveau remplacés. Ou utilisez les applets de commande Set-LabelPolicy ou Set-label avec le paramètre *AdvancedSettings* d’Office 365 Centre de sécurité et de conformité PowerShell.

- L’action **copier les stratégies** vérifie les éléments suivants pour chaque stratégie avant de la copier :
    
    - Les utilisateurs et les groupes attribués à la stratégie sont actuellement dans Azure AD. Si un ou plusieurs comptes sont absents, la stratégie n’est pas copiée. L’appartenance au groupe n’est pas vérifiée.
    
    - La stratégie globale contient au moins une étiquette. Étant donné que les centres d’étiquetage des administrateurs ne prennent pas en charge les stratégies d’étiquette sans étiquette, une stratégie globale sans étiquette n’est pas copiée.

- Si vous copiez des stratégies, puis que vous les supprimez de votre centre d’étiquetage des administrateurs, attendez au moins deux heures avant d’utiliser l’action **copier les stratégies** pour garantir un temps suffisant pour la réplication de la suppression.

- Les stratégies copiées à partir de Azure Information Protection n’ont pas le même nom, mais elles sont nommées avec un préfixe de **AIP_** . Les noms de stratégie ne peuvent pas être modifiés par la suite. 

Pour plus d’informations sur la configuration des paramètres de stratégie, des paramètres client avancés et des paramètres d’étiquette pour le client d’étiquetage unifié Azure Information Protection, consultez [configurations personnalisées pour le client d’étiquetage unifié Azure information protection](./rms-client/clientv2-admin-guide-customizations.md) à partir du Guide de l’administrateur.

### <a name="clients-and-services-that-support-unified-labeling"></a>Clients et services prenant en charge l’étiquetage unifié

Pour vérifier si les clients et les services que vous utilisez prennent en charge l’étiquetage unifié, reportez-vous à leur documentation pour vérifier s’ils peuvent utiliser des étiquettes de sensibilité publiées à partir de l’un des centres d’administration : Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center ou Microsoft 365 Center Compliance Center. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>Les clients qui prennent en charge l’étiquetage unifié sont :

- Le [Azure information protection client d’étiquetage unifié pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Pour obtenir une comparaison entre ce client et le client Azure Information Protection (Classic), consultez [comparer les clients d’étiquetage pour les ordinateurs Windows](./rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers).

- Applications Office qui se trouvent à différentes phases de disponibilité. Pour plus d’informations, consultez [prise en charge des fonctionnalités d’étiquette de sensibilité dans les applications](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps) de la documentation de conformité Microsoft 365.
    
- Applications d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>Les services qui prennent en charge l’étiquetage unifié sont :

- [Power BI (en préversion)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)

- Office Online (en version préliminaire) et Outlook sur le Web

- SharePoint Online, OneDrive entreprise, Microsoft teams et les groupes Office 365 (en version préliminaire)
    
    Pour plus d’informations, consultez [utiliser des étiquettes de sensibilité avec Microsoft Teams, les groupes office 365 et les sites SharePoint (version préliminaire publique)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites) et [activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive (version préliminaire publique)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    Ce service prend en charge les étiquettes avant la migration vers le magasin d’étiquetage unifié et après la migration, selon la logique suivante :
    
    - Si les centres d’administration ont des étiquettes de sensibilité, ces étiquettes sont récupérées à partir des centres d’administration. Pour que ces étiquettes puissent être sélectionnées dans Cloud App Security, au moins une étiquette doit être publiée sur au moins un utilisateur.
    
    - Si les centres d’administration n’ont pas d’étiquette de sensibilité, Azure Information Protection étiquettes sont récupérées à partir du Portail Azure.

- Services d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes :

Pour obtenir des conseils supplémentaires et des conseils de notre équipe de l’expérience utilisateur, consultez les ressources suivantes :

- Billet de blog : [comprendre la migration unifiée d’étiquetage](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)

- Webinaire : [enregistrement d’étiquettes, de jeux et de FAQ unifiés](https://github.com/nihendle/MIP-Comp/tree/master/MIP/Webinars/Unified%20Labeling%20Migration)

Pour plus d’informations sur vos étiquettes migrées qui peuvent maintenant être configurées et publiées dans l’un des centres d’administration d’étiquetage, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) et [créer et configurer des étiquettes de sensibilité et leurs stratégies](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels).

Si vous ne l’avez pas déjà fait, installez le client d’étiquetage unifié Azure Information Protection. Pour obtenir des informations sur la version, un guide d’administration et un guide de l’utilisateur, consultez [Azure information protection le client d’étiquetage unifié pour Windows](./rms-client/aip-clientv2.md).
