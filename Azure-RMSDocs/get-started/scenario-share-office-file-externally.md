---
title: "Scénario AIP : Partager des fichiers Microsoft Office avec des utilisateurs externes"
description: "Ce scénario et la documentation utilisateur associée s’appuient sur la protection Azure Rights Management pour permettre à des utilisateurs d’envoyer un fichier Office par e-mail en toute sécurité à des personnes appartenant à une autre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c10a4d7b-f57a-4a43-b66e-477777be59cc
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bf7fac8cf06281fd75376fc3d5d2fa4fe17a6a33
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="scenario---share-an-office-file-with-users-in-another-organization"></a>Scenario : partager un fichier Office avec des utilisateurs d’une autre organisation

>*S’applique à : Azure Information Protection, Office 365*

Ce scénario et la documentation utilisateur associée s’appuient sur la technologie Azure Rights Management d’Azure Information Protection pour permettre à des utilisateurs d’envoyer un fichier Office par e-mail en toute sécurité à des personnes appartenant à une autre organisation. Le fichier Office peut être un document Word, une feuille de calcul Excel ou une présentation PowerPoint qui contient, par exemple, des informations tarifaires pour un partenaire, une liste de produits pour un revendeur ou une liste de délais de livraison pour des clients potentiels. Lorsque les utilisateurs suivent les instructions, le fichier joint au message électronique est protégé par Azure Rights Management.

Ce scénario convient dans les cas suivants :

-   L’employé doit envoyer des informations à l’extérieur de l’organisation par e-mail sous la forme d’un document Office en pièce jointe.

-   Le document contient des informations qui, sans être publiques, ne sont pas réservées à une utilisation interne.

-   Les utilisateurs destinataires n'ont pas besoin de partager ces informations avec d'autres, de les imprimer ou de les utiliser dans le cadre de leur propre documentation. Si tel n'est pas le cas, vous pouvez modifier les instructions de l'utilisateur, en passant des autorisations d'affichage en lecture seule à une autre option permettant au destinataire de modifier la pièce jointe.

-   L’employé peut être soucieux de savoir quand ce document est ouvert par l’utilisateur externe.

## <a name="deployment-instructions"></a>Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont remplies avant de poursuivre avec la documentation utilisateur.

## <a name="requirements-for-this-scenario"></a>Conditions requises pour ce scénario
Pour que les instructions pour l'utilisateur décrites dans ce scénario fonctionnent, les éléments suivants doivent être en place :

