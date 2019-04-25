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
ms.openlocfilehash: 93975ad0f2113fc10bff3f54f0b6729dfa33bad3
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178350"
---
# <a name="how-to-enable-error-and-performance-logging"></a>Procédure : activer la journalisation des erreurs et des performances
Le SDK Microsoft Rights Management 4.2 gère le chargement des journaux de diagnostic et de performances par le biais d’une propriété d’appareil unique.

## <a name="overview"></a>Vue d'ensemble ##
Vous pouvez améliorer l’expérience de vos utilisateurs et faciliter la résolution de leurs problèmes en activant le chargement automatique des données des journaux de diagnostic, de performances et de télémétrie vers Microsoft. 

> [!IMPORTANT] 
> Afin de respecter la confidentialité de l’utilisateur, en tant que développeur d’applications, vous devez lui demander son consentement avant d’activer la journalisation automatique.

> [!NOTE]
> À titre d’exemple, voici un message standard que Microsoft utilise pour la notification de journalisation : 
>
> *En activant la journalisation des erreurs et des performances, vous acceptez d’envoyer les données des erreurs et des performances à Microsoft.  Microsoft collecte les données des erreurs et des performances via Internet (« Données »).  Microsoft utilise ces données pour fournir et améliorer la qualité, la sécurité et l’intégrité des produits et des services Microsoft.  Par exemple, nous analysons les performances et la fiabilité, comme les fonctionnalités que vous utilisez, la rapidité de réponse des fonctionnalités, les performances de l’appareil, les interactions de l’interface utilisateur et tous les problèmes que vous rencontrez avec le produit.  Les données incluent également des informations sur la configuration de votre logiciel, comme le logiciel en cours d’exécution et l’adresse IP.*  

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

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## <a name="ios"></a>iOS ##
Activer la journalisation automatique

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

Définir le contrôle de niveau de journalisation

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

Obtenir le paramètre de contrôle de niveau de journalisation

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## <a name="windows"></a>Windows ##
Activer la journalisation automatique

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Pour plus d’informations sur les paramètres facultatifs, consultez [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx).

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Remarque** : Les extraits de code Windows ci-dessus sont en C++. Pour C\#, mettez à jour la syntaxe avec « . » à la place de « :: ».

**Linux / C++**  : Ce SDK présente une journalisation de base qui n’est pas aussi complète que celle des autres plateformes. Pour plus d’informations, consultez la section **Dépannage** de « README.md » dans [RMS SDK pour C++ portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).
