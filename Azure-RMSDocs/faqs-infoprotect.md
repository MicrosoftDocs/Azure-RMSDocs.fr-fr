---
title: FAQ sur la classification et l’étiquetage - AIP
description: Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b41195e6eb50dffe5aada630b423a73c0024d244
ms.sourcegitcommit: 0793013ad733ac2af5de498289849979501b8f6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88788626"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>Quel client dois-je installer pour tester les nouvelles fonctionnalités ?

Actuellement, il existe deux clients Azure Information Protection pour Windows : 

- Le **Azure information protection client d’étiquetage unifié** qui télécharge des étiquettes et des paramètres de stratégie à partir de l’un des centres d’administration suivants : Office 365 Security & Compliance center, Microsoft 365 Security center, Microsoft 365 Compliance Center. Ce client est désormais en disponibilité générale et peut disposer d’une préversion pour tester des fonctionnalités supplémentaires pour une version ultérieure.

- Le **client Azure information protection (Classic)** qui télécharge des étiquettes et des paramètres de stratégie à partir du portail Azure. Ce client s’appuie sur les versions de disponibilité générale précédentes du client.

Nous vous recommandons de tester avec le client d’étiquetage unifié si son ensemble de fonctionnalités et ses fonctionnalités actuelles répondent aux besoins de votre entreprise. Si ce n’est pas le cas, ou si vous avez configuré des étiquettes dans le Portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](configure-policy-migrate-labels.md), utilisez le client classique. Pour plus d’informations, consultez [Choisir le client Azure Information Protection à utiliser](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers), notamment pour visualiser un tableau de comparaison des fonctionnalités.

Le client Azure Information Protection est pris en charge sur Windows uniquement. Pour classifier et protéger des documents et des e-mails sur iOS, Android, macOS et le Web, utilisez des [applications Office qui prennent en charge l’étiquetage intégré](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Où puis-je trouver des informations sur l’utilisation des étiquettes de sensibilité pour les applications Office ?

Consultez les ressources de documentation suivantes :

- [En savoir plus sur les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) 

- [Utiliser des étiquettes de sensibilité dans les applications Office](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)

- [Activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Appliquer des étiquettes de sensibilité à vos documents et e-mails au sein d’Office](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

Pour plus d’informations sur les autres scénarios qui prennent en charge les étiquettes de sensibilité, consultez [scénarios courants pour les étiquettes de sensibilité](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels).

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Toutefois, si les utilisateurs sélectionnent une sous-étiquette, cela revient à appliquer deux étiquettes à la fois : une étiquette principale et une étiquette secondaire. Les sous-étiquettes permettent d’attribuer à un fichier deux classifications avec une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **confidentiel** peut contenir des sous-étiquettes telles que **juridique** et **finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **confidentiel** elle-même ; une seule de ses sous-étiquettes, par exemple **légal**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Quand vous utilisez des sous-étiquettes, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Quand vous utilisez des sous-niveaux, configurez ces paramètres pour la sous-étiquette uniquement. Si vous configurez ces paramètres sur l’étiquette principale et sa sous-étiquette, ce sont les paramètres de la sous-étiquette qui sont prioritaires.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Comment empêcher une personne de supprimer ou de changer une étiquette ?

Bien qu’il existe un [paramètre de stratégie](configure-policy-settings.md) qui oblige les utilisateurs à indiquer la raison pour laquelle ils abaissent une étiquette de classification, supprime une étiquette ou suppriment la protection, ce paramètre n’empêche pas ces actions. Pour empêcher les utilisateurs de supprimer ou de changer une étiquette, le contenu doit déjà être protégé et les autorisations de protection ne doivent pas leur accorder le [droit d’utilisation](configure-usage-rights.md) Exportation ou Contrôle total. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

Pour plus d’informations sur ces métadonnées, consultez [Étiquettes d’information stockées dans des e-mails et des documents](configure-policy.md#label-information-stored-in-emails-and-documents).

Pour obtenir des exemples d’utilisation de ces métadonnées avec des règles de flux de messagerie Exchange Online, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>Peut-on créer un modèle de document qui inclut automatiquement la classification ?

Oui. Vous pouvez configurer une étiquette qui [applique un en-tête ou un pied de page comportant le nom d’étiquette](configure-policy-markings.md). Toutefois, si cela ne répond pas à vos besoins, pour le client Azure Information Protection (Classic) uniquement, vous pouvez créer un modèle de document avec la mise en forme de votre choix et ajouter la classification en tant que code de champ. 

Par exemple, vous pouvez avoir une table dans l’en-tête de votre document qui affiche la classification, ou utiliser une formulation spécifique pour une introduction faisant référence à la classification du document.

Pour ajouter ce code de champ dans votre document :

1. Étiquetez le document et enregistrez-le. Cette action crée de nouveaux champs de métadonnées que vous pouvez alors utiliser dans votre code de champ.

2. Dans le document, placez le curseur à l’endroit où vous souhaitez ajouter la classification de l’étiquette ; ensuite, dans l’onglet **Insérer**, sélectionnez **Texte** > **QuickPart** > **Champ**.

3. Dans la liste déroulante **Catégories** de la boîte de dialogue **Champ**, sélectionnez **Informations sur le document**. Ensuite, dans la liste déroulante **Noms de champs**, sélectionnez **DocProperty**.

4. Dans la liste déroulante **Propriété**, sélectionnez **Sensibilité**, puis **OK**.

La classification de l’étiquette actuelle s’affiche dans le document ; cette valeur est actualisée automatiquement à chaque fois que vous ouvrez le document ou que vous utilisez le modèle. Par conséquent, lorsque l’étiquette change, la classification qui s’affiche pour ce code de champ est automatiquement mise à jour dans le document.

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>Comment la classification des e-mails utilise-t-elle Azure Information Protection différente de la classification des messages Exchange ?

La classification des messages Exchange est une fonctionnalité plus ancienne qui peut classer les e-mails et est implémentée indépendamment des étiquettes de Azure Information Protection ou des étiquettes de sensibilité qui appliquent la classification.

Toutefois, vous pouvez intégrer cette fonctionnalité plus ancienne à des étiquettes, de sorte que lorsque les utilisateurs classifient un e-mail à l’aide d’Outlook sur le Web et en utilisant des applications de messagerie mobile, la classification des étiquettes et les marques d’étiquette correspondantes sont automatiquement ajoutées.

Vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec Outlook sur le web et les applications de messagerie mobile.

Notez qu’il n’est pas nécessaire de le faire si vous utilisez Outlook sur le Web avec Exchange Online, car cette combinaison prend en charge l’étiquetage intégré lorsque vous publiez des étiquettes de sensibilité à partir du centre de conformité d’Office 365 Security &, Microsoft 365 Security Center ou Microsoft Compliance Center.

Si vous ne pouvez pas utiliser l’étiquetage intégré avec Outlook sur le Web, consultez les étapes de configuration de cette solution de contournement : intégration de la [classification des messages Exchange avec Azure information protection pour une solution d’étiquetage des appareils mobiles](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution).
