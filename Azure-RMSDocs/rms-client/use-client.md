---
title: Client pour Azure Information Protection-AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 94348ea8b214e0ece964dba2d0a49f6e03de49d0
ms.sourcegitcommit: 908ca5782fe86e88502dccbd0e82fa18db9b96ad
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71060116"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- Le client peut être le client Azure Information Protection (Classic), le client d’étiquetage unifié Azure Information Protection ou le client Rights Management. Quel que soit le client que vous utilisez, il s’intègre aux applications que vous exécutez sur des ordinateurs et des appareils mobiles. 
- Le service réside dans le cloud (Azure Information Protection, qui utilise le service Azure Rights Management pour la protection des données) ou localement (Active Directory Rights Management Services, plus couramment appelés services AD RMS). 

Le client Azure Information Protection (Classic) et le client d’étiquetage unifié Azure Information Protection prennent en charge la classification et la protection avec étiquetage. Le client classique prend également en charge la protection sans étiquetage. Les deux clients s’intègrent aux applications Office et doivent être installés séparément.

Le client Rights Management (RMS) est installé automatiquement avec certaines applications, telles que les applications Office, le client Azure Information Protection (Classic) et le client d’étiquetage unifié Azure Information Protection, ainsi que les applications compatibles avec RMS. des éditeurs de logiciels. Toutefois, il peut également être [installé de manière autonome](https://www.microsoft.com/en-us/download/details.aspx?id=38396) pour prendre en charge la [synchronisation des fichiers à partir des bibliothèques protégées par IRM et de OneDrive Entreprise](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668), et pour les développeurs souhaitant intégrer la protection de gestion des droits aux applications métier.

## <a name="choose-which-azure-information-protection-client-to-use"></a>Choisir le client Azure Information Protection à utiliser

Le **client Azure information protection (Classic)** télécharge des étiquettes et des paramètres de stratégie à partir du portail Azure. Pour plus d’informations sur ce client, consultez [le client Azure information protection: Historique de publication et politique de support des versions](client-version-release-history.md).

Le **client d’étiquetage unifié Azure Information Protection** télécharge les étiquettes et les paramètres de stratégie à partir des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 et le Centre de conformité Microsoft 365. Pour plus d’informations sur ce client, consultez [le Azure information protection client d’étiquetage unifié: Informations sur la version](unifiedlabelingclient-version-release-history.md).

Quel client convient-il d’installer ?

- Installez le client d’étiquetage unifié Azure Information Protection pour les étiquettes qui peuvent également être utilisées par MacOS, iOS et Android, et si vous n’avez pas besoin des nombreuses fonctionnalités qui ne sont pas encore prises en charge. Ces fonctionnalités incluent la protection du contenu avec une clé locale (HYOK) et une version de disponibilité générale du scanneur pour les magasins de données locaux.

- Installez le client Azure Information Protection (Classic) si vous avez besoin d’une version du client qui possède des fonctionnalités qui ne sont pas encore disponibles avec le client d’étiquetage unifié. Le compromis est que les étiquettes ne peuvent pas être utilisées sur d’autres plateformes clientes et l’administration à l’aide d’un autre portail de gestion.

La dernière version de la disponibilité générale du client d’étiquetage unifié l’amène à fermer la parité dans les fonctionnalités avec le client classique. À mesure que cet intervalle se ferme, vous pouvez vous attendre à ce que les nouvelles fonctionnalités soient ajoutées uniquement au client d’étiquetage unifié. Pour cette raison, nous vous recommandons de déployer le client d’étiquetage unifié si son ensemble de fonctionnalités et ses fonctionnalités actuelles répondent aux besoins de votre entreprise. Si ce n’est pas le cas, ou si vous avez configuré des étiquettes dans le Portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](../configure-policy-migrate-labels.md), utilisez le client classique.

Vous pouvez également installer les deux clients dans le même environnement pour prendre en charge les différents besoins de l’entreprise, comme illustré dans l’exemple suivant. Pour ce scénario, nous vous recommandons de migrer les étiquettes dans le Portail Azure afin que les deux ensembles de clients partagent le même ensemble d’étiquettes pour faciliter l’administration.

##### <a name="example-deployment-strategy"></a>Exemple de stratégie de déploiement:

