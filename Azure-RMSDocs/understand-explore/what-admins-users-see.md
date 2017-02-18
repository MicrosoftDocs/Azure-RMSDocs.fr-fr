---
title: Ce que voient les utilisateurs et les administrateurs | Azure Information Protection
description: "Découvrez quelques exemples classiques illustrant comment les administrateurs et les utilisateurs voient et peuvent utiliser la technologie Azure Rights Management (Azure RMS) pour protéger des informations sensibles ou confidentielles."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e47a065737c950d4b616230c2915b4f2c8b6ee88
ms.openlocfilehash: d4dd6bed227f959b7791249af5f4103f25c27c6e


---


# <a name="azure-rms-in-action-what-administrators-and-users-see"></a>Azure RMS en action : ce que voient les utilisateurs et les administrateurs

>*S’applique à : Azure Information Protection, Office 365*

Cet article présente quelques exemples classiques illustrant comment les administrateurs et les utilisateurs voient et peuvent utiliser Azure Rights Management (Azure RMS) pour protéger des informations sensibles ou confidentielles.

> [!NOTE]
> Dans tous ces exemples où Azure RMS protège des données, le propriétaire du contenu continue à avoir un accès complet aux données (fichiers ou courrier électronique), même si la protection appliquée accorde des autorisations à un groupe dont le propriétaire n'était pas un membre, ou si la protection appliquée inclut une date d'expiration.
>
> De même, le service informatique peut toujours accéder aux données protégées sans restriction, en utilisant la fonctionnalité de super utilisateur de Rights Management, qui accorde un accès délégué aux utilisateurs autorisés ou aux services que vous spécifiez. En outre, le service informatique peut suivre et analyser l'utilisation des données protégées, par exemple, pour déterminer qui accède aux données et à quel moment.

Pour d’autres captures d’écran et vidéos qui montrent RMS en action, consultez [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de sécurité et de mobilité d’entreprise).

## <a name="activating-and-configuring-rights-management"></a>Activation et configuration de Rights Management
Bien que vous puissiez utiliser Windows PowerShell pour activer et configurer Azure RMS, cela est plus facile à partir du portail de gestion. Dès que le service est activé, vous disposez de deux modèles par défaut permettant aux administrateurs et aux utilisateurs d'appliquer rapidement et facilement la protection des informations aux fichiers. Vous pouvez également créer vos propres modèles personnalisés afin d'avoir accès à des paramètres et options supplémentaires.

![Captures d’écran des portails de gestion montrant l’option pour activer le service Azure Rights Management](../media/AzRMS_StoryboardActivate_small1.png)


**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 1 :** pour activer RMS, vous pouvez utiliser le Centre d’administration Office 365 (première image) ou le portail Azure Classic (deuxième image).<br /><br />Un simple clic permet d'activer RMS et un autre de confirmer l'activation. Ensuite, la protection des informations est activée pour les administrateurs et les utilisateurs au sein de votre organisation.

---

