---
title: Guide de l’administrateur du client Azure Information Protection
description: Instructions et informations destinées aux administrateurs d’un réseau d’entreprise en charge du déploiement du client Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: cec2614cacffa41ef3e4a345455c582ad92682f2
ms.sourcegitcommit: 746963b045072ea74e147895a8acda6a2e5bc9ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57226289"
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guide de l’administrateur du client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Utilisez les informations de ce guide si vous êtes responsable du client Azure Information Protection sur un réseau d’entreprise, ou si vous souhaitez des informations techniques supplémentaires par rapport au [Guide de l’administrateur du client Azure Information Protection](client-user-guide.md). 

Par exemple :

- Comprendre les différents composants de ce client et si vous devez les installer ou non

- Comment installer le client pour les utilisateurs, avec des informations sur les conditions préalables, des options et paramètres d’installation et des contrôles de vérification

- Guide de prise en charge des configurations personnalisées qui nécessitent une modification fréquente du registre

- Localiser les fichiers du client et les journaux d’utilisation

- Identifier les types de fichiers pris en charge par le client

- Configurer et utiliser le site de suivi de documents pour les utilisateurs

- Utiliser le client avec PowerShell pour le contrôle de ligne de commande

**Vous avez une question qui n’est pas traitée dans cette documentation ?** Visitez notre [site Yammer Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Présentation technique du client Azure Information Protection

Le client Azure Information Protection inclut les éléments suivants :

- Un complément Office, qui installe la barre Azure Information Protection pour que les utilisateurs sélectionnent des étiquettes de classification, et un bouton **Protéger** sur le ruban pour les autres options. Pour Outlook, un bouton **Ne pas transférer** est également disponible pour le ruban.

- L’Explorateur de fichiers Windows, avec des options contextuelles permettant aux utilisateurs d’appliquer des étiquettes de classification et la protection aux fichiers.

- Une visionneuse pour afficher les fichiers protégés lorsqu’une application native ne peut pas les ouvrir.

- Un module PowerShell pour appliquer et supprimer des étiquettes de classification et la protection de fichiers. 
    
    Ce module comprend des applets de commande pour installer et configurer le [scanneur Azure Information Protection](../deploy-aip-scanner.md) qui s’exécute comme un service sur Windows Server. Ce service vous permet de découvrir, classifier et protéger des fichiers sur des magasins de données tels que des partages réseau et des bibliothèques SharePoint Server.

- Le client Rights Management qui communique avec Azure Rights Management (Azure RMS) ou Active Directory Rights Management Services (AD RMS).

Le client Azure Information Protection est plus adapté pour fonctionner avec ses services Azure ; Azure Information Protection et son service de protection des données, Azure Rights Management. Toutefois, avec certaines restrictions, le client Azure Information Protection fonctionne également avec la version locale de Rights Management, AD RMS. Pour une comparaison complète des fonctionnalités prises en charge par Azure Information Protection et AD RMS, consultez [Comparaison d’Azure Information Protection avec AD RMS](../compare-on-premise.md). 

Si vous avez AD RMS et que vous souhaitez migrer AD RMS vers Azure Information Protection, consultez [Migration d’AD RMS vers Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-client"></a>Devez-vous déployer le client Azure Information Protection ?

Déployez le client Azure Information Protection si l’une des situations suivantes s’applique :

- Vous souhaitez classifier (et éventuellement protéger) des documents et des e-mails en sélectionnant des étiquettes à partir de vos applications Office (Word, Excel, PowerPoint, Outlook).

- Vous souhaitez classifier (et éventuellement protéger) des fichiers à l’aide de l’Explorateur de fichiers, qui prend en charge des types de fichiers supplémentaires que ceux pris en charge par Office, des sélections multiples et des dossiers.

- Vous souhaitez exécuter des scripts qui classifient (et éventuellement protègent) des documents à l’aide de commandes PowerShell.

- Vous souhaitez exécuter un service qui découvre, classifie (et éventuellement protège) des fichiers qui sont stockés localement.

- Vous souhaitez afficher des documents protégés lorsqu’une application native permettant d’afficher le fichier n’est pas installée ou ne parvient pas à ouvrir ces documents.

- Vous souhaitez uniquement protéger les fichiers à l’aide de l’Explorateur de fichiers ou des commandes PowerShell.

- Vous souhaitez que les utilisateurs et administrateurs soient en mesure de suivre et de révoquer des documents protégés.

- Voulez-vous supprimer le chiffrement des fichiers et des conteneurs (annuler la protection) en bloc aux fins de récupération des données.

- Vous exécutez Office 2010 et souhaitez protéger des documents et des e-mails à l’aide du service Azure Rights Management.

Exemple qui illustre le complément du client Azure Information Protection pour une application Office, affiche les étiquettes de classification de votre organisation ainsi que le nouveau bouton **Protéger** sur le ruban :

![Barre Azure Information Protection avec la stratégie par défaut](../media/word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-client"></a>Installation et prise en charge du client Azure Information Protection

Vous pouvez installer le client Azure Information Protection en utilisant un fichier exécutable ou un fichier Windows Installer. Pour plus d’informations sur chaque option et pour obtenir des instructions, consultez [Installer le client Azure Information Protection pour les utilisateurs](client-admin-guide-install.md).  

Utilisez les sections suivantes pour plus d’informations sur l’installation du client. 

### <a name="installation-checks-and-troubleshooting"></a>Vérifications et résolution des problèmes liés à l’installation

Quand le client est installé, utilisez l’option **Aide et commentaires** pour ouvrir la boîte de dialogue **Microsoft Azure Information Protection** :

- Depuis une application Office : Sous l’onglet **Accueil**, dans le groupe **Protection**, sélectionnez **Protéger**, puis **Aide et commentaires**.

- Depuis l'Explorateur de fichiers : Cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**. 

#### <a name="help-and-feedback-section"></a>Section **Aide et commentaires**

Le **lien En savoir plus** pointe par défaut sur le site web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection), mais vous pouvez le configurer pour qu’il pointe sur une URL personnalisée dans le cadre des [paramètres de stratégie](../configure-policy-settings.md) Azure Information Protection.

Le lien **Signaler un problème** s’affiche seulement si vous spécifiez un [paramètre client avancé](client-admin-guide-customizations.md#add-report-an-issue-for-users). Quand vous configurez ce paramètre, vous spécifiez un lien HTTP, comme l’adresse e-mail de votre support technique.

L’option **Exporter les journaux** permet de collecter et de joindre automatiquement des fichiers journaux pour le client Azure Information Protection si vous devez les envoyer au support Microsoft. Cette option peut également être utilisée par les utilisateurs finaux pour envoyer ces fichiers journaux à votre support technique.

L’option **Réinitialiser les paramètres** déconnecte l’utilisateur, supprime la stratégie Azure Information Protection téléchargée et rétablit les paramètres utilisateur pour le service Azure Rights Management.

##### <a name="more-information-about-the-reset-settings-option"></a>Informations supplémentaires sur l’option Réinitialiser les paramètres

- Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 

- Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers dans les emplacements suivants. Ces fichiers incluent les certificats clients, les modèles Rights Management, la stratégie Azure Information Protection et les informations d’identification de l’utilisateur mises en cache. Les fichiers journaux clients ne sont pas supprimés.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Les clés de Registre et les paramètres suivants sont supprimés. Si les paramètres d’une de ces clés de Registre ont des valeurs personnalisées, ils doivent être reconfigurés après la réinitialisation du client. 
    
    En général, pour les réseaux d’entreprise, ces paramètres sont configurés à l’aide de la stratégie de groupe, auquel cas ils sont automatiquement réappliqués lorsque la stratégie de groupe est actualisée sur l’ordinateur. Par contre, certains paramètres peuvent avoir été configurés ponctuellement, par le biais d’un script ou manuellement. Dans ce cas, vous devez prendre des mesures supplémentaires pour reconfigurer ces paramètres. Par exemple, les ordinateurs peuvent exécuter un script ponctuellement afin de configurer des paramètres pour une redirection vers Azure Information Protection, car vous procédez à la migration depuis AD RMS et vous disposez toujours d’un point de connexion de service sur votre réseau. Après la réinitialisation du client, l’ordinateur doit réexécuter ce script.
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- L’utilisateur actuellement connecté est déconnecté.

#### <a name="client-status-section"></a>Section **État du client**

Utilisez la valeur **Connecté en tant que** pour confirmer que le nom d’utilisateur affiché identifie le compte à utiliser pour l’authentification avec Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory. Le compte doit également appartenir à un locataire configuré pour Azure Information Protection.

Si vous avez besoin de vous connecter avec un nom d’utilisateur différent de celui qui est affiché, consultez la personnalisation [Se connecter avec l’identité d’un autre utilisateur](client-admin-guide-customizations.md#sign-in-as-a-different-user).

La **Dernière connexion** affiche la date/l’heure de la dernière connexion du client au service Azure Information Protection de votre organisation. Vous pouvez utiliser ces informations avec la date et l’heure auxquelles la **stratégie Information Protection a été installée** pour confirmer la date et l’heure de la dernière installation ou mise à jour de la stratégie Azure Information Protection. Lorsque le client se connecte au service, il télécharge automatiquement la dernière stratégie s’il détecte des modifications dans sa stratégie actuelle, ainsi que toutes les 24 heures. Si vous avez apporté des modifications à la stratégie après l’heure affichée, fermez et rouvrez l’application Office.

Si vous voyez **Ce client n’a pas de licence pour Office Professionnel Plus** : Le client Azure Information Protection a détecté que l’édition d’Office installée ne prend pas en charge l’application de la protection Rights Management. Si ce problème est détecté, les étiquettes qui appliquent la protection ne s’affichent pas dans la barre Azure Information Protection.

Utilisez l’information **Version** pour vérifier la version installée sur le client. Vous pouvez vérifier s’il s’agit de la dernière version et s’il existe des correctifs correspondants et des nouvelles fonctionnalités en cliquant sur le lien **Nouveautés** pour lire l’[historique de publication des versions](client-version-release-history.md) du client.

## <a name="support-for-multiple-languages"></a>Prise en charge de plusieurs langues

Le client Azure Information Protection prend en charge les mêmes langues qu’Office 365. Pour obtenir la liste de ces langues, consultez la section **Office 365, Exchange Online Protection et Power BI** dans la page [Disponibilité internationale](https://products.office.com/business/international-availability) des produits Office.

Pour ces langues, les options de menu, boîtes de dialogue et messages du client Azure Information Protection s’affichent dans la langue de l’utilisateur. Il existe un programme d’installation unique qui détecte la langue. Ainsi, aucune configuration supplémentaire n’est nécessaire pour installer le client Azure Information Protection pour différentes langues. 

Toutefois, les noms et les descriptions d’étiquette que vous spécifiez ne sont pas traduits automatiquement quand vous configurez des étiquettes dans la stratégie Azure Information Protection. Depuis le 30 août 2017, la [stratégie par défaut](../configure-policy-default.md) actuelle inclut la prise en charge de certaines langues. Pour que les utilisateurs puissent voir les étiquettes dans la langue de leur choix, fournissez vos propres traductions et configurez la stratégie Azure Information Protection pour les utiliser. Pour plus d’informations, consultez le [Guide de configuration des étiquettes pour des langues différentes dans Azure Information Protection](../configure-policy-languages.md). Les marquages visuels ne sont pas traduits et ne prennent pas en charge plusieurs langues.

## <a name="post-installation-tasks"></a>Tâches post-installation

Une fois que vous avez installé le client Azure Information Protection, assurez-vous de donner aux utilisateurs les instructions pour savoir comment étiqueter leurs e-mails et documents, ainsi que des conseils sur les étiquettes à choisir pour des scénarios spécifiques. Par exemple :

- Instructions en ligne pour l’utilisateur : [Azure Information Protection - Guide de l’utilisateur](client-user-guide.md)

- Téléchargez un guide d’utilisation personnalisable : [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="upgrading-and-maintaining-the-azure-information-protection-client"></a>Mise à niveau et maintenance du client Azure Information Protection

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des nouvelles fonctionnalités et des correctifs. Les annonces sont postées sur le [site Yammer](https://www.yammer.com/AskIPTeam) de l’équipe.

Si vous utilisez Windows Update, le client Azure Information Protection met automatiquement à niveau la version en disponibilité générale du client, indépendamment de la manière dont ce dernier a été installé. Les nouvelles versions de client sont publiées dans le catalogue quelques semaines après le lancement.

Vous pouvez également mettre à niveau manuellement le client en téléchargeant la nouvelle version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installez ensuite la nouvelle version pour mettre à niveau le client. Vous devez utiliser cette méthode pour mettre à niveau des préversions.

Lorsque vous mettez à niveau manuellement, ne désinstallez la version précédente que si vous changez de méthode d’installation. Par exemple, si vous passez de la version du fichier exécutable (.exe) du client à la version du programme d’installation (.msi) Windows du client. Ou si vous devez installer une version antérieure du client. Par exemple, vous avez installé la préversion actuelle pour la tester et vous devez maintenant revenir à la version actuelle en disponibilité générale.

Consultez [Historique des versions et politique du support](client-version-release-history.md) pour comprendre la politique de support du client Azure Information Protection, savoir quelles versions sont actuellement prises en charge et prendre connaissance des nouveautés et modifications des versions prises en charge. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Mise à niveau du scanneur Azure Information Protection

La méthode de mise à niveau du scanneur varie selon que vous mettez à niveau vers la version en disponibilité générale actuelle ou la préversion actuelle.

#### <a name="to-upgrade-the-scanner-to-the-current-ga-version"></a>Pour mettre à niveau le scanneur vers la version en disponibilité générale actuelle

Pour mettre à niveau le scanneur Azure Information Protection, installez la dernière version du client Azure Information Protection. Effectuez ensuite l’action unique suivante. Après cela, il n’est pas nécessaire de relancer l’analyse de fichiers déjà scannés.

- Exécutez [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) après avoir mis à niveau le client Azure Information Protection. Vos paramètres de configuration pour le scanneur et les référentiels sont conservés. L’exécution de cette applet de commande est nécessaire pour mettre à jour le schéma de base de données pour le scanneur et si nécessaire, le compte de service du scanneur se voit également accorder des autorisations de suppression pour la base de données du scanneur. 
    
    Tant que vous n’avez pas exécuté cette applet de commande de mise à jour, le scanneur ne s’exécute pas et vous voyez en général l’ID d’événement **1000** s’afficher dans le journal des événements Windows, avec le message d’erreur suivant : **Nom d’objet non valide « ScannerStatus »**.

#### <a name="to-upgrade-the-scanner-to-the-current-preview-version"></a>Pour mettre à niveau le scanneur vers la préversion actuelle

> [!IMPORTANT]
> Pour un chemin de mise à niveau correct, n’installez pas la préversion du client Azure Information Protection sur l’ordinateur qui exécute le scanneur comme première étape de mise à niveau du scanneur. Utilisez plutôt les instructions de mise à niveau suivantes.

Pour la préversion actuelle du scanneur, le processus de mise à niveau est différent des versions précédentes. La mise à niveau automatique du scanneur modifie le scanneur pour qu’il obtienne ses paramètres de configuration à partir du portail Azure. Le schéma est également mis à jour pour la base de données de configuration du scanneur, et cette base de données est également renommée à partir d’AzInfoProtection :

- Si vous ne spécifiez pas votre propre nom de profil, la base de données de configuration est renommée **AIPScanner_\<nom_ordinateur>**. 

- Si vous spécifiez votre propre nom de profil, la base de données de configuration est renommée **AIPScanner_\<nom_profil>**.

Bien qu’il soit possible de suivre une autre séquence pour mettre à niveau le scanneur, nous vous recommandons les étapes suivantes :

1. Utilisez le portail Azure pour créer un nouveau profil de scanneur qui inclut des paramètres pour le scanneur et vos référentiels de données avec tous les paramètres dont ils ont besoin. Pour obtenir de l’aide sur cette étape, consultez la section [Configurer le scanneur dans le portail Azure](../deploy-aip-scanner-preview.md#configure-the-scanner-in-the-azure-portal) dans les instructions de déploiement du scanneur en préversion.
    
    Si l’ordinateur qui exécute le scanneur est déconnecté d’Internet, vous devez toujours effectuer cette étape. Ensuite, à partir du portail Azure, utilisez l’option **Exporter** pour exporter votre profil de scanneur dans un fichier.

2. Sur l’ordinateur du scanneur, arrêtez le service du scanneur, **Scanneur Azure Information Protection**.

3. Mettez à niveau le client Azure Information Protection en installant la préversion actuelle depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

4. Dans une session PowerShell, exécutez la commande Update-AIPScanner avec le même nom de profil que vous avez spécifié à l’étape 1. Par exemple : `Update-AIPScanner –Profile USWest`

5. Uniquement si le scanneur est exécuté sur un ordinateur déconnecté : Exécutez maintenant [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration) et spécifiez le fichier qui contient les paramètres exportés.

6. Redémarrez le service **Scanneur Azure Information Protection**.

##### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>Mise à niveau selon une séquence différente des étapes recommandées

Si vous ne configurez pas le scanneur dans le portail Azure avant d’exécuter la commande Update-AIPScanner, vous ne devrez pas spécifier de nom de profil qui identifie vos paramètres de configuration de scanneur pour le processus de mise à niveau. 

Dans ce scénario, lorsque vous configurez le scanneur dans le portail Azure, vous devez spécifier exactement le même nom de profil que celui utilisé lors de l’exécution de la commande Update-AIPScanner. Si le nom ne correspond pas, le scanneur ne sera pas configuré pour vos paramètres. 

> [!TIP]
> Pour identifier les scanneurs dont la configuration est incorrecte, utilisez le panneau **Azure Information Protection - Nœuds** dans le portail Azure.
>  
> Les scanneurs connectés à Internet affichent leur nom d’ordinateur avec le numéro de préversion du client Azure Information Protection, mais pas de nom de profil. Seuls les scanneurs portant le numéro de version 1.41.51.0 ne doivent pas afficher de nom de profil dans ce panneau. 

Si vous n’avez pas spécifié de nom de profil lors de l’exécution de la commande Update-AIPScanner, le nom d’ordinateur est utilisé pour créer automatiquement le nom du profil du scanneur.

#### <a name="moving-the-scanner-configuration-database-to-a-different-sql-server-instance"></a>Déplacement de la base de données de configuration du scanneur vers une autre instance SQL Server

Dans la préversion actuelle, il existe un problème connu si vous essayez de déplacer la base de données de configuration du scanneur vers une nouvelle instance SQL Server après avoir exécuté la commande de mise à niveau.

Si vous savez si vous déplacerez la base de données de configuration du scanneur pour la préversion, procédez comme suit :

1. Désinstallez le scanneur à l’aide de [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner).

2. Si vous n’avez pas encore mis à niveau vers la préversion du client Azure Information Protection, mettez le client à niveau maintenant.

3. Installez le scanneur à l’aide de [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner), en spécifiant la nouvelle instance SQL Server et le nom du profil.

4. Facultatif : Si vous ne souhaitez pas que le scanneur relance l’analyse de tous les fichiers, exportez la table ScannerFiles et importez-la dans la nouvelle base de données.

## <a name="uninstalling-the-azure-information-protection-client"></a>Désinstallation du client Azure Information Protection

Vous pouvez utiliser l’une des options suivantes pour désinstaller le client :

- Utiliser le Panneau de configuration pour désinstaller un programme : Cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez le fichier exécutable (par exemple, **AzInfoProtection.exe**) et dans la page **Modifier l’installation**, cliquez sur **Désinstaller**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Étapes suivantes
Pour installer le client, consultez [Installer le client Azure Information Protection pour les utilisateurs](client-admin-guide-install.md).

Si vous avez déjà installé le client, consultez les informations supplémentaires suivantes sur la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


