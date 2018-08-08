---
title: Client Azure Information Protection - historique des versions et politique du support
description: Découvrez les nouveautés et les modifications d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 61762157ff6419bb325d92470d5264dc9b55f840
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474213"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : historique des versions et politique du support

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. 

Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle (si elle est disponible) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). La version en disponibilité générale se trouve également dans le catalogue Microsoft Update (catégorie : **Azure Information Protection**), ce qui vous permet de mettre à niveau le client à l’aide de WSUS, de Configuration Manager ou d’autres systèmes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. Les versions non prises en charge du client ne sont pas incluses dans cette page. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les versions préliminaires ne doivent pas être déployées auprès des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les modifications d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est répertoriée en première position. 

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-12950"></a>Versions supérieures à 1.29.5.0

Si votre version du client est supérieure à la version 1.29.5.0, il s’agit d’une préversion générée à des fins de test et d’évaluation.

Cette version inclut MSIPC version 1.0.3557.524 du client RMS.

**Nouvelles fonctionnalités** : 

- Prise en charge de nouveaux types d’informations sensibles pour vous aider à classer les documents qui contiennent des informations personnelles. [Plus d’informations](../deploy-use/configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Prise en charge d’étiquetage pour le format **Strict Open XML Document** dans les fichiers Word, Excel et PowerPoint. Pour plus d’informations sur les formats Open XML, consultez le billet de blog Office, [Nouvelles options de format de fichier dans le nouvel Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/). 

- Prise en charge de la norme ISO pour le chiffrement PDF en configurant une nouvelle [configuration avancée du client](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Quand cette option est configurée, les documents PDF que vous protégez conservent leur extension de nom de fichier .pdf (plutôt que de devenir .ppdf) et peuvent être ouverts sur les lecteurs de fichiers PDF prenant en charge cette norme ISO. 

- Prise en charge des fichiers qui sont protégés par Secure Islands quand ils ne sont pas des documents PDF et Office. Par exemple, des fichiers texte et image protégés. Ou des fichiers avec une extension de nom de fichier .pfile. Cette prise en charge permet de nouveaux scénarios, par exemple le scanneur Azure Information Protection peut inspecter ces fichiers pour y rechercher des informations sensibles et les réétiqueter automatiquement pour Azure Information Protection. [Plus d’informations](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Pour le scanneur Azure Information Protection :

    - Nouvelle applet de commande, [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) : Doit être exécutée une seule fois après la mise à niveau à partir de la version 1.26.6.0 ou antérieure.
    
    - Nouvelle applet de commande, [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus) : Obtient l’état actuel du service pour le scanneur.  
    
    - Nouvelle applet de commande, [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) : Demande au scanneur de démarrer un seul cycle d’analyse quand la planification est définie sur Manuelle.
    
    - SharePoint Server 2010 est pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
**Correctifs**

- Pour le scanneur Azure Information Protection :
    
    - Pour les documents protégés dans les bibliothèques SharePoint, si le paramètre *DefaultOwner* n’est pas utilisé pour le référentiel de données, la valeur de l’éditeur SharePoint est maintenant utilisée comme valeur par défaut au lieu de la valeur de l’auteur.
    
    - Les rapports du scanneur incluent « Dernière modification par » pour les documents Office. 

- Lorsque vous classez et protégez en utilisant PowerShell ou le scanneur, les métadonnées des documents Office ne sont pas supprimées ou chiffrées.

- L’affichage des e-mails à l’aide des icônes des flèches Élément suivant et Élément précédent dans la barre d’outils Accès rapide montre la bonne étiquette pour chaque e-mail.

- Les autorisations personnalisées prennent en charge les adresses e-mail des destinataires qui contiennent une apostrophe.

- L’environnement informatique s’initialise (s’amorce) correctement quand cette action est lancée en ouvrant un document protégé stocké dans SharePoint Online. 

**Autres modifications** :
   
- Pour [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) :
    
    - Les valeurs du paramètre *Planification* ne sont plus **Une fois**, **Continue** et **Jamais**, mais **Manuelle** et **Toujours**.
        
    - Le paramètre *Type* est supprimé, donc il est également supprimé de la sortie quand vous exécutez [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration).
    
- Pour le scanneur, la liste d’exclusion par défaut inclut maintenant les fichiers .rtf. [Plus d’informations](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner)

- La version de stratégie est remplacée par 1.4. L’identification du numéro de version est obligatoire pour la [configuration des ordinateurs déconnectés](client-admin-guide-customizations.md#support-for-disconnected-computers). 


## <a name="version-12950"></a>Version 1.29.5.0 

**Date de publication** : 26/06/2018

Cette version inclut MSIPC version 1.0.3403.1224 du client RMS.

**Correctifs** :

- Pour les versions d’Outlook 16.0.9324.1000 et ultérieures (Office « Démarrer en un clic »), la barre Azure Information Protection prend en charge les dernières options d’affichage du moniteur qui auparavant pouvaient entraîner l’affichage de la barre en dehors de l’application Outlook.

- Les marquages visuels que vous configurez [par type d’application Office](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook) remplacent maintenant un en-tête ou un pied de page qui était précédemment appliqué par une étiquette Azure Information Protection.

- Désormais, quand un fichier Excel porte déjà un étiquette et que celle-ci applique des marquages visuels, une nouvelle feuille possède également les marquages visuels de l’étiquette appliqués.

- Lorsque vous utilisez le paramètre client avancé pour [étiqueter un document Office à l’aide d’une propriété personnalisée existante](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property), l’étiquetage automatique ne remplace pas l’étiquetage manuel.

## <a name="version-127480"></a>Version 1.27.48.0

**Date de publication** : 30/05/2018

Cette version inclut MSIPC version 1.0.3403.1224 du client RMS.

**Nouvelles fonctionnalités** : 

- Pour le scanneur Azure Information Protection :
    
    - Vous pouvez établir une liste de types de fichiers à inclure ou exclure de l’analyse. Pour établir cette liste, utilisez [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes). Après avoir spécifié votre liste de types de fichiers, vous pouvez ajouter un nouveau type de fichier à l’aide de [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) et en supprimer un à l’aide de [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes).
    
    - Vous pouvez appliquer une étiquette aux fichiers sans en inspecter le contenu en spécifiant une étiquette par défaut. Utilisez l’applet de commande [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) et définissez le paramètre *MatchPolicy* sur **Off**. 
    
    - Vous pouvez découvrir les fichiers contenant des informations sensibles sans configurer d’étiquettes pour la classification automatique. Pour cela, utilisez l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) et définissez le paramètre *DiscoverInformationTypes* sur **All**.
    
    - Par défaut, seuls les types de documents Office sont protégés. Les autres types de fichiers peuvent être protégés lorsque vous les définissez dans le Registre. Pour obtenir des instructions, consultez [Configuration de l’API de fichier](../develop/file-api-configuration.md) dans le Guide du développeur.
    
    - Par défaut, le scanneur s’exécute désormais avec un niveau d’intégrité faible afin de fournir une sécurité accrue si vous exécutez le scanneur avec un compte qui dispose de droits privilégiés. Lorsque le compte de service qui exécute le scanneur dispose seulement des droits documentés dans les [prérequis du scanneur](../deploy-use/deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), le niveau d’intégrité faible n’est pas nécessaire et n’est pas recommandé car il a un impact négatif sur les performances. Vous pouvez utiliser un paramètre client avancé pour désactiver le niveau d’intégrité faible. [Plus d’informations](../rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- La sortie de l’applet de commande [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus) inclut désormais le propriétaire Rights Management et l’émetteur Rights Management, ainsi que la date à laquelle le contenu a été protégé.
 
**Autres modifications** :

- Pour le scanneur Azure Information Protection : 
    
    - Si vous avez installé une version précédente du scanneur, réexécutez la commande d’installation du scanneur avec [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) une fois que vous avez mis à niveau le client Azure Information Protection. Vos paramètres de configuration pour le scanneur et les référentiels sont conservés. La réinstallation du scanneur accorde au compte de service du scanneur des autorisations de suppression pour la base de données du scanneur, qui seront nécessaires pour les rapports.    
    
    - Le paramètre *ScanMode* de l’applet de commande [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) a été renommé **Enforce**, avec les valeurs Off et On.
    
    - Pour utiliser une étiquette par défaut, vous n’avez plus besoin de la configurer dans les paramètres de stratégie. Il suffit de la spécifier dans la configuration du référentiel. 

- Suppression de la page d’accueil « Félicitations ! » et de la page « Nouveautés dans Azure Information Protection » qui s’affichaient lors de la première utilisation dans les applications Office.

## <a name="version-12660"></a>Version 1.26.6.0

**Date de publication** : 17/04/2018

Cette version inclut MSIPC version 1.0.3403.1224 du client RMS.

**Nouvelles fonctionnalités** :

- Analyseur Azure Information Protection : le module PowerShell inclus avec le client dispose de nouvelles applets de commande pour installer et configurer le moteur d’analyse qui va permettre de détecter, classer et protéger les fichiers sur vos magasins de données locaux. Pour obtenir des instructions, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](../deploy-use/deploy-aip-scanner.md). 

- Vous pouvez maintenant définir des marquages visuels différents pour Word, Excel, PowerPoint et Outlook à l’aide d’une déclaration de variable « If.App » dans la chaîne de texte et identifier le type d’application. [Plus d’informations](../deploy-use/configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- Prise en charge du [paramètre de stratégie](../deploy-use/configure-policy-settings.md) **Afficher la barre Information Protection dans les applications Office**. Lorsque ce paramètre est désactivé, les utilisateurs peuvent sélectionner des étiquettes au moyen du bouton **Protéger** dans le ruban.

- Nouveau paramètre client avancé (encore en préversion) pour activer l’exécution de la classification en continu en arrière-plan. Quand ce paramètre est configuré, pour les applications Office, la classification automatique et recommandée s’exécute en continu en arrière-plan, au lieu de s’exécuter lors de l’enregistrement de documents. Ce changement de comportement permet désormais d’appliquer la classification automatique et recommandée aux documents stockés dans SharePoint Online. [Plus d’informations](client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)

- Nouveau paramètre avancé du client, qui permet à Outlook de ne pas appliquer l’étiquette par défaut qui est configurée dans la stratégie Azure Information Protection. Au lieu de cela, Outlook peut appliquer une autre étiquette par défaut ou ne rien appliquer. [Plus d’informations](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- Pour les applications Office, lorsque vous spécifiez des autorisations personnalisées, vous pouvez maintenant parcourir et sélectionner les utilisateurs à partir d’une icône de carnet d’adresses. Cette option apporte une certaine parité à l’expérience utilisateur lorsque vous spécifiez des autorisations personnalisées à l’aide de l’Explorateur de fichiers.

- Prise en charge d’une méthode d’authentification non interactive, pour les comptes de service qui utilisent PowerShell et qui ne peuvent pas bénéficier de la **connexion en local** directement. Cette méthode d’authentification requiert l’utilisation du nouveau paramètre *Token* avec [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication), et l’exécution d’un script PowerShell en tant que tâche. [Plus d’informations](../rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- Nouveau paramètre, *IntegratedAuth* pour [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication). Ce paramètre prend en charge le mode serveur pour AD RMS, qui est nécessaire pour qu’AD RMS puisse prendre en charge l’infrastructure de classification des fichiers de Windows Server.


**Correctifs** :

Correctifs apportés pour accroître la stabilité et prendre en charge des scénarios spécifiques :

- Pour les versions d’Office 16.0.8628.2010 et ultérieures (Office « Démarrer en un clic »), la barre Azure Information Protection prend en charge les dernières options d’affichage du moniteur qui pourrait entraîner l’affichage d’applications Office externes dans la barre.

- Lorsque deux organisations utilisant Azure Information Protection partagent des documents et des e-mails étiquetés, leurs propres étiquettes sont conservées et ne sont pas remplacées par les étiquettes de l’autre organisation.

- Pour Excel :
        
    - Prise en charge de la modification des thèmes Office ou Windows, ce qui précédemment empêchait Excel d’afficher les données une fois le thème modifié.
        
    - Prise en charge des cellules qui contiennent des références croisées, ce qui provoquait auparavant une altération du texte dans cette cellule.
    
    - Prise en charge de la saisie de caractères japonais, chinois et coréens, ce qui provoquait auparavant la fermeture d’une fenêtre et empêchait la sélection de ces caractères.
    
    - Prise en charge des commentaires, ce qui provoquait auparavant la fermeture du commentaire pendant sa saisie.

- Pour PowerPoint : prise en charge de la co-création, qui pouvait auparavant entraîner la perte de données.

- Les fichiers ayant une extension de nom de fichier .xml peuvent désormais être vérifiées en vue de la classification automatique ou recommandée.

- La visionneuse peut maintenant ouvrir des fichiers texte protégés (.ptxt et .pxml) supérieurs à 20 Mo. 
- Blocage d’Outlook lors de l’utilisation de rappels Outlook évité.

- Bon fonctionnement de Bootstrap dans Office 64 bits pour une protection des documents et des e-mails.

- Vous pouvez désormais configurer une étiquette pour les autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers, et également utiliser le paramètre avancé du client pour masquer les options des autorisations personnalisées. [Plus d’informations](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- Retour à la police Calibri si les marqueurs visuels de la stratégie Azure Information Protection sont configurés pour un nom de police qui n’est pas installé sur le client.

- Pannes d’Office suite à la mise à niveau du client Azure Information Protection évitées.

- Amélioration des performances et de l’utilisation de la mémoire pour les applications Office.

- Lorsque vous configurez une étiquette pour des autorisations définies par l’utilisateur et la protection HYOK (AD RMS), la protection n’utilise plus les services AD RMS (Active Directory Rights Management Services) de manière incorrecte.

- Pour une expérience de gestion plus cohérente, sublabels n’hérite plus des marqueurs visuels et des paramètres de protection de son étiquette parent.

**Autres modifications** :

- Pour la [journalisation de l’utilisation client](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client ) : l’ID d’événement 102 et l’ID d’événement 103 sont remplacés par l’ID d’événement 101.

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

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)


