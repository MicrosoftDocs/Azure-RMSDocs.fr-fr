---
title: "Étape 5 du didacticiel de démarrage rapide | Azure Information Protection"
description: "Étape 5 d’un didacticiel de prise en main vous permettant de tester rapidement Microsoft Azure Information Protection dans votre organisation en environ 30 minutes."
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4e59a3b3-f0f4-4535-8b96-cac68303d855
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1af9f3b3451bf8ceafbaf3cddd2b26c37fe9d597
ms.openlocfilehash: d607c19d37da6b6fb23513067e9e30f33f0260de


---


# Étape 5 : Voir le partage de fichiers protégés en action et effectuer le suivi de votre document 

>*S’applique à : Azure Information Protection*

Pour cette étape finale du didacticiel, recherchez un document Word que vous avez déjà créé et que vous allez envoyer à un partenaire ou à un collègue. Dans le cadre de ce didacticiel, faites en sorte que le document contienne du texte, quel qu’il soit, afin de pouvoir confirmer plus facilement que le destinataire autorisé a pu le lire.

Ensuite, vous pouvez partager en toute sécurité ce document par courrier électronique. 

## Partage en toute sécurité d’un document par courrier électronique

1.  Dans Word, ouvrez votre document. Vous verrez que l’étiquette par défaut **Interne** est automatiquement réappliquée. 

2.  Sous l’onglet **Accueil** du groupe **RMS**, cliquez sur **Partage protégé**, puis cliquez sur **Partage protégé** dans le menu :

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 5 : Partage protégé](../media/share-protected-callout.png)

    Vous verrez la boîte de dialogue **partage protégé**, similaire à cette image :

    ![Didacticiel de démarrage rapide Azure Information Protection Étape 5 : Boîte de dialogue partage protégé](../media/example-share-protected-dialog.png)

3. Dans la zone **UTILISATEURS**, tapez une ou plusieurs adresses e-mail professionnelles, comme quand vous envoyez un document à une personne avec laquelle votre organisation entretient des relations commerciales. Ou bien, vous pouvez spécifier l’adresse e-mail d’un collègue. Veillez à indiquer une adresse e-mail professionnelle, comme **janetm@contoso.com** ou **p.dover@fabrikam.com**, car Azure Information Protection ne prend pas en charge les adresses e-mail personnelles. 

    Le fait de savoir si le destinataire possède également Azure Information Protection n’est pas important.

4. Sélectionnez **Visionneuse – Affichage uniquement**.

    Cela signifie que les destinataires seront en mesure d’afficher le document, mais pas de le modifier ou de l’imprimer.

5. Sélectionnez **M’avertir par message électronique lorsque quelqu’un essaie d’ouvrir ces documents**.

    Vous recevrez une notification par courrier électronique chaque fois que les destinataires ou d’autres personnes tenteront d’ouvrir la pièce jointe, par exemple, si votre destinataire transfère le courrier à un collègue. Si le document est transféré, vous verrez que l’accès a été refusé, et dans les détails de l’utilisateur, vous pouvez décider d’envoyer à cette personne une copie du document qu’elle peut ouvrir.

6. Sélectionnez **M’autoriser à révoquer de suite l’accès à ces documents**.

    Cette option nécessite que les destinataires disposent d’une connexion Internet chaque fois qu’ils ouvrent la pièce jointe, mais le point positif réside dans le fait que si vous révoquez ultérieurement le document, ils ne seront pas en mesure de l’ouvrir lors de leur prochaine tentative d’ouverture. 

