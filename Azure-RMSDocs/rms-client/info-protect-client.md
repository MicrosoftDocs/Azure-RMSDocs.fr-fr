---
title: Installation du client Azure Information Protection | Azure Information Protection
description: "Instructions pour installer le client qui ajoute une barre Information Protection à vos applications Office, à partir de laquelle vous pouvez sélectionner des étiquettes de classification pour vos documents et e-mails."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 23c437479c756f2a9335606e686f117d514a38f6
ms.openlocfilehash: 71972b0a057b1958dfa5e5b4af41b65d5080a086


---

# <a name="installing-the-azure-information-protection-client"></a>Installation du client Azure Information Protection

>*S’applique à : Azure Information Protection*

Pour classer les documents et les e-mails à l’aide d’Azure Information Protection, vous devez d’abord installer le client Azure Information Protection client. Cette installation ajoute une barre Information Protection à vos applications Office (Word, Excel, PowerPoint, Outlook), qui affiche les étiquettes de classification pour votre organisation, en plus d’un nouveau groupe **Protection** dans l’onglet **Accueil** (Word, Excel, PowerPoint), qui contient un bouton nommé **Protéger** :

L’illustration suivante montre cette barre Information Protection et les étiquettes de la [stratégie par défaut](../deploy-use/configure-policy-default.md) :

![Barre Azure Information Protection avec la stratégie par défaut](../media/info-protect-bar-default.png)

Téléchargez le client Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Actuellement, vous pouvez installer la version en disponibilité générale et la préversion. La préversion inclut de nouvelles fonctionnalités à des fins d’évaluation et est susceptible de changer. Pour plus d’informations, consultez le billet de blog suivant sur la disponibilité de la [préversion de décembre d’Azure Information protection](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/).

