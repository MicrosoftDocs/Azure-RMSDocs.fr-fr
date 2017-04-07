---
title: "Guide de l’administrateur du client Azure Information Protection"
description: "Instructions et informations destinées aux administrateurs d’un réseau d’entreprise en charge du déploiement du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 63843acfe9f7b4ded77ccbdcaaab8cb98598dd9f
ms.sourcegitcommit: 8733730882bea6f505f4c6d53d4bdf08c3106f40
translationtype: HT
---
# <a name="azure-information-protection-client-administrator-guide"></a>Guide de l’administrateur du client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*


Utilisez les informations suivantes si vous êtes responsable du client Azure Information Protection sur un réseau d’entreprise, ou si vous souhaitez des informations techniques supplémentaires par rapport au [Guide de l’administrateur du client Azure Information Protection](client-user-guide.md).

Le client Azure Information Protection inclut les éléments suivants :

- Un module complémentaire Office, qui installe la barre Azure Information Protection pour que les utilisateurs sélectionnent des étiquettes de classification, et un bouton **Protéger** sur le ruban pour les autres options.

- L’Explorateur de fichiers Windows, avec des options contextuelles permettant aux utilisateurs d’appliquer des étiquettes de classification et la protection aux fichiers.

- Une visionneuse pour afficher les fichiers protégés lorsqu’une application native ne peut pas les ouvrir.

- Un module PowerShell pour appliquer et supprimer des étiquettes de classification et la protection de fichiers.

- Le client Rights Management qui communique avec Azure Rights Management (Azure RMS) ou Active Directory Rights Management Services (AD RMS).

Le client Azure Information Protection est plus adapté pour fonctionner avec ses services Azure ; Azure Information Protection et son service de protection des données, Azure Rights Management. Toutefois, avec certaines restrictions, le client Azure Information Protection fonctionne également avec la version locale de Rights Management, AD RMS. Pour une comparaison complète des fonctionnalités prises en charge par Azure Information Protection et AD RMS, consultez [Comparaison d’Azure Information Protection avec AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). 

