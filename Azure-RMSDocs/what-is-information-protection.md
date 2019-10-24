---
title: Qu’est-ce qu’Azure Information Protection ? - AIP
description: Vue d’ensemble technique du service Azure Information Protection, qui permet à une organisation d’étiqueter des documents et des e-mails pour classifier et protéger ses données, où que celles-ci résident.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/18/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 0659abcb6211bc05a6db435db759eed8f6c44cea
ms.sourcegitcommit: 2f092b395e31ce64df8b9148433032be5702217e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72589604"
---
# <a name="what-is-azure-information-protection"></a>Qu’est-ce qu’Azure Information Protection ?

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection (parfois appelée AIP) est une solution basée sur le cloud qui permet à une organisation de classifier et, facultativement, de protéger ses documents et e-mails en y appliquant des étiquettes. Les étiquettes peuvent être appliquées automatiquement par les administrateurs qui définissent des règles et des conditions ou manuellement par les utilisateurs, qui peuvent éventuellement recevoir des suggestions. 

L’image suivante illustre Azure Information Protection en action sur l’ordinateur d’un utilisateur. L’administrateur a configuré une étiquette avec des règles qui détectent les données sensibles. Dans notre exemple, il s’agit d’informations sur une carte de crédit. Quand un utilisateur enregistre un document Word qui contient un numéro de carte de crédit, il voit une info-bulle personnalisée qui lui recommande l’étiquette que l’administrateur a configurée. Cette étiquette classifie le document et le protège. 

