---
title: FAQ sur la classification et l’étiquetage - AIP
description: Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4a8df46df14a4c06196d204865f7a99ce5fa5821
ms.sourcegitcommit: 332801617ce83ebb3f01edf34cbb69b810662be7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68808048"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Que puis-je faire avec les fonctionnalités de classification disponibles dans Azure Information Protection ?

Essayez notre tutoriel [Modifier la stratégie et créer une nouvelle étiquette](infoprotect-quick-start-tutorial.md) pour en voir une démonstration de quelques minutes seulement.

Pour être informé de la mise à disposition de fonctionnalités de classification supplémentaires, consultez les annonces publiées sur le [blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). La version actuelle présente quelques limites, notamment :

- Aucune possibilité d’étiquetage dans Office Web Apps (Office pour le Web).

- Aucune intégration de classification et d’étiquetage n’est assurée avec Exchange Online ou SharePoint Online.

> [!NOTE]
> **Maintenant en préversion** :
> - Création de rapports centralisée pour la classification et l’étiquetage. Pour plus d’informations, consultez [Création de rapports centralisée pour Azure Information Protection](reports-aip.md).
>
>**Récemment publié** :
> - capacité d’étiquetage intégrée aux applications Office pour appareils mobiles (iOS et Android) et ordinateurs Mac. Pour plus d’informations, consultez [Appliquer des étiquettes de sensibilité à vos documents et e-mails dans Office](https://aka.ms/officemipdocs).

Demandez de nouvelles fonctionnalités et votez pour les demandes en visitant le [site UserVoice](https://msip.uservoice.com/) pour Azure Information Protection.

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>Quel client dois-je installer pour tester les nouvelles fonctionnalités?

Actuellement, il existe deux clients pour Windows: 

- Le **Azure information protection client d’étiquetage unifié** qui télécharge des étiquettes et des paramètres de stratégie à partir de l’un des centres d’administration suivants: Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center, Microsoft 365 Compliance Center. Ce client est désormais en disponibilité générale et dispose d’une version préliminaire qui vous permet de tester des fonctionnalités supplémentaires pour une version ultérieure.

- Le **client Azure information protection (Classic)** qui télécharge des étiquettes et des paramètres de stratégie à partir du portail Azure. Ce client s’appuie sur les versions de disponibilité générale précédentes du client.

Nous vous recommandons de tester avec le client d’étiquetage unifié si son ensemble de fonctionnalités et ses fonctionnalités actuelles répondent aux besoins de votre entreprise. Si ce n’est pas le cas, ou si vous avez configuré des étiquettes dans le Portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](configure-policy-migrate-labels.md), utilisez le client classique.

Pour plus d’informations, consultez [Choisir le client Azure Information Protection à utiliser](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use), notamment pour visualiser un tableau de comparaison des fonctionnalités.

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Toutefois, si les utilisateurs sélectionnent une sous-étiquette, cela revient à appliquer deux étiquettes à la fois : une étiquette principale et une étiquette secondaire. Les sous-étiquettes permettent d’attribuer à un fichier deux classifications avec une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **Confidentiel** peut contenir des sous-étiquettes comme **Juridique** et **Finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **Confidentiel** elle-même. Il peut seulement sélectionner une de ses sous-étiquettes, comme **Juridique**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Quand vous utilisez des sous-étiquettes, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Quand vous utilisez des sous-niveaux, configurez ces paramètres pour la sous-étiquette uniquement. Si vous configurez ces paramètres sur l’étiquette principale et sa sous-étiquette, ce sont les paramètres de la sous-étiquette qui sont prioritaires.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Comment empêcher une personne de supprimer ou de changer une étiquette ?

Il existe bien un [paramètre de stratégie](configure-policy-settings.md) qui demande aux utilisateurs d’indiquer pourquoi ils baissent une étiquette de classement, ou suppriment une étiquette ou une protection, mais il ne les empêche pas d’effectuer ces actions. Pour empêcher les utilisateurs de supprimer ou de changer une étiquette, le contenu doit déjà être protégé et les autorisations de protection ne doivent pas leur accorder le [droit d’utilisation](configure-usage-rights.md) Exportation ou Contrôle total. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

Pour plus d’informations sur ces métadonnées, consultez [Étiquettes d’information stockées dans des e-mails et des documents](configure-policy.md#label-information-stored-in-emails-and-documents).

Pour obtenir des exemples d’utilisation de ces métadonnées avec des règles de flux de messagerie Exchange Online, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>Peut-on créer un modèle de document qui inclut automatiquement la classification ?

Oui. Vous pouvez configurer une étiquette qui [applique un en-tête ou un pied de page comportant le nom d’étiquette](configure-policy-markings.md). Si toutefois cela ne répond pas à vos besoins, vous pouvez créer un modèle de document présentant la mise en forme de votre choix et ajouter la classification comme code de champ. 

Par exemple, vous pouvez avoir une table dans l’en-tête de votre document qui affiche la classification, ou utiliser une formulation spécifique pour une introduction faisant référence à la classification du document.

Pour ajouter ce code de champ dans votre document :

1. Étiquetez le document et enregistrez-le. Cette action crée de nouveaux champs de métadonnées que vous pouvez alors utiliser dans votre code de champ.

2. Dans le document, placez le curseur à l’endroit où vous souhaitez ajouter la classification de l’étiquette ; ensuite, dans l’onglet **Insérer**, sélectionnez **Texte** > **QuickPart** > **Champ**.

3. Dans la liste déroulante **Catégories** de la boîte de dialogue **Champ**, sélectionnez **Informations sur le document**. Ensuite, dans la liste déroulante **Noms de champs**, sélectionnez **DocProperty**.

4. Dans la liste déroulante **Propriété**, sélectionnez **Sensibilité**, puis **OK**.

La classification de l’étiquette actuelle s’affiche dans le document ; cette valeur est actualisée automatiquement à chaque fois que vous ouvrez le document ou que vous utilisez le modèle. Par conséquent, lorsque l’étiquette change, la classification qui s’affiche pour ce code de champ est automatiquement mise à jour dans le document.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>En quoi la classification Azure Information Protection pour les e-mails est-elle différente de celle des messages Exchange ?

La classification des messages Exchange est une ancienne fonctionnalité permettant de classer des e-mails. Elle est mise en œuvre indépendamment de la classification Azure Information Protection. 

Toutefois, vous pouvez intégrer les deux solutions pour que, quand les utilisateurs classifient un e-mail à l’aide de la version web d’Outlook et de certaines applications de messagerie mobile, la classification Azure Information Protection et ses marquages d’étiquette correspondants soient automatiquement ajoutés. 

Vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec Outlook sur le web et les applications de messagerie mobile.

Pour les étapes de configuration, consultez [Intégration de la classification des messages Exchange avec Azure Information Protection pour une solution d’étiquetage sur appareil mobile](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution).
