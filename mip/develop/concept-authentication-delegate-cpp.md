---
title: Concepts – Implémentation d’un délégué d’authentification (C++)
description: Cet article vous aidera à comprendre comment implémenter un délégué d’authentification dans C++.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9a9256d4c67845f43eeb1598926ea5c02f07f822
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445731"
---
# <a name="microsoft-information-protection-sdk---implementing-an-authentication-delegate-c"></a>Kit SDK Microsoft Information Protection – Implémentation d’un délégué d’authentification (C++)

Le kit SDK MIP implémente un délégué d’authentification pour gérer les défis d’authentification et répondre avec un jeton. Il n’implémente pas lui-même l’acquisition du jeton. Le processus d’acquisition de jeton incombe au développeur et s’effectue en étendant la classe `mip::AuthDelegate`, en particulier la fonction membre `AcquireOAuth2Token`.

## <a name="building-authdelegateimpl"></a>Génération d’AuthDelegateImpl

Pour étendre la classe de base `mip::AuthDelegate`, nous créons une nouvelle classe appelée `sample::auth::AuthDelegateImpl`. Cette classe implémente la fonctionnalité `AcquireOAuth2Token` et configure le constructeur pour qu’il accepte nos paramètres d’authentification.

### <a name="authdelegateimplh"></a>auth_delegate_impl.h

Pour cet exemple, le constructeur par défaut accepte simplement le nom d’utilisateur, le mot de passe et l’[ID d’application](/azure/active-directory/develop/developer-glossary.md#application-id-client-id) de l’application. Ces éléments seront stockées dans les variables privées `mUserName`, `mPassword` et `mClientId`.

Il est important de noter que des informations telles que le fournisseur d’identité ou l’URI de ressource ne sont pas tenues d’être implémentées, du moins pas dans le constructeur `AuthDelegateImpl`. Ces informations sont transmises dans le cadre de `AcquireOAuth2Token` dans l’objet `OAuth2Challenge`. Au lieu de cela, nous transmettrons ces détails à l’appel `AcquireToken` dans `AcquireOAuth2Token`.

```cpp
//auth_delegate_impl.h
#include <string.h>
#include "mip/common_types.h"

namespace sample {
namespace auth {
class AuthDelegateImpl final : public mip::AuthDelegate { //extend mip::AuthDelegate base class
public:
  AuthDelegateImpl() = delete;

  //constructor accepts username, password, and clientId, all plain strings.
  AuthDelegateImpl(
    const std::string& userName,
    const std::string& password,
    const std::string& clientId
  );

  bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) override;

private:
  std::string mUserName;
  std::string mPassword;
  std::string mClientId;
};

}
}
```

### <a name="authdelegateimplcpp"></a>auth_delegate_impl.cpp

L’appel du fournisseur OAuth2 sera effectué dans `AcquireOAuth2Token`. Dans l’exemple ci-dessous, il y a deux appels à `AcquireToken()`. Dans la pratique, un seul appel serait effectué. Ces implémentations seront couvertes dans les sections répertoriées sous [Étapes suivantes](#next-steps).

```cpp
//auth_delegate_impl.cpp
#include "auth_delegate_impl.h"
#include <stdexcept>
#include "auth.h" //contains the auth class used later for token acquisition

using std::runtime_error;
using std::string;

namespace sample {
namespace auth {

AuthDelegateImpl::AuthDelegateImpl(
    const string& userName,
    const string& password,
    const string& clientId)
    : mUserName(userName),
    mPassword(password),
    mClientId(clientId) {
}

//Here we could simply add our token acquisition code to AcquireOAuth2Token
//Instead, that code is implemented in auth.h/cpp to demonstrate calling an external library
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/, //This won't be used
    const OAuth2Challenge& challenge,
    const OAuth2Token& token) {

      //sample::auth::AcquireToken is the code where the token acquisition routine is implemented.
      //AcquireToken() returns a string that contains the OAuth2 token.

      //Simple example for getting hard coded token. Comment out if not used.
      string accessToken = sample::auth::AcquireToken();

      //Practical example for calling external OAuth2 library with provided authentication details.
      string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetAuthority(), challenge.GetResource());  

      //set the passed in OAuth2Token value to the access token acquired by our provider
      token.SetAccessToken(accessToken);
      return true;
    }
}
}
```

## <a name="next-steps"></a>Étapes suivantes

Pour terminer l’implémentation de l’authentification, il est nécessaire de générer le code figurant derrière la fonction `AcquireToken()`. Les exemples ci-dessous décrivent plusieurs façons d’acquérir le jeton.

- [Exemple d’acquisition de jeton simple/PowerShell](concept-authentication-acquire-token-ps.md)
- [Exemple d’acquisition de jeton Python](concept-authentication-acquire-token-py.md)
