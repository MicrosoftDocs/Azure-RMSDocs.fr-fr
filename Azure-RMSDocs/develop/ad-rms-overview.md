---
title: Présentation - RMS SDK 2.1 | Azure RMS
description: Rights Management Services (RMS) est une technologie de protection des informations qui vous aide à protéger les informations numériques contre les utilisations non autorisées.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 001cace1cdc3a9fd3e5cc1dd1a06a77215bd438c
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95567978"
---
# <a name="overview-of-rights-management-services-sdk-21"></a>Présentation du kit de développement logiciel (SDK) Rights Management Services 2,1

Rights Management Services SDK 2.1 est une technologie de protection des informations qui vous aide à protéger les informations numériques contre toute utilisation non autorisée. Dans votre application avec gestion des droits, les propriétaires de contenu peuvent définir qui peut ouvrir, modifier, imprimer, transférer ou effectuer d’autres actions avec le contenu.

AD RMS est constitué de composants [serveur](ad-rms-server.md) et [client](ad-rms-client.md). Le serveur, qui s’exécute sur Azure ou Windows Server, se compose de plusieurs services web.

Le composant [client](ad-rms-client.md) peut être exécuté sur un système d’exploitation client ou serveur et il contient des fonctions qui permettent à une application de chiffrer et déchiffrer du contenu, de récupérer des modèles et des listes de révocation, d’acquérir des licences et des certificats auprès d’un serveur, ainsi que d’autres tâches liées à la gestion des droits.

Pour plus d’informations, consultez [types d’applications](application-types.md).

Voici quelques scénarios pour lesquels des applications basées sur le SDK Rights Management Services 2.1 peuvent être utilisées.

-   Un cabinet juridique veut empêcher que les e-mails sensibles soient imprimés ou transférés.
-   Les développeurs de logiciels de conception et de fabrication assistées par ordinateur veulent limiter l’accès au module de dessin à un petit groupe d’utilisateurs de la division Recherche sans exiger l’utilisation de mots de passe.
-   Les propriétaires d’un site web de conception graphique veulent utiliser une même licence permettant la consultation gratuite de copies basse résolution de leurs images, mais exigeant un paiement pour accéder aux versions haute résolution.
-   Les propriétaires d’une bibliothèque de documents en ligne veulent octroyer les droits d’afficher, d’imprimer ou de modifier des documents en fonction de l’identité de l’utilisateur.
-   Une entreprise veut publier des informations sensibles sur les employés sur un site web interne qui limite les droits de consultation et de modification à certains utilisateurs.

Pour plus d’informations sur le serveur AD RMS, sur le client AD RMS et sur leurs fonctionnalités, consultez le contenu TechNet concernant la [documentation d’AD RMS pour les professionnels de l’informatique](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771234(v=ws.10)).

Les autres rubriques de cette section traitent de l’architecture RMS et ses implémentations.

## <a name="in-this-section"></a>Contenu de cette section

| Rubrique | Description |
|-------|-------------|
|[Client](ad-rms-client.md) |Cette rubrique décrit l’objectif et la fonction du client RMS 2.1. |
|[Serveur](ad-rms-server.md) | Cette rubrique décrit l’objectif et les fonctions du serveur RMS pour Azure et Windows Server.|


## <a name="related-topics"></a>Rubriques connexes

* [Concepts RMS](application-types.md)
* [Prise en main](getting-started-with-ad-rms-2-0.md)
* [Documentation d’AD RMS pour les professionnels de l’informatique](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771234(v=ws.10))