- Pour la majorité des utilisateurs, vous déployez le client d’étiquetage unifié Azure Information Protection, car ce client répond aux besoins de l’entreprise pour ces utilisateurs. 
    
    Pour ces utilisateurs, leur étiquetage est très similaire sur Windows, Mac, iOS et Android, car ils ont les mêmes étiquettes publiées et les mêmes paramètres de stratégie. En tant qu’administrateur, vous gérez ces étiquettes et paramètres de stratégie dans le même centre de gestion.

- Vous installez également le client d’étiquetage unifié pour vous-même, afin de tester la version préliminaire du scanneur Azure Information Protection et des nouvelles fonctionnalités du client.

- Pour un sous-ensemble d’utilisateurs, vous déployez le client classique, car ces utilisateurs nécessitent des étiquettes qui appliquent la protection de votre propre clé (HYOK).
    
    Pour ces utilisateurs, ils ont une expérience d’étiquetage légèrement différente lorsqu’ils utilisent ce client. Par exemple, ils voient un bouton **protéger** au lieu d’un bouton de **sensibilité** dans les applications Office. En tant qu’administrateur, vous devez gérer les étiquettes des paramètres HYOK et des paramètres de stratégie dans un autre centre de gestion pour les étiquettes et les paramètres des autres plateformes clientes.

- Vous avez des magasins de données locaux avec des documents qui doivent être analysés à la recherche d’informations sensibles ou classifiées et protégées. Pour une utilisation en production, vous déployez le client Classic sur les serveurs pour exécuter le scanneur de Azure Information Protection.

### <a name="compare-the-clients"></a>Comparer les clients

Utilisez le tableau suivant pour comparer les fonctionnalités prises en charge par les deux clients Azure Information Protection.

