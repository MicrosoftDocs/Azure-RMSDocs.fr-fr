---
title: Prise en main | Azure RMS
description: "La plateforme RMS SDK 2.1 permet aux développeurs de créer des applications qui tirent parti de la protection des informations RMS."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 728113C9-FCF9-4280-BE1D-6AF5C15E449E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 577f9813203f7bb7be4b5a7fd489dfba8d7fd33f


---
# <a name="getting-started"></a>Mise en route

La plateforme de Rights Management Services SDK 2.1 permet aux développeurs de créer des applications qui tirent parti de la protection des informations par le biais d’un serveur RMS ou d’Azure RMS. La plateforme gère des pratiques de sécurité complexes, comme la gestion des clés, et le traitement du chiffrement et du déchiffrement. Elle offre une API simplifiée pour le développement d’applications.

## <a name="get-started-with-rms-sdk-21"></a>Prise en main de RMS SDK 2.1

Cette rubrique vous guide tout au long du processus de configuration et d’exécution de votre application avec gestion des droits dans un environnement de test. Les rubriques suivantes expliquent comment configurer votre environnement de développement. L’ordre dans lequel elles sont répertoriées suggère l’ordre dans lequel vous pouvez effectuer les tâches.

## <a name="in-this-sections"></a>Dans cette section

| Rubrique | Description |
|-------|-------------|
| [Notes de publication](release-notes-rtm.md) | Cette rubrique contient des informations importantes sur cette version du Kit RMS SDK 2.1 et sur les versions précédentes.|
| [Installer le SDK](install-the-rms-sdk.md) | Cette rubrique vous guide tout au long de l’installation des outils de développement.|
| [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) | Cette rubrique contient des instructions sur la configuration d’un projet Visual Studio en vue d’utiliser RMS SDK 2.1.|
| [Développement de votre application](developing-your-application.md) | Cette rubrique contient des conseils essentiels liés aux principaux aspects d’une application compatible RMS. Vous pouvez vous appuyer sur ces conseils pour développer votre propre application.|
| [Test de votre application](how-to-set-up-your-test-environment.md) |Cette rubrique contient des instructions sur la configuration de test de votre application.|
| [Déployer en production](deploying-your-application.md) |Cette rubrique décrit les options de déploiement pour votre application avec gestion des droits.|


Essayez d’utiliser RMS SDK 2.1 en suivant les instructions des rubriques suivantes :

- [Installer le SDK](install-the-rms-sdk.md)
- [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
- [Développement de votre application](developing-your-application.md)
- [Test de votre application](how-to-set-up-your-test-environment.md)
- [Déployer en production](deploying-your-application.md)

### <a name="why-use-rms-sdk-21-for-protecting-your-content"></a>Pourquoi utiliser RMS SDK 2.1 pour protéger votre contenu ?

Pour les développeurs qui veulent ajouter la prise en charge de RMS à leurs applications nouvelles et existantes, RMS SDK 2.1 facilite :

-   La création d’applications RMS gérables, conformes et robustes.
-   Le chiffrement persistant des données utilisateur. Les données restent chiffrées, quel que soit l’environnement, l’appareil ou le système d’exploitation.
-   L’application d’un ensemble étendu de restrictions d’utilisation, comme l’impossibilité d’effectuer des captures d’écran de vos données sensibles.
-   La prise en charge de stratégies de protection gérées par l’entreprise.
-   La prise en charge de nouveaux mécanismes d’authentification et algorithmes de chiffrement dès qu’ils sont disponibles.

RMS SDK 2.1 prend en charge plusieurs plateformes client et serveur importantes. Pour plus d’informations, consultez [Plateformes](supported-platforms.md) prises en charge.

## <a name="core-principles"></a>Principes de base

**Simplicité** : Les commentaires et les modèles d’utilisation pour AD RMS SDK 1.0 ont été analysés, et ces données ont été utilisées pour simplifier ou automatiser les tâches de programmation les plus difficiles. Les applications RMS créées avec RMS SDK 2.1 nécessitent généralement 5 à 10 fois moins de lignes de code RMS que les applications RMS écrites avec AD RMS SDK 1.0.
**Écrire une seule fois** : Les applications RMS SDK 2.1 ne nécessitent pas de modification du code ni de recompilation pour utiliser les dernières fonctionnalités RMS. Les nouvelles fonctionnalités RMS sont disponibles dans votre application existante dès qu’elles sont ajoutées au serveur RMS.
**Cohérence** : RMS SDK 2.1 facilite l’écriture des applications qui respectent les différentes configurations de RMS. Il réduit également sensiblement la quantité d’interface utilisateur RMS que vous devez créer en tant que développeur d’applications, en encourageant une apparence cohérente et en réduisant la nécessité de former les utilisateurs.

## <a name="related-topics"></a>Rubriques connexes

* [Guide du développeur RMS](developers-guide.md)
* [AD RMS Developer’s Corner](http://blogs.msdn.com/b/rms/)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


