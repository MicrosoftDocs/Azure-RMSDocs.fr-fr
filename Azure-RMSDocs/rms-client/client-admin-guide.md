---
title: "Guide de l’administrateur du client Azure Information Protection | Azure Information Protection"
description: "Instructions et informations destinées aux administrateurs d’un réseau d’entreprise en charge du déploiement du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f82c7964b16ad984ad920059e2f61f19ad0f471a
ms.openlocfilehash: dff30520c149c29663c340b70a12c427b31659b9


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

Le client Azure Information Protection est plus adapté pour fonctionner avec ses services Azure ; Azure Information Protection et son service de protection des données, Azure Rights Management. Toutefois, avec certaines restrictions, le client Azure Information Protection fonctionne également avec la version locale de Rights Management, AD RMS. Pour une comparaison complète des fonctionnalités prises en charge par Azure Information Protection et AD RMS, consultez [Comparaison d’Azure Information Protection avec AD RMS](../understand-explore/compare-azure-rms-ad-rms.md). Si vous avez AD RMS et que vous souhaitez migrer AD RMS vers Azure Information Protection, consultez [Migration d’AD RMS vers Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

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

![Barre Azure Information Protection avec la stratégie par défaut](../media/info-protect-bar-default.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>Procédure d’installation du client Azure Information Protection pour les utilisateurs

Avant d’installer le client, vérifiez que vous disposez des versions et des applications nécessaires du système d’exploitation pour le client Azure Information Protection : [Configuration requise pour Azure Information Protection](../get-started/requirements-azure-rms.md). 

De plus :

- L’installation complète du client Azure Information Protection requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de télécharger et d’installer ce composant requis. Lorsque ce composant requis est installé dans le cadre de l’installation du client, l’ordinateur doit être redémarré.

- Si la visionneuse Azure Information Protection est installée séparément, une version minimale de Microsoft .NET Framework 4.5.2 est requise. Si cette version est manquante, le programme d’installation ne procède pas au téléchargement ni à l’installation.

- Les ordinateurs exécutant Windows 7 Service Pack 1 nécessitent [KB2533623](https://support.microsoft.com/en-us/kb/2533623) qui peut être installé après l’installation du client. Si cette mise à jour est requise et qu’elle n’est pas installée, vous êtes invité à l’installer.

> [!NOTE]
> L’installation nécessite des autorisations administratives locales.

Outre les instructions suivantes, le client Azure Information Protection est également inclus dans le catalogue Microsoft Update, ce qui vous permet d’installer et de mettre à jour ce client à l’aide de n’importe quel service de mise à jour de logiciel utilisant le catalogue. 

1. Téléchargez le client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

2. Pour une installation par défaut, exécutez simplement le fichier exécutable, **AzInfoProtection.exe**. Toutefois, pour afficher les options d’installation, commencez par exécuter le fichier exécutable avec **/Help** : `AzInfoProtection.exe /help`

   Exemple pour installer le client en mode silencieux : `AzInfoProtection.exe /quiet`
   
   Exemple d’installation silencieuse unique des applets de commande PowerShell :`AzInfoProtection.exe  PowerShellOnly=true /quiet`
   
   En outre, si vous installez le client sur des ordinateurs exécutant Office 2010, vous devez spécifier le paramètre **ServiceLocation** (non inclus dans l’écran d’aide) si vos utilisateurs ne sont pas des administrateurs locaux sur leurs ordinateurs. Pour plus d'informations, consultez la section suivante.

3. En cas d’installation interactive, sélectionnez l’option d’installation d’une **stratégie de démonstration** si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation.
    
4. Pour achever l'installation : 

    - Si votre ordinateur exécute Office 2010, redémarrez-le. 
        
        Si le client n’était pas installé avec le paramètre ServiceLocation, lorsque vous commencez par ouvrir l’une des applications Office qui utilise la barre Azure Information Protection (par exemple, Word), vous devez confirmer les invites pour mettre à jour le Registre pour cette première utilisation. La fonction [Détection du service](../rms-client/client-deployment-notes.md#rms-service-discovery) est utilisée pour remplir les clés de registre. 
    
    - Pour les autres versions d’Office, redémarrez les applications Office et toutes les instances de l’Explorateur de fichiers. 
        


### <a name="additional-instructions-for-office-2010-only"></a>Instructions supplémentaires pour Office 2010 uniquement

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


## <a name="to-uninstall-the-azure-information-protection-client"></a>Désinstallation du client Azure Information Protection

Choisissez l’une des méthodes suivantes :

- Utilisez le panneau de configuration pour désinstaller un programme : cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez le fichier exécutable (par exemple, **AzInfoProtection.exe**) et dans la page **Modifier l’installation**, cliquez sur **Désinstaller**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-send-feedback"></a>Vérification de l’installation et de l’état de la connexion, ou envoi de commentaires

1. Ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**.

2. Notez les éléments suivants dans la boîte de dialogue **Microsoft Azure Information Protection** :

    - Dans la section **état du client** : utilisez la valeur de **Version** pour vérifier que l’installation a réussi. En outre, vous voyez quand le client s’est connecté pour la dernière fois au service Azure Information Protection et quand la stratégie Azure Information Protection a été installée ou mise à jour pour la dernière fois. Lorsque le client se connecte au service, il télécharge automatiquement la dernière stratégie s’il détecte des modifications dans sa stratégie actuelle. Si vous avez apporté des modifications à la stratégie après l’heure affichée, fermez et rouvrez l’application Office.
    
        Vous voyez aussi votre nom d’utilisateur qui identifie le compte utilisé pour vous authentifier auprès d’Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory et qui appartient à un locataire configuré pour Azure Information Protection.

    - Dans la section **Aide et commentaires** : le **lien En savoir plus** pointe par défaut vers le site web [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection), mais vous pouvez le configurer pour qu’il pointe vers une URL personnalisée dans le cadre des [paramètres de la stratégie](../deploy-use/configure-policy-settings.md) Azure Information Protection.
        
        Utilisez le lien **Envoyer des commentaires** pour envoyer des suggestions ou des requêtes à l’équipe Information Protection. N’utilisez pas cette option pour le support technique, mais consultez plutôt [Options de support technique et ressources de la communauté](../get-started/information-support.md#support-options-and-community-resources). 
    
        Pour des informations de diagnostic et pour réinitialiser le client, cliquez sur **Exécuter les diagnostics**. Quand les tests de diagnostic sont terminés, cliquez sur **Copier les résultats** pour coller les informations dans un e-mail que vous pouvez envoyer à votre support technique ou au support technique Microsoft. Une fois les tests terminés, vous pouvez aussi réinitialiser le client.
        
        Plus d’informations sur l’option **Reset** :
        
        - Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 
        
        - Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers de **%localappdata%\Microsoft\MSIPC**, qui est l’emplacement où les certificats clients et les modèles de gestion des droits sont stockés. Elle ne supprime pas la stratégie Azure Information Protection ni les fichiers journaux du client, et elle ne déconnecte pas l’utilisateur.
        
        - La clé et les paramètres de Registre suivants sont supprimés : **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si vous configurez des paramètres pour cette clé de Registre (par exemple des paramètres pour la redirection de votre locataire Azure Information Protection car vous migrez depuis AD RMS et vous avez toujours un point de connexion de service sur votre réseau), vous devez reconfigurer les paramètres du Registre après avoir réinitialisé le client.
        
        - Après avoir réinitialisé le client, vous devez réinitialiser l’environnement utilisateur (opération également appelée « amorçage »), ce qui télécharge des certificats pour le client et les derniers modèles. Pour cela, fermez toutes les instances d’Office et redémarrez une application Office. Cette action vérifie également que vous avez téléchargé la dernière stratégie Azure Information Protection. Ne réexécutez pas les tests de diagnostic tant que vous n’avez pas fait ceci.


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez installé le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


