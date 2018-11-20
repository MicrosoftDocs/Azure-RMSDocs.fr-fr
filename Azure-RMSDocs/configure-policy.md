---
title: Configurer la stratégie Azure Information Protection
description: Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/13/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9813f71535de9058c2cb3382ae590ba5f8102fd1
ms.sourcegitcommit: ad37950f6a747c86f6496c6de859e18446f9b03f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51644792"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Configuration de la stratégie Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Pour configurer la classification, l’étiquetage et la protection, vous devez configurer la stratégie Azure Information Protection. Cette stratégie est ensuite téléchargée sur les ordinateurs sur lesquels est installé le [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

La stratégie contient des paramètres et des étiquettes :

- Les étiquettes appliquent une valeur de classification aux documents et aux e-mails et peuvent éventuellement protéger ce contenu. Le client Azure Information Protection affiche ces étiquettes pour vos utilisateurs dans les applications Office et quand les utilisateurs cliquent avec le bouton droit à partir de l’Explorateur de fichiers. Ces étiquettes peuvent également être appliquées à l’aide de PowerShell et le scanneur Azure Information Protection.

- Les paramètres changent le comportement par défaut du client Azure Information Protection. Par exemple, vous pouvez sélectionner une étiquette par défaut si tous les documents et les e-mails doivent avoir une étiquette, et si la barre Azure Information Protection est affichée dans les applications Office.

## <a name="subscription-support"></a>Support d'abonnement

Azure Information Protection prend en charge différents niveaux d’abonnement :

- Azure Information Protection P2 : Prise en charge de toutes les fonctionnalités de classification, d’étiquetage et de protection.

- Azure Information Protection P1 : Prise en charge de la plupart des fonctionnalités de classification, d’étiquetage et de protection, mais pas la classification automatique ou le HYOK.

- Office 365 incluant le service Azure Rights Management : prise en charge de la protection, mais pas de la classification et de l’étiquetage.

Les options qui nécessitent un abonnement Azure Information Protection P2 sont identifiées dans le portail.

Si votre organisation a différents types d’abonnements, vous êtes responsable de vous assurer que les utilisateurs n’utilisent pas de fonctionnalités que la licence de leur compte ne les autorise pas à utiliser. Le client Azure Information Protection ne procède pas à la vérification et l’application de la licence. Lorsque vous configurez des options pour lesquelles certains utilisateurs n’ont pas de licence, utilisez les stratégies délimitées ou un paramètre du Registre pour vérifier que votre organisation est toujours en conformité avec vos licences :

- **Si votre organisation possède une combinaison de licences Azure Information Protection P1 et Azure Information Protection P2** : pour les utilisateurs qui ont une licence P2, créez et utilisez une ou plusieurs [stratégies délimitées](configure-policy-scope.md) lorsque vous configurez des options qui nécessitent une licence Azure Information Protection P2. Assurez-vous que votre stratégie globale ne contient pas d’options qui nécessitent une licence Azure Information Protection P2.

- **Si votre organisation a un abonnement à Azure Information Protection, mais que certains utilisateurs possèdent uniquement une licence pour Office 365 qui inclut le service Azure Rights Management** : pour les utilisateurs qui n’ont pas de licence pour Azure Information Protection, modifiez le Registre sur leurs ordinateurs pour qu’ils ne téléchargent pas la stratégie Azure Information Protection. Pour obtenir des instructions, consultez le guide d’administration pour la personnalisation suivante : [Appliquer le mode Protection uniquement si votre organisation possède différents types de licences](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses).

Pour plus d’informations sur les abonnements, consultez [De quel abonnement ai-je besoin pour Azure Information Protection et quelles sont les fonctionnalités incluses ?](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)

## <a name="signing-in-to-the-azure-portal"></a>Connexion au portail Azure

Pour vous connecter au portail Azure et configurer et gérer Azure Information Protection :

- Utilisez le lien suivant : https://portal.azure.com

