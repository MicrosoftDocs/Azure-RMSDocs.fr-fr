---
title: "Scénario - Envoyer un e-mail confidentiel de l’entreprise | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 950799e9-2289-48c7-b95a-f54a8ead520a
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: b6f3b06485dda81be2a36035fea7477f4061a8e9


---

# Scénario - Envoyer un e-mail confidentiel de l’entreprise

*S’applique à : Azure Rights Management, Office 365*

Ce scénario et la documentation utilisateur associée utilisent Azure Rights Management afin que n’importe quel utilisateur de l’organisation puisse envoyer de manière sécurisée des communications par e-mail qui ne peuvent pas être lues à l’extérieur de l’organisation. Par exemple, si quelqu’un transfère l’e-mail à une personne d’une autre organisation ou vers un compte de messagerie personnel. Les e-mails et pièces jointes sont protégés par Azure Rights Management et un modèle choisi par les utilisateurs à partir du client de messagerie.

La façon la plus simple d’activer ce scénario consiste à utiliser un des modèles par défaut intégrés qui limitent automatiquement l’accès à tous les utilisateurs de votre organisation. Si nécessaire, vous pouvez le rendre plus restrictif en créant un modèle personnalisé qui, par exemple, restreint l’accès à un sous-ensemble d’utilisateurs, ou qui comporte d’autres restrictions, telles que la lecture seule ou une date d’expiration, ou qui désactive le bouton Transférer du client de messagerie.

> [!IMPORTANT]
> Dans ce scénario vous pouvez supprimer le droit de **transfert** à partir d’un modèle personnalisé que vous configurez pour désactiver le bouton Transférer du client de messagerie. Toutefois, cette configuration n’empêche pas les utilisateurs de partager l’e-mail avec un autre utilisateur autorisé. Le destinataire peut enregistrer l’e-mail (et les pièces jointes), puis partager les informations à l’aide d’autres mécanismes de partage.
> 
> Par exemple, Bob envoie un e-mail à Alice à l’aide d’un modèle personnalisé qui applique les droits personnalisés Enregistrer le fichier et Modifier le contenu au groupe Marketing et n’inclut pas le droit de transfert. Même si Alice ne peut pas transférer l’e-mail à d’autres personnes, elle peut enregistrer le message et ses pièces jointes sur un lecteur USB ou un partage de serveur de fichiers, que n’importe quel membre du groupe Marketing peut ensuite lire et modifier s’il a accès à ces fichiers. Les utilisateurs qui n’appartiennent pas au groupe Marketing ne seront pas en mesure d’ouvrir le contenu.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   N’importe quel utilisateur souhaite partager des informations avec d’autres personnes au sein d’une organisation. Toutefois, les informations ne doivent pas être partagées à l’extérieur de celle-ci.

-   Les informations à partager peuvent se trouver dans un e-mail ou une pièce jointe.

-   Les utilisateurs doivent sélectionner manuellement le modèle à partir de leur client de messagerie.

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont remplies avant de poursuivre avec la documentation utilisateur.

## Conditions requises pour ce scénario
Pour pouvoir appliquer les instructions de ce scénario, les conditions suivantes doivent être réunies :

