---
title: "Scénario - Sécuriser vos fichiers les plus précieux | Azure Information Protection"
description: "Ce scénario et la documentation utilisateur associé utilisent Azure Rights Management pour protéger de manière manuelle et personnalisée un certain nombre de fichiers que vous considérez comme les plus précieux, qui assure le plus haut niveau de protection qui soit contre tout accès non autorisé."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0f2fb608be647e967d8e5857414f25ebba1d4d29


---

# <a name="scenario---secure-your-most-few-valuable-files"></a>Scénario - Sécuriser vos fichiers les plus précieux

>*S’applique à : Azure Information Protection, Office 365*

Ce scénario et la documentation utilisateur associée utilisent la technologie Azure Rights Management d’Azure Information Protection pour protéger de manière manuelle et personnalisée un certain nombre de fichiers que vous considérez comme les plus précieux, qui assure le plus haut niveau de protection qui soit contre tout accès non autorisé. Il s’agit généralement de fichiers auxquels seules quelques personnes doivent pouvoir accéder. Par exemple, les instructions relatives à la recette d’un produit alimentaire distinctif de votre société ou des plans de reprise qui ne doivent pas être rendus publics avant une date définie.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Vous avez identifié l’ensemble de fichiers à protéger.

-   Les fichiers sont dans un des formats de fichier Office prenant en charge Rights Management. Si les formats de fichiers sont différents (par exemple, s’il s’agit de fichiers de CAO), vérifiez qu’ils prennent en charge Azure RMS et que vous déployez des applications prenant en charge Azure RMS de manière native. Pour plus d’informations, consultez [Comment les applications prennent en charge le service Azure Rights Management](../understand-explore/applications-support.md).

-   Les fichiers contiennent des informations hautement confidentielles et sensibles qui doivent être accessibles à quelques personnes uniquement.

-   La nécessité de disposer d’une connexion Internet pour autoriser chaque accès à un fichier est un compromis acceptable pour ces personnes, dans la mesure où cela garantit une meilleure sécurité.

-   Ces utilisateurs n’ont pas besoin de partager ces informations avec d’autres personnes. Ils peuvent toutefois modifier ces informations et les enregistrer.

-   L’administrateur doit être en mesure de savoir qui accède aux fichiers et à quel moment et de bloquer l’accès si nécessaire.

## <a name="deployment-instructions"></a>Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont réunies, puis suivez les instructions pour mener à bien les procédures associées avant de poursuivre avec la documentation utilisateur.

## <a name="requirements-for-this-scenario"></a>Conditions requises pour ce scénario
Pour ce scénario, les éléments suivants doivent être en place :

