---
title: "Configurations personnalisées pour le client Azure Information Protection"
description: Informations sur la personnalisation du client Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9e7e5e67b664d177f60a445aa54df3f6072ff9c7
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="custom-configurations-for-the-azure-information-protection-client"></a>Configurations personnalisées pour le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Utilisez les informations suivantes pour les configurations avancées nécessaires dont vous pourrez avoir besoin pour des scénarios spécifiques, ou pour un sous-ensemble d’utilisateurs lorsque vous gérez le client Azure Information Protection.

Certains de ces paramètres nécessitent une modification du Registre, et certains autres utilisent des paramètres avancés que vous devez configurer dans le portail Azure, puis publier pour les clients à télécharger. En outre, certains paramètres peuvent n’être disponibles que dans une préversion du client Azure Information Protection. Pour ces paramètres, il existe une documentation concernant la version minimale du client. Pour les paramètres et les configurations pris en charge dans la version publique du client, il n’existe aucune documentation relative à la version minimale du client.

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>Comment configurer les paramètres avancés de configuration du client dans le portail

Cette configuration est actuellement en préversion.

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général, puis accédez au panneau **Azure Information Protection**.

2. Dans le premier panneau Azure Information Protection, sélectionnez **Stratégies étendues**.

3. Dans la panneau **Azure Information Protection - Stratégies étendues**, sélectionnez le menu contextuel (**...**) à côté de la stratégie qui doit contenir les paramètres avancés. Ensuite, sélectionnez **Paramètres avancés**.
    
    Vous pouvez configurer des paramètres avancés pour la stratégie globale et pour les stratégies étendues.

4. Dans le panneau **Paramètres avancés**, tapez le nom et la valeur du paramètre avancé, puis sélectionnez **Enregistrer et fermer**.

5. Cliquez sur **Publier**, puis veillez à ce que les utilisateurs de cette stratégie redémarrent toutes les applications Office qu’ils avaient ouvertes.

6. Si vous n’avez plus besoin de ce paramètre et souhaitez rétablir le comportement par défaut : dans le panneau **Paramètres avancés**, sélectionnez le menu contextuel (**...**) à côté du paramètre dont vous n’avez plus besoin, puis sélectionnez **Supprimer**. Ensuite, cliquez sur **Enregistrer et fermer**, puis republier la stratégie modifiée.

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>Empêcher l’affichage des invites de connexion sur les ordinateurs AD RMS uniquement

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection. Pour les ordinateurs qui communiquent uniquement avec AD RMS, cette configuration peut entraîner inutilement l’affichage d’une invite de connexion pour les utilisateurs. Vous pouvez empêcher l’affichage de cette invite de connexion en modifiant le Registre :

Recherchez le nom de valeur suivant et définissez la valeur à **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indépendamment de ce paramètre, le client Azure Information Protection se conforme au [processus de découverte du service RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) pour trouver le cluster AD RMS associé.

## <a name="sign-in-as-a-different-user"></a>Se connecter avec l’identité d’un autre utilisateur

Dans un environnement de production, les utilisateurs ne doivent généralement pas se connecter sous un autre nom lorsqu’ils utilisent le client Azure Information Protection. Toutefois, en tant qu’administrateur, vous devrez peut-être vous connecter sous un autre nom d’utilisateur pendant une phase de test. 

Vous pouvez vérifier le compte auquel vous êtes actuellement connecté à l’aide de la boîte de dialogue **Microsoft Azure Information Protection** : ouvrez une application Office et, dans l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, puis sur **Aide et commentaires**. Votre nom de votre compte s’affiche dans la section **État du client**.

Pensez à vérifier le nom de domaine du compte connecté. En effet, vous pouvez accidentellement vous connecter avec le bon nom de compte, mais avec le mauvais domaine. Vous pouvez vous apercevoir que vous utilisez le mauvais compte en cas d’échec du téléchargement de la stratégie Azure Information Protection ou si vous ne voyez pas les étiquettes ou le comportement auxquels vous vous attendez.

Pour se connecter avec l’identité d’un autre utilisateur :

1. Selon la version du client Azure Information Protection : 
    
    - Pour obtenir la version grand public du client Azure Information Protection : à l’aide d’un éditeur du Registre, accédez à **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** et supprimez la valeur **TokenCache** (et les données de valeur associées).
    
    - Pour la préversion actuelle du client Azure Information Protection : accédez à **%localappdata%\Microsoft\MSIP** et supprimez le fichier **TokenCache**.

2. Redémarrez les applications Office ouvertes et connectez-vous avec votre autre compte d’utilisateur. Si l’invite de connexion au service Azure Information Protection n’apparaît pas dans votre application Office, revenez à la boîte de dialogue **Microsoft Azure Information Protection** et cliquez sur **Connexion** depuis la section mise à jour **État du Client**.

