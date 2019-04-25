---
title: Le client pour Azure Information Protection - AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: ed762332e023843326fc4ec4d89e8fc44ede39be
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180814"
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

- Installation Azure Information Protection unifiée étiquetage client pour les étiquettes qui peut également être utilisé par Mac OS, iOS et Android, et si vous n’avez pas besoin des fonctionnalités avancées, telles que les paramètres du client avancé, les autorisations définies par l’utilisateur, un local clé (HYOK), ou scanneur pour les magasins de données sur site

- Installer le client Azure Information Protection si vous avez besoin des fonctionnalités avancées qui ne sont pas encore disponibles dans le client d’étiquetage unifié, mais les étiquettes ne peut pas être utilisés sur d’autres plateformes client.

Actuellement, le client Azure Information Protection et le client d’étiquetage unifié Azure Information Protection ne pas de parité de leurs fonctionnalités. Nous prévoyons toutefois de supprimer cette différence, puis d’ajouter des fonctionnalités au seul client d’étiquetage unifié Azure Information Protection. Pour cette raison, nous vous recommandons de que déployer le client d’étiquetage unifié Azure Information Protection si sa fonctionnalité et un ensemble de fonctionnalités actuel répond aux besoins de votre entreprise. Dans le cas contraire ou si vous avez configuré des étiquettes dans le portail Azure que vous n’avez pas encore [migrées vers le magasin d’étiquetage unifié](../configure-policy-migrate-labels.md), utilisez le client Azure Information Protection.

Vous pouvez également installer les deux clients dans le même environnement pour prendre en charge des besoins métier différents, comme illustré dans l’exemple suivant. Pour ce scénario, nous vous recommandons de que migrer les étiquettes dans le portail Azure afin que les deux ensembles de clients partagent le même jeu d’étiquettes pour faciliter l’administration.

##### <a name="example-deployment-strategy"></a>Stratégie de déploiement d’exemple :

- Pour la majorité des utilisateurs, vous déployez le client d’étiquetage unifié Azure Information Protection, car la plupart des utilisateurs n’avez pas besoin fonctions ou fonctionnalités qui sont disponibles uniquement avec le client d’étiquetage unifié Azure Information Protection. 
    
    Pour ces utilisateurs, leur expérience étiquetage est très similaire s’ils ont également des appareils qui exécutent Mac OS, iOS et Android, et ces appareils ont une version d’Office qui prend en charge des étiquettes de sensibilité.

- Pour un sous-ensemble d’utilisateurs, vous déployez le client Azure Information Protection, car ces utilisateurs ont besoin d’étiquettes qui appliquent la maintenez votre propre protection de clés (HYOK) ou d’une invite autorisations définies par l’utilisateur.
    
    Pour ces utilisateurs, ils ont des fonctionnalités complémentaires, mais une expérience légèrement différente si elles ont également les appareils qui exécutent Mac OS, iOS et Android et que ces appareils ont une version d’Office qui prend en charge des étiquettes de sensibilité. Par exemple, ils voient un **protéger** bouton au lieu d’un **sensibilité** bouton sur le ruban d’Office et la barre Information Protection peut être affiché par défaut.

- Vous avez des banques de données sur site avec des documents qui doivent être analysés pour des informations sensibles ou classifiés et protégés. Vous déployez le client Azure Information Protection sur les serveurs pour exécuter le scanneur Azure Information Protection.

### <a name="compare-the-clients"></a>Comparer les clients

Utilisez le tableau suivant pour aider à comparer les fonctionnalités qui sont prises en charge par les deux clients Azure Information Protection.

