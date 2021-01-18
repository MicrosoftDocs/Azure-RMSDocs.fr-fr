---
title: Client pour Azure Information Protection-AIP
description: Microsoft Azure Information Protection fournit une solution client-serveur qui permet de protéger les données d’une organisation. Le client (le client Azure Information Protection ou le client Rights Management) est intégré aux applications que vous exécutez sur des ordinateurs et appareils mobiles.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 0019699301b68df2d6ee4fd05d29a0e64734fc6e
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98559861"
---
# <a name="the-client-side-of-azure-information-protection"></a>Côté client d’Azure Information Protection

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection),[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, Windows server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.


Le client d’étiquetage unifié Azure Information Protection fournit une solution client-serveur qui permet de protéger les documents et les e-mails d’une organisation, et constitue une alternative à la [solution d’étiquetage intégrée pour Microsoft Office](/microsoft-365/compliance/sensitivity-labels). 

Outre l’intégration directe avec les applications Office, le client d’étiquetage unifié prend en charge l’Explorateur de fichiers et PowerShell, afin que vous puissiez classer et protéger des fichiers en dehors d’Office. Les composants supplémentaires incluent une visionneuse pour les images et les fichiers PDF protégés, ainsi qu’un scanneur pour les magasins de données locaux.

Le client d’étiquetage unifié doit être installé séparément pour les applications Office.

Le service réside dans le Cloud ou localement :

- Le service Cloud est **Azure information protection** et utilise le service Azure Rights Management pour la protection des données
- Le service local est **services AD RMS (Active Directory Rights Management Services)** (AD RMS)

## <a name="choose-your-windows-labeling-solution"></a>Choisir une solution d’étiquetage Windows

Les étiquettes facilitent l’application de la protection pour vos utilisateurs, et fournissent également une classification pour vous permettre de suivre et de gérer vos données. 

Lors du choix d’une solution d’étiquetage Windows, tenez compte des différences de base suivantes :

- **Emplacement de téléchargement des étiquettes et des stratégies d’étiquette** 

    La solution d’étiquetage intégrée et le client d’étiquetage unifié AIP utilisent l’un des centres d’administration suivants : 
    
    - Centre de sécurité et conformité Office 365 
    - Centre de sécurité Microsoft 365 
    - Centre de conformité Microsoft 365
      
    Si vous utilisez le client classique AIP hérité, vos étiquettes et vos stratégies d’étiquette sont téléchargées et gérées dans le Portail Azure. 

- **Configuration requise**

    La solution d’étiquetage intégrée ne nécessite pas d’installation distincte.

    Le client d’étiquetage unifié AIP et le client classique hérité requièrent tous deux une installation distincte pour Office. Téléchargez et installez le client d’étiquetage unifié à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=53018).  

    Si vous avez besoin de télécharger et d’installer le client classique traditionnel, contactez le support technique et ouvrez un ticket pour accéder au fichier d’installation. 

Utilisez les sections suivantes pour vous aider à déterminer quel client est le mieux adapté à votre organisation :

