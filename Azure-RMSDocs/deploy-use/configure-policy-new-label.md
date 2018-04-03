---
title: Nouvelle étiquette Azure Information Protection
description: Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/20/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.openlocfilehash: f24b4e8ac44377ab1c0b18244a376971ade87ebb
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Comment créer une étiquette pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection.

Vous pouvez ajouter une nouvelle étiquette ou sous-étiquette à une étiquette existante quand vous avez besoin d’un niveau supplémentaire de classification. Par exemple, la dernière étiquette de la [stratégie par défaut](configure-policy-default.md) contient des sous-étiquettes.

Lorsque vous créez la première sous-étiquette d’une étiquette, les utilisateurs ne peuvent plus sélectionner l’étiquette parente d’origine. Si nécessaire, créez une nouvelle sous-étiquette pour recréer les paramètres d’étiquette parente et permettre aux utilisateurs d’appliquer les mêmes paramètres.

Utilisez les instructions suivantes pour ajouter une étiquette à la stratégie Azure Information Protection.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si la nouvelle étiquette à ajouter s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**.
    
    Si la nouvelle étiquette à ajouter concerne les utilisateurs sélectionnés dans une [stratégie délimitée](configure-policy-scope.md), dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Dans le panneau **Azure Information Protection - Stratégie globale** ou le panneau **Stratégie :\<nom>**, effectuez l’une des actions suivantes :
    
    - Pour créer une étiquette, cliquez sur **Ajouter une nouvelle étiquette**.
    
    - Pour créer une sous-étiquette, cliquez avec le bouton droit ou sélectionnez le menu contextuel (**...**) de l’étiquette pour laquelle vous voulez créer une sous-étiquette, puis cliquez sur **Ajouter une sous-étiquette**.

4. Dans le panneau **Étiquette** ou **Sous-étiquette**, sélectionnez les options que vous souhaitez pour cette nouvelle étiquette, puis cliquez sur **Enregistrer**.
    
    Lorsque vous spécifiez un nom d’affichage, certains caractères ne peuvent pas être spécifiés (par exemple la barre oblique inverse et l’esperluette), car ils ne sont pas pris en charge pour tous les services et applications utilisant Azure Information Protection. Outre les caractères qui sont bloqués, ne spécifiez pas le caractère **#**.    
    
    Notez que la couleur noire est automatiquement affectée aux nouvelles étiquettes. Choisissez une couleur distinctive dans la liste des couleurs ou entrez un code (triplet hexadécimal) représentant les composants RVB (rouge, vert, bleu) de la couleur. Par exemple, **#DAA520**. Si vous souhaitez obtenir des informations de référence sur ces codes, la page [Colors by Name](https://msdn.microsoft.com/library/aa358802\(v=vs.85).aspx) dans la documentation MSDN constitue un bon point de départ. Ces codes sont utilisés dans de nombreux programmes de retouche d’images, par exemple Microsoft Paint. Quand vous choisissez une couleur personnalisée à partir d’une palette, les valeurs RVB s’affichent automatiquement.

5. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** initial sur **Publier**.

6. Si vous souhaitez que ces nouveaux nom d’étiquette et description s’affichent dans différentes langues pour les utilisateurs, suivez les procédures de [Guide pratique pour configurer des étiquettes pour des langues différentes](configure-policy-languages.md). 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

