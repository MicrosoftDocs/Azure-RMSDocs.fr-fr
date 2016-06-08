---
# required metadata

title: Notes du développeur | Azure RMS
description: Cette rubrique traite de recommandations propres à différents scénarios de développement importants. 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** Ce contenu de SDK n’est pas à jour. Vous trouverez temporairement la [version actuelle](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentation sur MSDN. **
# Notes du développeur

Cette section traite de recommandations propres à différents scénarios de développement importants. Les scénarios de cette section sont spécifiques à cette version de Rights Management Services SDK 2.1 et peuvent être modifiés dans les versions ultérieures.

- [Ajouter des droits de propriétaire explicites](add-explicit-owner-rights.md) - Votre application doit ajouter explicitement les droits &quot;Propriétaire&quot; lors de la création d’une licence à partir de rien ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)).
- [Conditions d’erreur courantes et solutions](common-error-conditions-and-solutions.md) - Cette rubrique répertorie les messages d’erreur les plus courants susceptibles de s’afficher quand vous utilisez les outils de développement de RMS SDK 2.1.
- [Activation des notifications par e-mail](how-to-enable-email-notification.md) - Les notifications par e-mail permettent à un propriétaire de contenu protégé d’être averti quand un utilisateur accède à son contenu.
- [Configuration de l’API de fichier](file-api-configuration.md) - Le comportement de l’API de fichier peut être configuré via des paramètres du Registre.
- [IPCHelloWorld : un exemple d’application](how-to-build-your-first-application.md) - Cette rubrique contient des instructions pour créer un exemple d’application avec gestion des droits.
- [Définition du mode de sécurité de l’API](setting-the-api-security-mode-api-mode.md) - Vous pouvez choisir le mode de sécurité qu’exécute votre application API de fichier à l’aide de la fonction [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).
- [Formats de fichier pris en charge](supported-file-formats.md) - L’API de fichier prend en charge les formats natif et Pfile.
- [Suivi du contenu](tracking-content.md) - Cette rubrique propose des conseils de base pour implémenter le suivi de documents sur du contenu protégé à l’aide de RMS SDK 2.1.
- [Utilisation du chiffrement](working-with-encryption.md) - Cette rubrique vous oriente vers nos offres de chiffrement et présente quelques extraits de code pour illustrer leur utilisation.

 

## Rubriques connexes ##
* [Vue d'ensemble](ad-rms-overview.md)
* [Utilisation de procédures](how-to-use-msipc.md)
 

 


<!--HONumber=Jun16_HO1-->


