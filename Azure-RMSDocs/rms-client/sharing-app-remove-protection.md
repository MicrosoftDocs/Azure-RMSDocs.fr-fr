---
title: Supprimer la protection d’un fichier via l’application de partage RMS - AIP
description: Instructions à suivre pour supprimer la protection d’un fichier protégé (autrement dit, pour le déprotéger) à l’aide de l’application de partage RMS.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.service: information-protection
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4f6491e63cf5eca1274ddc7727320dc739f4fe43
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42803427"
---
# <a name="remove-protection-from-a-file-by-using-the-rights-management-sharing-application"></a>Suppression de la protection d'un fichier avec l'application de partage Rights Management

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Pour supprimer la protection d'un fichier (autrement dit, le dé-protéger) protégé à l'aide de l'application de partage RMS, utilisez l'option **Supprimer la Protection** de l'Explorateur de fichiers.

> [!IMPORTANT]
> Pour pouvoir supprimer la protection d'un fichier, vous devez être propriétaire de celui-ci.

## <a name="to-remove-protection-from-a-file"></a>Pour supprimer la protection d'un fichier

1.  Dans l’Explorateur de fichiers, cliquez avec le bouton droit sur le fichier (par exemple, Sample.ptxt), sélectionnez **Protéger avec RMS**, **Protéger sur place**, puis cliquez sur **Supprimer la protection** :

    ![Option de menu Supprimer la protection de l’application de partage RMS](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Il se peut que vous soyez invité à fournir vos informations d'identification.

Remarque : Si vous ne voyez pas ces options, l’application de partage RMS n’est peut-être pas installée sur votre ordinateur, la version la plus récente n’est peut-être pas installée ou votre ordinateur doit peut-être être redémarré pour terminer l’installation. Pour plus d’informations sur l’installation de l’application de partage, consultez [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

Le fichier protégé d'origine (par exemple, Sample.ptxt) est supprimé et remplacé par un fichier du même nom, mais avec l'extension de nom de fichier non protégé (par exemple, Sample.txt).

## <a name="examples-and-other-instructions"></a>Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que voulez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)
