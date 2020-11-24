---
title: 'Comment : activer la journalisation des erreurs et des performances | Azure RMS'
description: Le SDK Microsoft Rights Management 4.2 gère le chargement des journaux de diagnostic et de performances par le biais d’une propriété d’appareil unique.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 4a9a0029cbf9d3d171b24fc7a20a146a4646f799
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95567954"
---
# <a name="how-to-enable-error-and-performance-logging"></a>Comment : activer la journalisation des erreurs et des performances
Le SDK Microsoft Rights Management 4.2 gère le chargement des journaux de diagnostic et de performances par le biais d’une propriété d’appareil unique.

## <a name="overview"></a>Vue d’ensemble ##
Vous pouvez améliorer l’expérience de vos utilisateurs et faciliter la résolution de leurs problèmes en activant le chargement automatique des données des journaux de diagnostic, de performances et de télémétrie vers Microsoft. 

> [!IMPORTANT] 
> Afin de respecter la confidentialité de l’utilisateur, en tant que développeur d’applications, vous devez lui demander son consentement avant d’activer la journalisation automatique.

> [!NOTE]
> À titre d’exemple, voici un message standard que Microsoft utilise pour la notification de journalisation : 
>
> *En activant la journalisation des erreurs et des performances, vous acceptez d’envoyer des données d’erreur et de performances à Microsoft.  Microsoft collectera les données d’erreur et de performances sur Internet (« Data »).  Microsoft utilise ces données pour fournir et améliorer la qualité, la sécurité et l’intégrité des produits et services Microsoft.  Par exemple, nous analysons les performances et la fiabilité, comme les fonctionnalités que vous utilisez, la rapidité de réponse des fonctionnalités, les performances de l’appareil, les interactions de l’interface utilisateur et les problèmes que vous rencontrez avec le produit.  Les données incluent également des informations sur la configuration de votre logiciel, comme le logiciel en cours d’exécution et l’adresse IP.*  

Vous allez gérer le contrôle de la journalisation via deux propriétés.

-   Activez la journalisation via la propriété **IpcCustomerExperienceDataCollectionEnabled**. Le paramètre est persistant entre les réinitialisations de l’appareil.
-   Contrôlez le niveau de journalisation via la propriété **IpcLogLevel** à l’aide des paramètres suivants.

    * 1 : Commentaires
    * 2 : Informations
    * 3 : Avertissement
    * 4 : Erreur
    * 5 : Critique

Dans chacun des exemples d’extraits de code suivants, l’application appelante peut définir ou interroger la propriété.

### <a name="android"></a>Android ###
Activer la journalisation automatique

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
SharedPreferences.Editor editor = preferences.edit();
editor.putBoolean("IpcCustomerExperienceDataCollectionEnabled", true);
editor.commit();
```

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

```java
SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);
```

## <a name="ios"></a>iOS ##
Activer la journalisation automatique

```objectivec
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setBool:FALSE forKey:@"IpcCustomerExperienceDataCollectionEnabled"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcCustomerExperienceDataCollectionEnabled"];
```

Définir le contrôle de niveau de journalisation

```java
NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
    [prefs setInteger:1 forKey:@"IpcLogLevel"];
    [[NSUserDefaults standardUserDefaults] synchronize];
```

Obtenir le paramètre de contrôle de niveau de journalisation

```java
[[NSUserDefaults standardUserDefaults] boolForKey:@"IpcLogLevel"];
```

## <a name="windows"></a>Windows ##
Activer la journalisation automatique

```cpp
CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;
```

Pour plus d’informations sur les paramètres facultatifs, consultez [CustomerExperienceOptions](/previous-versions/windows/desktop/msipcthin2/customerexperienceoptions).

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

```cpp
CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;
```

**Remarque** : Les extraits de code Windows ci-dessus sont en C++. Pour C\#, mettez à jour la syntaxe avec « . » à la place de « :: ».

**Linux / C++**  : Ce SDK présente une journalisation de base qui n’est pas aussi complète que celle des autres plateformes. Pour plus d’informations, consultez la section **Dépannage** de « README.md » dans [RMS SDK pour C++ portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).