![Exemple de classification recommandée pour Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classicfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Capture d’écran du [client Azure Information Protection (classique)](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

Une fois que votre contenu est classifié (et éventuellement protégé), vous pouvez suivre et contrôler son utilisation. Vous pouvez analyser les flux de données pour obtenir des informations sur vos activités, détecter les comportements à risque et prendre des mesures correctives, suivre l’accès aux documents, empêcher la fuite de données ou une mauvaise utilisation des données, etc.

## <a name="how-labels-apply-classification"></a>Comment les étiquettes appliquent la classification

Les étiquettes Azure Information Protection vous permettent d’appliquer une classification aux documents et e-mails. Ainsi, la classification est identifiable, quel que soit l’endroit où les données sont stockées ou les personnes avec lesquelles elles sont partagées. Les étiquettes peuvent intégrer des marquages visuels comme les en-têtes, pieds de page ou filigranes. Les métadonnées sont ajoutées aux fichiers et aux en-têtes d’e-mail en texte clair. Le texte clair fait en sorte que les autres services, comme les solutions de prévention de perte de données, puissent identifier la classification et prendre les mesures appropriées. 

Par exemple, l’e-mail suivant a été classé sous l’étiquette « Général ». L’étiquette a ajouté un pied de page de « Sensibilité : Général » à l’e-mail. Ce pied de page est un indicateur visuel pour tous les destinataires auxquels il est destiné spécifiant qu’il s’agit de données métier d’ordre général qui ne doivent pas être envoyées à l’extérieur de l’organisation. Cette étiquette est incorporée aux en-têtes d’e-mail afin que les services d’e-mail puissent inspecter cette valeur et éventuellement créer une entrée d’audit ou empêcher son envoi à l’extérieur de l’organisation.

![Exemple d’en-têtes et de pied de page d’e-mail montrant la classification Azure Information Protection](./media/example-email-footerv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classicfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Capture d’écran du [client Azure Information Protection (classique)](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

## <a name="how-data-is-protected"></a>Comment les données sont protégées

La technologie de protection utilise *Azure Rights Management* (ou Azure RMS, dans sa forme abrégée courante). Cette technologie est intégrée à d’autres services cloud et applications Microsoft, tels qu’Office 365 et Azure Active Directory. Vous pouvez aussi l’utiliser avec vos propres applications métier et avec les solutions de protection des informations d’autres éditeurs de logiciels, que ces applications et solutions soient locales ou dans le cloud.

Cette technologie de protection utilise des stratégies de chiffrement, d’identité et d’autorisation. À l’image des étiquettes appliquées, la protection avec Rights Management reste associée aux documents et aux e-mails, indépendamment de leur emplacement (à l’intérieur ou en dehors de votre organisation, de vos réseaux, de vos serveurs de fichiers et de vos applications). Cette solution de protection des informations vous permet de garder le contrôle de vos données, même quand vous les partagez avec d'autres personnes.

Par exemple, vous pouvez configurer un document (rapport, feuille de calcul de prévision de ventes, etc.) pour qu’il soit accessible uniquement par les personnes de votre organisation et déterminer s’il peut être modifié, s’il est disponible en lecture seule uniquement ou empêcher son impression. Vous pouvez configurer les e-mails de la même façon et également empêcher leur transfert ou l'utilisation de l'option Répondre à tous. 

Ces paramètres de protection peuvent être inclus dans votre configuration d’étiquette pour permettre aux utilisateurs de classifier et protéger leurs documents et e-mails simplement en appliquant une étiquette. Toutefois, les mêmes paramètres de protection peuvent aussi être utilisés par les applications et services qui prennent en charge la protection, mais pas l’étiquetage. Pour ces applications et services, les paramètres de protection deviennent disponibles en tant que *modèles Rights Management*.

### <a name="rights-management-templates"></a>Modèles Rights Management

Dès que le service Azure Rights Management est activé, deux modèles par défaut sont disponibles, qui vous permettent de limiter l’accès aux données aux utilisateurs appartenant à votre organisation. Vous pouvez utiliser ces modèles pour empêcher immédiatement une fuite des données hors de votre organisation. Vous pouvez également compléter ces modèles par défaut en configurant vos propres paramètres de protection qui appliquent des contrôles plus restrictifs.

Quand vous créez une étiquette pour Azure Information Protection qui inclut des paramètres de protection, cette action crée en fait un modèle Rights Management correspondant. Vous pouvez ensuite utiliser aussi ce modèle avec les applications et services qui prennent en charge Azure Rights Management.

Par exemple, à partir du centre d’administration Exchange, configurez les règles de flux de courrier Exchange Online pour utiliser ces modèles :

![Exemple de sélection de modèles pour Exchange Online](./media/templates-exchangeonline-callouts.png)

Pour plus d’informations sur la protection Azure Rights Management, consultez [Qu’est-ce qu’Azure Rights Management ?](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>Intégration avec les flux de travail de l’utilisateur final pour les documents et les e-mails

Azure Information Protection s’intègre aux workflows existants des utilisateurs finaux quand le client Azure Information Protection est installé. Ce client installe la barre Information Protection dans les applications Office, comme illustré dans la première image qui montre cette barre dans Word. La même barre Information Protection est ajoutée à Excel, PowerPoint et Outlook. Par exemple :

![Exemple de la barre Azure Information Protection dans Excel](./media/excelproplus-infoprotect-bar.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Capture d’écran du [client d’étiquetage unifié Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) 

Cette barre Information Protection permet aux utilisateurs finaux de sélectionner des étiquettes pour une classification correcte. Si nécessaire, les étiquettes peuvent également être appliquées automatiquement pour faciliter le travail des utilisateurs ou pour respecter les stratégies de votre organisation.

Pour classer et protéger d’autres types de fichiers, et pour prendre en charge plusieurs fichiers à la fois, les utilisateurs peuvent cliquer avec le bouton droit sur les fichiers ou sur un dossier à partir de l’Explorateur de fichiers Windows :

![Menu contextuel de l’Explorateur de fichiers, Classifier et protéger avec Azure Information Protection](./media/right-click-classify-protect-folder.png)

Lorsque les utilisateurs sélectionnent l’option **Classifier et protéger**dans l’Explorateur de fichiers, ils peuvent ensuite sélectionner une étiquette de la même façon qu’ils utilisent la barre Information Protection dans leurs applications de bureau Office. Ils peuvent également définir leurs propres autorisations personnalisées, si nécessaire.

Les utilisateurs avancés (et administrateurs) peuvent trouver l’utilisation des commandes PowerShell plus efficace pour la gestion et la configuration de la classification et de la protection de plusieurs fichiers. Les commandes PowerShell pour effectuer ces actions sont automatiquement incluses dans le client, même si vous pouvez également installer le module PowerShell séparément.

Après qu’un document a été protégé, les utilisateurs et administrateurs peuvent utiliser un site de suivi des documents pour surveiller qui accède à ces documents et à quel moment. En outre, s’ils suspectent une utilisation incorrecte, ils peuvent révoquer l’accès à ces documents :

![Icône Révoquer l’accès du site de suivi de document](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Intégration supplémentaire pour les e-mails

Lorsque vous utilisez Azure Information Protection avec Exchange Online, vous recevez un avantage supplémentaire : La possibilité d’envoyer des e-mails protégés à n’importe quel utilisateur, avec l’assurance qu’ils peuvent le lire sur n’importe quel appareil.

Par exemple, des utilisateurs doivent envoyer des informations sensibles à des adresses e-mail personnelles qui utilisent un compte **Gmail**, **Hotmail** ou **Microsoft**. Ou à des utilisateurs qui n’ont pas de compte dans Office 365 ou Azure AD. Ces e-mails doivent être chiffrés au repos et pendant le transit, et être lus seulement par les destinataires d’origine.

Ce scénario nécessite les [nouvelles fonctionnalités de chiffrement de messages d’Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Si les destinataires ne peuvent pas ouvrir l’e-mail protégé dans leur client de messagerie natif, ils peuvent utiliser un code secret à usage unique pour lire les informations sensibles dans un navigateur.

Par exemple, un utilisateur Gmail voit ceci dans un e-mail :

![Expérience du destinataire Gmail pour OME et AIP](./media/ome-message.png)

Pour les utilisateurs qui envoient l’e-mail, leur flux de travail ne diffère pas de l’envoi d’un e-mail protégé à un utilisateur de leur propre organisation. Par exemple, ils peuvent sélectionner le bouton **Ne pas transférer** que le client Azure Information Protection peut ajouter au ruban Outlook. Cette fonctionnalité Ne pas transférer peut aussi être intégrée dans une étiquette que les utilisateurs sélectionnent, pour que l’e-mail soit classé et protégé. Par exemple :

![Sélection d’une étiquette configurée pour appliquer la règle Ne pas transférer](./media/recipients-only-label2.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Capture d’écran du [client d’étiquetage unifié Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

Vous pouvez aussi fournir automatiquement une protection aux utilisateurs avec des règles de flux de messagerie qui appliquent une protection des droits. 

Quand vous joignez des documents Office à ces e-mails, ces documents sont eux aussi automatiquement protégés.

## <a name="classifying-and-protecting-existing-documents"></a>Classification et la protection de documents existants

Dans l’idéal, les documents et e-mails sont étiquetés lors de leur création. Mais vous avez probablement dans vos banques de données de nombreux documents que vous souhaitez classifier pour les protéger également. Ces magasins de données peut être locaux ou dans le cloud.

Pour vos magasins de données locaux, utilisez le scanneur Azure Information Protection pour détecter, classifier et protéger des documents sur des dossiers locaux, des partages réseau et des sites SharePoint Server, ainsi que des bibliothèques. Le scanneur s’exécute en tant que service sur Windows Server. Vous pouvez utiliser les mêmes règles en termes de stratégie pour détecter les informations sensibles et appliquer des étiquettes spécifiques aux documents. Ou vous pouvez appliquer une étiquette par défaut à tous les documents dans un référentiel de données sans inspecter le contenu des fichiers. Vous pouvez également utiliser l’Analyseur de fichier uniquement en mode de création de rapports pour vous aider à découvrir des informations sensibles dont vous ignorez peut-être qu’elles sont en votre possession. 

Pour en savoir plus sur le déploiement et l’utilisation du scanneur, consultez [Déploiement du scanneur Azure Information Protection pour classifier et protéger automatiquement les fichiers](deploy-aip-scanner.md).

Pour vos magasins de données cloud, utilisez Microsoft Cloud App Security pour appliquer vos étiquettes aux documents dans Box, SharePoint Online et OneDrive entreprise. Pour plus d’informations, consultez [Appliquer automatiquement des étiquettes de classification Azure Information Protection](/cloud-app-security/use-case-information-protection) et [Intégration d’Azure Information Protection](/cloud-app-security/azip-integration).

## <a name="latest-labeling-updates-for-microsoft-365"></a>Mises à jour les plus récentes de l’étiquetage pour Microsoft 365

Consultez les dernières informations sur la façon dont Azure Information Protection vous aide à détecter, classifier, protéger et surveiller vos informations sensibles, où qu’il réside :

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

## <a name="resources-for-azure-information-protection"></a>Ressources pour Azure Information Protection

- Essai gratuit : [Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Options d'abonnement et tarification : [Tarification d’Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)

- Téléchargez le client : [Client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- Téléchargez un guide d’utilisation personnalisable : [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

- Foires aux questions : [Forum aux questions sur Azure Information Protection](faqs.md)

- Yammer : [Azure Information Protection](https://www.yammer.com/AskIPTeam)

- Nouveautés de la documentation : [Blog technique Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/bg-p/AzureInformationProtectionBlog/label-name/Docs)

Ressources supplémentaires : [Informations et prise en charge pour Azure Information Protection](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2019 dans Orlando arrive ! Il y aura un grand nombre d’informations utiles sur Azure Information Protection avec les dernières mises à jour et améliorations. Nous espérons vous y rencontrer, mais si vous ne pouvez pas nous rejoindre, les sessions sont enregistrées pour être consultées ultérieurement.

Consultez la liste suivante pour connaitre les cinq premières sessions recommandées. Des liens sont ajoutés lorsque les enregistrements sont disponibles :

- BRK2119 : sécurisez vos données sensibles ! Comprendre les fonctionnalités les plus récentes de Microsoft Information Protection
 
- BRK3100 : à quoi ressemble votre paysage de données sensibles ? Meilleures pratiques pour la découverte, la classification, l’analyse et les rapports de données

- BRK3103 : la protection des fichiers et des données sensibles peut être difficile. Choisir les options de protection des données appropriées qui équilibrent la productivité de la sécurité et du travail

- BRK2120 : activer Azure Information Protection ? Navigation dans l’étiquetage unifiée, configuration de stratégie, clients et analytique

- BRK2121 : étendez la puissance de l’étiquetage et la protection de la sensibilité à vos propres applications et solutions ISV avec le kit de développement logiciel (SDK) Microsoft Information Protection

## <a name="next-steps"></a>Étapes suivantes

Configurez et découvrez Azure Information Protection par vous-même avec nos [démarrages rapides](quickstart-viewpolicy.md) et nos [tutoriels](infoprotect-quick-start-tutorial.md). Ou, si vous êtes prêt à déployer ce service pour votre organisation, consultez les [guides pratiques](how-to-guides.md).
