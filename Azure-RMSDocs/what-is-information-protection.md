---
title: Qu’est-ce qu’Azure Information Protection (AIP) ?
description: Azure Information Protection (AIP) étend l’infrastructure Microsoft Information Protection (MIP) pour étendre les fonctionnalités d’étiquetage et de classification fournies par Microsoft 365.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to extend Microsoft 365's labeling and classification functionality to the File Explorer, PowerShell, third party apps and services, and more.
ms.custom: contperf-fy21q2
search.appverid:
- MET150
ms.openlocfilehash: d1316fb289c39766b956931758da438b722f018d
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415311"
---
# <a name="what-is-azure-information-protection"></a>Qu’est-ce qu’Azure Information Protection ?

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection (AIP) est une solution cloud qui permet aux organisations de découvrir, de classifier et de protéger leurs documents et leurs e-mails en appliquant des étiquettes au contenu.

AIP fait partie de la solution Microsoft Information Protection (MIP) et étend les fonctionnalités d’[étiquetage](/microsoft-365/compliance/sensitivity-labels) et de [classification](/microsoft-365/compliance/data-classification-overview) fournies par Microsoft 365.

L’illustration suivante montre ce qu’ajoute Azure Information Protection à la protection MIP, notamment le [**client d’étiquetage unifié**](#aip-unified-labeling-client), le [**scanneur**](#aip-on-premises-scanner) et le kit [**SDK**](#microsoft-information-protection-sdk).

:::image type="content" source="media/what-is-mip.png" alt-text="Zones Azure Information Protection de la structure Microsoft Information Protection":::

Microsoft Information Protection est la structure de protection des informations commune qui est exploitée par le client d’étiquetage unifié d’AIP. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/protect-information).

> [!NOTE]
> Pour plus d’informations sur les fonctionnalités les plus récentes et la préversion publique du client d’étiquetage unifié, consultez [Client d’étiquetage unifié Azure Information Protection - Historique des versions et politique de support](rms-client/unifiedlabelingclient-version-release-history.md).
> 
## <a name="aip-unified-labeling-client"></a>Client d’étiquetage unifié AIP

Le client d’étiquetage unifié Azure Information Protection étend les fonctionnalités d’étiquetage, de classification et de protection à des types de fichiers supplémentaires, ainsi qu’à l’Explorateur de fichiers et à PowerShell. 

Par exemple, dans l’Explorateur de fichiers, cliquez avec le bouton droit sur un ou plusieurs fichiers et sélectionnez **Classer et protéger** pour gérer la fonctionnalité AIP sur les fichiers sélectionnés.

:::image type="content" source="media/protect-from-file-explorer.png" alt-text="Classer et protéger à partir de l’Explorateur de fichiers":::


Téléchargez le client depuis la [page de téléchargement de Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018).
    
## <a name="aip-on-premises-scanner"></a>Scanneur local AIP

L’analyseur local Azure Information Protection permet aux administrateurs d’analyser leurs référentiels de fichiers locaux à la recherche de contenu sensible à étiqueter, à classer ou à protéger.

Le scanneur local est installé via des applets de commande PowerShell fournies dans le cadre du client d’étiquetage unifié, et peut être géré en utilisant PowerShell et la zone Azure Information Protection dans le portail Azure.

Par exemple, utilisez les données du scanneur montrées dans le portail Azure pour rechercher les référentiels sur votre réseau pouvant avoir un contenu sensible à risque :

:::image type="content" source="media/risky-repos-small.png" alt-text="Rechercher les référentiels à risque dans les réseaux analysés" lightbox="media/risky-repos.png":::

Pour plus d’informations, consultez :

- [Qu’est-ce que le scanneur d’étiquetage unifié AIP ?](deploy-aip-scanner.md)
- Les sections « Scanneur » de [Client d’étiquetage unifié AIP- Historique des versions](rms-client/unifiedlabelingclient-version-release-history.md)

Téléchargez l’installation du scanneur en même temps que le client depuis la [page de téléchargement de Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018).


## <a name="microsoft-information-protection-sdk"></a>Kit SDK Microsoft Information Protection

Le SDK Microsoft Information Protection étend les étiquettes de sensibilité aux applications et services tiers. Les développeurs peuvent utiliser le kit SDK pour générer une prise en charge intégrée afin d’appliquer des étiquettes et une protection aux fichiers.

Par exemple, vous pouvez utiliser le SDK MIP pour :

- Application métier qui applique des étiquettes de classification aux fichiers lors de l’exportation.
- Application d’une conception CAO/FAO qui assure une prise en charge intégrée de l’étiquetage Microsoft Information Protection.
- Répartiteur de sécurité d’accès cloud (CASB) ou solution de protection contre la perte de données sécurité qui réfléchit aux données chiffrées avec Azure Information Protection.

