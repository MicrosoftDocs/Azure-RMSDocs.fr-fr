---
# required metadata

title: Vue d’ensemble | Azure RMS
description: Rights Management Services (RMS) est une technologie de protection des informations qui vous aide à protéger les informations numériques contre les utilisations non autorisées.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a58894d5-3271-46d7-bb1c-fbd22eae8530

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Vue d'ensemble

Rights Management Services (RMS) est une technologie de protection des informations qui vous aide à protéger les informations numériques contre les utilisations non autorisées. Dans votre application avec gestion des droits, les propriétaires de contenu peuvent définir qui peut ouvrir, modifier, imprimer, transférer ou effectuer d’autres actions avec le contenu.

## Vue d'ensemble

AD RMS est constitué de composants [serveur](ad-rms-server.md) et [client](ad-rms-client.md). Les composants serveur comprennent plusieurs services web qui s’exécutent sur un serveur Windows Server, comme Windows Server 2008 R2, ou via le cloud à travers des services web RMS dans Azure. Le composant client peut être exécuté sur un système d’exploitation client ou serveur, et il contient des fonctions qui permettent à une application de chiffrer et déchiffrer du contenu, de récupérer des modèles et des listes de révocation, d’acquérir des licences et des certificats auprès d’un serveur, ainsi que d’autres tâches liées à la gestion des droits.

Pour plus d’informations, consultez [Types d’applications](application-types.md).

Voici quelques scénarios pour lesquels des applications basées sur Rights Management Services SDK 2.1 peuvent être utilisées.

-   Un cabinet juridique veut empêcher que les e-mails sensibles soient imprimés ou transférés.
-   Les développeurs de logiciels de conception et de fabrication assistées par ordinateur veulent limiter l’accès au module de dessin à un petit groupe d’utilisateurs de la division recherche sans exiger l’utilisation de mots de passe.
-   Les propriétaires d’un site web de conception graphique veulent utiliser une même licence permettant la consultation gratuite de copies basse résolution de leurs images, mais exigeant un paiement pour accéder aux versions haute résolution.
-   Les propriétaires d’une bibliothèque de documents en ligne veulent octroyer les droits d’afficher, d’imprimer ou de modifier des documents en fonction de l’identité de l’utilisateur.
-   Une entreprise veut publier des informations sensibles sur les employés sur un site web interne qui limite les droits de consultation et de modification à certains utilisateurs.

Pour plus d’informations sur le serveur AD RMS, sur le client AD RMS et sur leurs fonctionnalités, consultez le contenu TechNet concernant la [documentation d’AD RMS pour les professionnels de l’informatique](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx).

Pour commencer, consultez [Prise en main](getting-started-with-ad-rms-2-0.md).

## Rubriques connexes

* [Concepts d’AD RMS](application-types.md)
* [Différences entre AD RMS et AD RMS 2.1](differences-between-ad-rms-and-ad-rms-2-0.md)
* [Prise en main](getting-started-with-ad-rms-2-0.md)
* [Documentation d’AD RMS pour les professionnels de l’informatique](https://TechNet.Microsoft.Com/en-us/library/cc771234.aspx)
* [serveur](ad-rms-server.md)
* [client](ad-rms-client.md)
 

 





<!--HONumber=Apr16_HO3-->


