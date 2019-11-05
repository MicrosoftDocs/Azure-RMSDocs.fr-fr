---
title: Client pour Azure Information Protection-AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: abe085b36bd940dd69c2cc5f0f7a564fd6707548
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561128"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- Le client peut être le client d’étiquetage intégré pour Office, le Azure Information Protection client d’étiquetage unifié pour Windows, le client Azure Information Protection (Classic) pour Windows ou le client Rights Management.
    
    Ces clients sont souvent désignés comme le **client d’étiquetage Office intégré**, le client d' **étiquetage unifié**, le client **classique**et le **client RMS**, respectivement. Quel que soit le client que vous utilisez, il s’intègre aux applications que vous exécutez sur des ordinateurs et des appareils mobiles.

- Le service réside dans le Cloud ou localement. Le service Cloud est Azure Information Protection, qui utilise le service Azure Rights Management pour la protection des données. Le service local est services AD RMS (Active Directory Rights Management Services), plus communément appelé AD RMS. 

Tous ces clients s’intègrent aux applications Office, mais le client d’étiquetage unifié et le client classique doivent être installés séparément et prendre en charge des fonctionnalités et composants supplémentaires. Par exemple, ces clients incluent la prise en charge de l’Explorateur de fichiers, ce qui vous permet de classer et de protéger des fichiers en dehors d’Office. Les composants supplémentaires incluent une visionneuse pour les documents PDF protégés et les images protégées, ainsi qu’un scanneur pour les magasins de données locaux.

Le client RMS offre une protection uniquement. Ce client est installé automatiquement avec certaines applications, telles que les applications Office, les clients Azure Information Protection et les applications compatibles RMS des éditeurs de logiciels. Toutefois, il peut également être [installé de manière autonome](https://www.microsoft.com/en-us/download/details.aspx?id=38396) pour prendre en charge la [synchronisation des fichiers à partir des bibliothèques protégées par IRM et de OneDrive Entreprise](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668), et pour les développeurs souhaitant intégrer la protection de gestion des droits aux applications métier.

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>Choisir le client d’étiquetage à utiliser pour les ordinateurs Windows

Dans la mesure du possible, utilisez l’un des clients d’étiquetage, car les étiquettes font abstraction de la complexité de l’application de la protection pour les utilisateurs, et les étiquettes fournissent également une classification pour vous permettre de suivre et de gérer vos données.

Le choix de l’étiquetage du client pour vos ordinateurs Windows peut être influencé par le portail de gestion que vous utilisez :

- Le client d’étiquetage d’Office intégré et le client d’étiquetage unifié Azure Information Protection sont téléchargés des étiquettes et des paramètres de stratégie à partir des centres d’administration suivants : 
    - Office 365 Centre de sécurité et de conformité
    - Centre de sécurité Microsoft 365
    - Centre de conformité Microsoft 365

- Le client Azure Information Protection (Classic) télécharge les paramètres d’étiquette et de stratégie à partir du Portail Azure.

Étant donné que le client d’étiquetage unifié et le client Classic requièrent une installation distincte pour Office, vous devez télécharger et installer ces clients à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Quel client devez-vous utiliser ?

- Utilisez le **client d’étiquetage intégré à Office** pour vos ordinateurs Windows quand vous avez des applications Office 365 dont la version 1910 est minimale, que vous souhaitez utiliser les mêmes étiquettes et paramètres de stratégie que MacOS, iOS et Android, et que vous n’avez pas besoin de fonctionnalités dans  vos applications Office qui requièrent le client d’étiquetage unifié ou Classic. Ces fonctionnalités incluent la barre de Information Protection sous le ruban pour faciliter la sélection et la visibilité des étiquettes. Ce client prend en charge le basculement de comptes et parce qu’il n’utilise pas de complément Office, il offre de meilleures performances dans les applications Office que l’utilisation de l’un des clients Azure Information Protection.

- Utilisez l' **Azure information protection client d’étiquetage unifié** sur les ordinateurs Windows pour les étiquettes et les paramètres de stratégie qui peuvent également être utilisés par MacOS, iOS et Android. vous souhaitez étiqueter les fichiers indépendamment des applications Office 365 et vous n’avez pas besoin de fonctionnalités sont uniquement prises en charge par le client classique. Ces fonctionnalités incluent actuellement la protection du contenu avec une clé locale (HYOK) et une version de disponibilité générale du scanneur pour les magasins de données locaux.

- Installez le **client Azure information protection (Classic)** sur les ordinateurs Windows si vous avez besoin d’une version du client qui possède des fonctionnalités qui ne sont pas encore disponibles avec le client d’étiquetage unifié. Bien que ce client puisse utiliser les mêmes étiquettes que celles utilisées par MacOS, iOS et Android, il possède des paramètres de stratégie différents. Votre compromis est donc l’administration à l’aide d’un autre portail de gestion et d’une expérience utilisateur différente pour les utilisateurs.

La dernière version du client d’étiquetage unifié l’amène à fermer la parité dans les fonctionnalités avec le client classique. À mesure que cet intervalle se ferme, vous pouvez vous attendre à ce que les nouvelles fonctionnalités soient ajoutées uniquement au client d’étiquetage unifié. Pour cette raison, nous vous recommandons de déployer le client d’étiquetage unifié si son ensemble de fonctionnalités et ses fonctionnalités actuelles répondent aux besoins de votre entreprise. Si ce n’est pas le cas, ou si vous avez configuré des étiquettes dans le Portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](../configure-policy-migrate-labels.md), utilisez le client classique.

