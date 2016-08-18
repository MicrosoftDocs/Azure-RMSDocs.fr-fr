---
title: "Didacticiel de démarrage rapide Azure Information Protection Étape 2 | Azure Rights Management"
description: "Étape 2 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en seulement quatre étapes et environ 10 minutes."
author: cabailey
manager: mbaldwin
ms.date: 07/291/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 128952778ec317584e558e409961e2921c4ecd07


---

# Étape 1 : activation du service Rights Management
 
>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

> [!NOTE]
>Si vous voulez uniquement classifier vos données (sans les protéger avec Azure Rights Management) ou si vous avez déjà activé Azure Rights Management pour votre client, passez directement à l’[étape suivante](infoprotect-tutorial-step2.md). 

Quand Azure Rights Management est activé, vous pouvez protéger vos documents et fichiers les plus sensibles une fois qu’ils ont été classés. Pour activer Azure Rights Management, vous pouvez utiliser le Centre d’administration Office 365 ou le portail Azure Classic :

-   Si vous avez un abonnement Office 365 qui inclut le service Azure Rights Management ou bien un abonnement Office 365 qui l’exclut, mais que vous disposez d’un abonnement pour Azure RMS Premium : **utilisez le Centre d’administration Office 365**.

-   Si vous n’avez pas d’abonnement Office 365 : **utilisez le portail Azure Classic**.

### Pour activer Rights Management à partir du Centre d’administration classique Office 365

> [!NOTE]
> Si vous utilisez la **préversion du Centre d’administration Office 365** plutôt que le Centre d’administration classique Office 365, vous pouvez utiliser les instructions indiquées dans [Comment activer Azure Rights Management à partir de la version préliminaire du centre d’administration Office 365](../deploy-use/activate-office365-preview.md), ou basculez vers la version classique pour utiliser ces instructions. Pour basculer, cliquez sur **Go to the old admin center** (Accéder à l’ancien Centre d’administration) dans la page **Accueil**, une fois que vous vous êtes connecté.

1.  Accédez au [portail Office 365](https://portal.office.com/) et connectez-vous avec votre compte d’administrateur général Office 365.

2.  Si le centre d’administration Office 365 ne s’affiche pas automatiquement, sélectionnez l’icône de lancement d’application en haut à gauche, puis choisissez **Administrer**. La vignette **Admin** s'affiche uniquement pour les administrateurs Office 365.

  > [!TIP]
  > Pour obtenir l'aide du centre d'administration, consultez [À propos du Centre d'administration Office 365 - Aide de l'administrateur](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  Dans le volet gauche, développez **PARAMÈTRES DE SERVICE**.

4.  Cliquez sur **Rights Management**.

5.  Sur la page **RIGHTS MANAGEMENT** , cliquez sur **Gérer**.

6.  Dans la page **Rights Management** , cliquez sur **Activer**.

7.  Lorsque l’invite **Voulez-vous activer Rights Management ?**apparaît, cliquez sur **activer**.

Vous devriez maintenant voir **Rights management est activé** , ainsi que l’option de désactivation (vous devrez peut-être actualiser la page manuellement).

À ce stade, ne cliquez pas sur **fonctionnalités avancées**. Vous seriez redirigé vers le portail Azure Classic permettant de configurer des modèles personnalisés qui sont superflus pour ce didacticiel. Choisissez plutôt de fermer le Centre d’administration Office 365.

### Pour activer Rights Management à partir du portail Azure Classic

1.  Accédez au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081) et connectez-vous avec votre compte d’administrateur général Azure Active Directory.

2.  Dans le volet gauche, cliquez sur **Active Directory**.

3.  Dans la page **Active Directory** , cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez l’annuaire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **ACTIVER**, puis confirmez votre action.

**Statut de Rights Management** doit désormais afficher l’état **Actif** et l’option **ACTIVER** est remplacée par **DÉSACTIVER**.

Bien que vous puissiez configurer d’autres options pour Rights Management dans le portail, celles-ci ne sont pas nécessaires pour ce didacticiel. Vous pouvez donc fermer le portail Azure Classic.

C’est tout ce que vous avez à faire pour cette première étape. Le service Azure Rights Management est activé pour que, plus loin dans ce didacticiel, vous puissiez sélectionner l’un des modèles Azure Rights Management par défaut pour protéger les documents et les messages électroniques classés comme confidentiels.

Pour un déploiement de production, vous souhaiterez probablement configurer des modèles personnalisés, en plus ou au lieu des deux modèles Azure Rights Management par défaut. Les modèles personnalisés n’étant pas nécessaires pour ce didacticiel, vous pouvez passer à l’Étape 2.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’activation de Rights Management|[Activation d'Azure Rights Management](../deploy-use/activate-service.md)|
|Modèles par défaut et création de modèles personnalisés|[Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; Introduction](infoprotect-quick-start-tutorial.md)
[Étape 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Jul16_HO5-->


