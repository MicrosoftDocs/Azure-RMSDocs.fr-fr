---
# required metadata

title: Créer, configurer et publier un modèle personnalisé | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d6e9aa0c-1694-4a53-8898-4939f31cc13f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Créer, configurer et publier un modèle personnalisé

Vous créez et gérez des modèles personnalisés dans le portail Azure Classic. Pour cela, vous pouvez accéder directement au portail Azure Classic ou vous connecter au Centre d’administration Office 365, puis choisir **Fonctionnalités avancées** de Rights Management. Vous êtes alors redirigé vers le portail Azure Classic.

Utilisez les procédures suivantes pour créer, configurer et publier des modèles personnalisés pour la Gestion des droits.

## Pour créer un modèle personnalisé

1.  Selon que vous vous connectez au Centre d’administration Office 365 ou au portail Azure Classic, procédez de l’une des manières suivantes :

    -   Depuis le [centre d’administration Office 365](https://portal.office.com/):

        1.  Dans le panneau de gauche, cliquez sur **paramètres de service**.

        2.  À partir de la page **paramètres de service** , cliquez sur **rights management**.

        3.  Dans la section **Protéger vos informations** , cliquez sur **Gérer**.

        4.  Dans la section **Rights Management** , cliquez sur **fonctionnalités avancées**.

            > [!NOTE]
            > Si vous n’avez pas activé Rights Management, cliquez d’abord sur **activer** et confirmez votre action. Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md).
            > 
            > Si vous n’avez pas encore cliqué sur **Fonctionnalités avancées**, une fois Rights Management activé, suivez les instructions à l’écran pour obtenir un abonnement Azure gratuit, nécessaire pour accéder au portail Azure Classic.

            Quand vous cliquez sur **Fonctionnalités avancées**, le portail Azure Classic s’ouvre et vous permet de gérer **RIGHTS MANAGEMENT** pour Azure Active Directory dans votre organisation.

    -   À partir du [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081) :

        1.  Dans le volet gauche, cliquez sur **Active Directory**.

        2.  À partir du **répertoire actif** , cliquez sur **RIGHTS MANAGEMENT**.

        3.  Sélectionnez l'annuaire concerné par la Gestion des droits.

        4.  Si vous n’avez pas encore activé Rights Management, cliquez sur **ACTIVER** et confirmez votre action.

            > [!NOTE]
            > Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md).

2.  Créer un modèle :

    -   Dans le portail Azure Classic, dans la page de démarrage rapide **Prise en main de Rights Management**, cliquez sur **Créer un modèle de stratégie de droits**.

        Si cette page ne s’affiche pas immédiatement après que vous avez suivi les instructions pour Office 365, utilisez les instructions de navigation fournies ci-dessus pour le portail Azure Classic.

3.  Sur la page **Ajouter un nouveau modèle de stratégie de droits** , choisissez la langue dans laquelle vous allez taper le nom et la description du modèle en fonction de vos utilisateurs (vous pourrez ajouter d’autres langues ultérieurement). Tapez ensuite un nom unique et une description, puis cliquez sur le bouton Terminé.

Depuis la page de démarrage rapide **Prise en main de Rights Management** , cliquez sur **Gérer vos modèles de stratégie de droits**. Le modèle que vous venez de créer a été ajouté à la liste des modèles. Son état est **Archivé**. À ce stade, le modèle est créé mais pas configuré. Les utilisateurs ne peuvent pas le voir.

## Pour configurer et publier un modèle personnalisé

1.  Sélectionnez votre modèle nouvellement créé dans la page **MODÈLES** du portail Azure Classic.

