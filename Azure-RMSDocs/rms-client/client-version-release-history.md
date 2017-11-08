---
title: "Client Azure Information Protection &colon; historique de publication des versions"
description: "Découvrez ce qui est nouveau ou ce qui a changé dans une version du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ec73c1e0c0c2d5ef959f15975b2a972086a3bcff
ms.sourcegitcommit: 91585427fe62956fd78d4e7897ec8abe55b3c11d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2017
---
# <a name="azure-information-protection-client-version-release-history"></a>Client Azure Information Protection : historique des versions

>*S’applique à : Azure Information Protection*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. Le client est intégré au Catalogue Microsoft Update (catégorie : **Azure Information Protection**) et vous pouvez continuer à télécharger la version de disponibilité générale la plus récente et la préversion actuelle à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt les versions préliminaires pour tester de nouvelles fonctionnalités ou de nouveaux correctifs à paraître dans la prochaine version en disponibilité générale. 

Pour déterminer les nouveautés ou modifications apportées à une version en disponibilité générale, utilisez les informations ci-après. La dernière version est répertoriée en première position. 

> [!NOTE]
> Les correctifs mineurs n’y sont pas répertoriés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, vérifiez d’abord qu’il ne s’agit pas d’un problème avec la version en disponibilité générale la plus récente. Si tel est le cas, vérifiez la version préliminaire actuelle.
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../get-started/information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-110560"></a>Versions postérieures à 1.10.56.0

Si votre version du client est ultérieure à 1.10.56.0, il s’agit d’une préversion à des fins de test et d’évaluation. 