|Configuration requise|Si vous avez besoin d'informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory|[Préparation d’Azure Information Protection](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management est activé|[Activation d’Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|L'application de partage Rights Management est déployée sur les ordinateurs des utilisateurs qui exécutent Windows|[Déploiement automatique de l'application de partage Microsoft Rights Management](../rms-client/sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)|
|Les utilisateurs disposent d'Outlook version Office 2013|Si les utilisateurs disposent d’Office 2016 ou Office 2010, remplacez la capture d’écran par une version équivalente afin que l’image corresponde à ce que les utilisateurs voient.|
|Votre abonnement Azure Information Protection inclut le suivi de document|Si votre abonnement n’inclut pas le suivi et la révocation de document, les utilisateurs ne seront pas en mesure de suivre toutes les étapes des instructions pour l’utilisateur. Dans ce cas, achetez un abonnement ne prenant pas en charge ces fonctionnalités, ou modifiez les instructions pour l'utilisateur en supprimant les étapes qui utilisent ces fonctionnalités.<br /><br />Consultez la [liste des fonctionnalités](https://www.microsoft.com/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection.|

## <a name="user-documentation-instructions"></a>Instructions de la documentation utilisateur
En utilisant le modèle suivant, copiez et collez les instructions utilisateur dans une communication à destination de vos utilisateurs finaux, puis apportez ces modifications en les adaptant à votre environnement :

1.  Remplacez *&lt;nom du type de document Office&gt;* par le type de document que vos utilisateurs enverront. Utilisez une formulation spécifique de leurs flux de travail qui leur est familière, telle que « tarifs », « délais de livraison » ou « soumission d'appel d'offres », plutôt que « document Word » ou « Feuille de calcul Excel ». Cette formulation plus spécifique permet d’augmenter les chances qu’ils suivent les instructions quand ils utiliseront ces documents.

2.  Remplacez *&lt;coordonnées&gt;* par des instructions indiquant comment contacter le support technique, telles qu’un lien vers un site web, une adresse e-mail ou un numéro de téléphone.

3.  **Voici des modifications supplémentaires que vous pouvez être amené à effectuer :**

    -   À l’étape 2, nous vous suggérons de choisir l’autorisation **Visionneuse – Affichage uniquement**, qui a pour effet de rendre le document joint (pas l’original) accessible en lecture seule pour les destinataires. Si cette restriction n’est pas adaptée aux besoins de votre entreprise, modifiez cette option en choisissant un autre jeu d’autorisations, par exemple, **Réviseur – Affichage et modification**.

    -   À l'étape 3, nous vous suggérons de sélectionner l'option **M'autoriser à révoquer de suite l'accès à ces document** afin qu'une décision éventuelle de vos utilisateurs de révoquer le document soit appliquée immédiatement, mais cette option nécessite que le destinataire dispose toujours d'une connexion Internet pour ouvrir la pièce jointe. Cette étape nécessite également que vous ayez un abonnement prenant en charge le suivi et la révocation des documents. Supprimez cette étape si elle n'est pas pertinente pour vos utilisateurs.

    -   À l'étape 4, nous vous suggérons de sélectionner l'option **M'envoyer un message électronique quand quelqu'un tente d'ouvrir ce document**. Si les utilisateurs suivent leurs documents via le portail de suivi de document, vous pouvez décider que la notification par courrier électronique n'est pas nécessaire et supprimer cette étape.

    -   Les étapes n'incluent pas la définition d'une date d'expiration. Si les informations ne doivent pas être utilisées après une certaine date, ajoutez une autre étape pour définir un délai d’expiration approprié, par exemple, 90 jours après l’envoi du message électronique.

    > [!NOTE]
    > Pour plus d'informations sur chacune des options que les utilisateurs peuvent sélectionner, consultez [Options de boîte de dialogue pour l'application de partage Rights Management](https://technet.microsoft.com/library/dn574738.aspx)

4.  Apportez les autres modifications que vous voulez éventuellement apporter à cet ensemble d’instructions, puis adressez-le à ces utilisateurs.

L’exemple de documentation illustre la façon dont ces instructions se présentent aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="how-to-share-a-ltname-of-office-document-typegt"></a>Comment partager un &lt;nom du type de document Office&gt;

1.  Créez votre e-mail en spécifiant une ou plusieurs adresses e-mail, tapez votre message, puis joignez le *&lt;nom du type de document Office&gt;* à l’e-mail. Ensuite, sous l'onglet **MESSAGE** , dans le groupe **RMS** , cliquez sur **Partager le fichier protégé** , puis de nouveau sur **Partager le fichier protégé** :

    ![Capture d’écran du partage de document Office à l’aide d’Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Dans la boîte de dialogue **Partager le fichier protégé** , sélectionnez **Visionneuse – Affichage uniquement**:

    ![boîte de dialogue Partager le fichier protégé - Visionneuse - Affichage uniquement](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Sélectionnez **M'autoriser à révoquer de suite l'accès à ces documents**:

    ![boîte de dialogue Partager le fichier protégé - révoquer de suite](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Sélectionnez **M'envoyer un message électronique quand quelqu'un tente d'ouvrir ces documents**:

    ![boîte de dialogue Partager le fichier protégé - m’envoyer un message électronique](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Cliquez sur **Envoyer maintenant**.

Quand une personne mentionnée sur la ligne **À**, **Cc** ou **Cci** reçoit cet e-mail, elle voit un message contenant des instructions sur la manière de lire le fichier joint *&lt;nom du type de document Office&gt;*. Elle peut lire le document sur de nombreux appareils tels que iPad, iPhone, tablettes et téléphones Android, ordinateurs Mac et ordinateurs Windows.

Utilisez le [portail de suivi de document](https://track.azurerms.com/) pour savoir si et quand elle ouvre le &lt;nom du type de document Office&gt; joint. Envisagez de la contacter à l’aide d’un appel téléphonique de suivi dès que vous voyez qu’elle a ouvert le &lt;nom du type de document Office&gt;.

**Vous avez besoin d'aide ?**

-   Pour plus d'informations :

    -   [Protéger un fichier que vous partagez par e-mail](../rms-client/sharing-app-protect-by-email.md)

    -   [Suivre et révoquer vos documents](../rms-client/sharing-app-track-revoke.md)

-   Contactez le support technique :

    -   *&lt;coordonnées&gt;*

### <a name="example-customized-user-documentation"></a>Exemple de documentation utilisateur personnalisée
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

#### <a name="how-to-share-a-price-list-with-your-customer"></a>Comment partager une liste de prix avec votre client

1.  Créez votre message électronique en spécifiant les adresses de messagerie de votre client, tapez votre message, puis joignez la dernière liste de prix au message électronique. Ensuite, sous l'onglet **MESSAGE** , dans le groupe **RMS** , cliquez sur **Partager le fichier protégé** , puis de nouveau sur **Partager le fichier protégé** :

    ![Capture d’écran du partage de document Office à l’aide d’Outlook](../media/AzRMSUserInstructions_ShareProtectedRibbon2013.png)

2.  Dans la boîte de dialogue **Partager le fichier protégé** , sélectionnez **Visionneuse – Affichage uniquement**:

    ![boîte de dialogue Partager le fichier protégé - Visionneuse - Affichage uniquement](../media/AzRMS_SharedProtected_ViewerOnly.PNG)

3.  Sélectionnez **M'autoriser à révoquer de suite l'accès à ces documents**:

    ![boîte de dialogue Partager le fichier protégé - révoquer de suite](../media/AzRMS_SharedProtected_InstantRevoke.PNG)

4.  Sélectionnez **M'envoyer un message électronique quand quelqu'un tente d'ouvrir ces documents**:

    ![boîte de dialogue Partager le fichier protégé - m’envoyer un message électronique](../media/AzRMS_SharedProtected_EmailMe.PNG)

5.  Cliquez sur **Envoyer maintenant**.

Quand une personne mentionnée sur la ligne **À**, **Cc**ou **Cci** reçoit ce courrier électronique, elle voit un message contenant des instructions sur la manière de lire la liste de prix jointe. Elle peut lire le document sur de nombreux appareils tels que iPad, iPhone, tablettes et téléphones Android, ordinateurs Mac et ordinateurs Windows.

Utilisez le [portail de suivi de document](https://track.azurerms.com/) pour savoir si et quand elle ouvre la liste de prix jointe. Envisagez de la contacter à l'aide d'un appel téléphonique de suivi dès que vous voyez qu'elle a ouvert la liste de prix.

**Vous avez besoin d'aide ?**

-   Pour plus d'informations :

    -   [Protéger un fichier que vous partagez par e-mail](../rms-client/sharing-app-protect-by-email.md)

    -   [Suivre et révoquer vos documents](../rms-client/sharing-app-track-revoke.md)

-   Contactez le support technique :

    -   E-mail : helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
