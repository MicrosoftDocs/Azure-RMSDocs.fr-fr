---
# required metadata

title: Didacticiel de démarrage rapide Azure RMS – étape 2 |Azure RMS
description: Deuxième étape d’un didacticiel vous permettant de tester rapidement Microsoft Azure Rights Management au sein de votre organisation en seulement 5 étapes qui devraient vous prendre moins de 15 minutes.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: f32cf2f3-29e2-429c-a0fd-b16cc482484a

# optional metadata

ROBOTS: 
audience:
ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm:
ms.technology:
ms.custom:

---



# Démarrage rapide Azure RMS – étape 2 : installer l’application de partage Rights Management

Atteindre : 
> [!div class="op_single_selector"]
- [Introduction](quick-start-tutorial.md)
- [Étape 1 : activer Azure RMS](tutorial-step1.md)
- [Étape 2 : installer l’application de partage RMS](tutorial-step2.md)
- [Étape 3 : envoyer le document confidentiel par e-mail](tutorial-step3.md)
- [Étape 4 : le destinataire lit le document](tutorial-step4.md)
- [Étape 5 : suivre votre document](tutorial-step5.md)


![](../media/AzRMS_QuickStartSteps2.PNG)

L’application de partage Rights Management (également appelée « application de partage RMS ») n’est pas obligatoire pour Azure Rights Management, mais nous la recommandons pour tous les ordinateurs et appareils mobiles prenant en charge Azure Rights Management. L’application de partage RMS s’intègre aux applications Office via l’installation d’un complément Office, afin de permettre aux utilisateurs de protéger facilement des fichiers directement depuis le ruban. Elle permet également de protéger tout type de fichier en appliquant une protection générique pour les fichiers qui ne sont pas pris en charge en mode natif par Azure Rights Management, et propose un site de suivi de document pour suivre et révoquer les fichiers sous protection. Nous utiliserons le site de suivi de document plus loin dans ce didacticiel.

Cette application peut être téléchargée gratuitement et propose une installation par script pour les environnements de production. Dans le cadre de ce didacticiel, nous allons l’installer localement.

![](../media/AzRMS_Tutorial_2_Screenshots.png)

### Pour télécharger et installer l’application de partage Rights Management

1.  Accédez à la page [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) sur le site web Microsoft.

2.  Dans la section **Ordinateurs** , cliquez sur l’icône de l’ **application RMS pour Windows** et enregistrez le fichier **Setup.exe** pour installer l’application de partage Microsoft Rights Management.

3.  Pour une installation locale, vous devez utiliser un compte d’administrateur pour exécuter le fichier Setup.exe qui a été téléchargé. Si vous êtes invité à continuer, cliquez sur **Oui**.

4.  Dans la page **Installer Microsoft RMS** , cliquez sur **Suivant**, puis attendez que l’installation se termine.

5.  Une fois l’installation terminée, cliquez sur **Redémarrer** si vous êtes invité à redémarrer votre ordinateur, ou sur  **Fermer** pour terminer l’installation.

Vous êtes maintenant prêt à protéger les fichiers contenant des informations que vous souhaitez partager, mais uniquement avec les personnes que vous indiquez.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Installation locale de l’application de partage Rights Management pour Windows et instructions utilisateur|[Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md)|
|Installation par script de l’application de partage Rights Management pour Windows et informations techniques|[guide de l'administrateur de l'application de partage Rights Management](../rms-client/sharing-app-admin-guide.md)|
|Pour comprendre la différence entre la protection native et la protection générique|[Quelle est la différence entre la protection générique et la protection intégrée (native) ?](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection-)|


>[!div class="step-by-step"]
[« Étape 1](quick-start-tutorial.md)
[Étape 3 »](tutorial-step3.md)

<!--HONumber=Apr16_HO3-->


