---
title: Concepts – Utilisation de PowerShell pour acquérir un jeton d’accès
description: Cet article vous aidera à comprendre comment utiliser PowerShell pour acquérir un jeton d’accès OAuth2. Cela est requis par l’implémentation du délégué d’authentification.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a5ce346d044a9a56d37777e569582087026c9ce6
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223877"
---
# <a name="acquire-an-access-token-powershell"></a>Acquérir un jeton d’accès (PowerShell)

Cet exemple montre comment appeler un script PowerShell externe pour obtenir un jeton OAuth2. Cela est requis par l’implémentation du délégué d’authentification.

Ce code n’est pas destiné à être utilisé en production, mais peut être utilisé pour le développement et la compréhension des concepts d’authentification. 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Nous créons une fonction unique appelée AcquireToken. Dans la mesure où la valeur de retour sera codée en dur pour ce tutoriel, nous n’acceptons aucun paramètre et retournons simplement une chaîne (le jeton).

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();
  }
}
```

### <a name="authcpp"></a>auth.cpp

Notre fichier source retourne une valeur de jeton qui sera codée en dur dans une étape ultérieure.

```cpp
//auth.cpp
#include <string>
#include "auth.h"

namespace sample {
  namespace auth {
    string AcquireToken() {
      std::string mToken = "your token here";
      return mToken;
    }
  }
}
```

## <a name="mint-a-token"></a>Émettre un jeton

Pour finir, émettez un jeton à placer dans la variable mToken. L’exemple ci-dessous montre un script PowerShell qui peut être utilisé pour obtenir rapidement le jeton OAuth2 via la bibliothèque ADAL et PowerShell sur Windows. Ce jeton est accordé uniquement pour le point de terminaison du Centre de sécurité et conformité Office 365. Par conséquent, les actions de protection échoueront à moins que l’URL de la ressource soit mise à jour. Il est recommandé de passer directement à la section [Étapes suivantes](#next-steps) si vous souhaitez tester l’étiquetage et la protection à ce stade.

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>Installer [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) à partir de la galerie PS

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Utiliser Get-ADALToken pour obtenir le jeton d’accès

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://dataservice.o365filtering.com"
#clientId and redirectUri are from the RMS Sharing Application. 
#Once custom app registration is supported, a custom id and uri will be required. 
$clientId = "0edbblll-8773-44de-b87c-b8c6276d41eb"
$redirectUri = "com.microsoft.rms-sharing-for-win://authorize"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copiez le jeton à partir du Presse-papiers dans auth.cpp comme valeur pour `string mToken`, en remplaçant « your token here » ci-dessus. Il peut être nécessaire de réexécuter le script, selon la durée des étapes suivantes.


