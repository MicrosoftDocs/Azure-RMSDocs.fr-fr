---
title: Migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365
description: Migrez les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365 pour les clients qui prennent en charge l’étiquetage unifié.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/11/2018
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 075330138910da90049cad3c1ccc74a1a360a218
ms.sourcegitcommit: 39403f0e9fe5912d467b119ed45da94bccd1cc80
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100633"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Cette fonctionnalité est en préversion et migre votre locataire vers une nouvelle plateforme qui est également en préversion. La migration est irréversible. La nouvelle plateforme prend en charge l’étiquetage unifié afin que les étiquettes que vous créez et gérez puissent être utilisées par plusieurs clients et services.

Migrez vos étiquettes si vous souhaitez être en mesure de les utiliser dans le Centre de sécurité et conformité Office 365, où elles peuvent être publiées et ensuite téléchargées par les [clients qui prennent en charge l’étiquetage unifié](#clients-that-support-unified-labeling). Le client Azure Information Protection continue de télécharger les étiquettes avec la stratégie Azure Information Protection à partir du portail Azure. 

Une fois que vous avez migré vos étiquettes, vous pouvez ensuite les modifier dans le portail Azure ou le Centre de sécurité et conformité Office 365, et les clients respectifs téléchargent la même modification.

## <a name="considerations-for-unified-labels"></a>Éléments à prendre en considération pour les étiquettes unifiées

Avant de migrer vos étiquettes, tenez compte des changements et des considérations qui suivent :

- Actuellement, les clients ne prennent pas tous en charge les étiquettes unifiées. Vérifiez que vous avez des [clients pris en charge](#clients-that-support-unified-labeling) et préparez-vous à des tâches d’administration à la fois dans le portail Azure (pour les clients qui ne prennent pas en charge les étiquettes unifiées) et le Centre de sécurité et conformité (pour les clients qui prennent en charge les étiquettes unifiées).

- Si vous êtes en train de définir et configurer les étiquettes que vous souhaitez utiliser, nous vous recommandons d’effectuer ce processus à l’aide du portail Azure, puis de migrer les étiquettes. Cette stratégie évite la duplication des étiquettes pendant le processus de migration, qui devront ensuite être modifiées dans le Centre de sécurité et conformité.

- Les stratégies, notamment les paramètres de stratégie et les personnes qui y ont accès (stratégies délimitées), ainsi que tous les paramètres avancés du client ne sont pas migrés. Pour ces modifications qui ne sont pas migrées, vous devez configurer les options appropriées dans le Centre de sécurité et conformité une fois que les étiquettes sont migrées.
    
    Pour une expérience utilisateur plus cohérente, nous vous recommandons de publier les mêmes étiquettes dans les mêmes étendues du Centre de sécurité et conformité.

- Les paramètres issus d’une étiquette migrée ne sont pas tous pris en charge par le Centre de sécurité et conformité. Utilisez le tableau de la section [Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et conformité](#label-settings-that-are-not-supported-in-the-security--compliance-center) pour vous aider à identifier ces paramètres et savoir si vous devez exclure les étiquettes migrées de la publication dans le Centre de sécurité et conformité.

- Modèles de protection :
    
    - Les modèles qui utilisent une clé cloud et qui font partie d’une configuration d’étiquettes sont également migrés avec l’étiquette. Les autres modèles de protection ne sont pas migrés. 
    
    - Une fois qu’une étiquette avec des paramètres de protection dans le cloud a été migrée, l’étendue résultante du modèle de protection est l’étendue qui est définie dans le portail Azure (ou à l’aide du module PowerShell ADDRM) et l’étendue qui est définie dans le Centre de sécurité et conformité. 

- Quand vous migrez vos étiquettes,les résultats de la migration indiquent si une étiquette a été **créée**, **mise à jour** ou **renommée** en raison de la duplication :

    - Quand une étiquette est créée, vous devez ensuite la publier dans le Centre de sécurité et conformité pour la rendre disponible aux applications et services.
    
    - Quand une étiquette est renommée, vous devez ensuite la modifier, ce que vous pouvez faire dans le Centre de sécurité et conformité ou le portail Azure. 

- Pour chaque étiquette, le portail Azure indique uniquement le nom d’affichage de l’étiquette, que vous pouvez modifier. Le Centre de sécurité et conformité indique à la fois ce nom d’affichage pour une étiquette et le nom de l’étiquette. Le nom de l’étiquette est le nom initial que vous avez spécifié lors de la création de l’étiquette et cette propriété est utilisée par le service back-end à des fins d’identification.

- Aucune chaîne localisée pour les étiquettes n’est migrée. Vous devez définir de nouvelles chaînes localisées pour les étiquettes migrées dans le Centre de sécurité et conformité.

- Après la migration, quand vous modifiez une étiquette migrée dans le portail Azure, la même modification est automatiquement répercutée dans le Centre de sécurité et conformité. Toutefois, quand vous modifiez une étiquette migrée dans le Centre de sécurité et conformité, vous devez ensuite mettre à jour l’étiquette dans le portail Azure pour qu’elle récupère la modification. Par exemple, modifiez la zone **Add notes for administrator use** (Ajouter des notes pour l’administrateur) dans le panneau **Étiquette**. 

- L’étiquetage unifié est toujours en cours de déploiement sur les locataires. S’il n’est pas encore pris en charge pour votre locataire, la migration n’aboutit pas et annule normalement toutes les modifications. Jusqu’à sa prise en charge pour tous les locataires, vous devez utiliser un lien spécial pour accéder à l’option de migration de vos locataire et étiquettes. Ce lien est fourni dans les instructions qui suivent.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Paramètres d’étiquette qui ne sont pas pris en charge dans le Centre de sécurité et conformité

Utilisez le tableau suivant pour identifier les paramètres de configuration d’une étiquette migrée qui ne sont pas pris en charge pour les clients qui utilisent ces étiquettes, et pour savoir si vous devez modifier et publier l’étiquette migrée dans le Centre de sécurité et conformité. Si vous publiez des étiquettes identifiées comme devant être exclues de la publication, aucune étiquette ne s’affiche pour les clients qui prennent en charge l’étiquetage unifié.

Les clients Azure Information Protection peuvent utiliser ces paramètres d’étiquette sans aucun problème, car ils continuent de télécharger les étiquettes à partir du portail Azure.

|Configuration d’étiquettes|Prise en charge dans le Centre de sécurité et conformité|Exclure de la modification et de la publication dans le Centre de sécurité et conformité|
|-------------------|---------------------------------------------|-------------------------|
|État activé ou désactivé<br /><br />Remarques : Pas de synchronisation avec le Centre de sécurité et conformité |Non applicable|Non applicable|
|Couleur d’étiquette : sélectionnez une valeur dans la liste ou spécifiez-la à l’aide du code RVB<br /><br />Remarques : Les couleurs d’étiquettes ne sont pas prises en charge par le Centre de sécurité et conformité |Non applicable|Non applicable|
|Protection dans le cloud ou protection basée sur HYOK à l’aide d’un modèle prédéfini |Non|Oui|
|Protection dans le cloud à l’aide des autorisations définies par l’utilisateur dans Word, Excel et PowerPoint |Non|Oui|
|Protection basée sur HYOK à l’aide des autorisations définies par l’utilisateur dans Outlook pour l’option Ne pas transférer |Non|Oui|
|Supprimer la protection |Non|Oui|
|Marquages visuels (en-tête, pied de page, filigrane) : police personnalisée et couleur de police personnalisée par code RVB|Non|Recommandée si vous utilisez des variables<br /><br />- Sur les clients, les variables s’affichent sous forme de texte au lieu d’afficher les valeurs dynamiques|
|Marquages visuels par application|Non|Recommandée si vous utilisez des variables<br /><br />- Sur les clients, les variables s’affichent sous forme de texte au lieu d’afficher les valeurs dynamiques|
|Conditions et paramètres associés <br /><br />Remarques : Inclut l’étiquetage automatique et recommandé ainsi que les info-bulles|Non applicable|Non|


## <a name="to-migrate-azure-information-protection-labels"></a>Pour migrer des étiquettes Azure Information Protection

> [!IMPORTANT]
> Ne migrez pas vos étiquettes tant que vous n’avez pas confirmé que vous pouvez modifier et publier des étiquettes de sensibilité dans le Centre de sécurité et conformité Office 365. Les étiquettes de sensibilité commencent à se déployer sur les locataires Office 365, mais ne sont pas encore disponibles pour tous les locataires.
> 
> Pour vérifier : dans le Centre de sécurité et conformité Office 365, accédez à **Classifications** > **Étiquettes** et voyez si vous disposez d’un onglet **Sensibilité**. Si vous ne voyez pas cet onglet, votre locataire n’est pas encore prêt pour les étiquettes de sensibilité et vous ne devez pas migrer vos étiquettes Azure Information Protection pour l’instant.

Après avoir confirmé que votre locataire prend en charge les étiquettes de sensibilité dans le Centre de sécurité et conformité, utilisez les instructions suivantes pour migrer votre locataire et les étiquettes Azure Information Protection.

1. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au portail Azure en utilisant le lien suivant : https://portal.azure.com/?ActivateMigration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/migrationActivationBlade 

2. Dans le panneau **Azure Information Protection - Unified labeling** (Azure Information Protection - Étiquetage unifié), sélectionnez **Activer** et suivez les instructions en ligne.

Les étiquettes qui ont correctement migré peuvent désormais être utilisées par les [clients qui prennent en charge l’étiquetage unifié](#clients-that-support-unified-labeling). Toutefois, vous devez tout d’abord publier ces étiquettes dans le Centre de sécurité et conformité.


### <a name="clients-that-support-unified-labeling"></a>Clients qui prennent en charge l’étiquetage unifié

Les clients qui prennent en charge l’étiquetage unifié sont notamment :

- Applications du programme Office Insider. Pour plus d’informations, consultez la section [Où cette fonctionnalité est-elle disponible aujourd’hui ?](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable) dans la documentation Office.
    
- Clients des éditeurs de logiciels et développeurs qui utilisent le [SDK MIP](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference).


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration et la publication de vos étiquettes migrées dans le Centre de sécurité et conformité Office 365, consultez le billet de blog [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492).