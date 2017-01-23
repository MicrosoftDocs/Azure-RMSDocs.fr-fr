---
title: "Comment : activer la journalisation des erreurs et des performances | Azure RMS"
description: "Microsoft Rights Management SDK 4.2 gère le chargement des journaux de diagnostic et de performances via une propriété d’appareil unique."
keywords: 
author: bruceperlerms
ms.author: bruceper
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
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 9a81746a17988f788503ca706f19a4ed89702c4e


---

# <a name="how-to-enable-error-and-performance-logging"></a>Comment : activer la journalisation des erreurs et des performances
Microsoft Rights Management SDK 4.2 gère le chargement des journaux de diagnostic et de performances via une propriété d’appareil unique.

## <a name="overview"></a>Vue d’ensemble ##
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

**Linux / C++** : Ce SDK présente une journalisation de base qui n’est pas aussi complète que celle des autres plateformes. Pour plus d’informations, consultez la section **Dépannage** de « README.md » dans [RMS SDK pour C++ portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


