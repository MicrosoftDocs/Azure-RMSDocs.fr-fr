---
title: Le client pour Azure Information Protection - AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 5bb792bcc396d1aac4fcb7cb0e6558a65988477a
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236862"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et e-mails d’une organisation :

- Le client peut être le client Azure Information Protection, le client d’étiquetage unifié Azure Information Protection ou le client Rights Management. Retenue de ces clients vous utilisez, il s’intègre aux applications que vous exécutez sur des ordinateurs et appareils mobiles. 

- Le service réside dans le cloud (Azure Information Protection, qui utilise le service Azure Rights Management pour la protection des données) ou localement (Active Directory Rights Management Services, plus couramment appelés services AD RMS). 

Le client Azure Information Protection et le client d’étiquetage unifié Azure Information Protection prend en charge la classification et la protection avec l’étiquetage. Le client Azure Information Protection prend également en charge la protection sans l’étiquetage. Les deux clients s’intègrent avec les applications Office et doivent être installés séparément.

Le client Rights Management (RMS) est automatiquement installé avec certaines applications, telles que les applications Office, le client Azure Information Protection et Azure Information Protection unifiée étiquetage client et les applications compatibles RMS à partir de éditeurs de logiciels. Toutefois, il peut également être [installé de manière autonome](https://www.microsoft.com/en-us/download/details.aspx?id=38396) pour prendre en charge la [synchronisation des fichiers à partir des bibliothèques protégées par IRM et de OneDrive Entreprise](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668), et pour les développeurs souhaitant intégrer la protection de gestion des droits aux applications métier.

## <a name="choose-which-azure-information-protection-client-to-use"></a>Choisir le client Azure Information Protection à utiliser

Le **client Azure Information Protection** télécharge les étiquettes et les paramètres de stratégie à partir du portail Azure. Pour plus d’informations sur ce client, consultez le [client Azure Information Protection : Historique de publication et politique de support des versions](client-version-release-history.md).

Le **client d’étiquetage unifié Azure Information Protection** télécharge les étiquettes et les paramètres de stratégie à partir des centres d’administration : le Centre de sécurité et conformité Office 365, le Centre de sécurité Microsoft 365 et le Centre de conformité Microsoft 365. Pour plus d’informations sur ce client, consultez le [étiquetage client unifié, Azure Information Protection : Informations sur la version](unifiedlabelingclient-version-release-history.md).

Quel client convient-il d’installer ?

- Installer la version actuelle de la disponibilité du client étiquetage unifiée Azure Information Protection pour les étiquettes qui peut également être utilisée par Mac OS, iOS et Android et si vous n’avez pas besoin des fonctionnalités avancées, telles qu’avancée des paramètres client, les autorisations définies par l’utilisateur, une clé en local (HYOK), ou le moteur d’analyse pour les banques de données locales.
    
    La préversion du client Azure Information Protection unifiée étiquetage prend en charge les paramètres de client avancé et des autorisations définies par l’utilisateur, mais pas une clé en local (HYOK) ou le moteur d’analyse de données locales.

- Installer le client Azure Information Protection si vous avez besoin d’une version du client qui est en général de disponibilité avec des fonctionnalités avancées qui ne sont pas encore disponibles dans la disposition générale unifiée étiquetage client actuel. Le compromis est que les étiquettes ne peut pas être utilisés sur d’autres plateformes client.

Actuellement, le client Azure Information Protection et le client d’étiquetage unifié Azure Information Protection ne pas de parité de leurs fonctionnalités. Toutefois, avec la version préliminaire actuelle, cet écart se ferme et vous pouvez vous attendre de nouvelles fonctionnalités pour être ajouté uniquement au client Azure Information Protection unifié étiquetage. Pour cette raison, nous vous recommandons de que déployer le client d’étiquetage unifié Azure Information Protection si sa fonctionnalité et un ensemble de fonctionnalités actuel répond aux besoins de votre entreprise. Dans le cas contraire ou si vous avez configuré des étiquettes dans le portail Azure que vous n’avez pas encore [migrées vers le magasin d’étiquetage unifié](../configure-policy-migrate-labels.md), utilisez le client Azure Information Protection.

Vous pouvez également installer les deux clients dans le même environnement pour prendre en charge des besoins métier différents, comme illustré dans l’exemple suivant. Pour ce scénario, nous vous recommandons de que migrer les étiquettes dans le portail Azure afin que les deux ensembles de clients partagent le même jeu d’étiquettes pour faciliter l’administration.

##### <a name="example-deployment-strategy"></a>Stratégie de déploiement d’exemple :

- Pour la majorité des utilisateurs, vous déployez le client d’étiquetage unifié Azure Information Protection, car la plupart des utilisateurs n’avez pas besoin fonctions ou fonctionnalités qui sont disponibles uniquement avec le client Azure Information Protection. 
    
    Pour ces utilisateurs, leur expérience étiquetage est très similaire s’ils ont également des appareils qui exécutent Mac OS, iOS et Android, et ces appareils ont une version d’Office qui prend en charge des étiquettes de sensibilité.

- Simplement pour vous-même, vous installez la préversion du client étiquetage unifiée Azure Information Protection pour tester les nouvelles fonctionnalités qui incluent des autorisations définies par l’utilisateur et les paramètres de clients avancés.

- Pour un sous-ensemble d’utilisateurs, vous déployez le client Azure Information Protection, car ces utilisateurs ont besoin d’étiquettes qui appliquent la maintenez votre propre protection de clés (HYOK) ou d’une invite autorisations définies par l’utilisateur.
    
    Pour ces utilisateurs, ils ont des fonctionnalités complémentaires, mais une expérience légèrement différente si elles ont également les appareils qui exécutent Mac OS, iOS et Android et que ces appareils ont une version d’Office qui prend en charge des étiquettes de sensibilité. Par exemple, ils voient un **protéger** bouton au lieu d’un **sensibilité** bouton sur le ruban d’Office et la barre Information Protection peut être affiché par défaut.

- Vous avez des banques de données sur site avec des documents qui doivent être analysés pour des informations sensibles ou classifiés et protégés. Vous déployez le client Azure Information Protection sur les serveurs pour exécuter le scanneur Azure Information Protection.

### <a name="compare-the-clients"></a>Comparer les clients

Utilisez le tableau suivant pour aider à comparer les fonctionnalités qui sont prises en charge par les deux clients Azure Information Protection.

|Composant|Client Azure Information Protection|Azure Information Protection<br /> Client d’étiquetage unifié Azure Information Protection|
|-------|-----------------------------------|----------------------------------------------------|
|Étiquetage des actions : manuel, recommandé, automatique| Oui | Oui |
|Création centralisée de rapports (analytique) :| Oui | Oui, avec des restrictions :<br /><br /> - [Correspondances de contenu](../reports-aip.md#content-matches-for-deeper-analysis) nécessitent la préversion du client |
|Paramètres de réinitialisation et journaux d’exportation :| Oui | Oui |
|Autorisations définies par l’utilisateur :| Oui | Oui, avec des restrictions : <br /><br />-Pour Outlook uniquement (ne pas transférer) : Pris en charge<br /><br />-Pour Word, Excel, PowerPoint et l’Explorateur de fichiers : Prise en charge avec la préversion du client lorsque vous configurez l’étiquette dans le portail Azure |
|Autorisations personnalisées :| Oui | Explorateur de fichiers et de PowerShell (version préliminaire) <br /><br /> Dans les applications Office, les utilisateurs peuvent également sélectionner **Informations sur le fichier** > **Protéger le document** > **Restreindre l’accès**. |
|Barre Information Protection dans les applications Office :| Oui | Oui, avec des restrictions :<br /><br /> - Pas de titre ou d’info-bulle personnalisable<br /><br /> - Couleur d’étiquette non affichée pour l’étiquette appliquée|
|Les étiquettes peuvent appliquer des marquages visuels (en-tête, pied de page, filigrane) :| Oui | Oui, avec des restrictions :<br /><br /> - Les en-têtes et les pieds de page ne gèrent pas les variables pour les valeurs dynamiques <br /><br /> - Pas de prise en charge pour Word, Excel, PowerPoint et Outlook de différents marquages visuels|
|Dans l’Explorateur de fichiers, actions déclenchées par clic droit :| Oui | Oui, avec des restrictions :<br /><br /> - Impossible de protéger les documents PDF au format .ppdf <br /><br />  - Pas de prise en charge du mode Protection uniquement|
|Visionneuse des fichiers protégés :| Oui | Oui, avec des restrictions :<br /><br /> - Pour les fichiers protégés de manière générique (.pfile), contrairement à la visionneuse du client Azure Information Protection, il n’existe aucune possibilité d’enregistrer des modifications dans le fichier ouvert à l’origine.|
|Commandes PowerShell :| Oui | Oui, avec des restrictions :<br /><br />- Cmdlets incluses : [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus), [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions)(preview client), [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />-Actuellement, vous ne pouvez pas supprimer la protection à partir des fichiers de conteneur (zip, .rar, .7z, .msg et .pst)|
|Prise en charge hors connexion des actions de protection :| Oui | Oui, avec des restrictions : <br /><br />- Pour l’Explorateur de fichiers et les commandes PowerShell, l’utilisateur doit être connecté à Internet pour protéger les fichiers. |
|Prise en charge des ordinateurs déconnectés avec gestion de fichier de stratégie manuelle :| Oui |Non |
|Prise en charge de HYOK :| Oui | Non<br /><br /> Les étiquettes que vous migrez à partir du portail Azure et qui sont configurées pour la protection HYOK sont affichées par le client d’étiquetage unifié Azure Information Protection, mais n’appliquent pas de protection. |
|Journalisation de l’utilisation dans l’observateur d’événements :| Oui | Non|
|Héritage d’étiquette à partir des pièces jointes aux e-mails :| Oui | Oui (client en version préliminaire uniquement) |
|Afficher le bouton Ne pas transférer dans Outlook| Oui | Non |
|Les [personnalisations](client-admin-guide-customizations.md#available-advanced-client-settings) sont les suivantes :<br />- Étiquette par défaut pour e-mail<br />- Activer les autorisations personnalisées <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| Oui | Oui, à l’aide de [PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) (client en version préliminaire uniquement) |
|Scanneur pour magasins de données locaux :| Oui | Non |
|Suivre et révoquer :| Oui | Non |
|Mode protection uniquement (aucune étiquette) à l’aide de modèles :| Oui | Non |
|Prise en charge multilingue :| Oui | Non |
|Prise en charge des services AD RMS :| Oui | Seule l’action suivante est prise en charge :<br /><br /> - La visionneuse peut ouvrir des documents protégés quand vous déployez l’[extension Appareils mobiles AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="detailed-comparisons-for-the-clients"></a>Comparaisons détaillées pour les clients

Lorsque les deux clients prennent en charge la même fonctionnalité, utilisez le tableau suivant pour faciliter l’identification des différences fonctionnelles entre les deux clients.

|Fonctionnalité |Client Azure Information Protection|Azure Information Protection<br /> Client d’étiquetage unifié Azure Information Protection|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurer :| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|Sélection et affichage d’étiquette en cas d’application dans les applications Office :|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|Gérer la barre Information Protection dans les applications Office :|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Protéger** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, par défaut, elle est masquée dans cette application, mais continue de s’afficher automatiquement dans les applications récemment ouvertes. <br /><br /> Pour les administrateurs : <br /><br />- Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre à la première ouverture d’une application, et de contrôler si la barre reste automatiquement masquée pour les applications récemment ouvertes une fois qu’un utilisateur a choisi de masquer la barre|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Critère de diffusion** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, celle-ci est masquée dans cette application et dans les applications récemment ouvertes <br /><br />Pour les administrateurs : <br /><br />-Paramètre PowerShell pour gérer la barre (client en version préliminaire uniquement)|
|Couleur d’étiquette : | À configurer dans le portail Azure | Conservées après la migration d’étiquette à Office 365 et à configurer avec PowerShell <br /><br /> Nouvelles étiquettes créées dans les centres d’administration n’ont pas une couleur mais couleurs peuvent être configurés à l’aide de [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Mise à jour de la stratégie : | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 24 heures | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 4 heures|
|Formats pris en charge pour PDF :| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /><br /> - .ppdf <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br /> <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint|
|Cmdlets prises en charge :| Ensemble des cmdlets documentées pour [AzureInformationProtection](/powershell/module/azureinformationprotection) | Set-AIPAuthentication prend en charge les sessions non interactives à l’aide de la préversion du client uniquement <br /><br /> Les cmdlets Set-AIPFileClassification et Set-AIPFileLabel ne prennent pas en charge le paramètre *Propriétaire* ni les bibliothèques SharePoint Server. <br /><br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> Set-AIPFileClassification dans la préversion du client prend en charge la *WhatIf* paramètre, donc il peut être exécuté en mode de découverte <br /><br /> La cmdlet Set-AIPFileLabel ne prend pas en charge le paramètre *EnableTracking*. <br /><br /> La cmdlet Get-AIPFileStatus ne retourne aucune information d’étiquette à partir d’autres abonnés et n’affiche pas le paramètre *RMSIssuedTime*.<br /><br />En outre, le *LabelingMethod* affiche les paramètres de Get-AIPFileStatus **privilégié** ou **Standard** au lieu de **manuel** ou **Automatique**. Pour plus d’informations, consultez la [documentation en ligne](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Invites de justification (si configurées) par action dans Office : | Fréquence : par fichier <br /><br /> Diminution du niveau de confidentialité <br /><br /> Suppression d’une étiquette<br /><br /> Suppression de la protection | Fréquence : par session <br /><br /> Diminution du niveau de confidentialité<br /><br /> Suppression d’une étiquette|
|Supprimer les actions de l’étiquette appliquée : | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou l’étiquette automatique (si configurée) n’est pas appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.  <br /><br />| L’utilisateur n’a pas à confirmer la suppression.<br /><br /> L’étiquette par défaut ou l’étiquette automatique (si configurée) est appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.|
|Étiquettes automatiques et recommandées : | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br /><br />- Nombre de valeurs uniques/non uniques <br /><br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br /><br />- Nombre de valeurs uniques seulement <br /><br />- Nombre de valeurs minimales et maximales <br /><br />- Prise en charge des clauses AND et OR avec les types d’informations <br /><br />- Dictionnaire de mots clés<br /><br />- Niveau de confiance et proximité des caractères personnalisables|
|Conseil de stratégie personnalisables pour les étiquettes automatiques et recommandées : | Oui <br /><br />Utiliser le portail Azure pour remplacer le message par défaut pour les utilisateurs | Non <br /><br /> Bien que les centres d’administration ont une option permettant de fournir un Conseil de stratégie personnalisée, cette option n'est pas actuellement pris en charge par le client d’étiquetage unifié|
|Modification du niveau de protection par défaut des fichiers : | Oui <br /><br />Vous pouvez utiliser [des modifications du Registre](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) pour remplacer les valeurs par défaut de la protection native et générique | Non |

Pour une comparaison détaillée des différences de comportement pour les paramètres de protection spécifique, consultez [comparant le comportement des paramètres de protection pour une étiquette](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Fonctionnalité n’est ne pas planifiée pour être dans le client d’étiquetage unifié Azure Information Protection

Bien que le client d’étiquetage unifié Azure Information Protection est en cours de développement, les fonctionnalités suivantes et les différences de comportement à partir du client Azure Information Protection ne sont pas actuellement planifiées pour être disponible dans les versions futures pour Azure Client Information Protection unifiée étiquetage : 

- Autorisations personnalisées dans les applications Office : Word, Excel et PowerPoint

- Suivre et révoquer depuis des applications Office et l’Explorateur de fichiers

- Barre de titre et info-bulle Azure Information Protection

- Mode protection uniquement (aucune étiquette) à l’aide de modèles

- Protéger le document PDF en tant que format .ppdf

- Afficher le bouton Ne pas transférer dans Outlook

- Stratégie de démonstration

- Justification de la suppression de la protection

- Invite de confirmation **voulez-vous supprimer cette étiquette ?** pour les utilisateurs lorsque vous n’utilisez pas le paramètre de stratégie pour la justification

- Étiqueter un document Office avec une propriété personnalisée existante (paramètres du client avancé SyncPropertyName et SyncPropertyState)

- Applets de commande PowerShell distinctes pour la connexion à un service Rights Management


#### <a name="parent-labels-and-their-sublabels"></a>Étiquettes parentes et sous-étiquettes associées 

Le client Azure Information Protection ne prend pas en charge les configurations qui spécifient une étiquette parente dotée de sous-étiquettes. Ces configurations incluent la spécification d’une étiquette par défaut et d’une étiquette pour la classification automatique ou recommandée. Si une étiquette dispose de sous-étiquettes, vous pouvez spécifier l’une d’elles, mais pas l’étiquette parente.

Pour des raisons de parité, le client d’étiquetage unifié Azure Information Protection ne prend pas non plus en charge l’application d’étiquettes parentes comportant des sous-étiquettes, même si elles peuvent être sélectionnées dans les centres d’administration. Dans ce scénario, le client d’étiquetage unifié Azure Information Protection n’applique pas l’étiquette parente.

## <a name="see-also"></a>Voir aussi
Consultez la documentation suivante pour en savoir plus sur le déploiement et l’utilisation de ces clients :

- [Client Azure Information Protection](AIP-client.md)

- [Client d’étiquetage unifié Azure Information Protection](unifiedlabelingclient-version-release-history.md)

- [Notes sur le déploiement du client RMS](client-deployment-notes.md)

Bien que le client Azure Information Protection puisse être utilisé avec les services AD RMS, le client Azure Information Protection est mieux adapté pour fonctionner avec ses services Azure : Azure Information Protection et son service de protection des données, Azure Rights Management. Pour comparer les services d’Azure Information Protection, voir [Comparaison d’Azure Information Protection avec AD RMS](../compare-on-premise.md).