|Composant|Client Azure Information Protection|Azure Information Protection<br /> Client d’étiquetage unifié Azure Information Protection|
|-------|-----------------------------------|----------------------------------------------------|
|Étiquetage des actions : manuel, recommandé, automatique| Oui | Oui |
|Création centralisée de rapports (analytique) :| Oui | Oui |
|Paramètres de réinitialisation et journaux d’exportation :| Oui | Oui |
|Autorisations définies par l’utilisateur :| Oui | Pour Outlook uniquement (Ne pas transférer) |
|Autorisations personnalisées :| Oui | Explorateur de fichiers uniquement <br /><br /> Dans les applications Office, les utilisateurs peuvent également sélectionner **Informations sur le fichier** > **Protéger le document** > **Restreindre l’accès**. |
|Barre Information Protection dans les applications Office :| Oui | Oui, avec des restrictions :<br /><br /> - Pas de titre ou d’info-bulle personnalisable<br /><br /> - Couleur d’étiquette non affichée pour l’étiquette appliquée|
|Les étiquettes peuvent appliquer des marquages visuels (en-tête, pied de page, filigrane) :| Oui | Oui, avec des restrictions :<br /><br /> - Les en-têtes et les pieds de page ne gèrent pas les variables pour les valeurs dynamiques <br /><br /> - Pas de prise en charge pour Word, Excel, PowerPoint et Outlook de différents marquages visuels|
|Dans l’Explorateur de fichiers, actions déclenchées par clic droit :| Oui | Oui, avec des restrictions :<br /><br /> - Impossible de protéger les documents PDF au format .ppdf <br /><br />  - Pas de prise en charge du mode Protection uniquement|
|Visionneuse des fichiers protégés :| Oui | Oui, avec des restrictions :<br /><br /> - Pour les fichiers protégés de manière générique (.pfile), contrairement à la visionneuse du client Azure Information Protection, il n’existe aucune possibilité d’enregistrer des modifications dans le fichier ouvert à l’origine.|
|Commandes PowerShell :| Oui | Oui, avec des restrictions :<br /><br />- Cmdlets incluses : [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus), [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- Les cmdlets qui se connectent directement à un service de protection ne sont pas incluses.|
|Prise en charge hors connexion des actions de protection :| Oui | Oui, avec des restrictions : <br /><br />- Pour l’Explorateur de fichiers et les commandes PowerShell, l’utilisateur doit être connecté à Internet pour protéger les fichiers. |
|Prise en charge des ordinateurs déconnectés avec gestion de fichier de stratégie manuelle :| Oui |Non |
|Prise en charge de HYOK :| Oui | Non<br /><br /> Les étiquettes que vous migrez à partir du portail Azure et qui sont configurées pour la protection HYOK sont affichées par le client d’étiquetage unifié Azure Information Protection, mais n’appliquent pas de protection. |
|Journalisation de l’utilisation dans l’observateur d’événements :| Oui | Non|
|Héritage d’étiquette à partir des pièces jointes aux e-mails :| Oui | Non |
|Afficher le bouton Ne pas transférer dans Outlook| Oui | Non |
|Les [personnalisations](client-admin-guide-customizations.md#available-advanced-client-settings) sont les suivantes :<br />- Étiquette par défaut pour e-mail<br />- Activer les autorisations personnalisées <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| Oui | Non |
|Scanneur pour magasins de données locaux :| Oui | Non |
|Suivre et révoquer :| Oui | Non |
|Mode Protection uniquement (pas d’étiquettes) :| Oui | Non |
|Prise en charge multilingue :| Oui | Non |
|Prise en charge des services AD RMS :| Oui | Seule l’action suivante est prise en charge :<br /><br /> - La visionneuse peut ouvrir des documents protégés quand vous déployez l’[extension Appareils mobiles AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="detailed-comparisons-for-the-clients"></a>Comparaisons détaillées pour les clients

Lorsque les deux clients prennent en charge la même fonctionnalité, utilisez le tableau suivant pour faciliter l’identification des différences fonctionnelles entre les deux clients.

|Fonctionnalité |Client Azure Information Protection|Azure Information Protection<br /> Client d’étiquetage unifié Azure Information Protection|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurer :| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|Sélection et affichage d’étiquette en cas d’application dans les applications Office :|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|Gérer la barre Information Protection dans les applications Office :|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Protéger** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, par défaut, elle est masquée dans cette application, mais continue de s’afficher automatiquement dans les applications récemment ouvertes. <br /><br /> Pour les administrateurs : <br /><br />- Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre à la première ouverture d’une application, et de contrôler si la barre reste automatiquement masquée pour les applications récemment ouvertes une fois qu’un utilisateur a choisi de masquer la barre|Pour les utilisateurs : <br /><br />- Option permettant d’afficher ou de masquer la barre à partir du bouton **Critère de diffusion** situé sur le ruban<br /><br />- Lorsqu’un utilisateur choisit de masquer la barre, celle-ci est masquée dans cette application et dans les applications récemment ouvertes <br /><br />Pour les administrateurs : <br /><br />- Pas de paramètre de stratégie pour gérer la barre|
|Couleur d’étiquette : | À configurer dans le portail Azure | Conservée après la migration d’étiquette vers Office 365 <br /><br /> Les nouvelles étiquettes créées dans les centres d’administration n’ont pas de couleur|
|Mise à jour de la stratégie : | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 24 heures | Quand une application Office s’ouvre <br /><br /> Lorsque vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br /><br />Lorsque vous exécutez les cmdlets PowerShell pour l’étiquetage et la protection<br /><br />Toutes les 4 heures|
|Formats pris en charge pour PDF :| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /><br /> - .ppdf <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint| Protection : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br /> <br /><br /> Consommation : <br /><br /> - Norme ISO pour le chiffrement PDF <br /><br />- .ppdf<br /><br />- Protection IRM pour SharePoint|
|Cmdlets prises en charge :| Ensemble des cmdlets documentées pour [AzureInformationProtection](/powershell/module/azureinformationprotection) | Set-AIPAuthentication ne prend pas en charge les sessions non interactives <br /><br /> Les cmdlets Set-AIPFileClassification et Set-AIPFileLabel ne prennent pas en charge le paramètre *Propriétaire* ni les bibliothèques SharePoint Server. <br /><br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> La cmdlet Set-AIPFileLabel ne prend pas en charge le paramètre *EnableTracking*. <br /><br /> La cmdlet Get-AIPFileStatus ne retourne aucune information d’étiquette à partir d’autres abonnés et n’affiche pas le paramètre *RMSIssuedTime*.<br /><br />En outre, le paramètre *LabelingMethod* de la cmdlet Get-AIPFileStatus affiche les valeurs **Privilégié**, **Standard** or **Automatique** et non **Manuel** ou **Automatique**. Pour plus d’informations, consultez la [documentation en ligne](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Invites de justification (si configurées) par action dans Office : | Fréquence : par fichier <br /><br /> Diminution du niveau de confidentialité <br /><br /> Suppression d’une étiquette<br /><br /> Suppression de la protection | Fréquence : par session <br /><br /> Diminution du niveau de confidentialité<br /><br /> Suppression d’une étiquette|
|Supprimer les actions de l’étiquette appliquée : | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou l’étiquette automatique (si configurée) n’est pas appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.  <br /><br />| L’utilisateur n’a pas à confirmer la suppression.<br /><br /> L’étiquette par défaut ou l’étiquette automatique (si configurée) est appliquée automatiquement la prochaine fois que l’application Office ouvre le fichier.|
|Classification automatique et recommandée : | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br /><br />- Nombre de valeurs uniques/non uniques <br /><br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br /><br />- Nombre de valeurs uniques seulement <br /><br />- Nombre de valeurs minimales et maximales <br /><br />- Prise en charge des clauses AND et OR avec les types d’informations <br /><br />- Dictionnaire de mots clés<br /><br />- Niveau de confiance et proximité des caractères personnalisables|

Pour une comparaison détaillée des différences de comportement pour les paramètres de protection spécifique, consultez [comparant le comportement des paramètres de protection pour une étiquette](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Fonctionnalité n’est ne pas planifiée pour être dans le client d’étiquetage unifié Azure Information Protection

Bien que le client d’étiquetage unifié Azure Information Protection est en cours de développement, les fonctionnalités suivantes et les différences de comportement à partir du client Azure Information Protection ne sont pas actuellement planifiées pour être disponible dans les versions futures pour Azure Client Information Protection unifiée étiquetage : 

- Autorisations personnalisées dans les applications Office : Word, Excel et PowerPoint

- Suivre et révoquer depuis des applications Office et l’Explorateur de fichiers

- Barre de titre et info-bulle Azure Information Protection

- Mode Protection uniquement (pas d’étiquettes)

- Protéger le document PDF en tant que format .ppdf

- Afficher le bouton Ne pas transférer dans Outlook

- Stratégie de démonstration

- Justification de la suppression de la protection

- Invite de confirmation avant la suppression d’une étiquette appliquée

- Lien Signaler un problème dans la boîte de dialogue Aide et commentaires

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