![Captures d’écran du portail Azure Classic montrant les deux modèles par défaut et le début de l’Assistant permettant de créer un nouveau modèle](../media/AzRMS_TemplatesPortal_small.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 2 :** après l’activation, deux modèles de stratégie des droits sont automatiquement disponibles pour votre organisation. Un modèle est en lecture seule (**Affichage confidentiel uniquement** est inclus dans son nom), tandis que l’autre est accessible en lecture et en modification (**Confidentiel**).

Lorsque ces modèles sont appliqués à des fichiers ou à des messages électroniques, ils restreignent l'accès aux utilisateurs de votre organisation. Il s'agit d'un moyen très simple et rapide d'empêcher une fuite de données de votre organisation vers des personnes extérieures à celle-ci.

> [!TIP]
> Ces modèles par défaut sont aisément reconnaissables, car ils ont pour préfixe le nom de votre organisation. Dans notre exemple, **VanArsdel, Ltd**.

Si vous ne voulez pas que les utilisateurs puissent voir ces modèles, ou si vous voulez créer vos propres modèles, vous pouvez spécifier cela via le portail Azure Classic. Comme le montre cette illustration, un assistant vous accompagne tout au long du processus de création d'un modèle personnalisé.

---

![Captures d’écran du portail Azure Classic montrant certaines options de configuration de modèle](../media/AzRMS_TemplatesSettings3.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 3 :** l’accès hors connexion, les paramètres d’expiration et la publication (affichage dans les applications qui prennent en charge Rights Management) immédiate ou non du modèle figurent parmi les paramètres de configuration disponibles si vous décidez de créer vos propres modèles.

---

![Captures d’écran de l’Explorateur de fichiers et de Word montrant les modèles que les utilisateurs peuvent sélectionner](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 4 :** suite à la publication de ces modèles, les utilisateurs peuvent sélectionner ceux-ci dans des applications telles que l’Explorateur de fichiers et Microsoft Word :

- Un utilisateur peut choisir le modèle par défaut, **VanArsdel, Ltd – Confidentiel**. Ensuite, seuls les employés de l'organisation VanArsdel peuvent ouvrir et utiliser ce document, même s'il est ultérieurement envoyé par courrier électronique à une personne extérieure à l'organisation, ou enregistré dans un emplacement public.

- Un utilisateur peut choisir le modèle personnalisé créé par l’administrateur, **Ventes et Marketing – Lecture et impression uniquement**. Ensuite, non seulement le fichier est protégé contre des personnes extérieures à l'organisation, mais son accès est également limité aux employés du département Ventes et Marketing. Par ailleurs, ces employés ne disposent pas de tous les droits sur le document, mais uniquement de ceux de le lire et de l'imprimer. Ils ne peuvent donc ni le modifier, ni en copier le contenu.

---

**Plus d’informations sur ce scénario :**

- Pour obtenir des instructions pas à pas, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md) et [Configuration de modèles personnalisés pour le service Azure Rights Management](../deploy-use/configure-custom-templates.md).

- Pour aider les utilisateurs à protéger des fichiers d’entreprise importants, consultez [Aider les utilisateurs à protéger des fichiers en utilisant le service Azure Rights Management](../deploy-use/help-users.md).

Vous pouvez voir ci-dessous quelques exemples de la façon dont les administrateurs peuvent appliquer les modèles afin de configurer automatiquement la protection des informations pour des fichiers et des courriers électroniques.

## <a name="automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure"></a>Protection automatique de fichiers sur des serveurs de fichiers exécutant Windows Server et l'infrastructure de classification des fichiers

Cet exemple montre comment vous pouvez utiliser Azure RMS pour protéger automatiquement des fichiers sur des serveurs de fichiers qui exécutent au moins Windows Server 2012, et sont configurés pour utiliser l'infrastructure de classification des fichiers.

Il existe de nombreuses façons d'appliquer des valeurs de classification à des fichiers. Par exemple, vous pouvez examiner le contenu des fichiers et appliquer en conséquence des classifications intégrées, telles que Confidentialité et Informations d'identification personnelle. Toutefois, dans cet exemple, un administrateur crée une classification personnalisée **Marketing** , qui est appliquée automatiquement à tous les documents utilisateur enregistrés dans le dossier **Marketing Promotions** . Bien que ce dossier soit protégé par des autorisations NTFS qui limitent l'accès aux membres du groupe Marketing, l'administrateur sait que ces autorisations peuvent être perdues si un membre de ce groupe déplace les fichiers ou les envoie par courrier électronique. Ensuite, des utilisateurs non autorisés pourraient accéder aux informations contenues dans les fichiers.

![Captures d’écran montrant l’installation et la configuration du connecteur Rights Management](../media/AzRMS_FCI_ConnectorSmall.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 1 :** l’administrateur installe et configure le connecteur RMS (Rights Management), qui joue le rôle de relais entre les serveurs locaux et Azure RMS.

---

![Captures d’écran des boîtes de dialogue permettant de configurer l’infrastructure de classification des fichiers sur Windows Server](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 2 :** sur le serveur de fichiers, l’administrateur configure les règles et tâches de classification pour que tous les fichiers utilisateur enregistrés dans le dossier **Marketing Promotions** soient automatiquement classés sous la catégorie **Marketing** et protégés par un chiffrement RMS.

Il sélectionne le modèle RMS personnalisé créé dans notre premier exemple, ce qui restreint l'accès aux membres des départements Ventes et Marketing : **Vente et Marketing - Lecture et impression uniquement**.

Par conséquent, tous les documents de ce dossier sont automatiquement associés à la classification Marketing, et protégés par le modèle RMS Ventes et Marketing.

---

![Captures d’écran d’un exemple d’e-mail avec une pièce jointe protégée, qui demande à l’utilisateur de s’authentifier pour ouvrir la pièce jointe](../media/AzRMS_FCI_EmailSmall.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 3 :** voici comment RMS permet d’éviter une fuite de données vers des personnes qui ne doivent pas avoir accès à des informations sensibles ou confidentielles :

- Janet, du département Marketing, envoie un rapport confidentiel extrait du dossier Marketing Promotions. Ce rapport décrivant de nouvelles fonctionnalités d'un produit et des plans de campagne publicitaire, est demandé par un collègue qui est actuellement en déplacement professionnel. Toutefois, Janet envoie accidentellement le rapport par courrier électronique à la mauvaise personne, n'ayant pas remarqué qu'elle a involontairement sélectionné un destinataire portant un nom similaire, mais travaillant pour une autre société.<br><br>
Le destinataire ne peut pas lire le rapport confidentiel, car il n'est pas membre du groupe Ventes et Marketing.

---

**Plus d’informations sur ce scénario :**

- Pour obtenir des instructions détaillées, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="automatically-protecting-emails-with-exchange-online-and-data-loss-prevention-policies"></a>Protection automatique des messages électroniques avec Exchange Online et des stratégies de prévention de perte de données

L'exemple précédent a montré comment protéger automatiquement des fichiers contenant des informations sensibles ou confidentielles, mais que se passe-t-il si ces informations ne figurent pas dans un fichier, mais dans un message électronique ? C'est là que les stratégies de prévention des pertes de données d'Exchange Online entrent en jeu, soit en demandant aux utilisateurs d'appliquer la protection des informations (en suivant les Conseils de stratégie), soit en les appliquant automatiquement à leur place (à l'aide de règles de transport).

Dans cet exemple, l'administrateur configure une stratégie permettant à l'organisation de rester en conformité avec les réglementations des États-Unis en matière de protection des informations d'identification personnelle, mais des règles peuvent également être définies en fonction d'autres règlements ou de prescriptions personnalisées que vous définissez.

![Exemples de captures d’écran montrant quelques-unes des options permettant de configurer la protection contre la perte de données Exchange Online](../media/AzRMS_DLPExample1.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 1 :** dans le Centre d’administration Exchange, le modèle Exchange nommé **Données relatives aux informations d’identification personnelles (PII) pour les États-Unis** permet de créer et de configurer une nouvelle stratégie DLP. Ce modèle recherche des informations telles que des numéros de sécurité sociale ou des numéros de permis de conduire dans les messages électroniques.

Les règles sont configurées de telle sorte que les messages électroniques contenant de telles informations, qui sont envoyés à l'extérieur de l'organisation, fassent automatiquement l'objet d'une protection des droits appliquée à l'aide d'un modèle RMS restreignant l'accès aux seuls employés de la société.

Ici, la règle est configurée pour utiliser un des modèles par défaut, **VanArsdel, Ltd – Confidentiel**, de notre premier exemple. Mais vous pouvez également voir comment le choix de modèles inclut tous les modèles personnalisés que vous avez créés, ainsi qu'une option **Ne pas transférer** spécifique d'Exchange.

> [!NOTE]
> Si les options de configuration qui s’affichent sont légèrement différentes de celles de l’image, vous devez d’abord sélectionner **Plus d’options** quand vous configurez la règle. Vous pouvez ensuite sélectionner **Modifier la sécurité du message** > **Appliquer la protection des droits**, puis sélectionnez le modèle RMS.

---

![Capture d’écran d’un exemple d’e-mail contenant un numéro de sécurité sociale](../media/AzRMS_DLPUnprotectedEmail_small.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 2 :** le responsable du recrutement écrit un e-mail qui contient le numéro de sécurité sociale d’un employé embauché récemment. Il envoie ce message électronique à Sherrie du département Ressources humaines.

---

![Capture d’écran d’un exemple d’e-mail maintenant protégé par Azure Rights Management car il va être envoyé à l’extérieur de l’organisation](../media/AzRMS_DLPProtectedEmail_small.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 3 :** si cet e-mail est envoyé ou transféré à quelqu’un extérieur à l’organisation, la règle DLP applique automatiquement la protection des droits.

Le message électronique est chiffré quand il quitte l'infrastructure de l'organisation, afin que le numéro de sécurité sociale soit illisible pendant le transit ou une fois dans la boîte de réception du destinataire. Le destinataire ne peut pas lire le message, sauf s'il est un employé de VanArsdel.

---

**Plus d’informations sur ce scénario :**

-   Pour plus d’informations sur le fonctionnement d’Azure RMS avec Exchange Online, consultez la section [Exchange Online et Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) dans [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

-   Pour obtenir des instructions détaillées en vue de configurer Exchange Online pour Azure RMS, consultez [Exchange Online : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#exchange-online-irm-configuration) dans [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

## <a name="automatically-protecting-files-with-sharepoint-online-and-protected-libraries"></a>Protection automatique de fichiers avec SharePoint Online et des bibliothèques protégées

Cela montre comment protéger facilement des documents lorsque vous utilisez SharePoint Online et des bibliothèques protégées.

Dans cet exemple, l'administrateur SharePoint de Contoso a créé une bibliothèque pour chaque département, qui permet de stocker et d'extraire de façon centralisée des documents à des fins de modification et de contrôle de version. Par exemple, il existe une bibliothèque pour le département Ventes, une autre pour le département Marketing, une troisième pour le département Ressources humaines, et ainsi de suite. Quand un nouveau document est chargé ou créé dans une de ces bibliothèques protégées, ce document hérite de la protection de la bibliothèque (sans qu'il faille sélectionner un modèle de stratégie de droits). Il est alors automatiquement protégé et le reste, même s'il est déplacé hors de la bibliothèque SharePoint.

![Capture d’écran de l’option SharePoint Online permettant d’activer IRM](../media/AzRMS_StoryboardSPO_small1.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 1 :** l’administrateur active Information Rights Management pour le site SharePoint.

---

![Capture d’écran de l’option SharePoint Online permettant de protéger une bibliothèque par IRM](../media/AzRMS_StoryboardSPO_small2.png)

**CE QUE LES ADMINISTRATEURS VOIENT À L’ÉTAPE 2 :** ensuite, il active Rights Management pour une bibliothèque. Bien qu'il existe des options supplémentaires, ce simple paramètre est souvent suffisant.

Désormais, quand des documents sont téléchargés à partir de cette bibliothèque, ils sont automatiquement protégés par Rights Management et héritent de la protection configurée pour la bibliothèque.

---

![Capture d’écran d’un document téléchargé à partir d’une bibliothèque SharePoint Online protégée, avec la bannière d’informations indiquant que celui-ci est protégé](../media/AzRMS_StoryboardSPO_small3.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 3 :** quand une personne du département des ventes extrait ce rapport de la bibliothèque, la bannière d’informations affichée en haut du rapport lui indique clairement qu’il s’agit d’un document protégé dont l’accès est restreint.

Le document reste protégé, même si l'utilisateur le renomme, l'enregistre ailleurs ou le partage par courrier électronique. Quel que soit le nom du fichier, l'emplacement où il est stocké, ou l'adresse à laquelle il a été envoyé par courrier électronique, seuls les membres du département des ventes peuvent le lire.

---

**Plus d’informations sur ce scénario :**

-   Pour plus d’informations sur le fonctionnement d’Azure RMS avec SharePoint, consultez la section [SharePoint Online et SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) dans [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

-   Pour obtenir des instructions détaillées en vue de configurer SharePoint pour Azure RMS, consultez [SharePoint Online et OneDrive Entreprise : configuration de la gestion des droits relatifs à l’information](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dans [Configuration d’applications pour Azure Rights Management](../deploy-use/configure-applications.md).

## <a name="users-safely-share-attachments-with-mobile-users"></a>Partage en toute sécurité de pièces jointes avec des utilisateurs mobiles

Les exemples précédents ont montré comment les administrateurs peuvent appliquer automatiquement une protection des informations à des données sensibles et confidentielles. Toutefois, dans certains cas, les utilisateurs doivent appliquer cette protection eux-mêmes. Par exemple, s'ils collaborent avec des partenaires d'une autre organisation, ils ont besoin d'autorisations ou de paramètres personnalisés qui ne sont pas définis dans les modèles, dans des situations spécifiques non couvertes par les exemples précédents. Dans ces situations, les utilisateurs peuvent appliquer les modèles RMS eux-mêmes, ou configurer des autorisations personnalisées.

Cet exemple montre comment un utilisateur peut aisément partager un document avec une personne d’une autre société avec laquelle il collabore, tout en étant en mesure de protéger le document avec la certitude que le destinataire pourra le lire, même sur un appareil mobile. Ce scénario utilise l'application de partage Rights Management, que pouvez déployer automatiquement sur des ordinateurs Windows au sein de votre organisation. Les utilisateurs peuvent également installer l'application eux-mêmes.

Dans cet exemple, Alice, de Contoso, envoie par courrier électronique un document Word confidentiel qu'elle adresse à Bob, de Fabrikam. Celui-ci lit le document sur son iPad, mais il pourrait tout aussi bien le lire sur un iPhone, une tablette ou un téléphone Android, un ordinateur Mac, ainsi qu'un téléphone ou un ordinateur Windows.

![Capture d’écran montrant un exemple d’e-mail avec une pièce jointe et la boîte de dialogue Partager le fichier protégé dans l’application de partage Rights Management](../media/AzRMS_StoryboardEmail_small1.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 1 :** sur son PC Windows, Alice crée un e-mail standard auquel elle joint un document.

Quand elle clique sur **Partage protégé** dans le ruban, la boîte de dialogue **Partager le fichier protégé** de l'application de partage RMS s'ouvre.

Souhaitant que Bob puisse afficher et modifier le document, mais pas le copier ou l'imprimer, Alice active l'option **Réviseur – Affichage et modification**. Elle souhaite également recevoir un courrier électronique quand quelqu'un tente d'ouvrir le document, et avoir la possibilité de révoquer celui-ci ultérieurement si nécessaire en sachant que la révocation prendra effet immédiatement.

---

![Capture d’écran montrant l’e-mail d’un utilisateur sur un iPad, avec le message, les pièces jointes et les instructions](../media/AzRMS_StoryboardEmail_small2.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 2 :** Bob voit l’e-mail sur son iPad.

En plus de la pièce jointe, le message d'Alice contient des instructions qu'il suit pour s'inscrire et installer l'application de partage RMS sur son iPad.

---

![Capture d’écran de l’utilisateur lisant la pièce jointe protégée sur l’iPad](../media/AzRMS_StoryboardEmail_small3.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 3 :** Bob peut à présent ouvrir la pièce jointe. Il est d'abord invité à se connecter pour confirmer qu'il est bien le destinataire souhaité.

Lorsque Bob consulte le document, il voit également les informations d'accès restreint qui lui indiquent qu'il peut afficher et modifier le document, mais pas le copier ou l'imprimer.

---

![Capture d’écran d’un exemple d’e-mail de confirmation de l’utilisateur expéditeur](../media/AzRMS_StoryboardEmail_small4.png)

**CE QUE LES UTILISATEURS VOIENT À L’ÉTAPE 4 :** Alice reçoit un e-mail lui indiquant que Bob a ouvert avec succès le document qu’elle a envoyé, ainsi que le moment auquel il y a accédé.

Si Bob transfère le message électronique avec la pièce jointe, ou l'enregistre dans un emplacement où d'autres personnes peuvent y accéder, ou si le message est intercepté sur le réseau, personne d'autre que lui n'est en mesure de lire le document.

---

**Plus d’informations sur ce scénario :**

- Pour obtenir des instructions détaillées, consultez [Protéger un fichier que vous partagez par e-mail](../rms-client/sharing-app-protect-by-email.md) et [Afficher et utiliser des fichiers qui ont été protégés](../rms-client/sharing-app-view-use-files.md) dans le [Guide d’utilisation de l’application de partage Rights Management](../rms-client/sharing-app-user-guide.md).

- Le [Didacticiel de démarrage rapide pour Azure Rights Management](../get-started/quick-start-tutorial.md) inclut des instructions détaillées pour ce scénario.

## <a name="next-steps"></a>Étapes suivantes

Après avoir vu ces quelques exemples de ce qu'Azure RMS peut faire, peut-être souhaitez-vous savoir comment il le fait. Pour obtenir des informations techniques sur le fonctionnement d’Azure RMS, consultez [Fonctionnement d’Azure RMS](how-does-it-work.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