Pour connaître les nouveautés ou les modifications apportées à la préversion actuelle depuis la dernière version en disponibilité générale, consultez la section **Détails** dans la [page de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

## <a name="version-110560"></a>Version 1.10.56.0

**Date de publication** : 18/09/2017

Cette version inclut MSIPC version 1.0.3219.0619 du client RMS.

**Nouvelles fonctionnalités** :

- Prise en charge des nouvelles conditions DLP Office 365 que vous pouvez configurer pour une étiquette. Pour plus d’informations, consultez [Configurer les conditions d’une étiquette Azure Information Protection](../deploy-use/configure-policy-classification.md).

- Prise en charge des étiquettes configurées pour les actions définies par l’utilisateur. Pour Outlook, cette étiquette applique automatiquement l’option Outlook Ne pas transférer. Pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette invite l’utilisateur à spécifier des autorisations personnalisées. Pour plus d’informations, consultez [Configurer une étiquette Azure Information Protection à des fins de protection](../deploy-use/configure-policy-protection.md).

- Pour afficher les étiquettes, utilisez le bouton **Protéger** dans le ruban Office. Les étiquettes figurent également dans la barre Information Protection. 

- Protection native pour les types de fichiers Visio suivants : .vsdm, .vsdx, .vssm, .vssx, .vstm, .vstx

- Prise en charge des configurations de client avancées que vous configurez dans le portail Azure. Ces configurations sont les suivantes :
    
    - [Masquer le bouton Ne pas transférer dans Outlook](../rms-client/client-admin-guide-customizations.md#hide-the-do-not-forward-button-in-outlook)
    
    - [Désactiver les options d’autorisations personnalisées pour les utilisateurs](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [Masquer définitivement la barre Azure Information Protection](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-unavailable-to-users)
    
    - [Activer la classification recommandée dans Outlook](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- Pour PowerShell, prise en charge de l’étiquetage des fichiers d’étiquette de manière non interactive à l’aide des nouvelles applets de commande PowerShell [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) et [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). Pour plus d’informations sur l’utilisation de ces applets de commande, consultez la [section PowerShell](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) du guide de l’administrateur.

- Les applets de commande PowerShell [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) et [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) disposent de nouveaux paramètres : **Owner** et **PreserveFileDetails** . Ces paramètres vous permettent de spécifier une adresse e-mail pour la propriété personnalisée Owner. La date des documents que vous étiquetez est inchangée.

**Correctifs** :

Correctifs apportés pour accroître la stabilité et prendre en charge des scénarios spécifiques :

- Prise en charge de la protection générique des fichiers volumineux (supérieurs à 1 Go) qui causaient précédemment des dysfonctionnements. À présent, la taille de fichier est uniquement limitée par l’espace disque et la mémoire disponibles. Pour plus d’informations sur les limitations de taille de fichier, consultez [Tailles de fichiers prises en charge pour la protection](client-admin-guide-file-types.md#file-sizes-supported-for-protection) dans le guide de l’administrateur.

- La visionneuse du client Azure Information Protection ouvre les fichiers PDF protégés (.ppdf) en lecture seule.

- Prise en charge de l’étiquetage et de la protection des fichiers stockés sur un serveur SharePoint.

- Les filigranes prennent désormais en charge plusieurs lignes. De plus, les marquages visuels sont à présent appliqués à un document au [premier enregistrement uniquement](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied), et non à chaque enregistrement.

- L’option **Exécuter des diagnostics** dans la boîte de dialogue **Aide et commentaires** est remplacée par **Réinitialiser les paramètres**. Le comportement de cette action inclut désormais la déconnexion de l’utilisateur et la suppression de la stratégie Azure Information Protection. Pour plus d’informations, consultez [Informations supplémentaires sur l’option Réinitialiser les paramètres](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) dans le guide de l’administrateur.

- Prise en charge pour l’authentification proxy.

Des correctifs ont été apportés pour améliorer l’expérience utilisateur :

- Validation par e-mail quand des utilisateurs spécifient des autorisations personnalisées. De plus, vous pouvez à présent spécifier plusieurs adresses e-mail en appuyant sur Entrée.

- L’étiquette parent n’est pas affichée si toutes ses sous-étiquettes sont configurées pour la protection et que le client ne dispose pas d’une édition d’Office prenant en charge la protection. 

## <a name="version-172100"></a>Version 1.7.210.0

**Publiée le** : 06/06/2017

Cette version inclut MSIPC version 1.0.2217.1 du client RMS.

**Nouvelles fonctionnalités** :

- Nouvelle applet de commande PowerShell, [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification). Lorsque vous exécutez cette applet de commande, elle inspecte le contenu du fichier et applique automatiquement des étiquettes pour les fichiers sans étiquette, selon les conditions que vous spécifiez dans la stratégie Azure Information Protection.

**Correctifs** :

- Toutes les applets de commande de classification et d’étiquetage sont désormais prises en charge sur les ordinateurs qui ne sont pas connectés à Internet mais qui ont une stratégie Azure Information Protection valide.

- Par souci de cohérence, un paramètre de sortie de l’applet de commande [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) est modifié de l’anglais britannique (**IsLabelled**) vers l’anglais américain (**IsLabeled**). Si vous avez des scripts ou des processus automatisés qui ressemblent à ce paramètre, mettez à jour l’orthographe de ce paramètre.

- Des correctifs de stabilité généraux qui incluent :

    - Pour Outlook : Correctifs pour les plantages, la consommation élevée de la mémoire et les problèmes d’affichage pour les menus.
    
    - Pour Word, Excel et PowerPoint : Correctifs pour l’utilisation élevée du processeur, les problèmes d’affichage lors de l’enregistrement des fichiers Excel volumineux, et les problèmes pour lesquels l’application cesse de répondre. 
    
    Pour ces applications, les correctifs comprennent aussi l’amélioration des performances pour Office 2016 avec SharePoint Online et OneDrive Entreprise, l’étiquetage automatique et recommandé est appliqué lors de la fermeture du fichier plutôt que lorsque le fichier est enregistré (enregistre automatiquement ou demande à l’utilisateur de choisir d’enregistrer ou non). De même, si le paramètre **Tous les documents et e-mails doivent avoir une étiquette** est activé, les utilisateurs ne sont pas invités à sélectionner une étiquette avant la fermeture du fichier. L’exception concerne Word 2016 et Excel 2016, lorsque l’utilisateur sélectionne l’option **Enregistrer sous**. Ensuite, cette action déclenche ces comportements d’étiquetage s’ils sont configurés. 

## <a name="version-14210"></a>Version 1.4.21.0

**Publiée le** : 15/03/2017

**Modification de la configuration requise :**

Avec la version précédente, il était obligatoire de disposer de Microsoft .NET Framework 4.6.2 pour profiter du client complet. Bien que cela ne soit pas conseillé, vous pouvez ignorer cette condition à l’aide d’un paramètre d’installation personnalisé : **DowngradeDotNetRequirement**. Pour plus d’informations, consultez [Installer le client Azure Information Protection pour les utilisateurs](client-admin-guide-install.md) dans le guide de l’administrateur.

**Nouvelles fonctionnalités** :

- Vous pouvez définir des autorisations personnalisées à partir de votre application Office. Vous pouvez définir une protection de différents niveaux : pour vous uniquement, pour des groupes externes ou pour tous les utilisateurs d’une autre organisation. Pour plus d’informations, consultez la section [Définir des autorisations personnalisées pour un document](client-classify-protect.md#set-custom-permissions-for-a-document) du guide de l’utilisateur.
    
- Les fichiers PDF prennent maintenant en charge les étiquettes qui appliquent la classification uniquement.

- Pour les fichiers PDF, la visionneuse prend désormais en charge les options telles que la recherche, le zoom et le pivotement. Pour utiliser ces options, cliquez avec le bouton droit sur le fichier lorsqu’il est affiché dans la visionneuse.

**Correctifs** :

- Prise en charge des lecteurs mappés pour classifier et protéger les fichiers.

- Prise en charge des fichiers volumineux (supérieurs à 250 Mo) dans la visionneuse du client Azure Information Protection. 

- Lorsque HYOK est configuré, Outlook peut appliquer des étiquettes qui sont configurées pour utiliser des modèles Azure Rights Management ou AD RMS.

## <a name="version-131552"></a>Version 1.3.155.2

**Date de publication** : 08/02/2017

**Nouvelles conditions requises** :

Microsoft .NET Framework

- Cette version du client Azure Information Protection requiert une version minimale de Microsoft .NET Framework 4.6.2. Si cette version est manquante, le programme d’installation tente de la télécharger et de l’installer. Un redémarrage de l’ordinateur peut être nécessaire une fois l’installation du client Azure Information Protection terminée.

- Si la visionneuse Azure Information Protection est installée séparément, une version minimale de Microsoft .NET Framework 4.5.2 est requise. Si cette version est manquante, le programme d’installation ne procède pas au téléchargement ni à l’installation.

**Nouvelles fonctionnalités** :

- Un nouveau client unifié, associant les fonctionnalités de l’application de partage Rights Management pour Windows au client Azure Information Protection. Inclut :
    
    - Intégration avec l’Explorateur de fichiers Windows (clic droit) pour appliquer les étiquettes et la protection. Prise en charge de formats de fichiers supplémentaires et de la sélection de plusieurs fichiers.
    - Une visionneuse de documents protégés (inclut les PDF protégés pour SharePoint).
    - Des applets de commande PowerShell pour obtenir et définir des étiquettes pour les fichiers qui sont stockés en local ou sur les partages réseau. Ces applets de commande installent les applets de commande précédemment incluses avec l’outil de protection RMS (module RMSProtection).
    - Les journaux d’utilisation du client qui enregistrent les informations d’étiquette appliquée, de mode d’application et d’utilisateur.

Cette version du client est la [version en disponibilité générale](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/) du client en préversion annoncé en décembre 2016. Pour plus d’informations sur cette version du client, consultez les guides suivants :

- [Client Azure Information Protection - Guide de l’administrateur](client-admin-guide.md)

- [Azure Information Protection - Guide de l’utilisateur](client-user-guide.md)


## <a name="version-1240"></a>Version 1.2.4.0

**Publiée le** : 27/10/2016

**Nouvelle fonctionnalité** :

- Tests de diagnostic et option de réinitialisation qu’un utilisateur peut exécuter depuis l’application Office quand le client Azure Information Protection est installé : sous l’onglet **Accueil**, dans le groupe **Protection**, cliquez sur **Protéger**, cliquez sur **Aide et commentaires**, puis cliquez sur **Exécuter des diagnostics**. 

    Pour plus d’informations sur cette option, consultez la section [Vérifications supplémentaires et dépannage](client-admin-guide.md#installation-checks-and-troubleshooting) du guide de l’administrateur.

**Correctifs** :

- L’installation du client se termine quand le service Windows Update est désactivé.

- Dans Office 2016, quand vous enregistrez un document et qu’une étiquette appliquée est configurée pour un en-tête ou un pied de page, le curseur ne passe pas à l’en-tête ou au pied de page.

- La classification automatique fonctionne dans Word pour le texte dans les zones de texte groupées.


## <a name="version-11230"></a>Version 1.1.23.0

**Publiée le** : 01/10/2016

Disponibilité générale.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation et l’utilisation du client :

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