2.  Depuis la page de démarrage rapide **Votre modèle a été ajouté !** , cliquez sur **Mise en route** à l’étape 1, **Configurer des droits pour les utilisateurs et les groupes** , puis cliquez sur **PRENDRE EN MAIN MAINTENANT** ou **AJOUTER**et sélectionnez les utilisateurs et groupes autorisés à utiliser le contenu protégé par le nouveau modèle.

    > [!NOTE]
    > Les utilisateurs ou groupes que vous sélectionnez doivent avoir une adresse de messagerie. Dans un environnement de production, ce sera presque toujours le cas, mais dans un simple environnement de test, vous devrez ajouter des adresses de messagerie aux comptes d'utilisateur ou groupes.

    Nous vous recommandons d’utiliser des groupes plutôt que des utilisateurs, pour simplifier la gestion des modèles. Si vous disposez d’Active Directory localement et effectuez une synchronisation avec Azure AD, vous pouvez utiliser des groupes de sécurité ou de distribution à extension messagerie. Toutefois, si vous voulez accorder des droits à tous les utilisateurs de l'organisation, il est plus efficace de copier un des modèles par défaut que de spécifier plusieurs groupes. Pour plus d’informations, consultez la section [Comment copier un modèle](copy-template.md).

    > [!TIP]
    > Vous pouvez par la suite ajouter au modèle des utilisateurs extérieurs à votre organisation en utilisant le [module Windows PowerShell pour Azure Rights Management](install-powershell.md) et en employant l’une des méthodes suivantes :
    > 
    > -   **Utiliser un objet de définition de droits pour mettre à jour un modèle** : spécifiez les adresses de messagerie externes et leurs droits dans un objet de définition de droits, que vous pouvez ensuite utiliser pour mettre à jour un modèle. Vous spécifiez l’objet de définition de droits à l’aide de l’applet de commande [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour créer une variable et spécifier ensuite cette variable dans le paramètre -RightsDefinition avec l’applet de commande [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727076.aspx) pour modifier un modèle existant. Cependant, si vous ajoutez ces utilisateurs à un modèle existant, vous devez aussi définir des objets de définition de droits pour les groupes existants des modèles et pas seulement les nouveaux utilisateurs externes.
    > -   **Exporter, modifier et importer le modèle mis à jour** : utilisez l’applet de commande [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) pour exporter le modèle vers un fichier que vous pouvez modifier pour ajouter les adresses de messagerie externes et les droits de ces utilisateurs aux groupes et droits existants. Utilisez ensuite l’applet de commande [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) pour réimporter cette modification dans Azure RMS.

3.  Cliquez sur le bouton Suivant, puis attribuez l'un des droits répertoriés à vos utilisateurs et groupes sélectionnés.

    Pour plus d'informations sur chaque droit (et pour les droits personnalisés), utilisez la description affichée. Vous trouverez des informations plus détaillées dans [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Toutefois, la manière dont les applications qui prennent en charge RMS implémentent ces droits peut varier. Consultez la documentation des applications et testez vous-mêmes celles dont les utilisateurs se servent afin de vérifier leur comportement avant de déployer le modèle pour les utilisateurs. Pour que ce modèle soit visible uniquement par les administrateurs dans le cadre de ce test, configurez-le comme modèle départemental (étape 6).

4.  Si vous avez sélectionné **Personnalisé**, cliquez sur le bouton Suivant, puis sélectionnez ces droits personnalisés.

    Bien que vous puissiez utiliser n'importe quelle combinaison de droits individuels disponibles, dans certaines applications, certains droits peuvent dépendre d'autres droits individuels. Le cas échéant, les droits dépendants sont automatiquement sélectionnés.

    > [!TIP]
    > Vous pouvez ajouter le droit **Copier et extraire le contenu** et l’accorder à des administrateurs ou du personnel spécifiques dans d’autres rôles ayant des responsabilités en matière de récupération d’informations. L'accord de ce droit leur permet de supprimer la protection, si nécessaire, des fichiers et des messages électroniques qui seront protégés à l'aide de ce modèle. Cette capacité à supprimer la protection au niveau du modèle fournit un contrôle plus précis que l’utilisation de la fonctionnalité de super utilisateur.

5.  Cliquez sur le bouton Terminé.

6.  Si vous souhaitez que seul un sous-ensemble d'utilisateurs puissent voir le modèle lorsqu'ils consultent la liste des modèles dans des applications : Pour configurer ce modèle comme modèle départemental, cliquez sur **ÉTENDUE** , puis sur **PRISE EN MAIN**. Sinon, passez à l'étape 9.

    Informations supplémentaires sur les modèles départementaux : par défaut, tous les utilisateurs figurant dans votre annuaire Azure voient tous les modèles publiés, et peuvent les sélectionner à partir d'applications quand ils souhaitent protéger du contenu. Si vous souhaitez que seuls certains utilisateurs puissent voir les modèles publiés, vous devez restreindre l'étendue de ces modèles à ces utilisateurs. Ensuite, seuls ces utilisateurs peuvent sélectionner ces modèles. Les autres utilisateurs non spécifiés ne les voient pas et ne peuvent donc pas les sélectionner. Cette technique peut aider les utilisateurs à choisir le modèle correct, en particulier si vous créez des modèles conçus pour être utilisés par des groupes ou départements spécifiques. Les utilisateurs ne voient alors que les modèles conçus pour eux.

    Par exemple, supposez que vous avez créé un modèle pour le service Ressources humaines (Human Resources) qui applique l’autorisation Lecture seule aux membres du service Finance. Pour que seuls les membres du département Ressources humaines puissent appliquer ce modèle quand ils utilisent l’application de partage Rights Management, vous définissez l’étendue du modèle sur le groupe à extension messagerie HumanResources. Ensuite, seuls les membres de ce groupe peuvent voir et appliquer ce modèle.

7.  Dans la page **VISIBILITÉ DU MODÈLE**, sélectionnez les utilisateurs et les groupes qui peuvent afficher et sélectionner le modèle à partir d’applications compatibles avec RMS. Comme précédemment, il est recommandé d'utiliser des groupes plutôt que des utilisateurs, et les groupes ou utilisateurs que vous sélectionnez doivent avoir une adresse de messagerie.

8.  Cliquez sur le bouton Suivant, puis décidez si vous devez configurer la compatibilité des applications pour votre modèle départemental. Si oui, cliquez sur **COMPATIBILITÉ DES APPLICATIONS**, cochez la case, puis cliquez sur **Terminer**.

    Pourquoi configurer la compatibilité des applications ? Certaines applications ne prennent pas en charge les modèles départementaux. Pour ce faire, l'application doit s'authentifier auprès du service RMS avant de télécharger les modèles. Si le processus d'authentification ne se produit pas, par défaut, aucun modèle départemental ne peut être téléchargé. Pour modifier ce comportement, spécifiez que tous les modèles départementaux doivent être téléchargeables en configurant la compatibilité des applications et en cochant la case **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l’identité de l’utilisateur** .

    Par exemple, si vous ne configurez pas la compatibilité des applications pour le modèle départemental dans notre exemple Ressources humaines, seuls les utilisateurs du département Ressources humaines voient ce modèle quand ils utilisent l'application de partage RMS, mais aucun utilisateur ne peut le voir s'il utilise Outlook Web Access (OWA) à partir d'Exchange Server 2013, car Exchange OWA et Exchange ActiveSync ne prennent pas en charge les modèles départementaux. Si vous modifiez ce comportement par défaut en configurant la compatibilité des applications, seuls les utilisateurs du département Ressources humaines voient le modèle départemental quand ils utilisent l'application de partage RMS, mais tous les utilisateurs le voient quand ils utilisent Outlook Web Access (OWA). En cas d'utilisation d'OWA ou d'Exchange ActiveSync à partir d'Exchange Online, soit tous les utilisateurs voient les modèles départementaux, soit aucun ne les voit, en fonction de l'état du modèle (archivé ou publié) dans Exchange Online.

    Office 2016 prend en charge en mode natif les modèles départementaux, tout comme le fait Office 2013 depuis la version 15.0.4727.1000, publiée en juin 2015 dans le cadre de ([KB 3054853](https://support.microsoft.com/kb/3054853)).

    > [!NOTE]
    > Si vous disposez d’applications qui ne prennent pas encore en charge les modèles départementaux en mode natif, vous pouvez utiliser un script de téléchargement de modèle RMS personnalisé ou d’autres outils pour déployer ces modèles dans le dossier client RMS local. Ensuite, ces applications affichent correctement les modèles départementaux uniquement aux utilisateurs et aux groupes que vous sélectionnez pour l'étendue du modèle :
    > 
    > -   Pour Office 2010, le dossier client est **%localappdata%\Microsoft\DRM\Templates**.
    > -   À partir d'un ordinateur client ayant téléchargé tous les modèles, vous pouvez copier et coller les fichiers de modèle sur d'autres ordinateurs.
    > 
    > Vous pouvez [télécharger le script de modèle RMS personnalisé à partir du site Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Si une erreur s’affiche lorsque vous cliquez sur ce lien, vous n’êtes probablement pas inscrit à Microsoft Connect.   Pour vous inscrire :
    > 
    > 1.  Accédez au [site Microsoft Connect](http://www.connect.microsoft.com), puis connectez-vous avec votre compte Microsoft.
    > 2.  Cliquez sur **Annuaire**, puis sélectionnez la catégorie **Afficher les produits Connect n’acceptant pas actuellement de commentaire**.
    > 3.  Recherchez **Rights Management Services** et, pour le programme **Microsoft RMS Enterprise Features**, cliquez sur **Rejoindre**.

9. Cliquez sur **CONFIGURER** et ajoutez les autres langues que les utilisateurs utilisent, ainsi que le nom et la description du modèle dans ces langues. Quand vos utilisateurs sont multilingues, il est important d’ajouter chacune des langues qu’ils utilisent ainsi que de fournir un nom et une description dans cette langue. Les utilisateurs peuvent alors voir le nom et la description du modèle dans la même langue que celle de leur système d'exploitation client. Vous êtes ainsi sûr qu'ils comprennent la stratégie appliquée à un document ou message électronique. Si aucune langue ne correspond à celle de leur système d'exploitation client, le nom et la description qui s'affichent le sont dans la langue que vous avez définie au moment où vous avez créé le modèle.

    Vérifiez ensuite si vous voulez apporter des modifications aux paramètres suivants :

    |Paramètre|Plus d'informations|
    |-----------|--------------------|
    |**expiration du contenu**|Définissez une date ou un nombre de jours après lesquels les fichiers protégés par le modèle ne devront plus s'ouvrir. Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée aux fichiers.<br /><br />Lorsque vous spécifiez une date, celle-ci prend effet à minuit, dans votre fuseau horaire actuel.|
    |**accès hors connexion**|Utilisez ce paramètre pour contrebalancer vos éventuelles exigences de sécurité quand les utilisateurs doivent pouvoir ouvrir des fichiers protégés alors qu’ils n’ont pas de connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est uniquement disponible pendant un nombre de jours spécifié, quand ce seuil est atteint, les utilisateurs doivent s’authentifier à nouveau et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter préalablement pour pouvoir ouvrir les fichiers.<br /><br />En plus d’une nouvelle authentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent accéder de nouveau ou ne plus accéder à un même fichier si des modifications ont été apportées à la stratégie ou à l'appartenance au groupe depuis leur dernier accès.|

10. Lorsque vous êtes certain que le modèle est correctement configuré pour vos utilisateurs, cliquez sur **PUBLIER** pour rendre le modèle visible pour les utilisateurs, puis cliquez sur **ENREGISTRER**.

11. Cliquez sur le bouton Précédent dans le portail Azure Classic pour revenir à la page **MODÈLES**, dans laquelle votre modèle affiche à présent l’état **Publié**.

Pour apporter des modifications à votre modèle, sélectionnez-le, puis utilisez de nouveau les étapes de démarrage rapide. Ou sélectionnez l'une des options suivantes :

-   Pour ajouter d'autres utilisateurs et groupes, puis définir leurs droits : Cliquez sur **DROITS**, puis sur **AJOUTER**.

-   Pour supprimer des utilisateurs ou groupes que vous avez précédemment sélectionnés : Cliquez sur **DROITS**, sélectionnez l’utilisateur ou le groupe dans la liste, puis cliquez sur **SUPPRIMER**.

-   Pour modifier les utilisateurs pouvant voir les modèles pour les sélectionner à partir d'applications : Cliquez sur **ÉTENDUE**, puis sur **AJOUTER** ou **SUPPRIMER**ou sur **COMPATIBILITÉ DES APPLICATIONS**.

-   Pour que le modèle ne soit plus visible par tous les utilisateurs : Cliquez sur **CONFIGURER**, sur **ARCHIVER**, puis sur **ENREGISTRER**.

-   Pour apporter d'autres modifications de configuration : Cliquez sur **CONFIGURER**, apportez vos modifications, puis cliquez sur **ENREGISTRER**.

> [!WARNING]
> Quand vous apportez des modifications à un modèle déjà enregistré, les clients ne voient pas ces modifications tant qu'ils n'ont pas actualisé le modèle sur leurs ordinateurs. Pour plus d’informations, consultez la section [Actualisation des modèles pour les utilisateurs](refresh-templates.md).

## Voir aussi
[Configurer des modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->


