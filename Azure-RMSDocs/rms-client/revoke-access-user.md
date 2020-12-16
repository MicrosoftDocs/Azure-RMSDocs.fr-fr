---
title: Révoquer l’accès au document-Azure Information Protection
description: Décrit comment les utilisateurs finaux peuvent utiliser le client AIP pour révoquer l’accès au document pour les documents qu’ils ont protégés.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: abb96719d51658226211653b4ab4d171fcaa6b2e
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97592743"
---
# <a name="user-guide-revoke-document-access-with-azure-information-protection-public-preview"></a>Guide de l’utilisateur : révoquer l’accès aux documents avec Azure Information Protection (version préliminaire publique)

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 *
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le Guide de l' [utilisateur : suivre et révoquer vos documents lorsque vous utilisez le client classique AIP](client-track-revoke.md). *

Cet article explique comment révoquer l’accès pour les documents que vous avez protégés de Microsoft Office.

Révoquer l’accès d’un document protégé empêche les autres utilisateurs d’accéder au document, même si vous leur avez donné un accès auparavant. Pour plus d’informations, consultez [le Guide de l’utilisateur : classifier et protéger avec le client d’étiquetage unifié Azure information protection](clientv2-classify-protect.md).

Les fonctionnalités Track et REVOKE du client d’étiquetage unifié sont actuellement en version préliminaire. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale. 

## <a name="revoke-access-from-microsoft-office-apps"></a>Révoquer l’accès à partir des applications Microsoft Office

Pour révoquer l’accès à partir de Word, Excel ou PowerPoint :

1. Ouvrez le fichier protégé dont vous souhaitez révoquer l’accès. Il doit s’agir d’un fichier dans lequel *vous* avez appliqué la protection, à l’aide de votre compte d’utilisateur *actuel* .

    > [!TIP]
    > Si vous n’avez appliqué qu’une étiquette et une protection, vous ne pouvez pas révoquer l’accès dans la même session. Rouvrez le document si vous devez révoquer l’accès.

1. Dans l’onglet dossier de **démarrage** , cliquez sur le bouton **sensibilité** et sélectionnez **révoquer l’accès**:

    :::image type="content" source="../media/track-revoke-word.png" alt-text="Sélectionnez révoquer l’accès à partir de Microsoft Word":::

    > [!NOTE]
    > Vous ne voyez pas cette option ? Pour plus d’informations, consultez les scénarios possibles [ci-dessous](#dont-see-the-revoke-access-option).
    >
 
1. Dans le message de confirmation qui s’affiche, cliquez sur **Oui** pour continuer.

L’accès est révoqué et les autres utilisateurs ne peuvent plus accéder au document.

### <a name="dont-see-the-revoke-access-option"></a>Vous ne voyez pas l’option révoquer l’accès ?

Si vous ne voyez pas l’option permettant de **révoquer l’accès** dans le menu **sensibilité** , vous pouvez avoir l’un des scénarios suivants :

- Vous avez peut-être appliqué la protection dans cette session. Si c’est le cas, fermez et rouvrez le document pour réessayer.

- Vous pouvez consulter un document non protégé. La révocation de l’accès ne s’applique qu’aux documents protégés.

- La dernière version du client d’étiquetage unifiée AIP n’est peut-être pas installée, ou vous devrez peut-être redémarrer vos applications ou ordinateurs Office après l’installation. 

    Pour plus d’informations, consultez [le Guide de l’utilisateur : Télécharger et installer le client Azure information protection](install-client-app.md).

## <a name="revoking-access-where-the-document-protection-has-been-changed-on-a-copy"></a>Révocation de l’accès lorsque la protection de document a été modifiée sur une copie

Si un autre utilisateur a modifié l’étiquette ou la protection sur une copie du document, l’accès n’est *pas révoqué* sur cette copie du document. 

En effet, le suivi et la révocation de l’accès s’effectuent à l’aide d’une valeur ContentID unique, qui change chaque fois que la protection est modifiée.

> [!IMPORTANT]
> Si vous pensez qu’un utilisateur a peut-être modifié l’étiquette ou le niveau de protection d’un document et que vous devez révoquer l’accès, contactez un administrateur système pour vous aider à révoquer l’accès à cette copie du document.
> 
## <a name="next-steps"></a>Étapes suivantes

Pour plus d'informations, consultez les pages suivantes :

- [Guide de l’utilisateur du client d’étiquetage unifié AIP](clientv2-user-guide.md)
- [Guide de l’administrateur du client d’étiquetage unifié AIP](clientv2-admin-guide.md)
- [Problèmes connus pour le suivi et la révocation de l’accès aux documents](../known-issues.md#tracking-and-revoking-document-access-public-preview)