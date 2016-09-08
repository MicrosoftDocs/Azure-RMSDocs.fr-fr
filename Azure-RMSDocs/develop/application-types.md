---
title: "Types d’applications | Azure RMS"
description: "Cette rubrique traite des types d’applications que vous pouvez choisir de créer avec une gestion des droits."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: b22ba1fc4c4599ec2ee47ce39049377a742f0c55


---

# Application types (Types d’applications)


Cette rubrique traite des types d’applications que vous pouvez choisir de créer avec une gestion des droits.

Les types d’application suivants sont actuellement pris en charge par Rights Management Services SDK 2.1

## Applications simples

Une application simple peut être un outil de ligne de commande conçu pour chiffrer un fichier donné. Pour obtenir un exemple d’application simple avec gestion des droits, consultez [IPCHelloWorld : un exemple d’application](how-to-build-your-first-application.md).

### Applications en mode serveur

Le *mode serveur* est conçu pour les applications non interactives qui consomment, protègent ou traitent du contenu protégé par RMS. Un exemple est une application de *protection contre la perte de données* qui s’exécute en tant que service sur un serveur de fichiers et qui protège automatiquement les documents sensibles. Consultez l’[exemple IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d) pour un exemple de ce type d’application.

Si votre application utilise le *mode serveur*, elle doit s’authentifier auprès du serveur RMS en mode silencieux. Contrairement au *mode client*, RMS SDK 2.1 n’ouvre pas une invite demandant des informations d’identification quand il échoue à s’authentifier en mode silencieux. En outre, lors de l’exécution en *mode serveur*, un manifeste d’application n’est pas nécessaire.

Pour plus d’informations sur la définition du mode de sécurité de l’API, consultez [Définition du mode de sécurité de l’API](setting-the-api-security-mode-api-mode.md).

### Applications clientes enrichies

Une application cliente enrichie permet aux utilisateurs d’afficher et de manipuler des données via une interface utilisateur graphique. Souvent, les données présentées dans cette interface utilisateur sont importantes et sensibles au vol ou à une exposition accidentelle. La prise en charge de la protection des informations améliore généralement les scénarios existants, mais elle n’est pas l’objectif principal du développement de l’application.

L’utilisation de RMS SDK 2.1 avec des applications clientes enrichies vous aide à :

-   Vérifier que ces données sont toujours chiffrées.

-   Empêcher les utilisateurs d’extraire des données à un format non protégé (par exemple pour empêcher l’utilisation du Presse-papiers pour copier et coller).

Microsoft Notepad est une application cliente enrichie simple. Microsoft Office est une application cliente enrichie plus complexe.

Pour plus d’informations sur la protection de votre application, consultez [Comprendre les restrictions d’utilisation](understanding-usage-restrictions.md).

## Rubriques connexes

* [Exemple IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [Exemple d’application IPCHelloWorld](how-to-build-your-first-application.md)
* [Définition du mode de sécurité de l’API](setting-the-api-security-mode-api-mode.md)
* [Comprendre les restrictions d’utilisation](understanding-usage-restrictions.md)



<!--HONumber=Aug16_HO4-->


