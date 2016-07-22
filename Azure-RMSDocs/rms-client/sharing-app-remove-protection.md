---
title: "Supprimer la protection d’un fichier à l’aide de l’application de partage Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 4aea0c89e5d97a7a0190962e073f0b4bc95bef25


---

# Suppression de la protection d'un fichier avec l'application de partage Rights Management

*S’applique à : Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*

Pour supprimer la protection d'un fichier (autrement dit, le dé-protéger) protégé à l'aide de l'application de partage RMS, utilisez l'option **Supprimer la Protection** de l'Explorateur de fichiers.

> [!IMPORTANT]
> Pour pouvoir supprimer la protection d'un fichier, vous devez être propriétaire de celui-ci.

## Pour supprimer la protection d'un fichier

1.  Dans l’Explorateur de fichiers, cliquez avec le bouton droit sur le fichier (par exemple, Sample.ptxt), sélectionnez **Protéger avec RMS**, **Protéger sur place**, puis cliquez sur **Supprimer la protection** :

    ![Option de menu Supprimer la protection de l’application de partage RMS](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Il se peut que vous soyez invité à fournir vos informations d'identification.

Remarque : Si vous ne voyez pas ces options, l’application de partage RMS n’est peut-être pas installée sur votre ordinateur, la version la plus récente n’est peut-être pas installée ou votre ordinateur doit peut-être être redémarré pour terminer l’installation. Pour plus d’informations sur l’installation de l’application de partage, voir [Télécharger et installer l’application de partage Rights Management](install-sharing-app.md).

Le fichier protégé d'origine (par exemple, Sample.ptxt) est supprimé et remplacé par un fichier du même nom, mais avec l'extension de nom de fichier non protégé (par exemple, Sample.txt).

## Exemples et autres instructions
Pour obtenir des exemples et des instructions concernant l’utilisation de l’application de partage Rights Management, voir les sections suivantes dans le Guide d’utilisation de l’application de partage Rights Management :

-   [Exemples d’utilisation de l’application de partage RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Que souhaitez-vous faire ?](sharing-app-user-guide.md#what-do-you-want-to-do)

## Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)



<!--HONumber=Jul16_HO3-->


