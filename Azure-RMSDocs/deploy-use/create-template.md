---
title: "Configurer et publier un modèle Azure RMS personnalisé"
description: "Instructions à suivre pour créer et gérer des modèles personnalisés dans le portail Azure Classic. Les modèles permettent aux utilisateurs finaux et à d’autres administrateurs d’appliquer facilement des stratégies appropriées qui protègent les documents et les e-mails."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d6e9aa0c-1694-4a53-8898-4939f31cc13f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cf11e0ac3bb13dcb31d14bad5f97ad117bd09953
ms.sourcegitcommit: 16fec44713c7064959ebb520b9f0857744fecce9
translationtype: HT
---
# <a name="create-configure-and-publish-a-custom-template"></a>Créer, configurer et publier un modèle personnalisé

>*S’applique à : Azure Information Protection, Office 365*


Vous créez et gérez des modèles personnalisés dans le portail Azure Classic. Pour cela, vous pouvez accéder directement au portail Azure Classic ou vous connecter au Centre d’administration Office 365, puis choisir **Fonctionnalités avancées** de Rights Management. Vous êtes alors redirigé vers le portail Azure Classic.

Vous devez être administrateur global pour créer et gérer des modèles dans le portail Azure Classic. Si vous avez attribué le rôle d’administrateur général pour le service Azure Rights Management à d’autres utilisateurs, ils peuvent également créer et gérer des modèles, mais ils doivent utiliser [PowerShell](configure-templates-with-powershell.md). Pour plus d’informations, consultez [Dois-je être administrateur général pour configurer Azure RMS ou puis-je déléguer cette opération à d’autres administrateurs ?](../get-started/faqs-rms.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators) 

Utilisez les procédures suivantes pour créer, configurer et publier des modèles personnalisés pour la Gestion des droits.

## <a name="to-create-a-custom-template"></a>Pour créer un modèle personnalisé

1.  Selon que vous vous connectez au Centre d’administration Office 365 ou au portail Azure Classic, procédez de l’une des manières suivantes :

    -   Dans le **Centre d’administration Office 365**, la navigation varie selon que vous utilisez sa version préliminaire (et la version en question), ou le centre d’administration Office 365 classique. Toutefois, pour toutes les versions, vous pouvez accéder directement à la page de[gestion des droits](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) : 

        1.  Dans la section **Configuration supplémentaire** , cliquez sur **Fonctionnalités avancées**.

            > [!NOTE]
            > Si le service Rights Management n’est pas activé, cliquez d’abord sur **activer** et confirmez votre action. Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md).
            > 
            > Si vous n’avez pas encore cliqué sur **Fonctionnalités avancées**, une fois Rights Management activé, suivez les instructions à l’écran pour obtenir un abonnement Azure gratuit, nécessaire pour accéder au portail Azure Classic.

            Quand vous cliquez sur **Fonctionnalités avancées**, le portail Azure Classic s’ouvre et vous permet de gérer **RIGHTS MANAGEMENT** pour Azure Active Directory dans votre organisation.

    -   À partir du [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=275081) :

        1. Dans le volet gauche, cliquez sur **Active Directory**.

        2. Dans la page **Active Directory** , cliquez sur **RIGHTS MANAGEMENT**.

        3. Si **STATUT DE RIGHTS MANAGEMENT** affiche **Inactif**, cliquez sur **ACTIVER**, puis confirmez votre action.

            > [!NOTE]
            > Pour plus d’informations, consultez [Activation d’Azure Rights Management](activate-service.md)
            >
        4. Si **STATUT DE RIGHTS MANAGEMENT** affiche **Actif**, sélectionnez le nom de votre locataire Active Directory.

2.  Créer un modèle :

    -   Dans le portail Azure Classic, dans la page de démarrage rapide **Prise en main de Rights Management**, cliquez sur **Créer un modèle de stratégie de droits**.

        Si cette page ne s’affiche pas immédiatement après que vous avez suivi les instructions pour Office 365, utilisez les instructions de navigation fournies ci-dessus pour le portail Azure Classic.

