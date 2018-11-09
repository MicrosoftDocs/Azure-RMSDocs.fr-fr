---
title: Concepts – Utilisation de Python pour acquérir un jeton d’accès.
description: Cet article vous aidera à comprendre comment utiliser Python pour acquérir un jeton d’accès OAuth2. Cela est requis par l’implémentation du délégué d’authentification.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 4d6db3d2bd2e2b980770027e07104f7528264e66
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223878"
---
# <a name="acquire-an-access-token-python"></a>Acquérir un jeton d’accès (Python)

Cet exemple montre comment appeler un script Python externe pour obtenir un jeton OAuth2. Cela est requis par l’implémentation du délégué d’authentification.

Ce code n’est pas destiné à être utilisé en production, mais peut être utilisé pour le développement et la compréhension des concepts d’authentification. L’exemple est multiplateforme.

## <a name="prerequisites"></a>Prérequis

Pour exécuter l’exemple ci-dessous, les opérations suivantes doivent être terminées :

- Installez Python 2.7.
- Implémentez utils.h/cpp dans votre projet. 
- Le fichier auth.py doit être ajouté à votre projet et figurer dans le même répertoire que les fichiers binaires au moment de la génération.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

Dans l’exemple d’authentification simple, nous avons présenté une fonction `AcquireToken()` simple qui n’a pris aucun paramètre et retourné une valeur de jeton codée en dur. Dans cet exemple, nous allons surcharger AcquireToken() pour accepter des paramètres d’authentification et appeler un script Python externe pour retourner le jeton.

### <a name="authh"></a>auth.h

Dans auth.h, `AcquireToken()` est surchargée, et la fonction surchargée et les paramètres mis à jour sont les suivants :

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();

    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The AAD client ID of your application.
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

    string AcquireToken() { //ignore in this sample
    }

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
    cmd += (!clientId.empty() ? clientId : "0edbblll-8773-44de-b87c-b8c6276d41eb");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Script Python

Ce script acquiert des jetons d’authentification directement via une demande http simple. Cela est inclus uniquement comme un moyen d’acquérir des jetons d’authentification destinés à être utilisés par les exemples d’applications et n’est pas destiné à être utilisé dans le code de production. Le script fonctionne uniquement sur les locataires qui prennent en charge une authentification http traditionnelle par nom d’utilisateur/mot de passe. L’authentification basée sur MFA ou des certificats échouera.

```python
import getopt
import sys
import json
import urllib
import urllib2
import re

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
    authority = authority + 'token'

  # Build REST call
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
  }

  params = {
    'resource': resource,
    'client_id': clientId,
    'grant_type': 'password',
    'username': username,
    'password': password
  }

  req = urllib2.Request(
    url = authority,
    headers = headers,
    data = urllib.urlencode(params))

  f = urllib2.urlopen(req)
  response = f.read()
  f.close()
  sys.stdout.write(json.loads(response)['access_token'])

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


