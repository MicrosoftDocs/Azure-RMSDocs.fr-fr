---
title: Client Azure Information Protection - historique des versions et politique du support
description: Découvrez les nouveautés et les changements d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/27/2018
ms.topic: conceptual
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 94120417c5e2e61f1d28fc16d714ec1c91a4ed0f
ms.sourcegitcommit: 630f03a91f84d79219e04b4085bdfb5bc6478e88
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54011971"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : Historique de publication et politique de support des versions

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

L’équipe Azure Information Protection met régulièrement à jour le client Azure Information Protection avec des correctifs et des nouvelles fonctionnalités. 

Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle (si elle est disponible) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Après un court délai d’environ deux semaines en général, la dernière version en disponibilité générale est également incluse dans le catalogue Microsoft Update (catégorie : **Azure Information Protection**). Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. La documentation n’inclut pas d’informations sur les versions non pris en charge du client. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les changements d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est la première sur la liste. 

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, consultez la préversion actuelle.
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="version-141510"></a>Version 1.41.51.0

> [!TIP]
> Vous vous intéressez à l’évaluation au client d’étiquetage unifié Azure Information Protection, car vos étiquettes sont publiées à partir du Centre de sécurité et de conformité Office 365 ? Consultez [Client d’étiquetage unifié Azure Information Protection : Informations sur la version](unifiedlabelingclient-version-release-history.md).

**Date de publication** : 27/11/2018

Cette version inclut la version 1.0.3592.627 de MSIPC du client RMS.

**Nouvelles fonctionnalités :**

- Le client Azure Information Protection par défaut protège maintenant les fichiers PDF à l’aide de la norme ISO pour le chiffrement PDF. Auparavant, vous deviez activer cette prise en charge avec un paramètre client avancé.
    
    Si vous souhaitez que le client rétablisse la protection des fichiers PDF à l’aide d’une extension de nom de fichier .ppdf, utilisez le même [paramètre client avancé](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), mais spécifiez **False**.

- Prise en charge de la [création de rapports centralisée](../reports-aip.md) pour les fonctionnalités d’analyse Azure Information Protection annoncées au Microsoft Ignite.

- Prise en charge des [marquages visuels](../configure-policy-markings.md) de différentes couleurs dans Excel.

