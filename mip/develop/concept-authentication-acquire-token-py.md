---
title: Concepts – Utilisation de Python pour acquérir un jeton d’accès.
description: Cet article vous aidera à comprendre comment utiliser Python pour acquérir un jeton d’accès OAuth2. Cela est requis par l’implémentation du délégué d’authentification.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: b46f478dc38e9010cc2eb221f587f3d3ca3f60a2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884735"
---
# <a name="acquire-an-access-token-python"></a>Acquérir un jeton d’accès (Python)

Cet exemple montre comment appeler un script Python externe pour obtenir un jeton OAuth2. Un jeton d’accès OAuth2 valide est requis par l’implémentation du délégué d’authentification.

## <a name="prerequisites"></a>Prérequis

Pour exécuter l’exemple ci-dessous:

- Installez Python 2,7 ou une version plus récente.
- Implémentez utils.h/cpp dans votre projet. 
- Auth.py doit être ajouté à votre projet et se trouver dans le même répertoire que les binaires de la Build.
- [Installation et configuration du kit de développement logiciel (MIP) SDK](setup-configure-mip.md). Entre autres tâches, vous allez inscrire votre application cliente dans votre locataire Azure Active Directory (Azure AD). Azure AD fournira un ID d’application, également appelé ID client, qui est utilisé dans votre logique d’acquisition de jeton.

Ce code n’est pas destiné à une utilisation en production. Elle ne peut être utilisée que pour le développement et la compréhension des concepts d’authentification. L’exemple est multiplateforme.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

Dans l’exemple d’authentification simple, nous avons démontré `AcquireToken()` une fonction simple qui n’a pris aucun paramètre et a retourné une valeur de jeton codée en dur. Dans cet exemple, nous allons surcharger AcquireToken() pour accepter des paramètres d’authentification et appeler un script Python externe pour retourner le jeton.

### <a name="authh"></a>auth.h

Dans auth.h, `AcquireToken()` est surchargée, et la fonction surchargée et les paramètres mis à jour sont les suivants :

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {    
    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The Azure AD client ID (also known as Application ID) of your application.
        const std::string& resource, //The resource URL for which an OAuth2 token is required. Provided by challenge object.
        const std::string& authority); //The authentication authority endpoint. Provided by challenge object.
    }
}
```

Les trois premiers paramètres seront entrés par l’utilisateur ou codés en dur dans votre application. Les deux derniers paramètres sont fournis par le kit SDK au délégué d’authentification. 


### <a name="authcpp"></a>auth.cpp

Dans auth.cpp, nous ajoutons la définition de la fonction surchargée, puis définissons le code nécessaire pour appeler le script Python. La fonction accepte tous les paramètres fournis et les transmet au script Python. Le script s’exécute et retourne le jeton au format chaîne.

```cpp
#include "auth.h"
#include "utils.h"

#include <fstream>
#include <functional>
#include <memory>
#include <string>

using std::string;
using std::runtime_error;

namespace sample {
    namespace auth {

    //This function implements token acquisition in the application by calling an external Python script.
    //The Python script requires username, password, clientId, resource, and authority.
    //Username, Password, and ClientId are provided by the user/developer
    //Resource and Authority are provided as part of the OAuth2Challenge object that is passed in by the SDK to the AuthDelegate.
    string AcquireToken(
        const string& userName,
        const string& password,
        const string& clientId,
        const string& resource,
        const string& authority) {

    string cmd = "python";
    if (sample::FileExists("auth.py"))
        cmd += " auth.py -u ";

    else
        throw runtime_error("Unable to find auth script.");

    cmd += userName;
    cmd += " -p ";
    cmd += password;
    cmd += " -a ";
    cmd += authority;
    cmd += " -r ";
    cmd += resource;
    cmd += " -c ";
    // Replace <application-id> with the Application ID provided during your Azure AD application registration.
    cmd += (!clientId.empty() ? clientId : "<application-id>");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Script Python

Ce script acquiert des jetons d’authentification directement via [Adal pour Python](https://github.com/AzureAD/azure-activedirectory-library-for-python). Ce code est inclus uniquement comme un moyen d’acquérir des jetons d’authentification pour une utilisation par les exemples d’applications et n’est pas destiné à être utilisé en production. Le script fonctionne uniquement sur les locataires qui prennent en charge une authentification http traditionnelle par nom d’utilisateur/mot de passe. L’authentification basée sur MFA ou des certificats échouera.

> [!NOTE] 
> Avant d’exécuter cet exemple, vous devez installer ADAL pour Python en exécutant l’une des commandes suivantes:

```shell
pip install adal
pip3 install adal
```

```python
import getopt
import sys
import json
import re
from adal import AuthenticationContext

def printUsage():
  print('auth.py -u <username> -p <password> -a <authority> -r <resource> -c <clientId>')

def main(argv):
  try:
    options, args = getopt.getopt(argv, 'hu:p:a:r:c:')
  except getopt.GetoptError:
    printUsage()
    sys.exit(-1)

  username = ''
  password = ''
  authority = ''
  resource = ''

  clientId = ''
    
  for option, arg in options:
    if option == '-h':
      printUsage()
      sys.exit()
    elif option == '-u':
      username = arg
    elif option == '-p':
      password = arg
    elif option == '-a':
      authority = arg
    elif option == '-r':
      resource = arg
    elif option == '-c':
      clientId = arg

  if username == '' or password == '' or authority == '' or resource == '' or clientId == '':
    printUsage()
    sys.exit(-1)

  # Find everything after the last '/' and replace it with 'token'
  if not authority.endswith('token'):
    regex = re.compile('^(.*[\/])')
    match = regex.match(authority)
    authority = match.group()
    authority = authority + username.split('@')[1]

  auth_context = AuthenticationContext(authority)
  token = auth_context.acquire_token_with_username_password(resource, username, password, clientId)
  print(token["accessToken"])

if __name__ == '__main__':  
  main(sys.argv[1:])
```

## <a name="update-acquireoauth2token"></a>Mettre à jour AcquireOAuth2Token

Enfin, mettez à jour la fonction `AcquireOAuth2Token` dans `AuthDelegateImpl` pour appeler la fonction `AcquireToken` surchargée. Les URL de ressource et d’autorité sont obtenues en lisant `challenge.GetResource()` et `challenge.GetAuthority()`. Le `OAuth2Challenge` est transmis au délégué d’authentification lorsque le moteur est ajouté. Ce travail est effectué par le SDK et ne nécessite aucun travail supplémentaire de la part du développeur. 

```cpp
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/,
    const OAuth2Challenge& challenge,
    OAuth2Token& token) {

    //call our AcquireToken function, passing in username, password, clientId, and getting the resource/authority from the OAuth2Challenge object
    string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetResource(), challenge.GetAuthority());
    token.SetAccessToken(accessToken);
    return true;
}
```

Lorsque `engine` est ajouté, le kit SDK appelle la fonction AcquireOAuth2Token, transmet le défi, exécute le script Python, reçoit un jeton, puis présente le jeton au service.


