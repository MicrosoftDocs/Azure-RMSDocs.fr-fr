---
# required metadata

title: Scénario - Configurer des dossiers de travail pour la protection permanente | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f189345-a69e-4bf5-8a45-eb0fe5bb542b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Scénario - Configurer des dossiers de travail pour la protection permanente

*S’applique à : Azure Rights Management, Office 365*

Ce scénario et la documentation utilisateur associée utilisent Azure Rights Management pour appliquer une protection permanente aux documents Office des [dossiers de travail](https://technet.microsoft.com/library/dn265974.aspx). Dossiers de travail utilise un service de rôle pour les serveurs de fichiers exécutant Windows Server qui offre aux utilisateurs une manière cohérente d’accéder à leurs fichiers professionnels depuis leurs PC et leurs appareils. Bien que Dossiers de travail fournisse son propre chiffrement pour protéger les fichiers, le déplacement de ces derniers en dehors de l’environnement Dossiers de travail entraîne la perte de cette protection. Les utilisateurs peuvent par exemple copier les fichiers synchronisés et les enregistrer sur un stockage qui n’est pas sous le contrôle de votre service informatique ou les fichiers sont envoyés par e-mail à d’autres personnes.

La protection supplémentaire fournie par Azure Rights Management permet d’éviter la perte accidentelle de données en empêchant la consultation des fichiers par des personnes extérieures à votre organisation. Pour ce faire, vous pouvez utiliser un des modèles de stratégie de droits par défaut intégrés. Toutefois, avant de déployer ce scénario, vérifiez si les utilisateurs peuvent avoir légitimement besoin de partager ces fichiers avec des personnes extérieures à l’organisation. Par exemple, après avoir travaillé sur un projet de liste de prix, un utilisateur envoie par e-mail la version finale aux clients d’une autre organisation. Lorsque vous utilisez le modèle Rights Management par défaut pour Dossiers de travail, le client de l’autre organisation ne peut pas lire ce document envoyé par e-mail. Vous pouvez satisfaire à cette exigence en créant un modèle personnalisé qui permet aux utilisateurs d’appliquer une nouvelle stratégie de droits au fichier, qui remplace la restriction d’origine relative à tous les employés à une restriction concernant les personnes indiquées dans l’e-mail.

> [!NOTE]
> Lorsque vous utilisez le modèle personnalisé documenté pour ce scénario, bien que les utilisateurs puissent partager intentionnellement des fichiers avec des personnes non définies dans le modèle, la protection supplémentaire appliquée avec Azure Rights Management fournit de nombreux avantages. Cette protection supplémentaire empêche la perte accidentelle de données si le contenu est déplacé en dehors de Dossiers de travail, dans la mesure où le contenu reste protégé contre les utilisateurs non autorisés, qu’il soit au repos ou transmis. Par exemple, un utilisateur perd un périphérique qui utilise Dossiers de travail, ou cet appareil est volé ou le contenu synchronisé vers et à partir de cet appareil est transféré sur une infrastructure sécurisée.
> 
> Si un utilisateur partage le contenu avec une personne d’une autre organisation, l’utilisation de la fonctionnalité de partage protégé de l’application de partage Rights Management permet à l’utilisateur de remplacer la protection d’origine par sa propre stratégie de protection. Par conséquent, le contenu reste protégé contre tout accès non autorisé et seules les personnes spécifiées par l’utilisateur peuvent accéder au contenu.

Vous pouvez appliquer cette protection permanente à tous les documents Office se trouvant dans les dossiers de travail des utilisateurs ou uniquement aux fichiers qui contiennent des données sensibles ou HBI (high-business-impact).

Les instructions conviennent pour l’ensemble des situations suivantes :

-   Les fichiers de Dossier de travail que vous souhaitez protéger à l’aide de la protection permanente sont des fichiers Office. Ces fichiers peuvent être protégés en mode natif par Azure Right Management et ne nécessitent pas de modification de leur extension de nom de fichier ou de workflow différent pour leur ouverture.

-   Vous souhaitez appliquer la protection permanente à tous les fichiers Office des dossiers de travail des utilisateurs ou à une sélection de fichiers identifiés à l’aide de l’infrastructure de classification des fichiers à partir du Gestionnaire de ressources du serveur de fichiers dans Windows Server.

-   Pour les fichiers qui doivent être partagés avec des personnes qui ne sont pas spécifiées dans le modèle de stratégie de droits (par exemple, les utilisateurs d’une autre organisation), les utilisateurs doivent appliquer une nouvelle stratégie de droits pour remplacer la protection de la stratégie de droits d’origine.

## Instructions de déploiement
![Instructions destinées aux administrateurs pour le déploiement rapide Azure RMS](../media/AzRMS_AdminBanner.png)

Vérifiez que les conditions suivantes sont réunies, puis suivez les instructions pour mener à bien les procédures associées avant de poursuivre avec la documentation utilisateur.

## Conditions requises pour ce scénario
Pour pouvoir appliquer les instructions de ce scénario, les conditions suivantes doivent être réunies :

|Configuration requise|Si vous avez besoin d'informations supplémentaires|
|---------------|--------------------------------|
|Azure Rights Management est activé|[Activation d'Azure Rights Management](https://technet.microsoft.com/library/jj658941.aspx)|
|Vous avez synchronisé vos comptes d'utilisateurs Active Directory locaux avec Azure Active Directory ou Office 365, y compris leurs adresses électroniques. Cela est nécessaire pour tous les utilisateurs utilisant Dossiers de travail.|[Préparation pour Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Une des causes suivantes :<br /><br />- Pour utiliser un modèle par défaut pour tous les utilisateurs qui ne leur permet pas d’appliquer une nouvelle stratégie de droits, consultez : Vous n’avez pas archivé le modèle par défaut **&lt;nom de l’organisation&gt; - Confidentiel**.<br /><br />- Pour utiliser un modèle personnalisé qui permet aux utilisateurs d’appliquer une nouvelle stratégie de droits : utilisez les instructions ci-après pour créer un modèle personnalisé|[Configuration de modèles personnalisés pour Azure Rights Management](https://technet.microsoft.com/library/dn642472.aspx)|
|Le connecteur Rights Management autorisé pour l’ordinateur Windows Server et configuré pour le rôle **Serveur ICF** est installé.|[Déploiement du connecteur Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|L'application de partage Rights Management est déployée sur les ordinateurs des utilisateurs qui exécutent Windows|[Déploiement automatique de l'application de partage Microsoft Rights Management](https://technet.microsoft.com/library/dn339003%28v=ws.10%29.aspx)|

### Configuration du modèle de stratégie de droits personnalisé afin que les utilisateurs puissent partager les fichiers de Dossiers de travail à l’extérieur de l’organisation

1.  Connectez-vous au portail classique Azure et accédez aux modèles Azure Rights Management.

2.  Copiez le modèle **&lt;nom de l’organisation&gt; - Confidentiel** et indiquez un nom et une description pour ce scénario Dossiers de travail. Nous vous suggérons ce qui suit :

    -   Nom : **Contenu protégé par Dossiers de travail**

    -   Description : **Ce contenu est protégé par Dossiers de travail et est limité aux employés de la société uniquement. Pour partager ce contenu avec des personnes extérieures à l’organisation, joignez le document à un e-mail et utilisez la fonction Partage protégé.**

3.  Sur la page **DROITS** :

    -   Modifiez les droits existants en remplaçant **Personnalisé** par **Copropriétaire**.

4.  Sur la page **CONFIGURER** :

    -   Assurez-vous que l’**ÉTAT** est défini sur **PUBLIER**

    -   Pour le **nom et la description**, supprimez les entrées des langues que vous n’utilisez pas. Pour les langues que vous utilisez, mettez à jour à jour le **NOM** et la **DESCRIPTION** afin qu’ils correspondent au nom et à la description que vous avez donnés à ce modèle, à l’aide de la langue spécifiée.

5.  Enregistrez le modèle.

### Configuration de Dossiers de travail pour appliquer une protection permanente à un fichier Office

1.  Implémentez Dossiers de travail pour vos utilisateurs afin de pouvoir synchroniser les fichiers enregistrés localement dans un dossier du serveur de fichiers, appelé *partage de synchronisation*. Le partage de synchronisation du serveur de fichiers ne doit pas être sur le même serveur exécutant le connecteur Rights Management.

    Cette solution requiert le service de rôle Dossiers de travail dans le Gestionnaire de serveur pour le rôle Services de fichiers et de stockage. Le serveur de fichiers doit exécuter une version minimale de Windows Server 2012 R2 et peut être situé sur site ou dans une machine virtuelle Azure. Pour plus d’informations sur Dossiers de travail, consultez [Vue d’ensemble des Dossiers de travail](https://technet.microsoft.com/library/dn265974.aspx).

    Pour obtenir des instructions de déploiement, consultez [Déploiement des Dossiers de travail](https://technet.microsoft.com/library/dn528861.aspx). Assurez-vous d’avoir sélectionné le chiffrement intégré (l’option **Chiffrer Dossiers de travail**), qui sera appliquée en plus du chiffrement Azure Rights Management. De plus :

    -   Lorsque vous liez le certificat SSL sur le serveur de synchronisation (étape 4) : utilisez la commande netsh (plutôt que la console de gestion IIS) pour lier le certificat à l’interface HTTPS du site Web par défaut.

    -   Pour éviter aux utilisateurs d’obtenir l’erreur d’installation de Dossiers de travail **Un problème s’est produit lors de l’application des stratégies de sécurité.** et l’obligation d’être un administrateur local sur leurs ordinateurs joints à un domaine : utilisez l’applet de commande [Set-SyncShare](https://technet.microsoft.com/library/dn296649%28v=wps.630%29.aspx) avec le paramètre PasswordAutolockExcludeDomain et spécifiez les noms de domaine sur lesquels ces ordinateurs se trouvent (par exemple, contoso.com).

2.  Pour terminer la configuration du connecteur Rights Management :

    1.  À l’aide du Gestionnaire de ressources du serveur de fichiers, créez une tâche de gestion de fichiers qui identifie le dossier de partage de synchronisation comme étant l’étendue.

    2.  Pour l’action, choisissez **Chiffrement RMS**, puis sélectionnez un modèle :

        -   Si vous n’avez pas créé de modèle personnalisé parce que vous ne souhaitez pas que les utilisateurs puissent partager des fichiers avec des personnes extérieures à l’organisation, sélectionnez le nom du modèle de **&lt;nom de l’organisation&gt; - Confidentiel**. Par exemple **VanArsdel, Ltd - Confidentiel**.

        -   Si vous avez créé un modèle personnalisé à l’aide des instructions précédentes, sélectionnez ce modèle. Par exemple : **Contenu protégé par Dossiers de travail**.

    3.  Définissez un calendrier qui permet de laisser suffisamment de temps pour que tous les fichiers Office soient chiffrés par Azure Rights Management et spécifiez l’option **Exécuter en continu sur les nouveaux fichiers**.

3.  Pour tester manuellement cette configuration, assurez-vous que le dossier contient des fichiers Office, puis utilisez l’option **Exécuter maintenant une tâche de gestion de fichiers**, puis sélectionnez **Attendre la fin de l’exécution de la tâche**.

    Attendez que la boîte de dialogue **Exécution de la tâche de gestion des fichiers** se ferme, puis consultez les résultats dans le rapport qui s'affiche automatiquement. Le champ **Fichiers** doit indiquer le nombre de fichiers figurant dans le dossier que vous avez choisi. Vérifiez que les fichiers figurant dans le dossier choisi sont à présent protégés par Azure Rights Management. Par exemple, ouvrez un fichier et vérifiez que la bannière d’informations située en haut du document affiche le nom et la description du modèle Rights Management.

4.  Si vous avez décidé de protéger les fichiers de manière sélective en utilisant l’infrastructure de classification des fichiers, configurez votre règle de classification et votre calendrier, puis modifiez la tâche de gestion de fichiers pour inclure cette propriété de classification en tant que condition.

## Instructions de la documentation utilisateur
Si les fichiers que vous protégez avec Azure Rights Management ne doivent pas nécessairement être partagés avec des personnes extérieures à votre organisation, il se peut que vous n’ayez aucune autre instruction à donner aux utilisateurs, que celles fournies pour l’utilisation de Dossiers de travail. Lorsque les utilisateurs ouvrent les fichiers protégés par Azure Rights Management et le modèle par défaut, les fichiers, s’ouvrent comme d’habitude dans Office, à la seule différence que les utilisateurs peuvent être invités à s’authentifier, et qu’ils voient une barre d’informations s’afficher en haut du document, les informant que le contenu contient des informations propriétaires destinées aux utilisateurs internes uniquement.

Si vous avez configuré le modèle personnalisé comme décrit pour ce scénario, les utilisateurs voient la description du modèle suivante s’afficher dans la barre d’informations : **Ce contenu est protégé par Dossiers de travail et est limité aux employés de la société uniquement. Pour partager ce contenu avec des personnes extérieures à l’organisation, joignez le document à un e-mail et utilisez la fonction Partage protégé.** Bien que cette description résume comment partager le fichier en dehors de l’organisation, les utilisateurs auront probablement besoin d’instructions détaillées relatives à la manière de procéder, notamment les premières fois. Pour prendre en charge ce scénario ultérieur, suivez les instructions de l’administrateur et de l’utilisateur final de [Scénario - Partage d’un fichier Office avec les utilisateurs d’une autre organisation](scenario-share-office-file-externally.md).

> [!TIP]
> Si vous avez décidé de ne pas utiliser le modèle personnalisé dans ces instructions, car vous ne souhaitez pas que les utilisateurs puissent partager ces fichiers en dehors de l’organisation sans supervision de l’équipe informatique, informez en votre support technique de sorte que, si l’exigence de partage est légitime, celle-ci puisse être autorisée par l’utilisation de tout mécanisme le mieux adapté à votre entreprise. Par exemple, une personne considérée comme [super utilisateur](https://technet.microsoft.com/library/mt147272.aspx) pourrait appliquer un nouveau modèle au contenu qui accorde des droits de contrôle complets à l’utilisateur qui en fait la demande afin qu’il puisse ensuite utiliser la fonction de partage protégé.
> 
> Après un certain temps, si vous découvrez l’existence de nombreuses demandes du même type, vous pouvez décider de définir votre propre modèle personnalisé pour ce scénario qui accorde l’option Copropriétaire uniquement à des utilisateurs spécifiques (tels que les responsables ou le support technique), tandis que les utilisateurs standard se voient attribuer l’option Coauteur ou tout autre [droit](https://technet.microsoft.com/library/mt169423.aspx) qui vous semble approprié.



<!--HONumber=May16_HO3-->