- [Solution d’étiquetage Office intégrée](#built-in-office-labeling-solution)
- [Client d’étiquetage unifié Azure Information Protection](#azure-information-protection-unified-labeling-client)
- [Client classique Azure Information Protection](#azure-information-protection-classic-client)
- [Utilisation de plusieurs clients dans le même environnement](#using-multiple-clients-in-the-same-environment)

Pour plus d’informations, consultez : [comparaisons détaillées pour les clients](#detailed-comparisons-for-the-azure-information-protection-clients) et les [fonctionnalités AIP non planifiés pour le client d’étiquetage unifié](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client).

> [!NOTE]
> La dernière version du client d’étiquetage unifié l’amène à fermer la parité dans les fonctionnalités avec le client classique. À mesure que cet intervalle se ferme, vous pouvez vous attendre à ce que les nouvelles fonctionnalités soient ajoutées uniquement au client d’étiquetage unifié. 
>
> Nous vous recommandons de déployer le client d’étiquetage unifié si son ensemble de fonctionnalités et ses fonctionnalités actuelles répondent aux besoins de votre entreprise.
> 

### <a name="built-in-office-labeling-solution"></a>Solution d’étiquetage Office intégrée

La solution d’étiquetage intégrée à Microsoft Office :

- Nécessite un ordinateur Windows avec Microsoft 365 applications, version minimale 1910
- Vous permet de partager des étiquettes et des paramètres de stratégie qui peuvent également être utilisés par macOS, iOS et Android
- Prend en charge le basculement de comptes
- Offre de meilleures performances dans les applications Office
- Ne nécessite pas d’installation et de maintenance distinctes
- Ne peut être désactivée.

**N’utilisez pas** le client d’étiquetage Office intégré Si vous avez besoin de fonctionnalités fournies uniquement les clients Azure information protection, tels que la barre de information protection sous le ruban. Cette barre facilite la sélection et la visibilité des étiquettes.

### <a name="azure-information-protection-unified-labeling-client"></a>Client d’étiquetage unifié Azure Information Protection

Le client d’étiquetage unifié requiert un ordinateur Windows et vous permet de partager des étiquettes et des paramètres de stratégie qui peuvent également être utilisés par macOS, iOS et Android.

**N’utilisez pas** le client d’étiquetage unifié si vous avez configuré des étiquettes dans le portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](../configure-policy-migrate-labels.md).

### <a name="azure-information-protection-classic-client"></a>Client classique Azure Information Protection

Le client classique est le client hérité de AIP, prend en charge des fonctionnalités similaires à celles du client d’étiquetage unifié et doit également être installé séparément pour les applications Office. 

Le client classique est [déconseillé en mars 2021](https://aka.ms/aipclassicsunset).

Utilisez le client classique uniquement si vous n’avez pas encore migré vers un étiquetage unifié. Pour plus d’informations, consultez [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](../tutorial-migrating-to-ul.md).

Le client classique a des paramètres de stratégie différents pour macOS, iOS et Android. Ainsi, bien que vous souhaitiez utiliser les fonctionnalités supplémentaires, vous devez utiliser un portail de gestion et une expérience utilisateur distincts pour protéger le contenu sur les systèmes d’exploitation.

Dans la mesure du possible, nous vous recommandons d’utiliser le client d’étiquetage unifié au lieu du client classique.

### <a name="using-multiple-clients-in-the-same-environment"></a>Utilisation de plusieurs clients dans le même environnement

Vous pouvez utiliser différents clients dans le même environnement pour prendre en charge différents besoins de l’entreprise, comme illustré dans l’exemple de déploiement suivant. Dans un environnement client mixte, nous vous recommandons d’utiliser des étiquettes unifiées afin que les clients partagent le même ensemble d’étiquettes pour faciliter l’administration. Par défaut, les nouveaux clients ont des étiquettes unifiées, car leurs locataires se trouvent sur la plateforme d’étiquetage unifiée. Pour plus d’informations, consultez [Comment puis-je déterminer si mon locataire se trouve sur la plateforme d’étiquetage unifiée ?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Si vous disposez d’un ordinateur Windows qui exécute Microsoft 365 applications qui sont au minimum la version 1910 et l’un des clients Azure Information Protection est installé, par défaut la solution d’étiquetage intégrée est désactivée dans les applications Office. Toutefois, vous pouvez modifier ce comportement pour utiliser la solution d’étiquetage intégrée uniquement pour vos applications Office. Avec cette configuration, le client Azure Information Protection reste disponible pour l’étiquetage dans l’Explorateur de fichiers, PowerShell et le scanneur. Pour obtenir des instructions sur la désactivation du client Azure Information Protection dans Microsoft 365 Apps, consultez la section [solution d’étiquetage Office intégrée et le client Azure information protection](/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) dans la documentation relative à la conformité de Microsoft 365.

##### <a name="sample-deployment-strategy"></a>Exemple de stratégie de déploiement

- Pour la majorité des utilisateurs, vous déployez le client d’étiquetage unifié Azure Information Protection, car ce client répond aux besoins de l’entreprise pour ces utilisateurs. 
    
    Pour ces utilisateurs, leur étiquetage est similaire sur Windows, Mac, iOS et Android, car ils ont les mêmes étiquettes publiées et les mêmes paramètres de stratégie. En tant qu’administrateur, vous gérez ces étiquettes et paramètres de stratégie dans le même centre de gestion.

- Vous installez également le client d’étiquetage unifié pour vous-même, afin de tester le scanneur Azure Information Protection.

- Pour un sous-ensemble d’utilisateurs, vous déployez le client classique, car ces utilisateurs nécessitent des étiquettes qui appliquent la protection de votre propre clé ([hyok](../configure-adrms-restrictions.md)).
    
    Pour ces utilisateurs, ils ont une expérience d’étiquetage légèrement différente lorsqu’ils utilisent ce client. Par exemple, ils voient un bouton **protéger** au lieu d’un bouton de **sensibilité** dans les applications Office. En tant qu’administrateur, vous devez gérer les étiquettes des paramètres HYOK et des paramètres de stratégie dans un autre centre de gestion pour les étiquettes et les paramètres des autres plateformes clientes.

- Vous avez des magasins de données locaux avec des documents qui doivent être analysés à la recherche d’informations sensibles ou classifiées et protégées. Pour une utilisation en production, vous déployez le client d’étiquetage unifié sur les serveurs pour exécuter le [scanneur de Azure information protection](../deploy-aip-scanner.md).

#### <a name="rights-management-client"></a>Client Rights Management

Le client RMS fournit uniquement une protection et est automatiquement installé avec certaines applications, notamment les applications Office, l’étiquetage unifié AIP et les clients classiques, ainsi que les applications compatibles RMS d’autres éditeurs de logiciels. 

Vous pouvez également [installer le client RMS vous-même](https://www.microsoft.com/download/details.aspx?id=38396), pour prendre en charge la [synchronisation des fichiers à partir des bibliothèques protégées par IRM et de OneDrive](/onedrive/deploy-on-windows), et pour les développeurs qui souhaitent intégrer la protection Rights Management à des applications métier.

## <a name="compare-the-labeling-solutions-for-windows-computers"></a>Comparer les solutions d’étiquetage pour les ordinateurs Windows

Utilisez le tableau suivant pour comparer les fonctionnalités prises en charge par les trois solutions d’étiquetage pour les ordinateurs Windows.

Pour comparer les fonctionnalités d’étiquetage de sensibilité intégrées à Office sur différentes plateformes de système d’exploitation (Windows, macOS, iOS et Android) et pour le Web, consultez la documentation de conformité Microsoft 365, [prise en charge des fonctionnalités d’étiquette de sensibilité dans les applications](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). Cette documentation comprend également les numéros de version Office ou les informations de canal Office Update pour les fonctionnalités prises en charge.

Pour plus d’informations, consultez également :
- [Comparaisons détaillées pour les clients Azure Information Protection](#detailed-comparisons-for-the-azure-information-protection-clients)
- [Fonctionnalités non planifiées dans le client d’étiquetage unifié Azure Information Protection](#features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client)

|Fonctionnalité|Client classique|Client d’étiquetage unifié|Solution d’étiquetage Office intégrée|
|:------|:------------:|:---------------------:|:-----------------------------:|
|**Étiquetage manuel**| ![Oui](../media/yes-icon.png)   | ![Oui](../media/yes-icon.png)   |![Oui](../media/yes-icon.png) |
|**Étiquette par défaut**| ![Oui](../media/yes-icon.png)| ![Oui](../media/yes-icon.png)| ![Oui](../media/yes-icon.png)|
|**Étiquetage automatique ou recommandé** <br />Pour Word, Excel, PowerPoint, Outlook|![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |
|**Étiquetage obligatoire**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
|**Autorisations définies par l’utilisateur pour une étiquette**: <br />Ne pas transférer pour les e-mails| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |
|**Autorisations définies par l’utilisateur pour une étiquette**: <br />Autorisations personnalisées pour Word, Excel, PowerPoint| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |
|**Prise en charge multilingue pour les étiquettes**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |![Oui](../media/yes-icon.png) |
|**Héritage des étiquettes dans les pièces jointes**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png)  | ![non](../media/no-icon.png)|
|Les **personnalisations qui incluent**:<br />- Étiquette par défaut pour e-mail<br />-Afficher les messages dans Outlook <br />- Prise en charge de S/MIME<br />- Option Signaler un problème| ![oui ](../media/yes-icon.png) <sup>1</sup> | ![oui ](../media/yes-icon.png) <sup>2</sup> |  ![non](../media/no-icon.png)|
|**Scanneur pour les magasins de données locaux**| ![Oui](../media/yes-icon.png) |  ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
|**Rapports centraux (analytique)**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
|**Autorisations personnalisées définies indépendamment d’une étiquette**| ![Oui](../media/yes-icon.png) | ![oui ](../media/yes-icon.png) <sup>3</sup>|  ![non](../media/no-icon.png)|
|**Barre de Information Protection dans les applications Office**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png)|  ![non](../media/no-icon.png)|
|**Marquages visuels comme une action d’étiquette**<br> (en-tête, pied de page, filigrane)| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png)|
|**Marquages visuels par application**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![oui ](../media/yes-icon.png) <sup>9</sup>|
|**Marquages visuels dynamiques avec des variables**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![oui ](../media/yes-icon.png) <sup>9</sup>|
|**Supprimer le marquage de contenu externe dans l’application**| ![Oui](../media/yes-icon.png)| ![Oui](../media/yes-icon.png)| ![non](../media/no-icon.png)|
|**Étiquette avec l’Explorateur de fichiers**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
|**Visionneuse pour les fichiers protégés** <br> (texte, images, PDF,. pfile)| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![non](../media/no-icon.png)|
|**Prise en charge PPDF pour l’application des étiquettes**| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|  ![non](../media/no-icon.png)|
|**Applets de commande d’étiquetage PowerShell**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png)  |  ![non](../media/no-icon.png)|
|**Prise en charge hors connexion des actions de protection**| ![Oui](../media/yes-icon.png) | ![oui ](../media/yes-icon.png) <sup>4</sup> | ![Oui](../media/yes-icon.png) |
|**Gestion manuelle des fichiers de stratégie pour les ordinateurs déconnectés**| ![Oui](../media/yes-icon.png) |![Oui](../media/yes-icon.png)|  ![non](../media/no-icon.png)|
|**Support HYOK**| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|  ![non](../media/no-icon.png)|
|**Journalisation de l’utilisation dans observateur d’événements**| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)| ![non](../media/no-icon.png)|
|**Afficher le bouton Ne pas transférer dans Outlook**| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|  ![non](../media/no-icon.png)|
|**Suivre les documents protégés**| ![oui ](../media/yes-icon.png) <sup>5</sup> | ![oui ](../media/yes-icon.png) <sup>5</sup> |  ![non](../media/no-icon.png)|
|**Révoquer des documents protégés**| ![oui ](../media/yes-icon.png) <sup>5</sup> |  ![oui ](../media/yes-icon.png) <sup>5</sup>|  ![non](../media/no-icon.png)|
|**Mode protection uniquement** (aucune étiquette)| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|  ![non](../media/no-icon.png)|
|**Prise en charge du changement de compte**|  ![non](../media/no-icon.png)|  ![non](../media/no-icon.png)| ![Oui](../media/yes-icon.png) |
|**Prise en charge de Services Bureau à distance**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |
|**Prise en charge de AD RMS**| ![Oui](../media/yes-icon.png) |  ![non ](../media/no-icon.png) <sup>6</sup> |  ![non](../media/no-icon.png)|
|**Prise en charge des formats Microsoft Office 97-2003**| ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |  ![non ](../media/no-icon.png) <sup>8</sup>|
|**Chiffrement à clé double**|  ![non](../media/no-icon.png)| ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
|**Cloud de la communauté gouvernementale** | ![Oui](../media/yes-icon.png) | ![Oui](../media/yes-icon.png) |  ![non](../media/no-icon.png)|
| | | | |

**Notes de bas de page**:

<sup>1</sup> ces paramètres, et bien plus encore, sont pris en charge en tant que [Paramètres client avancés que vous configurez dans la portail Azure](client-admin-guide-customizations.md#how-to-configure-advanced-classic-client-configuration-settings-in-the-portal).

<sup>2</sup> ces paramètres, et bien plus encore, sont pris en charge en tant que [Paramètres avancés que vous configurez avec PowerShell](clientv2-admin-guide-customizations.md#configuring-advanced-settings-for-the-client-via-powershell).

<sup>3</sup> pris en charge par l’Explorateur de fichiers et PowerShell. Dans les applications Office, les utilisateurs peuvent sélectionner les **informations de fichier**  >  **protéger le document**  >  **restreindre l’accès**.

<sup>4</sup> pour l’Explorateur de fichiers et les commandes PowerShell, l’utilisateur doit être connecté à Internet pour protéger des fichiers.

<sup>5</sup> pour plus d’informations, consultez : **Unified Labeling client**: Guide d’administration (préversion [publique)](track-and-revoke-admin.md)  |   [Guide de l’utilisateur (](revoke-access-user.md)préversion publique). Le suivi est pris en charge uniquement pour les administrateurs généraux. **Client classique**: Guide de l’utilisateur du Guide de l' [administrateur](client-admin-guide-document-tracking.md)  |  [](client-track-revoke.md). Les administrateurs peuvent également utiliser la [création de rapports centralisée](../reports-aip.md) pour déterminer si les documents protégés sont accessibles à partir d’ordinateurs Windows et si l’accès a été accordé ou refusé.

<sup>6</sup> les actions d’étiquetage et de protection ne sont pas prises en charge. Toutefois, pour un déploiement AD RMS, la visionneuse peut ouvrir des documents protégés lorsque vous utilisez l' [extension d’appareil Mobile services AD RMS (Active Directory Rights Management Services)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).

<sup>8</sup> tandis que les clients AIP prennent en charge les formats de fichier Microsoft Office 97-2003, tels que **. doc**, ainsi que les formats XML ouverts Office, tels que **. docx**, l’étiquetage intégré prend uniquement en charge les formats Open XML.

<sup>9</sup> pour plus d’informations sur la prise en charge des marquages de contenu dynamiques et des marquages de contenu par application pour la solution d’étiquetage intégrée, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels-office-apps#dynamic-markings-with-variables).

### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Comparaisons détaillées pour les clients Azure Information Protection

Lorsque le client Azure Information Protection Classic et le Azure Information Protection client d’étiquetage unifié prennent tous deux en charge la même fonctionnalité, utilisez les listes suivantes pour identifier les différences fonctionnelles entre les deux clients :


|Fonctionnalités |Client classique|Client d’étiquetage unifié|
|--------------|-----------------------------------|-----------------------------------------------------------|
|**Paramétrage**| Option d’installation d’une stratégie de démonstration locale | Pas de stratégie de démonstration locale|
|**Marquer la sélection et l’affichage quand elle est appliquée dans les applications Office**|À partir du bouton **Protéger** situé sur le ruban <br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|À partir du bouton **Critère de diffusion** situé sur le ruban<br /><br /> À partir de la barre Information Protection (barre horizontale située sous le ruban)|
|**Gérer la barre de Information Protection dans les applications Office**|**Pour les utilisateurs**:<br />Option permettant d’afficher ou de masquer la barre à partir du bouton **protéger** du ruban<br /><br>Quand un utilisateur choisit de masquer la barre, par défaut, la barre est masquée dans cette application, mais continue à s’afficher automatiquement dans les applications récemment ouvertes <br /><br /> **Pour les administrateurs**: <br />Paramètres de stratégie permettant d’afficher ou de masquer automatiquement la barre quand une application s’ouvre pour la première fois et de contrôler si la barre reste automatiquement masquée pour les nouvelles applications ouvertes après qu’un utilisateur a sélectionné de masquer la barre|**Pour les utilisateurs**: <br />Option permettant d’afficher ou de masquer la barre à partir du bouton **sensibilité** sur le ruban. <br><br />Lorsqu’un utilisateur sélectionne pour masquer la barre, la barre est masquée dans cette application et également dans les applications récemment ouvertes <br /><br />**Pour les administrateurs**: <br />Paramètre PowerShell pour gérer la barre |
|**Couleur de l’étiquette**| Configurer dans le portail Azure | Conservé après la migration des étiquettes et configurable avec [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|**Les étiquettes prennent en charge différentes langues**| Configurer dans le portail Azure | Configurer à l’aide d' [Office 365 Security & Compliance PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)|
|**Mise à jour de stratégie**| -Quand une application Office s’ouvre <br /> -Quand vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br />-Quand vous exécutez les applets de commande PowerShell pour l’étiquetage et la protection<br />-Toutes les 24 heures <br />-Pour le scanneur : toutes les heures et lorsque le service démarre et que la stratégie est antérieure à une heure| -Quand une application Office s’ouvre <br />-Quand vous cliquez avec le bouton droit pour classifier et protéger un fichier ou un dossier <br />-Quand vous exécutez les applets de commande PowerShell pour l’étiquetage et la protection<br />-Toutes les 4 heures <br />-Pour le scanneur : toutes les 4 heures|
|**Formats pris en charge pour PDF**| **Protection**: <br /> - Norme ISO pour le chiffrement PDF (par défaut) <br /> - .ppdf <br /><br> **Consommation**: <br /> - Norme ISO pour le chiffrement PDF <br />- .ppdf<br />- Protection IRM pour SharePoint| **Protection**: <br /> - Norme ISO pour le chiffrement PDF <br /> <br /> **Consommation**: <br /> - Norme ISO pour le chiffrement PDF <br />- .ppdf<br />- Protection IRM pour SharePoint|
|**Fichiers protégés de façon générique (. pfile) ouverts avec la visionneuse**| Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché, modifié et enregistré sans protection | Le fichier s’ouvre dans l’application d’origine, où il peut ensuite être affiché et modifié, mais pas enregistré|
|**Applets de commande prises en charge**| -Applets de commande pour l’étiquetage <br> -Applets de commande pour la protection uniquement | **Applets de commande pour l’étiquetage**:<br /> [Set-AIPFileClassification](/powershell/module/azureinformationprotection/get-aipfileclassification) et [Set-AIPFileLabel](/powershell/module/azureinformationprotection/get-aipfilelabel) ne prennent pas en charge le paramètre **owner** <br /> En outre, le commentaire unique « Aucune étiquette à appliquer » existe pour tous les scénarios dans lesquels aucune étiquette n’est appliquée. <br /><br /> [Set-AIPFileClassification](/powershell/module/azureinformationprotection/get-aipfileclassification) prend en charge le paramètre **WhatIf** , afin qu’il puisse être exécuté en mode détection <br /><br /> [Set-AIPFileLabel](/powershell/module/azureinformationprotection/get-aipfilelabel) ne prend pas en charge le paramètre *EnableTracking* <br /><br /> L’AIPFileStatus de la [récupération](/powershell/module/azureinformationprotection/get-aipfilestatus) ne retourne pas d’informations sur les étiquettes d’autres locataires et n’affiche pas le paramètre **RMSIssuedTime**<br />En outre, le **paramètre LabelingMethod** pour la [fonction AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) affiche **Privileged** ou **standard**, et non **Manuel** ou **automatique**.|
|**Les invites de justification (si elles sont configurées) par action dans Office** | -Frequency : par fichier <br /> -Diminuer le niveau de sensibilité <br /> -Suppression d’une étiquette<br /> -Suppression de la protection | -Frequency : par session <br /> -Diminuer le niveau de sensibilité<br />-Suppression d’une étiquette|
|**Supprimer les actions relatives aux étiquettes appliquées** | L’utilisateur doit confirmer la suppression. <br /><br />L’étiquette par défaut ou une étiquette automatique (si elle est configurée) n’est pas automatiquement appliquée la prochaine fois que l’application Office ouvre le fichier  | L’utilisateur n’est pas invité à confirmer<br /><br /> L’étiquette par défaut ou une étiquette automatique (si elle est configurée) est automatiquement appliquée la prochaine fois que l’application Office ouvre le fichier|
|**Étiquettes automatiques et recommandées** | Configurée en tant que [conditions d’étiquette](../configure-policy-classification.md) dans le portail Azure avec des types d’informations intégrées et des conditions personnalisées utilisant des expressions régulières ou non <br /><br />Les options de configuration comprennent ce qui suit : <br />- Nombre de valeurs uniques/non uniques <br /> - Nombre minimal| Configurée dans les centres d’administration avec les types d’informations sensibles intégrés et des [types d’informations personnalisés](/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Les options de configuration comprennent ce qui suit :  <br />- Nombre de valeurs uniques seulement <br />- Nombre de valeurs minimales et maximales <br />- Prise en charge des clauses AND et OR avec les types d’informations <br />- Dictionnaire de mots clés<br />- Niveau de confiance et proximité des caractères personnalisables|
|**Prise en charge des commandes pour les sous-étiquettes sur les pièces jointes** | Activé avec un [paramètre client avancé](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) | Activé par défaut, aucune configuration n’est requise|
|**Modifier le comportement de protection par défaut pour les types de fichiers**| Utilisez les [modifications du Registre](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) pour remplacer les valeurs par défaut de protection native et générique | Utiliser [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) pour modifier les types de fichiers qui sont protégés|
|**Analyses automatiques** | Les analyses complètes sont exécutées automatiquement chaque fois que l’analyseur détecte une modification de la stratégie ou des paramètres d’étiquetage | À partir de la version [2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850), les administrateurs peuvent choisir d’ignorer une nouvelle analyse complète après avoir apporté des modifications aux paramètres de la stratégie ou du travail d’analyse du contenu. |
|**Détection de réseau** |Les fonctionnalités de découverte du réseau ne sont pas disponibles pour le scanneur classique | Les administrateurs peuvent découvrir des référentiels à risque supplémentaires en analysant une adresse IP ou une plage spécifiée.|
| | | |

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Fonctionnalités non planifiées dans le client d’étiquetage unifié Azure Information Protection

Bien que le client d’étiquetage unifié Azure Information Protection soit toujours en cours de développement, les fonctionnalités et les différences de comportement suivantes du client classique ne sont pas prévues pour le moment dans les futures versions du client d’étiquetage unifié : 

- Autorisations personnalisées en tant qu' [option distincte que les utilisateurs peuvent sélectionner dans les applications Office : Word, Excel et PowerPoint](client-classify-protect.md#set-custom-permissions-for-a-document)

- La barre d’outils sensibilité n’affiche pas le titre de **sensibilité** , ni une info-bulle de titre. La barre elle-même est affichée dans le client d’étiquetage unifié.

- [Mode protection uniquement](client-protection-only-mode.md) (aucune étiquette) à l’aide de modèles

- Protéger le document PDF en tant que [. ppdf (ancien format)](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- Afficher le bouton **ne pas transférer** dans Outlook

- Stratégie de démonstration

- Applets de commande PowerShell distinctes pour la connexion à un service Rights Management

- Affichage de l’identité de l’utilisateur qui a appliqué une étiquette


### <a name="parent-labels-and-their-sublabels"></a>Étiquettes parentes et sous-étiquettes associées 

Le client Azure Information Protection Classic ne prend pas en charge les configurations qui spécifient une étiquette parente avec des sous-étiquettes. Ces configurations incluent la spécification d’une étiquette par défaut et d’une étiquette pour la classification automatique ou recommandée. Si une étiquette dispose de sous-étiquettes, vous pouvez spécifier l’une d’elles, mais pas l’étiquette parente.

Pour des raisons de parité, le client d’étiquetage unifié Azure Information Protection ne prend pas non plus en charge l’application d’étiquettes parentes comportant des sous-étiquettes, même si elles peuvent être sélectionnées dans les centres d’administration. Dans ce scénario, le client d’étiquetage unifié Azure Information Protection n’applique pas l’étiquette parente.

## <a name="next-steps"></a>Étapes suivantes

Pour installer et configurer le client d’étiquetage unifié Azure Information Protection, consultez :

- [Guide de l’administrateur du client d’étiquetage unifié Azure Information Protection](clientv2-admin-guide.md)
- [Guide de l’utilisateur d’étiquetage unifié Azure Information Protection](clientv2-user-guide.md)

Pour plus d’informations sur l’utilisation de la solution d’étiquetage intégrée pour les applications Microsoft 365, consultez [étiquettes de sensibilité dans les applications Office](/microsoft-365/compliance/sensitivity-labels-office-apps).
