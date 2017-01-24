---
title: "Guide d’utilisation de l’application de partage Rights Management | Azure Information Protection"
description: "L’application de partage Microsoft Rights Management (RMS) pour Windows vous aide à protéger vos images et documents importants afin qu’ils ne soient pas accessibles aux personnes non autorisées, même lorsque vous les envoyez par courrier électronique ou que vous les enregistrez sur un autre appareil."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 8acc80758eb27cfbe537b705342220418c22fa96


---

# <a name="rights-management-sharing-application-user-guide"></a>Guide d’utilisation de l’application de partage Rights Management

>*S’applique à : Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

L’application de partage Microsoft Rights Management (RMS) pour Windows vous aide à protéger vos images et documents importants afin qu’ils ne soient pas accessibles aux personnes non autorisées, même lorsque vous les envoyez par courrier électronique et que vous les enregistrez sur un autre appareil. Vous pouvez également utiliser cette application pour ouvrir et utiliser des fichiers protégés par d’autres personnes à l’aide de la même technologie de protection Rights Management.

Tout ce dont vous avez besoin, c’est d’un ordinateur exécutant au moins Windows 7 avec Service Pack 1. Ensuite, [téléchargez et installez](http://go.microsoft.com/fwlink/?LinkId=303970) cette application gratuite de Microsoft.

Si vous avez des questions auxquelles ce guide ne répond pas, voir le [Forum Aux Questions relatif à l’application de partage Rights Management pour Windows](http://go.microsoft.com/fwlink/?LinkId=303971). Cette page contient également des informations de dépannage, si vous rencontrez des problèmes.

## <a name="examples-for-using-the-rms-sharing-application"></a>Exemples d’utilisation de l’application de partage RMS
Voici quelques exemples d’utilisation de l’application de partage RMS pour protéger vos fichiers.

|Je veux...|Procédure|
|----------------|------------------|
|**... partager en toute sécurité des informations financières avec quelqu’un de confiance qui travaille pour une autre organisation**<br /><br />Vous travaillez avec une société partenaire et souhaitez envoyer par courrier électronique une feuille de calcul Excel qui contient des prévisions de chiffres de vente. Vous voulez que vos destinataires puissent voir les chiffres, mais pas les modifier.|Cliquez le bouton **Partage protégé** sur le ruban dans Excel, entrez les adresses de messagerie des deux personnes avec lesquelles vous travaillez dans la société partenaire, sélectionnez **Visionneuse - Affichage uniquement**, puis cliquez sur **Envoyer**.<br /><br />Lorsque le message électronique arrive à la société partenaire, seuls ses destinataires peuvent afficher la feuille de calcul. Ils ne peuvent pas l’enregistrer, la modifier, l’imprimer ou la transférer.<br /><br />Procédure pas à pas : [Protéger un fichier que vous partagez par e-mail à l’aide de l’application de partage Rights Management](sharing-app-protect-by-email.md).|
|**... envoyer en toute sécurité un document par courrier électronique à une personne qui utilise un appareil iOS**<br /><br />Vous souhaitez envoyer un document Word hautement confidentiel à un collègue qui consulte régulièrement sa messagerie électronique sur un appareil iOS.|Utilisez l’Explorateur de fichiers pour faire un clic droit sur le fichier et sélectionnez **Partage protégé** pour envoyer le fichier en pièce jointe à votre collaborateur.<br /><br />Le destinataire reçoit l’e-mail sur son appareil iOS. Étant donné que le destinataire ne dispose pas d’Office pour iPad et iPhone, il clique sur le lien dans l’e-mail qui indique comment télécharger l’application de partage, installe la version pour les appareils iOS, puis affiche le document¹.<br /><br />Procédure pas à pas : [Protéger un fichier que vous partagez par e-mail à l’aide de l’application de partage Rights Management](sharing-app-protect-by-email.md).|
|**... vérifier qui a ouvert mes documents protégés et quand, et révoquer l’accès si nécessaire**<br /><br />Vous avez partagé en toute sécurité un document de conception confidentiel avec des fournisseurs potentiels, et voulez maintenant voir qui l’a consulté, quand et où. Ensuite, une fois le fournisseur choisi, vous souhaitez révoquer l’accès au document d’origine afin que les personnes avec lesquelles vous l’avez partagé ne puissent plus le lire.|Après avoir partagé un document par courrier électronique, vous accédez au [site de suivi de document](http://go.microsoft.com/fwlink/?LinkId=529562) pour vérifier qui a accédé au document et quand. Lorsque vous voulez mettre fin au partage, vous sélectionnez l’option permettant de révoquer l’accès.<br /><br />Procédure pas à pas : [Suivre et révoquer vos documents lorsque vous utilisez l’application de partage RMS](sharing-app-track-revoke.md).|
|**... ouvrir en toute sécurité un fichier partagé reçu en pièce jointe d’un e-mail, mais que je ne parviens pas à lire, car mon entreprise n’utilise pas Rights Management**<br /><br />L’expéditeur du courrier électronique est quelqu’un à qui vous faites confiance pour avoir fait des affaires avec lui par le passé, et vous pensez qu’il vous envoie des informations concernant une opportunité commerciale.|Suivez les instructions contenues dans le message électronique et cliquez sur le lien pour vous inscrire à Microsoft Rights Management. Microsoft confirme que votre organisation ne dispose pas d’un abonnement à Azure Information Protection et vous envoie un e-mail pour terminer le processus d’inscription gratuite. Vous pouvez alors vous connecter avec votre nouveau compte. Cliquez sur le deuxième lien contenu dans le message électronique pour installer l’application de partage Rights Management. Vous pouvez ensuite ouvrir les pièces jointes pour prendre connaissance de la nouvelle opportunité commerciale.<br /><br />Procédure pas à pas : [Afficher et utiliser des fichiers qui ont été protégés par Rights Management](sharing-app-view-use-files.md).|
|**... protéger des fichiers confidentiels de mon entreprise sur mon ordinateur portable pour que des personnes extérieures à l’entreprise ne puissent pas y accéder**<br /><br />Vous voyagez beaucoup et utilisez votre ordinateur portable pour ouvrir et modifier des fichiers figurant dans un dossier qui doit être protégé contre tout accès non autorisé.|L’application de partage RMS est installée sur votre ordinateur portable. Vous utilisez l’Explorateur de fichiers pour protéger les fichiers en utilisant un modèle qui protège rapidement les fichiers. En cas de vol de votre ordinateur portable, vous pouvez garder l’esprit tranquille, car personne d’extérieur à la société ne pourra accéder à ces documents.<br /><br />Procédure pas à pas : [Protéger un fichier sur un appareil &#40;protéger sur place&#41; à l’aide de l’application de partage Rights Management](sharing-app-protect-in-place.md).|
¹ Rendu PDF avec Foxit. Copyright © 2003-2014 Foxit Corporation.

## <a name="what-do-you-want-to-do"></a>Que souhaitez-vous faire ?
> [!NOTE]
> Pour obtenir des informations techniques supplémentaires, comme les [types de fichiers pris en charge](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) et la [procédure d’installation de cette application sur un réseau d’entreprise](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application), consultez le [Guide de l’administrateur de l’application de partage Rights Management](sharing-app-admin-guide.md).

- [Télécharger et installer l’application de partage](install-sharing-app.md)

- [Protéger un fichier sur un appareil (protéger sur place)](sharing-app-protect-in-place.md)

- [Protéger un fichier que vous partagez par e-mail](sharing-app-protect-by-email.md)

- [Changer les autorisations sur des fichiers protégés](sharing-app-reprotect-files.md)

- [Suivre et révoquer vos documents](sharing-app-track-revoke.md)

- [Afficher et utiliser des fichier protégés](sharing-app-view-use-files.md)

- [Supprimer la protection d’un fichier](sharing-app-remove-protection.md)

- [Utiliser les raccourcis clavier](sharing-app-keyboard-shortcuts.md)

- [Spécifier les paramètres dans la boîte de dialogue](sharing-app-dialog-box.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


