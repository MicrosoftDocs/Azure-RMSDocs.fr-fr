---
title: Migrer des étiquettes Azure Information Protection sur Office 365 – AIP
description: Migrez des étiquettes Azure Information Protection vers des étiquettes de confidentialité Office 365 pour les clients et les services qui prennent en charge les étiquettes unifiées.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/03/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 1f1952a871940fcd24e7e81bf6d4312fdef8d014
ms.sourcegitcommit: 1b8e87bda58bb40f3e32b2edf264385e7235b7c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2019
ms.locfileid: "66462242"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>Guide pratique pour migrer des étiquettes Azure Information Protection vers des étiquettes de confidentialité Office 365

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Migrer vos étiquettes dans Azure Information Protection afin que vous puissiez les utiliser comme étiquettes de sensibilité par [les clients et les services qui prennent en charge l’étiquetage unifiée](#clients-and-services-that-support-unified-labeling).

Après la migration, gérer et publier ces étiquettes à partir de la sécurité Office 365 & centre de conformité, ou le centre de sécurité Microsoft 365 et le centre de conformité de Microsoft 365. Ces étiquettes peuvent être utilisées par le client d’étiquetage unifié Azure Information Protection. Si vous continuez à utiliser le client Azure Information Protection, ce client continue à télécharger les étiquettes avec la stratégie Azure Information Protection à partir du portail Azure.

Avant de lire les instructions détaillées sur la migration de vos étiquettes, vous trouverez probablement utiles les questions fréquemment posées suivantes :

- [Quelle est la différence entre les étiquettes dans Azure Information Protection et celles dans Office 365 ?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Comment définir le bon moment pour migrer mes étiquettes vers Office 365 ?](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>Informations importantes sur les rôles administratifs

Le [rôle Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) de **administrateur Azure Information Protection** (anciennement **administrateur Information Protection**) ne prend pas en charge l’étiquetage unifiée plateforme. Si ce rôle d’administration est utilisé dans votre organisation, avant de migrer vos étiquettes, ajoutez les utilisateurs qui possèdent ce rôle aux rôles Azure AD **Administrateur de sécurité** ou **Administrateur de conformité**. Si vous avez besoin d’aide, consultez [Donner aux utilisateurs accès au Centre de sécurité et de conformité Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center). Vous pouvez également attribuer ces rôles dans le portail Azure AD, le centre de sécurité Microsoft 365 et le centre de conformité Microsoft 365.

Au lieu d’utiliser des rôles, dans les centres d’administration, vous pouvez créer un nouveau groupe de rôles pour ces utilisateurs et ajoutez les rôles **Administrateur d’étiquette de sensibilité** ou **Configuration de l’organisation** à ce groupe.

Si vous ne donnez pas accès aux centres d’administration à ces utilisateurs suivant l’une de ces configurations, ils ne pourront pas configurer Azure Information Protection dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux de votre locataire pourront continuer à gérer les étiquettes et les stratégies sur le Portail Azure et dans les centres d’administration une fois vos étiquettes migrées.


## <a name="considerations-for-unified-labels"></a>Éléments à prendre en considération pour les étiquettes unifiées

Avant de migrer vos étiquettes, tenez compte des changements et des considérations qui suivent :

- Actuellement, les clients ne prennent pas tous en charge les étiquettes unifiées. Vérifiez que vous avez des [clients pris en charge](#clients-and-services-that-support-unified-labeling) et préparez-vous à des tâches d’administration à la fois sur le Portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et dans les centres d’administration (pour les autres).

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Ces modifications non migrées impliquent de configurer les options correspondantes dans les centres d’administration une fois les étiquettes migrées.
    
    Pour une expérience utilisateur plus homogène, nous vous recommandons de publier les mêmes étiquettes avec les mêmes étendues dans les centres d’administration.

- Les paramètres d’une étiquette migrée ne sont pas tous pris en charge par les centres d’administration. Suivez le tableau de la section [Paramètres d’étiquette non pris en charge dans les centres d’administration](#label-settings-that-are-not-supported-in-the-admin-centers) pour identifier ces paramètres et la procédure recommandée.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Si vous avez des étiquettes configurées pour un modèle prédéfini, modifiez ces étiquettes et sélectionnez l’option **Définir les autorisations** pour configurer les mêmes paramètres de protection que ceux de votre modèle. Les étiquettes comportant des modèles prédéfinis ne bloquent pas la migration des étiquettes, mais cette configuration n’est pas prise en charge dans les centres d’administration.
        
        Conseil : Pour reconfigurer ces étiquettes plus facilement, vous pouvez utiliser deux fenêtres de navigateur : Une fenêtre dans laquelle vous sélectionnez le bouton **Modifier le modèle** de l’étiquette pour afficher les paramètres de protection, et l’autre fenêtre pour configurer les mêmes paramètres quand vous sélectionnez **Définir des autorisations**.
    
    - Une fois qu’une étiquette comportant des paramètres de protection cloud a été migrée, l’étendue résultante du modèle de protection correspond aux étendues définies sur le Portail Azure (ou à l’aide du module PowerShell AADRM) et dans les centres d’administration. 

- Quand vous migrez vos étiquettes,les résultats de la migration indiquent si une étiquette a été **créée**, **mise à jour** ou **renommée** en raison de la duplication :

    - Quand une étiquette est créée, vous devez ensuite la publier dans l’un des centres d’administration pour la rendre accessible aux applications et services.
    
    - Quand une étiquette est renommée, vous devez ensuite la modifier dans l’un des centres d’administration ou sur le Portail Azure.

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Les centres d’administration indiquent à la fois ce nom d’affichage et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous avez spécifié lors de la création de l’étiquette et cette propriété est utilisée par le service back-end à des fins d’identification.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Il faut définir de nouvelles chaînes localisées pour les étiquettes migrées dans les centres d’administration.

- Après la migration, tout modification d’une étiquette migrée sur le Portail Azure est automatiquement répercutée dans les centres d’administration. Si en revanche vous modifiez une étiquette migrée dans l’un des centres d’administration, vous devez revenir sur le Portail Azure, dans le panneau **Azure Information Protection – Étiquetage unifié**, puis sélectionner **Publier**. Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection récupèrent les modifications de l’étiquette.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Paramètres d’étiquette non pris en charge dans les centres d’administration

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée non pris en charge par le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. Si vous avez des étiquettes comportant ces paramètres, suivrez les instructions d’administration de la dernière colonne une fois la migration terminée avant de les publier dans l’un des centres d’administration.

Si vous n’êtes pas sûr de la façon dont vos étiquettes sont configurées, affichez leurs paramètres dans le portail Azure. Si vous avez besoin d’aide, consultez [Configuration de la stratégie Azure Information Protection](configure-policy.md).

Les clients Azure Information Protection peuvent utiliser tous les paramètres d’étiquette listés sans aucun problème, car ils continuent de télécharger les étiquettes à partir du portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié| Aide pour les centres d’administration|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Remarques : non synchronisées avec les centres d’administration |Non applicable|L’équivalent est si l’étiquette est publiée ou non. |
|Couleur d’étiquette que vous sélectionnez dans la liste ou que vous spécifiez avec un code RVB |Oui|Aucune option de configuration pour les couleurs des étiquettes. Au lieu de cela, vous pouvez configurer les couleurs des étiquettes dans le portail Azure.|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Aucune option de configuration pour les modèles prédéfinis. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Protection cloud avec des autorisations définies par l’utilisateur pour Word, Excel et PowerPoint |Non|Aucune option de configuration pour les autorisations définies par l’utilisateur pour ces applications Office. Nous vous déconseillons de publier une étiquette avec cette configuration. Si vous le faites néanmoins, prenez connaissance des résultats de l’application de l’étiquette listés dans le [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protection HYOK avec des autorisations définies par l’utilisateur dans Outlook (Ne pas transférer) |Non|Aucune option de configuration pour HYOK. Nous vous déconseillons de publier une étiquette avec cette configuration. Si vous le faites néanmoins, prenez connaissance des résultats de l’application de l’étiquette listés dans le [tableau suivant](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Supprimer la protection |Non|Aucune option de configuration pour supprimer la protection. Nous vous déconseillons de publier une étiquette avec cette configuration.<br /><br /> Si vous publiez cette étiquette, lorsqu’il est appliqué, protection est supprimée si elle a été précédemment appliquée par une étiquette. Si la protection a été précédemment appliquée indépendamment d’une étiquette, la protection est conservée.|
|Police personnalisée et couleur de police personnalisée par code RVB pour les marquages visuels (en-tête, pied de page, filigrane)|Oui|La configuration pour les marquages visuels est limitée à une liste de couleurs et de tailles de police. Vous pouvez publier cette étiquette sans rien changer, même si les valeurs configurées n’apparaissent pas dans les centres d’administration. <br /><br />Pour changer ces options, vous pouvez utiliser le portail Azure. Cependant, pour des raisons de simplicité d’administration, vous pouvez remplacer la couleur par l’une des options listées dans les centres d’administration.|
|Variables dans les marquages visuels (en-tête, pied de page)|Non|Si vous publiez cette étiquette sans changement, les variables s’affichent sous forme de texte sur les clients au lieu d’afficher les valeurs dynamiques. Avant de publier l’étiquette, modifiez les chaînes pour supprimer les variables.|
|Marquages visuels par application|Non|Si vous publiez cette étiquette sans changement, les variables d’application s’affichent sous forme de texte sur les clients dans toutes les applications, au lieu d’afficher vos chaînes de texte sur les applications choisies. Publiez cette étiquette seulement si elle convient pour toutes les applications, et modifiez les chaînes pour supprimer les variables d’application.|
|Conditions et paramètres associés <br /><br />Remarques : Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Non applicable|Reconfigurez vos conditions en utilisant l’étiquetage d’automatique comme configuration distincte des paramètres d’étiquette.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Comparaison du comportement des paramètres de protection pour une étiquette

Utilisez le tableau suivant pour identifier la manière dont le même paramètre de protection pour une étiquette se comporte différemment, selon qu’il soit utilisé par le client Azure Information Protection, le client d’étiquetage Azure Information Protection unifié, ou par les applications Office qui ont l’étiquetage intégrée (également appelé « Office natifs 

Si vous n’êtes pas sûr de la façon dont vos paramètres de protection sont configurés, affichez leurs paramètres dans le volet **Protection** du portail Azure. Si vous avez besoin d’aide, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Les paramètres de protection qui se comportent de la même façon n’apparaissent pas dans le tableau, à ces exceptions près :
- Dans le cas d’applications Office avec étiquetage intégré, les étiquettes ne sont pas visibles dans l’Explorateur de fichiers à moins d’installer également le client d’étiquetage unifié Azure Information Protection.
- Dans le cas d’applications Office avec étiquetage intégré, si une protection a déjà été appliquée indépendamment d’une étiquette, elle est conservée[[1]](#footnote-1).

|Paramètre de protection pour une étiquette |Client Azure Information Protection|Client d’étiquetage unifié Azure Information Protection| Applications Office avec étiquetage intégré
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (clé cloud) avec des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers :| Visible dans Word, Excel, PowerPoint et l’Explorateur de fichiers <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs sont invités à définir des autorisations personnalisées qui sont ensuite appliquées comme protection avec une clé cloud| Non visible |Visible dans Word, Excel, PowerPoint et Outlook : <br /><br /> Quand l’étiquette est appliquée :<br /><br /> - Les utilisateurs ne sont pas invités à définir des autorisations personnalisées et aucune protection n’est appliquée. <br /><br /> - Si la protection a été précédemment appliquée indépendamment d’une étiquette, cette protection est conservée [[1]](#footnote-1)|
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

Vous devez être un administrateur de conformité, un administrateur de sécurité ou un administrateur Global pour migrer vos étiquettes.

> [!NOTE]
> Si vous avez des étiquettes de rétention ou des stratégies de protection contre la perte de données pour Office 365, nous vous recommandons d’avoir le rôle d’administrateur de conformité, ou le rôle d’administrateur général pour migrer vos étiquettes.
> 
> Les administrateurs de sécurité n’ont accès aux stratégies de protection contre la perte étiquettes ou des données des rétention, par conséquent, si vous avez un d'entre eux et ils ont le même nom que vos étiquettes Azure Information Protection, le processus de migration ne peut pas terminer manuellement jusqu'à ce que vous renommez un des doublons. Toutefois, si vous avez un des autres rôles, le processus de migration peut renommer l’étiquette Azure Information Protection pour vous, afin que la migration puisse s’exécuter.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de la **gérer** option de menu, sélectionnez **unifiés l’étiquetage**.

3. Dans le panneau **Azure Information Protection - Unified labeling** (Azure Information Protection - Étiquetage unifié), sélectionnez **Activer** et suivez les instructions en ligne.
    
    Si l’option d’activation n’est pas disponible, vérifiez **l’état de l’étiquetage unifié** : Si vous voyez **Activé**, votre locataire utilise déjà le magasin d’étiquetage unifié et il n’est pas nécessaire de migrer vos étiquettes.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Toutefois, il faut tout d’abord publier ces étiquettes dans l’un des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors du portail Azure, pour les clients Azure Information Protection, revenez dans ce panneau **Azure Information Protection - Étiquetage unifié**, puis sélectionnez **Publier**.

### <a name="clients-and-services-that-support-unified-labeling"></a>Clients et services prenant en charge l’étiquetage unifié

Pour savoir si les clients et services que vous utilisez prennent en charge l’étiquetage unifié, regardez dans leur documentation s’ils peuvent utiliser des étiquettes de confidentialité publiées à partir d’un des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>Les clients qui prennent en charge l’étiquetage unifié sont :

- Le [Azure Information Protection unifiée étiquetage client pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Pour obtenir une comparaison de ce client avec le client Azure Information Protection, consultez [comparer les clients](./rms-client/use-client.md#compare-the-clients).

- Applications Office qui se trouvent à différentes phases de disponibilité. Pour plus d’informations, consultez la section **Où est-ce que la fonctionnalité est disponible aujourd’hui ?** de l’article [Appliquer des étiquettes de critère de diffusion à vos documents et vos e-mails dans Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) dans la documentation Office.
    
- Applications d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>Les services qui prennent en charge l’étiquetage unifié sont :

- Defender Microsoft Advanced Threat Protection

- Microsoft Cloud App Security
    
    Ce service prend en charge les étiquettes avant la migration vers le magasin d’étiquetage unifié et après la migration, selon la logique suivante :
    
    - Si les centres d’administration ont les mêmes étiquettes que le Portail Azure : les étiquettes unifiées sont récupérées à partir des centres d’administration. Pour que ces étiquettes puissent être sélectionnées dans Cloud App Security, au moins une étiquette doit être publiée sur au moins un utilisateur.
    
    - Si les centres d’administration n’ont pas les mêmes étiquettes que le Portail Azure : les étiquettes unifiées des centres d’administration ne sont pas utilisées ; les étiquettes sont récupérées auprès du Portail Azure.

- Services d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les étiquettes migrées maintenant configurables et publiables dans l’un des centres d’administration, voir [Vue d’ensemble des étiquettes de confidentialité](/Office365/SecurityCompliance/sensitivity-labels).

Si vous n’avez pas déjà fait, installez le client d’étiquetage unifié Azure Information Protection. Pour plus d’informations de version, un guide de l’administrateur et guide de l’utilisateur, consultez [Azure Information Protection unifiée étiquetage client pour Windows](./rms-client/aip-clientv2.md).
