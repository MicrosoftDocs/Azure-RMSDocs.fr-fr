---
title: Client Azure Information Protection&colon; historique des versions et politique du support
description: "Découvrez les nouveautés et les modifications d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/06/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 19390c05719ebfee7e3442437d3f5bdfd303c652
ms.sourcegitcommit: d32d1f5afa5ee9501615a6ecc4af8a4cd4901eae
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : historique des versions et politique du support

>*S’applique à : Azure Information Protection*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. 

Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Ces versions se trouvent également dans le catalogue Microsoft Update (catégorie : **Azure Information Protection**), ce qui vous permet de déployer le client à l’aide de WSUS, de Configuration Manager ou d’autres systèmes de déploiement de logiciels qui utilisent Microsoft Update.

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. Les versions non prises en charge du client ne sont pas incluses dans cette page. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les modifications d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est répertoriée en première position. 

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../get-started/information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-110560"></a>Versions postérieures à 1.10.56.0

Si votre version du client est ultérieure à 1.10.56.0, il s’agit d’une préversion à des fins de test et d’évaluation.

La préversion est **1.21.203.0** et intègre les modifications suivantes depuis la version GA actuelle du client.

Cette version inclut MSIPC version 1.0.3403.1224 du client RMS.

**Nouvelles fonctionnalités** :

- Analyseur Azure Information Protection : le module PowerShell inclus avec le client dispose de nouvelles applets de commande pour installer et configurer le moteur d’analyse qui va permettre de détecter, classer et protéger les fichiers sur vos magasins de données locaux. Pour obtenir des instructions, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](../deploy-use/deploy-aip-scanner.md). 

- Pour les applications Office, la classification automatique et recommandée s’exécute en continu en arrière-plan, au lieu de s’exécuter lors de l’enregistrement de documents. Ce changement de comportement permet désormais d’appliquer la classification automatique et recommandée aux documents stockés dans SharePoint Online. [Plus d’informations](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied) 

