---
title: "Forum aux questions sur l’application Azure Information Protection pour iOS et Android | Azure Information Protection"
description: 
keywords: "Quelques questions fréquemment posées pour vous aider à utiliser l’application Azure Information Protection pour iOS et Android"
author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2f1930f4657278d25ef6dd369866f16e4ba71644
ms.openlocfilehash: 1cafa88ded2bf951f8af93e4b27cc526735d19e8


---

# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>Forum aux questions sur l’application Microsoft Azure Information Protection pour iOS et Android

*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection*

Cette page fournit des réponses aux questions les plus fréquemment posées sur l’application Azure Information Protection pour iOS et Android.

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Que puis-je faire avec l’application Azure Information Protection ?

Cette application vous permet d’afficher des e-mails protégés par des droits (fichiers .rpmsg) si votre application de messagerie ne prend pas en charge la protection des données Rights Management. Cette application vous permet également d’afficher les fichiers PDF, les images et les fichiers texte protégés par des droits. Actuellement, vous ne pouvez pas utiliser cette application pour créer des e-mails protégés, y répondre, ou créer ou modifier des fichiers protégés.

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>Puis-je ouvrir des fichiers PDF qui se trouvent dans des bibliothèques protégées SharePoint et dans OneDrive Entreprise ?

Oui, vous pouvez ouvrir des fichiers PDF protégés que d’autres ont partagés avec vous par l’intermédiaire de SharePoint et de OneDrive Entreprise. Appuyez sur le lien, puis choisissez cette application pour ouvrir automatiquement le fichier. 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>Comment commencer à utiliser l’application de visionneuse ?

Sur votre appareil mobile, vous devez accéder à l’un des fichiers que l’application prend en charge pour voir la visionneuse en action. Exemple :

- **Un fichier .rpmsg** : il s’agit d’un e-mail protégé par des droits qui s’affiche comme pièce jointe dans un e-mail lorsque votre application de messagerie sur votre appareil mobile ne prend pas en charge la protection des données Rights Management de manière native. 
    
    Utilisez un autre appareil pour vous envoyer un e-mail protégé par des droits auquel vous pouvez accéder à partir de votre appareil mobile. Par exemple, utilisez Outlook à partir d’un ordinateur Windows. Pour obtenir la liste des clients de messagerie prenant en charge la gestion des droits de manière native, consultez la colonne Adresse de messagerie dans [Applications prenant en charge la protection des données Azure Rights Management](../get-started/requirements-applications.md).

- **Un fichier PDF protégé par des droits** : utilisez l’application de partage Rights Management à partir d’un ordinateur Windows ou une application PDF prenant en charge la gestion des droits de manière native pour vous envoyer un fichier PDF protégé par des droits comme pièce jointe dans un e-mail. Vous pouvez également télécharger un fichier PDF dans une bibliothèque protégée SharePoint, puis la partager en utilisant votre adresse e-mail.

- **Un fichier .ptxt, .pjpg ou .ppng** : Utilisez l’application de partage Rights Management sur un ordinateur Windows et l’option [Partage protégé](sharing-app-protect-by-email.md) pour vous envoyer un fichier protégé comme pièce jointe d’e-mail. Pour obtenir la liste complète des types de fichiers que vous pouvez utiliser pour le test, consultez le premier tableau de la section [Types de fichier pris en charge et extensions de nom de fichier](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) dans le Guide de l'administrateur de l'application de partage Rights Management. 

Pour afficher ces fichiers dans l’application de visionneuse Azure Information Protection, cliquez sur la pièce jointe ou le lien dans l’e-mail. Lorsque vous êtes invité à sélectionner une application avez laquelle les ouvrir, sélectionnez l’application **Visionneuse d’accès et de protection des informations**. Vous êtes ensuite invité à vous connecter avec votre compte professionnel ou scolaire. Une fois que vous êtes correctement authentifié, l’application Azure Information Protection affiche l’e-mail ou le fichier pour vous permettre de les lire.

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>Quelles informations d’identification utiliser pour se connecter à cette application ?

Si votre organisation dispose déjà d’AD RMS en local (avec l’extension Appareils mobiles) ou utilise le service Azure Rights Management, vous pouvez utiliser vos informations d’identification pour vous connecter. Dans le cas contraire, vous pouvez vous inscrire pour obtenir un nouveau compte gratuit à l’aide de la [page Azure Information Protection](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload).

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>Puis-je m’inscrire au compte gratuit avec mon adresse e-mail personnelle, comme un compte Hotmail ou Gmail ?

Pas encore. Aujourd’hui, vous pouvez vous inscrire uniquement avec votre adresse e-mail professionnelle (compte professionnel ou scolaire). Nous travaillons à la prise en charge des adresses e-mail personnelles et mettrons à jour cette entrée quand elle sera disponible.

## <a name="which-file-extensions-can-i-open-with-this-app"></a>Quelles extensions de fichier puis-je ouvrir avec cette application ?

Vous pouvez ouvrir les fichiers .rpmsg, .pdf, .ppdf, .pjpg, .ptxt et plusieurs autres formats de fichiers texte et images.

##  <a name="how-do-i-provide-feedback-about-this-app"></a>Comment envoyer des commentaires concernant cette application ?

Dans l’application, accédez à **Paramètres** > **Envoyer des commentaires**.


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>Aucune réponse n’a été apportée à ma question. Que dois-je faire ?

Publiez votre question sur notre [site Yammer](http://www.yammer.com/AskIPTeam), ou [envoyez un e-mail à l’équipe Information Protection](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app).



<!--HONumber=Nov16_HO1-->


