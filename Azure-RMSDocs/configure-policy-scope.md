---
title: Configurer des stratégies délimitées pour Azure Information Protection – AIP
description: Pour configurer différents paramètres et étiquettes pour des utilisateurs spécifiques, vous devez configurer une stratégie délimitée pour Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b815109ddaa62c48a5034d3277b807495d0a7a97
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806615"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Quand la stratégie Azure Information Protection se télécharge sur des ordinateurs sur lesquels est installé le client Azure Information Protection, tous les utilisateurs obtiennent les paramètres et étiquettes de la stratégie par défaut ou les modifications que vous avez configurées pour la stratégie globale. Si vous souhaitez compléter cette configuration pour des utilisateurs spécifiques, en utilisant des paramètres et des étiquettes différents, vous devez créer une **stratégie délimitée** configurée pour ces utilisateurs.

## <a name="how-scoped-policies-work"></a>Fonctionnement des stratégies délimitées

Pour les applications prenant en charge le client Azure Information Protection, tous les utilisateurs reçoivent la stratégie globale, qui contient la barre de titre et l’info-bulle, les paramètres globaux et les étiquettes globales Information Protection. Si vous avez configuré des stratégies délimitées pour des utilisateurs spécifiques, ces utilisateurs reçoivent alors ces paramètres et étiquettes supplémentaires. 

Notez qu’en plus des applications de bureau Office qui prennent en charge le client Azure Information Protection, les étiquettes sont aussi prises en charge avec PowerShell et le scanneur Azure Information Protection. Vous pouvez donc créer et configurer des stratégies délimitées pour les comptes qui exécutent des commandes PowerShell, ou le scanneur. 

Les stratégies délimitées, comme les étiquettes, sont classées dans le portail Azure. Si un utilisateur est configuré pour plusieurs étendues, une stratégie effective est calculée pour cet utilisateur avant d’être téléchargée. Selon l’ordre des stratégies, le dernier paramètre de stratégie est appliqué. Les étiquettes que l’utilisateur voit proviennent de la stratégie globale et des étiquettes supplémentaires des stratégies délimitées auxquelles appartient l’utilisateur.

L’exception est lorsqu’un utilisateur de votre locataire ouvre un document ou un e-mail étiqueté et que cet utilisateur n’est pas inclus dans l’étendue de l’étiquette. Dans ce scénario, l’utilisateur voit le nom de l’ensemble d’étiquettes, mais l’étiquette n’est pas affichée comme étant disponible pour la sélection.  

Étant donné qu’une stratégie délimitée hérite toujours des étiquettes et paramètres de la stratégie globale, les étiquettes de la stratégie globale s’affichent quand vous créez ou modifiez une stratégie délimitée. Toutefois, vous ne pouvez pas modifier les étiquettes de la stratégie globale quand vous modifiez une stratégie délimitée. En revanche, vous pouvez ajouter des sous-étiquettes à ces étiquettes héritées.

Par exemple, si vous disposez d’une étiquette nommée **Confidentiel** dans la stratégie globale, tous les utilisateurs la voient. Vous ne pouvez pas la supprimer ni la réorganiser avec une stratégie délimitée. Mais vous pouvez éventuellement créer une stratégie délimitée pour le service Marketing permettant d’ajouter une nouvelle sous-étiquette à Confidentiel, afin que ces utilisateurs voient **Confidentiel\Promotions**. Vous devez également créer une autre stratégie délimitée pour le service commercial qui ajoute une nouvelle sous-étiquette à la sous-étiquette Confidentiel, afin que ces utilisateurs voient **Confidentiel\Partenaires**. Chaque sous-étiquette peut alors être configurée pour des paramètres différents et la sous-étiquette est uniquement visible pour les utilisateurs relevant des services respectifs.

## <a name="configure-a-scoped-policy"></a>Configurer une stratégie délimitée

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**.

    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **classifications**  >  **stratégies** : dans le volet **Azure information protection-stratégies** , sélectionnez **Ajouter une nouvelle stratégie**. Vous voyez alors le volet **stratégie** qui affiche votre stratégie globale existante, où vous pouvez désormais configurer votre nouvelle stratégie délimitée.

3. Spécifiez le nom et la description de la stratégie que seuls les administrateurs voient dans le portail Azure. Ce nom doit être unique pour votre locataire. Sélectionnez ensuite **spécifier les utilisateurs/groupes qui obtiennent cette stratégie** et dans les volets suivants, vous pouvez rechercher et sélectionner les utilisateurs et les groupes pour cette stratégie. Les étiquettes et paramètres que vous configurez dans cette stratégie délimitée sont appliqués à ces utilisateurs uniquement.
    
    Pour des raisons de performances, l’appartenance au groupe des stratégies délimitées est [mise en cache](prepare.md#group-membership-caching-by-azure-information-protection).

    > [!NOTE]
    > Sélectionnez jusqu’à 200 utilisateurs ou groupes. Si plus de 200 utilisateurs sont nécessaires pour obtenir la stratégie délimitée, créez un groupe, ajoutez des utilisateurs appropriés au groupe, puis définissez l’étendue de la stratégie sur le nouveau groupe. 

4. Maintenant, ajoutez des étiquettes ou configurez les paramètres de la stratégie délimitée. La stratégie globale est toujours appliquée en premier, afin de compléter la stratégie globale avec les nouvelles étiquettes et de remplacer les paramètres globaux. Par exemple, la stratégie globale peut ne pas avoir d’étiquette par défaut spécifiée et vous configurez une étiquette par défaut différente dans les différentes stratégies délimitées à des services spécifiques.

    Si vous avez besoin d’aide pour la configuration des étiquettes ou des paramètres, utilisez les liens de la section Configuration de la [stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy) .

6. Tout comme lorsque vous modifiez la stratégie globale, lorsque vous apportez des modifications dans un volet de Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications ou sur **Ignorer** pour rétablir les derniers paramètres enregistrés. 

7. Lorsque vous avez terminé d’apporter les modifications souhaitées pour cette stratégie délimitée, dans le volet **Azure information protection-stratégies** initiales, assurez-vous que cette stratégie délimitée respecte l’ordre dans lequel vous souhaitez l’appliquer. Cette vérification s’avère importante quand vous avez sélectionné le même utilisateur pour plusieurs stratégies délimitées. Pour changer l’ordre, sélectionnez le menu contextuel (**...**), puis **Monter** ou **Descendre**. 

Le client Azure Information Protection vérifie toutes les modifications à chaque démarrage d’une application Office prise en charge ou à chaque ouverture de l’Explorateur de fichiers. Il télécharge les modifications dans la stratégie globale ou les stratégies délimitées qui s’appliquent à cet utilisateur.

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, suivez le tutoriel [Modifier la stratégie et créer une nouvelle étiquette](infoprotect-quick-start-tutorial.md).