4.  Cliquez sur **Envoyer** pour afficher un e-mail prêt à être envoyé aux destinataires que vous avez spécifiés et contenant un texte par défaut pour les instructions. Exemple :

    ![Exemple d’e-mail dans le cadre d’un partage protégé](../media/example-email-share-protected.png)
    
    **REMARQUE** : Si Outlook était ouvert quand vous avez installé le client Azure Information Protection, la barre Information Protection illustrée dans l’image précédente n’apparaît pas : comme elle n’est pas spécifiquement utilisée dans cette étape qui illustre le partage de documents protégés, vous n’avez pas besoin de fermer et rouvrir Outlook pour suivre ce didacticiel. Si vous avez ouvert Outlook après avoir installé le client Azure Information Protection, cet e-mail, comme notre document Word à sa première ouverture, se voit appliquer l’étiquette **Interne** par défaut, car ce paramètre global est configuré dans la stratégie Azure Information Protection.
    
    Vous remarquerez peut-être que vous avez deux pièces jointes ; le document Word d’origine et un fichier qui porte le même nom, mais **.ppdf** en guise d’extension de nom de fichier. La version .ppdf est un fichier PDF protégé qui est automatiquement créé par l’application de partage Rights Management, au cas où le destinataire n’aurait pas une version d’Office qui prend en charge les documents protégés. Ce fichier supplémentaire permet au destinataire de lire le document protégé à l’aide de la visionneuse qui est installée avec l’application de partage Rights Management.

    Cliquez sur **Envoyer** dans votre e-mail.

Maintenant que vous avez envoyé votre document protégé, vous pouvez demander à vos destinataires de l’ouvrir dès qu’ils le reçoivent. Ne fermez pas Word, car nous allons le réutiliser au cours de la procédure finale pour suivre le document partagé.

## demande au destinataires d’ouvrir le document envoyé par courrier électronique

Vos destinataires peuvent utiliser de nombreux appareils pour lire le document protégé que vous avez envoyé en pièce jointe d’un courrier électronique. Les appareils incluent les iPad, les iPhone, les tablettes et les téléphones Android, les ordinateurs Mac, ainsi que les ordinateurs Windows.

