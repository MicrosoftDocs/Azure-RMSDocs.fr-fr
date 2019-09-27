---
title: Guide d’administration du client d’étiquetage unifié Azure Information Protection
description: Instructions et informations pour les administrateurs sur un réseau d’entreprise qui sont responsables du déploiement du client d’étiquetage Azure Information Protection unifié pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5353fa25af08c8ef9c979d232945c7f203a0de07
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71313954"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Guide de l’administrateur du client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Utilisez les informations de ce guide si vous êtes responsable de la Azure Information Protection client d’étiquetage unifié sur un réseau d’entreprise, ou si vous souhaitez des informations plus techniques que celles de l' [utilisateur du client d’étiquetage unifié Azure information protection Guide](clientv2-user-guide.md). 

Exemple :

- Comprendre les différents composants de ce client et si vous devez les installer ou non

- Comment installer le client pour les utilisateurs, avec des informations sur les conditions préalables, des options et paramètres d’installation et des contrôles de vérification

- Localiser les fichiers du client et les journaux d’utilisation

- Identifier les types de fichiers pris en charge par le client

- Utiliser le client avec PowerShell pour le contrôle de ligne de commande

**Vous avez une question qui n’est pas traitée dans cette documentation ?** Visitez notre [site Yammer Azure Information Protection](https://www.yammer.com/AskIPTeam). 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Présentation technique du client d’étiquetage unifié Azure Information Protection

Le client d’étiquetage unifié Azure Information Protection comprend les éléments suivants:

- Un complément Office, qui installe un bouton de **sensibilité** sur le ruban pour permettre aux utilisateurs de sélectionner des étiquettes de sensibilité, et une option pour afficher la barre de Azure information protection pour une meilleure visibilité des étiquettes.

- L’Explorateur de fichiers Windows, avec des options contextuelles permettant aux utilisateurs d’appliquer des étiquettes de classification et la protection aux fichiers.

- Une visionneuse pour afficher les fichiers protégés lorsqu’une application native ne peut pas les ouvrir.

- Un module PowerShell pour découvrir des informations sensibles dans des fichiers et appliquer ou supprimer des étiquettes de classification et la protection des fichiers. 
    
    La version préliminaire du client comprend des applets de commande permettant d’installer et de configurer le [scanneur Azure information protection](../deploy-aip-scanner.md) qui s’exécute en tant que service sur Windows Server. Ce service vous permet de découvrir, classifier et protéger des fichiers dans des magasins de données tels que des partages réseau et des bibliothèques SharePoint Server.

- Le client Rights Management qui communique avec le service de protection (Azure Rights Management) pour chiffrer et protéger des fichiers.

À l’exception de la visionneuse, le Azure Information Protection client d’étiquetage unifié ne peut pas être utilisé avec des applications et des services qui communiquent directement avec le service de protection ou services AD RMS (Active Directory Rights Management Services).

Si vous avez AD RMS et que vous souhaitez migrer AD RMS vers Azure Information Protection, consultez [Migration d’AD RMS vers Azure Information Protection](../migrate-from-ad-rms-to-azure-rms.md).


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>Devez-vous déployer le client d’étiquetage unifié Azure Information Protection?

Déployez le client d’étiquetage unifié Azure Information Protection si vous utilisez des [étiquettes de sensibilité dans le centre de sécurité et de conformité Office 365](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels), et que l’une des conditions suivantes s’applique:

- Vous souhaitez classer (et éventuellement protéger) des documents et des messages électroniques en sélectionnant des étiquettes dans vos applications Office (Word, Excel, PowerPoint, Outlook) sur les ordinateurs Windows.

- Vous souhaitez classifier (et éventuellement protéger) des fichiers à l’aide de l’Explorateur de fichiers, qui prend en charge des types de fichiers supplémentaires que ceux pris en charge par Office, des sélections multiples et des dossiers.

- Vous souhaitez exécuter des scripts qui classifient (et éventuellement protègent) des documents à l’aide de commandes PowerShell.

- Vous souhaitez tester un service actuellement en version préliminaire qui découvre, classifie (et éventuellement protège) les fichiers qui sont stockés en local.

- Vous souhaitez afficher des documents protégés lorsqu’une application native permettant d’afficher le fichier n’est pas installée ou ne parvient pas à ouvrir ces documents.

Exemple montrant le complément Office pour le Azure Information Protection client d’étiquetage unifié, affichant le nouveau bouton **sensibilité** sur le ruban et la barre de Azure information Protection facultative:

![Barre Azure Information Protection avec la stratégie par défaut](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>Installation et prise en charge du client d’étiquetage unifié Azure Information Protection

Vous pouvez installer le client d’étiquetage unifié Azure Information Protection à l’aide d’un fichier exécutable ou d’un fichier Windows Installer. Pour plus d’informations sur chaque choix et pour obtenir des instructions, consultez [installer le client d’étiquetage unifié Azure information protection pour les utilisateurs](clientv2-admin-guide-install.md).  

Utilisez les sections suivantes pour plus d’informations sur l’installation du client. 

### <a name="installation-checks-and-troubleshooting"></a>Vérifications et résolution des problèmes liés à l’installation

Quand le client est installé, utilisez l’option **Aide et commentaires** pour ouvrir la boîte de dialogue **Microsoft Azure Information Protection** :

- À partir d’une application Office: Dans l’onglet dossier de **démarrage** , dans le groupe **sensibilité** , sélectionnez **sensibilité**, puis sélectionnez **aide et commentaires**.

- Depuis l’Explorateur de fichiers : Cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**. 

#### <a name="help-and-feedback-section"></a>Section **Aide et commentaires**

Le **lien en savoir plus** , par défaut, est dirigé vers le site Web [Azure information protection](https://www.microsoft.com/cloud-platform/azure-information-protection) . Vous pouvez configurer votre propre lien d’URL qui accède à une page d’aide personnalisée en tant qu’un des paramètres de stratégie dans votre centre de gestion d’étiquetage : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 ou le Centre de conformité Microsoft 365.

Le lien **signaler un problème** s’affiche uniquement si vous spécifiez un [paramètre avancé](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users). Quand vous configurez ce paramètre, vous spécifiez un lien HTTP, comme l’adresse e-mail de votre support technique. 

Les **journaux d’exportation** collectent et attachent automatiquement les fichiers journaux de l’Azure information protection client d’étiquetage unifié si vous avez été invité à les envoyer à support Microsoft. Cette option peut également être utilisée par les utilisateurs finaux pour envoyer ces fichiers journaux à votre support technique. Vous pouvez également utiliser l’applet de commande PowerShell [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) (nécessite la version préliminaire du client).

Les **paramètres** de réinitialisation déconnectent l’utilisateur, supprime les étiquettes de sensibilité et les stratégies d’étiquette actuellement téléchargées, puis réinitialise les paramètres utilisateur pour le service Azure Rights Management.

> [!NOTE]
> Si vous rencontrez des problèmes techniques avec le client, consultez [options de support et ressources](../information-support.md#support-options-and-community-resources)de la communauté.

##### <a name="more-information-about-the-reset-settings-option"></a>Informations supplémentaires sur l’option Réinitialiser les paramètres

- Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 

- Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers dans les emplacements suivants. Ces fichiers incluent des certificats clients, des modèles de protection, des étiquettes de sensibilité et des stratégies à partir de votre centre de gestion des étiquettes, ainsi que les informations d’identification de l’utilisateur mises en cache. Les fichiers journaux clients ne sont pas supprimés.
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - \\ *%LocalAppData%\Microsoft\MSIP\mipProcessName\<\mip\>*
    
    - %LocalAppData%\Microsoft\MSIP\AppDetails
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- Les clés de Registre et les paramètres suivants sont supprimés. Si les paramètres d’une de ces clés de Registre ont des valeurs personnalisées, ils doivent être reconfigurés après la réinitialisation du client.
    
    En général, pour les réseaux d’entreprise, ces paramètres sont configurés à l’aide de la stratégie de groupe, auquel cas ils sont automatiquement réappliqués lorsque la stratégie de groupe est actualisée sur l’ordinateur. Par contre, certains paramètres peuvent avoir été configurés ponctuellement, par le biais d’un script ou manuellement. Dans ce cas, vous devez prendre des mesures supplémentaires pour reconfigurer ces paramètres. Par exemple, les ordinateurs peuvent exécuter un script ponctuellement afin de configurer des paramètres pour une redirection vers Azure Information Protection, car vous procédez à la migration depuis AD RMS et vous disposez toujours d’un point de connexion de service sur votre réseau. Après la réinitialisation du client, l’ordinateur doit réexécuter ce script.
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC

- L’utilisateur actuellement connecté est déconnecté.

#### <a name="client-status-section"></a>Section **État du client**

Utilisez la valeur **Connecté en tant que** pour confirmer que le nom d’utilisateur affiché identifie le compte à utiliser pour l’authentification avec Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory. Le compte doit également appartenir à un client Office 365 configuré pour les étiquettes de sensibilité dans votre portail de gestion des étiquettes.

Si vous devez vous connecter en tant qu’utilisateur différent de celui qui est affiché, consultez les instructions [se connecter en tant qu’utilisateur différent](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user) .

Utilisez l’information **Version** pour vérifier la version installée sur le client. Vous pouvez vérifier s’il s’agit de la version la plus récente, ainsi que des correctifs et des nouvelles fonctionnalités correspondants en lisant les [informations](unifiedlabelingclient-version-release-history.md) de version du client.

## <a name="support-for-multiple-languages"></a>Prise en charge de plusieurs langues

Le client d’étiquetage unifié Azure Information Protection prend en charge les mêmes langues que celles prises en charge par Office 365. Pour obtenir la liste de ces langues, consultez la section **Office 365, Exchange Online Protection et Power BI** dans la page [Disponibilité internationale](https://products.office.com/business/international-availability) des produits Office.

Pour ces langues, les options de menu, les boîtes de dialogue et les messages de l’Azure Information Protection client d’étiquetage unifié s’affichent dans la langue de l’utilisateur. Il existe un programme d’installation unique qui détecte la langue, de sorte qu’aucune configuration supplémentaire n’est requise pour installer le client d’étiquetage unifié Azure Information Protection pour différentes langues. 

Toutefois, les noms et les descriptions d’étiquette que vous spécifiez ne sont pas traduits automatiquement lorsque vous configurez des étiquettes dans votre centre d’étiquetage. Pour que les utilisateurs puissent voir les étiquettes dans leur langue par défaut, fournissez vos propres traductions et configurez-les pour les étiquettes à l’aide de à l’aide d’Office 365 Security & Compliance PowerShell et du paramètre *LocaleSettings* pour [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps). Les marquages visuels ne sont pas traduits et ne prennent pas en charge plusieurs langues.

## <a name="post-installation-tasks"></a>Tâches post-installation

Après avoir installé le client d’étiquetage unifié Azure Information Protection, assurez-vous de fournir aux utilisateurs des instructions sur la façon d’étiqueter leurs documents et e-mails, ainsi que des conseils sur les étiquettes à choisir pour des scénarios spécifiques. Exemple :

- Instructions en ligne pour l’utilisateur : [Guide de l’utilisateur d’étiquetage unifié Azure Information Protection](clientv2-user-guide.md)

- Téléchargez un guide d’utilisation personnalisable : [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="installing-the-azure-information-protection-scanner"></a>Installation du scanneur Azure Information Protection

La version actuelle du scanneur pour le client d’étiquetage unifié est en version préliminaire pour le test. Au cours de cette version préliminaire, installez la préversion actuelle du client d’étiquetage unifié à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Si vous installez le scanneur pour la première fois sur un ordinateur, téléchargez et installez ce client, puis suivez les instructions de [la procédure de déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](../deploy-aip-scanner.md).

Si vous mettez à niveau le scanneur à partir du client Azure Information Protection (Classic), consultez la section [Upgrading the Azure information protection scanner](#upgrading-the-azure-information-protection-scanner) pour obtenir des instructions.

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>Mise à niveau et maintenance du client d’étiquetage unifié Azure Information Protection

> [!NOTE]
> Le client d’étiquetage unifié Azure Information Protection prend en charge la mise à niveau du client Azure Information Protection (Classic), ainsi que la mise à niveau à partir de versions précédentes du client d’étiquetage unifié Azure Information Protection.

L’équipe Azure Information Protection met régulièrement à jour le Azure Information Protection client d’étiquetage unifié pour les nouvelles fonctionnalités et les nouveaux correctifs. Les annonces sont postées sur le [site Yammer](https://www.yammer.com/AskIPTeam) de l’équipe.

Si vous utilisez Windows Update, le client d’étiquetage unifié Azure Information Protection met automatiquement à niveau la version de disponibilité générale de ce client, quelle que soit la façon dont le client a été installé. Les nouvelles versions de client sont publiées dans le catalogue quelques semaines après le lancement.

Vous pouvez également mettre à niveau manuellement le client en téléchargeant la nouvelle version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Installez ensuite la nouvelle version pour mettre à niveau le client. Vous devez utiliser cette méthode pour mettre à niveau les versions préliminaires et si vous effectuez une mise à niveau à partir du client Azure Information Protection.

Si vous effectuez une mise à niveau à partir du client Azure Information Protection (Classic) sur Windows 7, toutes les applications Office redémarrent automatiquement au cours de la mise à niveau du client. Ce redémarrage automatique ne s’applique pas aux systèmes d’exploitation ultérieurs, ou si vous effectuez une mise à niveau à partir d’une version antérieure du client d’étiquetage unifié.

Lorsque vous mettez à niveau manuellement, ne désinstallez la version précédente que si vous changez de méthode d’installation. Par exemple, si vous passez de la version du fichier exécutable (.exe) du client à la version du programme d’installation (.msi) Windows du client. Ou si vous devez installer une version antérieure du client. Par exemple, vous avez installé la préversion actuelle pour la tester et vous devez maintenant revenir à la version actuelle en disponibilité générale.

Utilisez l' [historique des versions et la stratégie de support](unifiedlabelingclient-version-release-history.md) pour comprendre la stratégie de prise en charge pour le client d’étiquetage unifié Azure information protection, les versions actuellement prises en charge et les nouveautés et modifications des versions prises en charge. 

### <a name="upgrading-the-azure-information-protection-scanner"></a>Mise à niveau du scanneur Azure Information Protection

Si vous utilisez actuellement le scanneur de Azure Information Protection à partir du client Azure Information Protection (Classic), vous pouvez le mettre à niveau pour utiliser des types d’informations sensibles et des étiquettes de sensibilité publiées à partir de la & de sécurité d’Office 365 Le centre de conformité (ou le Microsoft 365 Security Center ou le centre de conformité Microsoft 365).

#### <a name="to-upgrade-the-scanner-to-the-preview-version"></a>Pour mettre à niveau le scanneur vers la version préliminaire

La procédure de mise à niveau du scanneur dépend de la version du client Azure Information Protection (Classic) en cours d’exécution :

- [Mettre à niveau à partir de la version 1.48.204.0 et versions ultérieures](#upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client)

- [Mise à niveau à partir de versions antérieures à 1.48.204.0](#upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040)

Notez que contrairement au scanneur du client Azure Information Protection (Classic), cette version préliminaire du scanneur du client unifié ne prend pas en charge l’exécution sur un ordinateur déconnecté.

La mise à niveau crée une nouvelle base de données nommée **\<AIPScannerUL_ profile_name >** , et la base de données de l’analyseur précédente est conservée au cas où vous en aurez besoin pour la version précédente. Si vous êtes certain que vous n’avez pas besoin de la base de données de l’analyseur précédente, vous pouvez la supprimer. Étant donné que la mise à niveau crée une nouvelle base de données, le moteur de base de données analyse tous les fichiers la première fois qu’elle est exécutée.

##### <a name="upgrade-from-the-azure-information-protection-client-classic-version-1482040-and-later-versions-of-this-client"></a>Mettre à niveau à partir de Azure Information Protection la version 1.48.204.0 client (Classic) version et versions ultérieures de ce client

1. Sur l’ordinateur du scanneur, arrêtez le service du scanneur, **Scanneur Azure Information Protection**.

2. Effectuez une mise à niveau vers le client d’étiquetage unifié Azure Information Protection en téléchargeant et en installant la version préliminaire du client d’étiquetage unifield à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

3. Dans une session PowerShell, exécutez la commande Update-AIPScanner avec le profil de votre scanneur. Par exemple : `Update-AIPScanner –Profile Europe`.
    
    Cette étape permet de créer une base de données portant le nom **\<AIPScannerUL_ profile_name >**

4. Redémarrez le service **Scanneur Azure Information Protection**.

Vous pouvez maintenant utiliser le reste des instructions dans [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](../deploy-aip-scanner.md), en omettant l’étape d’installation du scanneur. Étant donné que le scanneur est déjà installé, il n’y a aucune raison de l’installer à nouveau.

##### <a name="upgrade-from-the-azure-information-protection-client-classic-versions-earlier-than-1482040"></a>Mise à niveau à partir des versions du client Azure Information Protection (Classic) antérieures à 1.48.204.0

> [!IMPORTANT]
> Pour un chemin de mise à niveau sans heurts, n’installez pas le client d’étiquetage unifié Azure Information Protection sur l’ordinateur exécutant le scanneur comme première étape de mise à niveau du scanneur. Utilisez plutôt les instructions de mise à niveau suivantes.

À partir de la version 1.48.204.0, le scanneur obtient ses paramètres de configuration à partir du Portail Azure, à l’aide d’un profil de configuration. La mise à niveau du scanneur implique de demander au scanneur d’utiliser cette configuration en ligne et le client d’étiquetage unifié. la configuration hors connexion pour le scanneur n’est pas prise en charge.

1. Utilisez le portail Azure pour créer un nouveau profil de scanneur qui inclut des paramètres pour le scanneur et vos référentiels de données avec tous les paramètres dont ils ont besoin. Pour obtenir de l’aide pour cette étape, consultez la section [configurer le scanneur dans la portail Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal) dans les instructions de déploiement de l’analyseur.

2. Sur l’ordinateur du scanneur, arrêtez le service du scanneur, **Scanneur Azure Information Protection**.

3. Effectuez une mise à niveau vers le client d’étiquetage unifié Azure Information Protection en téléchargeant et en installant la version préliminaire du client d’étiquetage unifié à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

4. Dans une session PowerShell, exécutez la commande Update-AIPScanner avec le même nom de profil que vous avez spécifié à l’étape 1. Par exemple : `Update-AIPScanner –Profile Europe`

5. Redémarrez le service **Scanneur Azure Information Protection**.

Vous pouvez maintenant utiliser le reste des instructions dans [déploiement de l’analyseur de Azure information protection pour classifier et protéger automatiquement les fichiers](../deploy-aip-scanner.md), en omettant l’étape d’installation du scanneur. Étant donné que le scanneur est déjà installé, il n’y a aucune raison de l’installer à nouveau.

###### <a name="upgrading-in-a-different-order-to-the-recommended-steps"></a>Mise à niveau selon une séquence différente des étapes recommandées

Lorsque vous effectuez une mise à niveau à partir d’une version antérieure à 1.48.204.0 et que vous ne configurez pas le scanneur dans le Portail Azure avant d’exécuter la commande Update-AIPScanner, vous n’avez pas de nom de profil à spécifier pour identifier les paramètres de configuration de votre analyseur pour la mise à niveau traiter. 

Dans ce scénario, lorsque vous configurez le scanneur dans le portail Azure, vous devez spécifier exactement le même nom de profil que celui utilisé lors de l’exécution de la commande Update-AIPScanner. Si le nom ne correspond pas, le scanneur ne sera pas configuré pour vos paramètres. 

> [!TIP]
> Pour identifier les scanneurs dont la configuration est incorrecte, utilisez le panneau **Azure Information Protection - Nœuds** dans le portail Azure.
>  
> Pour les scanneurs disposant d’une connexion Internet, ils affichent le nom de leur ordinateur avec le numéro de version GA du client Azure Information Protection, mais aucun nom de profil. Seuls les scanneurs portant le numéro de version 1.41.51.0 ne doivent pas afficher de nom de profil dans ce panneau. 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>Désinstallation du client d’étiquetage unifié Azure Information Protection

Vous pouvez utiliser l’une des options suivantes pour désinstaller le client :

- Utiliser le Panneau de configuration pour désinstaller un programme : Cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez l’exécutable (par exemple, **AzInfoProtection_UL. exe**) et, à partir de la page **modifier l’installation** , cliquez sur **désinstaller**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Étapes suivantes
Pour installer le client, consultez [installer le client d’étiquetage unifié Azure information protection pour les utilisateurs](clientv2-admin-guide-install.md).

Si vous avez déjà installé le client, consultez les informations supplémentaires suivantes sur la prise en charge de ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


