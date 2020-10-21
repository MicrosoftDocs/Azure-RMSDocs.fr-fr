---
title: Démarrage rapide – Affichage d’Azure Information Protection (AIP) sur le Portail Azure
description: Si Azure Information Protection (AIP) est nouveau pour votre organisation, suivez ce guide pour ajouter le service au Portail Azure, vérifier que le service de protection est activé et publier les étiquettes et les paramètres de stratégie.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 29c79c49de5d28c82281614846f5938ecbf40f89
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91587896"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Démarrage rapide : Bien démarrer avec Azure Information Protection dans le portail Azure

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Dans ce démarrage rapide, vous allez ajouter Azure Information Protection au portail Azure, vérifier que le service de protection est activé, créer des étiquettes par défaut si vous n’avez pas d’étiquettes et afficher les paramètres de stratégie pour le client Azure Information Protection (classique).

**Temps nécessaire :** Ce démarrage rapide prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour effectuer ce démarrage rapide, les éléments suivants sont requis :

- L’accès à votre compte [**Portail Azure**](https://portal.azure.com/)

- Un abonnement comportant le [**plan Azure Information Protection 1 ou 2**](https://azure.microsoft.com/pricing/details/information-protection/)

    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Ajouter Azure Information Protection au Portail Azure

Même si vous disposez d’un abonnement comportant le plan Azure Information Protection 1 ou 2, AIP n’est pas automatiquement disponible sur le Portail Azure.

Pour ajouter AIP au Portail Azure, procédez ainsi :

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec le compte Administrateur général de votre locataire.

    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. Sélectionnez **+ Créer une ressource**. Dans la zone de recherche de la Place de marché, tapez puis sélectionnez **Azure Information Protection**. Sur la page Azure Information Protection, sélectionnez **Créer**, puis à nouveau **Créer**.

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Ajout d’Azure Information Protection au Portail Azure":::

    > [!TIP]
    > Si c’est la première fois que vous effectuez cette étape, une icône **Épingler au tableau de bord** ![icône Épingler au tableau de bord](media/qs-tutor/pin-to-dashboard.png "Icône Épingler au tableau de bord") apparaît à côté du nom du volet. Sélectionnez-la pour créer une vignette dans votre tableau de bord vous permettant d’y accéder directement la prochaine fois.

## <a name="confirm-that-the-protection-service-is-activated"></a>Vérification de l’activation du service de protection

Le service de protection est maintenant activé automatiquement pour les nouveaux clients. Vérifiez qu’il est activé maintenant ou plus tard de la façon suivante :

1. Dans le volet **Azure Information Protection**, sélectionnez **Gérer** > **Activation de la protection**.

1. Vérifiez que la protection est activée pour votre locataire. Par exemple :

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="Ajout d’Azure Information Protection au Portail Azure":::

    Si la protection n’est pas activée et que vous devez l’activer, sélectionnez **Activer** ![Activer AIP](media/qs-tutor/activate.png "Activer AIP"). Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

## <a name="create-and-publish-labels"></a>Créer et publier des étiquettes

Votre entreprise peut déjà disposer d’étiquettes, car elles ont été créées automatiquement pour votre locataire, ou parce que vous avez des étiquettes de sensibilité dans le Centre de sécurité et de conformité Office 365, le centre de sécurité Microsoft ou le centre de conformité Microsoft. Voyons voir :

1. Sous **Classifications**, sélectionnez **Étiquettes**.

    Il se peut que des étiquettes par défaut aient déjà été créées. L’illustration suivante indique les étiquettes créées par défaut avec Azure Information Protection :

    :::image type="content" source="media/info-protect-defaultlabels.png" alt-text="Ajout d’Azure Information Protection au Portail Azure":::

    **Si les étiquettes par défaut n’apparaissent pas ou en l’absence d’étiquette** :

    Si les étiquettes par défaut n’apparaissent pas ou en l’absence d’étiquette, sélectionnez **Générer les étiquettes par défaut** pour les créer et pouvoir ainsi les utiliser dans le client classique.

    Si vous ne voyez pas le bouton **Générer les étiquettes par défaut** au-dessus de la grille, sélectionnez **Étiquetage unifié** sous **Gérer**. Si l’état d’étiquetage unifié est **Non activé**, sélectionnez **Activer**, puis revenez au volet **Classification** > **Étiquettes**.

    > [!NOTE]
    > Pour le client d’étiquetage unifié, les étiquettes sont gérées dans Microsoft 365. Pour plus d’informations, consultez [Restriction de l’accès au contenu à l’aide du chiffrement dans les étiquettes de confidentialité](/microsoft-365/compliance/encryption-sensitivity-labels).
    >

1. Publiez vos étiquettes sur le Portail Azure pour les rendre accessibles au client classique Azure Information Protection :

    1. Ouvrez la stratégie **Globale**. Sous **Classifications**, sélectionnez **Stratégies** > **Globale**.

    1. Sélectionnez **Ajouter ou supprimer des étiquettes**.

    1. Dans le panneau **Stratégie : Ajouter ou supprimer des étiquettes**, sélectionnez toutes les étiquettes, puis **OK**.

    1. De retour dans le panneau **Stratégie : Globale**, sélectionnez le bouton **Enregistrer** ![Enregistrer](media/qs-tutor/save-icon.png "Enregistrer").

        À l’invite, cliquez sur **OK** pour publier vos modifications.

## <a name="view-your-labels"></a>Afficher vos étiquettes

Vous pouvez maintenant vous familiariser avec vos étiquettes.

Si la stratégie **Globale** est toujours ouverte, cliquez sur la croix **X** en haut à droite pour fermer le volet. Sous **Classifications**, sélectionnez **Étiquettes**.

Voici les étiquettes de classification Azure Information Protection par défaut :

- **Personnel**
- **Général**
- **Confidentiel**
- **Hautement confidentiel**

Par défaut, des marquages visuels sont déjà configurés pour certaines étiquettes. Il peut s’agir d’un pied de page, d’un en-tête ou d’un filigrane. La protection est également configurée pour d’autres étiquettes.

Sélectionnez une étiquette et parcourez-la pour voir sa configuration détaillée.

> [!TIP]
> Développez l’étiquette **Hautement confidentiel** pour voir un exemple de classification comportant des sous-catégories.
>

## <a name="view-your-policy-settings"></a>Afficher vos paramètres de stratégie

La première fois que vous vous connectez au service Azure Information Protection sur le Portail Azure, les paramètres de stratégie par défaut utilisés par le client Azure Information Protection sont toujours créés automatiquement.

- **Client classique :** les étiquettes et les paramètres de stratégie sont téléchargés sur le client dans la stratégie Azure Information Protection.

- **Client d’étiquetage unifié :** seules les étiquettes sont téléchargées sur le client. Les paramètres de stratégie sont téléchargés à partir du Centre de sécurité et conformité Office 365, du Centre de conformité Microsoft 365 ou du Centre de sécurité Microsoft 365. Utilisez ces centres d’administration au lieu du portail Azure pour modifier vos étiquettes et stratégies d’étiquette.

    Pour plus d’informations, consultez [Présentation des étiquettes de confidentialité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365.

**Instructions relatives au client classique :**

Pour afficher les paramètres de la stratégie Azure Information Protection par défaut pour le client classique :

1. Sous **Classifications**, sélectionnez **Stratégies** > **Général** afin d’afficher les paramètres de stratégie Azure Information Protection créés par défaut pour votre locataire.

1. Les paramètres de stratégie apparaissent après les étiquettes, dans la section **Configurer les paramètres à présenter et à appliquer aux utilisateurs finaux d’Information Protection**. Par exemple, aucune étiquette par défaut n’est définie, les documents ou e-mails ne doivent pas obligatoirement avoir une étiquette et les utilisateurs n’ont pas à fournir de justification quand ils changent les étiquettes :

    :::image type="content" source="media/defaultsettings-aip.png" alt-text="Ajout d’Azure Information Protection au Portail Azure":::

1. Vous pouvez maintenant fermer les volets du portail que vous avez ouverts.

## <a name="next-steps"></a>Étapes suivantes

Les étapes suivantes sont différentes pour le client classique et le client d’étiquetage unifié. Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).

**Si vous utilisez le client classique :**

- Vous trouverez peut-être le tutoriel suivant utile pour poursuivre : [Modifier la stratégie et créer une étiquette pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

- Pour obtenir des instructions détaillées sur la configuration de tous les aspects de la stratégie Azure Information Protection, voir [Configurer la stratégie Azure Information Protection](configure-policy.md).

**Si vous utilisez le client d’étiquetage unifié :**

Consultez [Découvrir les étiquettes de confidentialité](/microsoft-365/compliance/sensitivity-labels) dans la documentation sur la conformité Microsoft 365.