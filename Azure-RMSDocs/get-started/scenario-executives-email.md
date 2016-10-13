---
title: "Scénario : échange sécurisé d’informations confidentielles entre cadres| Azure Information Protection"
description: "Ce scénario et la documentation utilisateur associée s’appuient sur la protection Azure Rights Management pour permettre à des cadres de s’échanger des e-mails et des pièces jointes en toute sécurité, tandis que des stratégies limitent automatiquement l’accès aux cadres, sans que ceux-ci aient à prendre des mesures particulières."
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e18cf5df-859e-4028-8d19-39b0842df33d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 8481c275609e74ff5e09a0397e0e3a0346aa4430


---

# Scénario : échange sécurisé d’informations confidentielles entre cadres

>*S’applique à : Azure Information Protection, Office 365*

Ce scénario et la documentation utilisateur associée s’appuient sur la technologie Azure Rights Management d’Azure Information Protection pour permettre à des cadres de s’échanger des e-mails et des pièces jointes en toute sécurité, tandis que des stratégies limitent automatiquement l’accès aux cadres, sans que ceux-ci aient à prendre des mesures particulières. Les e-mails et les pièces jointes éventuelles sont protégés automatiquement par Azure Rights Management.

Si nécessaire, vous pouvez ajouter une exception à la règle, comme l’abréviation NPP (pour « ne pas protéger ») dans l’objet de l’e-mail, pour permettre aux cadres d’apporter cette mention au cas où ils auraient besoin d’envoyer un e-mail non protégé aux autres cadres, par exemple, pour qu’ils l’examinent avant qu’il soit communiqué à d’autres personnes.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Les cadres s’échangent des informations confidentielles qui ne doivent pas être partagées avec d’autres utilisateurs.

-   Les cadres n’ont pas à changer leurs habitudes lorsqu’ils envoient ces messages. Ils doivent simplement les envoyer à une adresse e-mail professionnelle plutôt qu’une adresse personnelle.

-   Les cadres ont la possibilité de remplacer eux-mêmes la règle s’ils ont besoin d’envoyer un e-mail non protégé à d’autres cadres.

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont réunies, puis suivez les instructions pour mener à bien les procédures associées avant de poursuivre avec la documentation utilisateur.

## Conditions requises pour ce scénario
Pour pouvoir appliquer les instructions de ce scénario, les conditions suivantes doivent être réunies :