Avant d’installer le client, vérifiez que vous disposez des versions et des applications nécessaires du système d’exploitation pour le client Azure Information Protection : [Configuration requise pour Azure Information Protection](../get-started/requirements-azure-rms.md). De plus, pour la préversion du client, les ordinateurs exécutant Windows 7 SP1 nécessitent [KB 2533623](https://support.microsoft.com/en-us/kb/2533623), lequel peut être installé une fois le client lui-même installé. Si cette mise à jour est requise et qu’elle n’est pas installée, vous serez invité à l’installer.

## <a name="to-install-the-azure-information-protection-client-manually"></a>Installation manuelle du client Azure Information Protection

1. Après avoir [téléchargé le client](https://www.microsoft.com/en-us/download/details.aspx?id=53018), exécutez le fichier exécutable comme **AzInfoProtection.exe** et suivez les invites pour installer le client. Cette installation nécessite des autorisations administratives locales.

    Sélectionnez l’option d’installation d’une stratégie de démonstration si vous ne pouvez pas vous connecter à Office 365 ou Azure Active Directory mais souhaitez évaluer l’expérience avec le client Azure Information Protection à l’aide d’une stratégie locale à des fins de démonstration. Lorsque votre client se connecte à un service Azure Information Protection, cette stratégie de démonstration est remplacée par la stratégie Azure Information Protection de votre organisation. 

2. Pour commencer à utiliser le client Azure Information Protection : si votre ordinateur exécute Office 2010, redémarrez votre ordinateur. Pour d’autres versions d’Office, redémarrez les applications Office.

## <a name="to-install-the-azure-information-protection-client-for-users"></a>Installation du client Azure Information Protection pour des utilisateurs

Vous pouvez créer un script pour automatiser l’installation du client Azure Information Protection à l’aide d’options de ligne de commande. Pour afficher les options d’installation, exécutez le fichier exécutable avec **/help**. Par exemple : `AzInfoProtection.exe /help`.

Exemple pour installer le client en mode silencieux : `AzInfoProtection.exe /passive | quiet`

La version en disponibilité générale du client Azure Information Protection est également incluse dans le catalogue Microsoft Update, ce qui vous permet d’installer et de mettre à jour ce client à l’aide de n’importe quel service de mise à jour de logiciel utilisant le catalogue. Les préversions du client ne sont pas incluses dans le catalogue Microsoft Update.

## <a name="to-uninstall-the-azure-information-protection-client"></a>Désinstallation du client Azure Information Protection

Choisissez l’une des méthodes suivantes :

- Utilisez le panneau de configuration pour désinstaller un programme : cliquez sur **Microsoft Azure Information Protection** > **Désinstaller**

- Réexécutez le fichier exécutable (par exemple, **AzInfoProtection.exe**) et dans la page **Modifier l’installation**, cliquez sur **Désinstaller**. 

- Exécutez le fichier exécutable avec **/uninstall**. Par exemple : `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>Vérification de l’installation et de l’état de la connexion, ou signalisation d’un problème

1. Ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**.

2. Notez les éléments suivants dans la boîte de dialogue **Microsoft Azure Information Protection** :

    - Dans la section **état du client** : utilisez la valeur de **Version** pour vérifier que l’installation a réussi. En outre, vous voyez quand le client s’est connecté pour la dernière fois au service Azure Information Protection et quand la stratégie Azure Information Protection a été installée ou mise à jour pour la dernière fois. Lorsque le client se connecte au service, il télécharge automatiquement la dernière stratégie s’il détecte des modifications dans sa stratégie actuelle. Si vous avez apporté des modifications à la stratégie après l’heure affichée, fermez et rouvrez l’application Office.
    
        Vous voyez aussi votre nom d’utilisateur qui identifie le compte utilisé pour vous authentifier auprès d’Azure Information Protection. Ce nom d’utilisateur doit correspondre à un compte que vous utilisez pour Office 365 ou Azure Active Directory et qui appartient à un locataire configuré pour Azure Information Protection.

    - Dans la section **Aide et commentaires** : le **lien En savoir plus** pointe par défaut vers le site web [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection), mais vous pouvez le configurer pour qu’il pointe vers une URL personnalisée dans le cadre des [paramètres de la stratégie](../deploy-use/configure-policy-settings.md) Azure Information Protection.
        
        Utilisez le lien **Envoyer des commentaires** pour joindre automatiquement les journaux de votre client à un e-mail qui peut être envoyé à l’équipe d’Information Protection en vue d’examiner un problème. 
    
        Pour des informations de diagnostic et pour réinitialiser le client, cliquez sur **Exécuter les diagnostics**. Quand les tests de diagnostic sont terminés, cliquez sur **Copier les résultats** pour coller les informations dans un e-mail que vous pouvez envoyer à votre support technique ou au support technique Microsoft. Une fois les tests terminés, vous pouvez aussi réinitialiser le client.
        
        Plus d’informations sur l’option **Reset** :
        
        - Il n’est pas obligatoire d’être un administrateur local pour utiliser cette option, et cette action n’est pas enregistrée dans l’Observateur d’événements. 
        
        - Sauf si des fichiers sont verrouillés, cette action supprime tous les fichiers de **%localappdata%\Microsoft\MSIPC**, qui est l’emplacement où les certificats clients et les modèles de gestion des droits sont stockés. Elle ne supprime pas la stratégie Azure Information Protection ni les fichiers journaux du client, et elle ne déconnecte pas l’utilisateur.
        
        - La clé et les paramètres de Registre suivants sont supprimés : **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC**. Si vous configurez des paramètres pour cette clé de Registre (par exemple des paramètres pour la redirection de votre locataire Azure Information Protection car vous migrez depuis AD RMS et vous avez toujours un point de connexion de service sur votre réseau), vous devez reconfigurer les paramètres du Registre après avoir réinitialisé le client.
        
        - Après avoir réinitialisé le client, vous devez réinitialiser l’environnement utilisateur (opération également appelée « amorçage »), ce qui télécharge des certificats pour le client et les derniers modèles. Pour cela, fermez toutes les instances d’Office et redémarrez une application Office. Cette action vérifie également que vous avez téléchargé la dernière stratégie Azure Information Protection. Ne réexécutez pas les tests de diagnostic tant que vous n’avez pas fait ceci.


## <a name="usage-logging"></a>Journalisation de l’utilisation

**[ Cette fonctionnalité requiert la préversion du client et est susceptible d’être modifiée. ]**

Pour la préversion du client Azure Information Protection, le client enregistre l’activité de l’utilisateur dans le journal des événements **Applications et services** Windows local, **Azure Information Protection**. Les événements incluent les informations suivantes :

- Date, version du client, ID de stratégie

- Nom d’utilisateur, nom d’ordinateur connectés

- Nom et emplacement de fichier

- Action :

    - Définir l’étiquette : ID d’informations 101
    
    - Définir l’étiquette (inférieure) : ID d’informations 102
    
    - Définir l’étiquette (supérieure) : ID d’informations 103
    
    - Supprimer l’étiquette : ID d’informations 104
   
    - Astuce recommandée : ID d’informations 105
    
    - Appliquer la protection personnalisée : ID d’informations 201
    
    - Supprimer la protection personnalisée : ID d’informations 202
    
    - Connexion (opérationnelle) : ID d’informations 902
    
    - Télécharger la stratégie (opérationnelle) : ID d’informations 901
    
- Source de l’action :
    
    - Manuel 
    
    - Recommandé
    
    - Automatique  
    
    - Système (pour la stratégie de connexion et de téléchargement)
    
- Étiquette avant et après l’action 
    
- Protection avant et après l’action
    
- Justification de l’utilisateur (le cas échéant)
    

## <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Raccourcis clavier de la barre Azure Information Protection

Pour accéder à la barre Azure Information Protection à l’aide du clavier, utilisez la combinaison de touches suivante :

- Appuyez sur **Ctrl** + **Maj** + **~** 

Utilisez ensuite la touche de tabulation pour sélectionner les étiquettes et autres commandes de la barre (icônes **Masquer les étiquettes** et **Supprimer les étiquettes**), puis appuyez sur la touche Entrée pour les sélectionner.


## <a name="file-locations"></a>Emplacements des fichiers

Fichiers du client :   

- Pour les systèmes d’exploitation 64 bits : **\ProgramFiles (x86) \Microsoft Azure Information Protection**

- Pour les systèmes d’exploitation 32 bits : **\Program Files\Microsoft Azure Information Protection**

Fichiers journaux du client et fichier de stratégie actuellement installé :

- Pour les systèmes d’exploitation 64 bits et 32 bits : **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>Étapes suivantes

Pour modifier les étiquettes dans la barre Information Protection, vous devez configurer la stratégie Azure Information Protection. Pour en savoir plus, consultez [Configuration de la stratégie Azure Information Protection](../deploy-use/configure-policy.md).

Pour obtenir un exemple montrant comment personnaliser la stratégie par défaut et voir le comportement qui en résulte dans une application Office, essayez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Pour vérifier les informations de version pour le client, consultez l’[historique des versions](client-version-release-history.md).



<!--HONumber=Dec16_HO1-->