En outre :

- Cette solution prend en charge la connexion sous un nom d’utilisateur différent à partir du même locataire. Elle ne prend en pas charge la connexion sous un nom d’utilisateur différent à partir d’un autre locataire. Pour tester Azure Information Protection avec plusieurs locataires, utilisez des ordinateurs différents.

- Si vous utilisez l’authentification unique, vous devrez vous déconnecter de Windows et vous reconnecter avec votre autre compte d’utilisateur après avoir modifié le Registre. Le client Azure Information Protection peut alors vous authentifier automatiquement à l’aide du compte d’utilisateur connecté à ce moment-là.

- Si vous souhaitez réinitialiser les paramètres utilisateur pour le service Azure Rights Management, utilisez l’option **Aide et commentaires**.

- Si vous souhaitez supprimer la stratégie Azure Information Protection actuellement téléchargée, supprimez le fichier **Policy.msip** du dossier **%localappdata%\Microsoft\MSIP**.

- Si vous avez la préversion actuelle du client Azure Information Protection, vous pouvez utiliser l’option **Réinitialiser les paramètres** dans **Aide et commentaires** pour vous déconnecter et supprimer la stratégie Azure Information Protection téléchargée.

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>Masquer l’option de menu Classifier et protéger dans l’Explorateur de fichiers Windows

Cette configuration est actuellement en préversion.

Vous pouvez définir cette configuration avancée en modifiant le Registre lorsque vous disposez de la version 1.3.0.0 du client Azure Information Protection ou d’une version ultérieure. 

Créez le nom de la valeur DWORD suivant (avec toutes données de la valeur) :

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>Prise en charge des ordinateurs déconnectés

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection pour télécharger la dernière stratégie Azure Information Protection. Si vous disposez d’ordinateur qui ne sera pas en mesure de se connecter à Internet pendant une période donnée, vous pouvez empêcher le client d’essayer de se connecter au service en modifiant le Registre. 

Recherchez le nom de la valeur suivant et définissez les données de la valeur sur **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Vérifiez que le client a d’un fichier de stratégie valide nommé **Policy.msip** dans le dossier **%LocalAppData%\Microsoft\MSIP**. Si nécessaire, vous pouvez exporter la stratégie à partir du portail Azure et copier le fichier exporté sur l’ordinateur client. Vous pouvez également utiliser cette méthode pour remplacer un fichier de stratégie obsolète par la dernière stratégie publiée.

Quand vous exportez la stratégie, cette action télécharge un fichier compressé avec plusieurs versions de la stratégie qui correspondent à différentes versions du client Azure Information Protection :

1. Décompressez le fichier et utilisez le tableau suivant pour identifier le fichier de stratégie dont vous avez besoin. 
    
    |Nom du fichier|Version du client correspondante|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |version 1.2|
    |Policy1.2.msip |version 1.3 - 1.7|
    |Policy1.3.msip |version 1.8 et ultérieure|
    
2. Renommez le fichier identifié en **Policy.msip** et copiez-le dans le dossier **%LocalAppData%\Microsoft\MSIP** sur les ordinateurs où le client Azure Information Protection est installé. 


## <a name="hide-the-do-not-forward-button-in-outlook"></a>Masquer le bouton Ne pas transférer dans Outlook

Cette option de configuration est actuellement en préversion.

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. Ce paramètre nécessite également la préversion **1.8.41.0** du client Azure Information Protection ou une version ultérieure.

Lorsque vous configurez ce paramètre, celui-ci masque le bouton **Ne pas transférer** du ruban Outlook. Ce paramètre ne permet pas de masquer cette option dans les menus Office.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **DisableDNF**

- Valeur : **True**

## <a name="make-the-custom-permissions-options-unavailable-to-users"></a>Désactiver les options d’autorisations personnalisées pour les utilisateurs

Cette option de configuration est actuellement en préversion.

> [!IMPORTANT]
> N’utilisez pas cette option si vous avez des étiquettes configurées pour des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers. Si vous le faites, quand l’étiquette est appliquée, les utilisateurs ne sont pas invités à configurer les autorisations personnalisées. Par conséquent, le document est étiqueté, mais n’est pas protégé comme prévu.

