---
title: Migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée-AIP
description: Migrez Azure Information Protection étiquettes vers des étiquettes de sensibilité unifiée pour les clients et les services qui prennent en charge Microsoft Information Protection Framework.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1cdeb5fec9ea57decf319b9d65104a5a334a0585
ms.sourcegitcommit: 32ec752f3bda160011c48c82e24f31ffffe5d6ac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70888077"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>Comment migrer des étiquettes Azure Information Protection vers des étiquettes de sensibilité unifiée

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Migrez vos étiquettes dans Azure Information Protection afin de pouvoir les utiliser en tant qu’étiquettes de sensibilité par [les clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling).

Ces étiquettes peuvent ensuite être utilisées par le client d’étiquetage unifié Azure Information Protection. Si vous continuez à utiliser le client Azure Information Protection (Classic), ce client continue de télécharger les étiquettes avec la stratégie de Azure Information Protection à partir du Portail Azure.

Avant de lire les instructions pour migrer vos étiquettes, vous trouverez peut-être les questions fréquemment posées suivantes:

- [Quelle est la différence entre les étiquettes dans Azure Information Protection et celles dans Office 365 ?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Quand est-il approprié de migrer mes étiquettes ?](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Rôles d’administration qui prennent en charge la plateforme d’étiquetage unifiée

Si vous utilisez des rôles d’administrateur pour l’administration déléguée dans votre organisation, vous devrez peut-être effectuer certaines modifications pour la plateforme d’étiquetage unifiée:

Le [rôle Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) de **Azure information protection administrateur** (anciennement **information protection administrateur**) n’est pas pris en charge par la plateforme d’étiquetage unifiée. Si ce rôle d’administration est utilisé dans votre organisation, ajoutez les utilisateurs qui possèdent ce rôle aux rôles de Azure AD de l’administrateur de la **conformité**, de l’administrateur des **données de conformité**ou de l’administrateur de la **sécurité**. Si vous avez besoin d’aide, consultez [Donner aux utilisateurs accès au Centre de sécurité et de conformité Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center). Vous pouvez également attribuer ces rôles dans le portail Azure AD, le centre de sécurité Microsoft 365 et le centre de conformité Microsoft 365.

Au lieu d’utiliser des rôles, dans les centres d’administration, vous pouvez créer un nouveau groupe de rôles pour ces utilisateurs et ajoutez les rôles **Administrateur d’étiquette de sensibilité** ou **Configuration de l’organisation** à ce groupe.

Si vous ne donnez pas accès aux centres d’administration à ces utilisateurs suivant l’une de ces configurations, ils ne pourront pas configurer Azure Information Protection dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux de votre locataire pourront continuer à gérer les étiquettes et les stratégies sur le Portail Azure et dans les centres d’administration une fois vos étiquettes migrées.

## <a name="before-you-begin"></a>Avant de commencer

La migration des étiquettes présente de nombreux avantages, mais est irréversible. Assurez-vous que vous avez pris connaissance des modifications et des considérations suivantes :

- Assurez-vous que vous avez des [clients qui prennent en charge des étiquettes unifiées](#clients-and-services-that-support-unified-labeling) et, si nécessaire, préparez-vous à l’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et les centres d’administration (pour le client qui prennent en charge les étiquettes unifiées).

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Les options de configuration de ces paramètres après la migration de votre étiquette sont les suivantes:
    - Votre centre d’administration pour les étiquettes de sensibilité.
    - [Office 365 Security & Compliance PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), que vous devez utiliser pour configurer les [Paramètres avancés du client](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    

- Les paramètres d’une étiquette migrée ne sont pas tous pris en charge par les centres d’administration. Suivez le tableau de la section [Paramètres d’étiquette non pris en charge dans les centres d’administration](#label-settings-that-are-not-supported-in-the-admin-centers) pour identifier ces paramètres et la procédure recommandée.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Si vous avez des étiquettes configurées pour un modèle prédéfini, modifiez ces étiquettes et sélectionnez l’option **Définir les autorisations** pour configurer les mêmes paramètres de protection que ceux de votre modèle. Les étiquettes comportant des modèles prédéfinis ne bloquent pas la migration des étiquettes, mais cette configuration n’est pas prise en charge dans les centres d’administration.
        
        Conseil : Pour reconfigurer ces étiquettes plus facilement, vous pouvez utiliser deux fenêtres de navigateur : Une fenêtre dans laquelle vous sélectionnez le bouton **Modifier le modèle** de l’étiquette pour afficher les paramètres de protection, et l’autre fenêtre pour configurer les mêmes paramètres quand vous sélectionnez **Définir des autorisations**.
    
    - Après la migration d’une étiquette avec des paramètres de protection basés sur le Cloud, l’étendue résultante du modèle de protection est définie dans l’étendue définie dans le Portail Azure (ou à l’aide du module PowerShell AIPService) et l’étendue définie dans les centres d’administration. 

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Les utilisateurs voient ce nom d’étiquette dans leurs applications. Les centres d’administration indiquent à la fois ce nom d’affichage et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous spécifiez lorsque l’étiquette est créée pour la première fois et cette propriété est utilisée par le service principal à des fins d’identification. Lorsque vous migrez vos étiquettes, le nom d’affichage reste le même et le nom de l’étiquette est renommé avec l’ID d’étiquette du Portail Azure.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Définissez de nouvelles chaînes localisées pour les étiquettes migrées à l’aide d’Office 365 Security & Compliance PowerShell et du paramètre *LocaleSettings* pour [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- Après la migration, tout modification d’une étiquette migrée sur le Portail Azure est automatiquement répercutée dans les centres d’administration. Si en revanche vous modifiez une étiquette migrée dans l’un des centres d’administration, vous devez revenir sur le Portail Azure, dans le panneau **Azure Information Protection – Étiquetage unifié**, puis sélectionner **Publier**. Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection (Classic) récupèrent les modifications apportées aux étiquettes.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Paramètres d’étiquette non pris en charge dans les centres d’administration

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée non pris en charge par le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. Si vous avez des étiquettes avec ces paramètres, une fois la migration terminée, utilisez les conseils d’administration de la dernière colonne avant de publier vos étiquettes dans l’un des centres d’administration référencés.

Si vous n’êtes pas sûr de la façon dont vos étiquettes sont configurées, affichez leurs paramètres dans le portail Azure. Si vous avez besoin d’aide, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Les clients Azure Information Protection (Classic) peuvent utiliser tous les paramètres d’étiquette indiqués sans aucun problème, car ils continuent de télécharger les étiquettes à partir du Portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié| Aide pour les centres d’administration|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Cet État n’est pas synchronisé avec les centres d’administration |Non applicable|L’équivalent est si l’étiquette est publiée ou non. |
|Couleur d’étiquette que vous sélectionnez dans la liste ou que vous spécifiez avec un code RVB |Oui|Aucune option de configuration pour les couleurs des étiquettes. Au lieu de cela, vous pouvez configurer les couleurs des étiquettes dans le Portail Azure ou utiliser [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Aucune option de configuration pour les modèles prédéfinis. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Protection cloud avec des autorisations définies par l’utilisateur pour Word, Excel et PowerPoint |Oui|Les centres d’administration disposent désormais d’une option de configuration pour les autorisations définies par l’utilisateur. <br /><br /> Si vous publiez une étiquette avec cette configuration, vérifiez les résultats de l’application de l’étiquette à partir du [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protection HYOK avec des autorisations définies par l’utilisateur dans Outlook (Ne pas transférer) |Non|Aucune option de configuration pour HYOK. Nous vous déconseillons de publier une étiquette avec cette configuration. Si vous le faites néanmoins, prenez connaissance des résultats de l’application de l’étiquette listés dans le [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Supprimer la protection |Non|Aucune option de configuration pour supprimer la protection. Nous vous déconseillons de publier une étiquette avec cette configuration.<br /><br /> Si vous publiez une étiquette avec cette configuration, quand elle est appliquée, la protection est supprimée si elle a été appliquée précédemment par une étiquette. Si la protection a été précédemment appliquée indépendamment d’une étiquette, la protection est conservée.|
|Police personnalisée et couleur de police personnalisée par code RVB pour les marquages visuels (en-tête, pied de page, filigrane)|Oui|La configuration pour les marquages visuels est limitée à une liste de couleurs et de tailles de police. Vous pouvez publier cette étiquette sans rien changer, même si les valeurs configurées n’apparaissent pas dans les centres d’administration. <br /><br />Pour changer ces options, vous pouvez utiliser le portail Azure. Cependant, pour des raisons de simplicité d’administration, vous pouvez remplacer la couleur par l’une des options listées dans les centres d’administration.|
|Variables dans les marquages visuels (en-tête, pied de page)|Non|Si vous publiez cette étiquette sans changement, les variables s’affichent sous forme de texte sur les clients au lieu d’afficher les valeurs dynamiques. Avant de publier l’étiquette, modifiez les chaînes pour supprimer les variables.|
|Marquages visuels par application|Non|Si vous publiez cette étiquette sans changement, les variables d’application s’affichent sous forme de texte sur les clients dans toutes les applications, au lieu d’afficher vos chaînes de texte sur les applications choisies. Publiez cette étiquette seulement si elle convient pour toutes les applications, et modifiez les chaînes pour supprimer les variables d’application.|
|Conditions et paramètres associés <br /><br /> Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Non applicable|Reconfigurez vos conditions en utilisant l’étiquetage d’automatique comme configuration distincte des paramètres d’étiquette.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Comparaison du comportement des paramètres de protection pour une étiquette

Utilisez le tableau suivant pour identifier le comportement du même paramètre de protection pour une étiquette, selon qu’elle est utilisée par le client Azure Information Protection (Classic), le client d’étiquetage unifié Azure Information Protection ou les applications Office qui ont des étiquettes intégrées (également appelées «étiquetage Office natif»). Les différences de comportement des étiquettes peuvent modifier votre décision de publier les étiquettes, en particulier lorsque vous avez un mélange de clients dans votre organisation.

Si vous n’êtes pas sûr de la façon dont vos paramètres de protection sont configurés, affichez leurs paramètres dans le volet **Protection** du portail Azure. Si vous avez besoin d’aide, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Les paramètres de protection qui se comportent de la même façon n’apparaissent pas dans le tableau, à ces exceptions près :
- Dans le cas d’applications Office avec étiquetage intégré, les étiquettes ne sont pas visibles dans l’Explorateur de fichiers à moins d’installer également le client d’étiquetage unifié Azure Information Protection.
- Dans le cas d’applications Office avec étiquetage intégré, si une protection a déjà été appliquée indépendamment d’une étiquette, elle est conservée[[1]](#footnote-1).

|Paramètre de protection pour une étiquette |Client Azure Information Protection (classique) |Client d’étiquetage unifié Azure Information Protection| Applications Office avec étiquetage intégré
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (clé cloud) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs sont invités à définir des autorisations personnalisées qui sont ensuite appliquées comme protection avec une clé cloud| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs sont invités à définir des autorisations personnalisées qui sont ensuite appliquées comme protection avec une clé cloud|Visible dans Word, Excel, PowerPoint et Outlook : <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs ne sont pas invités à définir des autorisations personnalisées et aucune protection n’est appliquée. <br /><br /> - Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|
|HYOK (AD RMS) avec un modèle :| Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection HYOK est appliquée aux documents et aux e-mails | Visible dans Word, Excel, PowerPoint, Outlook et l’Explorateur de fichiers  <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |Visible dans Word, Excel, PowerPoint et Outlook <br /><br /> Quand cette étiquette est appliquée : <br /><br />- Aucune protection n’est appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1) |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers<br /><br /> Quand cette étiquette est appliquée :<br /><br /> - La protection HYOK est appliquée aux documents et aux e-mails| Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Word, Excel et PowerPoint <br /><br /> Quand cette étiquette est appliquée : <br /><br />- La protection n’est pas appliquée et la protection est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée |
|HYOK (AD RMS) avec des autorisations définies par l’utilisateur pour Outlook :|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- « Ne pas transférer » avec la protection HYOK est appliqué aux e-mails|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br /> - La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée|Visible dans Outlook<br /><br />Quand cette étiquette est appliquée :<br /><br />- La protection n’est pas appliquée et elle est supprimée [[2]](#footnote-2) si elle a été précédemment appliquée par une étiquette <br /><br />- Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|

###### <a name="footnote-1"></a>Note 1

Dans Outlook pour Mac, la protection est conservée à une exception près : Quand un e-mail a été protégé avec l’option Chiffrer uniquement, cette protection est supprimée.


###### <a name="footnote-2"></a>Note 2

La protection est supprimée si l’utilisateur a un droit d’utilisation ou un rôle qui prend en charge cette action :
- Le [droit d’utilisation](configure-usage-rights.md#usage-rights-and-descriptions) Exporter ou Contrôle total.
- Le rôle de [Émetteur Rights Management ou Propriétaire Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), ou de [super utilisateur](configure-super-users.md).

Si l’utilisateur n’a pas un de ces droits d’utilisation ou un de ces rôles, l’étiquette n’est pas appliquée et la protection d’origine est conservée.


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

Utilisez les instructions suivantes pour migrer votre locataire et étiquettes Azure Information Protection pour utiliser le nouveau magasin d’étiquetage unifié.

Vous devez être administrateur de la conformité, administrateur des données de conformité, administrateur de la sécurité ou administrateur général pour migrer vos étiquettes.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans l’option de menu **gérer** , sélectionnez **étiquetage unifié**.

3. Dans le panneau **Azure Information Protection - Unified labeling** (Azure Information Protection - Étiquetage unifié), sélectionnez **Activer** et suivez les instructions en ligne.
    
    Si l’option d’activation n’est pas disponible, vérifiez **l’état de l’étiquetage unifié** : Si vous voyez **Activé**, votre locataire utilise déjà le magasin d’étiquetage unifié et il n’est pas nécessaire de migrer vos étiquettes.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Toutefois, il faut tout d’abord publier ces étiquettes dans l’un des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors de la Portail Azure, pour les clients Azure Information Protection (Classic), revenez à ce panneau d' **étiquetage Azure information protection-Unified** , puis sélectionnez **publier**.

### <a name="clients-and-services-that-support-unified-labeling"></a>Clients et services prenant en charge l’étiquetage unifié

Pour savoir si les clients et services que vous utilisez prennent en charge l’étiquetage unifié, regardez dans leur documentation s’ils peuvent utiliser des étiquettes de confidentialité publiées à partir d’un des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>Les clients qui prennent en charge l’étiquetage unifié sont :

- Le [Azure information protection client d’étiquetage unifié pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Pour obtenir une comparaison entre ce client et le client Azure Information Protection (Classic), consultez [comparer les clients](./rms-client/use-client.md#compare-the-clients).

- Applications Office qui se trouvent à différentes phases de disponibilité. Pour plus d’informations, consultez la section **Où est-ce que la fonctionnalité est disponible aujourd’hui ?** de l’article [Appliquer des étiquettes de critère de diffusion à vos documents et vos e-mails dans Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) dans la documentation Office.
    
- Applications d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>Les services qui prennent en charge l’étiquetage unifié sont :

- Microsoft Defender-protection avancée contre les menaces

- Microsoft Cloud App Security
    
    Ce service prend en charge les étiquettes avant la migration vers le magasin d’étiquetage unifié et après la migration, selon la logique suivante :
    
    - Si les centres d’administration ont les mêmes étiquettes que le Portail Azure : les étiquettes unifiées sont récupérées à partir des centres d’administration. Pour que ces étiquettes puissent être sélectionnées dans Cloud App Security, au moins une étiquette doit être publiée sur au moins un utilisateur.
    
    - Si les centres d’administration n’ont pas les mêmes étiquettes que le Portail Azure : les étiquettes unifiées des centres d’administration ne sont pas utilisées ; les étiquettes sont récupérées auprès du Portail Azure.

- Services d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir de l’aide et des conseils supplémentaires de notre équipe de l’expérience utilisateur, consultez le billet de blog suivant : [Compréhension de la migration d’étiquetage unifiée](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185).

Pour plus d’informations sur les étiquettes migrées maintenant configurables et publiables dans l’un des centres d’administration, voir [Vue d’ensemble des étiquettes de confidentialité](/Office365/SecurityCompliance/sensitivity-labels).

Si vous ne l’avez pas déjà fait, installez le client d’étiquetage unifié Azure Information Protection. Pour obtenir des informations sur la version, un guide d’administration et un guide de l’utilisateur, consultez [Azure information protection le client d’étiquetage unifié pour Windows](./rms-client/aip-clientv2.md).
