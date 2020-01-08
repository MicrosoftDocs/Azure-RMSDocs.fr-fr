---
title: Démarrage rapide - Protection Active Directory Rights Management Server
description: Guide de démarrage rapide sur la procédure de configuration d’Active Directory Rights Management Server (AD RMS)
author: tommoser
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/17/2019
ms.author: tommos
ms.openlocfilehash: 424a260b1646a381dca23de71785dd34f92fc281
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555158"
---
# <a name="quickstart-active-directory-rights-management-server-ad-rms-protection"></a>Démarrage rapide : Protection Active Directory Rights Management Server (AD RMS)

Ce guide de démarrage rapide vous montre comment implémenter la prise en charge d’Active Directory Rights Management Server (AD RMS) avec le SDK MIP.

> [!NOTE]
> Les étapes décrites dans ce guide de démarrage rapide s’appliquent uniquement à l’API File pour C# ou C++ et à l’API Protection pour C++.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas déjà fait, veillez à :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation d’une application cliente (C++)](quick-app-initialization-cpp.md) pour créer une solution Visual Studio de démarrage.
- Effectuez d’abord les étapes du [Démarrage rapide : Répertorier les étiquettes de sensibilité (C++)](quick-file-list-labels-cpp.md) ou du [Démarrage rapide : Répertorier les étiquettes de sensibilité (C#)](quick-file-list-labels-csharp.md)
- Déployez AD RMS avec l’[extension Appareils mobiles](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11)).
- Le cas échéant, assurez-vous que l’[enregistrement DNS SRV pour AD RMS MDE](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension) est publié.

## <a name="service-discovery"></a>Détection du service

Le SDK effectue la détection du service sur la base de `mip::Identity` fourni via `FileEngineSettings` ou `ProtectionEngineSettings` en utilisant le suffixe UPN ou de l’adresse mail. Il recherche d’abord l’enregistrement *_rmsdisco* dans la hiérarchie du domaine pour MDE. Pour plus de détails sur ce processus, reportez-vous à la [Spécification des enregistrements SRV DNS pour l’extension Appareils mobiles AD RMS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn673574(v%3dws.11)#specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension). Si cet enregistrement DNS SRV est introuvable, le service Azure Information Protection est utilisé par défaut comme emplacement de service.

Si une identité n’est pas disponible ou si l'enregistrement DNS SRV pour MDE n’a pas été publié, le processus de détection du service peut être annulé en définissant explicitement l’[URL du point de terminaison cloud](https://docs.microsoft.com/information-protection/develop/reference/class_mip_fileengine_settings#setpolicycloudendpointbaseurl-function).

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>Configuration de l’API File dans C# pour utiliser AD RMS

Deux modifications mineures sont requises si votre application utilise la bibliothèque d’authentification Azure Active Directory (ADAL) et l’API File sur C#. L’objet `FileEngineSettings` et le constructeur `AuthenticationContext` doivent être mis à jour pour fonctionner avec AD RMS et Active Directory Federations Services (ADFS).

Si vous avez déployé l’enregistrement DNS SRV de l’extension d’appareil mobile et prévoyez de passer un nom d’utilisateur principal ou une adresse e-mail, [suivez les instructions d’utilisation d’une identité](#update-the-file-engine-settings-to-use-ad-rms-with-an-identity).

Si vous n’avez pas l’enregistrement DNS SRV de l’extension d’appareil mobile ou si vous n’avez pas d'identité au moment de l'exécution, [suivez les instructions du point de terminaison explicite](#update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-identity"></a>Définir les paramètres du moteur de fichiers pour utiliser AD RMS avec une identité

Si l’enregistrement DNS SRV pour MDE a été publié et que `Microsoft.InformationProtection.Identity` a été fourni dans le cadre des paramètres du moteur, la seule modification de code requise est de définir `FileEngineSettings.ProtectionOnlyEngine = true`. Cette propriété doit être définie car les opérations d’étiquetage (stratégie) ne sont pas prises en charge pour les paramètres de protection AD RMS.

```csharp
// Configure FileEngineSettings as protection only engine.
var engineSettings = new FileEngineSettings("", "", "en-US")
{
     // Provide the identity for service discovery.
     Identity = identity,
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true
};
```

### <a name="update-the-file-engine-settings-to-use-ad-rms-with-an-explicit-endpoint"></a>Mettre à jour les paramètres du moteur de fichiers pour utiliser AD RMS avec un point de terminaison explicite

Si l’enregistrement DNS SRV pour MDE n’est pas publié ou si `Microsoft.InformationProtection.Identity` n’est pas disponible lors de la création de `FileEngine`, deux modifications de code sont nécessaires. est de définir `FileEngineSettings.ProtectionOnlyEngine = true`. Cette propriété doit être définie car les opérations d’étiquetage (stratégie) ne sont pas prises en charge pour les paramètres de protection AD RMS.

```csharp
// Configure FileEngineSettings as protection only engine and generate a unique engine id.
var engineSettings = new FileEngineSettings("", "", "en-US")
{
     // Set ProtectionOnlyEngine to true for AD RMS as labeling isn't supported
     ProtectionOnlyEngine = true,
     // Provide the explicit AD RMS endpoint
     ProtectionCloudEndpointBaseUrl = "https://rms.contoso.com"
};
```

### <a name="update-the-authentication-delegate"></a>Mettre à jour le délégué d’authentification

Si vous utilisez la Bibliothèque d’authentification Active Directory dans votre application .NET, vous devrez modifier l’implémentation de `Microsoft.InformationProtection.AuthDelegate` afin de désactiver la validation des autorisations. Désactivez la validation des autorisations en définissant `validateAuthority` dans le constructeur `AuthenticationContext` sur **false**.

   ```csharp
   AuthenticationContext authContext = new AuthenticationContext(authority, false, tokenCache);
   ```

## <a name="configuring-file-api-in-c-to-use-ad-rms"></a>Configuration de l’API File dans C++ pour utiliser AD RMS

Si vous avez déployé l’enregistrement DNS SRV de l’extension d’appareil mobile et prévoyez de passer un nom d’utilisateur principal ou une adresse e-mail, [suivez les instructions d’utilisation d’une identité](#update-the-fileenginesettings-to-use-ad-rms-with-an-identity).

Si vous n’avez pas l’enregistrement DNS SRV de l’extension d’appareil mobile ou si vous n’avez pas d'identité au moment de l’exécution, [suivez les instructions du point de terminaison explicite](#update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-identity"></a>Mettre à jour FileEngine::Settings pour utiliser AD RMS avec une identité

Si l’enregistrement DNS SRV pour MDE a été publié et que `mip::Identity` est fourni dans `FileEngine::Settings`, la seule action requise est de régler le moteur sur un moteur de protection uniquement.

```cpp
FileEngine::Settings engineSettings(mip::Identity(mUsername), "");
engineSettings.SetProtectionOnlyEngine = true;
```

### <a name="update-the-fileenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>Mettre à jour FileEngine::Settings pour utiliser AD RMS avec un point de terminaison explicite

Si l’enregistrement DNS SRV pour MDE n’est pas publié ou si une identité n’est pas disponible pour la détection de service, le moteur doit être configuré sur protection uniquement et l’URL du point de terminaison cloud explicite doit être fournie via `SetProtectionCloudEndpointBaseUrl()`.

```cpp
FileEngine::Settings engineSettings("", "");
engineSettings.SetProtectionOnlyEngine = true;
engineSettings.SetProtectionCloudEndpointBaseUrl("https://rms.contoso.com");
```

## <a name="configuring-protection-api-in-c-to-use-ad-rms"></a>Configuration de l’API Protection dans C++ pour utiliser AD RMS

Si vous avez déployé l’enregistrement DNS SRV de l’extension d’appareil mobile et prévoyez de passer un nom d’utilisateur principal ou une adresse e-mail, [suivez les instructions d’utilisation d’une identité](#set-the-protectionenginesettings-to-use-ad-rms-with-an-identity).

Si vous n’avez pas l’enregistrement DNS SRV de l’extension d’appareil mobile ou si vous n’avez pas d’identité au moment de l’exécution, [suivez les instructions du point de terminaison explicite](#set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint).

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-identity"></a>Définir ProtectionEngine::Settings pour utiliser AD RMS avec une identité

Si l’enregistrement DNS SRV de l’extension d’appareil mobile a été publié et qu’une identité est fournie dans `ProtectionEngine::Settings`, aucun changement d’option supplémentaire n’est nécessaire pour utiliser AD RMS. La détection de service identifie le terminal AD RMS et l’utilise pour les opérations de protection.

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity(mUsername), "");
```

### <a name="set-the-protectionenginesettings-to-use-ad-rms-with-an-explicit-endpoint"></a>Définir ProtectionEngine::Settings pour utiliser AD RMS avec un point de terminaison explicite

Si l’enregistrement DNS SRV n’est pas publié ou si une identité n’est pas fournie dans `ProtectionEngine::Settings`, alors l’URL du point de terminaison de protection doit être définie explicitement via `SetProtectionCloudEndpointBaseUrl()`.

```cpp
ProtectionEngine::Settings engineSettings("", "");
engineSettings.SetProtectionCloudEndpointBaseUrl("https://RMS.CONTOSO.COM");
```

## <a name="remove-or-comment-label-references"></a>Supprimer ou commenter des références d’étiquettes

Si vous créez l’application à partir de l’un des guides de démarrage rapide, vous constaterez que votre application contient des références aux étiquettes sous la forme de `fileEngine.SensitivityLabels` ou `engine->ListSensitivityLabels();`. Du fait que l’application a été définie sur la protection uniquement, ces blocs de code doivent être commentés ou supprimés car leur exécution entraînera une exception.

## <a name="next-steps"></a>Étapes suivantes

À présent que vous avez effectué les modifications pour prendre en charge AD RMS, votre application peut effectuer toutes les opérations de protection uniquement, en utilisant le service AD RMS comme fournisseur de protection.