Cette configuration utilise un [paramètre client avancé](#how-to-configure-advanced-client-configuration-settings-in-the-portal) que vous devez configurer dans le portail Azure. 

Lorsque vous configurez ce paramètre et publiez la stratégie pour les utilisateurs, les options relatives aux autorisations personnalisées deviennent indisponibles dans les emplacements suivants :

- Dans les applications Office : onglet **Accueil** > groupe **Protection** > **Protéger** > **Autorisations personnalisées**

- Dans l’Explorateur de fichiers : cliquez avec le bouton droit sur > **Classifier et protéger** > **Autorisations personnalisées**

Ce paramètre n’a aucun effet sur les autorisations personnalisées que vous pouvez configurer à l’aide des options de menu Office. 

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **EnableCustomPermissions**

- Valeur : **False**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Masquer définitivement la barre Azure Information Protection

Cette configuration utilise un paramètre avancé que vous devez configurer dans le portail Azure. Ce paramètre nécessite également la préversion **1.9.58.0** du client Azure Information Protection ou une version ultérieure.

Lorsque vous configurez ce paramètre et publiez la stratégie pour les utilisateurs, si un utilisateur choisit de ne pas afficher la barre Azure Information Protection dans ses applications Office, la barre reste masquée. Cela se produit lorsque l’utilisateur décoche l’option **Afficher la barre** dans l’onglet **Accueil**, groupe **Protection** groupe, bouton **Protéger**. Ce paramètre n’a aucun effet si l’utilisateur ferme la barre à l’aide de l’icône **Fermer cette barre**.

Même si la barre Azure Information Protection reste masquée, les utilisateurs peuvent encore sélectionner une étiquette dans la barre d’outils qui s’affiche temporairement si vous avez configuré la classification recommandée ou si un document ou un e-mail doit avoir une étiquette. Le paramètre n’a aucun effet sur les étiquettes que vous ou d’autres avez configurées, telles que la classification automatique ou manuelle, ou la définition d’une étiquette par défaut.

Pour configurer ce paramètre avancé, entrez les chaînes suivantes :

- Clé : **EnableBarHiding**

- Valeur : **True**

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Intégration avec la classification des messages Exchange pour une solution d’étiquetage des appareils mobiles

Bien que Outlook sur le web ne prenne pas encore en charge la protection et la classification Azure Information Protection, vous pouvez utiliser la classification des messages Exchange pour étendre vos étiquettes d’Azure Information Protection à vos utilisateurs mobiles.

Pour obtenir cette solution : 

1. Utilisez l’applet de commande PowerShell Exchange [New-MessageClassification](https://technet.microsoft.com/library/bb124400) pour créer des classifications des messages avec la propriété Name qui correspond à vos noms d’étiquette dans votre stratégie Azure Information Protection. 

2. Créez une règle de transport Exchange pour chaque étiquette : appliquez la règle quand les propriétés de message incluent la classification que vous avez configurée, puis modifiez les propriétés de message pour définir un en-tête de message. 

    Pour l’en-tête de message, vous trouvez les informations à spécifier en examinant les en-têtes Internet d’un e-mail que vous avez envoyé et classifié à l’aide de votre étiquette Azure Information Protection. Recherchez l’en-tête **msip_labels** et la chaîne qui suit immédiatement, jusqu’au point-virgule inclus. Dans l’exemple précédent :
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Ensuite, pour l’en-tête du message dans la règle, spécifiez **msip_labels** pour l’en-tête, et le reste de cette chaîne pour la valeur de l’en-tête. Exemple :
    
    ![Exemple de règles de transport Exchange Online qui définit l’en-tête de message pour une étiquette Azure Information Protection spécifique](../media/exchange-rule-for-message-header.png)

Avant de tester cette configuration, n’oubliez pas qu’il y a souvent un délai quand vous créez ou modifiez des règles de transport (attendez par exemple une heure). Quand la règle est effective, les événements suivants se produisent si les utilisateurs se servent d’Outlook sur le web ou sur un client d’appareil mobile qui prend en charge la protection Rights Management : 

- Les utilisateurs sélectionnent la classification des messages Exchange et envoient l’e-mail.

- La règle Exchange détecte la classification Exchange et modifie en conséquence l’en-tête de message pour ajouter la classification Azure Information Protection.

- Quand les destinataires qui disposent du client Azure Information Protection affichent l’e-mail dans Outlook, ils voient l’étiquette Azure Information Protection attribuée et tout en-tête, pied de page ou filigrane correspondants. 

Si vos étiquettes Azure Information Protection appliquent la protection de la gestion des droits, ajoutez la protection à la configuration de la règle en sélectionnant l’option permettant de modifier la sécurité des messages, appliquez la protection des droits, puis sélectionnez le modèle RMS ou l’option Ne pas transférer.

Vous pouvez également configurer des règles de transport pour effectuer le mappage inverse. Quand une étiquette Azure Information Protection est détectée, définissez la classification de messages Exchange correspondante :

- Pour chaque étiquette Azure Information Protection, créez une règle de transport appliquée quand l’en-tête **msip_labels** inclut le nom de votre étiquette (par exemple **Général**), puis appliquez une classification de messages qui correspond à cette étiquette.


## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez personnalisé le client Azure Information Protection, consultez les ressources suivantes pour obtenir des informations supplémentaires sur la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
