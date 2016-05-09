---
# required metadata

title: Didacticiel de démarrage rapide Azure RMS – étape 4 |Azure RMS
description: Quatrième étape d’un didacticiel vous permettant de tester rapidement Microsoft Azure Rights Management au sein de votre organisation en seulement 5 étapes qui devraient vous prendre moins de 15 minutes.
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c

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


# Démarrage rapide Azure RMS – étape 4 : demander aux destinataires d’ouvrir le document envoyé par e-mail

Atteindre : 
> [!div class="op_single_selector"]
- [Introduction](quick-start-tutorial.md)
- [Étape 1 : activer Azure RMS](tutorial-step1.md)
- [Étape 2 : installer l’application de partage RMS](tutorial-step2.md)
- [Étape 3 : envoyer le document confidentiel par e-mail](tutorial-step3.md)
- [Étape 4 : le destinataire lit le document](tutorial-step4.md)
- [Étape 5 : suivre votre document](tutorial-step5.md)


![](../media/AzRMS_QuickStartSteps4.PNG)

Vos destinataires peuvent utiliser de nombreux appareils pour lire le document protégé que vous avez envoyé en pièce jointe d’un courrier électronique. Les appareils incluent les iPad, les iPhone, les tablettes et les téléphones Android, les ordinateurs Mac, ainsi que les ordinateurs Windows.

Demandez-leur de lire le message électronique que vous leur avez envoyé. Avant de voir votre message électronique, ils verront le message suivant :

**L’expéditeur a protégé les pièces jointes avec Microsoft RMS. Vous devez vous **[connecter](http://aka.ms/rms)
      **pour les ouvrir.**

Lorsqu’ils cliquent sur le lien, ils sont redirigés vers les instructions pour installer l’application de partage RMS et pour se connecter à un compte gratuit, si nécessaire. Le compte gratuit leur accorde un abonnement à RMS for individuals, et garantit que les utilisateurs autorisés pourront toujours lire un document protégé, même si leur organisation ne dispose pas d’Azure RMS. Ils peuvent ensuite lire les pièces jointes protégées à l’aide des instructions suivantes.

![](../media/AzRMS_Tutorial_4_Screenshots.png)

### Affichage de la pièce jointe du document protégé

1.  Étant donné qu’Azure Rights Management a protégé un document Word, il existe deux pièces jointes au courrier électronique. Il s’agit en fait de deux versions du même fichier, mais avec différentes extensions. Ouvrez la version avec l’extension de nom de fichier **.ppdf** (**Confidential.ppdf**).

    Si vous disposez sur votre appareil d’une version d’[Office qui prend en charge Rights Management](https://technet.microsoft.com/library/dn655136.aspx), vous pouvez ouvrir l’autre version du fichier (**Confidential.docx**) pour qu’il s’ouvre dans Word.

2.  Si vous êtes invité à saisir votre nom d’utilisateur et votre mot de passe, indiquez votre nom d’utilisateur dans le même format que l’adresse de messagerie utilisée pour vous envoyer le courrier électronique et la pièce jointe. Par exemple, **janetm@contoso.com** ou **p.dover@fabrikam.com**. En ce qui concerne votre mot de passe, saisissez celui que vous avez fourni lors de votre inscription à RMS for individuals. Si votre organisation a Azure RMS, entrez votre mot de passe professionnel habituel.

Le document s’ouvre et vous pouvez maintenant lire le contenu. Par exemple, il peut contenir le message **Si vous pouvez lire ce texte à partir de la pièce jointe de votre e-mail, l’expéditeur a réussi à partager un fichier protégé par Azure RMS.** Étant donné que le document est en lecture seule, vous ne pouvez pas modifier son contenu.

Vous pouvez éventuellement demander à votre destinataire de transférer le courrier électronique à d’autres personnes que vous n’avez pas incluses dans votre courrier d’origine. Même si ces personnes travaillent pour une organisation qui dispose d’Azure Rights Management ou s’il demandent un abonnement à RMS for individuals, ils ne seront pas en mesure d’ouvrir la pièce jointe. Lorsqu’elles sont invitées à saisir leur nom d’utilisateur, l’accès au document leur est refusé.

Maintenant que le destinataire a ouvert la pièce jointe et l’a éventuellement transférée à une autre personne, attendez-vous à recevoir une notification par courrier électronique qui vous informe de cette activité. Toutefois, les courriers électroniques se perdent facilement au fil du temps. Afin d’assurer un meilleur suivi des personnes ayant accédé à votre document, utilisez le site de suivi de document (sujet traité dans la dernière étape de ce didacticiel).

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Instructions détaillées pour afficher les fichiers protégés par Azure Rights Management|[Afficher et utiliser des fichiers qui ont été protégés par Rights Management](../rms-client/sharing-app-view-use-files.md)|
|Abonnement gratuit RMS for individuals|[RMS for Individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|Deux versions du fichier joint à l’e-mail|[Qu'est-ce que le fichier .ppdf créé automatiquement ?](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created-)|


>[!div class="step-by-step"]
[« Étape 3](tutorial-step3.md)
[Étape 5 »](tutorial-step5.md)

<!--HONumber=Apr16_HO3-->


