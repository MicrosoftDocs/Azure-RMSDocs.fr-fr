---
title: "Présentation - RMS SDK 2.1 | Azure RMS"
description: "Rights Management Services (RMS) est une technologie de protection des informations qui vous aide à protéger les informations numériques contre les utilisations non autorisées."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 816d665314fb77931433e36420b54c3ab6f689b9


---

# <a name="overview"></a>Vue d'ensemble

Rights Management Services SDK 2.1 est une technologie de protection des informations qui vous aide à protéger les informations numériques contre toute utilisation non autorisée. Dans votre application avec gestion des droits, les propriétaires de contenu peuvent définir qui peut ouvrir, modifier, imprimer, transférer ou effectuer d’autres actions avec le contenu.

AD RMS est constitué de composants [serveur](ad-rms-server.md) et [client](ad-rms-client.md). Le serveur, qui s’exécute sur Azure ou Windows Server, se compose de plusieurs services web.

Le composant [client](ad-rms-client.md) peut être exécuté sur un système d’exploitation client ou serveur et il contient des fonctions qui permettent à une application de chiffrer et déchiffrer du contenu, de récupérer des modèles et des listes de révocation, d’acquérir des licences et des certificats auprès d’un serveur, ainsi que d’autres tâches liées à la gestion des droits.

Pour plus d’informations, voir [Types d’applications](application-types.md).

Voici quelques scénarios pour lesquels des applications basées sur Rights Management Services SDK 2.1 peuvent être utilisées.

-   Un cabinet juridique veut empêcher que les e-mails sensibles soient imprimés ou transférés.
-   Les développeurs de logiciels de conception et de fabrication assistées par ordinateur veulent limiter l’accès au module de dessin à un petit groupe d’utilisateurs de la division recherche sans exiger l’utilisation de mots de passe.
-   Les propriétaires d’un site web de conception graphique veulent utiliser une même licence permettant la consultation gratuite de copies basse résolution de leurs images, mais exigeant un paiement pour accéder aux versions haute résolution.
-   Les propriétaires d’une bibliothèque de documents en ligne veulent octroyer les droits d’afficher, d’imprimer ou de modifier des documents en fonction de l’identité de l’utilisateur.
-   Une entreprise veut publier des informations sensibles sur les employés sur un site web interne qui limite les droits de consultation et de modification à certains utilisateurs.

Pour plus d’informations sur le serveur AD RMS, sur le client AD RMS et sur leurs fonctionnalités, consultez le contenu TechNet concernant la [documentation d’AD RMS pour les professionnels de l’informatique](https://TechNet.Microsoft.Com/library/cc771234.aspx).

Les autres rubriques de cette section traitent de l’architecture RMS et ses implémentations.

## <a name="in-this-section"></a>Dans cette section

| Rubrique | Description |
|-------|-------------|
|[Client](ad-rms-client.md) |Cette rubrique décrit l’objectif et la fonction du client RMS 2.1. |
|[Serveur](ad-rms-server.md) | Cette rubrique décrit l’objectif et les fonctions du serveur RMS pour Azure et Windows Server.|


## <a name="related-topics"></a>Rubriques connexes

* [Concepts RMS](application-types.md)
* [Prise en main](getting-started-with-ad-rms-2-0.md)
* [Documentation d’AD RMS pour les professionnels de l’informatique](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
 

 



<!--HONumber=Nov16_HO2-->