Pour plus d’informations, consultez la [Vue d’ensemble du SDK Microsoft Information Protection](/information-protection/develop/overview).

## <a name="next-steps"></a>Étapes suivantes

**Pour commencer à utiliser AIP**, téléchargez et installez le client d’étiquetage unifié et le scanneur.

- [S’inscrire pour un essai gratuit](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)  (Enterprise Mobility + Security E5)
- [Télécharger le client](https://www.microsoft.com/download/details.aspx?id=53018)
- [Démarrage rapide : Déployer le client d’étiquetage unifié](quickstart-deploy-client.md)

**Familiarisez-vous avec AIP** avec nos premiers tutoriels :

- [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection](tutorial-install-scanner.md)
- [Tutoriel : Recherche de votre contenu sensible avec le scanneur Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Tutoriel : Empêcher les partages inappropriés dans Outlook avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)

**Quand vous êtes prêt à personnaliser davantage AIP**, consultez [Guide d’administration : Configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).

**Pour bien démarrer avec le kit SDK MIP**, consultez [Installation et configuration du kit SDK Microsoft Information Protection (MIP)](/information-protection/develop/setup-configure-mip).

### <a name="additional-resources"></a>Ressources supplémentaires

|Ressource  |Liens et description  |
|---------|---------|
|**Options d’abonnement et tarifs**     |    [Tarification d’Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)     |
|**Questions fréquentes (FAQ) et problèmes connus**     | [Forum aux questions sur Azure Information Protection](faqs.md) </br> [Problèmes connus - Azure Information Protection](known-issues.md)       |
|**Options de support**     | [Options de support pour Azure Information Protection](information-support.md)        |
|**Yammer**     |  [Azure Information Protection](https://www.yammer.com/AskIPTeam)       |
|**Nouveautés**     | Découvrez les nouvelles fonctionnalités liées à AIP dans les Centres d’administration Microsoft 365 et SharePoint :   </br>- [Nouveautés du Centre d’administration Microsoft 365](/microsoft-365/admin/whats-new-in-preview) </br>- [Nouveautés du Centre d’administration SharePoint](/sharepoint/what-s-new-in-admin-center)     |
|     |         |

#### <a name="top-ignite-sessions"></a>Principales sessions Ignite

Consultez les sessions Ignite 2020 enregistrées suivantes :

- [Supercharge information protection and governance across cloud, on-premise, endpoints and remote work environments](https://myignite.microsoft.com/sessions/ceba117f-9bc7-4426-9ebc-753d94c6a476) (Optimiser la protection des informations et la gouvernance dans le cloud, localement, sur les points de terminaison et dans les environnements de travail à distance)

- [Be a risk management hero with intelligent data protection and compliance solutions](https://myignite.microsoft.com/sessions/9a1e2716-55f5-4c3e-8626-0cb77e60eb87)

- [Know your data, protect your data and prevent data loss with Microsoft Information Protection](https://myignite.microsoft.com/sessions/46ff69cf-2c8f-4e61-a923-f72f5740f02f) (Apprenez à connaître vos données, protégez vos données et prévenez la perte de données avec Microsoft Information Protection)

- [Ask the Expert: Ask anything about Microsoft Compliance: information protection & governance, insider risks, Compliance Management, and more](https://myignite.microsoft.com/sessions/5ce48b36-9827-4d60-8540-90546333063d) (Demandez à l’expert : Posez des questions sur la conformité Microsoft : protection des informations et gouvernance, risques internes, gestion de la conformité, et ainsi de suite)
## <a name="aips-classic-client"></a>Client classique d’AIP

Le client classique d’Azure Information Protection est la version antérieure d’AIP ; il permet aux administrateurs de gérer les étiquettes de classification directement dans le portail Azure.

Les étiquettes AIP gérées dans le portail Azure ne sont *pas* prises en charge par la plateforme d’étiquetage unifié : elles sont limitées à une utilisation avec le client et le scanneur Azure Information Protection, et avec Microsoft Cloud App Security. 

Nous vous recommandons de migrer vers l’étiquetage unifié pour prendre en charge ces fonctionnalités, ainsi que SharePoint, les applications Microsoft 365, Outlook pour le web et les appareils mobiles, la protection des données Power BI, etc. Pour plus d’informations, consultez [Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié](tutorial-migrating-to-ul.md).

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. 
>
> Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à l’étiquetage unifié en utilisant la solution d’étiquetage unifié de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
