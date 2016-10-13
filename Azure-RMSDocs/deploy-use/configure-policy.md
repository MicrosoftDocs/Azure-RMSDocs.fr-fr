---
title: "Configuration de la stratégie | Azure Information Protection"
description: "Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ebb11148718f22c79bb49c82b9855f5e6f2a5b18
ms.openlocfilehash: 472541f32c429eea34ea0afb76905bee8abf9747


---

# Configuration de la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection. Cette stratégie est ensuite téléchargée sur les ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Pour configurer la stratégie Azure Information Protection :

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général.

2. Accédez au panneau **Azure Information Protection**: par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 

    Vous voyez ensuite le panneau **Azure Information Protection**, dans lequel vous pouvez configurer la stratégie Azure Information Protection, qui contient les éléments suivants :

    - Le titre et l’info-bulle de la barre Information Protection, que les utilisateurs voient dans leurs applications Office.

    - Les étiquettes qui permettent aux utilisateurs de classifier des documents et des e-mails.

    - L’option permettant d’appliquer la classification lorsque des utilisateurs enregistrent des documents et envoient des e-mails.

    - L’option permettant de définir une étiquette par défaut comme point de départ de la classification de documents et d’e-mails.

    - L’option invitant les utilisateurs à fournir une raison lorsqu’ils sélectionnent une étiquette qui a un niveau de confidentialité inférieur à l’étiquette originale.


Azure Information Protection est fourni avec une [stratégie par défaut](configure-policy-default.md), qui contient les étiquettes **Personnel**, **Public**, **Interne**, **Confidentiel**, et **Secret**. Vous pouvez utiliser les étiquettes par défaut sans les modifier, vous pouvez les personnaliser, ou encore les supprimer et créer de nouvelles étiquettes.

Lorsque vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. 

Lorsque vous avez terminé les modifications souhaitées, cliquez sur **Publier**. 

Le client Azure Information Protection vérifie si des modifications ont été apportées au démarrage d’une application Office prise en charge et télécharge les modifications en tant que stratégie Azure Information Protection.

## Configuration de la stratégie de votre organisation

Utilisez les informations suivantes pour configurer votre stratégie Azure Information Protection :

- [La stratégie Information Protection par défaut](configure-policy-default.md)

- [Comment configurer les paramètres de stratégie globaux](configure-policy-settings.md)

- [Comment créer une nouvelle étiquette](configure-policy-new-label.md)

- [Comment supprimer ou réorganiser une étiquette](configure-policy-delete-reorder.md)

- [Comment modifier ou personnaliser une étiquette existante](configure-policy-change-label.md)

- [Comment configurer une étiquette pour appliquer la protection](configure-policy-protection.md)

- [Comment configurer une étiquette pour appliquer des marquages visuels](configure-policy-markings.md)

- [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)

## Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).




<!--HONumber=Sep16_HO4-->


