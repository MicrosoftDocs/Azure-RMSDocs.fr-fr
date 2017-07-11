---
title: "Scénario AIP : Contrôler des documents stockés dans SharePoint"
description: "Ce scénario et la documentation utilisateur associée s’appuient sur la protection Azure Rights Management pour s’assurer que les documents Office stockés dans SharePoint restent sous votre contrôle en utilisant des bibliothèques protégées."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3815ed1fdfd7b5201dfec258e6c20364c0397a8b
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="scenario---retain-control-of-documents-stored-in-sharepoint" class="xliff"></a>

# Scenario : garder le contrôle des documents stockés dans SharePoint

>*S’applique à : Azure Information Protection, Office 365*

Ce scénario et la documentation utilisateur associée s’appuient sur la technologie Azure Rights Management d’Azure Information Protection pour s’assurer que les documents Office stockés dans SharePoint restent sous votre contrôle en utilisant des bibliothèques protégées. Par exemple, les documents sont automatiquement protégés contre les fuites accidentelles ou volontaires par les utilisateurs et vous pouvez bloquer l’accès au contenu même après qu’il a été téléchargé ou synchronisé. Les fichiers que vous voulez protéger peuvent être destinés à des actions de collaboration interne sur des documents de conception ou des plans ou pour d’autres livrables. Quand vous configurez des bibliothèques protégées pour SharePoint, les fichiers Office qui y sont stockés sont protégés par Azure Rights Management.

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Les employés partagent et collaborent à partir de documents Office qui se trouvent dans une bibliothèque SharePoint.

-   Les employés n’ont pas besoin de définir ou de modifier les autorisations qu’un administrateur définit au niveau de la bibliothèque.

-   Les employés n’ont pas besoin de partager ces documents avec des personnes extérieures à votre organisation.

<a id="deployment-instructions" class="xliff"></a>

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont remplies et que les procédures associées sont en place avant de poursuivre avec la documentation utilisateur.

<a id="requirements-for-this-scenario" class="xliff"></a>

## Conditions requises pour ce scénario
Pour pouvoir appliquer ce scénario, les éléments suivants doivent être en place :