Vous pouvez utiliser différents clients dans le même environnement pour prendre en charge différents besoins de l’entreprise, comme illustré dans l’exemple de déploiement suivant. Dans un environnement client mixte, nous vous recommandons d’utiliser des étiquettes unifiées afin que les clients partagent le même ensemble d’étiquettes pour faciliter l’administration. Par défaut, les nouveaux clients ont des étiquettes unifiées, car leurs locataires se trouvent sur la plateforme d’étiquetage unifiée. Pour plus d’informations, consultez [Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Si vous disposez d’un ordinateur Windows qui exécute les applications Office 365 dont la version 1910 est minimale et l’une des Azure Information Protection clients est installée, par défaut, le client d’étiquetage intégré est désactivé dans les applications Office. Toutefois, vous pouvez modifier ce comportement pour utiliser le client d’étiquetage intégré uniquement pour vos applications Office. Avec cette configuration, le client Azure Information Protection (étiquetage classique ou unifié) reste disponible pour l’étiquetage dans l’Explorateur de fichiers, PowerShell et le scanneur. Pour obtenir des instructions sur la désactivation du client Azure Information Protection dans les applications Office 365, consultez la section [peut être sensible à des étiquettes exécutées en même temps que le client Azure information protection dans Office pour Windows ?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#can-sensitivity-labels-run-alongside-the-azure-information-protection-client-in-office-for-windows) à partir de la documentation Office.

##### <a name="example-deployment-strategy"></a>Exemple de stratégie de déploiement :

- Pour la majorité des utilisateurs, vous déployez le client d’étiquetage unifié Azure Information Protection, car ce client répond aux besoins de l’entreprise pour ces utilisateurs. 
    
    Pour ces utilisateurs, leur étiquetage est très similaire sur Windows, Mac, iOS et Android, car ils ont les mêmes étiquettes publiées et les mêmes paramètres de stratégie. En tant qu’administrateur, vous gérez ces étiquettes et paramètres de stratégie dans le même centre de gestion.

- Vous installez également le client d’étiquetage unifié pour vous-même, afin de tester la version préliminaire du scanneur Azure Information Protection.

- Pour un sous-ensemble d’utilisateurs, vous déployez le client classique, car ces utilisateurs nécessitent des étiquettes qui appliquent la protection de votre propre clé (HYOK).
    
    Pour ces utilisateurs, ils ont une expérience d’étiquetage légèrement différente lorsqu’ils utilisent ce client. Par exemple, ils voient un bouton **protéger** au lieu d’un bouton de **sensibilité** dans les applications Office. En tant qu’administrateur, vous devez gérer les étiquettes des paramètres HYOK et des paramètres de stratégie dans un autre centre de gestion pour les étiquettes et les paramètres des autres plateformes clientes.

- Vous avez des magasins de données locaux avec des documents qui doivent être analysés à la recherche d’informations sensibles ou classifiées et protégées. Pour une utilisation en production, vous déployez le client Classic sur les serveurs pour exécuter le scanneur de Azure Information Protection.

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Comparer les clients d’étiquetage pour les ordinateurs Windows

Utilisez le tableau suivant pour comparer les fonctionnalités prises en charge par les trois clients d’étiquetage pour les ordinateurs Windows.

Pour comparer les fonctionnalités d’étiquetage de sensibilité intégrées à Office sur différentes plateformes de système d’exploitation (Windows, MacOS, iOS et Android) et pour le Web, consultez la documentation Office, [Quelles sont les fonctionnalités d’étiquette de sensibilité prises en charge dans Office aujourd’hui ?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#what-sensitivity-label-capabilities-are-supported-in-office-today)

|Composant|Client classique|Client d’étiquetage unifié|Client d’étiquetage Office intégré|
|:------|:------------:|:---------------------:|:-----------------------------:|
|Étiquetage manuel :| **Oui** | **Oui** |**Oui** |
|Étiquette par défaut :| **Oui** | **Oui** | **Oui** |
|Étiquetage automatique ou recommandé :| **Oui** | **Oui** | Non |
|Étiquetage obligatoire :| **Oui** | **Oui** | Non |
|Autorisations définies par l’utilisateur pour une étiquette :<br />-Ne pas transférer pour les e-mails<br />-Autorisations personnalisées pour Word, Excel, PowerPoint, Explorateur de fichiers| **Oui** | **Oui** | Non |
|Prise en charge multilingue des étiquettes :| **Oui** | **Oui** |**Oui** |
|Héritage d’étiquette à partir des pièces jointes aux e-mails :| **Oui** | **Oui**  |Non |
|Les personnalisations qui incluent :<br />- Étiquette par défaut pour e-mail<br />-Messages contextuels dans Outlook <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| **Oui** <sup>1</sup> | **Oui** <sup>2</sup> | Non |
|Scanneur pour magasins de données locaux :| **Oui** | **Oui <br />(version préliminaire)** | Non |
|Création centralisée de rapports (analytique) :| **Oui** | **Oui** | Non |
|Les autorisations personnalisées sont définies indépendamment d’une étiquette :| **Oui** | **Oui** <sup>3</sup>| Non |
|Barre Information Protection dans les applications Office :| **Oui** | **Oui**| Non |
|Marquages visuels en tant qu’action d’étiquette (en-tête, pied de page, filigrane) :| **Oui** | **Oui** | **Oui**|
|Marquages visuels par application :| **Oui** | Non | Non |
|Marquages visuels dynamiques avec des variables :| **Oui** | Non | Non |
|Étiquette avec l’Explorateur de fichiers :| **Oui** | **Oui** | Non |
|Visionneuse pour les fichiers protégés (texte, images, PDF,. pfile) :| **Oui** | **Oui** | Non|
|Prise en charge PPDF pour l’application des étiquettes :| **Oui** | Non | Non |
|Applets de commande d’étiquetage PowerShell :| **Oui** | **Oui** <sup>4</sup> | Non |
|Gestion manuelle des fichiers de stratégie pour les ordinateurs déconnectés :| **Oui** |**Oui** <sup>6</sup>| Non |
|Prise en charge hors connexion des actions de protection :| **Oui** | **Oui** <sup>5</sup> | **Oui** |
|Prise en charge de HYOK :| **Oui** | Non | Non |
|Journalisation de l’utilisation dans observateur d’événements :| **Oui** | Non |Non |
|Afficher le bouton ne pas transférer dans Outlook :| **Oui** | Non | Non |
|Suivre les documentés protégés :| **Oui** | **Oui** <sup>7</sup> | Non |
|Révoquer les documents protégés :| **Oui** | Non | Non |
|Mode Protection uniquement (pas d’étiquettes) :| **Oui** | Non | Non |
|Prise en charge du changement de compte :| Non | Non | **Oui** |
|Prise en charge des services AD RMS :| **Oui** | Non <sup>8</sup> | Non |

Notes de bas de page :

<sup>1</sup> ces paramètres, et bien plus encore, sont pris en charge en tant que [Paramètres client avancés que vous configurez dans la portail Azure](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal).

<sup>2</sup> ces paramètres, et bien plus encore, sont pris en charge en tant que [Paramètres avancés que vous configurez avec PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).

<sup>3</sup> pris en charge par l’Explorateur de fichiers et PowerShell. Dans les applications Office, les utilisateurs peuvent sélectionner les **informations de fichier** > **protéger le document** > **restreindre l’accès**.

<sup>4</sup> aucune prise en charge de la suppression de la protection des fichiers de conteneur (zip,. rar,. 7z,. MSG et. pst).

<sup>5</sup> pour l’Explorateur de fichiers et les commandes PowerShell, l’utilisateur doit être connecté à Internet pour protéger des fichiers.

<sup>6</sup> pris en charge pour l’étiquetage avec l’Explorateur de fichiers, PowerShell et le scanneur. Non pris en charge pour l’étiquetage dans les applications Office.

<sup>7</sup> le site de suivi des documents pris en charge par le client classique n’est pas pris en charge par le client d’étiquetage unifié. Toutefois, si vous n’avez pas besoin d’enregistrer d’abord le document pour le suivi, les administrateurs peuvent utiliser la [création de rapports centralisée](../reports-aip.md) pour déterminer si les documents protégés sont accessibles à partir d’ordinateurs Windows et si l’accès a été accordé ou refusé. 

<sup>8</sup> les actions d’étiquetage et de protection ne sont pas prises en charge. Toutefois, pour un déploiement AD RMS, la visionneuse peut ouvrir des documents protégés lorsque vous utilisez l' [extension d’appareil Mobile services AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Comparaisons détaillées pour les clients Azure Information Protection

Lorsque le client Azure Information Protection (Classic) et le Azure Information Protection client d’étiquetage unifié prennent tous deux en charge la même fonctionnalité, utilisez le tableau suivant pour identifier les différences fonctionnelles entre les deux clients.

|Fonctionnalités |Client classique|Client d’étiquetage unifié|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurer :| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|Sélection et affichage d’étiquette en cas d’application dans les applications Office :|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|Gérer la barre Information Protection dans les applications Office :|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Protéger** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, par défaut, elle est masquée dans cette application, mais continue de s’afficher automatiquement dans les applications récemment ouvertes. <br /><br /> Pour les administrateurs : <br /><br />- Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre à la première ouverture d’une application, et de contrôler si la barre reste automatiquement masquée pour les applications récemment ouvertes une fois qu’un utilisateur a choisi de masquer la barre|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Critère de diffusion** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, celle-ci est masquée dans cette application et dans les applications récemment ouvertes <br /><br />Pour les administrateurs : <br /><br />-Paramètre PowerShell pour gérer la barre |
|Couleur d’étiquette : | À configurer dans le portail Azure | Conservé après la migration des étiquettes et configurable avec [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Les étiquettes prennent en charge différentes langues :| À configurer dans le portail Azure | Configurer à l’aide d’Office 365 Security & Compliance PowerShell et le paramètre *LocaleSettings* pour [New-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) et [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|Mise à jour de la stratégie : | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 24 heures | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 4 heures|
|Formats pris en charge pour PDF :| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /><br /> - .ppdf <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br /> <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint|
|Fichiers protégés de façon générique (. pfile) ouverts avec la visionneuse :| Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché, modifié et enregistré sans protection | Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché et modifié, mais pas enregistré|
|Cmdlets prises en charge :| Applets de commande pour l’étiquetage et les applets de commande pour la protection uniquement | Applets de commande pour l’étiquetage :<br /><br /> Set-AIPFileClassification et Set-AIPFileLabel ne prennent pas en charge le paramètre *owner* <br /><br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> Set-AIPFileClassification prend en charge le paramètre *WhatIf* , afin qu’il puisse être exécuté en mode détection <br /><br /> La cmdlet Set-AIPFileLabel ne prend pas en charge le paramètre *EnableTracking*. <br /><br /> La cmdlet Get-AIPFileStatus ne retourne aucune information d’étiquette à partir d’autres abonnés et n’affiche pas le paramètre *RMSIssuedTime*.<br /><br />En outre, le *paramètre LabelingMethod* pour la fonction de récupération de l' **activité** de l’accès à AIPFileStatus affiche **Privileged** ou standard au lieu du **Manuel** ou **automatique**. Pour plus d’informations, consultez la [documentation en ligne](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Invites de justification (si configurées) par action dans Office : | Fréquence : par fichier <br /><br /> Diminution du niveau de confidentialité <br /><br /> Suppression d’une étiquette<br /><br /> Suppression de la protection | Fréquence : par session <br /><br /> Diminution du niveau de confidentialité<br /><br /> Suppression d’une étiquette|
|Supprimer les actions de l’étiquette appliquée : | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou l’étiquette automatique (si configurée) n’est pas appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.  <br /><br />| L’utilisateur n’a pas à confirmer la suppression.<br /><br /> L’étiquette par défaut ou l’étiquette automatique (si configurée) est appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.|
|Étiquettes automatiques et recommandées : | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br /><br />- Nombre de valeurs uniques/non uniques <br /><br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br /><br />- Nombre de valeurs uniques seulement <br /><br />- Nombre de valeurs minimales et maximales <br /><br />- Prise en charge des clauses AND et OR avec les types d’informations <br /><br />- Dictionnaire de mots clés<br /><br />- Niveau de confiance et proximité des caractères personnalisables|
|Conseil de stratégie personnalisable pour les étiquettes automatiques et recommandées : | Oui <br /><br />Utiliser la Portail Azure pour remplacer le message par défaut pour les utilisateurs | Non <br /><br /> Bien que les centres d’administration disposent d’une option pour fournir un Conseil de stratégie personnalisé, cette option n’est pas prise en charge par le client d’étiquetage unifié.|
|Modifier le comportement de protection par défaut pour les types de fichiers : | Vous pouvez utiliser des [modifications du Registre](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) pour remplacer les valeurs par défaut de protection native et générique | Vous pouvez utiliser [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) pour modifier les types de fichiers qui sont protégés|

Pour une comparaison détaillée des différences de comportement pour des paramètres de protection spécifiques, consultez [comparaison du comportement des paramètres de protection pour une étiquette](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Fonctionnalités non planifiées dans le client d’étiquetage unifié Azure Information Protection

Bien que le client d’étiquetage unifié Azure Information Protection soit toujours en cours de développement, les fonctionnalités et les différences de comportement suivantes du client classique ne sont pas prévues pour le moment dans les futures versions du client d’étiquetage unifié : 

- Prendre en charge les applications Office pour les ordinateurs déconnectés avec gestion manuelle des fichiers de stratégie

- Autorisations personnalisées en tant qu’option distincte que les utilisateurs peuvent sélectionner dans les applications Office : Word, Excel et PowerPoint

- Suivre et révoquer depuis des applications Office et l’Explorateur de fichiers

- Barre de titre et info-bulle Azure Information Protection

- Mode protection uniquement (aucune étiquette) à l’aide de modèles

- Protéger le document PDF en tant que format .ppdf

- Afficher le bouton Ne pas transférer dans Outlook

- Stratégie de démonstration

- Justification de la suppression de la protection

- Invite de confirmation voulez **-vous supprimer cette étiquette ?** pour les utilisateurs lorsque vous n’utilisez pas le paramètre de stratégie pour la justification

- Applets de commande PowerShell distinctes pour la connexion à un service Rights Management


### <a name="parent-labels-and-their-sublabels"></a>Étiquettes parentes et sous-étiquettes associées 

Le client Azure Information Protection (Classic) ne prend pas en charge les configurations qui spécifient une étiquette parente avec des sous-étiquettes. Ces configurations incluent la spécification d’une étiquette par défaut et d’une étiquette pour la classification automatique ou recommandée. Si une étiquette dispose de sous-étiquettes, vous pouvez spécifier l’une d’elles, mais pas l’étiquette parente.

Pour des raisons de parité, le client d’étiquetage unifié Azure Information Protection ne prend pas non plus en charge l’application d’étiquettes parentes comportant des sous-étiquettes, même si elles peuvent être sélectionnées dans les centres d’administration. Dans ce scénario, le client d’étiquetage unifié Azure Information Protection n’applique pas l’étiquette parente.

## <a name="next-steps"></a>Étapes suivantes

Pour installer et configurer les clients Azure Information Protection, utilisez la documentation suivante :

- [Client Azure Information Protection](AIP-client.md)

- [Client d’étiquetage unifié Azure Information Protection](unifiedlabelingclient-version-release-history.md)

Pour plus d’informations sur l’utilisation du client d’étiquetage intégré pour les applications Office 365, consultez [étiquettes de sensibilité dans les applications Office](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps).
