---
title: Client Azure Information Protection- Installer et configurer
description: Informations destinées aux administrateurs sur le déploiement des clients Azure Information Protection sur des ordinateurs Windows et des appareils mobiles.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2da5d348f497a74e88c0bf11da023be6e3cb0152
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583538"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection : installation et configuration pour les clients

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Le client d’étiquetage unifié AIP est recommandé pour tous les ordinateurs Windows, car il installe un complément Office qui permet aux utilisateurs d’étiqueter et de protéger facilement des documents directement à partir du ruban Office. 

Le client offre également les éléments suivants :

- Étiquetage et protection des types de fichiers qui ne sont pas pris en charge par le service de protection intégré (Azure Rights Management).
- Visionneuse pour les fichiers protégés qui ne peuvent pas être ouverts par les applications Office. Il existe une visionneuse similaire pour iOS et Android.
- Fonctionnalités de suivi et de révocation de l’accès aux fichiers protégés.

Les ordinateurs qui exécutent Office 2010 requièrent le client Azure Information Protection pour s’authentifier auprès du service Azure Information Protection. Pour plus d’informations, consultez [AIP pour Windows et les versions d’Office dans support étendu](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).
## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Le client Azure Information Protection pour Windows : installation et configuration

Pour une installation et une configuration d’entreprise du client pour Windows, consultez le Guide de l' [administrateur du client d’étiquetage Azure information protection unifié](./rms-client/clientv2-admin-guide.md).

Si vous souhaitez installer et tester rapidement ces clients pour un seul ordinateur, consultez [Télécharger et installer le client d’étiquetage unifié Azure information protection](./rms-client/install-unifiedlabelingclient-app.md).

**Client classique uniquement**: si le client Classic est installé, utilisez ces liens à la place :

- [Client Azure Information Protection - Guide de l’administrateur](./rms-client/client-admin-guide.md)
- [Téléchargez et installez le client Azure information protection](./rms-client/install-client-app.md).

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>L’application Azure Information Protection pour iOS et Android : installation et gestion

Pour installer la visionneuse d’applications Azure Information Protection pour iOS et Android, utilisez les liens de la [page Microsoft Azure information protection](https://go.microsoft.com/fwlink/?LinkId=303970). Aucune configuration n'est requise.

> [!NOTE]
> Pour les ordinateurs Mac, les liens de cette page téléchargent l’application de partage RMS. Ces ordinateurs ne prennent pas en charge le client Azure Information Protection.

### <a name="integration-with-intune"></a>Intégration à Intune

Étant donné que l’application Azure Information Protection Viewer utilise le kit de développement logiciel (SDK) d’application Microsoft Intune, lorsque des appareils iOS et Android sont inscrits par Intune, vous pouvez déployer et gérer l’application Azure Information Protection Viewer pour ces appareils :

1. [Ajouter l’application Azure Information Protection à Intune](/intune/apps/apps-add)

2. Effectuez l’une des actions suivantes, ou les deux :

    - Déployer l’application en [l’assignant à des utilisateurs](/intune/apps/apps-deploy)

    - Gérer l’application en utilisant des [stratégies de protection des applications](/intune/apps/app-protection-policies)

Informations supplémentaires quand vous ajoutez l’application Azure Information Protection à Intune :

- Pour iOS : recherchez et ajoutez l’application à partir d’Intune.

- Pour Android : quand vous ajoutez l’application, utilisez l' **URL AppStore** suivante :

    ```md
    https://play.google.com/store/apps/details?id=com.microsoft.ipviewer
    ```

Quand l’application Azure Information Protection est configurée pour une stratégie de protection d’application pour les appareils Android, en plus d’ouvrir le texte, les images et les documents PDF protégés, elle peut aussi ouvrir des fichiers audio et vidéo. Pour plus d’informations, consultez [Afficher des fichiers multimédias avec l’application Azure Information Protection](/intune/fundamentals/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez installé et configuré Azure Information Protection clients, vous devrez peut-être en savoir plus sur la façon dont le client interprète les différents droits d’utilisation qui peuvent être utilisés pour protéger des documents et des e-mails. Pour plus d’informations, consultez [Configuration des droits d’utilisation pour Azure Information Management](configure-usage-rights.md).