|Configuration requise|Si vous avez besoin d'informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory|[Préparation pour Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Votre clé de locataire Azure Rights Management est gérée par Microsoft ; vous n’utilisez pas BYOK|[Planification et implémentation de votre clé de locataire Azure Rights Management](https://technet.microsoft.com/library/dn440580.aspx)|
|Azure Rights Management est activé|[Activation d'Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Une des causes suivantes :<br /><br />- Exchange Online est activé pour Azure Rights Management<br /><br />- Le connecteur RMS est installé et configuré pour Exchange sur site|Pour Exchange Online : consultez la section **Exchange Online : configuration de la gestion des droits relatifs à l’information** dans [Configuration d’applications pour Azure Rights Management](https://technet.microsoft.com/library/jj585031.aspx).<br /><br />Pour Exchange sur site : [Déploiement du connecteur Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Vous n’avez pas archivé le modèle Azure Rights Management par défaut **&lt;organisation&gt; - confidentiel**. Ou bien, vous avez configuré un modèle personnalisé à cette fin, car vous avez besoin des paramètres plus restrictifs ou seul un sous-ensemble d’utilisateurs de l’organisation doit être en mesure de lire les e-mails protégés.|[Configuration de modèles personnalisés pour Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)<br /><br />Conseil : si vous avez besoin de paramètres de stratégie d’utilisation plus restrictifs pour tous les utilisateurs de l’organisation, copiez et modifiez un des modèles par défaut, plutôt que de créer un nouveau modèle.<br /><br />Les modèles mis à jour ne sont pas immédiatement actualisés pour les clients de messagerie de ce scénario. Consultez la section [Actualisation des modèles pour les utilisateurs](https://technet.microsoft.com/library/dn642472.aspx) de l’article portant sur les modèles de configuration pour obtenir des informations supplémentaires.|
|Les utilisateurs qui envoient l’e-mail protégé disposent d’Outlook 2013, Outlook 2016 ou d’Outlook Web Access.<br /><br />Les utilisateurs qui reçoivent l’e-mail ont un client de messagerie prenant en charge Azure Rights Management.|Vous pouvez utiliser Outlook 2010, toutefois vous devez [installer l’application de partage Rights Management pour Windows](https://technet.microsoft.com/library/dn339003.aspx) et adapter les instructions de l’utilisateur en conséquence.<br /><br />Pour consulter la liste des clients de messagerie prenant en charge Azure Rights Management, consultez la colonne **E-mail** du tableau [Capacité des périphériques clients ](https://technet.microsoft.com/library/dn655136.aspx) de [Conditions requises pour Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx)|

## Instructions de la documentation utilisateur
En utilisant le modèle suivant, copiez et collez les instructions utilisateur dans une communication à destination de vos utilisateurs finaux, puis apportez ces modifications en les adaptant à votre environnement :

1.  Remplacez toutes les instances de *&lt;nom de l’organisation&gt;* par le nom de votre organisation.

2.  Remplacez toutes les instances de *&lt;nom de l’organisation - Confidentiel&gt;* par le nom de votre modèle par défaut ou personnalisé.

3.  Remplacez les captures d’écran afin qu’elles affichent les noms de modèle de votre organisation.

4.  Remplacez *&lt;coordonnées&gt;* par des instructions indiquant comment contacter le support technique, telles qu’un lien vers un site web, une adresse e-mail ou un numéro de téléphone.

5.  **Voici des modifications supplémentaires que vous pouvez être amené à effectuer :**

    -   S’il est pratique de limiter les instructions à un seul client de messagerie, envisagez de l’effectuer par souci de simplicité et de supprimer l’autre ensemble d’instructions.

    -   Si vous utilisez un modèle personnalisé plutôt que celui suggéré par défaut, modifiez la formulation en conséquence :

        -   Utilisez un titre plus spécifique.

        -   Indiquez les utilisateurs ou les groupes à sélectionner à l’étape 1.

        -   Spécifiez le nom du modèle personnalisé à l’étape 2.

        -   Modifiez le paragraphe final explicatif des restrictions qui s’appliquent aux destinataires.

6.  Apportez les autres modifications de votre choix à cet ensemble d’instructions, puis adressez-le à ces utilisateurs.

7.  Étant donné que certains clients ne prennent pas en charge Rights Management, vous devrez peut-être fournir des informations et des recommandations aux destinataires de ces e-mails protégés. Ces informations reposent sur les appareils et les applications de messagerie utilisés au sein de votre organisation et sur vos préférences. Recommandez, par exemple, que les utilisateurs iOS lisent les e-mails protégés avec Outlook pour iPad et iPhone plutôt qu’avec le client de messagerie iOS natif.

    Pour en savoir plus sur les clients de messagerie, consultez la colonne **E-mail** du tableau [Capacité des périphériques clients ](https://technet.microsoft.com/library/dn655136.aspx) de [Conditions requises pour Azure Rights Management](https://technet.microsoft.com/library/dn655136.aspx).

L’exemple de documentation illustre la façon dont ces instructions se présentent aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### Procédure d’envoi d’e-mails contenant des informations confidentielles de l’entreprise à l’aide d’Outlook

1.  Dans Outlook, créez un message, ajoutez les pièces jointes que vous souhaitez inclure, puis sélectionnez les utilisateurs ou les groupes dans *&lt;nom de l’organisation&gt;*.

2.  Sous l’onglet **OPTIONS**, cliquez sur **Autorisation**, puis sélectionnez **&lt;nom de l’organisation - Confidentiel&gt;** :

    ![Capture d’écran de procédure d’envoi de messages contenant des informations confidentielles de l’entreprise à l’aide d’Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envoyez le message.

### Procédure d’envoi d’e-mails contenant des informations confidentielles de l’entreprise à l’aide d’Outlook Web App

1.  Dans Outlook Web App, créez un message, ajoutez les pièces jointes que vous souhaitez inclure, puis sélectionnez les utilisateurs ou les groupes de *&lt;nom de l’organisation&gt;* dans le carnet d’adresses.

2.  Cliquez sur **…**, sur **Définir les autorisations**, puis sélectionnez **&lt;nom de l’organisation - Confidentiel&gt;** :

    ![Capture d’écran de procédure d’envoi de messages contenant des informations confidentielles de l’entreprise à l’aide d’Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envoyez le message.

Quand une personne figurant sur la ligne **À**, **Cc**, ou **Cci** reçoit ce message, il peut lui être demandé de s’authentifier avant de pouvoir lire le message pour vérifier qu’il s’agit d’un utilisateur de *&lt;nom de l’organisation&gt;*. Les utilisateurs ne sont pas invités à s’authentifier lorsqu’ils le sont déjà.

Les destinataires de votre message pourront le transférer à d’autres personnes, mais seuls les utilisateurs de *&lt;nom de l’organisation&gt;* pourront le lire. Si vous attachez un document Office, celui-ci aura la même protection, même si cette pièce jointe est enregistrée avec un nom différent, à un autre emplacement. Toutefois, les utilisateurs authentifiés avec succès peuvent effectuer des opérations de copier et coller ou d’impression à partir de l’e-mail ou de la pièce jointe. Si vous avez besoin d’une protection plus restrictive empêchant des actions telles que celles-ci, contactez le support technique.

**Vous avez besoin d'aide ?**

-   Contactez le support technique :

    -   *&lt;coordonnées&gt;*

### Exemple de documentation utilisateur personnalisée
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Procédure d’envoi d’e-mails contenant des informations confidentielles de l’entreprise à l’aide d’Outlook

1.  Dans Outlook, créez un nouvel e-mail, ajoutez les pièces jointes que vous souhaitez inclure, puis sélectionnez les utilisateurs ou les groupes VanArsdel à partir du carnet d’adresses.

2.  À partir de l’onglet **OPTIONS**, cliquez sur **Autorisation**, puis sélectionnez **VanArsdel, Ltd - Confidentiel** :

    ![Capture d’écran de procédure d’envoi de messages contenant des informations confidentielles de l’entreprise à l’aide d’Outlook](../media/AzRMS_OutlookTemplate.PNG)

3.  Envoyez le message.

#### Procédure d’envoi d’e-mails contenant des informations confidentielles de l’entreprise à l’aide d’Outlook Web App

1.  Dans Outlook Web App, créez un nouvel e-mail, ajoutez les pièces jointes que vous souhaitez inclure, puis sélectionnez les utilisateurs ou les groupes VanArsdel à partir du carnet d’adresses.

2.  Cliquez sur **…**, sur **Définir les autorisations**, puis sélectionnez **VanArsdel, Ltd - Confidentiel** :

    ![Capture d’écran de procédure d’envoi de messages contenant des informations confidentielles de l’entreprise à l’aide d’Outlook Web App](../media/AzRMS_OWATemplate.png)

3.  Envoyez le message.

Lorsqu’une personne figurant sur la ligne **À**, **Cc**, ou **Cci** reçoit cet e-mail, il peut lui être demandé de s’authentifier avant de pouvoir lire le message afin de vérifier qu’il s’agit d’un utilisateur de VanArsdel, Ltd. Les utilisateurs ne sont pas invités à s’authentifier lorsqu’ils le sont déjà.

Les destinataires de votre e-mail pourront le transférer à d’autres personnes, toutefois seuls les utilisateurs de VanArsdel pourront le lire. Si vous attachez un document Office, celui-ci aura la même protection, même si cette pièce jointe est enregistrée avec un nom différent, à un autre emplacement. Toutefois, les utilisateurs authentifiés avec succès peuvent effectuer des opérations de copier et coller ou d’impression à partir de l’e-mail ou de la pièce jointe. Si vous avez besoin d’une protection plus restrictive empêchant des actions telles que celles-ci, contactez le support technique.

**Vous avez besoin d'aide ?**

-   Contactez le support technique :

    -   Adresse électronique : helpdesk@vanarsdelltd.com




<!--HONumber=Jun16_HO4-->


