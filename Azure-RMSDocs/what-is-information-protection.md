---
title: Qu’est-ce qu’Azure Information Protection (AIP) ?
description: Azure Information Protection (AIP) est un service qui aide les organisations à étiqueter des documents et des e-mails. Il classe et protège les données, quel que soit l’endroit où elles sont enregistrées.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/23/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 25b520e08d8379580226d589fec511d502065156
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91588403"
---
# <a name="what-is-azure-information-protection"></a>Qu’est-ce qu’Azure Information Protection ?

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (AIP) est une solution basée sur le cloud qui permet à une organisation de classifier et de protéger ses documents et ses e-mails en les étiquetant. Il existe différents modes d’application des étiquettes :

- **Automatique**, par les administrateurs, avec des règles et des conditions
- **Manuelle**, par les utilisateurs
- **Mixte**, où les administrateurs définissent les recommandations présentées aux utilisateurs

Par exemple, votre administrateur peut configurer une étiquette avec des règles qui détectent des données sensibles, telles que les informations d’une carte de crédit. Dans ce cas, quand un utilisateur enregistre les informations d’une carte de crédit dans un fichier Word, une info-bulle recommandant d’appliquer l’étiquette correspondant à ce scénario est susceptible d’apparaître en haut du document.

Les étiquettes servent à [classer](#how-labels-apply-classification-with-aip) et, éventuellement, à [protéger](#how-aip-protects-your-data) les documents, ce qui permet d’effectuer différentes actions :

- **Suivre et contrôler** la manière dont le contenu est utilisé
- **Analyser les flux de données** pour mieux comprendre l’entreprise
**Détecter les comportements risqués** et prendre des mesures correctives
- **Effectuer un suivi de l’accès aux documents** et empêcher la fuite et l’usage abusif des données
- Etc.

## <a name="how-labels-apply-classification-with-aip"></a>Mode d’application de la classification des étiquettes avec AIP

Utilisez Azure Information Protection pour appliquer des étiquettes de classification aux documents et aux e-mails.

L’étiquetage du contenu comprend :

- Une **classification**, qui peut être détectée indépendamment de l’endroit où les données sont stockées ou des personnes avec qui elles sont partagées.
- Des **Marquages visuels** comme des en-têtes, des pieds de page ou des filigranes.
- Des **métadonnées** ajoutées aux fichiers et aux en-têtes d’e-mail en texte clair. Les métadonnées en texte clair permettent à d’autres services d’identifier la classification et de prendre des mesures appropriées.

Par exemple, dans l’image ci-dessous, l’étiquetage a classifié un e-mail dans la catégorie *Général* à l’aide du [client d’étiquetage unifié](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) :

:::image type="content" source="media/example-email-footerv2.png" alt-text="Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection":::

Dans cet exemple, l’étiquette a également :

- **Ajouté le pied de page *Sensibilité : Général* à l’e-mail.** Ce pied de page est un indicateur visuel pour tous les destinataires auxquels il est destiné spécifiant qu’il s’agit de données métier d’ordre général qui ne doivent pas être envoyées à l’extérieur de l’organisation.
- **Incorporé des métadonnées dans les en-têtes d’e-mail.** Les données d’en-tête permettent aux services de messagerie d’inspecter l’étiquette et de créer théoriquement une entrée d’audit ou d’empêcher son envoi en dehors de l’organisation.

## <a name="how-aip-protects-your-data"></a>Protection des données avec AIP

Azure Information Protection utilise le [*service Azure Rights Management* (Azure RMS)](what-is-azure-rms.md) pour protéger les données. 

Azure RMS est intégré à d’autres services et applications cloud Microsoft, comme Microsoft 365 et Azure Active Directory. Il peut également être utilisé avec vos propres applications et solutions de protection des informations ou celles de tiers. Azure RMS fonctionne avec les solutions locales et cloud.

Azure RMS utilise des stratégies de chiffrement, d’identité et d’autorisation. À l’image des étiquettes AIP, la protection avec Azure RMS reste associée aux documents et aux e-mails, indépendamment de leur emplacement, ce qui vous permet de garder le contrôle de votre contenu, même quand vous le partagez avec d’autres personnes.

Les paramètres de protection peuvent être :

- **inclus dans votre configuration des étiquettes** pour permettre aux utilisateurs de classer et de protéger leurs documents et leurs e-mails en appliquant simplement une étiquette ; 
- **utilisés seuls**, par les applications et services qui prennent en charge la protection, mais non l’étiquetage. 

    Pour les applications et les services qui ne prennent en charge que la protection, les paramètres de protection sont utilisés en tant que [modèles Rights Management](#rights-management-templates).

Par exemple, vous pouvez configurer un document, comme un rapport ou une feuille de calcul de prévision de ventes, pour qu’il soit accessible uniquement par les personnes de votre organisation. Dans ce cas, vous devez appliquer des paramètres de protection pour contrôler si ce document peut être modifié, le limiter à un accès en lecture seule ou empêcher son impression.

Vous pouvez appliquer des paramètres de protection semblables aux e-mails pour empêcher leur transfert ou l’utilisation de l’option Répondre à tous.

### <a name="rights-management-templates"></a>Modèles Rights Management

Dès que le service Azure Rights Management est activé, deux modèles de gestion des droits par défaut sont disponibles : ils vous permettent de limiter l’accès aux données aux utilisateurs appartenant à votre organisation. Vous pouvez utiliser ces modèles immédiatement ou configurer vos propres paramètres de protection pour appliquer des contrôles plus restrictifs dans de nouveaux modèles.

Les modèles Rights Management peuvent être utilisés avec n’importe quel service ou application prenant en charge Azure Rights Management.

L’image suivante montre un exemple du centre d’administration Exchange, dans lequel vous pouvez configurer des règles de flux de messagerie Exchange Online pour utiliser les modèles RMS :

:::image type="content" source="media/templates-exchangeonline-callouts.png" alt-text="Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection":::

> [!NOTE]
> Quand vous créez une étiquette AIP qui inclut des paramètres de protection, vous créez également un modèle Rights Management correspondant qui peut être utilisé séparément de l’étiquette. 
>  

Pour plus d’informations, consultez [En quoi consiste Azure Rights Management ?](what-is-azure-rms.md)

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>Intégration d’AIP à l’interface utilisateur final pour les documents et les e-mails

Le client AIP installe la barre Information Protection pour les applications Office et permet aux utilisateurs finaux d’intégrer AIP à leurs documents et e-mails.

Par exemple, dans Excel, si vous utilisez le [client d’étiquetage unifié](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) :

![Exemple de la barre Azure Information Protection dans Excel](./media/excelproplus-infoprotect-bar.png)

Bien que les étiquettes puissent être appliquées automatiquement aux documents et aux e-mails, ce qui permet de faciliter le travail des utilisateurs ou de respecter les stratégies d’une organisation, la barre Information Protection permet aux utilisateurs finaux de sélectionner des étiquettes et d’appliquer leur propre classification.

Par ailleurs, le client AIP permet aux utilisateurs de classifier et de protéger d’autres types de fichiers, ou plusieurs fichiers à la fois, à l’aide du menu contextuel de l’Explorateur de fichiers Windows. Par exemple :

:::image type="content" source="media/right-click-classify-protect-folder.png" alt-text="Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection":::

L’option de menu **Classifier et protéger** fonctionne de manière similaire à la barre Information Protection dans les applications Office, ce qui permet aux utilisateurs de sélectionner une étiquette ou de définir des autorisations personnalisées.

> [!TIP]
> Les utilisateurs avancés ou les administrateurs peuvent trouver l’utilisation des commandes PowerShell plus efficace pour la gestion et la configuration de la classification et de la protection de plusieurs fichiers. Les [commandes PowerShell pertinentes](/powershell/module/azureinformationprotection) sont incluses avec le client et peuvent également être installées séparément.

Les utilisateurs et les administrateurs peuvent utiliser les sites de suivi de documents pour superviser les documents protégés, qui y accède et quand. En outre, s’ils suspectent une utilisation incorrecte, ils peuvent révoquer l’accès à ces documents. Par exemple :

![Icône Révoquer l’accès du site de suivi de document](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Intégration supplémentaire pour les e-mails

L’utilisation d’AIP avec Exchange Online offre un avantage supplémentaire : la possibilité d’envoyer des e-mails protégés à n’importe quel utilisateur, avec l’assurance qu’il peut le lire sur n’importe quel appareil.

Par exemple, vous pouvez être amené à envoyer des informations sensibles à des adresses e-mail personnelles qui utilisent un compte **Gmail**, **Hotmail** ou **Microsoft** voire à des utilisateurs qui n’ont pas de compte dans Microsoft 365 ou Azure AD. Ces e-mails doivent être chiffrés au repos et pendant le transit, et être lus seulement par les destinataires d’origine.

Ce scénario nécessite les [fonctionnalités de chiffrement de messages d’Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Si les destinataires ne peuvent pas ouvrir l’e-mail protégé dans leur client de messagerie natif, ils peuvent utiliser un code secret à usage unique pour lire les informations sensibles dans un navigateur.

Par exemple, un utilisateur Gmail peut voir l’invite suivante dans un e-mail qu’il reçoit :

:::image type="content" source="media/ome-message.png" alt-text="Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection":::

Pour l’utilisateur qui envoie l’e-mail, les actions requises sont les mêmes que pour envoyer un e-mail protégé à un utilisateur de sa propre organisation. Par exemple, il peut sélectionner le bouton **Ne pas transférer** que le client AIP peut ajouter au ruban Outlook. 

La fonctionnalité Ne pas transférer peut également être intégrée dans une étiquette que les utilisateurs peuvent sélectionner pour que l’e-mail soit classifié et protégé. Par exemple, si vous utilisez le [client d’étiquetage unifié](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) :

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

## <a name="latest-labeling-updates-for-microsoft-365"></a>Mises à jour les plus récentes de l’étiquetage pour Microsoft 365

Consultez les dernières informations sur la façon dont Azure Information Protection vous aide à détecter, classifier, protéger et superviser vos informations sensibles, où qu’elles se trouvent, à l’aide de Microsoft 365 :

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

Pour plus d'informations, voir :

- [Nouveautés du Centre d’administration Microsoft 365](/microsoft-365/admin/whats-new-in-preview)
- [Nouveautés du Centre d’administration SharePoint](/sharepoint/what-s-new-in-admin-center)

## <a name="additional-azure-information-protection-resources"></a>Ressources supplémentaires sur Azure Information Protection

- **Essai gratuit :** [Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- **Options d’abonnement et tarifs :** [Tarification d’Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)

- **Téléchargement du client :** [Client Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018)

- **Téléchargement d’un guide d’utilisation personnalisable :** [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- **FAQ :** [Forum aux questions sur Azure Information Protection](faqs.md)

- **Yammer :** [Azure Information Protection](https://www.yammer.com/AskIPTeam)

- **Flux Twitter Docs :** [https://twitter.com/docsmsft](https://twitter.com/docsmsft)

**Ressources complémentaires :** [Informations et prise en charge pour Azure Information Protection](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

L’événement Microsoft Ignite 2019 organisé à Orlando a connu un immense succès ! Il y avait un grand nombre d’informations utiles sur Azure Information Protection avec les dernières mises à jour et améliorations. Si vous n’avez pas pu y participer, les sessions sont enregistrées pour être consultées ultérieurement.

Consultez la liste suivante pour connaitre les cinq premières sessions recommandées :

- [BRK2119 : sécurisez vos données sensibles ! Comprendre les fonctionnalités les plus récentes de Microsoft Information Protection](https://myignite.techcommunity.microsoft.com/sessions/81172?source=sessions)
 
- [THR3067 : connaissez vos données : cinq trucs et astuces pour mieux comprendre votre environnement de données sensibles](https://myignite.techcommunity.microsoft.com/sessions/81183)

- [BRK3103 : la protection des fichiers et des données sensibles peut être difficile. Choisir les options de protection des données appropriées qui équilibrent la productivité de la sécurité et du travail](https://myignite.techcommunity.microsoft.com/sessions/81177?source=sessions)

- [BRK2120 : activer Azure Information Protection ? Navigation dans l’étiquetage unifiée, configuration de stratégie, clients et analytique](https://myignite.techcommunity.microsoft.com/sessions/81178?source=sessions)

- [BRK2121 : étendez la puissance de l’étiquetage et la protection de la sensibilité à vos propres applications et solutions ISV avec le kit de développement logiciel (SDK) Microsoft Information Protection](https://myignite.techcommunity.microsoft.com/sessions/81179?source=sessions)

Dernier billet de blog : [Découvrir où se trouvent vos données sensibles et les protéger intelligemment avec Microsoft 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Understand-where-your-sensitive-data-is-located-and/ba-p/960465)


## <a name="next-steps"></a>Étapes suivantes

Configurez et découvrez Azure Information Protection par vous-même avec nos [guides de démarrage rapide](quickstart-viewpolicy.md) et nos [tutoriels](infoprotect-quick-start-tutorial.md). 

Si vous êtes prêt à déployer ce service pour votre organisation, consultez les [guides pratiques](how-to-guides.md).