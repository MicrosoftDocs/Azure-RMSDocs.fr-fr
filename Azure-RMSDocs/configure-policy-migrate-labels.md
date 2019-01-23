---
title: Migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365 - AIP
description: Migrez les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365 pour les clients qui prennent en charge l’étiquetage unifié.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/17/20198
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 221b503fa3621e51c4822a6ad5a6d08fae4f1bad
ms.sourcegitcommit: 8dec864bf25c7da62b9e0f628f1bf673c81c15ae
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54356009"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Cette fonctionnalité est en préversion et migre votre locataire vers une nouvelle plateforme qui est également en préversion. La migration est irréversible. La nouvelle plateforme prend en charge l’étiquetage unifié afin que les étiquettes que vous créez et gérez puissent être utilisées par plusieurs clients et services.

Migrez vos étiquettes si vous souhaitez être en mesure de les utiliser dans le Centre de sécurité et conformité Office 365, où elles peuvent être publiées et ensuite téléchargées par les [clients qui prennent en charge l’étiquetage unifié](#clients-that-support-unified-labeling). Le client Azure Information Protection continue de télécharger les étiquettes avec la stratégie Azure Information Protection à partir du portail Azure. 

Une fois que vous avez migré vos étiquettes, vous pouvez ensuite les modifier dans le portail Azure ou le Centre de sécurité et conformité Office 365, et les clients respectifs téléchargent la même modification.

### <a name="important-information-about-administrative-roles"></a>Informations importantes sur les rôles administratifs

Les [rôles Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) **Administrateur de la sécurité** et **Administrateur Information Protection** ne sont pas pris en charge par la plateforme d’étiquetage unifié. Si ces rôles administratifs sont utilisés dans votre organisation, avant de migrer vos étiquettes, ajoutez les utilisateurs qui disposent de ces rôles aux groupes de rôles **Administrateur de conformité** ou **Gestion de l’organisation** pour le Centre de sécurité et de conformité Office 365. Vous pouvez aussi créer un nouveau groupe de rôles pour ces utilisateurs et ajouter les rôles **Gestion de la rétention** ou **Configuration de l’organisation** à ce groupe. Pour obtenir des instructions, consultez [Donner aux utilisateurs accès au Centre de sécurité et de conformité Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center).

Si vous ne donnez pas à ces utilisateurs accès au Centre de sécurité et de conformité à l’aide de l’une de ces configurations, ils perdront l’accès aux étiquettes et stratégies dans le portail Azure une fois vos étiquettes migrées.

Les administrateurs généraux pour votre locataire peuvent continuer à gérer les étiquettes et les stratégies dans le portail Azure et le Centre de sécurité et de conformité une fois vos étiquettes migrées.


## <a name="considerations-for-unified-labels"></a>Éléments à prendre en considération pour les étiquettes unifiées

Avant de migrer vos étiquettes, tenez compte des changements et des considérations qui suivent :

- Actuellement, les clients ne prennent pas tous en charge les étiquettes unifiées. Vérifiez que vous avez des [clients pris en charge](#clients-that-support-unified-labeling) et préparez-vous à des tâches d’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et le Centre de sécurité et conformité (pour les clients qui prennent en charge les étiquettes unifiées).

- Si vous êtes en train de définir et configurer les étiquettes que vous souhaitez utiliser, nous vous recommandons d’effectuer ce processus à l’aide du portail Azure, puis de migrer les étiquettes. Cette stratégie évite la duplication des étiquettes pendant le processus de migration, qui devront ensuite être modifiées dans le Centre de sécurité et conformité.

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Pour ces modifications qui ne sont pas migrées, vous devez configurer les options appropriées dans le Centre de sécurité et conformité une fois que les étiquettes sont migrées.
    
    Pour une expérience utilisateur plus cohérente, nous vous recommandons de publier les mêmes étiquettes dans les mêmes étendues du Centre de sécurité et conformité.

- Les paramètres issus d’une étiquette migrée ne sont pas tous pris en charge par le Centre de sécurité et conformité. Utilisez le tableau de la section [Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et de conformité](#label-settings-that-are-not-supported-in-the-security--compliance-center) pour vous aider à identifier les paramètres qui ne sont pas pris en charge dans le Centre de sécurité et de conformité.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Une fois qu’une étiquette avec des paramètres de protection dans le cloud a été migrée, l’étendue résultante du modèle de protection est l’étendue qui est définie dans le portail Azure (ou à l’aide du module PowerShell AADRM) et l’étendue qui est définie dans le Centre de sécurité et conformité. 

- Quand vous migrez vos étiquettes,les résultats de la migration indiquent si une étiquette a été **créée**, **mise à jour** ou **renommée** en raison de la duplication :

    - Quand une étiquette est créée, vous devez ensuite la publier dans le Centre de sécurité et conformité pour la rendre disponible aux applications et services.
    
    - Quand une étiquette est renommée, vous devez ensuite la modifier, ce que vous pouvez faire dans le Centre de sécurité et conformité ou le portail Azure. 

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Le Centre de sécurité et conformité indique à la fois ce nom d’affichage pour une étiquette et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous avez spécifié lors de la création de l’étiquette et cette propriété est utilisée par le service back-end à des fins d’identification.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Vous devez définir de nouvelles chaînes localisées pour les étiquettes migrées dans le Centre de sécurité et conformité.

- Après la migration, quand vous modifiez une étiquette migrée dans le portail Azure, la même modification est automatiquement répercutée dans le Centre de sécurité et conformité. Toutefois, lorsque vous modifiez une étiquette migrée dans le Centre de sécurité et de conformité, vous devez retourner au portail Azure, dans le panneau **Azure Information Protection - Étiquetage unifié**, puis sélectionner **Publier**. Cette action supplémentaire est nécessaire pour que les clients Azure Information Protection récupèrent les modifications de l’étiquette.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et conformité

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée qui ne sont pas pris en charge par les clients d’étiquetage unifié ou qui sont pris en charge avec des limitations. Pour éviter toute confusion, nous vous recommandons de ne configurer les paramètres qui n’ont aucun effet sur les clients d’étiquetage unifié.

Les clients Azure Information Protection peuvent utiliser ces paramètres d’étiquette sans aucun problème, car ils continuent de télécharger les étiquettes à partir du portail Azure.

|Configuration d’étiquettes|Pris en charge par les clients d’étiquetage unifié|Exclure de la modification dans le Centre de sécurité et de conformité|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Remarques : Pas de synchronisation avec le Centre de sécurité et conformité |Non applicable|Non applicable|
|Couleur d’étiquette : sélectionnez une valeur dans la liste ou spécifiez-la à l’aide du code RVB<br /><br />Remarques : Les couleurs d’étiquettes ne sont pas prises en charge par le Centre de sécurité et conformité |Non applicable|Non applicable|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Oui|
|Protection dans le cloud à l’aide des autorisations définies par l’utilisateur dans Word, Excel et PowerPoint |Non|Oui|
|Protection basée sur HYOK à l’aide des autorisations définies par l’utilisateur dans Outlook pour l’option Ne pas transférer |Non|Oui|
|Supprimer la protection |Non|Oui|
|Marquages visuels (en-tête, pied de page, filigrane) : police personnalisée et couleur de police personnalisée par code RVB|Non|Recommandée si vous utilisez des variables<br /><br />- Sur les clients, les variables s’affichent sous forme de texte au lieu d’afficher les valeurs dynamiques|
|Marquages visuels par application|Non|Recommandée si vous utilisez des variables<br /><br />- Sur les clients, les variables s’affichent sous forme de texte au lieu d’afficher les valeurs dynamiques|
|Conditions et paramètres associés <br /><br />Remarques : Inclut l’étiquetage automatique et recommandé ainsi que leurs info-bulles|Non applicable|Non|


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

Utilisez les instructions suivantes pour migrer votre locataire et étiquettes Azure Information Protection pour utiliser le nouveau magasin d’étiquetage unifié.

Vous devez être un administrateur général pour migrer vos étiquettes.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans l’option de menu **Gérer**, sélectionnez **Unified labeling (Preview)** (Étiquetage unifié (préversion)).

3. Dans le panneau **Azure Information Protection - Unified labeling** (Azure Information Protection - Étiquetage unifié), sélectionnez **Activer** et suivez les instructions en ligne.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients qui prennent en charge l’étiquetage unifié](#clients-that-support-unified-labeling). Toutefois, vous devez tout d’abord publier ces étiquettes dans le Centre de sécurité et conformité.

> [!IMPORTANT]
> Si vous modifiez les étiquettes en dehors du portail Azure, pour les clients Azure Information Protection, revenez dans ce panneau **Azure Information Protection - Étiquetage unifié**, puis sélectionnez **Publier**.

### <a name="clients-that-support-unified-labeling"></a>Clients qui prennent en charge l’étiquetage unifié

Les clients qui prennent en charge l’étiquetage unifié sont notamment :

- Le [client d’étiquetage unifié Azure Information Protection pour Windows](./rms-client/unifiedlabelingclient-version-release-history.md) - en préversion

- Applications du programme Office Insider. Pour plus d’informations, consultez la section [Où cette fonctionnalité est-elle disponible aujourd’hui ?](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable) dans la documentation Office.
    
- Clients des éditeurs de logiciels et développeurs qui utilisent le [SDK MIP](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference).


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur vos étiquettes migrées qui peuvent maintenant être configurées et publiées dans le Centre de sécurité et de conformité Office 365, consultez [Vue d’ensemble des étiquettes de sensibilité](/Office365/SecurityCompliance/sensitivity-labels).

Pour lire le billet de blog d’annonce : [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492).