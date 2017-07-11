---
title: "Configurations personnalisées pour le client Azure Information Protection"
description: Informations sur la personnalisation du client Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ab5465db1527e6236d2dca466936c36b260f03d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
<a id="custom-configurations-for-the-azure-information-protection-client" class="xliff"></a>

# Configurations personnalisées pour le client Azure Information Protection

>*S’applique à : Services Active Directory Rights Management, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

Utilisez les informations suivantes pour les configurations avancées nécessaires pour des scénarios spécifiques ou un sous-ensemble d’utilisateurs lorsque vous gérez le client Azure Information Protection. 

<a id="prevent-sign-in-prompts-for-ad-rms-only-computers" class="xliff"></a>

## Empêcher l’affichage des invites de connexion sur les ordinateurs AD RMS uniquement

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection. Pour les ordinateurs qui communiquent uniquement avec AD RMS, cela peut entraîner inutilement l’affichage d’une invite de connexion pour les utilisateurs. Vous pouvez empêcher l’affichage de cette invite de connexion en modifiant le Registre :

Recherchez le nom de valeur suivant et définissez la valeur à **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Indépendamment de ce paramètre, le client Azure Information Protection se conforme au [processus de découverte du service RMS](../rms-client/client-deployment-notes.md#rms-service-discovery) pour trouver le cluster AD RMS associé.

<a id="sign-in-as-a-different-user" class="xliff"></a>

## Se connecter avec l’identité d’un autre utilisateur

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

<a id="hide-the-classify-and-protect-menu-option-in-windows-file-explorer" class="xliff"></a>

## Masquer l’option de menu Classifier et protéger dans l’Explorateur de fichiers Windows

Vous pouvez définir cette configuration avancée en modifiant le Registre lorsque vous disposez de la version 1.3.0.0 du client Azure Information Protection ou d’une version ultérieure. 

Créez le nom de la valeur DWORD suivant (avec toutes données de la valeur) :

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

<a id="support-for-disconnected-computers" class="xliff"></a>

## Prise en charge des ordinateurs déconnectés

Par défaut, le client Azure Information Protection tente automatiquement de se connecter au service Azure Information Protection pour télécharger la dernière stratégie Azure Information Protection. Si vous disposez d’ordinateur qui ne sera pas en mesure de se connecter à Internet pendant une période donnée, vous pouvez empêcher le client d’essayer de se connecter au service en modifiant le Registre. Recherchez le nom de la valeur suivant et définissez les données de la valeur sur **0** :

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

Assurez-vous que le client dispose d’un fichier de stratégie valide nommé **Policy.msip**, dans le dossier **%localappdata%\Microsoft\MSIP**. Si nécessaire, vous pouvez exporter la stratégie à partir du portail Azure et copier le fichier exporté sur l’ordinateur client. Vous pouvez également utiliser cette méthode pour remplacer un fichier de stratégie obsolète par la dernière stratégie publiée.

<a id="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution" class="xliff"></a>

## Intégration avec la classification des messages Exchange pour une solution d’étiquetage des appareils mobiles

Bien que Outlook sur le web ne prenne pas encore en charge la protection et la classification Azure Information Protection, vous pouvez utiliser la classification des messages Exchange pour étendre vos étiquettes d’Azure Information Protection à vos utilisateurs mobiles.

Pour obtenir cette solution : 

1. Utilisez l’applet de commande PowerShell Exchange [New-MessageClassification](https://technet.microsoft.com/library/bb124400) pour créer des classifications des messages avec la propriété Name qui correspond à vos noms d’étiquette dans votre stratégie Azure Information Protection. 

2. Créez une règle de transport Exchange pour chaque étiquette : appliquez la règle quand les propriétés de message incluent la classification que vous avez configurée, puis modifiez les propriétés de message pour définir un en-tête de message. 

    Pour l’en-tête de message, vous trouvez les informations à spécifier en examinant les en-têtes Internet d’un e-mail que vous avez envoyé et classifié à l’aide de votre étiquette Azure Information Protection. Recherchez l’en-tête **msip_labels** et la chaîne qui suit immédiatement, jusqu’au point-virgule inclus. Dans l’exemple précédent :
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    Ensuite, pour l’en-tête du message dans la règle, spécifiez **msip_labels** pour l’en-tête, et le reste de cette chaîne pour la valeur de l’en-tête. Exemple :
    
    ![Exemple de règles de transport Exchange Online qui définit l’en-tête de message pour une étiquette Azure Information Protection spécifique](../media/exchange-rule-for-message-header.png)

Avant de tester ceci, n’oubliez pas qu’il y a souvent un délai quand vous créez ou que vous modifiez des règles de transport (attendez par exemple une heure). Quand la règle est effective, voici ce qui se produit quand les utilisateurs utilisent la version web ou un client d’appareil mobile qui prend en charge la protection RMS : 

- Les utilisateurs sélectionnent la classification des messages Exchange et envoient l’e-mail.

- La règle Exchange détecte la classification Exchange et modifie en conséquence l’en-tête de message pour ajouter la classification Azure Information Protection.

- Quand les destinataires exécutant le client Azure Information Protection affichent l’e-mail dans Outlook, ils voient l’étiquette Azure Information Protection attribuée et tout en-tête, pied de page ou filigrane correspondants. 

Si vos étiquettes Azure Information Protection appliquent la protection de la gestion des droits, ajoutez-la à la configuration de la règle en sélectionnant l’option permettant de modifier la sécurité des messages, appliquez la protection des droits, puis sélectionnez le modèle RMS ou l’option Ne pas transférer.

Vous pouvez également configurer des règles de transport pour effectuer le mappage inverse : quand une étiquette Azure Information Protection est détectée, définissez la classification de messages Exchange correspondante. Pour effectuer cette opération :

- Pour chaque étiquette Azure Information Protection, créez une règle de transport appliquée quand l’en-tête **msip_labels** inclut le nom de votre étiquette (par exemple **Général**), puis appliquez une classification de messages qui correspond à cette étiquette.


<a id="next-steps" class="xliff"></a>

## Étapes suivantes
Maintenant que vous avez personnalisé le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
