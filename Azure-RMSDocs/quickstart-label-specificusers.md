---
title: 'Démarrage rapide : Nouvelle étiquette Azure Information Protection pour des utilisateurs spécifiques – AIP'
description: Créez et configurez une nouvelle étiquette qui classifie les documents et e-mails pour un sous-ensemble d’utilisateurs à l’aide d’une stratégie délimitée.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: a66b6809047e8d1bd4b8147ea869a87b50e9e912
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809343"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>Démarrage rapide : Créer une étiquette Azure Information Protection pour des utilisateurs spécifiques

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne** : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Ce démarrage rapide vise à créer une nouvelle étiquette Azure Information Protection qui n’est visible et applicable que par certains utilisateurs pour classifier et protéger leurs documents et e-mails.

Cette configuration utilise une stratégie délimitée.

**Temps nécessaire** : Cette configuration prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

|Condition requise  |Description  |
|---------|---------|
|**Un abonnement avec prise en charge**     |  Il vous faut un abonnement comportant [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). </br></br>Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.       |
|**AIP ajouté au Portail Azure**    |  Vous avez ajouté le volet Azure Information Protection au Portail Azure et vérifié que le service de protection est activé. </br></br>Pour plus d’informations, consultez [Démarrage rapide : Bien démarrer avec le portail Azure](quickstart-viewpolicy.md).       |
|**Un groupe à extension messagerie dans Azure AD**     | Il vous faut un groupe à extension messagerie dans Azure AD, contenant les utilisateurs qui verront et appliqueront la nouvelle étiquette. </br></br>Si vous n’avez pas de groupe adapté, créez-en un nommé **Sales Team** et ajoutez au moins un utilisateur. |
|**Client classique installé**    |   Pour que vous puissiez tester la nouvelle étiquette, le client classique doit être installé sur votre ordinateur. </br></br>Le client classique Azure Information Protection est en cours de dépréciation pour mars 2021. Pour le déployer, ouvrez un ticket de support afin d’obtenir l’accès au téléchargement.  |
| | |

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).

## <a name="create-a-new-label"></a>Créer une étiquette

Commencez par créer votre nouvelle étiquette.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com). Accédez ensuite au volet **Azure Information Protection**.

    Par exemple, dans la zone de recherche des ressources, services et documents, commencez à taper **Information** et sélectionnez **Azure Information Protection**.

    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

1. Sous **Classifications**, sélectionnez **Étiquettes**, puis cliquez sur **+ Ajouter une nouvelle étiquette**.

1. Dans le volet **Étiquette**, spécifiez au moins les champs suivants :

    |Champ  |Description  |
    |---------|---------|
    |**Nom d’affichage de l’étiquette**     |    Nom de l’étiquette que verront les utilisateurs et qui identifie la classification du contenu. </br>Par exemple : **Commercial – Accès restreint**.    |
    |**Description**     |   Info-bulle qui aide les utilisateurs à savoir quand sélectionner cette nouvelle étiquette. </br> Par exemple : **Données métier limitées à l’équipe commerciale**.     |
    | | | 

1. Vérifiez que l’option **Activé** est **choisie** (valeur par défaut), puis sélectionnez **Enregistrer** ![Enregistrer](media/qs-tutor/save-icon.png "Enregistrer").

    Sélectionnez la croix **X** en haut à droite pour fermer le volet **Nouvelle étiquette**.

## <a name="add-the-label-to-a-new-scoped-policy"></a>Ajouter l’étiquette à une nouvelle stratégie délimitée

Maintenant, ajoutez votre étiquette à une nouvelle stratégie délimitée.

1. À gauche toujours, sous **Classifications**, sélectionnez **Stratégies**, puis cliquez sur **Ajouter une nouvelle stratégie**.

1. Dans le champ **Nom de la stratégie**, entrez une valeur explicite décrivant les utilisateurs qui verront votre nouvelle étiquette.

    Par exemple, **Sales**.

1. Sélectionnez la ligne **Sélectionner les utilisateurs ou les groupes recevant cette stratégie** pour ouvrir le volet **Utilisateurs et groupes AAD**.

1. Dans le volet **Utilisateurs et groupes AAD**, recherchez et sélectionnez le groupe que vous avez identifié dans les prérequis, par exemple, **Sales Team**.

    Cliquez sur **Sélectionner** pour fermer le volet.

1. Dans le volet **Stratégie**, sous **Nom d’affichage de l’étiquette**, cliquez sur **Ajouter ou supprimer des étiquettes**.

1. Dans le panneau **Stratégie : Ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette que vous avez créée, par exemple, **Sales - Restricted**, puis **OK**.

1. Dans le volet **Stratégie**, sélectionnez **Enregistrer** ![Enregistrer](media/qs-tutor/save-icon.png "Enregistrer").

Votre nouvelle étiquette est maintenant publiée auprès des membres du groupe que vous avez spécifié.

## <a name="test-your-new-label"></a>Tester la nouvelle étiquette

Pour tester cette étiquette, il vous faut au minimum deux ordinateurs, car le client Azure Information Protection ne prend pas en charge plusieurs utilisateurs sur le même ordinateur :

- **Sur le premier ordinateur**, connectez-vous en tant que membre du groupe Sales Team. Ouvrez Word et vérifiez que la nouvelle étiquette apparaît. Si Word est déjà ouvert, redémarrez-le pour forcer l’actualisation de la stratégie.

- **Sur le second ordinateur**, connectez-vous en tant qu’utilisateur *non* membre du groupe Sales Team. Ouvrez Word et vérifiez que la nouvelle étiquette n’apparaît pas. Comme auparavant, si Word est déjà ouvert, redémarrez-le.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous ne souhaitez pas conserver cette étiquette et cette stratégie délimitée, suivez cette procédure :

1. Dans la zone **Classifications** > **Stratégies** : dans le volet **Azure Information Protection – Stratégies**, sélectionnez le menu contextuel ( **…** ) de la stratégie délimitée que vous avez créée. Par exemple, **Sales**.

1. Sélectionnez **Supprimer la stratégie**, puis **OK** si une confirmation vous est demandée.

1. Dans la zone **Classifications** > **Étiquette** : Dans le volet **Azure Information Protection – Étiquette**, sélectionnez le menu contextuel ( **…** ) de l’étiquette que vous avez créée.  par exemple, **Sales - Restricted**.

1. Sélectionnez **Supprimer cette étiquette**, puis **OK** si une confirmation vous est demandée.

## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide couvre les options de base afin de vous permettre de créer rapidement une étiquette pour certains utilisateurs à l’aide du client classique. Pour obtenir les instructions complètes, consultez les articles suivants :

- [Comment créer une étiquette](configure-policy-new-label.md)

- [Guide pratique pour configurer la stratégie pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md)

Par ailleurs, si vous souhaitez que l’étiquette protège le contenu de telle sorte que seuls les membres de Sales Team puissent l’ouvrir, il vous faut la configurer de façon à appliquer la protection. Pour obtenir des instructions, voir [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md).
