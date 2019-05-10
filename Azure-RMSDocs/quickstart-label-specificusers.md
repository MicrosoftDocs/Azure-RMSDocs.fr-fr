---
title: 'Démarrage rapide : Nouvelle étiquette Azure Information Protection pour des utilisateurs spécifiques – AIP'
description: Créez et configurez une nouvelle étiquette qui classifie les documents et e-mails pour un sous-ensemble d’utilisateurs à l’aide d’une stratégie délimitée.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 15359fac56b4bef68ae9668a31c82a8b742b208f
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767843"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>Démarrage rapide : Créer une étiquette Azure Information Protection pour des utilisateurs spécifiques

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Ce démarrage rapide vise à créer une nouvelle étiquette qui n’est visible et applicable que par certains utilisateurs pour classifier et protéger leurs documents et e-mails.

Cette configuration utilise une stratégie délimitée.

Cette configuration prend moins de 10 minutes.

## <a name="prerequisites"></a>Prérequis

Pour pouvoir suivre ce guide de démarrage rapide, il vous faut :

1. Un abonnement comportant le plan Azure Information Protection 1 ou 2.
    
    Si vous n’avez aucun de ces abonnements, vous pouvez créer un compte [gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) pour votre organisation.

2. Vous avez ajouté le panneau Azure Information Protection au Portail Azure et vérifié que le service de protection est activé.

    Si vous avez besoin d’aide avec ces actions, consultez [Démarrage rapide : Bien démarrer avec le portail Azure](quickstart-viewpolicy.md).

3. Un groupe compatible avec les e-mails dans Azure AD et contenant les utilisateurs qui verront et appliqueront la nouvelle étiquette.
    
    Si vous n’avez pas de groupe adapté, créez-en un nommé **Sales Team** et ajoutez au moins un utilisateur.

4. Pour tester la nouvelle étiquette : le client Azure Information Protection doit être installé sur les ordinateurs des utilisateurs. 
    
    Pour tester l’étiquette par vous-même, vous pouvez installer le client en accédant au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) et en téléchargeant **AzInfoProtection.exe** sur la page Azure Information Protection.

Pour obtenir la liste complète des prérequis d’Azure Information Protection, voir [Prérequis d’Azure Information Protection](requirements.md).
    
## <a name="create-a-new-label"></a>Créer une étiquette

Commencez par créer votre nouvelle étiquette.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.
    
    Si vous n’êtes pas l’administrateur général, utilisez le lien suivant pour les autres rôles : [Connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal)

2. À partir de l’option de menu **Classifications** > **Étiquettes** : Dans le panneau **Azure Information Protection - Étiquettes**, cliquez sur **Ajouter une nouvelle étiquette**.

3. Dans le panneau **Étiquette**, spécifiez au moins les éléments suivants :
    
    - **Nom d'affichage de l’étiquette** : Nom de l’étiquette que verront les utilisateurs et qui identifie la classification du contenu. Par exemple : `Sales - Restricted`.
    
    - **Description** : Info-bulle qui aide les utilisateurs à savoir quand sélectionner cette nouvelle étiquette. Par exemple : `Business data that is restricted to the Sales Team.`

4. Vérifiez que l’option est marquée **Activé** **(valeur par défaut)**, puis sélectionnez **Enregistrer**.

## <a name="add-the-label-to-a-new-scoped-policy"></a>Ajouter l’étiquette à une nouvelle stratégie délimitée

Maintenant, ajoutez votre étiquette à une nouvelle stratégie délimitée.

1. À partir de l’option de menu **Classifications** > **Stratégies** : Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez **Ajouter une nouvelle stratégie**. 

2. Dans la zone **Nom de la stratégie** du panneau **Stratégie**, entrez un nom identifiant le groupe d’utilisateurs qui verra votre nouvelle étiquette. Par exemple, `Sales`.

3. Sélectionnez l’option **Sélectionner les utilisateurs ou groupes qui recevront cette stratégie**.

4. Dans le panneau **Utilisateurs et groupes AAD**, sélectionnez **Utilisateurs/groupes**. Puis, dans le nouveau panneau **Utilisateurs/groupes**, recherchez et sélectionnez le groupe que vous avez identifié dans les prérequis. Par exemple, **Sales Team**. Cliquez sur **Sélectionnez** dans ce panneau, puis sur **OK**.

5. Dans le panneau **Stratégie**, sélectionnez **Ajouter ou supprimer des étiquettes**.

6. Dans le panneau **Stratégie : Ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette que vous avez créée, par exemple, **Sales - Restricted**, puis **OK**.

7. Dans le panneau **Stratégie**, sélectionnez **Enregistrer**. 

Votre nouvelle étiquette est maintenant publiée auprès des membres du groupe que vous avez spécifié. 

## <a name="test-your-new-label"></a>Tester la nouvelle étiquette

Pour tester cette étiquette, il vous faut au minimum deux ordinateurs, car le client Azure Information Protection ne prend pas en charge plusieurs utilisateurs sur le même ordinateur :

 - Sur le premier ordinateur, connectez-vous en tant que membre du groupe Sales Team. Ouvrez Word et vérifiez que la nouvelle étiquette apparaît. Si Word est déjà ouvert, redémarrez-le pour forcer l’actualisation de la stratégie.

- Sur le second ordinateur, connectez-vous en tant qu’utilisateur non membre du groupe Sales Team. Ouvrez Word et vérifiez que la nouvelle étiquette n’apparaît pas. Comme auparavant, si Word est déjà ouvert, redémarrez-le.

## <a name="clean-up-resources"></a>Nettoyer les ressources

Si vous ne souhaitez pas conserver cette étiquette et cette stratégie délimitée, suivez cette procédure :

1. À partir de l’option de menu **Classifications** > **Stratégies** : Dans le panneau **Azure Information Protection – Stratégies**, sélectionnez le menu contextuel (**…**) de la stratégie délimitée que vous avez créée. Par exemple, **Sales**.

2. Sélectionnez **Supprimer la stratégie**, puis **OK** si une confirmation vous est demandée.

3. Dans l’option de menu **Classifications** > **Étiquette** : Dans le panneau **Azure Information Protection – Étiquette**, sélectionnez le menu contextuel (**…**) de l’étiquette que vous avez créée.  par exemple, **Sales - Restricted**.

4.  Sélectionnez **Supprimer cette étiquette**, puis **OK** si une confirmation vous est demandée.


## <a name="next-steps"></a>Étapes suivantes

Ce démarrage rapide détaille les options de base afin de vous permettre de créer rapidement une nouvelle étiquette pour des utilisateurs spécifiques. Pour obtenir les instructions complètes, consultez les articles suivants :

- [Comment créer une étiquette](configure-policy-new-label.md)

- [Guide pratique pour configurer la stratégie pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md)

Par ailleurs, si vous souhaitez que l’étiquette protège le contenu de telle sorte que seuls les membres de Sales Team puissent l’ouvrir, il vous faut la configurer de façon à appliquer la protection. Pour obtenir des instructions, voir [Guide pratique pour configurer une étiquette pour la protection Rights Management](configure-policy-protection.md).

