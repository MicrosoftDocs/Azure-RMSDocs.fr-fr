---
title: Concepts – Utilisation de PowerShell pour acquérir un jeton d’accès
description: Cet article vous aidera à comprendre comment utiliser PowerShell pour acquérir un jeton d’accès OAuth2. Cela est requis par l’implémentation du délégué d’authentification.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: mbaldwin
ms.openlocfilehash: ddc962f97e6e7d6b0e7ff091821fa83063e9f068
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555855"
---
# <a name="acquire-an-access-token-powershell"></a>Acquérir un jeton d’accès (PowerShell)

L’exemple illustré montre comment appeler un script PowerShell externe pour obtenir un jeton OAuth2. Un jeton d’accès OAuth2 valide est requis par l’implémentation du délégué d’authentification.

## <a name="prerequisites"></a>Configuration requise

- [Installation et configuration du kit de développement logiciel (MIP) SDK](setup-configure-mip.md). Entre autres tâches, vous allez inscrire votre application cliente dans votre locataire Azure Active Directory (Azure AD). Azure AD fournira un ID d’application, également appelé ID client, qui est utilisé dans votre logique d’acquisition de jeton.

Ce code n’est pas destiné à une utilisation en production. Elle ne peut être utilisée que pour le développement et la compréhension des concepts d’authentification. 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Nous créons une fonction unique appelée AcquireToken. Étant donné que la valeur de retour sera codée en dur pour ce didacticiel, nous n’acceptons aucun paramètre et renvoyons une chaîne (le jeton).

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

Pour finir, émettez un jeton à placer dans la variable mToken. L’exemple ci-dessous montre un script PowerShell qui peut être utilisé pour obtenir rapidement le jeton OAuth2 via la bibliothèque ADAL et PowerShell sur Windows. Ce jeton est accordé uniquement pour le point de terminaison du Centre de sécurité et conformité Office 365. Par conséquent, les actions de protection échoueront à moins que l’URL de la ressource soit mise à jour. 

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>Installer [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) à partir de la galerie PS

Vous pouvez ignorer cette étape si vous l’avez effectuée précédemment dans [le kit de développement logiciel (MIP) SDK Setup and configuration](setup-configure-mip.md).

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Utiliser Get-ADALToken pour obtenir le jeton d’accès

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://syncservice.o365syncservice.com/"
#replace <application-id> and <redirect-uri>, with the Redirect URI and Application ID from your Azure AD application registration.
$clientId = "<application-id>"
$redirectUri = "<redirect-uri>"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copiez le jeton à partir du Presse-papiers dans auth.cpp comme valeur pour `string mToken`, en remplaçant « your token here » ci-dessus. Il peut être nécessaire de réexécuter le script, selon la durée des étapes suivantes.


