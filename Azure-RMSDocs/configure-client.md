---
title: Client Azure Information Protection- Installer et configurer
description: Informations destinées aux administrateurs sur le déploiement du client Azure Information Protection sur les ordinateurs et appareils mobiles Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79d4dbb1d6339f0261d57b32cf77addee9ca9744
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180339"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection : Installation et configuration pour les clients

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les ordinateurs qui exécutent Office 2010 exigent que le client Azure Information Protection s’authentifie auprès du service Azure Rights Management et le service Azure Information Protection. Ce client est également recommandé pour tous les ordinateurs Windows et les appareils iOS et Android qui prennent en charge le service Azure Rights Management et Azure Information Protection. 

Le client Azure Information Protection s’intègre aux applications Office grâce à l’installation d’un complément Office, afin de permettre aux utilisateurs d’étiqueter et de protéger facilement des documents et des e-mails directement depuis le ruban Office. Ce client offre également un étiquetage et une protection pour les types de fichiers qui ne sont pas pris en charge de manière native par le service Azure Rights Management, une visionneuse de fichiers protégés et un site de suivi de documents permettant aux utilisateurs de suivre et de révoquer les fichiers qu’ils ont protégés.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Client Azure Information Protection pour Windows : Installation et configuration

Pour une installation et une configuration du client en entreprise pour Windows, consultez le [Guide de l’administrateur Azure Information Protection](./rms-client/client-admin-guide.md).

> [!TIP]
> Si vous souhaitez installer et tester rapidement le client Azure Information Protection pour un seul ordinateur, consultez [Télécharger et installer le client Azure Information Protection](./rms-client/install-client-app.md) à partir du [Guide de l’utilisateur du client Azure Information Protection](./rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>Client Azure Information Protection pour iOS et Android : Installation et gestion

Pour installer le client Azure Information Protection pour ces plateformes mobiles populaires, vous pouvez télécharger l’application correspondante à l’aide des liens de la [page Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970). Aucune action de configuration n'est requise.

> [!NOTE]
> Pour les ordinateurs Mac, les liens de cette page téléchargent l’application de partage RMS. Ces ordinateurs ne prennent pas en charge le client Azure Information Protection.

### <a name="integration-with-intune"></a>Intégration à Intune

Comme l’application Azure Information Protection utilise le kit de développement logiciel (SDK) d’application Microsoft Intune, lorsque des appareils iOS et Android sont inscrits par Intune, vous pouvez déployer et gérer l’application Azure Information Protection pour ces appareils :

1. [Ajouter l’application Azure Information Protection à Intune](/intune/apps-add) 

2. Effectuez l’une des actions suivantes, ou les deux :
    
    - Déployer l’application en [l’assignant à des utilisateurs](/intune/apps-deploy)
    
    - Gérer l’application en utilisant des [stratégies de protection des applications](/intune/app-protection-policies)

Informations supplémentaires quand vous ajoutez l’application Azure Information Protection à Intune :

- Pour iOS : Recherchez et ajoutez l’application à partir d’Intune.

- Pour Android : Lorsque vous ajoutez l’application, utilisez l’**URL de l’Appstore** suivante :
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

Quand l’application Azure Information Protection est configurée pour une stratégie de protection d’application pour les appareils Android, en plus d’ouvrir le texte, les images et les documents PDF protégés, elle peut aussi ouvrir des fichiers audio et vidéo. Pour plus d’informations, consultez [Afficher des fichiers multimédias avec l’application Azure Information Protection](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Étapes suivantes

Après avoir installé et configuré le client Azure Information Protection, vous devrez peut-être en savoir plus sur la façon dont le client interprète les différents droits d’utilisation pouvant être utilisés pour protéger les documents et les e-mails. Pour plus d’informations, consultez [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md).