|Condition requise|Si vous avez besoin d’informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory.<br /><br />- Un groupe nommé **Accès privilégié** ayant accès aux e-mails, qui contient les personnes devant avoir accès à ces documents hautement confidentiels<br /><br />- Un groupe nommé **Responsables de la conformité informatique** ayant accès aux e-mails, qui contient les personnes dont le travail inclut eDiscovery, la surveillance et l’audit<br /><br />- Un groupe nommé **Administrateurs RMS** et tous les administrateurs chargés de configurer Azure RMS sont membres de ce groupe|[Préparation d’Azure Information Protection](../plan-design/deployment-roadmap.md)|
|Azure Rights Management est activé|[Activation d’Azure Rights Management](../deploy-use/activate-service.md)|
|Vous avez configuré un modèle personnalisé comme décrit ci-après|[Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md)|
|L’application de partage Rights Management est déployée sur votre ordinateur Windows afin que vous puissiez protéger ces fichiers sur place, comme décrit dans la section suivante|[Télécharger et installer l'application de partage Rights Management](../rms-client/install-sharing-app.md)|
|Les utilisateurs autorisés ont une version minimale d’Office 2013|Si les utilisateurs disposent d’Office 2010, ils doivent également installer l’application de partage Rights Management.|
|Votre abonnement Azure Information Protection inclut le suivi des documents|Si votre abonnement n’inclut pas le suivi et la révocation des documents, vous ne pouvez pas utiliser le site de suivi des documents pour voir qui accède à ces documents et en révoquer l’accès si nécessaire. Dans ce cas, souscrivez un abonnement prenant en charge le suivi des documents ou acceptez cette restriction. Vous pouvez également envisager d’utiliser les fonctionnalités de [journalisation de l’utilisation](../deploy-use/log-analyze-usage.md) du service Azure Rights Management, qui peuvent fournir des informations indiquant par exemple qui a accédé à chaque fichier et quand, pour vous permettre de détecter un comportement suspect potentiel.<br /><br />Consultez la [liste des fonctionnalités](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) sur le site Azure Information Protection.|

### <a name="to-configure-the-custom-template"></a>Pour configurer le modèle personnalisé :

1.  Dans le portail Azure classique : créez un nouveau modèle personnalisé pour Azure Rights Management qui contient les valeurs et les paramètres suivants :

    -   Nom : **Accès privilégié**

    -   Droits : accordez les droits **Coauteur** au groupe **Accès privilégié** ayant accès aux e-mails

    -   Étendue : sélectionnez les groupes **Accès privilégié**, **Responsables de la conformité informatique** et **Administrateurs RMS** ayant accès aux e-mails.

    -   Accès hors connexion : **Le contenu n’est disponible qu’avec une connexion Internet**

2.  Publiez le nouveau modèle.

### <a name="to-protect-the-files-in-place"></a>Pour protéger les fichiers sur place

1.  Dans l’Explorateur de fichiers, accédez au premier dossier qui contient les fichiers à protéger :

    -   Si vous voulez protéger tous les fichiers du dossier, sélectionnez le dossier.

    -   Si vous voulez protéger seulement certains fichiers du dossier, sélectionnez les fichiers concernés.

2.  Cliquez avec le bouton droit, sélectionnez **Protéger avec RMS**, puis **Protéger sur place**.

3.  Sélectionnez **Accès privilégié**.

4.  Il se peut que vous soyez invité à fournir vos informations d'identification. Patientez jusqu’à ce que les fichiers soient protégés, puis cliquez sur **Fermer** une fois la page indiquant que **les fichiers ont été protégés** s’est affichée.

5.  Si vous avez plusieurs fichiers à protéger dans d’autres dossiers, répétez les étapes 1 à 4 pour chaque dossier.

Pour en savoir plus sur la protection des fichiers sur place, consultez [Protéger un fichier sur un appareil (protéger sur place) à l’aide de l’application de partage Rights Management](../rms-client/sharing-app-protect-in-place.md).

> [!TIP]
> Si le nombre de fichiers à protéger est trop important pour ce processus manuel, envisagez d’utiliser l’[outil Protection RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256) pour protéger en bloc les fichiers avec le modèle.

### <a name="to-monitor-and-if-necessary-revoke-access-to-the-files"></a>Pour surveiller et si nécessaire, révoquer l’accès aux fichiers

1.  Dans l’Explorateur de fichiers, cliquez avec le bouton droit sur le fichier protégé, sélectionnez **Protéger avec RMS**, puis **Suivre l’utilisation**.

2.  Si on vous le demande, connectez-vous pour accéder au site de suivi de document.

3.  Vérifiez qui a accédé au fichier et aux autres fichiers protégés en accordant une attention toute particulière aux échecs de tentatives lorsqu’elles indiquent un comportement suspect. Si cela vous semble approprié, vous pouvez révoquer l’accès à chaque fichier.

## <a name="user-documentation-instructions"></a>Instructions de la documentation utilisateur
Il n’existe aucune instruction spécifique destinée aux utilisateurs pour ce scénario, car ces fichiers ne nécessitent aucune action spéciale de leur part. Les fichiers ont été protégés par vous et seront surveillés par vos soins. Toutefois, vous devrez informer ces utilisateurs et vos canaux de support des fichiers qui sont protégés et comment cela peut limiter leur utilisation des documents. Par exemple, si un utilisateur autorisé ne dispose pas de connexion Internet, il ne pourra pas ouvrir le fichier.

En utilisant le modèle suivant, copiez et collez l’annonce dans une communication à destination de vos utilisateurs finaux, puis apportez les modifications suivantes :

1.  Fournissez les noms réels des fichiers ou utilisez une référence claire que les utilisateurs autorisés comprendront.

2.  Remplacez *&lt;coordonnées&gt;* par des instructions expliquant comment ces utilisateurs peuvent contacter le support technique ou le service informatique par le biais d’un canal de support par réaffectation en fonction de l’importance de ces documents. Par exemple, indiquez un numéro de téléphone joignable 24 heures sur 24 pour les appels du support technique très importants.

3.  Apportez les modifications supplémentaires que vous voulez éventuellement apporter à l’annonce, puis adressez-la à ces utilisateurs.

L’exemple de documentation illustre la façon dont cette annonce se présente aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### <a name="it-announcement-protecting-ltorganization-namegts-top-secret-documents"></a>Annonce de l’équipe informatique : Protection des documents ultraconfidentiels de &lt;nom de l’organisation&gt;
Un niveau de protection très élevé est désormais appliqué à ces fichiers de sorte qu’ils sont accessibles et modifiables uniquement par les &lt;utilisateurs avec accès restreint&gt;. Pour les protéger contre tout accès non autorisé, votre application demandera automatiquement une autorisation chaque fois que vous ouvrirez ces fichiers. Vous devez donc disposer d’une connexion Internet. Il se peut que vos informations d’identification vous soient demandées :

-   &lt;document ultraconfidentiel, type ou emplacement 1&gt;

-   &lt;document ultraconfidentiel, type ou emplacement 2&gt;

-   &lt;document ultraconfidentiel, type ou emplacement 3&gt;

**Vous avez besoin d'aide ?**

-   Si vous ne pouvez pas accéder à ces fichiers, ou si vous remarquez des modifications suspectes dans les fichiers &lt;action et coordonnées&gt;.

#### <a name="example-customized-user-documentation"></a>Exemple de documentation utilisateur personnalisée
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

##### <a name="it-announcement-protecting-vanarsdels-top-secret-documents"></a>Annonce de l’équipe informatique : Protection des documents ultraconfidentiels de VanArsdel
Un niveau de protection très élevé est désormais appliqué à ces fichiers de sorte que seules les personnes figurant sur la liste des destinataires de ce message peuvent y accéder et les modifier. Pour les protéger contre tout accès non autorisé, vos applications demanderont automatiquement une autorisation chaque fois que vous ouvrirez ces fichiers. Vous devez donc disposer d’une connexion Internet pour les ouvrir. Il se peut que vos informations d’identification vous soient demandées :

-   Spécifications de conception pour le nom de code « Mercure »

-   Spécifications de conception pour le nom de code « Jupiter »

-   Spécifications de conception pour le nom de code « Saturne »

-   Spécifications de conception pour le nom de code « Neptune »

**Vous avez besoin d'aide ?**

-   Si vous ne pouvez pas accéder à ces fichiers, ou si vous remarquez des modifications suspectes dans les fichiers, appelez le numéro du support technique disponible 24 heures sur 24 chargé de remonter les incidents qui vous a été envoyé par le département informatique dans un e-mail protégé.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


