---
title: "Client Azure Information Protection &colon; historique de publication des versions"
description: "Découvrez ce qui est nouveau ou ce qui a changé dans une version du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 70c358954a39b02610a77ec81074379dc574158b
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
translationtype: HT
---
# <a name="azure-information-protection-client-version-release-history"></a>Client Azure Information Protection : historique des versions

>*S’applique à : Azure Information Protection*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. Le client est intégré au Catalogue Microsoft Update (catégorie : **Azure Information Protection**) et vous pouvez continuer à télécharger la version de disponibilité générale (GA) la plus récente et la prochaine version (préliminaire) depuis le [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt les versions préliminaires pour tester de nouvelles fonctionnalités ou de nouveaux correctifs à paraître dans la prochaine version en disponibilité générale. 

Pour déterminer les nouveautés ou modifications apportées à une version en disponibilité générale, utilisez les informations ci-après. La dernière version est répertoriée en première position. Pour plus d’informations sur la version préliminaire, consultez les informations sur la page de téléchargement.

> [!NOTE]
> Les correctifs mineurs n’y sont pas répertoriés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, vérifiez d’abord qu’il ne s’agit pas d’un problème avec la version en disponibilité générale la plus récente. Si tel est le cas, vérifiez la version préliminaire actuelle.
>  
> Si le problème persiste, consultez les informations dans [Options de support technique et ressources de la communauté](../get-started/information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="version-14210"></a>Version 1.4.21.0

**Publiée le** : 15/03/2017

**Modification de la configuration requise :**

Avec la version précédente, il était obligatoire de disposer de Microsoft .NET Framework 4.6.2 pour profiter du client complet. Bien que cela ne soit pas conseillé, vous pouvez ignorer cette condition à l’aide d’un paramètre d’installation personnalisé : **DowngradeDotNetRequirement**. Pour plus d’informations, consultez la [section sur l’installation du client](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) dans le guide de l’administrateur.


**Correctifs** :

- Prise en charge des lecteurs mappés pour classifier et protéger les fichiers.

- Prise en charge des fichiers volumineux (> 250 Mo) dans la visionneuse. 

- Lorsque HYOK est configuré, Outlook peut appliquer des étiquettes qui sont configurées pour utiliser des modèles Azure Rights Management ou AD RMS.


**Nouvelles fonctionnalités** :

- Vous pouvez définir des autorisations personnalisées à partir de votre application Office. Vous pouvez définir une protection de différents niveaux : pour vous uniquement, pour des groupes externes ou pour tous les utilisateurs d’une autre organisation. Pour plus d’informations, consultez la section [Définir des autorisations personnalisées pour un document](client-classify-protect.md#set-custom-permissions-for-a-document) du guide de l’utilisateur.
    
- Les fichiers PDF prennent maintenant en charge les étiquettes qui appliquent la classification uniquement.

- Pour les fichiers PDF, la visionneuse prend désormais en charge les options telles que la recherche, le zoom et le pivotement. Pour utiliser ces options, cliquez avec le bouton droit sur le fichier lorsqu’il est affiché dans la visionneuse.


## <a name="version-131552"></a>Version 1.3.155.2

**Date de publication** : 08/02/2017

**Nouvelles conditions requises** :

Microsoft .NET Framework

- Cette version du client Azure Information Protection requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de la télécharger et de l’installer. Un redémarrage de l’ordinateur peut être nécessaire une fois l’installation du client Azure Information Protection terminée.

- Si la visionneuse Azure Information Protection est installée séparément, une version minimale de Microsoft .NET Framework 4.5.2 est requise. Si cette version est manquante, le programme d’installation ne procède pas au téléchargement ni à l’installation.

**Nouvelles fonctionnalités** :

- Un nouveau client unifié, associant les fonctionnalités de l’application de partage Rights Management pour Windows au client Azure Information Protection. Inclut :
    
    - Intégration avec l’Explorateur de fichiers Windows (clic droit) pour appliquer les étiquettes et la protection. Prend en charge des formats de fichiers supplémentaires et la sélection de plusieurs fichiers.
    - Une visionneuse de documents protégés (inclut les PDF protégés pour SharePoint).
    - Des applets de commande PowerShell pour obtenir et définir des étiquettes pour les fichiers qui sont stockés en local ou sur les partages réseau. Ces applets de commande installent les applets de commande précédemment incluses avec l’outil de protection RMS (module RMSProtection).
    - Les journaux d’utilisation du client qui enregistrent les informations d’étiquette appliquée, de mode d’application et d’utilisateur.

Cette version du client est la [version en disponibilité générale](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) du client en préversion annoncé en décembre 2016. Pour plus d’informations sur cette version du client, consultez les guides suivants :

- [Client Azure Information Protection - Guide de l’administrateur](client-admin-guide.md)

- [Azure Information Protection - Guide de l’utilisateur](client-user-guide.md)


## <a name="version-1240"></a>Version 1.2.4.0

**Publiée le** : 27/10/2016

**Correctifs** :

- L’installation du client se termine quand le service Windows Update est désactivé.

- Dans Office 2016, quand vous enregistrez un document et qu’une étiquette appliquée est configurée pour un en-tête ou un pied de page, le curseur ne passe pas à l’en-tête ou au pied de page.

- La classification automatique fonctionne dans Word pour le texte dans les zones de texte groupées.

**Nouvelle fonctionnalité** :

- Tests de diagnostic et option de réinitialisation qu’un utilisateur peut exécuter depuis l’application Office quand le client Azure Information Protection est installé : sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, cliquez sur **Aide et commentaires**, puis cliquez sur **Exécuter des diagnostics**. 

    Pour plus d’informations sur cette option, consultez la section [Vérifications supplémentaires et dépannage](client-admin-guide.md#additional-checks-and-troubleshooting) du guide de l’administrateur.

## <a name="version-11230"></a>Version 1.1.23.0

**Publiée le** : 01/10/2016

Disponibilité générale.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation du client, consultez :

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]