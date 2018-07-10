---
title: Configurer la stratégie Azure Information Protection
description: Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/28/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 43fade205d4d518f6fc8f5dd7c7280a80d2c7eae
ms.sourcegitcommit: 1bc4c9d6e773809893d02a6abb09aeb4ae28cb03
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2018
ms.locfileid: "34562175"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Configuration de la stratégie Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection. Cette stratégie est ensuite téléchargée sur les ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

## <a name="subscription-support"></a>Support d'abonnement

Azure Information Protection prend en charge différents niveaux d’abonnement :

- Azure Information Protection P2 : Prise en charge de toutes les fonctionnalités de classification, d’étiquetage et de protection.

- Azure Information Protection P1 : Prise en charge de la plupart des fonctionnalités de classification, d’étiquetage et de protection, mais pas la classification automatique ou le HYOK.

- Office 365 incluant le service Azure Rights Management : prise en charge de la protection, mais pas de la classification et de l’étiquetage.

Les options qui nécessitent un abonnement Azure Information Protection P2 sont identifiées dans le portail.

Si votre organisation a différents types d’abonnements, vous êtes responsable de vous assurer que les utilisateurs n’utilisent pas de fonctionnalités que la licence de leur compte ne les autorise pas à utiliser. Le client Azure Information Protection ne procède pas à la vérification et l’application de la licence. Lorsque vous configurez des options pour lesquelles certains utilisateurs n’ont pas de licence, utilisez les stratégies délimitées ou un paramètre du Registre pour vérifier que votre organisation est toujours en conformité avec vos licences :

- **Si votre organisation possède une combinaison de licences Azure Information Protection P1 et Azure Information Protection P2** : pour les utilisateurs qui ont une licence P2, créez et utilisez une ou plusieurs [stratégies délimitées](configure-policy-scope.md) lorsque vous configurez des options qui nécessitent une licence Azure Information Protection P2. Assurez-vous que votre stratégie globale ne contient pas d’options qui nécessitent une licence Azure Information Protection P2.

- **Si votre organisation a un abonnement à Azure Information Protection, mais que certains utilisateurs possèdent uniquement une licence pour Office 365 qui inclut le service Azure Rights Management** : pour les utilisateurs qui n’ont pas de licence pour Azure Information Protection, modifiez le Registre sur leurs ordinateurs pour qu’ils ne téléchargent pas la stratégie Azure Information Protection. Pour obtenir des instructions, consultez le guide d’administration pour la personnalisation suivante : [Appliquer le mode Protection uniquement si votre organisation possède différents types de licences](../rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses).

