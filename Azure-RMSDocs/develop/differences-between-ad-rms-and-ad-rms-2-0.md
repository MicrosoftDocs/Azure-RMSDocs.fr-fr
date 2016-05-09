---
# required metadata

title: Améliorations offertes par ce SDK | Azure RMS
description: Cette rubrique décrit comment RMS SDK 2.1 représente une amélioration significative par rapport au Kit Active Directory Rights Management Services SDK d’origine.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ee4989d6-3903-4ed2-ac62-d5692e2ef494

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
# Améliorations offertes par ce SDK
Cette rubrique décrit comment Rights Management Services SDK 2.1 constitue une amélioration significative par rapport au Kit [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) d’origine en termes d’effort de développement à fournir pour créer une application avec gestion des droits.

**Surface de l’API** - La surface de l’API a été considérablement réduite via l’abstraction, ce qui vous évite les nombreux détails d’une implémentation principale. Par rapport à une surface de l’API de 84 fonctions pour RMS SDK, RMS SDK 2.1 inclut uniquement 20 fonctions d’API. La plupart des applications doivent utiliser uniquement une petite partie de cette surface de l’API.

**Délai de prise en main** - Avec RMS SDK 2.1, vous pouvez suivre un guide pas à pas pour identifier les ressources de votre application qui sont sensibles et comment les protéger. Avec RMS SDK, vous deviez avoir des connaissances approfondies en matière de certificats, formats et topologies, et écrire du code complexe pour le multithreading.

**Prise en charge de plusieurs topologies** - RMS SDK 2.1 vous aide à limiter la réécriture du code ; votre application doit fonctionner avec toutes les topologies puisque nous avons réduit la complexité de la topologie pour le développeur. Avec RMS SDK, vous deviez comprendre toutes les topologies prises en charge, puis écrire et tester un code spécifique pour chacune.

**Extensibilité** - RMS SDK 2.1 vous aide à limiter la réécriture du code de gestion des droits ; votre application doit fonctionner dans n’importe quel environnement RMS et bénéficier automatiquement des nouvelles fonctionnalités lors de la publication de fonctionnalités RMS de base mises à jour. Avec AD RMS SDK, vous deviez mettre à jour votre application pour bénéficier de toute nouvelle fonctionnalité de façon explicite.

**Avis important**  
Toutes les rubriques du Kit [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) d’origine dans la bibliothèque MSDN commencent désormais par la déclaration de prise en charge suivante :

Le Kit AD RMS SDK tirant parti des fonctionnalités exposées par le client dans Msdrm.dll peut être utilisé avec Windows Server 2008, Windows Vista, Windows Server 2008 R2, Windows 7, Windows Server 2012 et Windows 8. Il sera peut-être modifié ou indisponible dans les versions ultérieures. Utilisez plutôt [Active Directory Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md) qui exploite les fonctionnalités exposées par le client dans *Msipc.dll*.

 

## Rubriques connexes ##
* [Vue d'ensemble](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Apr16_HO3-->