|Fonctionnalité|Client classique|Client d’étiquetage unifié|
|-------|-----------------------------------|----------------------------------------------------|
|Étiquetage des actions : manuel, recommandé, automatique| Oui | Oui |
|Création centralisée de rapports (analytique) :| Oui | Oui, avec des restrictions :<br /><br /> -Les types d’informations sensibles personnalisés sont pris en charge avec la version préliminaire |
|Visionneuse pour les fichiers protégés (texte, images, PDF,. pfile) :| Oui | Oui |
|Prise en charge multilingue des étiquettes:| Oui | Oui |
|Héritage d’étiquette à partir des pièces jointes aux e-mails :| Oui | Oui  |
|Les personnalisations qui incluent:<br />- Étiquette par défaut pour e-mail<br />-Messages contextuels dans Outlook <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| Oui <br /><br /> Pris en charge comme [paramètres du client avancé que vous configurez dans le portail Azure](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal)| Oui <br /><br /> Pris en charge comme [Paramètres avancés que vous configurez avec PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) |
|Autorisations définies par l’utilisateur :| Oui | Oui |
|Scanneur pour magasins de données locaux :| Oui | Oui-version préliminaire |
|Autorisations personnalisées :| Oui | Explorateur de fichiers et PowerShell <br /><br /> Dans les applications Office, comme alternative, les utilisateurs peuvent sélectionner les **informations** > de fichier**protéger le document** > **restreindre l’accès** ou les administrateurs peuvent configurer une étiquette pour les autorisations définies par l’utilisateur|
|Barre Information Protection dans les applications Office :| Oui | Oui, avec des restrictions :<br /><br /> - Pas de titre ou d’info-bulle personnalisable<br /><br /> -Couleur de l’étiquette non affichée pour l’étiquette appliquée, sauf si vous utilisez la version préliminaire|
|Les étiquettes peuvent appliquer des marquages visuels (en-tête, pied de page, filigrane) :| Oui | Oui, avec des restrictions :<br /><br /> - Les en-têtes et les pieds de page ne gèrent pas les variables pour les valeurs dynamiques <br /><br /> - Pas de prise en charge pour Word, Excel, PowerPoint et Outlook de différents marquages visuels|
|Dans l’Explorateur de fichiers, actions déclenchées par clic droit :| Oui | Oui, avec des restrictions :<br /><br /> -Impossible de protéger les documents PDF au format ancien. ppdf <br /><br />  - Pas de prise en charge du mode Protection uniquement|
|Commandes PowerShell :| Oui | Oui, avec des restrictions :<br /><br />-Impossible de supprimer la protection des fichiers de conteneur (zip,. rar,. 7z,. MSG et. pst)|
|Prise en charge hors connexion des actions de protection :| Oui | Oui, avec des restrictions : <br /><br />- Pour l’Explorateur de fichiers et les commandes PowerShell, l’utilisateur doit être connecté à Internet pour protéger les fichiers. |
|Prise en charge des ordinateurs déconnectés avec gestion de fichier de stratégie manuelle :| Oui |Non |
|Prise en charge de HYOK :| Oui | Non <br /><br /> Les étiquettes que vous migrez à partir du portail Azure et qui sont configurées pour la protection HYOK sont affichées par le client d’étiquetage unifié Azure Information Protection, mais n’appliquent pas de protection. |
|Journalisation de l’utilisation dans l’observateur d’événements :| Oui | Non|
|Afficher le bouton Ne pas transférer dans Outlook| Oui | Non |
|Suivre et révoquer :| Oui | Non |
|Mode protection uniquement (aucune étiquette) à l’aide de modèles:| Oui | Non |
|Prise en charge des services AD RMS :| Oui | Seule l’action suivante est prise en charge :<br /><br /> - La visionneuse peut ouvrir des documents protégés quand vous déployez l’[extension Appareils mobiles AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="detailed-comparisons-for-the-clients"></a>Comparaisons détaillées pour les clients

Lorsque les deux clients prennent en charge la même fonctionnalité, utilisez le tableau suivant pour identifier les différences fonctionnelles entre les deux clients.

|Fonctionnalité |Client classique|Client d’étiquetage unifié|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurer :| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|Sélection et affichage d’étiquette en cas d’application dans les applications Office :|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|Gérer la barre Information Protection dans les applications Office :|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Protéger** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, par défaut, elle est masquée dans cette application, mais continue de s’afficher automatiquement dans les applications récemment ouvertes. <br /><br /> Pour les administrateurs : <br /><br />- Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre à la première ouverture d’une application, et de contrôler si la barre reste automatiquement masquée pour les applications récemment ouvertes une fois qu’un utilisateur a choisi de masquer la barre|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Critère de diffusion** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, celle-ci est masquée dans cette application et dans les applications récemment ouvertes <br /><br />Pour les administrateurs : <br /><br />-Paramètre PowerShell pour gérer la barre |
|Couleur d’étiquette : | À configurer dans le portail Azure | Conservé après la migration des étiquettes vers Office 365 et configurable avec PowerShell <br /><br /> Les couleurs peuvent être configurées à l’aide de [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Les étiquettes prennent en charge différentes langues:| À configurer dans le portail Azure | Configurer à l’aide d’Office 365 Security & Compliance PowerShell et le paramètre *LocaleSettings* pour [New-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) et [Set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|Mise à jour de la stratégie : | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 24 heures | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 4 heures|
|Formats pris en charge pour PDF :| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /><br /> - .ppdf <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br /> <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint|
|Fichiers protégés de façon générique (. pfile) ouverts avec la visionneuse :| Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché, modifié et enregistré sans protection | Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché et modifié, mais pas enregistré|
|Cmdlets prises en charge :| Applets de commande pour l’étiquetage et les applets de commande pour la protection uniquement | Applets de commande pour l’étiquetage :<br /><br />Set-AIPFileClassification, Set-AIPFileLabel et Set-AIPFileStatus ne prennent pas en charge les chemins SharePoint, sauf si vous utilisez la version préliminaire <br /><br /> Set-AIPFileClassification et Set-AIPFileLabel ne prennent pas en charge le paramètre *owner* <br /><br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> Set-AIPFileClassification prend en charge le paramètre *WhatIf* , afin qu’il puisse être exécuté en mode détection <br /><br /> La cmdlet Set-AIPFileLabel ne prend pas en charge le paramètre *EnableTracking*. <br /><br /> La cmdlet Get-AIPFileStatus ne retourne aucune information d’étiquette à partir d’autres abonnés et n’affiche pas le paramètre *RMSIssuedTime*.<br /><br />En outre, le *paramètre LabelingMethod* pour la fonction de récupération de l' **activité** de l’accès à AIPFileStatus affiche **Privileged** ou standard au lieu du **Manuel** ou **automatique**. Pour plus d’informations, consultez la [documentation en ligne](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Invites de justification (si configurées) par action dans Office : | Fréquence : par fichier <br /><br /> Diminution du niveau de confidentialité <br /><br /> Suppression d’une étiquette<br /><br /> Suppression de la protection | Fréquence : par session <br /><br /> Diminution du niveau de confidentialité<br /><br /> Suppression d’une étiquette|
|Supprimer les actions de l’étiquette appliquée : | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou l’étiquette automatique (si configurée) n’est pas appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.  <br /><br />| L’utilisateur n’a pas à confirmer la suppression.<br /><br /> L’étiquette par défaut ou l’étiquette automatique (si configurée) est appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.|
|Étiquettes automatiques et recommandées: | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br /><br />- Nombre de valeurs uniques/non uniques <br /><br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br /><br />- Nombre de valeurs uniques seulement <br /><br />- Nombre de valeurs minimales et maximales <br /><br />- Prise en charge des clauses AND et OR avec les types d’informations <br /><br />- Dictionnaire de mots clés<br /><br />- Niveau de confiance et proximité des caractères personnalisables|
|Conseil de stratégie personnalisable pour les étiquettes automatiques et recommandées: | Oui <br /><br />Utiliser la Portail Azure pour remplacer le message par défaut pour les utilisateurs | Non <br /><br /> Bien que les centres d’administration disposent d’une option pour fournir un Conseil de stratégie personnalisé, cette option n’est pas prise en charge par le client d’étiquetage unifié.|
|Modifier le niveau de protection par défaut des fichiers: | Oui <br /><br />Vous pouvez utiliser des [modifications du Registre](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) pour remplacer les valeurs par défaut de protection native et générique | Non |

Pour une comparaison détaillée des différences de comportement pour des paramètres de protection spécifiques, consultez [comparaison du comportement des paramètres de protection pour une étiquette](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Fonctionnalités non planifiées dans le client d’étiquetage unifié Azure Information Protection

Bien que le client d’étiquetage unifié Azure Information Protection soit toujours en cours de développement, les fonctionnalités et les différences de comportement suivantes du client classique ne sont pas prévues pour le moment dans les futures versions du client d’étiquetage unifié: 

- Prendre en charge les applications Office pour les ordinateurs déconnectés avec gestion manuelle des fichiers de stratégie

- Les autorisations personnalisées sont des options distinctes que les utilisateurs peuvent sélectionner dans les applications Office: Word, Excel et PowerPoint

- Suivre et révoquer depuis des applications Office et l’Explorateur de fichiers

- Barre de titre et info-bulle Azure Information Protection

- Mode protection uniquement (aucune étiquette) à l’aide de modèles

- Protéger le document PDF en tant que format .ppdf

- Afficher le bouton Ne pas transférer dans Outlook

- Stratégie de démonstration

- Justification de la suppression de la protection

- Invite de confirmation voulez **-vous supprimer cette étiquette?** pour les utilisateurs lorsque vous n’utilisez pas le paramètre de stratégie pour la justification

- Étiqueter un document Office avec une propriété personnalisée existante (paramètres du client avancé SyncPropertyName et SyncPropertyState)

- Applets de commande PowerShell distinctes pour la connexion à un service Rights Management


#### <a name="parent-labels-and-their-sublabels"></a>Étiquettes parentes et sous-étiquettes associées 

Le client Azure Information Protection (Classic) ne prend pas en charge les configurations qui spécifient une étiquette parente avec des sous-étiquettes. Ces configurations incluent la spécification d’une étiquette par défaut et d’une étiquette pour la classification automatique ou recommandée. Si une étiquette dispose de sous-étiquettes, vous pouvez spécifier l’une d’elles, mais pas l’étiquette parente.

Pour des raisons de parité, le client d’étiquetage unifié Azure Information Protection ne prend pas non plus en charge l’application d’étiquettes parentes comportant des sous-étiquettes, même si elles peuvent être sélectionnées dans les centres d’administration. Dans ce scénario, le client d’étiquetage unifié Azure Information Protection n’applique pas l’étiquette parente.

## <a name="see-also"></a>Voir aussi
Consultez la documentation suivante pour en savoir plus sur le déploiement et l’utilisation de ces clients :

- [Client Azure Information Protection](AIP-client.md)

- [Client d’étiquetage unifié Azure Information Protection](unifiedlabelingclient-version-release-history.md)

- [Notes sur le déploiement du client RMS](client-deployment-notes.md)

Bien que le client Azure Information Protection (Classic) puisse être utilisé avec AD RMS, ce client est mieux adapté à l’utilisation de ses services Azure. Azure Information Protection et son service de protection, Azure Rights Management. Pour comparer les services d’Azure Information Protection, voir [Comparaison d’Azure Information Protection avec AD RMS](../compare-on-premise.md).