3. Sur la page **Ajouter un nouveau modèle de stratégie de droits** , choisissez la langue dans laquelle vous allez taper le nom et la description du modèle en fonction de vos utilisateurs (vous pourrez ajouter d’autres langues ultérieurement). Tapez ensuite un nom unique et une description, puis cliquez sur le bouton Terminé.

    N’incluez pas de signe deux-points ou point-virgule dans la description ou le nom de votre modèle. Certains services et applications utilisant les modèles Rights Management ne peuvent pas prendre en charge ces caractères pour ces modèles. Dans ce scénario, ces applications et services peuvent ne pas être en mesure de récupérer ou d’utiliser ces modèles Azure Rights Management.

4. Depuis la page de démarrage rapide **Prise en main de Rights Management** , cliquez sur **Gérer vos modèles de stratégie de droits**. Le modèle que vous venez de créer a été ajouté à la liste des modèles. Son état est **Archivé**. À ce stade, le modèle est créé mais pas configuré. Les utilisateurs ne peuvent pas le voir.

## <a name="to-configure-and-publish-a-custom-template"></a>Pour configurer et publier un modèle personnalisé

1.  Sélectionnez votre modèle nouvellement créé dans la page **MODÈLES** du portail Azure Classic.

2.  Depuis la page de démarrage rapide **Votre modèle a été ajouté !** , cliquez sur **Mise en route** à l’étape 1, **Configurer des droits pour les utilisateurs et les groupes** , puis cliquez sur **PRENDRE EN MAIN MAINTENANT** ou **AJOUTER**et sélectionnez les utilisateurs et groupes autorisés à utiliser le contenu protégé par le nouveau modèle.

    > [!NOTE]
    > Les utilisateurs ou groupes que vous sélectionnez doivent avoir une adresse de messagerie. Dans un environnement de production, ce sera presque toujours le cas, mais dans un simple environnement de test, vous devrez ajouter des adresses de messagerie aux comptes d'utilisateur ou groupes.
    > 
    > Si une adresse de messagerie est modifiée après que vous ayez sélectionné l’utilisateur ou le groupe et enregistré le modèle, consultez la section [Éléments à prendre en considération en cas de modification des adresses de messagerie](../plan-design/prepare.md#considerations-if-email-addresses-change) de la documentation relative à la planification. 

    Nous vous recommandons d’utiliser des groupes plutôt que des utilisateurs, pour simplifier la gestion des modèles. Toutefois, si vous apportez des modifications à ce groupe, n’oubliez pas que pour des raisons de performances, Azure Rights Management [met en cache l’appartenance au groupe](../plan-design/prepare.md#group-membership-caching). 
    
    Si vous disposez d’Active Directory localement et effectuez une synchronisation avec Azure AD, vous pouvez utiliser des groupes de sécurité ou de distribution à extension messagerie. Si vous voulez accorder des droits à tous les utilisateurs de l’organisation, mieux vaut copier l’un des modèles par défaut que de spécifier plusieurs groupes. Pour plus d’informations, consultez [Comment copier un modèle](copy-template.md).

    > [!TIP]
    > Vous pouvez ajouter des utilisateurs extérieurs à votre organisation (« utilisateurs externes ») au modèle en sélectionnant un groupe à extension messagerie qui contient des contacts d’Office 365 ou Exchange Online. Cela vous permet d’attribuer des droits à ces utilisateurs de la même façon que vous pouvez attribuer des droits aux utilisateurs de votre organisation. Par exemple, vous pouvez empêcher les clients de modifier une liste de prix que vous leur envoyez. N’utilisez pas cette configuration de modèle pour protéger des e-mails si les utilisateurs extérieurs à votre organisation lisent les e-mails protégés à l’aide d’Outlook Web App.
    > 
    > En outre, vous pouvez ultérieurement ajouter des utilisateurs extérieurs à votre organisation au modèle, par **utilisateurs spécifiques**, **groupes** ou **tous les utilisateurs de cette organisation**. Pour ce faire, utilisez le [module Windows PowerShell pour Azure Rights Management](install-powershell.md) et l’une des méthodes suivantes :
    > 
    > -  **Utiliser un objet de définition de droits pour mettre à jour un modèle** : spécifiez les utilisateurs externes (par adresse e-mail d’utilisateur, adresse e-mail de groupe, ou par domaine pour tous les utilisateurs dans cette organisation) et leurs droits dans un objet de définition de droits. Ensuite, utilisez un objet de définition de droits pour mettre à jour votre modèle. Vous spécifiez l’objet de définition de droits à l’aide de l’applet de commande [New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition) pour créer une variable et spécifier ensuite cette variable dans le paramètre -RightsDefinition avec l’applet de commande [Add-AadrmTemplate](/powershell/aadrm/vlatest/set-aadrmtemplateproperty) pour modifier un modèle existant. Cependant, si vous ajoutez ces utilisateurs à un modèle existant, vous devez aussi définir des objets de définition de droits pour les groupes existants des modèles et pas seulement les nouveaux utilisateurs externes.
    > -  **Exporter, modifier et importer le modèle mis à jour** : utilisez l’applet de commande [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) pour exporter le modèle vers un fichier que vous pouvez modifier pour ajouter les utilisateurs externes (par adresse e-mail d’utilisateur, adresse e-mail de groupe, ou par domaine pour tous les utilisateurs dans cette organisation) et leurs droits aux groupes et droits existants. Utilisez ensuite l’applet de commande [Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate) pour réimporter cette modification dans Azure RMS.

3.  Cliquez sur le bouton Suivant, puis attribuez l'un des droits répertoriés à vos utilisateurs et groupes sélectionnés.

    Pour plus d'informations sur chaque droit (et pour les droits personnalisés), utilisez la description affichée. Vous trouverez des informations plus détaillées dans [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md). Toutefois, la manière dont les applications qui prennent en charge Rights Management implémentent ces droits peut varier. Consultez la documentation des applications et testez vous-mêmes celles dont les utilisateurs se servent afin de vérifier leur comportement avant de déployer le modèle pour les utilisateurs. Pour que ce modèle soit visible uniquement par les administrateurs dans le cadre de ce test, configurez-le comme modèle départemental (étape 6).

4.  Si vous avez sélectionné **Personnalisé**, cliquez sur le bouton Suivant, puis sélectionnez ces droits personnalisés.

    Bien que vous puissiez utiliser n'importe quelle combinaison de droits individuels disponibles, dans certaines applications, certains droits peuvent dépendre d'autres droits individuels. Le cas échéant, les droits dépendants sont automatiquement sélectionnés.

    > [!TIP]
    > Vous pouvez ajouter le droit **Copier et extraire le contenu** et l’accorder à des administrateurs ou du personnel spécifiques dans d’autres rôles ayant des responsabilités en matière de récupération d’informations. L'accord de ce droit leur permet de supprimer la protection, si nécessaire, des fichiers et des messages électroniques qui seront protégés à l'aide de ce modèle. Cette capacité à supprimer la protection au niveau du modèle fournit un contrôle plus précis que l’utilisation de la fonctionnalité de super utilisateur.

5.  Cliquez sur le bouton Terminé.

6.  Si vous souhaitez que seul un sous-ensemble d'utilisateurs puissent voir le modèle lorsqu'ils consultent la liste des modèles dans des applications : Pour configurer ce modèle comme modèle départemental, cliquez sur **ÉTENDUE** , puis sur **PRISE EN MAIN**. Sinon, passez à l'étape 9.

    Informations supplémentaires sur les modèles départementaux : par défaut, tous les utilisateurs figurant dans votre annuaire Azure voient tous les modèles publiés, et peuvent les sélectionner à partir d'applications quand ils souhaitent protéger du contenu. Si vous souhaitez que seuls certains utilisateurs puissent voir les modèles publiés, vous devez restreindre l'étendue de ces modèles à ces utilisateurs. Ensuite, seuls ces utilisateurs peuvent sélectionner ces modèles. Les autres utilisateurs non spécifiés ne les voient pas et ne peuvent donc pas les sélectionner. Cette technique peut aider les utilisateurs à choisir le modèle correct, en particulier si vous créez des modèles conçus pour être utilisés par des groupes ou départements spécifiques. Les utilisateurs ne voient alors que les modèles conçus pour eux.

    Par exemple, supposez que vous avez créé un modèle pour le service Ressources humaines (Human Resources) qui applique l’autorisation Lecture seule aux membres du service Finance. Pour que seuls les membres du département Ressources humaines puissent appliquer ce modèle quand ils utilisent le client Azure Information Protection, vous définissez l’étendue du modèle sur le groupe à extension messagerie HumanResources. Ensuite, seuls les membres de ce groupe peuvent appliquer ce modèle. En outre, si les utilisateurs exécutent le client Azure Information Protection en [mode protection uniquement](../rms-client/client-protection-only-mode.md), ils ne voient pas ce modèle.

7.  Dans la page **VISIBILITÉ DU MODÈLE**, sélectionnez les utilisateurs et les groupes qui peuvent afficher et sélectionner le modèle à partir d’applications compatibles avec RMS. Comme précédemment, il est recommandé d'utiliser des groupes plutôt que des utilisateurs, et les groupes ou utilisateurs que vous sélectionnez doivent avoir une adresse de messagerie.

8.  Cliquez sur le bouton Suivant, puis décidez si vous devez configurer la compatibilité des applications pour votre modèle départemental. Si oui, cliquez sur **COMPATIBILITÉ DES APPLICATIONS**, cochez la case, puis cliquez sur **Terminer**.

    Pourquoi configurer la compatibilité des applications ? Certaines applications ne prennent pas en charge les modèles départementaux. Pour ce faire, l'application doit s'authentifier auprès du service RMS avant de télécharger les modèles. Si le processus d'authentification ne se produit pas, par défaut, aucun modèle départemental ne peut être téléchargé. Pour modifier ce comportement, spécifiez que tous les modèles départementaux doivent être téléchargeables en configurant la compatibilité des applications et en cochant la case **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l’identité de l’utilisateur** .

    Par exemple, si vous ne configurez pas la compatibilité des applications pour le modèle départemental dans notre exemple Ressources humaines, seuls les utilisateurs du département Ressources humaines voient ce modèle quand ils utilisent le client Azure Information Protection en [mode protection uniquement](../rms-client/client-protection-only-mode.md), mais aucun utilisateur ne peut le voir s’il utilise Outlook Web Access (OWA) à partir d’Exchange Server 2013, car Exchange OWA et Exchange ActiveSync ne prennent pas en charge les modèles départementaux. Si vous modifiez ce comportement par défaut en configurant la compatibilité des applications, seuls les utilisateurs du département Ressources humaines voient le modèle départemental quand ils utilisent le client Azure Information Protection en mode protection uniquement, mais tous les utilisateurs le voient quand ils utilisent Outlook Web Access (OWA). En cas d'utilisation d'OWA ou d'Exchange ActiveSync à partir d'Exchange Online, soit tous les utilisateurs voient les modèles départementaux, soit aucun ne les voit, en fonction de l'état du modèle (archivé ou publié) dans Exchange Online.

    Office 2016 prend en charge en mode natif les modèles départementaux, tout comme le fait Office 2013 depuis la version 15.0.4727.1000, publiée en juin 2015 dans le cadre de [KB 3054853](https://support.microsoft.com/kb/3054853).

    > [!NOTE]
    > Si vous disposez d’applications qui ne prennent pas encore en charge les modèles départementaux en mode natif, vous pouvez utiliser un script de téléchargement de modèle RMS personnalisé ou d’autres outils pour déployer ces modèles dans le dossier client RMS local. Ensuite, ces applications affichent correctement les modèles départementaux uniquement aux utilisateurs et aux groupes que vous sélectionnez pour l'étendue du modèle :
    > 
    > -   Pour Office 2010, le dossier client est **%localappdata%\Microsoft\DRM\Templates**.
    > -   À partir d'un ordinateur client ayant téléchargé tous les modèles, vous pouvez copier et coller les fichiers de modèle sur d'autres ordinateurs.
    > 
    > Vous pouvez [télécharger le script de modèle RMS personnalisé à partir du site Microsoft Connect](http://go.microsoft.com/fwlink/?LinkId=524506). Si une erreur s’affiche lorsque vous cliquez sur ce lien, vous n’êtes probablement pas inscrit à Microsoft Connect. Pour vous inscrire :
    > 
    > 1.  Accédez au [site Microsoft Connect](http://www.connect.microsoft.com), puis connectez-vous avec votre compte Microsoft.
    > 2.  Cliquez sur **Annuaire**, puis sélectionnez la catégorie **Afficher les produits Connect n’acceptant pas actuellement de commentaire**.
    > 3.  Recherchez **Rights Management Services** et, pour le programme **Microsoft RMS Enterprise Features**, cliquez sur **Rejoindre**.

9. Cliquez sur **CONFIGURER** et ajoutez les autres langues que les utilisateurs utilisent, ainsi que le nom et la description du modèle dans ces langues. Quand vos utilisateurs sont multilingues, il est important d’ajouter chacune des langues qu’ils utilisent ainsi que de fournir un nom et une description dans cette langue. Les utilisateurs peuvent alors voir le nom et la description du modèle dans la même langue que celle de leur système d’exploitation client. Vous êtes ainsi sûr qu’ils comprennent la stratégie appliquée à un document ou message électronique. Si aucune langue ne correspond à celle de leur système d'exploitation client, le nom et la description qui s'affichent le sont dans la langue que vous avez définie au moment où vous avez créé le modèle.

    Vérifiez ensuite si vous voulez apporter des modifications aux paramètres suivants :

    |Paramètre|Plus d'informations| Paramètre recommandé
    |-----------|--------------------|--------------------|
    |**expiration du contenu**|Définissez une date ou un nombre de jours après lesquels les fichiers protégés par le modèle ne devront plus s'ouvrir. Vous pouvez spécifier une date ou un nombre de jours à partir du moment où la protection est appliquée aux fichiers.<br /><br />Lorsque vous spécifiez une date, celle-ci prend effet à minuit, dans votre fuseau horaire actuel.|**Le contenu n’expire jamais**, sauf s'il comporte une spécification de durée.|
    |**accès hors connexion**|Utilisez ce paramètre pour contrebalancer vos éventuelles exigences de sécurité quand les utilisateurs doivent pouvoir ouvrir des fichiers protégés alors qu’ils n’ont pas de connexion Internet.<br /><br />Si vous spécifiez que le contenu n’est pas disponible sans connexion Internet ou que ce contenu est uniquement disponible pendant un nombre de jours spécifié, quand ce seuil est atteint, les utilisateurs doivent s’authentifier à nouveau et leur accès est journalisé. Dans ce cas, si leurs informations d’identification ne sont pas mises en cache, les utilisateurs sont invités à se connecter préalablement pour pouvoir ouvrir les fichiers.<br /><br />En plus d’une nouvelle authentification, la stratégie et l’appartenance au groupe d’utilisateurs sont réévaluées. Cela signifie que les utilisateurs peuvent accéder de nouveau ou ne plus accéder à un même fichier si des modifications ont été apportées à la stratégie ou à l'appartenance au groupe depuis leur dernier accès.|En fonction de la sensibilité du contenu :<br /><br />- **Nombre de jours pendant lesquels le contenu est disponible sans connexion Internet** = **7** pour les données métier sensibles pouvant nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation offre un compromis entre sécurité et flexibilité. Il peut s'agir entre autres de contrats, de rapports de sécurité, de résumés de prévision et de données commerciales .<br /><br />- **Le contenu est disponible uniquement avec une connexion Internet** pour les données métier sensibles pouvant nuire à l’entreprise si elles sont partagées avec des personnes non autorisées. Cette recommandation met la priorité sur la sécurité avant la flexibilité. Il s'agit entre autres d'informations sur les clients et les employés, les mots de passe, le code source et des rapports financiers préalablement annoncés.|

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

## <a name="see-also"></a>Voir aussi
[Configurer des modèles personnalisés pour Azure Rights Management](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]