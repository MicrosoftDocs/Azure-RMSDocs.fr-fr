---
title: Étiquetage et protection-Kit de développement logiciel (SDK) Microsoft Information Protection
description: Opérations du kit de développement logiciel Microsoft Information Protection.
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 2e18b9ae65a4915807fdcb8fc37dd18396270fee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865008"
---
# <a name="labeling-and-pre-existing-protection-in-microsoft-information-protection-sdk"></a>Étiquetage et protection préexistante dans le kit de développement logiciel (SDK) Microsoft Information Protection

Microsoft Information Protection prend en charge les services d’étiquetage et de classification. Les utilisateurs et les applications peuvent appliquer les éléments suivants aux fichiers pris en charge :

- Classification uniquement par le biais de l’application d’une étiquette

- Classification et protection par le biais de l’application d’une étiquette

- Protection uniquement

Cet article explique comment le kit de développement logiciel (SDK) gère la tentative d’application d’une étiquette à un fichier qui dispose d’une protection préexistante. Lorsque le document dispose d’une protection préexistante par le biais de l’application d’une étiquette ou autre, le kit de développement logiciel (SDK) gère l’application d’une nouvelle étiquette dans les scénarios comme indiqué ci-dessous.

## <a name="label-based-protection-when-label-metadata-has-been-stripped"></a>Protection basée sur les étiquettes quand les métadonnées d’étiquette ont été supprimées

Si une étiquette est appliquée à un fichier et que l’étiquette a été appliquée, le kit de développement logiciel (SDK) doit être en mesure de résoudre cette protection de fichier en étiquette spécifique. Si un utilisateur disposant des autorisations « modifier » sur le fichier, supprime les métadonnées d’étiquette de manière accidentelle ou malveillante, la protection reste toujours. Lorsque le kit de développement logiciel (SDK) suivant interagit avec le fichier, il examine les données de protection, résout ce modèle de protection en étiquette d’origine et réapplique l’étiquette. Il s’agit d’un mécanisme de sécurité intégré au kit de développement logiciel (SDK) pour la protection des informations en cas de falsification des métadonnées d’étiquette.

## <a name="custom-protection-and-label-applications"></a>Applications de protection personnalisée et d’étiquette

Si le fichier a une certaine forme de protection appliquée, par le biais d’un modèle RMS et que l’utilisateur tente d’appliquer une étiquette au fichier, le kit de développement logiciel (SDK) doit tout d’abord être en mesure de résoudre la protection d’origine en étiquette. Si ce n’est pas possible, le kit de développement logiciel (SDK) ne sera pas en mesure de déterminer si le nouveau niveau de sensibilité de protection est plus restrictif ou permissif que le niveau de protection d’origine et, par conséquent, le kit de développement logiciel (SDK) n’appliquera pas la nouvelle étiquette au fichier.

## <a name="user-defined-permissions"></a>Autorisations définies par l’utilisateur

Si une étiquette est appliquée à un fichier et que l’étiquette a appliqué la protection définie par l’utilisateur, la protection est appliquée au fichier, mais il n’existe aucun moyen pour le kit de développement logiciel (SDK) de le résoudre en un modèle RMS. Dans ce cas, lorsqu’un utilisateur tente d’appliquer une nouvelle étiquette au fichier, le kit de développement logiciel (SDK) traite l’action comme indiqué ci-dessus et n’applique pas la nouvelle étiquette au fichier.
