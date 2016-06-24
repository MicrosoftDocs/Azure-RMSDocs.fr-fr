---
# required metadata

title: Didacticiel de démarrage rapide Azure RMS – étape 1 |Azure RMS
description: Première étape d’un didacticiel vous permettant de tester rapidement Microsoft Azure Rights Management au sein de votre organisation en seulement 5 étapes qui devraient vous prendre moins de 15 minutes.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Démarrage rapide Azure RMS – étape 1 : activer le service Rights Management

*S’applique à : Azure Rights Management, Office 365*


Atteindre : 
> [!div class="op_single_selector"]
- [Introduction](quick-start-tutorial.md)
- [Étape 1 : activer Azure RMS](tutorial-step1.md)
- [Étape 2 : Installer l’application de partage RMS](tutorial-step2.md)
- [Étape 3 : envoyer le document confidentiel par e-mail](tutorial-step3.md)
- [Étape 4 : Le destinataire lit le document](tutorial-step4.md)
- [Étape 5 : Suivre votre document](tutorial-step5.md)


![Didacticiel de démarrage rapide Azure RMS étape 1](../media/AzRMS_QuickStartSteps1.PNG)

Même si vous avez un abonnement prenant en charge Azure Rights Management, le service est désactivé par défaut. Pour l’activer, vous pouvez utiliser le Centre d’administration Office 365 ou le portail Azure Classic :

-   Si vous avez un abonnement Office 365 qui inclut le service Azure Rights Management ou bien un abonnement Office 365 qui l’exclut, mais que vous disposez d’un abonnement pour Azure RMS Premium : **utilisez le Centre d’administration Office 365**.

-   Si vous n’avez pas d’abonnement Office 365 : **utilisez le portail Azure Classic**.

![Captures d’écran de l’étape 1 du didacticiel](../media/AzRMS_Tutorial_1_Screenshots.png)

### Pour activer Rights Management à partir du Centre d’administration classique Office 365

1.  Accédez au [portail Office 365](https://portal.office.com/) et connectez-vous avec votre compte professionnel ou scolaire.

2.  Si le Centre d’administration Office 365 ne s’affiche pas automatiquement, sélectionnez l’icône de lancement d’application dans l’angle supérieur gauche, puis choisissez **Admin**. La vignette **Admin** s'affiche uniquement pour les administrateurs Office 365.

    > [!TIP]
    > Pour obtenir l’aide du centre d’administration, consultez [À propos du Centre d’administration Office 365 - Aide de l’administrateur](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547).

3.  Dans le volet gauche, développez **PARAMÈTRES DE SERVICE**.

4.  Cliquez sur **Rights Management**.

5.  Dans la page **RIGHTS MANAGEMENT**, cliquez sur **Gérer**.

6.  Dans la page **Rights Management**, cliquez sur **Activer**.

7.  Quand l’invite **Voulez-vous activer Rights Management ?** apparaît, cliquez sur **activer**.

Vous devriez maintenant voir **Rights management est activé** , ainsi que l’option de désactivation (vous devrez peut-être actualiser la page manuellement).

À ce stade, ne cliquez pas sur **fonctionnalités avancées**. Vous seriez redirigé vers le portail Azure Classic permettant de configurer des modèles qui sont superflus pour ce didacticiel. Choisissez plutôt de fermer le Centre d’administration Office 365.

### Pour activer Rights Management à partir du portail Azure Classic

1.  Accédez au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081), puis connectez-vous.

2.  Dans le volet gauche, cliquez sur **ACTIVE DIRECTORY**.

3.  Dans la page **active directory**, cliquez sur **RIGHTS MANAGEMENT**.

4.  Sélectionnez l’annuaire à gérer pour [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], cliquez sur **ACTIVER**, puis confirmez.

**Statut de Rights Management** doit désormais afficher l’état **Actif** et l’option **ACTIVER** est remplacée par **DÉSACTIVER**.

Bien que vous puissiez configurer d’autres options pour Rights Management dans le portail, celles-ci ne sont pas nécessaires pour ce didacticiel. Vous pouvez donc fermer le portail Azure Classic.

C’est tout ce que vous avez à faire pour cette première étape. Le service est activé : tous les utilisateurs de votre organisation peuvent maintenant commencer à protéger des documents importants et sensibles. Dans un environnement de production, vous souhaiterez peut-être limiter les personnes pouvant le faire au début, afin d’assurer un déploiement échelonné. Toutefois, ce n’est pas nécessaire pour ce didacticiel.

Bien que ce ne soit pas inclus dans cette rubrique, pour un déploiement de production, vous souhaiterez probablement configurer des modèles personnalisés. Les modèles facilitent l’application rapide des paramètres corrects lorsque les utilisateurs doivent protéger des fichiers. Lorsque vous activez Rights Management, vous obtenez automatiquement deux modèles par défaut que vous souhaiterez probablement compléter avec vos modèles personnalisés dans un environnement de production. Cependant, les modèles ne sont pas nécessaires pour ce didacticiel, vous pouvez donc passer à l’étape suivante.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Activation de Rights Management et contrôle des personnes pouvant protéger des fichiers et des e-mails quand le service est activé|[Activation d'Azure Rights Management](../deploy-use/activate-service.md)|
|Modèles par défaut et création de modèles personnalisés|[Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« Introduction](quick-start-tutorial.md)
[Étape 2 »](tutorial-step2.md)

<!--HONumber=Apr16_HO4-->


