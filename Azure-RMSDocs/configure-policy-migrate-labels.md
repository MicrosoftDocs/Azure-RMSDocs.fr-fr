---
title: Migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365 - AIP
description: Migrez les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365 pour les clients qui prennent en charge l’étiquetage unifié.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/14/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: ed3c77df8da01a4b87b30875a315eac5c075b438
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57829057"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Cette fonctionnalité est en préversion et migre votre locataire vers une nouvelle plateforme. La migration est irréversible. La nouvelle plateforme prend en charge l’étiquetage unifié pour que les étiquettes que vous créez et que vous gérez puissent être utilisées par des clients et des services qui prennent en charge les [solutions Microsoft Information Protection](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection).

Migrez vos étiquettes si vous voulez être en mesure de les utiliser comme étiquettes de sensibilité Office 365 dans le Centre de sécurité et conformité Office 365, pour qu’elles soient utilisées par des [clients et des services prenant en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Après la migration, le client Azure Information Protection continue de télécharger les étiquettes avec la stratégie Azure Information Protection à partir du portail Azure. 

Avant de lire les instructions détaillées sur la migration de vos étiquettes, vous trouverez probablement utiles les questions fréquemment posées suivantes :

- [Quelle est la différence entre les étiquettes dans Azure Information Protection et celles dans Office 365 ?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Comment définir le bon moment pour migrer mes étiquettes vers Office 365 ?](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [Une fois que j’ai migré mes étiquettes, quel portail de gestion utiliser ?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>Informations importantes sur les rôles administratifs

Les [rôles Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) **Administrateur de la sécurité** et **Administrateur Information Protection** ne sont pas pris en charge par la plateforme d’étiquetage unifié. Si ces rôles administratifs sont utilisés dans votre organisation, avant de migrer vos étiquettes, ajoutez les utilisateurs qui disposent de ces rôles aux groupes de rôles **Administrateur de conformité** ou **Gestion de l’organisation** pour le Centre de sécurité et de conformité Office 365. Vous pouvez aussi créer un nouveau groupe de rôles pour ces utilisateurs et ajouter les rôles **Gestion de la rétention** ou **Configuration de l’organisation** à ce groupe. Pour obtenir des instructions, consultez [Donner aux utilisateurs accès au Centre de sécurité et de conformité Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center).

Si vous ne donnez pas à ces utilisateurs accès au Centre de sécurité et de conformité à l’aide de l’une de ces configurations, ils perdront l’accès aux étiquettes et stratégies dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux pour votre locataire peuvent continuer à gérer les étiquettes et les stratégies dans le portail Azure et dans le Centre de sécurité et de conformité une fois vos étiquettes migrées.


## <a name="considerations-for-unified-labels"></a>Éléments à prendre en considération pour les étiquettes unifiées

Avant de migrer vos étiquettes, tenez compte des changements et des considérations qui suivent :

- Actuellement, les clients ne prennent pas tous en charge les étiquettes unifiées. Vérifiez que vous avez des [clients pris en charge](#clients-and-services-that-support-unified-labeling) et préparez-vous à des tâches d’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et le Centre de sécurité et conformité (pour les clients qui prennent en charge les étiquettes unifiées).

- Si vous êtes en train de définir et configurer les étiquettes que vous souhaitez utiliser, nous vous recommandons d’effectuer ce processus à l’aide du portail Azure, puis de migrer les étiquettes. Cette stratégie évite la duplication des étiquettes pendant le processus de migration, qui devront ensuite être modifiées dans le Centre de sécurité et conformité.

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Pour ces modifications qui ne sont pas migrées, vous devez configurer les options appropriées dans le Centre de sécurité et conformité une fois que les étiquettes sont migrées.
    
    Pour une expérience utilisateur plus cohérente, nous vous recommandons de publier les mêmes étiquettes dans les mêmes étendues du Centre de sécurité et conformité.

- Les paramètres issus d’une étiquette migrée ne sont pas tous pris en charge par le Centre de sécurité et conformité. Utilisez le tableau de la section [Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et de conformité](#label-settings-that-are-not-supported-in-the-security--compliance-center) pour identifier ces paramètres et la ligne de conduite recommandée.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Si vous avez des étiquettes qui sont configurées pour un modèle prédéfini, [convertissez ces modèles en étiquettes](configure-policy-templates.md#to-convert-templates-to-labels) avant de migrer vos étiquettes. Cette configuration ne bloque pas la migration de l’étiquette, mais n’est pas prise en charge dans le Centre de sécurité et de conformité.
    
    - Une fois qu’une étiquette avec des paramètres de protection dans le cloud a été migrée, l’étendue résultante du modèle de protection est l’étendue qui est définie dans le portail Azure (ou à l’aide du module PowerShell AADRM) et l’étendue qui est définie dans le Centre de sécurité et conformité. 

- Quand vous migrez vos étiquettes,les résultats de la migration indiquent si une étiquette a été **créée**, **mise à jour** ou **renommée** en raison de la duplication :

    - Quand une étiquette est créée, vous devez ensuite la publier dans le Centre de sécurité et conformité pour la rendre disponible aux applications et services.
    
    - Quand une étiquette est renommée, vous devez ensuite la modifier, ce que vous pouvez faire dans le Centre de sécurité et conformité ou le portail Azure. 

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Le Centre de sécurité et conformité indique à la fois ce nom d’affichage pour une étiquette et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous avez spécifié lors de la création de l’étiquette et cette propriété est utilisée par le service back-end à des fins d’identification.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Vous devez définir de nouvelles chaînes localisées pour les étiquettes migrées dans le Centre de sécurité et conformité.

- Après la migration, quand vous modifiez une étiquette migrée dans le portail Azure, la même modification est automatiquement répercutée dans le Centre de sécurité et conformité. Toutefois, lorsque vous modifiez une étiquette migrée dans le Centre de sécurité et de conformité, vous devez retourner au portail Azure, dans le panneau **Azure Information Protection - Étiquetage unifié**, puis sélectionner **Publier**. Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection récupèrent les modifications de l’étiquette.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et conformité

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée qui ne sont pas pris en charge par le Centre de sécurité et de conformité. Si vous avez des étiquettes avec ces paramètres, une fois la migration terminée, utilisez les instructions d’administration dans la dernière colonne avant de publier vos étiquettes dans le Centre de sécurité et de conformité Office 365.

Les clients Azure Information Protection peuvent utiliser tous les paramètres d’étiquette listés sans aucun problème, car ils continuent de télécharger les étiquettes à partir du portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié| Aide pour le Centre de sécurité et de conformité|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Remarques : Pas de synchronisation avec le Centre de sécurité et conformité |Non applicable|L’équivalent est si l’étiquette est publiée ou non. |
|Couleur d’étiquette que vous sélectionnez dans la liste ou que vous spécifiez avec un code RVB |Oui|Aucune option de configuration pour les couleurs des étiquettes. Au lieu de cela, vous pouvez configurer les couleurs des étiquettes dans le portail Azure.|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Aucune option de configuration pour les modèles prédéfinis. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Protection cloud avec des autorisations définies par l’utilisateur pour Word, Excel et PowerPoint |Non|Aucune option de configuration pour les autorisations définies par l’utilisateur pour ces applications Office. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Protection HYOK avec des autorisations définies par l’utilisateur dans Outlook (Ne pas transférer) |Non|Aucune option de configuration pour HYOK. Nous vous déconseillons de publier une étiquette avec cette configuration.|
|Supprimer la protection |Non|Aucune option de configuration pour supprimer la protection. Nous vous déconseillons de publier une étiquette avec cette configuration.<br /><br /> Si vous publiez cette étiquette, quand elle est appliquée, la protection est supprimée si elle a été précédemment appliquée par une étiquette. Si la protection a été précédemment appliquée indépendamment d’une étiquette, la protection est conservée.|
|Police personnalisée et couleur de police personnalisée par code RVB pour les marquages visuels (en-tête, pied de page, filigrane)|Oui|La configuration pour les marquages visuels est limitée à une liste de couleurs et de tailles de police. Vous pouvez publier cette étiquette sans rien changer, même si vous ne voyez pas les valeurs configurées dans le Centre de sécurité et de conformité. <br /><br />Pour changer ces options, vous pouvez utiliser le portail Azure. Cependant, pour une administration plus simple, vous pouvez changer la couleur pour une des options listées dans le Centre de sécurité et de conformité.|
|Variables dans les marquages visuels (en-tête, pied de page)|Non|Si vous publiez cette étiquette sans changement, les variables s’affichent sous forme de texte sur les clients au lieu d’afficher les valeurs dynamiques. Avant de publier l’étiquette, modifiez les chaînes pour supprimer les variables.|
|Marquages visuels par application|Non|Si vous publiez cette étiquette sans changement, les variables d’application s’affichent sous forme de texte sur les clients dans toutes les applications, au lieu d’afficher vos chaînes de texte sur les applications choisies. Publiez cette étiquette seulement si elle convient pour toutes les applications, et modifiez les chaînes pour supprimer les variables d’application.|
|Conditions et paramètres associés <br /><br />Remarques : Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Non applicable|Reconfigurez vos conditions en utilisant l’étiquetage d’automatique comme configuration distincte des paramètres d’étiquette.|


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

Utilisez les instructions suivantes pour migrer votre locataire et étiquettes Azure Information Protection pour utiliser le nouveau magasin d’étiquetage unifié.

Vous devez être un administrateur général pour migrer vos étiquettes.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans l’option de menu **Gérer**, sélectionnez **Unified labeling (Preview)** (Étiquetage unifié (préversion)).

3. Dans le panneau **Azure Information Protection - Unified labeling** (Azure Information Protection - Étiquetage unifié), sélectionnez **Activer** et suivez les instructions en ligne.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients et les services qui prennent en charge l’étiquetage unifié](#clients-and-services-that-support-unified-labeling). Toutefois, vous devez tout d’abord publier ces étiquettes dans le Centre de sécurité et conformité.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors du portail Azure, pour les clients Azure Information Protection, revenez dans ce panneau **Azure Information Protection - Étiquetage unifié**, puis sélectionnez **Publier**.

### <a name="clients-and-services-that-support-unified-labeling"></a>Clients et services prenant en charge l’étiquetage unifié

Pour savoir si les clients et les services que vous utilisez prennent en charge l’étiquetage unifié, consultez leur documentation pour vérifier s’ils peuvent utiliser des étiquettes de sensibilité qui sont publiées à partir du Centre de sécurité et de conformité Office 365. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>Les clients qui prennent en charge l’étiquetage unifié sont :

- Le [client d’étiquetage unifié Azure Information Protection pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md) - en préversion

- Applications Office qui se trouvent à différentes phases de disponibilité. Pour plus d’informations, consultez la section **Où est-ce que la fonctionnalité est disponible aujourd’hui ?** de l’article [Appliquer des étiquettes de critère de diffusion à vos documents et vos e-mails dans Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) dans la documentation Office.
    
- Applications d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>Les services qui prennent en charge l’étiquetage unifié sont :

- Windows Defender Azure Threat Protection

- Microsoft Cloud App Security
    
    Ce service prend en charge les étiquettes avant la migration vers le magasin d’étiquetage unifié et après la migration, selon la logique suivante :
    
    - Si le Centre de sécurité et de conformité Office 365 a les mêmes étiquettes que celles figurant dans le portail Azure : Les étiquettes unifiées sont récupérées auprès du Centre de sécurité et de conformité Office 365. Pour que ces étiquettes puissent être sélectionnées dans Cloud App Security, au moins une étiquette doit être publiée sur au moins un utilisateur.
    
    - Si le Centre de sécurité et de conformité Office 365 n’a pas les mêmes étiquettes que celles figurant dans le portail Azure : Les étiquettes unifiées ne sont pas utilisées à partir du Centre de sécurité et de conformité Office 365 ; au lieu de cela, les étiquettes sont récupérées auprès du portail Azure.

- Services d’éditeurs de logiciels et de développeurs qui utilisent le [SDK Microsoft Information Protection](https://docs.microsoft.com/en-us/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur vos étiquettes migrées qui peuvent maintenant être configurées et publiées dans le Centre de sécurité et de conformité Office 365, consultez [Vue d’ensemble des étiquettes de sensibilité](/Office365/SecurityCompliance/sensitivity-labels).

Pour lire le billet de blog d’annonce : [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492).
