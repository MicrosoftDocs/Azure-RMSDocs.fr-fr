---
title: "Configurer la stratégie Azure Information Protection"
description: "Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7a4922384a228457b683653e80afe4b8c8db6df2
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="configuring-azure-information-protection-policy" class="xliff"></a>

# Configuration de la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection. Cette stratégie est ensuite téléchargée sur les ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

<a id="subscription-support" class="xliff"></a>

## Support d'abonnement

La stratégie Azure Information Protection prend en charge différents niveaux d’abonnement :

- Azure Information Protection P2 : Prise en charge de toutes les fonctionnalités de classification, d’étiquetage et de protection.

- Azure Information Protection P1 : Prise en charge de la plupart des fonctionnalités de classification, d’étiquetage et de protection, mais pas la classification automatique ou le HYOK.

- Office 365 incluant le service Azure Rights Management : prise en charge de la protection, mais pas de la classification et de l’étiquetage.

Les options qui nécessitent un abonnement Azure Information Protection P2 sont dorénavant identifiées dans le portail.

Si vous avez une combinaison d’abonnements pour les utilisateurs de votre client, il vous incombe de vous assurer que la stratégie Azure Information Protection que les utilisateurs téléchargent ne contient pas d’options de configuration que leur compte n’est pas autorisé à utiliser. Lorsque vous configurez des options pour lesquelles tous les utilisateurs ne possèdent pas une licence, utilisez les stratégies délimitées afin que les utilisateurs ne soient pas configurés pour utiliser des fonctionnalités pour lesquels ils n’ont pas une licence.

Pour plus d’informations sur les abonnements, consultez [De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

Pour plus d’informations sur la façon de configurer des stratégies délimitées, consultez [Guide pratique pour configurer la stratégie pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md).

<a id="how-to-configure-the-azure-information-protection-policy" class="xliff"></a>

## Guide de configuration de la stratégie Azure Information Protection

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général.

2. Accédez au panneau **Azure Information Protection**: par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 
    
    La première fois que vous vous connectez au service, la page **Démarrage rapide** s’ouvre automatiquement. Pour configurer la stratégie que tous les utilisateurs obtiennent, cliquez sur **Stratégie globale** pour ouvrir le panneau **Stratégie : Globale**. Ce panneau s’ouvre automatiquement pour les connexions suivantes au service pour afficher et modifier la stratégie globale que tous les utilisateurs obtiennent. 
    
    La stratégie Azure Information Protection contient les éléments suivants que vous pouvez configurer :
    
    - Les étiquettes qui permettent aux utilisateurs de classifier des documents et des e-mails.
    
    - Le titre et l’info-bulle de la barre Information Protection, que les utilisateurs voient dans leurs applications Office.
    
    - L’option permettant d’appliquer la classification lorsque des utilisateurs enregistrent des documents et envoient des e-mails.
    
    - L’option permettant de définir une étiquette par défaut comme point de départ de la classification de documents et d’e-mails.
    
    - L’option invitant les utilisateurs à fournir une raison lorsqu’ils sélectionnent une étiquette qui a une sensibilité inférieure à l’étiquette originale.
    
    - L’option d’étiqueter automatiquement un e-mail en fonction de ses pièces jointes.
    
    - L’option permettant de fournir un lien d’aide personnalisé aux utilisateurs.

Azure Information Protection est livré avec une [stratégie par défaut](configure-policy-default.md), qui contient cinq étiquettes principales. Ces étiquettes peuvent être utilisées avec la gamme complète des données généralement créées et stockées par une organisation, de la classification la plus basse des données personnelles à la classification la plus élevée des données hautement confidentielles. 

Vous pouvez utiliser les étiquettes par défaut sans les modifier, vous pouvez les personnaliser, ou encore les supprimer et créer de nouvelles étiquettes. Pour plus d’informations, utilisez les liens dans la section suivante pour vous aider à localiser les options appropriées et découvrir comment les configurer. 

Lorsque vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. 

Lorsque vous avez terminé les modifications souhaitées, cliquez sur **Publier**. 

Le client Azure Information Protection vérifie si des modifications ont été apportées au démarrage d’une application Office prise en charge et télécharge les modifications en tant que dernière stratégie Azure Information Protection. Autres déclencheurs qui actualisent la stratégie sur le client :

- Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier.

- Lorsque vous exécutez les [applets de commande PowerShell](../rms-client/client-admin-guide-powershell.md) pour l’étiquetage et la protection (Get-AIPFileStatus, Set-AIPFileClassification et Set-AIPFileLabel).

- Toutes les 24 heures.

>[!NOTE]
>Quand le client télécharge la stratégie, attendez quelques minutes pour qu’elle soit entièrement opérationnelle. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration de la stratégie et la connectivité réseau. Si l’action résultante de vos étiquettes ne correspond pas à vos derniers changements, attendez 15 minutes au plus et réessayez.

<a id="configuring-your-organizations-policy" class="xliff"></a>

### Configuration de la stratégie de votre organisation

Utilisez les informations suivantes pour configurer votre stratégie Azure Information Protection :

- [La stratégie Information Protection par défaut](configure-policy-default.md)

- [Guide pratique pour configurer les paramètres de stratégie](configure-policy-settings.md)

- [Comment créer une étiquette](configure-policy-new-label.md)

- [Comment supprimer ou réorganiser une étiquette](configure-policy-delete-reorder.md)

- [Comment modifier ou personnaliser une étiquette existante](configure-policy-change-label.md)

- [Comment configurer une étiquette pour la protection](configure-policy-protection.md)

- [Comment configurer une étiquette pour appliquer des marquages visuels](configure-policy-markings.md)

- [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)

- [Guide pratique pour configurer la stratégie pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md)

- [Guide pratique pour configurer et gérer des modèles](configure-policy-templates.md)

- [Guide pratique pour configurer des étiquettes pour des langues différentes](configure-policy-languages.md)

<a id="next-steps" class="xliff"></a>

## Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