|Condition requise|Si vous avez besoin d’informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory.<br /><br />- Un groupe à extension messagerie nommé **Cadres**, dont tous les cadres sont membres<br /><br />- Un groupe nommé **Administrateurs RMS** et tous les administrateurs chargés de configurer Azure RMS sont membres de ce groupe|[Préparation d’Azure Information Protection](../plan-design/prepare.md)|
|Votre clé de locataire Azure Information Protection est gérée par Microsoft ; vous n’utilisez pas BYOK|[Planification et implémentation de la clé de locataire Azure Information Protection](../plan-design/plan-implement-tenant-key.md)|
|Azure Rights Management est activé|[Activation d'Azure Rights Management](../deploy-use/activate-service.md)|
|Une de ces configurations :<br /><br />- Exchange Online est activé pour Azure Rights Management<br /><br />- Le connecteur RMS est installé et configuré pour Exchange sur site|Pour Exchange Online : consultez les informations indiquées dans [Exchange Online : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#exchange-online-irm-configuration).<br /><br />Pour Exchange sur site : [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md)|
|Vous avez configuré un modèle personnalisé comme décrit ci-après|[Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|Vous avez configuré une règle de protection de transport pour IRM, comme décrit plus loin dans cet article|Pour Exchange Online : [Flux de messagerie ou règles de transport](https://technet.microsoft.com/library/jj919238(v=exchg.150).aspx)<br /><br />Pour Exchange 2013 : [Créer une règle de protection de transport](https://technet.microsoft.com/en-us/library/dd302432(v=exchg.150))<br /><br />Pour Exchange 2010 : [Créer une règle de protection de transport](https://technet.microsoft.com/library/dd302432(v=exchg.141))|

### Pour configurer le modèle personnalisé pour les cadres

1.  Dans le portail Azure Classic : créez un modèle personnalisé pour Azure Rights Management qui contienne les valeurs et les paramètres suivants :

    -   Nom : **Cadres**

    -   Droits : accordez au groupe à extension messagerie **Cadres** des droits de **Copropriétaire**

    -   Étendue : sélectionnez le groupe à extension messagerie **Cadres** et le groupe à extension messagerie **Administrateurs RMS**.

2.  Publiez le nouveau modèle.

3.  Pour Exchange Online uniquement : actualisez les modèles à l’aide de la commande Windows PowerShell pour Exchange Online :

    ```
    Import-RMSTrustedPublishingDomain -Name "RMS Online -1" -RefreshTemplates -RMSOnline
    ```

### Pour configurer la règle de transport pour IRM

-   Servez-vous de la documentation Exchange référencée dans le tableau pour savoir comment créer la règle de transport avec les paramètres suivants :

    -   Nom : **Appliquer les modèles Cadres aux e-mails des cadres**

    -   Définissez le groupe **Cadres** en tant qu’expéditeur et destinataire de la règle, ainsi qu’une condition supplémentaire.

    -   Pour l’action, sélectionnez **Appliquer la protection des droits au message avec**, puis sélectionnez le modèle **Cadres** que vous avez configuré.

    -   Ajoutez l’exception **NPP** (abréviation de « Ne pas protéger »), ou les termes de votre choix pour identifier cette exception, que vous devez inclure dans l’objet.

    -   Vérifiez que la règle est configurée pour être **appliquée**.

## Instructions de la documentation utilisateur
À moins que vous vouliez fournir des instructions sur la façon de spécifier **NPP** ou les termes ou expressions destinés à qualifier l’exception dans l’objet de l’e-mail, aucune instruction de procédure n’est à donner aux utilisateurs pour ce scénario, car la protection des e-mails en provenance et à destination des cadres n’appellent aucune action de leur part. Les e-mails et les pièces jointes sont automatiquement protégés de manière à ce que seuls les membres du groupe Cadres puissent y accéder.

Cependant, vous serez peut-être amené à informer les cadres et le support technique que ces e-mails sont automatiquement protégés et en quoi cela peut en limiter leur utilisation. Par exemple, ils ne pourront pas être lus par d’autres personnes si ces messages ou pièces jointes sont transférés par la suite à d’autres personnes. Si vous avez configuré l’exception NPP (ou un équivalent), vérifiez que le support technique a connaissance de cette configuration de sorte que les cadres puissent remplacer la règle par eux-mêmes, sans l’intervention d’un administrateur Exchange.

En utilisant le modèle suivant, copiez et collez l’annonce dans une communication à destination de vos utilisateurs finaux, puis apportez ces modifications en les adaptant à votre environnement :

1.  Remplacez les instances de *&lt;nom de l’organisation&gt;* par le nom de votre organisation.

2.  Si vous choisissez une autre chaîne que NPP pour qualifier l’exemption, remplacez cette valeur et l’explication en conséquence.

3.  Remplacez *&lt;domaine_messagerie&gt;* par le nom du domaine de messagerie de votre organisation.

4.  Remplacez *&lt;coordonnées&gt;* par des instructions indiquant comment contacter le support technique, telles qu’un lien vers un site web, une adresse e-mail ou un numéro de téléphone.

5.  Apportez les modifications supplémentaires que vous voulez éventuellement apporter à l’annonce, puis adressez-la à ces utilisateurs.

L’exemple de documentation illustre la façon dont cette annonce se présente aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### Annonce de l’équipe informatique : Les e-mails des cadres de &lt;nom de l’organisation&gt; sont désormais automatiquement protégés
Dès lors, chaque fois que vous enverrez des e-mails à un autre cadre de l’entreprise &lt;nom de l’organisation&gt;, le contenu de ces messages et les pièces jointes seront automatiquement protégés de telle sorte que seul un autre cadre de l’entreprise pourra y avoir accès et lire, imprimer ou encore copier les informations. Cette restriction s’applique même si vous transférez le message à d’autres personnes ou enregistrez les pièces jointes. Cette protection permet d’éviter une perte de données confidentielles et sensibles.

À noter que si vous voulez autoriser d’autres utilisateurs que des cadres de &lt;nom de l’organisation&gt; à lire et à modifier les informations que vous envoyez dans ces e-mails, vous devez les leur envoyer séparément. Ou bien, pour ignorer la protection automatique, tapez les lettres **NPP** (abréviation de « Ne pas protéger ») n’importe où dans l’objet de l’e-mail.

Lors de l’envoi d’informations confidentielles de votre société à un autre cadre de &lt;nom de l’organisation&gt;, pensez à les envoyer à une adresse e-mail professionnelle (*nom*@&lt;domaine_messagerie&gt;) et non à une adresse e-mail personnelle.

**Vous avez besoin d'aide ?**

-   Contactez le support technique : &lt;coordonnées&gt;

### Exemple de documentation utilisateur
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Annonce de l’équipe informatique : Les e-mails des cadres de VanArsdel sont désormais automatiquement protégés
Dès lors, chaque fois que vous enverrez des e-mails à un autre cadre de l’entreprise VanArsdel, le contenu de ces messages et les pièces jointes seront automatiquement protégés de telle sorte que seul un autre cadre de l’entreprise pourra y avoir accès et lire, imprimer ou encore copier les informations. Cette restriction s’applique même si vous transférez le message à d’autres personnes ou enregistrez les pièces jointes. Cette protection permet d’éviter une perte de données confidentielles et sensibles.

À noter que si vous voulez autoriser d’autres utilisateurs que des cadres de VanArsdel à lire et modifier les informations que vous envoyez dans ces e-mails, vous devez les leur envoyer séparément. Ou bien, pour ignorer la protection automatique, tapez les lettres **NPP** (abréviation de « Ne pas protéger ») n’importe où dans l’objet de l’e-mail.

Lors de l’envoi d’informations confidentielles de votre société à un autre cadre de VanArsdel, pensez à les envoyer à une adresse de messagerie professionnelle (*nom*@&lt;vanarsdelltd.com) et non à une adresse de messagerie personnelle.

**Vous avez besoin d'aide ?**

-   Contactez le support technique : helpdesk@vanarsdelltd.com




<!--HONumber=Oct16_HO1-->