- Vous pouvez maintenant définir des marquages visuels différents pour Word, Excel, PowerPoint et Outlook à l’aide d’une déclaration de variable « If.App » dans la chaîne de texte et identifier le type d’application. [Plus d’informations](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- Prise en charge du [paramètre de stratégie](../deploy-use/configure-policy-settings.md) **Afficher la barre Information Protection dans les applications Office**. Lorsque ce paramètre est désactivé, les utilisateurs peuvent sélectionner des étiquettes au moyen du bouton **Protéger** dans le ruban.

- Nouveau paramètre avancé du client, qui permet à Outlook de ne pas appliquer l’étiquette par défaut qui est configurée dans la stratégie Azure Information Protection. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer. [Plus d’informations](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- Pour les applications Office, lorsque vous spécifiez des autorisations personnalisées, vous pouvez maintenant parcourir et sélectionner les utilisateurs à partir d’une icône de carnet d’adresses. Cette option apporte une certaine parité à l’expérience utilisateur lorsque vous spécifiez des autorisations personnalisées à l’aide de l’Explorateur de fichiers.

- Prise en charge d’une méthode d’authentification non interactive, pour les comptes de service qui utilisent PowerShell et qui ne peuvent pas bénéficier de la **connexion en local** directement. Cette méthode d’authentification requiert l’utilisation du nouveau paramètre *Token* avec [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication), et l’exécution d’un script PowerShell en tant que tâche. [Plus d’informations](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- Nouveau paramètre, *IntegratedAuth* pour [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication). Ce paramètre prend en charge le mode serveur pour AD RMS, qui est nécessaire pour qu’AD RMS puisse prendre en charge l’infrastructure de classification des fichiers de Windows Server.


**Correctifs** :

Correctifs apportés pour accroître la stabilité et prendre en charge des scénarios spécifiques :

- Pour les versions d’Office 16.0.8628.2010 et ultérieures (Office « Démarrer en un clic »), la barre Azure Information Protection prend en charge les dernières options d’affichage du moniteur qui pourrait entraîner l’affichage d’applications Office externes dans la barre.

- Lorsque deux organisations utilisant Azure Information Protection partagent des documents et des e-mails étiquetés, leurs propres étiquettes sont conservées et ne sont pas remplacées par les étiquettes de l’autre organisation.

- Prise en charge des cellules dans Excel qui contiennent des références croisées, ce qui précédemment a provoqué une altération du texte dans cette cellule.

- Prise en charge de la modification des thèmes Office ou Windows, ce qui précédemment empêchait Excel d’afficher les données une fois le thème modifié.

- Les fichiers ayant une extension de nom de fichier .xml peuvent désormais être vérifiées en vue de la classification automatique ou recommandée.

- La visionneuse peut maintenant ouvrir des fichiers texte protégés (.ptxt et .pxml) supérieurs à 20 Mo. 

- Blocage d’Outlook lors de l’utilisation de rappels Outlook évité.

- Bon fonctionnement de Bootstrap dans Office 64 bits pour une protection des documents et des e-mails.

- Vous pouvez désormais configurer une étiquette pour les autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers et également utiliser le paramètre avancé du client pour masquer les options des autorisations personnalisées. [Plus d’informations](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- Retour à la police Calibri si les marqueurs visuels de la stratégie Azure Information Protection sont configurés pour un nom de police qui n’est pas installé sur le client.

- Pannes d’Office suite à la mise à niveau du client Azure Information Protection évitées.

- Amélioration des performances et de l’utilisation de la mémoire pour les applications Office.

- Lorsque vous configurez une étiquette pour des autorisations définies par l’utilisateur et la protection HYOK (AD RMS), la protection n’utilise plus les services AD RMS (Active Directory Rights Management Services) de manière incorrecte.

- Pour une expérience de gestion plus cohérente, sublabels n’hérite plus des marqueurs visuels et des paramètres de protection de son étiquette parent.


## <a name="version-110560"></a>Version 1.10.56.0

**Date de publication** : 18/09/2017

Cette version inclut MSIPC version 1.0.3219.0619 du client RMS.

**Nouvelles fonctionnalités** :

- Prise en charge des nouvelles conditions DLP Office 365 que vous pouvez configurer pour une étiquette. Pour plus d’informations, consultez [Configurer les conditions d’une étiquette Azure Information Protection](../deploy-use/configure-policy-classification.md).

- Prise en charge des étiquettes configurées pour les actions définies par l’utilisateur. Pour Outlook, cette étiquette applique automatiquement l’option Outlook Ne pas transférer. Pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette invite l’utilisateur à spécifier des autorisations personnalisées. Pour plus d’informations, consultez [Configurer une étiquette Azure Information Protection à des fins de protection](../deploy-use/configure-policy-protection.md).

- Les étiquettes prennent en charge plusieurs langues. Depuis le 30 août 2017, la [stratégie par défaut](../deploy-use/configure-policy-default.md) inclut la prise en charge de plusieurs langues que cette version du client affiche aux utilisateurs. Pour que les utilisateurs puissent voir les étiquettes dans la langue de leur choix à partir d’une stratégie par défaut avant cette date, ainsi que les étiquettes que vous configurez, consultez [Guide pratique pour configurer des étiquettes en plusieurs langues dans Azure Information Protection](../deploy-use/configure-policy-languages.md).

- Pour afficher les étiquettes, utilisez le bouton **Protéger** dans le ruban Office. Les étiquettes figurent également dans la barre Information Protection. 

- Protection native pour les types de fichiers Visio suivants : .vsdm, .vsdx, .vssm, .vssx, .vstm, .vstx

- Prise en charge des configurations de client avancées que vous configurez dans le portail Azure. Ces configurations sont les suivantes :
    
    - [Masquer ou afficher le bouton Ne pas transférer dans Outlook](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Activer ou désactiver les options d’autorisations personnalisées pour les utilisateurs](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Masquer définitivement la barre Azure Information Protection](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
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

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