Si vous avez AD RMS et que vous souhaitez migrer AD RMS vers Azure Information Protection, consultez [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

**Vous avez une question qui n’est pas traitée dans cette documentation ?** Visitez notre [site Yammer Azure Information Protection](https://www.yammer.com/AskIPTeam). 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>Devez-vous déployer le client Azure Information Protection ?

Déployez le client Azure Information Protection si l’une des situations suivantes s’applique :

- Vous souhaitez classifier (et éventuellement protéger) des documents et des e-mails en sélectionnant des étiquettes à partir de vos applications Office (Word, Excel, PowerPoint, Outlook).

- Vous souhaitez classifier (et éventuellement protéger) des documents et des e-mails à l’aide de l’Explorateur de fichiers, qui prend en charge des types de fichiers supplémentaires, des sélections multiples et des dossiers.

- Vous souhaitez exécuter des scripts qui classifient (et éventuellement protègent) des documents à l’aide de commandes PowerShell.

- Vous souhaitez afficher des documents protégés lorsqu’une application native permettant d’afficher le fichier n’est pas installée ou ne parvient pas à ouvrir ces documents.

- Vous souhaitez uniquement protéger les fichiers à l’aide de l’Explorateur de fichiers ou des commandes PowerShell.

- Vous souhaitez que les utilisateurs et administrateurs soient en mesure de suivre et de révoquer des documents protégés.

- Voulez-vous supprimer le chiffrement des fichiers et des conteneurs (annuler la protection) en bloc aux fins de récupération des données.

- Vous exécutez Office 2010 et souhaitez protéger des documents et des e-mails à l’aide du service Azure Rights Management.

Exemple illustrant le complément Client Azure Information Protection dans une application Office, affichant les étiquettes de classification pour votre organisation, ainsi que le nouveau bouton **Protéger** sur le ruban :

![Barre Azure Information Protection avec la stratégie par défaut](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Procédure d’installation du client Azure Information Protection pour les utilisateurs

Avant d’installer le client, vérifiez que vous disposez des versions et des applications nécessaires du système d’exploitation pour le client Azure Information Protection : [Configuration requise pour Azure Information Protection](../get-started/requirements-azure-rms.md). 

Prérequis supplémentaires pour le client Azure Information Protection :

- L’installation complète du client Azure Information Protection par défaut requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré. Bien que cela ne soit pas conseillé, vous pouvez ignorer cette condition à l’aide d’un paramètre d’installation personnalisé.

- Si la visionneuse Azure Information Protection est installée séparément, une version minimale de Microsoft .NET Framework 4.5.2 est requise. Si cette version est manquante, le programme d’installation ne procède pas au téléchargement ni à l’installation.

- Le module PowerShell nécessite Windows PowerShell version 4.0, que vous devrez peut-être installer sur les systèmes d’exploitation plus anciens. Pour en savoir plus, consultez la page relative à [l’installation de Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx). Ce programme d’installation ne vérifie pas ou n’installe pas cette condition préalable pour vous. Pour vérifier la version de Windows PowerShell que vous exécutez, saisissez la chaîne **$PSVersionTable** lors d’une session PowerShell.

- Les ordinateurs exécutant Windows 7 SP1 requièrent KB 2533623. Pour plus d’informations, consultez [Avis de sécurité Microsoft : le chargement non sécurisé de bibliothèque peut permettre l’exécution de code à distance](https://support.microsoft.com/en-us/kb/2533623). Vous pouvez peut-être installer cette mise à jour directement, ou elle peut être remplacée par une autre qui l’installe pour vous.
    
    Si cette mise à jour est requise, mais qu’elle n’est pas installée, l’installation du client vous avertit qu’elle doit l’être. Cette mise à jour peut être installée après l’installation du client, mais certaines actions seront bloquées et le message s’affichera à nouveau.  

> [!NOTE]
> L’installation nécessite des autorisations administratives locales.

Le client Azure Information Protection est également inclus dans le catalogue Microsoft Update, ce qui vous permet d’installer et de mettre à jour le client à l’aide de n’importe quel service de mise à jour de logiciel utilisant le catalogue. 

1. Téléchargez le client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 
    
    Si une version préliminaire est disponible, conservez cette version à des fins de test uniquement. Elle n’est pas destinée aux utilisateurs finaux dans un environnement de production. 

2. Pour une installation par défaut, exécutez simplement le fichier exécutable, par exemple **AzInfoProtection.exe**. Toutefois, pour afficher les options d’installation, commencez par exécuter le fichier exécutable avec **/Help** : `AzInfoProtection.exe /help`

    Exemple pour installer le client en mode silencieux : `AzInfoProtection.exe /quiet`
    
    Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    Paramètres supplémentaires qui ne figurent pas sur l’écran d’aide :
    
    - **ServiceLocation** : utilisez ce paramètre si vous installez le client sur des ordinateurs exécutant Office 2010 et que vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs ou que vous ne voulez pas qu’ils reçoivent un message. [Plus d’informations](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement** : utilisez ce paramètre pour éviter d’avoir à disposer de Microsoft Framework .NET version 4.6.2. [Plus d’informations](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

3. En cas d’installation interactive, sélectionnez l’option d’installation d’une **stratégie de démonstration** si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.
    
4. Pour achever l'installation : 

    - Si votre ordinateur exécute Office 2010, redémarrez-le. 
        
        Si le client n’était pas installé avec le paramètre ServiceLocation, lorsque vous commencez par ouvrir l’une des applications Office qui utilise la barre Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le Registre pour cette première utilisation. La fonction [Détection du service](../rms-client/client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers. 
        
5. Vous pouvez vérifier que l’installation a réussi en consultant le fichier journal de l’installation, qui est créé par défaut dans le dossier %temp%. Vous pouvez modifier cet emplacement à l’aide du paramètre d’installation **/log**. 
 
    Le nom du fichier a pour format : `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`.
    
    Par exemple : **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    Dans ce fichier journal, recherchez la chaîne suivante : **Produit : Microsoft Azure Information Protection -- Installation effectuée.** En cas d’échec de l’installation, ce fichier journal contient des informations pour vous aider à identifier et résoudre les problèmes.

### <a name="more-information-about-the-servicelocation-installation-parameter"></a>Plus d’informations sur le paramètre d’installation ServiceLocation

Lorsque vous installez le client pour des utilisateurs disposant d’Office 2010 et qu’ils n’ont pas d’autorisations d’administrateur local, spécifiez le paramètre ServiceLocation et l’URL de votre service Azure Rights Management. Ce paramètre et la valeur créent et définissent les clés de registre suivantes :

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

Utilisez la procédure suivante pour identifier la valeur à spécifier pour le paramètre ServiceLocation. 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>Pour identifier la valeur à spécifier pour le paramètre ServiceLocation

1. À partir d’une session PowerShell, exécutez d’abord [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) et spécifiez vos informations d’identification d’administrateur pour vous connecter au service Azure Rights Management. Exécutez [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration). 
 
    Si vous n’avez pas encore installé le module PowerShell pour le service Azure Rights Management, consultez la section [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. Dans le résultat de l'applet de commande, identifiez la valeur **LicensingIntranetDistributionPointUrl**.

    Par exemple : **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. À partir de la valeur, supprimez la section **_wmcs/licensing** de cette chaîne. Par exemple : **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    La chaîne restante correspond à la valeur à spécifier pour le paramètre ServiceLocation.

Exemple d’installation du client en mode silencieux pour Office 2010 et Azure RMS : `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>Plus d’informations sur le paramètre d’installation DowngradeDotNetRequirement

Pour prendre en charge les mises à jour automatiques via Windows Update et pour s’intégrer de façon fiable avec les applications Office, le client Azure Information Protection utilise Microsoft .NET Framework version 4.6.2. Par défaut, l’installation vérifie que cette version est installée et essaie de l’installer si elle est manquante. L’installation nécessite le redémarrage de l’ordinateur.

Si l’installation de cette version de Microsoft .NET Framework ne vous arrange pas, vous pouvez installer le client en indiquant le paramètre et la valeur suivants **DowngradeDotNetRequirement=True**, ce qui permet de contourner cette exigence si la version 4.5.1 de Microsoft .NET Framework est installée.

Par exemple : `AzInfoProtection.exe DowngradeDotNetRequirement=True`

Nous vous recommandons d’utiliser ce paramètre avec précaution, car des problèmes ont été signalés avec les applications Office. Il arrive que celles-ci se bloquent lorsque le client Azure Information Protection est utilisé avec cette ancienne version de Microsoft .NET Framework. Si vous rencontrez des problèmes de blocage, installez la version recommandée avant d’essayer d’autres solutions de dépannage. 

N’oubliez pas que si vous utilisez Windows Update pour mettre le client Azure Information Protection à jour, vous devrez utiliser un autre mécanisme de déploiement de logiciels pour mettre à niveau le client vers des versions ultérieures.

## <a name="additional-checks-and-troubleshooting"></a>Vérifications supplémentaires et dépannage

Utilisez l’option **Aide et commentaires** pour ouvrir la boîte de dialogue **Microsoft Azure Information Protection** :

- Dans une application Office, sous l’onglet **Accueil**, dans le groupe **Protection**, sélectionnez **Protéger**, puis **Aide et commentaires**.

- Dans l’Explorateur de fichiers : cliquez avec le bouton droit sur un ou plusieurs fichiers ou sur un dossier, sélectionnez **Classifier et protéger**, puis **Aide et commentaires**. 

### <a name="help-and-feedback-section"></a>Section **Aide et commentaires**

Le **lien En savoir plus** pointe par défaut vers le site web [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection), mais vous pouvez le configurer pour qu’il pointe vers une URL personnalisée dans le cadre des [paramètres de la stratégie](../deploy-use/configure-policy-settings.md) Azure Information Protection.

Utilisez le lien **Envoyez-nous des commentaires** pour envoyer des suggestions ou des requêtes à l’équipe Information Protection. N’utilisez pas cette option pour le support technique, mais consultez plutôt [Options de support technique et ressources de la communauté](../get-started/information-support.md#support-options-and-community-resources). 

L’option **Exporter les journaux** permet de collecter et de joindre automatiquement des fichiers journaux pour le client Azure Information Protection si vous devez les envoyer au support technique Microsoft. Cette option peut également être utilisée par les utilisateurs finaux pour envoyer ces fichiers journaux à votre support technique.

Pour des informations de diagnostic et pour réinitialiser le client, sélectionnez **Exécuter les diagnostics**. Quand les tests de diagnostic sont terminés, cliquez sur **Copier les résultats** pour coller les informations dans un e-mail que vous pouvez envoyer au support technique Microsoft ou que vos utilisateurs finaux peuvent envoyer à votre support technique. Une fois les tests terminés, vous pouvez aussi réinitialiser le client.

Plus d’informations sur l’option **Reset** :

- Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 

- Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers de **%localappdata%\Microsoft\MSIPC**, qui est l’emplacement où les certificats clients et les modèles de gestion des droits sont stockés. Elle ne supprime pas la stratégie Azure Information Protection ni les fichiers journaux du client, et elle ne déconnecte pas l’utilisateur.

- La clé et les paramètres de Registre suivants sont supprimés : **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si vous configurez des paramètres pour cette clé de Registre (par exemple des paramètres pour la redirection de votre locataire Azure Information Protection car vous migrez depuis AD RMS et vous avez toujours un point de connexion de service sur votre réseau), vous devez reconfigurer les paramètres du Registre après avoir réinitialisé le client.

- Après avoir réinitialisé le client, vous devez réinitialiser l’environnement utilisateur, ce qui télécharge des certificats pour le client et les derniers modèles. Pour cela, fermez toutes les instances d’Office et redémarrez une application Office. Cette action vérifie également que vous avez téléchargé la dernière stratégie Azure Information Protection. Ne réexécutez pas les tests de diagnostic tant que vous n’avez pas fait ceci.


### <a name="client-status-section"></a>Section **État du client**

Utilisez la valeur **Connecté en tant que** pour confirmer que le nom d’utilisateur affiché identifie le compte à utiliser pour l’authentification avec Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte utilisé pour Office 365 ou Azure Active Directory qui appartient à un locataire configuré pour Azure Information Protection.

Si vous avez besoin de vous connecter avec un nom d’utilisateur différent de celui qui est affiché, consultez la section [Se connecter avec l’identité d’un autre utilisateur](#sign-in-as-a-different-user) sur cette page.

La valeur du paramètre **Dernière connexion** indique la dernière connexion du client au service Azure Information Protection de votre organisation et peut être utilisée avec les valeurs date et heure du paramètre **La stratégie Information Protection a été installée sur** pour vérifier quand la stratégie Azure Information Protection a été installée ou mise à jour pour la dernière fois. Lorsque le client se connecte au service, il télécharge automatiquement la dernière stratégie s’il détecte des modifications dans sa stratégie actuelle, ainsi que toutes les 24 heures. Si vous avez apporté des modifications à la stratégie après l’heure affichée, fermez et rouvrez l’application Office.

Si vous voyez le message **Ce client n’est pas sous licence pour Office Professionnel Plus** : le client Azure Information Protection a détecté que l’édition d’Office installée ne prend pas en charge l’application de la protection Rights Management. Si ce problème est détecté, les étiquettes qui appliquent la protection ne s’affichent pas dans la barre Azure Information Protection.

Utilisez l’information **Version** pour vérifier la version installée sur le client. Vous pouvez vérifier s’il s’agit de la dernière version et s’il existe des correctifs correspondants et des nouvelles fonctionnalités en cliquant sur le lien **Nouveautés** pour lire l’[historique de publication des versions](client-version-release-history.md) du client.

## <a name="custom-configurations"></a>Configurations personnalisées

Utilisez les informations suivantes pour les configurations avancées nécessaires pour des scénarios spécifiques ou un sous-ensemble d’utilisateurs. 

### <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs ne doivent généralement pas se connecter sous un autre nom lorsqu’ils utilisent le client Azure Information Protection. Toutefois, vous devrez peut-être le faire en tant qu’administrateur si vous disposez de plusieurs locataires. Par exemple, vous disposez d’un locataire test en plus du locataire Office 365 ou Azure utilisé par votre organisation.

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure Information Protection** : ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Vérifiez le nom de domaine du compte connecté qui s’affiche, en particulier lorsque vous utilisez un compte d’administrateur. Par exemple, si vous avez un compte d’administrateur dans deux locataires différents, il peut être facile d’oublier que vous êtes connecté avec un nom du compte correct mais dans un domaine incorrect. Vous pouvez vous en apercevoir en cas d’échec du téléchargement de la stratégie Azure Information Protection ou si vous ne voyez pas les étiquettes ou le comportement que vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. À l’aide d’un éditeur du Registre, accédez à **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** et supprimez la valeur **TokenCache** (et les données de valeur associées).

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si l’invite de connexion au service Azure Information Protection n’apparaît pas dans votre application Office, revenez à la boîte de dialogue **Microsoft Azure Information Protection** et cliquez sur **Connexion** depuis la section mise à jour **État du Client**.

En outre :

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir modifié le registre. Le client Azure Information Protection vous authentifiera automatiquement à l’aide du compte d’utilisateur connecté à ce moment-là.

- Si vous souhaitez réinitialiser l’environnement pour le service Azure Rights Management (également appelé amorçage), vous pouvez utiliser l’option **Réinitialiser** depuis [l’outil d’analyse RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437).

- Si vous souhaitez supprimer la stratégie Azure Information Protection actuellement téléchargée, supprimez le fichier **Policy.msip** du dossier **%localappdata%\Microsoft\MSIP**.

### <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Masquer l’option de menu Classifier et protéger dans l’Explorateur de fichiers Windows

Vous pouvez définir cette configuration avancée en modifiant le Registre lorsque vous disposez de la version 1.3.0.0 du client Azure Information Protection ou d’une version ultérieure. 

Créez le nom de la valeur DWORD suivant (avec toutes données de la valeur) :

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

### <a name="support-for-disconnected-computers"></a>Prise en charge des ordinateurs déconnectés

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection pour télécharger la dernière stratégie Azure Information Protection. Si vous disposez d’ordinateur qui ne sera pas en mesure de se connecter à Internet pendant une période donnée, vous pouvez empêcher le client d’essayer de se connecter au service en modifiant le Registre. 

Recherchez le nom de la valeur suivant et définissez les données de la valeur sur **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Assurez-vous que le client dispose d’un fichier de stratégie valide nommé **Policy.msip**, dans le dossier **%localappdata%\Microsoft\MSIP**. Si nécessaire, vous pouvez exporter la stratégie à partir du portail Azure et copier le fichier exporté sur l’ordinateur client. Vous pouvez également utiliser cette méthode pour remplacer un fichier de stratégie obsolète par la dernière stratégie publiée.

## <a name="to-uninstall-the-azure-information-protection-client"></a>Désinstallation du client Azure Information Protection

Choisissez l’une des méthodes suivantes :

- Utilisez le panneau de configuration pour désinstaller un programme : cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez le fichier exécutable (par exemple, **AzInfoProtection.exe**) et dans la page **Modifier l’installation**, cliquez sur **Désinstaller**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez installé le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