Demandez-leur de lire le message électronique que vous leur avez envoyé. En supposant que c’est la première fois qu’ils ont reçu des pièces jointes protégées par Rights Management, demandez-leur de cliquer sur le lien des instructions. Ils voient alors la page [Bienvenue dans Microsoft RMS !](https://portal.azurerms.com/#/rmshelp), qui contient des instructions pour installer l’application de partage RMS et pour se connecter à un compte gratuit, si nécessaire. Ils sont ensuite prêts à lire la pièce jointe protégée.

### Instructions pour le destinataire : affichage de la pièce jointe du document protégé

1. Ouvrez une des pièces jointes pour lire le document :
    
    - Si vous disposez sur votre appareil d’une version d’Office qui prend en charge Rights Management :
    
        -  Ouvrez le document qui porte l’extension de nom de fichier **.docx**.
        
    - Si vous ne disposez pas d’une version d’Office qui prend en charge Rights Management, que vous n’en êtes pas sûr ou que vous souhaitez simplement essayer la visionneuse à partir de l’application de partage Rights Management : 
    
        - Ouvrez le document qui porte l’extension de nom de fichier **.ppdf**.

2.  Si vous êtes invité à saisir votre nom d’utilisateur et votre mot de passe, indiquez votre nom d’utilisateur dans le même format que l’adresse de messagerie utilisée pour vous envoyer le courrier électronique et la pièce jointe. Par exemple, **janetm@contoso.com** ou **p.dover@fabrikam.com**. En ce qui concerne votre mot de passe, saisissez celui que vous avez fourni lors de votre inscription à RMS for individuals. Ou, si votre organisation dispose d’un service cloud tel qu’Office 365 ou qu’elle utilise Azure, entrez votre mot de passe de travail habituel.

3. Lisez le contenu du document quand il s’ouvre. Étant donné que le document est en lecture seule, vous ne pouvez pas modifier son contenu.

Votre destinataire peut éventuellement transférer l’e-mail à d’autres personnes que vous n’avez pas spécifiées dans votre e-mail d’origine. Ces personnes ne pourront pas ouvrir la pièce jointe. Lorsqu’elles sont invitées à saisir leur nom d’utilisateur, l’accès au document leur est refusé.

Maintenant que le destinataire a ouvert la pièce jointe et l’a éventuellement transférée à une autre personne, attendez-vous à recevoir une notification par courrier électronique qui vous informe de cette activité. Toutefois, les e-mails se perdent facilement au fil du temps. Afin d’assurer un meilleur suivi des personnes ayant accédé à votre document, utilisez le site de suivi de document (sujet traité dans la dernière procédure).

## Suivi du document protégé

1.  De retour dans Word, sous l’onglet **Accueil**, dans le groupe **RMS**, cliquez sur **Partage protégé**, puis sur **Suivre l’utilisation** dans le menu :

    ![Option Suivre l’utilisation](../media/track-usage-callout.png)

    Vous accédez ainsi au site de suivi de document.

2.  Si la page **Protégez et partagez comme vous le souhaitez** apparaît, cliquez sur **Se connecter** et indiquez à nouveau votre nom d’utilisateur et votre mot de passe.

3.  Dans la page **Vos documents partagés** apparaît le nom du document que vous avez partagé. À ce stade, il s’agit du seul fichier affiché, mais la liste s’allongera à mesure que vous partagerez des fichiers.

    Sur cette page, vous pouvez voir le moment où vous avez partagé le document (moment de l’envoi du courrier électronique contenant la pièce jointe protégée), la date de la dernière activité et le nom du destinataire auquel vous avez envoyé le courrier. Cliquez sur le nom du document pour plus de détails.

4.  Sur la nouvelle page qui porte le nom du fichier sur lequel vous avez cliqué, vous pouvez voir les détails du résumé de ce document, ainsi qu’une liste d’autres options disponibles pour le document (**Liste**, **Chronologie**, **Carte**, **Paramètres**).

    Cliquez sur chaque option pour explorer les différentes façons de suivre votre document protégé. Sinon, sur la page **Résumé** , cliquez sur **Ouvrir dans Excel** pour exporter les informations dans une feuille de calcul, ou cliquez sur **Révoquer l’accès** pour cesser de partager le document.

Vous pouvez revenir sur ce site pour suivre les autres activités de votre document protégé ou révoquer son accès si nécessaire. Vous pouvez même accéder au site à partir de votre appareil mobile ou de votre tablette, à l’aide d’un navigateur et du lien suivant : [suivi de document](http://go.microsoft.com/fwlink/?LinkId=529562)



|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|Instructions détaillées et méthodes alternatives pour protéger des fichiers que vous partagez par e-mail|[Protégez un fichier partagé par courrier électronique à l’aide de l’application de partage Rights Management](../rms-client/sharing-app-protect-by-email.md)|
|Options de la boîte de dialogue **partage protégé**|[Options de boîte de dialogue pour l'application de partage Rights Management](../rms-client/sharing-app-dialog-box.md)|
|À propos du compte gratuit pour l’inscription d’autres utilisateurs|[RMS for individuals et Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|À propos de l’utilisation du site de suivi de document|[Suivre et révoquer vos documents](../rms-client/sharing-app-track-revoke.md)


## Étapes suivantes

Maintenant que vous avez vu comment personnaliser la stratégie Azure Information Protection par défaut et comment fonctionne l’étiquetage d’un document Word, essayez d’appliquer certains autres paramètres pour voir comment ils fonctionnent dans les autres applications Office qui prennent en charge Azure Information Protection : Excel, PowerPoint et Outlook. Si ces applications étaient ouvertes quand vous avez installé le client Azure Information Protection, fermez et rouvrez-les avant d’essayer de les utiliser avec Azure Information Protection.

Essayez de partager davantage de documents, suivez leur utilisation et vérifiez le fonctionnement de la révocation des documents.

Vous pouvez ensuite juger utile de consulter certains [forums aux questions](faqs.md) sur Azure Information Protection et de lire d’autres articles de la documentation. Mais si vous êtes prêt à déployer Azure Information Protection pour votre organisation, vous pouvez passer directement à la [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md). 


<!--HONumber=Sep16_HO4-->


