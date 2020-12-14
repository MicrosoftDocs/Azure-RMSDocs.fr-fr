---
title: FAQ sur la classification et l’étiquetage - AIP
description: Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d4bfec07900404c39a17a90468a726f6632078fe
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382273"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour plus d’informations, consultez également [FAQ pour le client classique uniquement](faqs-classic.md). *

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>Quel client dois-je installer pour tester les nouvelles fonctionnalités ?

Nous vous recommandons d’installer le **client d’étiquetage unifié Azure information protection**. Le client d’étiquetage unifié télécharge des étiquettes et des paramètres de stratégie à partir de l’un des centres d’administration suivants : 

- Centre de sécurité et conformité Office 365
- Centre de sécurité Microsoft 365
- Centre de conformité Microsoft 365.

Ce client est désormais en disponibilité générale et peut disposer d’une préversion pour tester des fonctionnalités supplémentaires pour une version ultérieure.

Si vous avez toujours configuré des étiquettes dans le Portail Azure que vous n’avez pas encore [migré vers le magasin d’étiquetage unifié](configure-policy-migrate-labels.md), utilisez à la place le **client Azure information protection Classic** .

Pour plus d’informations, notamment un tableau comparatif des fonctionnalités et des fonctionnalités, consultez [choisir votre solution d’étiquetage Windows](rms-client/use-client.md#choose-your-windows-labeling-solution).

> [!TIP]
> Le client Azure Information Protection est pris en charge sur Windows uniquement. 
>
> Pour classifier et protéger des documents et des e-mails sur iOS, Android, macOS et le Web, utilisez des [applications Office qui prennent en charge l’étiquetage intégré](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). 
> 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Où puis-je trouver des informations sur l’utilisation des étiquettes de sensibilité pour les applications Office ?

Consultez les ressources de documentation suivantes :

- [En savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) 

- [Utiliser des étiquettes de sensibilité dans les applications Office](/microsoft-365/compliance/sensitivity-labels-office-apps)

- [Activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Appliquer des étiquettes de sensibilité à vos documents et e-mails au sein d’Office](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

Pour plus d’informations sur les autres scénarios qui prennent en charge les étiquettes de sensibilité, consultez [scénarios courants pour les étiquettes de sensibilité](/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels).

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Toutefois, si les utilisateurs sélectionnent une sous-étiquette, cela revient à appliquer deux étiquettes à la fois : une étiquette principale et une étiquette secondaire. Les sous-étiquettes permettent d’attribuer à un fichier deux classifications avec une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **confidentiel** peut contenir des sous-étiquettes telles que **juridique** et **finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **confidentiel** elle-même ; une seule de ses sous-étiquettes, par exemple **légal**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Quand vous utilisez des sous-étiquettes, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Quand vous utilisez des sous-niveaux, configurez ces paramètres pour la sous-étiquette uniquement. Si vous configurez ces paramètres sur l’étiquette principale et sa sous-étiquette, ce sont les paramètres de la sous-étiquette qui sont prioritaires.

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>Comment empêcher une personne de supprimer ou de changer une étiquette ?

Pour empêcher les utilisateurs de supprimer ou de changer une étiquette, le contenu doit déjà être protégé et les autorisations de protection ne doivent pas leur accorder le [droit d’utilisation](configure-usage-rights.md) Exportation ou Contrôle total. 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes Office.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

Pour obtenir des exemples d’utilisation de ces métadonnées avec des règles de flux de messagerie Exchange Online, consultez [Configuration des règles de flux de messagerie Exchange Online pour les étiquettes Azure Information Protection](configure-exo-rules.md).