- Utilisez un compte avec l’un des [rôles d’administrateur](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants :
    
    - **Administrateur Information Protection**

    - **Administrateur de sécurité**

    - **Administrateur général/administrateur de la société**
    
    > [!NOTE] 
    > Si votre locataire a été migré vers le magasin d’étiquetage unifié, pour gérer les étiquettes à partir du portail Azure, votre compte doit également être autorisé à accéder au Centre de sécurité et de conformité Office 365. [Plus d’informations](configure-policy-migrate-labels.md#important-information-about-administrative-roles)

## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>Pour accéder au panneau Azure Information Protection pour la première fois

1. Connectez-vous au portail Azure.

2. Dans le menu hub, sélectionnez **Créer une ressource**, puis, à partir de la zone de recherche pour la Place de marché, tapez **Azure Information Protection**. 
    
3. Dans la liste des résultats, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.
    
    > [!TIP] 
    > Ou sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.
    
    Cliquez sur **Créer** à nouveau.

4. Vous voyez la page **Démarrage rapide** qui s’ouvre automatiquement la première fois que vous vous connectez au service. Parcourez les ressources suggérées ou utilisez les autres options de menu. Pour configurer les étiquettes que les utilisateurs peuvent sélectionner, utilisez la procédure suivante.

La prochaine fois que vous accéderez au panneau **Azure Information Protection**, l’option **Étiquettes** sera automatiquement sélectionnée pour vous permettre de voir et de configurer des étiquettes pour tous les utilisateurs. Vous pouvez revenir à la page **Démarrage rapide** en la sélectionnant à partir du menu **Général**.

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Guide de configuration de la stratégie Azure Information Protection

1. Vérifiez que vous êtes connecté au portail Azure avec l’un de ces rôles d’administration : Administrateur Information Protection, Administrateur de sécurité ou Administrateur général. Consultez la [section précédente](#signing-in-to-the-azure-portal) pour plus d’informations sur ces rôles d’administration.

2. Si besoin, accédez au panneau **Azure Information Protection** : par exemple, dans le menu hub, cliquez sur **Tous les services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 
    
    Le panneau **Azure Information Protection - Étiquettes** s’ouvre automatiquement pour vous permettre d’afficher et de modifier les étiquettes disponibles. Vous pouvez mettre les étiquettes à la disposition de tous les utilisateurs, de certains utilisateurs ou d’aucun utilisateur en les ajoutant à une stratégie ou en les supprimant de celle-ci.

3. Pour afficher et modifier les stratégies, sélectionnez **Stratégies** parmi les options de menu. Pour afficher et modifier la stratégie que reçoivent tous les utilisateurs, sélectionnez la stratégie **Globale**. Pour créer une stratégie personnalisée pour certains utilisateurs, sélectionnez **Ajouter une nouvelle stratégie**.
    

### <a name="making-changes-to-the-policy"></a>Apporter des modifications à la stratégie

Vous pouvez créer autant d’étiquettes que vous le souhaitez. Cependant, quand il commence à y en avoir trop pour que les utilisateurs puissent voir et sélectionner facilement la bonne étiquette, créez des stratégies délimitées de façon que les utilisateurs voient seulement les étiquettes qui sont pertinentes pour eux. Il existe une limite supérieure pour les étiquettes qui appliquent la protection, qui est de 500.

Lorsque vous apportez des modifications dans un panneau Azure Information Protection, cliquez sur **Enregistrer** pour enregistrer les modifications, ou cliquez sur **Ignorer** pour rétablir les derniers paramètres enregistrés. Quand vous enregistrez des modifications dans une stratégie ou apportez des modifications à des étiquettes qui sont ajoutées à des stratégies, ces modifications sont automatiquement publiées. Il n’y a pas d’option de publication distincte.

Le client Azure Information Protection vérifie si des modifications ont été apportées au démarrage d’une application Office prise en charge et télécharge les modifications en tant que dernière stratégie Azure Information Protection. Autres déclencheurs qui actualisent la stratégie sur le client :

- Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier.

- Lorsque vous exécutez les [applets de commande PowerShell](./rms-client/client-admin-guide-powershell.md) pour l’étiquetage et la protection (Get-AIPFileStatus, Set-AIPFileClassification et Set-AIPFileLabel).

- Toutes les 24 heures.

- Pour le [scanneur Azure Information Protection](deploy-aip-scanner.md) : quand le service démarre (si la stratégie remonte à plus d’une heure) et toutes les heures pendant l’opération.


>[!NOTE]
>Quand le client télécharge la stratégie, attendez quelques minutes pour qu’elle soit entièrement opérationnelle. La durée varie en fonction de différents facteurs comme la taille et la complexité de la configuration de la stratégie et la connectivité réseau. Si l’action résultante de vos étiquettes ne correspond pas à vos derniers changements, attendez 15 minutes au plus et réessayez.

### <a name="configuring-your-organizations-policy"></a>Configuration de la stratégie de votre organisation

Utilisez les informations suivantes pour configurer la stratégie Azure Information Protection :

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

- [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](configure-policy-migrate-labels.md)

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des exemples montrant comment personnaliser la stratégie Azure Information Protection et voir le comportement qui en résulte pour les utilisateurs, suivez les didacticiels ci-dessous :

- [Modifier la stratégie Azure Information Protection et créer une nouvelle étiquette](infoprotect-quick-start-tutorial.md)

- [Configurer les paramètres de stratégie Azure Information Protection qui interagissent](infoprotect-settings-tutorial.md)

Pour voir comment votre stratégie s’exécute, consultez [Création de rapports pour Azure Information Protection](reports-aip.md).