- Pour les déploiements S/MIME existants, nouveau paramètre client avancé (en préversion) permettant de configurer une étiquette de façon à ce qu’elle applique automatiquement la protection S/MIME dans Outlook. [Plus d’informations](client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Nouveau paramètre client avancé (qui évite d’avoir à modifier le Registre) permettant d’empêcher l’affichage des invites de connexion du service Azure Information Protection pour les [ordinateurs déconnectés](client-admin-guide-customizations.md#support-for-disconnected-computers).

**Correctifs** :

- Le client Azure Information Protection n’exclut plus les extensions de nom de fichier .msg, .rar et .zip pour l’Explorateur de fichiers (clic droit) et les commandes PowerShell. Toutefois, ces extensions de nom de fichier restent exclues par défaut pour le scanneur. 

- Le client Azure Information Protection peut ôter la protection de plusieurs fichiers (sélection multiple et dossier contenant des fichiers protégés) si vous utilisez l’Explorateur de fichiers avec clic droit.

- Pour Excel :
    
    - Les marquages visuels sont maintenant appliqués si la feuille de calcul est enregistrée pendant la modification d’une cellule.
    
    - Excel 2010 : Pour une feuille de calcul protégée au [niveau d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels) Co-auteur, le bouton **Supprimer l’étiquette** est désormais disponible quand vous cliquez avec le bouton droit sur le fichier et que vous choisissez **Classer et protéger**.

- Les paramètres client avancés permettant de [supprimer les en-têtes et pieds de page d’autres solutions d’étiquetage](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions) prennent désormais en charge les dispositions personnalisées.

**Autres modifications :**

- Quand la planification du scanneur est définie sur **Toujours**, il y a maintenant un délai de 30 secondes entre les analyses.

- Le scanneur ne modifie plus le propriétaire de Rights Management pour les fichiers qu’il étiquette lorsque le fichier est déjà protégé.

## <a name="version-137190"></a>Version 1.37.19.0

**Date de publication** : 17/09/2018

Cette version inclut la version 1.0.3592.627 de MSIPC du client RMS.

**Nouvelles fonctionnalités** : 

- Prise en charge de la norme ISO pour le chiffrement PDF en configurant une nouvelle [configuration avancée du client](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Quand cette option est définie sur **True**, les documents PDF que vous protégez conservent leur extension de nom de fichier .pdf (plutôt que de devenir .ppdf) et peuvent être ouverts sur les lecteurs de fichiers PDF prenant en charge cette norme ISO. Actuellement, vous devez donner aux utilisateurs l’instruction d’ouvrir manuellement ces documents PDF protégés avec la visionneuse Azure Information Protection. Pour les y aider, une page apparaît à l’ouverture d’un de ces documents ; elle comporte des icônes à sélectionner en fonction du système d’exploitation.

- Prise en charge de nouveaux types d’informations sensibles pour vous aider à classer les documents qui contiennent des informations personnelles. [Plus d’informations](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Les étiquettes qui appliquent la protection s’affichent maintenant dans les applications Office 2016 (version minimale 1805, build 9330.2078) quand une licence pour Azure Rights Management (également appelé Azure Information Protection pour Office 365) est attribuée à l’utilisateur.

- Prise en charge d’étiquetage pour le format **Strict Open XML Document** dans les fichiers Word, Excel et PowerPoint. Pour plus d’informations sur les formats Open XML, consultez le billet de blog Office, [Nouvelles options de format de fichier dans le nouvel Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/). 

- Prise en charge des fichiers qui sont protégés par Secure Islands quand ils ne sont pas des documents PDF et Office. Par exemple, des fichiers texte et image protégés. Ou des fichiers avec une extension de nom de fichier .pfile. Cette prise en charge offre de nouveaux scénarios, par exemple le scanneur Azure Information Protection peut inspecter ces fichiers pour y rechercher des informations sensibles et les réétiqueter automatiquement pour Azure Information Protection. [Plus d’informations](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Nouveaux paramètres clients avancés servant à supprimer les en-têtes et pieds de page qui ont été appliqués aux documents par d’autres solutions d’étiquetage. [Plus d’informations](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Pour le scanneur Azure Information Protection :

    - Nouvelle applet de commande [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) : Doit être exécutée une seule fois après la mise à niveau à partir de la précédente version en disponibilité générale (1.29.5.0) ou d’une version antérieure.
    
    - Nouvelle applet de commande [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus) : Obtient l’état actuel du service pour le scanneur.  
    
    - Nouvelle applet de commande [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) : Indique au scanneur de démarrer un seul cycle d’analyse quand la planification est définie sur Manuelle.
    
    - Les documents PDF sont désormais protégés par défaut quand vous utilisez la norme ISO pour le chiffrement des fichiers PDF.
    
    - SharePoint Server 2010 est pris en charge pour les clients qui bénéficient d’un [support étendu pour cette version de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
- Prise en charge du nouveau panneau **Azure Information Protection - Nodes (préversion)** dans le portail Azure, ce qui vous permet de gérer les scanneurs depuis un emplacement central. Les informations provenant de vos scanneurs déployés et qui disposent d’une connectivité à Azure sont mises à jour toutes les cinq minutes. Dans ce panneau, vous pouvez démarrer le scanneur afin de lancer une analyse ponctuelle, relancer l’analyse de tous les fichiers, vérifier l’état d’un scanneur, et afficher le taux d’analyse.

**Correctifs**

- Pour le scanneur Azure Information Protection :
    
    - Pour les documents protégés dans les bibliothèques SharePoint, si le paramètre *DefaultOwner* n’est pas utilisé pour le référentiel de données, la valeur de l’éditeur SharePoint est maintenant utilisée comme valeur par défaut au lieu de la valeur de l’auteur.
    
    - Les rapports du scanneur incluent « Dernière modification par » pour les documents Office.
    
    - Vous pouvez désormais protéger tous les types de fichiers à l’aide du caractère générique `*` quand vous modifiez le Registre comme décrit dans la section [Modification du registre pour le scanneur](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

- L’affichage des e-mails à l’aide des icônes des flèches Élément suivant et Élément précédent dans la barre d’outils Accès rapide montre la bonne étiquette pour chaque e-mail.

- Si vous utilisez l’Explorateur de fichiers, PowerShell ou le scanneur pour la classification et la protection, les métadonnées des documents Office ne sont ni supprimées ni chiffrées.

- Les autorisations personnalisées gèrent les adresses e-mail des destinataires qui contiennent une apostrophe.

- L’environnement informatique s’initialise (s’amorce) correctement quand cette action est lancée en ouvrant un document protégé stocké dans SharePoint Online.

- Si vous utilisez le client par clic droit dans l’Explorateur de fichiers, PowerShell ou le scanneur, l’étiquetage est bloqué pour les fichiers des emplacements WebDAV, car ce scénario n’est pas pris en charge.

- L’icône Supprimer l’étiquette ne s’affiche pas dans les applications clientes (Word, Excel, PowerPoint et Outlook) si le [Paramètre de stratégie](../configure-policy-settings.md) est configuré sur **Tous les documents et e-mails doivent avoir une étiquette**.

**Autres modifications** :

- Pour [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) :
    
    - Les valeurs du paramètre *Planification* ne sont plus **Une fois**, **Continue** et **Jamais**, mais **Manuelle** et **Toujours**.
        
    - Le paramètre *Type* est supprimé, donc il est également supprimé de la sortie quand vous exécutez [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). Par défaut, seuls les fichiers nouveaux ou modifiés sont inspectés après le premier cycle d’analyse. Si vous avez précédemment défini le paramètre *Type* sur **Complète** pour relancer l’analyse de tous les fichiers,exécutez à présent [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) avec le paramètre *Réinitialiser*. Le scanneur doit aussi être configuré pour une planification manuelle, donc le paramètre *Planification* doit être défini sur **Manuel** avec [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- La liste d’exclusions par défaut du client et du scanneur inclut maintenant les fichiers .msg, .rar et .zip. Le scanneur exclut également les fichiers .rtf. [Plus d’informations](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- La version de stratégie est remplacée par 1.4. L’identification du numéro de version est obligatoire pour la [configuration des ordinateurs déconnectés](client-admin-guide-customizations.md#support-for-disconnected-computers).

- Le lien **Envoyez-nous des commentaires** de la boîte de dialogue **Aide et commentaires** est supprimé. Il a été temporairement remplacé par **Signaler un problème** qui, par défaut, envoie un e-mail à Microsoft. À compter de décembre 2018, l’option **Signaler un problème** n’est pas affichée par défaut, mais elle peut être ajoutée avec un [paramètre client avancé](client-admin-guide-customizations.md#add-report-an-issue-for-users) où vous spécifiez une chaîne HTTP pour le lien. (par exemple, une page web personnalisée permettant aux utilisateurs de signaler des problèmes, ou une adresse e-mail qui pointe vers votre support technique). 

## <a name="version-12950"></a>Version 1.29.5.0 

**Date de publication** : 26/06/2018

Cette version inclut MSIPC version 1.0.3403.1224 du client RMS.

**Correctifs** :

- Pour les versions d’Outlook 16.0.9324.1000 et ultérieures (Office « Démarrer en un clic »), la barre Azure Information Protection prend en charge les dernières options d’affichage du moniteur qui auparavant pouvaient entraîner l’affichage de la barre en dehors de l’application Outlook.

- Les marquages visuels que vous configurez [par type d’application Office](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook) remplacent maintenant un en-tête ou un pied de page qui était précédemment appliqué par une étiquette Azure Information Protection.

- Désormais, quand un fichier Excel porte déjà un étiquette et que celle-ci applique des marquages visuels, une nouvelle feuille présente également les marquages visuels de l’étiquette appliqués.

- Lorsque vous utilisez le paramètre client avancé pour [étiqueter un document Office à l’aide d’une propriété personnalisée existante](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property), l’étiquetage automatique ne remplace pas l’étiquetage manuel.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Client Azure Information Protection - Guide de l’administrateur](client-admin-guide.md)
