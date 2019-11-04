---
title: Nouvelle étiquette Azure Information Protection – AIP
description: Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes que les utilisateurs voient dans la barre Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 6ffbe770864c2776abba2f2a726e07953baf5be4
ms.sourcegitcommit: fbd1834eaacb17857e59421d7be0942a9a0eefb2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445087"
---
# <a name="how-to-create-a-new-label-for-azure-information-protection"></a>Comment créer une étiquette pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Même si Azure Information Protection est fourni avec des étiquettes par défaut que vous pouvez personnaliser, vous pouvez également créer vos propres étiquettes.

Vous pouvez ajouter une nouvelle étiquette ou sous-étiquette à une étiquette existante quand vous avez besoin d’un niveau supplémentaire de classification. Par exemple, la dernière étiquette de la [stratégie par défaut](configure-policy-default.md) contient des sous-étiquettes.

Lorsque vous créez la première sous-étiquette d’une étiquette, les utilisateurs ne peuvent plus sélectionner l’étiquette parente d’origine. Si nécessaire, créez une nouvelle sous-étiquette pour recréer les paramètres d’étiquette parente et permettre aux utilisateurs d’appliquer les mêmes paramètres.

Utilisez les instructions suivantes pour ajouter une nouvelle étiquette, qui pourra ensuite être ajoutée à une stratégie Azure Information Protection.

## <a name="to-create-a-new-label"></a>Pour créer une nouvelle étiquette

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **Classifications** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, effectuez l’une des actions suivantes :
    
    - Pour créer une étiquette, cliquez sur **Ajouter une nouvelle étiquette**.
    
    - Pour créer une sous-étiquette, cliquez avec le bouton droit ou sélectionnez le menu contextuel ( **...** ) de l’étiquette pour laquelle vous voulez créer une sous-étiquette, puis cliquez sur **Ajouter une sous-étiquette**.

3. Dans le panneau **Étiquette** ou **Sous-étiquette**, sélectionnez les options que vous souhaitez pour cette nouvelle étiquette, puis cliquez sur **Enregistrer**.
    
    Lorsque vous spécifiez un nom d’affichage, certains caractères ne peuvent pas être spécifiés (par exemple la barre oblique inverse et l’esperluette), car ils ne sont pas pris en charge pour tous les services et applications utilisant Azure Information Protection. Outre les caractères qui sont bloqués, ne spécifiez pas le caractère **#** .    
    
    Notez que la couleur noire est automatiquement affectée aux nouvelles étiquettes. Choisissez une couleur distinctive dans la liste des couleurs ou entrez un code (triplet hexadécimal) représentant les composants RVB (rouge, vert, bleu) de la couleur. Par exemple, **#DAA520**. Si vous avez besoin d’une référence pour ces codes, vous trouverez une table utile à partir de la page [\<color >](https://developer.mozilla.org/docs/Web/CSS/color_value) à partir des documents Web MSDN. Vous trouverez également ces codes dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

4. Pour rendre votre nouvelle étiquette disponible aux utilisateurs : à partir de l’option de menu **Classifications** > **Stratégies**, sélectionnez la stratégie qui doit contenir la nouvelle étiquette. Sélectionnez **Ajouter ou supprimer des étiquettes**. Sélectionnez l’étiquette à partir du panneau **Stratégie : ajouter ou supprimer des étiquettes**, sélectionnez **OK**, puis **Enregistrer**.
    
    >[!TIP]
    >Dans le cas des nouvelles étiquettes, nous vous conseillons de les ajouter d’abord à une stratégie délimitée que vous utilisez à des fins de test. Quand vous êtes satisfait des résultats, supprimez l’étiquette de cette étendue de test, puis ajoutez-la à une stratégie que vous utilisez en production.     
    
    Pour plus d’informations sur l’ajout d’étiquettes, consultez [Guide pratique pour ajouter ou supprimer une étiquette](configure-policy-add-remove-label.md).
    
    Vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

5. Si vous souhaitez que ces nouveaux nom d’étiquette et description s’affichent dans différentes langues pour les utilisateurs, suivez les procédures indiquées dans le [Guide pratique pour configurer des étiquettes pour des langues différentes](configure-policy-languages.md). 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  


