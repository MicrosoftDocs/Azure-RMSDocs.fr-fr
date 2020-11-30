---
title: Concepts-concepts de base de la prise en charge du kit de développement logiciel MIP-proxy
description: Cet article vous aidera à comprendre la prise en charge du proxy dans le kit de développement logiciel MIP.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2020
ms.author: tommos
ms.openlocfilehash: fdbcf9d618612021a971af34380b65dc062c2802
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316532"
---
# <a name="microsoft-information-protection-sdk---proxy-support"></a>SDK Microsoft Information Protection-prise en charge du proxy

## <a name="proxies-and-the-mip-sdk"></a>Proxies et le kit de développement logiciel MIP

Aujourd’hui, dans le kit de développement logiciel MIP SDK, les proxies non transparents sont pris en charge uniquement sur Windows.

* Le **proxy transparent** fait référence à tout type de proxy qui ne requiert pas de configuration côté client, y compris les paramètres explicites ou AUTODÉCOUVERTS.
* Le **proxy authentifié** fait référence à n’importe quel type de proxy nécessitant l’authentification de l’appelant.
* La **découverte automatique de proxy** fait référence aux proxys ou aux paramètres détectés via la découverte automatique de proxy Web (WPAD).
* Le **Proxy explicite** fait référence à un proxy fourni directement au système d’exploitation ou à l’application.
  
| Plate-forme        | Proxy transparent | Proxys authentifiés | Détection automatique de proxy | Proxy explicite |
| --------------- | ----------------- | --------------------- | -------------------- | -------------- |
| **Windows**     | Prise en charge         | Non pris en charge         | Prise en charge            | Pris en charge      |
| **Linux (tout)** | Prise en charge         | Non pris en charge         | Non pris en charge        | Non pris en charge  |
| ****       | Prise en charge         | Non pris en charge         | Non pris en charge        | Non pris en charge  |
| **Android**     | Prise en charge         | Non pris en charge         | Non pris en charge        | Non pris en charge  |
| **iOS**         | Prise en charge         | Non pris en charge         | Non pris en charge        | Non pris en charge  |

## <a name="proxies-on-windows"></a>Proxies sur Windows

Les applications du kit de développement logiciel (SDK) MIP s’exécutant sous Windows utiliseront WinHTTP pour accéder au réseau. Le paramètre de configuration WinHTTP est indépendant des paramètres du proxy de navigation Internet de Windows Internet (WinINet) et peut uniquement détecter un serveur proxy à l’aide des méthodes de découverte suivantes :

* Méthodes AutoDiscovery :
  * Proxy transparent
  * Protocole WPAD (Web proxy AutoDiscovery)
* Configuration manuelle de proxy statique :
  * WinHTTP configuré à l’aide de la commande netsh

Pour plus d’informations sur la configuration de WinHTTP, consultez la [documentation WinHTTP](/windows/win32/winhttp/winhttp-start-page).

## <a name="proxies-on-other-platforms"></a>Proxies sur d’autres plateformes

Le kit de développement logiciel MIP ne prend pas en charge les proxies, mais totalement transparents, de n’importe quel type sur des plateformes non-Windows. Si vous avez besoin de cette fonctionnalité, consultez les sections délégation HTTP et solution de contournement personnalisées pour plus de détails.

## <a name="custom-http-delegate"></a>Délégué HTTP personnalisé

Le kit de développement logiciel (SDK) Microsoft Information Protection prend en charge l’implémentation d’un délégué HTTP personnalisé qui peut remplacer la pile HTTP par défaut du kit de développement logiciel (SDK). Lorsque des fonctionnalités sont absentes ou qu’une implémentation HTTP spécifique est requise, ce délégué peut être implémenté en ajoutant une nouvelle classe qui hérite de [`mip::HttpDelegate`](./reference/class_mip_httpdelegate.md) .

Cette `mip::HttpDelegate` classe dérivée de est définie via `mip::FileProfile::Settings` :

```cpp
std::shared_ptr<MyHttpDelegate> httpDelegate = std::make_shared<MyHttpDelegate>();
            
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDisk,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetHttpDelegate(httpDelegate);
```

## <a name="other-workarounds"></a>Autres solutions de contournement

Lorsqu’un délégué HTTP personnalisé n’est pas une option, il est nécessaire de contourner votre proxy et d’autoriser une connectivité réseau directe pour les points de terminaison d’étiquetage et de protection MIP, ainsi que pour Azure Active Directory. Si la [journalisation d’audit](/azure/information-protection/reports-aip) est souhaitée, le point de terminaison de journalisation d’audit est également requis.

| Point de terminaison           | HostName                                                                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Service de protection | https://api.aadrm.com                                                                                                                                                   |
| Stratégie             | https:// \* . protection.Outlook.com                                                                                                                                       |
| Journalisation d’audit      | https:// \* . Events.Data.Microsoft.com, https:// \* . Aria.Microsoft.com (iOS uniquement)                                                                                          |
| Authentification     | [Consulter la documentation Azure AD](/azure/active-directory/develop/authentication-national-cloud#azure-ad-authentication-endpoints) |