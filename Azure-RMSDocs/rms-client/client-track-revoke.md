---
title: "Suivi et révocation de documents - Azure Information Protection"
description: "Une fois que vous avez protégé vos documents, vous pouvez suivre la manière dont les personnes les utilisent. Si nécessaire, vous pouvez également révoquer l’accès à ces documents si ces personnes ne doivent plus être en mesure de les lire."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79c02795ca10ff875744f3b6c90cebd582cb8c3e
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="track-and-revoke-your-documents-when-you-use-azure-information-protection" class="xliff"></a>

# Suivre et révoquer vos documents quand vous utilisez Azure Information Protection

>*S’applique à : Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Une fois que vous avez protégé vos documents avec Azure Information Protection, vous pouvez suivre leur utilisation. Si nécessaire, vous pouvez également révoquer l’accès à ces documents si des personnes ne doivent plus être en mesure de les lire. Pour cela, utilisez le **site de suivi des documents**, auquel vous pouvez accéder à partir d’un ordinateur Windows ou Mac, d’une tablette ou d’un téléphone.

Après avoir accédé à ce site, connectez-vous pour assurer le suivi de vos documents. Sous réserve que votre organisation dispose d’un [abonnement qui prend en charge le suivi et la révocation de documents](https://www.microsoft.com/cloud-platform/azure-information-protection-features) et qu’une licence vous a été attribuée dans le cadre de cet abonnement, vous pouvez voir qui a essayé d’ouvrir les fichiers que vous avez protégés, si ces personnes y sont parvenues (ont bien été authentifiées) ou pas, Vous voyez également le nombre de fois où elles ont tenté d’accéder au document, ainsi que leur emplacement à ce moment-là. De plus :

- Si vous voulez cesser le partage d'un document : 
    
    - Cliquez sur **Révoquer l'accès**, notez la durée pendant laquelle le document continuera d'être disponible, décidez de faire savoir ou non aux personnes que vous révoquez l'accès à un document précédemment partagé et spécifiez un message personnalisé. Quand vous révoquez un document, il n’est pas supprimé, mais les utilisateurs autorisés ne peuvent plus l’ouvrir :
        
        ![Icône Révoquer l’accès du site de suivi de document](../media/tracking-site-revoke-access-icon.png)
        
- Si vous voulez exporter vers Excel : 
    
    - Cliquez sur **Exporter au format CSV**, de sorte que vous pouvez ensuite modifier les données et créer vos propres vues et graphiques :
         
        ![Icône Exporter au format CSV du site de suivi de document](../media/tracking-site-export-icon.png)
         
- Si vous voulez configurer des notifications par courrier électronique : 
     
    - Cliquez sur **Paramètres** et choisissez si vous voulez recevoir une notification quand une personne accède au document et si oui, comment :
        
        ![Icône Exporter au format CSV du site de suivi de document](../media/tracking-site-settings-email.png)

- Si vous souhaitez suivre et révoquer des documents partagés pour d’autres :
    
    - Les administrateurs pour Azure Information Protection peuvent cliquer sur l’icône Administrateur pour effectuer le suivi et la révocation de documents protégés pour d’autres utilisateurs. Cette icône n’est accessible qu’aux administrateurs :
        
        ![Icône Administrateur du site de suivi de document](../media/tracking-site-admin-icon.png)

À moins d’être un administrateur, vous pouvez suivre et révoquer uniquement les documents que vous avez protégés. Vous ne pouvez pas effectuer le suivi de vos messages électroniques protégés en utilisant le site de suivi de document.

> [!NOTE] 
> Si votre administrateur a configuré les contrôles de confidentialité pour le site de suivi de documents, vous ne verrez peut-être pas lorsque les utilisateurs de votre organisation ont accédé à un document que vous suivez. Un administrateur peut exempter tous les utilisateurs ou seulement certains. Toutefois, vous pouvez toujours révoquer l’accès aux documents que vous suivez.

Pour effectuer le suivi d’un document que vous avez protégé, vous devez utiliser votre ordinateur Windows pour l’inscrire auprès du site de suivi de documents. Pour ce faire, utilisez l’Explorateur de fichiers ou vos applications Office.

<a id="using-office-to-track-or-revoke-the-document" class="xliff"></a>

## Utilisation d’Office pour suivre ou révoquer le document

Pour les applications Office, Word, Excel, PowerPoint et Outlook : 

1. Ouvrez le document protégé que vous souhaitez suivre ou révoquer.

2. Dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger** > **Suivre et révoquer** :

    ![Option Suivre l’utilisation](../media/track-usage-callout.png)

Si vous ne voyez pas ces options dans vos applications Office, le client Azure Information Protection n’est probablement pas installé sur votre ordinateur, vous devez redémarrer vos applications Office ou vous devez redémarrer votre ordinateur pour terminer l’installation. Pour plus d’informations sur la façon d’installer le client Azure Information Protection, consultez [Télécharger et installer le client Azure Information Protection](install-client-app.md).

<a id="using-file-explorer-to-track-or-revoke-the-document" class="xliff"></a>

## Utilisation de l’Explorateur de fichiers pour suivre ou révoquer le document

1. Cliquez avec le bouton droit sur le fichier protégé, et sélectionnez **Classifier et protéger**.

2. À partir de la boîte de dialogue **Classifier et protéger - Azure Information Protection**, sélectionnez **Suivre et révoquer**.

    ![Icône Suivre et révoquer l’icône de la boîte de dialogue Classifier et protéger - Azure Information Protection](../media/track-and-revoke.png)


<a id="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered" class="xliff"></a>

### Utilisation d’un navigateur web pour suivre et révoquer des documents que vous avez enregistrés

Une fois que vous avez enregistré le document protégé à l’aide de vos applications Office ou de l’Explorateur de fichiers, vous pouvez suivre et révoquer ces documents à l’aide d’un navigateur web pris en charge :

- Sur votre PC Windows, ordinateur Mac ou appareil mobile, visitez le [site de suivi des documents](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Navigateurs pris en charge** : nous vous recommandons d’utiliser Internet Explorer (version 10 ou ultérieure). Toutefois, vous pouvez accéder au site de suivi de document depuis tous les navigateurs répertoriés ci-après :

    -   Internet Explorer : version 10 ou ultérieure

    -   Internet Explorer 9 avec MS12-037 minimum : mise à jour de sécurité cumulative pour Internet Explorer : 12 juin 2012

    -   Mozilla Firefox : version 12 ou ultérieure

    -   Apple Safari 5 : version 5 ou ultérieure

    -   Google Chrome : version 18 ou ultérieure


<a id="other-instructions" class="xliff"></a>

## Autres instructions
Plus d’instructions pratiques dans le guide de l’utilisateur Azure Information Protection :

- [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]