Pour plus d’informations sur les abonnements, consultez [De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>Connexion au portail Azure

Pour vous connecter au portail Azure et configurer et gérer Azure Information Protection :

- Utilisez le lien suivant : https://portal.azure.com

- Utilisez un compte avec l’un des [rôles d’administrateur](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants :
    
    - **Administrateur Information Protection**

    - **Administrateur de sécurité**

    - **Administrateur général/administrateur de la société**


## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>Pour accéder au panneau Azure Information Protection pour la première fois

1. Connectez-vous au portail Azure.

2. Dans le menu hub, sélectionnez **Créer une ressource**, puis, à partir de la zone de recherche pour la Place de marché, tapez **Azure Information Protection**. 
    
3. Dans la liste des résultats, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.
    
    > [!TIP] 
    > Ou sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.
    
    Cliquez sur **Créer** à nouveau.

4. Vous voyez la page **Démarrage rapide** qui s’ouvre automatiquement la première fois que vous vous connectez au service. Parcourez les ressources suggérées ou utilisez les autres options de menu. Pour configurer les étiquettes que les utilisateurs peuvent sélectionner, utilisez la procédure suivante.

La prochaine fois que vous accéderez au panneau **Azure Information Protection**, l’option **Étiquettes** sera automatiquement sélectionnée pour vous permettre de voir et de configurer des étiquettes pour tous les utilisateurs. Vous pouvez revenir à la page **Démarrage rapide** en la sélectionnant à partir du menu **GÉNÉRAL**.

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Guide de configuration de la stratégie Azure Information Protection

1. Vérifiez que vous êtes connecté au portail Azure avec l’un de ces rôles d’administration : Administrateur Information Protection, Administrateur de sécurité ou Administrateur général. Consultez la [section précédente](#signing-in-to-the-azure-portal) pour plus d’informations sur ces rôles d’administration.

2. Si besoin, accédez au panneau **Azure Information Protection** : par exemple, dans le menu hub, cliquez sur **Tous les services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 
    
    Le panneau **Azure Information Protection - Étiquettes** s’ouvre automatiquement pour vous permettre d’afficher et de modifier les étiquettes disponibles. Vous pouvez mettre les étiquettes à la disposition de tous les utilisateurs, de certains utilisateurs ou d’aucun utilisateur en les ajoutant à une stratégie ou en les supprimant de celle-ci.

3. Pour afficher et modifier les stratégies, sélectionnez **Stratégies** parmi les options de menu. Pour afficher et modifier la stratégie que reçoivent tous les utilisateurs, sélectionnez la stratégie **Globale**. Pour créer une stratégie personnalisée pour certains utilisateurs, sélectionnez **Ajouter une nouvelle stratégie**.
    
    Une stratégie Azure Information Protection contient les éléments suivants que vous pouvez configurer :
    
    - Les étiquettes incluses permettant aux administrateurs et aux utilisateurs de classer les documents et les e-mails.
    
    - Le titre et l’info-bulle de la barre Information Protection, que les utilisateurs voient dans leurs applications Office.
    
    - L’option permettant de définir une étiquette par défaut comme point de départ de la classification de documents et d’e-mails.
     
    - L’option permettant d’appliquer la classification lorsque des utilisateurs enregistrent des documents et envoient des e-mails.
    
    - L’option invitant les utilisateurs à fournir une raison lorsqu’ils sélectionnent une étiquette qui a une sensibilité inférieure à l’étiquette originale.
    
    - L’option d’étiqueter automatiquement un e-mail en fonction de ses pièces jointes.

    - L’option permettant de contrôler si la barre Information Protection est affichée dans les applications Office.

    - L’option permettant de contrôler si le bouton Ne pas transférer s’affiche dans Outlook.
    
    - L’option permettant aux utilisateurs de spécifier leurs propres autorisations pour les documents.
    
    - L’option permettant de fournir un lien d’aide personnalisé aux utilisateurs.

Azure Information Protection est livré avec une [stratégie par défaut](configure-policy-default.md), qui contient cinq étiquettes principales. Deux de ces étiquettes contiennent des sous-étiquettes pour fournir des sous-catégories, si nécessaire. Quand une étiquette est configurée pour des sous-étiquettes, les utilisateurs ne peuvent pas sélectionner l’étiquette principale, mais doivent sélectionner une des sous-étiquettes.

Les étiquettes Azure Information Protection peuvent être utilisées avec la gamme complète des données généralement créées et stockées par une organisation, de la classification la plus basse des données personnelles à la classification la plus élevée des données hautement confidentielles. 

Vous pouvez utiliser les étiquettes par défaut sans les modifier, vous pouvez les personnaliser, ou encore les supprimer et créer de nouvelles étiquettes. Pour plus d’informations, utilisez les liens dans la section suivante pour vous aider à localiser les options appropriées et découvrir comment les configurer.

Vous pouvez créer autant d’étiquettes que vous le souhaitez. Cependant, quand il commence à y en avoir trop pour que les utilisateurs puissent voir et sélectionner facilement la bonne étiquette, créez des stratégies délimitées de façon que les utilisateurs voient seulement les étiquettes qui sont pertinentes pour eux. Il existe une limite supérieure pour les étiquettes qui appliquent la protection, qui est de 500.

Lorsque vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. Quand vous enregistrez des modifications dans une stratégie ou apportez des modifications à des étiquettes qui sont ajoutées à des stratégies, ces modifications sont automatiquement publiées. Il n’y a pas d’option de publication distincte.

Le client Azure Information Protection vérifie si des modifications ont été apportées au démarrage d’une application Office prise en charge et télécharge les modifications en tant que dernière stratégie Azure Information Protection. Autres déclencheurs qui actualisent la stratégie sur le client :

- Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier.

- Lorsque vous exécutez les [applets de commande PowerShell](../rms-client/client-admin-guide-powershell.md) pour l’étiquetage et la protection (Get-AIPFileStatus, Set-AIPFileClassification et Set-AIPFileLabel).

- Toutes les 24 heures.

- Pour le [scanneur Azure Information Protection](deploy-aip-scanner.md) : quand le service démarre (si la stratégie remonte à plus d’une heure) et toutes les heures pendant l’opération.


>[!NOTE]
>Quand le client télécharge la stratégie, attendez quelques minutes pour qu’elle soit entièrement opérationnelle. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration de la stratégie et la connectivité réseau. Si l’action résultante de vos étiquettes ne correspond pas à vos derniers changements, attendez 15 minutes au plus et réessayez.

### <a name="configuring-your-organizations-policy"></a>Configuration de la stratégie de votre organisation

Utilisez les informations suivantes pour configurer votre stratégie Azure Information Protection :

- [La stratégie Information Protection par défaut](configure-policy-default.md)

- [Guide pratique pour configurer les paramètres de stratégie](configure-policy-settings.md)

- [Comment créer une étiquette](configure-policy-new-label.md)

- [Guide pratique pour ajouter ou supprimer une étiquette](configure-policy-add-remove-label.md)
 
- [Comment supprimer ou réorganiser une étiquette](configure-policy-delete-reorder.md)

- [Comment modifier ou personnaliser une étiquette existante](configure-policy-change-label.md)

- [Comment configurer une étiquette pour la protection](configure-policy-protection.md)

- [Comment configurer une étiquette pour appliquer des marquages visuels](configure-policy-markings.md)

- [Comment configurer des conditions pour la classification automatique et recommandée](configure-policy-classification.md)

- [Guide pratique pour configurer la stratégie pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md)

- [Guide pratique pour configurer et gérer des modèles](configure-policy-templates.md)

- [Guide pratique pour configurer des étiquettes pour des langues différentes](configure-policy-languages.md)

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
