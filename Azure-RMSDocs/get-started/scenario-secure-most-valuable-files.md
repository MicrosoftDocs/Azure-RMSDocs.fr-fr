---
title: "Scénario - Sécuriser vos fichiers les plus précieux | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 95f1844a-612c-4e67-bbe6-4b6b92295221
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 332e102cb27854314b93a71bfeae82a95c9a7812
ms.openlocfilehash: d4325fb8a0b27d0a8d4fd7451b9d11d10153ed8d


---

# Scénario - Sécuriser vos fichiers les plus précieux

*S’applique à : Azure Rights Management, Office 365*

Ce scénario et la documentation utilisateur associé utilisent Azure Rights Management pour protéger de manière manuelle et personnalisée un certain nombre de fichiers que vous considérez comme les plus précieux, qui assure le plus haut niveau de protection qui soit contre tout accès non autorisé. Il s’agit généralement de fichiers auxquels seules quelques personnes doivent pouvoir accéder. Par exemple, les instructions relatives à la recette d’un produit alimentaire distinctif de votre société ou des plans de reprise qui ne doivent pas être rendus publics avant une date définie.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Vous avez identifié l’ensemble de fichiers à protéger.

-   Les fichiers sont dans un des formats de fichier Office prenant en charge Rights Management. Si les formats de fichiers sont différents (par exemple, s’il s’agit de fichiers de CAO), vérifiez qu’ils prennent en charge Azure RMS et que vous déployez des applications prenant en charge Azure RMS de manière native. Pour plus d’informations, consultez [Mode de prise en charge d’Azure Rights Management par les applications](https://technet.microsoft.com/library/jj585004.aspx).

-   Les fichiers contiennent des informations hautement confidentielles et sensibles qui doivent être accessibles à quelques personnes uniquement.

-   La nécessité de disposer d’une connexion Internet pour autoriser chaque accès à un fichier est un compromis acceptable pour ces personnes, dans la mesure où cela garantit une meilleure sécurité.

-   Ces utilisateurs n’ont pas besoin de partager ces informations avec d’autres personnes. Ils peuvent toutefois modifier ces informations et les enregistrer.

-   L’administrateur doit être en mesure de savoir qui accède aux fichiers et à quel moment et de bloquer l’accès si nécessaire.

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont réunies, puis suivez les instructions pour mener à bien les procédures associées avant de poursuivre avec la documentation utilisateur.

## Conditions requises pour ce scénario
Pour ce scénario, les éléments suivants doivent être en place :

|Configuration requise|Si vous avez besoin d’informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory.<br /><br />- Un groupe nommé **Accès privilégié** ayant accès aux e-mails, qui contient les personnes devant avoir accès à ces documents hautement confidentiels<br /><br />- Un groupe nommé **Responsables de la conformité informatique** ayant accès aux e-mails, qui contient les personnes dont le travail inclut eDiscovery, la surveillance et l’audit<br /><br />- Un groupe nommé **Administrateurs RMS** et tous les administrateurs chargés de configurer Azure RMS sont membres de ce groupe|[Préparation pour Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management est activé|[Activation d'Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Vous avez configuré un modèle personnalisé comme décrit ci-après|[Configuration de modèles personnalisés pour Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|L’application de partage Rights Management est déployée sur votre ordinateur Windows afin que vous puissiez protéger ces fichiers sur place, comme décrit dans la section suivante|[Télécharger et installer l'application de partage Rights Management](https://technet.microsoft.com/library/dn574734%28v=ws.10%29.aspx)|
|Les utilisateurs autorisés ont une version minimale d’Office 2013|Si les utilisateurs disposent d’Office 2010, ils doivent également installer l’application de partage Rights Management.|
|Votre abonnement Azure RMS inclut le suivi de document|Si votre abonnement à Azure RMS n’inclut pas le suivi et la révocation des documents, vous ne pourrez pas utiliser le site de suivi de document pour voir qui accède à ces documents et révoquer l’accès si nécessaire. Dans ce cas, souscrivez un abonnement prenant en charge le suivi des documents ou acceptez cette restriction. Vous pouvez également envisager d’utiliser les fonctionnalités de [journalisation de l’utilisation](https://technet.microsoft.com/library/dn529121.aspx) d’Azure RMS, qui peuvent fournir des informations, indiquant par exemple qui a accédé à chaque fichier et à quel moment, pour vous permettre de détecter un comportement suspect potentiel.<br /><br />Pour vérifier la prise en charge de votre abonnement : [Comparaison des offres Rights Management Services (RMS)](https://technet.microsoft.com/dn858608)|

### Pour configurer le modèle personnalisé :

1.  Dans le portail Azure classique : créez un nouveau modèle personnalisé pour Azure Rights Management qui contient les valeurs et les paramètres suivants :

    -   Nom : **Accès privilégié**

    -   Droits : accordez les droits **Coauteur** au groupe **Accès privilégié** ayant accès aux e-mails

    -   Étendue : sélectionnez les groupes **Accès privilégié**, **Responsables de la conformité informatique** et **Administrateurs RMS** ayant accès aux e-mails.

    -   Accès hors connexion : **Le contenu n’est disponible qu’avec une connexion Internet**

2.  Publiez le nouveau modèle.

### Pour protéger les fichiers sur place

1.  Dans l’Explorateur de fichiers, accédez au premier dossier qui contient les fichiers à protéger :

    -   Si vous voulez protéger tous les fichiers du dossier, sélectionnez le dossier.

    -   Si vous voulez protéger seulement certains fichiers du dossier, sélectionnez les fichiers concernés.

2.  Cliquez avec le bouton droit, sélectionnez **Protéger avec RMS**, puis **Protéger sur place**.

3.  Sélectionnez **Accès privilégié**.

4.  Il se peut que vous soyez invité à fournir vos informations d'identification. Patientez jusqu’à ce que les fichiers soient protégés, puis cliquez sur **Fermer** une fois la page indiquant que **les fichiers ont été protégés** s’est affichée.

5.  Si vous avez plusieurs fichiers à protéger dans d’autres dossiers, répétez les étapes 1 à 4 pour chaque dossier.

Pour en savoir plus sur la protection des fichiers sur place, consultez [Protéger un fichier sur un appareil (protéger sur place) à l’aide de l’application de partage Rights Management](https://technet.microsoft.com/library/dn574733%28v=ws.10%29.aspx).

> [!TIP]
> Si le nombre de fichiers à protéger est trop important pour ce processus manuel, envisagez d’utiliser l’[outil Protection RMS](https://www.microsoft.com/en-us/download/details.aspx?id=47256) pour protéger en bloc les fichiers avec le modèle.

### Pour surveiller et si nécessaire, révoquer l’accès aux fichiers

1.  Dans l’Explorateur de fichiers, cliquez avec le bouton droit sur le fichier protégé, sélectionnez **Protéger avec RMS**, puis **Suivre l’utilisation**.

2.  Si on vous le demande, connectez-vous pour accéder au site de suivi de document.

3.  Vérifiez qui a accédé au fichier et aux autres fichiers protégés en accordant une attention toute particulière aux échecs de tentatives lorsqu’elles indiquent un comportement suspect. Si cela vous semble approprié, vous pouvez révoquer l’accès à chaque fichier.

## Instructions de la documentation utilisateur
Il n’existe aucune instruction spécifique destinée aux utilisateurs pour ce scénario, car ces fichiers ne nécessitent aucune action spéciale de leur part. Les fichiers ont été protégés par vous et seront surveillés par vos soins. Toutefois, vous devrez informer ces utilisateurs et vos canaux de support des fichiers qui sont protégés et comment cela peut limiter leur utilisation des documents. Par exemple, si un utilisateur autorisé ne dispose pas de connexion Internet, il ne pourra pas ouvrir le fichier.

En utilisant le modèle suivant, copiez et collez l’annonce dans une communication à destination de vos utilisateurs finaux, puis apportez les modifications suivantes :

1.  Fournissez les noms réels des fichiers ou utilisez une référence claire que les utilisateurs autorisés comprendront.

2.  Remplacez *&lt;coordonnées&gt;* par des instructions expliquant comment ces utilisateurs peuvent contacter le support technique ou le service informatique par le biais d’un canal de support par réaffectation en fonction de l’importance de ces documents. Par exemple, indiquez un numéro de téléphone joignable 24 heures sur 24 pour les appels du support technique très importants.

3.  Apportez les modifications supplémentaires que vous voulez éventuellement apporter à l’annonce, puis adressez-la à ces utilisateurs.

L’exemple de documentation illustre la façon dont cette annonce se présente aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

### Annonce de l’équipe informatique : Protection des documents ultraconfidentiels de &lt;nom de l’organisation&gt;
Un niveau de protection très élevé est désormais appliqué à ces fichiers de sorte qu’ils sont accessibles et modifiables uniquement par les &lt;utilisateurs avec accès restreint&gt;. Pour les protéger contre tout accès non autorisé, votre application demandera automatiquement une autorisation chaque fois que vous ouvrirez ces fichiers. Vous devez donc disposer d’une connexion Internet. Il se peut que vos informations d’identification vous soient demandées :

-   &lt;document ultraconfidentiel, type ou emplacement 1&gt;

-   &lt;document ultraconfidentiel, type ou emplacement 2&gt;

-   &lt;document ultraconfidentiel, type ou emplacement 3&gt;

**Vous avez besoin d'aide ?**

-   Si vous ne pouvez pas accéder à ces fichiers, ou si vous remarquez des modifications suspectes dans les fichiers &lt;action et coordonnées&gt;.

#### Exemple de documentation utilisateur personnalisée
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

##### Annonce de l’équipe informatique : Protection des documents ultraconfidentiels de VanArsdel
Un niveau de protection très élevé est désormais appliqué à ces fichiers de sorte que seules les personnes figurant sur la liste des destinataires de ce message peuvent y accéder et les modifier. Pour les protéger contre tout accès non autorisé, vos applications demanderont automatiquement une autorisation chaque fois que vous ouvrirez ces fichiers. Vous devez donc disposer d’une connexion Internet pour les ouvrir. Il se peut que vos informations d’identification vous soient demandées :

-   Spécifications de conception pour le nom de code « Mercure »

-   Spécifications de conception pour le nom de code « Jupiter »

-   Spécifications de conception pour le nom de code « Saturne »

-   Spécifications de conception pour le nom de code « Neptune »

**Vous avez besoin d'aide ?**

-   Si vous ne pouvez pas accéder à ces fichiers, ou si vous remarquez des modifications suspectes dans les fichiers, appelez le numéro du support technique disponible 24 heures sur 24 chargé de remonter les incidents qui vous a été envoyé par le département informatique dans un e-mail protégé.




<!--HONumber=Jun16_HO4-->