|Condition requise|Si vous avez besoin d'informations supplémentaires|
|---------------|--------------------------------|
|Vous avez préparé des comptes et des groupes pour Office 365 ou Azure Active Directory|[Préparation d’Azure Information Protection](../plan-design/prepare.md)|
|Azure Rights Management est activé|[Activation d’Azure Rights Management](../deploy-use/activate-service.md)|
|Si vous utilisez SharePoint Server : Déployez le connecteur RMS et configurez-le pour SharePoint|[Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md)|
|Configurer des autorisations pour le site SharePoint à protéger|[Gérer les autorisations pour une liste, une bibliothèque, un dossier, un document ou un élément de liste](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[Activation de la gestion des droits relatifs à l'information pour une liste ou une bibliothèque](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|Configurez SharePoint pour IRM et les bibliothèques protégées|[Configuration de la gestion des droits relatifs à l'information dans le centre d'administration SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Activation de la gestion des droits relatifs à l'information pour une liste ou une bibliothèque](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

<a id="to-configure-the-sharepoint-library-for-irm-settings" class="xliff"></a>

### Pour configurer la bibliothèque SharePoint pour les paramètres IRM

1.  Après avoir configuré SharePoint pour une utilisation du service IRM, accédez à la bibliothèque SharePoint à protéger avec Azure RMS. Dans la page **Paramètres** &gt; **Information Rights Management (IRM)** du site, après avoir sélectionné **Restreindre les autorisations sur cette bibliothèque lors du téléchargement** et spécifié un titre de stratégie pour les administrateurs et une description de la stratégie pour les utilisateurs, cliquez sur **AFFICHER LES OPTIONS**.

2.  Sélectionnez l’option suivante :

    -   **Interdire aux utilisateurs de télécharger des documents qui ne prennent pas en charge IRM**

    -   Facultatif : **Autoriser la protection de groupe. Groupe par défaut**, puis spécifiez le nom d’un groupe supplémentaire dont vous pourriez avoir besoin pour collaborer sur les documents stockés dans cette bibliothèque, mais en dehors de SharePoint. Par exemple, le groupe Ventes dispose d’autorisations de modification sur le site et un membre de ce groupe télécharge un document, l’enregistre sur disque et l’envoie par e-mail à une collègue. Le collaborateur aura uniquement accès au document (avec droits de modification) s’il est membre du groupe désigné.

        Sans cette option, seuls les utilisateurs qui ont accès à la bibliothèque SharePoint pourront collaborer sur ces documents et seulement en téléchargeant les documents directement à partir de SharePoint. Cette restriction convient dans de nombreux cas.

<a id="user-documentation-instructions" class="xliff"></a>

## Instructions de la documentation utilisateur
Il n’existe aucune instruction de procédure à communiquer aux utilisateurs pour ce scénario, car les bibliothèques protégées ne nécessitent aucune action spéciale de leur part. Les documents sont automatiquement protégés lors du téléchargement en fonction des autorisations définies par un administrateur SharePoint pour le site. Cependant, informez les utilisateurs de cette modification pour qu’ils sachent à quoi s’attendre et portez à la connaissance de votre support technique les bibliothèques qui sont protégées et en quoi cela peut limiter l’utilisation des documents. Par exemple, en raison des limitations actuelles, ces documents peuvent être affichés, mais pas modifiés avec des appareils mobiles. Si vous avez configuré la protection de groupe, portez à la connaissance des utilisateurs les groupes qui peuvent accéder et modifier des documents en dehors de SharePoint.

En utilisant le modèle suivant, copiez et collez l’annonce dans une communication à destination de vos utilisateurs finaux, puis apportez ces modifications en les adaptant à votre environnement :

1.  Remplacez chaque instance de *&lt;nom de la bibliothèque SharePoint&gt;* par le nom et le lien de la bibliothèque SharePoint que vous avez configurée pour Azure Rights Management. Si cette communication concerne plusieurs bibliothèques protégées, modifiez les instructions en conséquence.

2.  Si vous avez configuré l’option **Autoriser la protection de groupe. Groupe par défaut**, remplacez *&lt;nom du groupe&gt;* par le nom du groupe que vous avez configuré et indiquez dans la zone prévue à cet effet la &lt;raison pour laquelle ce groupe dispose des autorisations d’accès qui lui permettent de collaborer sur les fichiers, mais pas en utilisant la bibliothèque SharePoint&gt;. Si vous n’avez pas configuré cette option, supprimez cette phrase.

3.  Remplacez *&lt;coordonnées&gt;* par des instructions indiquant comment contacter le support technique, telles qu’un lien vers un site web, une adresse e-mail ou un numéro de téléphone.

4.  Apportez les modifications supplémentaires que vous voulez éventuellement apporter à l’annonce, puis adressez-la à ces utilisateurs.

L’exemple de documentation illustre la façon dont cette annonce se présente aux utilisateurs une fois vos personnalisations effectuées.

![Modèle de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_UsersBanner.png)

<a id="it-announcement-changes-to-the-ltname-of-sharepoint-librarygt-site" class="xliff"></a>

### Annonce de l’équipe informatique : Modifications apportées au site &lt;nom de la bibliothèque SharePoint&gt;
Le site SharePoint **&lt;nom de la bibliothèque SharePoint&gt;** est maintenant configuré pour une collaboration sécurisée. Désormais, seuls les membres du groupe &lt;nom du groupe&gt; peuvent ouvrir ces documents à partir de ce site, même si vous les enregistrez localement ou les envoyez par e-mail à quelqu’un d’autre. L’exception est que vous pouvez partager les documents avec les membres du groupe &lt;nom du groupe&gt; après les avoir téléchargés, &lt;raison pour laquelle ce groupe dispose des autorisations d’accès qui lui permettent de collaborer sur les fichiers, mais pas en utilisant la bibliothèque SharePoint&gt;. Lorsque vous modifiez un fichier, une bannière d’information de couleur jaune s’affiche en haut du document, indiquant qu’il est protégé et qui peut y accéder.

Cette modification permet de conserver les données confidentielles de notre entreprise hors de portée de personnes qui ne sont pas supposées y avoir accès. Si vous utilisez un appareil mobile pour accéder à ces documents protégés, vous pouvez les consulter, mais vous devez utiliser un appareil de bureau pour les modifier.

Vous ne pouvez pas charger des documents sur le site &lt;nom du site SharePoint&gt; s’ils ne prennent pas en charge la collaboration sécurisée.

**Vous avez besoin d'aide ?**

-   Contactez le support technique : &lt;coordonnées&gt;

<a id="example-user-documentation" class="xliff"></a>

### Exemple de documentation utilisateur
![Exemple de documentation utilisateur pour le déploiement rapide Azure RMS](../media/AzRMS_ExampleBanner.png)

<a id="it-announcement-changes-to-the-sales-forecasts-and-reports-site" class="xliff"></a>

#### Annonce de l’équipe informatique : Modifications du site de rapports et de prévisions de ventes
Le site SharePoint **Rapports et prévisions de ventes**est désormais configuré pour une collaboration sécurisée. À présent, seuls les membres de notre équipe Vente et Marketing peuvent ouvrir les documents provenant de ce site, même si vous les enregistrez localement ou les envoyez par e-mail à quelqu’un d’autre. L’exception est qu’après avoir téléchargé des documents, vous pouvez les partager avec des membres de l’équipe Finances afin qu’ils puissent en extraire les chiffres prévisionnels mensuels. Lorsque vous modifiez un fichier, une bannière d’information de couleur jaune s’affiche en haut du document, indiquant qu’il est protégé et qui peut y accéder.

Cette modification permet de conserver les données confidentielles de notre entreprise hors de portée de personnes qui ne sont pas supposées y avoir accès. Si vous utilisez un appareil mobile pour accéder à ces documents protégés, vous pouvez les consulter, mais vous devez utiliser un appareil de bureau pour les modifier.

Vous ne pouvez pas charger des documents sur le site Rapports et prévisions de ventes si celui-ci ne prend pas en charge la collaboration sécurisée.

**Vous avez besoin d'aide ?**

-   Contactez le support technique : helpdesk@vanarsdelltd.com

[!INCLUDE[Commenting house rules](../includes/houserules.md)]