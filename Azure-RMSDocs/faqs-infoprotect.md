---
title: FAQ sur la classification et l’étiquetage - AIP
description: Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 691bf76154689e69966f173a19e047120748687b
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474696"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Que puis-je faire avec les fonctionnalités de classification disponibles dans Azure Information Protection ?

Essayez notre didacticiel de démarrage rapide pour obtenir une démonstration en quelques minutes : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Pour être informé de la mise à disposition de fonctionnalités de classification supplémentaires, consultez les annonces publiées sur le [blog Enterprise Mobility and Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). La version actuelle présente quelques limites, notamment :

- Il n’existe aucun enregistrement centralisé pour la classification et l’étiquetage.

- L’étiquetage n’est pas pris en charge pour les applications Office pour appareils mobiles (iOS et Android) et les ordinateurs Mac, ni pour les applications web Office (Office Online).

- Aucune intégration de classification et d’étiquetage n’est assurée avec Exchange Online ou SharePoint Online.

Demandez de nouvelles fonctionnalités et votez pour les demandes en visitant le [site User Voice](https://msip.uservoice.com/) pour Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>Dois-je être un administrateur global pour configurer la classification et les étiquettes ?

Avec le nouveau rôle Administrateur Information Protection, cette question a maintenant sa réponse dans la page principale des questions fréquentes (FAQ) : [Faut-il être administrateur général pour configurer Azure Information Protection ou puis-je déléguer la configuration à d’autres administrateurs ?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

Toutefois, si vous sélectionnez cette option pour installer la stratégie de démonstration au moment de l’installation du [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), vous n’êtes pas obligé de vous connecter au portail pour voir et tester la fonctionnalité d’étiquetage. La stratégie de démonstration installe localement une stratégie par défaut pour Azure Information Protection. Vous pouvez donc essayer l’étiquetage des documents et des e-mails, mais vous ne pouvez pas modifier ni ajouter de nouvelles étiquettes sans vous connecter au portail Azure. 

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Toutefois, si les utilisateurs sélectionnent une sous-étiquette, cela revient à appliquer deux étiquettes à la fois : une étiquette principale et une étiquette secondaire. Les sous-étiquettes permettent d’attribuer à un fichier deux classifications avec une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **Confidentiel** peut contenir des sous-étiquettes comme **Juridique** et **Finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **Confidentiel** elle-même. Il peut seulement sélectionner une de ses sous-étiquettes, comme **Juridique**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Quand vous utilisez des sous-étiquettes, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Quand vous utilisez des sous-niveaux, configurez ces paramètres pour la sous-étiquette uniquement. Si vous configurez ces paramètres sur l’étiquette principale et sa sous-étiquette, ce sont les paramètres de la sous-étiquette qui sont prioritaires.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Comment empêcher une personne de supprimer ou de changer une étiquette ?

Il existe bien un [paramètre de stratégie](./deploy-use/configure-policy-settings.md) qui demande aux utilisateurs d’indiquer pourquoi ils baissent une étiquette de classement, ou suppriment une étiquette ou une protection, mais il ne les empêche pas d’effectuer ces actions. Pour empêcher les utilisateurs de supprimer ou de changer une étiquette, le contenu doit déjà être protégé et les autorisations de protection ne doivent pas leur accorder le [droit d’utilisation](./deploy-use/configure-usage-rights.md) Exportation ou Contrôle total. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

Pour plus d’informations et pour obtenir des exemples d’utilisation de ces métadonnées avec des règles de flux de messagerie Exchange Online, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](./deploy-use/configure-exo-rules.md).

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>En quoi la classification Azure Information Protection pour les e-mails est-elle différente de celle des messages Exchange ?

La classification des messages Exchange est une ancienne fonctionnalité permettant de classer des e-mails. Elle est mise en œuvre indépendamment de la classification Azure Information Protection. 

Toutefois, vous pouvez intégrer les deux solutions pour que, quand les utilisateurs classifient un e-mail à l’aide de la version web d’Outlook et de certaines applications de messagerie mobile, la classification Azure Information Protection et ses marquages d’étiquette correspondants soient automatiquement ajoutés. 

Vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec Outlook sur le web et les applications de messagerie mobile.

Pour les étapes de configuration, consultez [Intégration de la classification des messages Exchange avec Azure Information Protection pour une solution d’étiquetage sur appareil mobile](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution). 



