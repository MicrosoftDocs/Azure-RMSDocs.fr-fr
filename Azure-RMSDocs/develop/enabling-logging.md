---
title: "Comment : activer la journalisation des erreurs et des performances | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 gère le chargement des journaux de diagnostic et de performances via une propriété d’appareil unique."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 118aa3e25c6be9d0bf43141585d79030fc79224a


---

# Comment : activer la journalisation des erreurs et des performances
Microsoft Rights Management SDK 4.2 gère le chargement des journaux de diagnostic et de performances via une propriété d’appareil unique.

## Vue d'ensemble ##
Vous pouvez améliorer l’expérience de vos utilisateurs et faciliter la résolution de leurs problèmes en activant le chargement automatique des journaux de diagnostic et de performances sur Microsoft. Afin de respecter la confidentialité de l’utilisateur, en tant que développeur d’applications, vous devez lui demander son consentement avant d’activer la journalisation automatique.

Vous allez gérer le contrôle de la journalisation via deux propriétés.

-   Activez la journalisation via la propriété **IpcCustomerExperienceDataCollectionEnabled**. Le paramètre est persistant entre les réinitialisations de l’appareil.
-   Contrôlez le niveau de journalisation via la propriété **IpcLogLevel** à l’aide des paramètres suivants.

    * 1 : Commentaires
    * 2 : Informations
    * 3 : Avertissement
    * 4 : Erreur
    * 5 : Critique

Dans chacun des exemples d’extraits de code suivants, l’application appelante peut définir ou interroger la propriété.

### Android ###
Activer la journalisation automatique

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
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
 

## Windows ##
Activer la journalisation automatique

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Pour plus d’informations sur les paramètres facultatifs, consultez [CustomerExperienceOptions](/information-protection/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions).

Obtenir le paramètre d’indicateur de contrôle de la journalisation en cours

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Remarque** : Les extraits de code Windows ci-dessus sont en C++. Pour C\#, mettez à jour la syntaxe avec « . » à la place de « :: ».

**Linux / C++** : Ce SDK présente une journalisation de base qui n’est pas aussi complète que celle des autres plateformes. Pour plus d’informations, consultez la section **Dépannage** de « README.md » dans [RMS SDK pour C++ portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

 

 



<!--HONumber=Sep16_HO5-->


