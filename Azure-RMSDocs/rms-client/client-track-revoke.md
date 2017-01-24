---
title: "Suivre et révoquer vos documents protégés quand vous utilisez Azure Information Protection | Azure Information Protection"
description: "Une fois que vous avez protégé vos documents, vous pouvez suivre la manière dont les personnes les utilisent. Si nécessaire, vous pouvez également révoquer l’accès à ces documents si ces personnes ne doivent plus être en mesure de les lire."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 54abc32a6065bb3863cf55b42466250f8fc9c634


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Suivre et révoquer vos documents quand vous utilisez Azure Information Protection

>*S’applique à : Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

**[Cette version du client est une préversion susceptible d’être modifiée.]**

Une fois que vous avez protégé vos documents avec Azure Information Protection, vous pouvez suivre leur utilisation. Si nécessaire, vous pouvez également révoquer l’accès à ces documents si des personnes ne doivent plus être en mesure de les lire. Pour cela, utilisez le **site de suivi des documents**, auquel vous pouvez accéder à partir d’un ordinateur Windows ou Mac, d’une tablette ou d’un téléphone.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Après avoir accédé à ce site, connectez-vous pour assurer le suivi de vos documents. Sous réserve que votre organisation dispose d’un [abonnement qui prend en charge le suivi et la révocation de documents](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) et qu’une licence vous a été attribuée dans le cadre de cet abonnement, vous pouvez voir qui a essayé d’ouvrir les fichiers que vous avez protégés, si ces personnes y sont parvenues (ont bien été authentifiées) ou pas, Vous voyez également le nombre de fois où elles ont tenté d’accéder au document, ainsi que leur emplacement à ce moment-là. De plus :

-   Si vous souhaitez arrêter le partage d’un document : cliquez sur **Révoquer l’accès**, notez la durée pendant laquelle le document restera disponible et choisissez d’informer ou non les utilisateurs que vous révoquez l’accès au document partagé, puis envoyez un message personnalisé. Quand vous révoquez un document, il n’est pas supprimé, mais les utilisateurs autorisés ne peuvent plus l’ouvrir.

-   Si vous souhaitez exporter vers Excel : cliquez sur **Exporter au format CSV** pour pouvoir modifier les données et créer vos propres vues et graphiques.

-   Si vous souhaitez configurer des notifications par courrier électronique : cliquez sur **Paramètres** et indiquez si vous souhaitez recevoir des messages électroniques lorsque quelqu’un accède au document et de quelle manière.

- Si vous voulez suivre et révoquer des documents partagés pour d’autres utilisateurs : les administrateurs pour Azure Information Protection peuvent cliquer sur l’icône Administrateur pour effectuer le suivi et la révocation de documents protégés pour d’autres utilisateurs. Cette icône n’est accessible qu’aux administrateurs.

-   Si vous avez des questions ou souhaitez fournir des commentaires sur le site de suivi de document : cliquez sur l’icône d’aide pour accéder au [Forum aux questions sur le suivi de documents](http://go.microsoft.com/fwlink/?LinkId=523977).

## <a name="using-office-to-access-the-document-tracking-site"></a>Utilisation d’Office pour accéder au site de suivi de document

-   Pour les applications Office Word, Excel, PowerPoint et Outlook : sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Suivre l’utilisation**.

Si vous ne voyez pas ces options dans vos applications Office, le client Azure Information Protection n’est probablement pas installé sur votre ordinateur, vous devez redémarrer vos applications Office ou vous devez redémarrer votre ordinateur pour terminer l’installation. Pour plus d’informations sur la façon d’installer le client Azure Information Protection, consultez [Télécharger et installer le client Azure Information Protection](install-client-app.md).


### <a name="other-ways-to-track-and-revoke-your-documents"></a>Autres méthodes de suivi et de révocation de vos documents
Outre le suivi de vos documents protégés sur les ordinateurs Windows à l’aide des applications Office, vous pouvez également utiliser ces méthodes :

-   **Avec un navigateur web**: cette méthode fonctionne pour tous les appareils pris en charge.

-   **Avec l’Explorateur de fichiers**: cette méthode fonctionne sur tous les ordinateurs Windows.

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Utilisation d’un navigateur web pour accéder au site de suivi de document

-   Dans un navigateur pris en charge, accédez au [site de suivi de document](https://go.microsoft.com/fwlink/?LinkId=529562).

    Navigateurs pris en charge : nous vous recommandons d’utiliser Internet Explorer (version 10 ou ultérieure). Toutefois, vous pouvez accéder au site de suivi de document depuis tous les navigateurs répertoriés ci-après :

    -   Internet Explorer : version 10 ou ultérieure

    -   Internet Explorer 9 avec MS12-037 minimum : mise à jour de sécurité cumulative pour Internet Explorer : 12 juin 2012

    -   Mozilla Firefox : version 12 ou ultérieure

    -   Apple Safari 5 : version 5 ou ultérieure

    -   Google Chrome : version 18 ou ultérieure

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>Utilisation de l’Explorateur de fichiers pour accéder au site de suivi de document

-   Cliquez avec le bouton droit sur le fichier, sélectionnez **Classifier et protéger (préversion)**, puis dans **Azure Information Protection Viewer**, sélectionnez l’icône Suivre l’utilisation.


## <a name="other-instructions"></a>Autres instructions
Pour obtenir des instructions pratiques, consultez les sections suivantes du guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


