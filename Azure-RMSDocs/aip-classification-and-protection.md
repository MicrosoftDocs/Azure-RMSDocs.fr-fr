---
title: Azure Information Protection (AIP) étiquetage, classification et protection
description: Découvrez comment Azure Information Protection (AIP) peut étiqueter des documents et des e-mails pour classer et protéger vos données.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 3465bdb2eaf1efce3524d2f28332b094ba31db5d
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240850"
---
# <a name="azure-information-protection-aip-labeling-classification-and-protection"></a>Azure Information Protection (AIP) étiquetage, classification et protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne :** [Azure information protection client d’étiquetage unifié et client Classic pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Azure Information Protection (AIP) est une solution basée sur le cloud qui permet à une organisation de classifier et de protéger ses documents et ses e-mails en les étiquetant. 

Par exemple, votre administrateur peut configurer une étiquette avec des règles qui détectent des données sensibles, telles que les informations d’une carte de crédit. Dans ce cas, quand un utilisateur enregistre les informations d’une carte de crédit dans un fichier Word, une info-bulle recommandant d’appliquer l’étiquette correspondant à ce scénario est susceptible d’apparaître en haut du document.

Les étiquettes servent à [classer](#how-labels-apply-classification-with-aip) et, éventuellement, à [protéger](#how-aip-protects-your-data) les documents, ce qui permet d’effectuer différentes actions :

- **Suivre et contrôler** la manière dont le contenu est utilisé
- **Analyser les flux de données** pour mieux comprendre l’entreprise
**Détecter les comportements risqués** et prendre des mesures correctives
- **Effectuer un suivi de l’accès aux documents** et empêcher la fuite et l’usage abusif des données
- Etc.

## <a name="how-labels-apply-classification-with-aip"></a>Mode d’application de la classification des étiquettes avec AIP

L’étiquetage de votre contenu avec AIP comprend les éléments suivants :

- Une **classification**, qui peut être détectée indépendamment de l’endroit où les données sont stockées ou des personnes avec qui elles sont partagées.
- **Marquages visuels**, tels que les en-têtes, les pieds de page ou les filigranes.
- Les **métadonnées**, ajoutées aux fichiers et aux en-têtes de courrier électronique en texte clair. Les métadonnées en texte clair permettent à d’autres services d’identifier la classification et de prendre des mesures appropriées.

Par exemple, dans l’image ci-dessous, l’étiquetage a classé un message électronique comme *général*:

:::image type="content" source="media/example-email-footerv2.png" alt-text="Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection":::

Dans cet exemple, l’étiquette a également :

- **Ajout d’un pied de page de *sensibilité : général* au message électronique**. Ce pied de page est un indicateur visuel pour tous les destinataires auxquels il est destiné spécifiant qu’il s’agit de données métier d’ordre général qui ne doivent pas être envoyées à l’extérieur de l’organisation.
- **Métadonnées incorporées dans les en-têtes de message électronique**. Les données d’en-tête permettent aux services de messagerie d’inspecter l’étiquette et de créer théoriquement une entrée d’audit ou d’empêcher son envoi en dehors de l’organisation.

Les étiquettes peuvent être appliquées automatiquement par les administrateurs à l’aide de règles et de conditions, manuellement par les utilisateurs, ou à l’aide d’une combinaison dans laquelle les administrateurs définissent les recommandations présentées aux utilisateurs.

## <a name="how-aip-protects-your-data"></a>Protection des données avec AIP

Azure Information Protection utilise le [*service Azure Rights Management* (Azure RMS)](what-is-azure-rms.md) pour protéger les données. 

Azure RMS est intégré à d’autres services et applications cloud Microsoft, comme Office 365 et Azure Active Directory. Il peut également être utilisé avec vos propres applications et solutions de protection des informations ou celles de tiers. Azure RMS fonctionne avec les solutions locales et cloud.

Azure RMS utilise des stratégies de chiffrement, d’identité et d’autorisation. À l’image des étiquettes AIP, la protection avec Azure RMS reste associée aux documents et aux e-mails, indépendamment de leur emplacement, ce qui vous permet de garder le contrôle de votre contenu, même quand vous le partagez avec d’autres personnes.

Les paramètres de protection peuvent être :

- Une **partie de la configuration de votre étiquette**, afin que les utilisateurs puissent tous les classer et protéger des documents et des e-mails simplement en appliquant une étiquette. 
- **Utilisé seul**, par les applications et les services qui prennent en charge la protection, mais pas l’étiquetage. 

    Pour les applications et les services qui ne prennent en charge que la protection, les paramètres de protection sont utilisés en tant que [modèles Rights Management](#rights-management-templates).

Par exemple, vous pouvez configurer un document, comme un rapport ou une feuille de calcul de prévision de ventes, pour qu’il soit accessible uniquement par les personnes de votre organisation. Dans ce cas, vous devez appliquer des paramètres de protection pour contrôler si ce document peut être modifié, le limiter à un accès en lecture seule ou empêcher son impression.

Vous pouvez appliquer des paramètres de protection semblables aux e-mails pour empêcher leur transfert ou l’utilisation de l’option Répondre à tous.

### <a name="rights-management-templates"></a>Modèles Rights Management

Dès que le service Azure Rights Management est activé, deux modèles de gestion des droits par défaut sont disponibles : ils vous permettent de limiter l’accès aux données aux utilisateurs appartenant à votre organisation. Vous pouvez utiliser ces modèles immédiatement ou configurer vos propres paramètres de protection pour appliquer des contrôles plus restrictifs dans de nouveaux modèles.

Les modèles Rights Management peuvent être utilisés avec n’importe quel service ou application prenant en charge Azure Rights Management.

L’image suivante montre un exemple du centre d’administration Exchange, dans lequel vous pouvez configurer des règles de flux de messagerie Exchange Online pour utiliser les modèles RMS :

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="Exemple de sélection de modèles pour Exchange Online":::

> [!NOTE]
> Quand vous créez une étiquette AIP qui inclut des paramètres de protection, vous créez également un modèle Rights Management correspondant qui peut être utilisé séparément de l’étiquette. 
>  

Pour plus d’informations, consultez [En quoi consiste Azure Rights Management ?](what-is-azure-rms.md)

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>Intégration d’AIP à l’interface utilisateur final pour les documents et les e-mails

Le client AIP installe la barre Information Protection pour les applications Office et permet aux utilisateurs finaux d’intégrer AIP à leurs documents et e-mails.

Par exemple, dans Excel :

![Exemple de la barre Azure Information Protection dans Excel](./media/excelproplus-infoprotect-bar.png)

Bien que les étiquettes puissent être appliquées automatiquement aux documents et aux e-mails, ce qui permet de faciliter le travail des utilisateurs ou de respecter les stratégies d’une organisation, la barre Information Protection permet aux utilisateurs finaux de sélectionner des étiquettes et d’appliquer leur propre classification.

Par ailleurs, le client AIP permet aux utilisateurs de classifier et de protéger d’autres types de fichiers, ou plusieurs fichiers à la fois, à l’aide du menu contextuel de l’Explorateur de fichiers Windows. Par exemple :

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="Menu contextuel de l’Explorateur de fichiers : Classer et protéger avec Azure Information Protection":::

L’option de menu **Classifier et protéger** fonctionne de manière similaire à la barre Information Protection dans les applications Office, ce qui permet aux utilisateurs de sélectionner une étiquette ou de définir des autorisations personnalisées.

> [!TIP]
> Les utilisateurs avancés ou les administrateurs peuvent trouver l’utilisation des commandes PowerShell plus efficace pour la gestion et la configuration de la classification et de la protection de plusieurs fichiers. Les [commandes PowerShell pertinentes](/powershell/module/azureinformationprotection) sont incluses avec le client et peuvent également être installées séparément.

Les utilisateurs et les administrateurs peuvent utiliser les sites de suivi de documents pour superviser les documents protégés, qui y accède et quand. En outre, s’ils suspectent une utilisation incorrecte, ils peuvent révoquer l’accès à ces documents. Par exemple :

![Icône Révoquer l’accès du site de suivi de document](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Intégration supplémentaire pour les e-mails

L’utilisation d’AIP avec Exchange Online offre un avantage supplémentaire : la possibilité d’envoyer des e-mails protégés à n’importe quel utilisateur, avec l’assurance qu’il peut le lire sur n’importe quel appareil.

Par exemple, vous pouvez être amené à envoyer des informations sensibles à des adresses e-mail personnelles qui utilisent un compte **Gmail**, **Hotmail** ou **Microsoft** voire à des utilisateurs qui n’ont pas de compte dans Office 365 ou Azure AD. Ces e-mails doivent être chiffrés au repos et pendant le transit, et être lus seulement par les destinataires d’origine.

Ce scénario nécessite les [fonctionnalités de chiffrement de messages d’Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Si les destinataires ne peuvent pas ouvrir l’e-mail protégé dans leur client de messagerie intégré, ils peuvent utiliser un code secret à usage unique pour lire les informations sensibles dans un navigateur.

Par exemple, un utilisateur Gmail peut voir l’invite suivante dans un e-mail qu’il reçoit :

:::image type="content" source="media/ome-message.png" alt-text="Expérience du destinataire Gmail pour OME et AIP":::

Pour l’utilisateur qui envoie l’e-mail, les actions requises sont les mêmes que pour envoyer un e-mail protégé à un utilisateur de sa propre organisation. Par exemple, il peut sélectionner le bouton **Ne pas transférer** que le client AIP peut ajouter au ruban Outlook. 

Sinon, les fonctionnalités **ne pas transférer** peuvent être intégrées dans une étiquette que les utilisateurs peuvent sélectionner pour appliquer la classification et la protection à cet e-mail. Par exemple :

![Sélection d’une étiquette configurée pour appliquer la règle Ne pas transférer](./media/recipients-only-label2.png)

Les administrateurs peuvent également fournir automatiquement une protection aux utilisateurs en configurant des règles de flux de messagerie qui appliquent la protection des droits.

De même, tout document Office joint à ces e-mails est automatiquement protégé.

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>Recherche de contenu existant à classifier et à protéger

Dans l’idéal, vous étiquetez les documents et les e-mails au moment de leur création. Mais vous avez probablement de nombreux documents existants, stockés localement ou dans le cloud, que vous aimeriez aussi classifier et protéger.

Utilisez l’une des méthodes suivantes pour classifier et protéger le contenu existant :

- **Stockage local** : Utilisez le [scanneur Azure Information Protection](deploy-aip-scanner.md) pour découvrir, classifier et protéger des documents sur des partages réseau ainsi que des bibliothèques et des sites Microsoft SharePoint Server.

    Le scanneur s’exécute en tant que service sur Windows Server et utilise les mêmes règles de stratégie pour détecter les informations sensibles et appliquer des étiquettes spécifiques aux documents. 

    Vous pouvez également utiliser le scanneur pour appliquer une étiquette par défaut à tous les documents dans un référentiel de données sans inspecter le contenu des fichiers. Utilisez le scanneur en mode de création de rapports pour découvrir des informations sensibles dont vous ignorez peut-être qu’elles sont en votre possession.

- **Stockage de données dans le cloud** : Utilisez [Microsoft Cloud App Security](/cloud-app-security/azip-integration) pour appliquer vos étiquettes aux documents dans Box, SharePoint et OneDrive. Pour obtenir un tutoriel, consultez [Appliquer automatiquement des étiquettes de classification Azure Information Protection](/cloud-app-security/use-case-information-protection) 


## <a name="next-steps"></a>Étapes suivantes

Configurez et consultez les Azure Information Protection par vous-même avec notre guide de démarrage rapide et les didacticiels suivants :

- [Démarrage rapide : Déployer le client d’étiquetage unifié](quickstart-deploy-client.md)
- [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection](tutorial-install-scanner.md)
- [Tutoriel : Recherche de votre contenu sensible avec le scanneur Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Tutoriel : Empêcher les partages inappropriés dans Outlook avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)

Si vous êtes prêt à déployer ce service pour votre organisation, consultez les [guides pratiques](how-to-guides.md).