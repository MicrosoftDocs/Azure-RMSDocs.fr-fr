---
title: TEST Configuration de modèles personnalisés pour Azure Rights Management
ms.custom: na
ms.reviewer: na
ms.service: rights-management
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: TEST
author: Cabailey
---
# AVANT : Configuration de modèles personnalisés pour Azure Rights Management
Après avoir activé Azure Rights Management (Azure RMS), les utilisateurs peuvent automatiquement utiliser les deux modèles par défaut qui leur facilitent l'application de stratégies aux fichiers sensibles pour en restreindre l'accès aux utilisateurs autorisés de votre organisation. Ces deux modèles incluent les restrictions de stratégie de droits suivantes :

-   Affichage en lecture seule du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Affichage confidentiel uniquement**

    -   Autorisation spécifique : Afficher le contenu

-   Autorisations de lecture ou de modification du contenu protégé

    -   Nom d’affichage : **&lt;nom de l’organisation&gt; - Confidentiel**

    -   Autorisations spécifiques : Afficher le contenu, Enregistrer le fichier, Modifier le contenu, Afficher les droits affectés, Autoriser les macros, Transférer, Répondre, Répondre à tous

En outre, l’ [application de partage RMS](http://technet.microsoft.com/library/dn339006.aspx) permet aux utilisateurs de définir leur propre jeu d’autorisations. Et pour le client Outlook et Outlook Web Access, les utilisateurs peuvent sélectionner l’option **Ne pas transférer** pour les messages électroniques.

Les modèles par défaut peuvent suffire à de nombreuses organisations. Mais si vous souhaitez créer vos propres modèles de stratégie de droits personnalisés, rien ne vous empêche de le faire. Les raisons justifiant la création d'un modèle personnalisé sont les suivantes :

-   Vous voulez un modèle pour octroyer des droits à un sous-ensemble d'utilisateurs au sein de l'organisation plutôt qu'à tous les utilisateurs.

-   Vous voulez que seul un sous-ensemble d'utilisateurs, plutôt que tous les utilisateurs de l'organisation, puissent afficher et sélectionner un modèle (modèle départemental) à partir d'applications.

-   Vous voulez définir des droits personnalisés pour un modèle, par exemple Affichage et Modification, mais pas Copie et Impression.

-   Vous voulez configurer d'autres options dans un modèle, notamment une date d'expiration et l'accessibilité du contenu sans connexion Internet.

Pour que les utilisateurs puissent sélectionner un modèle personnalisé qui contient des paramètres comme ceux-là, vous devez d'abord créer un modèle personnalisé, le configurer, puis le publier.

Utilisez les sections suivantes pour vous aider à configurer et utiliser des modèles personnalisés :

-   [Comment créer, configurer et publier un modèle personnalisé](configure-custom-templates.md#BKMK_HowToConfigureCustomTemplates)

-   [Comment copier un modèle](configure-custom-templates.md#BKMK_HowToCopyTemplates)

-   [Comment supprimer (archiver) des modèles](configure-custom-templates.md#BKMK_HowToArchiveTemplates)

-   [Actualisation des modèles pour les utilisateurs](configure-custom-templates.md#BKMK_RefreshingTemplates)

-   [Référence Windows PowerShell](configure-custom-templates.md#BKMK_PowerShellTemplates)

## Comment créer, configurer et publier un modèle personnalisé
Vous créez et gérez des modèles personnalisés dans le portail Azure Classic. Pour cela, vous pouvez accéder directement au portail Azure Classic ou vous connecter au Centre d’administration Office 365, puis choisir **Fonctionnalités avancées** de Rights Management. Vous êtes alors redirigé vers le portail Azure Classic.

Utilisez les procédures suivantes pour créer, configurer et publier des modèles personnalisés pour la Gestion des droits.

#### Pour créer un modèle personnalisé

1.  Selon que vous vous connectez au Centre d’administration Office 365 ou au portail Azure Classic, procédez de l’une des manières suivantes :

    -   Depuis le [centre d’administration Office 365](https://portal.office.com/):

        1.  Dans le panneau de gauche, cliquez sur **paramètres de service**.

        2.  À partir de la page **paramètres de service** , cliquez sur **rights management**.

        3.  Dans la section **Protéger vos informations** , cliquez sur **Gérer**.

        4.  Dans la section **Rights Management** , cliquez sur **fonctionnalités avancées**.

            > [!NOTE]
            > Si vous n’avez pas activé la Rights Management, cliquez d’abord sur **activer** et confirmez votre action. Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md).
            > 
            > Si vous n’avez pas encore cliqué sur **Fonctionnalités avancées**, une fois Rights Management activé, suivez les instructions à l’écran pour obtenir un abonnement Azure gratuit, nécessaire pour accéder au portail Azure Classic.

            Quand vous cliquez sur **Fonctionnalités avancées**, le portail Azure Classic s’ouvre et vous permet de gérer **RIGHTS MANAGEMENT** pour Azure Active Directory dans votre organisation.

    -   À partir du [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081) :

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

#### Pour configurer et publier un modèle personnalisé

1.  Sélectionnez votre modèle nouvellement créé dans la page **MODÈLES** du portail Azure Classic.

2.  Depuis la page de démarrage rapide **Votre modèle a été ajouté !** , cliquez sur **Mise en route** à l’étape 1, **Configurer des droits pour les utilisateurs et les groupes** , puis cliquez sur **PRENDRE EN MAIN MAINTENANT** ou **AJOUTER**et sélectionnez les utilisateurs et groupes autorisés à utiliser le contenu protégé par le nouveau modèle.

    > [!NOTE]
    > Les utilisateurs ou groupes que vous sélectionnez doivent avoir une adresse de messagerie. Dans un environnement de production, ce sera presque toujours le cas, mais dans un simple environnement de test, vous devrez ajouter des adresses de messagerie aux comptes d'utilisateur ou groupes.

    Nous vous recommandons d’utiliser des groupes plutôt que des utilisateurs, pour simplifier la gestion des modèles. Si vous disposez d’Active Directory localement et effectuez une synchronisation avec Azure AD, vous pouvez utiliser des groupes de sécurité ou de distribution à extension messagerie. Toutefois, si vous voulez accorder des droits à tous les utilisateurs de l'organisation, il est plus efficace de copier un des modèles par défaut que de spécifier plusieurs groupes. Pour plus d’informations, consultez la section [Comment copier un modèle](configure-custom-templates.md#BKMK_HowToCopyTemplates) dans cette rubrique.

    > [!TIP]
    > Vous pouvez par la suite ajouter au modèle des utilisateurs extérieurs à votre organisation en utilisant le [module Windows PowerShell pour Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx) et en employant l’une des méthodes suivantes :
    > 
    > -   **Utiliser un objet de définition de droits pour mettre à jour un modèle** : Spécifiez les adresses e-mail externes et leurs droits dans un objet de définition de droits, que vous pouvez ensuite utiliser pour mettre à jour un modèle. Vous spécifiez l’objet de définition de droits à l’aide de l’applet de commande [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) pour créer une variable et spécifier ensuite cette variable dans le paramètre -RightsDefinition avec l’applet de commande [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727076.aspx) pour modifier un modèle existant. Cependant, si vous ajoutez ces utilisateurs à un modèle existant, vous devez aussi définir des objets de définition de droits pour les groupes existants des modèles et pas seulement les nouveaux utilisateurs externes.
    > -   **Exporter, modifier et importer le modèle mis à jour** : Utilisez l’applet de commande [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) pour exporter le modèle vers un fichier que vous pouvez modifier pour ajouter les adresses e-mail externes et les droits de ces utilisateurs aux groupes et droits existants. Utilisez ensuite l’applet de commande [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) pour réimporter cette modification dans Azure RMS.

3.  Cliquez sur le bouton Suivant, puis attribuez l'un des droits répertoriés à vos utilisateurs et groupes sélectionnés.

    Pour plus d'informations sur chaque droit (et pour les droits personnalisés), utilisez la description affichée. Vous trouverez des informations plus détaillées dans [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Toutefois, la manière dont les applications qui prennent en charge RMS implémentent ces droits peut varier. Consultez la documentation des applications et testez vous-mêmes celles dont les utilisateurs se servent afin de vérifier leur comportement avant de déployer le modèle pour les utilisateurs. Pour que ce modèle soit visible uniquement par les administrateurs dans le cadre de ce test, configurez-le comme modèle départemental (étape 6).

4.  Si vous avez sélectionné **Personnalisé**, cliquez sur le bouton Suivant, puis sélectionnez ces droits personnalisés.

    Bien que vous puissiez utiliser n'importe quelle combinaison de droits individuels disponibles, dans certaines applications, certains droits peuvent dépendre d'autres droits individuels. Le cas échéant, les droits dépendants sont automatiquement sélectionnés.

    > [!TIP]
    > Vous pouvez ajouter le droit **Copier et extraire le contenu** et l’accorder à des administrateurs ou du personnel spécifiques dans d’autres rôles ayant des responsabilités en matière de récupération d’informations. L'accord de ce droit leur permet de supprimer la protection, si nécessaire, des fichiers et des messages électroniques qui seront protégés à l'aide de ce modèle. Cette capacité à supprimer la protection au niveau du modèle fournit un contrôle plus précis que l’utilisation de la fonctionnalité de super utilisateur.

5.  Cliquez sur le bouton Terminé.

6.  Si vous souhaitez que seul un sous-ensemble d'utilisateurs puissent voir le modèle lorsqu'ils consultent la liste des modèles dans des applications : Pour configurer ce modèle comme modèle départemental, cliquez sur **ÉTENDUE** , puis sur **PRISE EN MAIN**. Sinon, passez à l'étape 9.

    Informations supplémentaires sur les modèles départementaux : par défaut, tous les utilisateurs figurant dans votre annuaire Azure voient tous les modèles publiés, et peuvent les sélectionner à partir d'applications quand ils souhaitent protéger du contenu. Si vous souhaitez que seuls certains utilisateurs puissent voir les modèles publiés, vous devez restreindre l'étendue de ces modèles à ces utilisateurs. Ensuite, seuls ces utilisateurs peuvent sélectionner ces modèles. Les autres utilisateurs non spécifiés ne les voient pas et ne peuvent donc pas les sélectionner. Cette technique peut aider les utilisateurs à choisir le modèle correct, en particulier si vous créez des modèles conçus pour être utilisés par des groupes ou départements spécifiques. Les utilisateurs ne voient alors que les modèles conçus pour eux.

    Par exemple, supposez que vous avez créé un modèle pour le département Ressources humaines (Human Resources) qui applique l’autorisation Lecture seule aux membres du département Finance. Pour que seuls les membres du département Ressources humaines puissent appliquer ce modèle quand ils utilisent l’application de partage Rights Management, vous définissez l’étendue du modèle sur le groupe à extension messagerie HumanResources. Ensuite, seuls les membres de ce groupe peuvent voir et appliquer ce modèle.

7.  Dans la page **VISIBILITÉ DU MODÈLE**, sélectionnez les utilisateurs et les groupes qui peuvent afficher et sélectionner le modèle à partir d’applications compatibles RMS. Comme précédemment, il est recommandé d'utiliser des groupes plutôt que des utilisateurs, et les groupes ou utilisateurs que vous sélectionnez doivent avoir une adresse de messagerie.

8.  Cliquez sur le bouton Suivant, puis décidez si vous devez configurer la compatibilité des applications pour votre modèle départemental. Si oui, cliquez sur **COMPATIBILITÉ DES APPLICATIONS**, cochez la case, puis cliquez sur **Terminer**.

    Pourquoi configurer la compatibilité des applications ? Certaines applications ne prennent pas en charge les modèles départementaux. Pour ce faire, l'application doit s'authentifier auprès du service RMS avant de télécharger les modèles. Si le processus d'authentification ne se produit pas, par défaut, aucun modèle départemental ne peut être téléchargé. Pour modifier ce comportement, spécifiez que tous les modèles départementaux doivent être téléchargeables en configurant la compatibilité des applications et en cochant la case **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l’identité de l’utilisateur** .

    Par exemple, si vous ne configurez pas la compatibilité des applications pour le modèle départemental dans notre exemple Ressources humaines, seuls les utilisateurs du département Ressources humaines voient ce modèle quand ils utilisent l'application de partage RMS, mais aucun utilisateur ne peut le voir s'il utilise Outlook Web Access (OWA) à partir d'Exchange Server 2013, car Exchange OWA et Exchange ActiveSync ne prennent pas en charge les modèles départementaux. Si vous modifiez ce comportement par défaut en configurant la compatibilité des applications, seuls les utilisateurs du département Ressources humaines voient le modèle départemental quand ils utilisent l'application de partage RMS, mais tous les utilisateurs le voient quand ils utilisent Outlook Web Access (OWA). En cas d'utilisation d'OWA ou d'Exchange ActiveSync à partir d'Exchange Online, soit tous les utilisateurs voient les modèles départementaux, soit aucun ne les voit, en fonction de l'état du modèle (archivé ou publié) dans Exchange Online.

    Office 2016 en mode natif et Office 2013 avec les dernières mises à jour Office ([KB 3054853](https://support.microsoft.com/kb/3054853)) prennent en charge les modèles départementaux.

    > [!NOTE]
    > Si vous disposez d’applications qui ne prennent pas encore en charge en mode natif les modèles départementaux, vous pouvez utiliser un script téléchargé de modèle RMS personnalisé ou d’autres outils pour déployer ces modèles dans le dossier de client RMS local. Ensuite, ces applications affichent correctement les modèles départementaux uniquement aux utilisateurs et aux groupes que vous sélectionnez pour l'étendue du modèle :
    > 
    > -   Pour Office 2010, le dossier du client est **%localappdata%\Microsoft\DRM\Templates**.
    > -   À partir d'un ordinateur client ayant téléchargé tous les modèles, vous pouvez copier et coller les fichiers de modèle sur d'autres ordinateurs.
    > 
    > Vous pouvez [télécharger le script de modèle RMS personnalisé à partir du site Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Si une erreur s’affiche lorsque vous cliquez sur ce lien, vous n’êtes probablement pas inscrit à Microsoft Connect.   Pour vous inscrire :
    > 
    > 1.  Accédez au [site Microsoft Connect](http://www.connect.microsoft.com), puis connectez-vous avec votre compte Microsoft.
    > 2.  Cliquez sur **Annuaire**, puis sélectionnez la catégorie **Afficher les produits Connect n’acceptant pas actuellement de commentaire**.
    > 3.  Recherchez **Rights Management Services** et, pour le programme **Microsoft RMS Enterprise Features**, cliquez sur **Rejoindre**.

9. Cliquez sur **CONFIGURER** et ajoutez les autres langues que les utilisateurs utilisent, ainsi que le nom et la description du modèle dans ces langues. Quand vos utilisateurs sont multilingues, il est important d’ajouter chacune des langues qu’ils utilisent et de fournir un nom et une description dans cette langue. Les utilisateurs peuvent alors voir le nom et la description du modèle dans la même langue que celle de leur système d’exploitation client. Vous êtes ainsi sûr qu’ils comprennent la stratégie appliquée à un document ou message électronique. Si aucune langue ne correspond à celle de leur système d'exploitation client, le nom et la description qui s'affichent le sont dans la langue que vous avez définie au moment où vous avez créé le modèle.

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
> Quand vous apportez des modifications à un modèle déjà enregistré, les clients ne voient pas ces modifications tant qu'ils n'ont pas actualisé le modèle sur leurs ordinateurs. Pour plus d’informations, consultez la section [Actualisation des modèles pour les utilisateurs](configure-custom-templates.md#BKMK_RefreshingTemplates) dans cette rubrique.

## Comment copier un modèle
Si vous voulez créer un nouveau modèle dont les paramètres sont très similaires à ceux d’un modèle existant, sélectionnez le modèle d’origine sur la page **MODÈLES** , cliquez sur **COPIER**, spécifiez un nom unique, puis apportez les modifications nécessaires.

> [!IMPORTANT]
> Quand vous copiez un modèle, son statut **Publié** ou **Archivé** est également copié. Donc, si vous copiez un modèle publié, son état actuel est publié si vous ne le modifiez pas.

Vous pouvez copier les modèles personnalisés et les modèles par défaut. Si vous voulez que le modèle octroie des droits à tous les utilisateurs au sein de votre organisation, nous vous recommandons de copier un des modèles par défaut au lieu de créer un modèle personnalisé. Cette méthode vous évite de créer ou de sélectionner plusieurs groupes pour spécifier tous les utilisateurs. En revanche, dans ce scénario, vous devez veiller à spécifier pour le modèle copié un nouveau nom et une nouvelle description correspondant aux langues supplémentaires.

## Comment supprimer (archiver) des modèles
Vous ne pouvez pas supprimer des modèles par défaut. En revanche, vous pouvez les archiver de manière à ce que les utilisateurs ne puissent pas les voir.

De même, si vous avez publié un modèle personnalisé et que vous ne voulez plus que les utilisateurs puissent le voir, vous pouvez le modifier, puis choisir **ARCHIVER** et **ENREGISTRER** sur la page **CONFIGURER** . Vous pouvez également sélectionner **ARCHIVER** depuis la page **MODÈLES**.

Puisque vous ne pouvez pas modifier les modèles par défaut, pour les archiver, vous devez utiliser l’option **ARCHIVER** sur la page **MODÈLES** . Vous ne pouvez pas archiver l’option Outlook **Ne pas transférer** .

#### Pour supprimer un modèle par défaut

-   Sur la page **MODÈLES** , sélectionnez le modèle par défaut, puis cliquez sur **ARCHIVER**.

L’état passe de **Publié** à **Archivé**. Si vous changez d’avis, sélectionnez le modèle et cliquez sur **PUBLIER**.

## Actualisation des modèles pour les utilisateurs
Quand vous utilisez Azure RMS, les modèles sont automatiquement téléchargés vers les ordinateurs clients pour que les utilisateurs puissent les sélectionner depuis leurs applications. En revanche, vous devrez peut-être effectuer d'autres étapes si vous apportez des modifications aux modèles :

|Application ou service|Mode d'actualisation des modèles après des modifications|
|--------------------------|---------------------------------------------|
|Exchange Online|Configuration manuelle requise pour actualiser les modèles.<br /><br />Pour connaître les étapes de configuration, développez la section suivante, [Exchange Online uniquement : Configurer Exchange pour télécharger des modèles personnalisés modifiés](configure-custom-templates.md#BKMK_ExchangeOnlineTemplatesUpdate).|
|Office 365|Actualisation automatique (aucune étape supplémentaire requise).|
|Office 2016 et Office 2013<br /><br />Application de partage RMS pour Windows|Actualisation automatique (selon une planification) :<br /><br />Pour ces versions ultérieures d’Office : L’intervalle d’actualisation par défaut est de 7 jours.<br /><br />Pour l’application de partage RMS pour Windows : À partir de la version 1.0.1784.0, l’intervalle d’actualisation par défaut est d’un jour. Les versions antérieures ont, par défaut, un intervalle d'actualisation de 7 jours.<br /><br />Pour forcer une actualisation avant cette planification, développez la section suivante, [Office 2016, Office 2013 et application de partage RMS pour Windows : Forcer une actualisation pour un modèle personnalisé modifié](#BKMK_Office2013ForceUpdate).|
|Office 2010|Actualisation lors de la connexion des utilisateurs.<br /><br />Pour forcer une actualisation, demandez aux utilisateurs de se déconnecter, puis de se reconnecter ou forcez-les à le faire. Ou voir la section [Office 2010 uniquement : comment forcer une actualisation d'un modèle personnalisé modifié](#BKMK_Office2010ForceUpdate).|
Pour les appareils mobiles qui utilisent l'application de partage RMS, les modèles sont automatiquement téléchargés (et actualisés au besoin) sans aucune qu'aucune configuration soit requise.

### Exchange Online uniquement : Configurer Exchange pour télécharger des modèles personnalisés modifiés
Si vous avez déjà configuré la Gestion des droits relatifs à l'information (IRM) pour Exchange Online, les modèles personnalisés ne peuvent pas être téléchargés par les utilisateurs tant que vous n'apportez pas les modifications suivantes à l'aide de Windows PowerShell dans Exchange Online.

> [!NOTE]
> Pour plus d’informations sur l’utilisation de Windows PowerShell dans Exchange Online, consultez [Utilisation de PowerShell avec Exchange Online](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx).

Vous devez suivre cette procédure chaque fois que vous modifiez un modèle.

##### Pour mettre à jour des modèles pour Exchange Online

1.  À l’aide de Windows PowerShell dans Exchange Online, connectez-vous au service :

    1.  Indiquez vos nom d’utilisateur et mot de passe Office 365 :

        ```
        $Cred = Get-Credential
        ```

    2.  Connectez-vous au service Exchange Online en exécutant les deux commandes suivantes :

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  Utilisez l’applet de commande [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) pour réimporter votre domaine de publication approuvé (TPD) à partir d’Azure RMS :

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    Par exemple, si votre nom TPD est **RMS Online - 1** (nom par défaut pour de nombreuses organisations), entrez : **Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > Pour vérifier votre nom TPD, vous pouvez utiliser l’applet de commande [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) .

3.  Pour vérifier que les modèles ont été importés correctement, patientez quelques minutes, puis exécutez l’applet de commande [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) et définissez le Type sur All. Exemple :

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > Il est utile de conserver une copie de la sortie afin de pouvoir facilement copier les noms ou GUID de modèles si vous archivez un modèle ultérieurement.

4.  Si vous voulez qu’un modèle importé soit disponible dans Outlook Web App, vous devez utiliser l’applet de commande [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) et définir le Type sur Distributed :

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Outlook Web Access mettant en cache l’interface utilisateur pendant 24 heures, il se peut que les utilisateurs ne voient pas le nouveau modèle avant un jour.

De plus, si vous archivez un modèle (personnalisé ou par défaut) et utilisez Exchange Online avec Office 365, les utilisateurs vont continuer de voir les modèles archivés s'ils utilisent Outlook Web App ou des appareils mobiles qui utilisent le protocole Exchange ActiveSync.

Pour que les utilisateurs ne voient plus ces modèles, connectez-vous au service à l’aide de Windows PowerShell dans Exchange Online, puis utilisez l’applet de commande [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) en exécutant la commande suivante :

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

### Office 2016, Office 2013 et application de partage RMS pour Windows : Forcer une actualisation pour un modèle personnalisé modifié
En modifiant le Registre sur les ordinateurs exécutant Office 2016, Office 2013 ou l'application de partage Rights Management (RMS) pour Windows, vous pouvez modifier la planification automatique afin que les modèles modifiés soient actualisés sur les ordinateurs à une fréquence supérieure à la fréquence par défaut. Vous pouvez également forcer une actualisation immédiate en supprimant les données existantes dans une valeur de registre.

> [!WARNING]
> Si vous n'utilisez pas l'Éditeur du Registre correctement, vous risquez de provoquer de sérieux problèmes pouvant vous amener à devoir réinstaller le système d'exploitation. Microsoft ne peut pas garantir la résolution des problèmes engendrés par une utilisation incorrecte de l'Éditeur du Registre. Utilisez l'Éditeur du Registre à vos propres risques.

##### Pour modifier la planification automatique

1.  Dans l'un Éditeur du Registre, créez et définissez l'une des valeurs de Registre suivantes :

    -   Pour définir une fréquence de mise à jour en jours (au moins 1 jour) :  créez une valeur de Registre nommée **TemplateUpdateFrequency** , et définissez une valeur entière pour les données, spécifiant la fréquence en jours de téléchargement des modifications dans un modèle téléchargé. Utilisez le tableau suivant pour rechercher le chemin d'accès du Registre afin de créer cette nouvelle valeur de Registre.

        |Chemin d'accès au registre|Type|Valeur|
        |-----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequency|

    -   Pour définir une fréquence de mise à jour en secondes (au moins 1 seconde) :  créez une valeur de Registre nommée **TemplateUpdateFrequencyInSeconds** , et définissez une valeur entière pour les données, spécifiant la fréquence en secondes de téléchargement des modifications dans un modèle téléchargé. Utilisez le tableau suivant pour rechercher le chemin d'accès du Registre afin de créer cette nouvelle valeur de Registre.

        |Chemin d'accès au registre|Type|Valeur|
        |-----------------|--------|---------|
        |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC|REG_DWORD|TemplateUpdateFrequencyInSeconds|

    Assurez-vous que vous créez et définissez l'une de ces valeurs de Registre, pas les deux. Si les deux sont présentes, **TemplateUpdateFrequency** est ignoré.

2.  Si vous souhaitez forcer une actualisation immédiate des modèles, passez à la procédure suivante. Dans le cas contraire, redémarrez maintenant vos applications et instances Office de l'Explorateur de fichiers.

##### Pour forcer une actualisation immédiate

1.  À l’aide d’un éditeur du Registre, supprimez les données de la valeur **LastUpdatedTime** . Par exemple, les données peuvent afficher **2015-04-20T15:52**. Supprimez 2015-04-20T15:52 pour qu’aucune donnée ne s’affiche. Utilisez le tableau suivant pour rechercher le chemin d’accès du registre pour supprimer cette valeur de registre.

    |Chemin d'accès au registre|Type|Valeur|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\&lt;MicrosoftRMS_FQDN&gt;\Template|REG_SZ|LastUpdatedTime|
    > [!TIP]
    > Dans le chemin du Registre, *&lt;MicrosoftRMS_FQDN&gt;* fait référence au nom de domaine complet de votre service Microsoft RMS. Si vous souhaitez vérifier cette valeur :
    > 
    > 1.  Exécutez l’applet de commande [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) pour Azure RMS. Si vous n’avez pas déjà installé le module Windows PowerShell pour Azure RMS, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).
    > 2.  Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl** .
    > 
    >     Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  Dans la valeur, supprimez **https://** et **/_wmcs/licensing** de cette chaîne. La valeur restante est votre nom de domaine complet (FQDN) du service Microsoft RMS. Dans notre exemple, le nom de domaine complet (FQDN) du service Microsoft RMS a la valeur suivante :
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  Supprimer le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3.  Redémarrez vos applications et instances les de l'Explorateur de fichiers.

### Office 2010 uniquement : Forcer une actualisation pour un modèle personnalisé modifié
En modifiant le Registre sur les ordinateurs qui exécutent Office 2010, vous pouvez définir une valeur de façon à ce que les modèles modifiés soient actualisés sur les ordinateurs sans attendre que les utilisateurs se déconnectent, puis se reconnectent. Vous pouvez également forcer une actualisation immédiate en supprimant les données existantes dans une valeur de registre.

> [!WARNING]
> Si vous n'utilisez pas l'Éditeur du Registre correctement, vous risquez de provoquer de sérieux problèmes pouvant vous amener à devoir réinstaller le système d'exploitation. Microsoft ne peut pas garantir la résolution des problèmes engendrés par une utilisation incorrecte de l'Éditeur du Registre. Utilisez l'Éditeur du Registre à vos propres risques.

##### Pour modifier la fréquence de mise à jour

1.  À l'aide d'un éditeur du Registre, créez une nouvelle valeur de Registre nommée **UpdateFrequency** et définir une valeur entière pour les données, qui spécifiant la fréquence en jours pour télécharger les modifications dans un modèle téléchargé. Utilisez le tableau suivant pour rechercher le chemin d'accès du Registre afin de créer cette nouvelle valeur de Registre.

    |Chemin d'accès au registre|Type|Valeur|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_DWORD|UpdateFrequency|

2.  Si vous souhaitez forcer une actualisation immédiate des modèles, passez à la procédure suivante. Dans le cas contraire, redémarrez vos applications Office.

##### Pour forcer une actualisation immédiate

1.  À l’aide d’un éditeur du Registre, supprimez les données de la valeur **LastUpdatedTime** . Par exemple, les données peuvent afficher **2015-04-20T15:52**. Supprimez 2015-04-20T15:52 pour qu’aucune donnée ne s’affiche. Utilisez le tableau suivant pour rechercher le chemin d’accès du registre pour supprimer cette valeur de registre.

    |Chemin d'accès au registre|Type|Valeur|
    |-----------------|--------|---------|
    |HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement|REG_SZ|lastUpdatedTime|

2.  Supprimer le dossier suivant et tous les fichiers qu’il contient : **%localappdata%\Microsoft\MSIPC\Templates**

3.  Redémarrez vos applications Office.

## Référence Windows PowerShell
Toutes les opérations de création et de gestion des modèles que vous pouvez effectuer dans le portail Azure Classic sont également exécutables à partir de la ligne de commande de Windows PowerShell. De plus, vous pouvez importer et exporter des modèles afin de pouvoir copier des modèles entre clients ou réaliser des modifications en bloc de propriétés complexes dans les modèles, par exemple, au niveau des noms et des descriptions dans plusieurs langues.

Vous pouvez aussi avoir recours à l’exportation et à l’importation pour sauvegarder et restaurer vos modèles personnalisés. Nous vous recommandons de sauvegarder régulièrement vos modèles personnalisés. De cette manière, si vous apportez une modification qui n’était pas désirée, vous pourrez facilement rétablir une version antérieure.

> [!IMPORTANT]
> Pour utiliser Windows PowerShell pour créer et gérer des modèles de stratégies de droits Azure RMS, vous devez disposer au minimum de la version 2.0.0.0 du [module Windows PowerShell pour Azure RMS](http://go.microsoft.com/fwlink/?LinkId=257721).
> 
> Si vous avez déjà installé ce module Windows PowerShell, exécutez la commande suivante dans une fenêtre PowerShell pour vérifier le numéro de version : `(Get-Module aadrm -ListAvailable).Version`

Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md).

Applets de commande prenant en charge la création et la gestion de modèles :

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impout-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)

## Étapes suivantes
Une fois vos modèles personnalisés configurés pour Azure Rights Management, utilisez la [Feuille de route pour le déploiement d’Azure Rights Management](deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] à la disposition des utilisateurs et des administrateurs. Si aucune autre étape de configuration n’est nécessaire, consultez [Utilisation d’Azure Rights Management](using-azure-rights-management.md) pour obtenir des instructions afin de réussir le déploiement au sein de votre organisation.

## Voir aussi
[Configuration d'Azure Rights Management](configuring-azure-rights-management.md)

<!--HONumber=Apr16_HO3-->


