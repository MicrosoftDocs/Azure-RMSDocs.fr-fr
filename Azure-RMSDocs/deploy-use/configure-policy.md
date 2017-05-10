---
title: "Configurer la stratégie Azure Information Protection"
description: "Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f412d36e8c58d874360c55c5c90416c2629ed69e
ms.sourcegitcommit: e3974cc1490581414084669632cad54b12b05d5a
ms.translationtype: HT
ms.contentlocale: fr-FR
---
# <a name="configuring-azure-information-protection-policy"></a>Configuration de la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection. Cette stratégie est ensuite téléchargée sur les ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Pour configurer la stratégie Azure Information Protection :

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général.

2. Accédez au panneau **Azure Information Protection**: par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 

    Lors de son chargement, le panneau **Azure Information Protection** ouvre automatiquement le panneau **Stratégie : Globale**, où vous pouvez afficher et modifier la stratégie globale que tous les utilisateurs obtiennent. Toutefois, vous pouvez également ajouter et modifier des stratégies délimitées. Les stratégies Azure Information Protection contiennent les éléments suivants que vous pouvez configurer :

    - Les étiquettes qui permettent aux utilisateurs de classifier des documents et des e-mails.

    - Le titre et l’info-bulle de la barre Information Protection, que les utilisateurs voient dans leurs applications Office.

    - L’option permettant d’appliquer la classification lorsque des utilisateurs enregistrent des documents et envoient des e-mails.

    - L’option permettant de définir une étiquette par défaut comme point de départ de la classification de documents et d’e-mails.

    - L’option invitant les utilisateurs à fournir une raison lorsqu’ils sélectionnent une étiquette qui a une sensibilité inférieure à l’étiquette originale.

    - L’option d’étiqueter automatiquement un e-mail en fonction de ses pièces jointes.

    - L’option permettant de fournir un lien d’aide personnalisé aux utilisateurs.

Azure Information Protection est livré avec une [stratégie par défaut](configure-policy-default.md), qui contient cinq étiquettes principales. Ces étiquettes peuvent être utilisées avec la gamme complète des données généralement créées et stockées par une organisation, de la classification la plus basse des données personnelles à la classification la plus élevée des données hautement confidentielles. Vous pouvez utiliser les étiquettes par défaut sans les modifier, vous pouvez les personnaliser, ou encore les supprimer et créer de nouvelles étiquettes.

Lorsque vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. 

Lorsque vous avez terminé les modifications souhaitées, cliquez sur **Publier**. 

Le client Azure Information Protection vérifie si des modifications ont été apportées au démarrage d’une application Office prise en charge et télécharge les modifications en tant que dernière stratégie Azure Information Protection. Autres déclencheurs qui actualisent la stratégie sur le client :

- Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier.

- Lorsque vous exécutez les applets de commande PowerShell pour l’étiquetage et la protection (Get-AIPFileStatus et Set-AIPFileLabel).

- Toutes les 24 heures.

>[!NOTE]
>Quand le client télécharge la stratégie, attendez quelques minutes pour qu’elle soit entièrement opérationnelle. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration de la stratégie et la connectivité réseau. Si l’action résultante des étiquettes ne correspond pas à vos derniers changements, attendez 15 minutes au plus et réessayez.

## <a name="configuring-your-organizations-policy"></a>Configuration de la stratégie de votre organisation

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

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
