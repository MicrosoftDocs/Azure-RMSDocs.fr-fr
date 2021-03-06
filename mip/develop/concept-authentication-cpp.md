---
title: Concepts – Authentification dans le kit SDK MIP
description: Cet article va vous aider à comprendre comment le kit SDK MIP implémente l’authentification, ainsi que les conditions requises pour que les applications clientes fournissent une logique d’acquisition de jeton d’accès OAuth2.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9cc8d3b874e4971907770ee18508f331acf1ea2d
ms.sourcegitcommit: 437057990372948c9435b620052a7398360264b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/20/2020
ms.locfileid: "97701626"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés à l’authentification

L’authentification dans le kit SDK MIP s’effectue en étendant la classe `mip::AuthDelegate` pour implémenter votre méthode d’authentification préférée. `mip::AuthDelegate` contient :

- `mip::AuthDelegate::OAuth2Challenge` – classe qui gère les informations d’autorité OAuth2 et fournit des données à l’application cliente.
- `mip::AuthDelegate::OAuth2Token` – classe qui gère l’acquisition d’un jeton accès OAuth2 (à partir de l’application cliente) et le stockage du jeton.
- `mip::AuthDelegate::AcquireOAuth2Token()` – fonction virtuelle pure, dont l’implémentation détermine la méthode d’acquisition de jeton d’accès. Après avoir été appelée par le kit SDK, elle acquiert le jeton d’accès, puis le fournit en retour à la logique d’authentification du kit SDK.

`mip::AuthDelegate::AcquireOAuth2Token` accepte les paramètres suivants et retourne une valeur booléenne indiquant si l’acquisition du jeton a réussi :

- `mip::Identity` : l’identité de l’utilisateur ou du service à authentifier, si elle est connue.
- `mip::AuthDelegate::OAuth2Challenge`: Accepte quatre paramètres, **autorité**, **ressource**, **revendications** et **étendues**. L’**autorité** est le service par rapport auquel le jeton sera généré. La **ressource** est le service auquel nous essayons d’accéder. Le kit SDK traitera la transmission de ces paramètres dans le délégué lorsqu’il sera appelé. Les **revendications** sont les revendications spécifiques aux étiquettes requises par le service de protection. Les **étendues** sont les étendues d’autorisation Azure ad requises pour accéder à la ressource. 
- `mip::AuthDelegate::OAuth2Token` : le résultat de jeton est écrit dans cet objet. Il sera consommé par le kit SDK lorsque le moteur sera chargé. En dehors de notre implémentation de l’authentification, il ne devrait pas être nécessaire d’obtenir ou de définir cette valeur.

**Important :** Les applications n’appellent pas `AcquireOAuth2Token` directement. Le kit SDK appellera cette fonction si nécessaire.

## <a name="consent"></a>Consentement

Azure AD exige qu’une application reçoive un consentement, avant d’être autorisée à accéder aux API/ressources sécurisées sous l’identité d’un compte. Le consentement est enregistré comme un accusé de réception permanent de l’autorisation dans le locataire du compte, pour le compte spécifique (consentement de l’utilisateur) ou pour tous les comptes (consentement de l’administrateur). Le consentement intervient dans divers scénarios, en fonction de l’API accédée et des autorisations que l’application recherche, ainsi que du compte utilisé pour la connexion : 

- les comptes du *locataire* où votre application est inscrite, si vous ou un administrateur n’avez pas explicitement donné votre consentement préalable pour un accès via la fonctionnalité « Accorder des autorisations ».
- les comptes d’un *autre locataire* si votre application est inscrite en tant qu’application multilocataire et que l’administrateur client n’a pas donné son consentement préalable pour tous les utilisateurs à l’avance.

La classe enum `mip::Consent` implémente une approche facile à utiliser qui permet aux développeurs d’applications de fournir une expérience de consentement personnalisée basée sur le point de terminaison accessible par le kit SDK. La notification peut indiquer à l’utilisateur des données qui seront collectées comment supprimer les données ou lui communiquer toute autre information requise par la réglementation ou les stratégies de conformité. Une fois que l’utilisateur a donné son consentement, l’application peut continuer. 

### <a name="implementation"></a>Implémentation

Le consentement est implémenté en étendant la classe de base `mip::Consent` et en implémentant `GetUserConsent` pour retourner l’une des valeurs enum `mip::Consent`. 

L’objet dérivé de `mip::Consent` est transmis au constructeur `mip::FileProfile::Settings` ou `mip::ProtectionProfile::Settings`.

Lorsqu’un utilisateur exécute une opération qui nécessiterait un consentement, le kit SDK appelle la méthode `GetUserConsent` et transmet l’URL de destination comme paramètre. Dans cette méthode, il est possible d’implémenter l’affichage des informations nécessaires à l’utilisateur, pour que celui-ci puisse décider ou non de donner son consentement à l’utilisation du service. 

### <a name="consent-options"></a>Options de consentement

- **AcceptAlways** : donner son consentement et se souvenir de la décision.
- **Accept** : donner son consentement une seule fois.
- **Reject** : ne pas donner son consentement.

Lorsque le Kit SDK requiert le consentement de l’utilisateur avec cette méthode, l’application cliente doit présenter l’URL à l’utilisateur. Les applications clientes doivent fournir un moyen d’obtenir le consentement de l’utilisateur et retourner l’énum de consentement appropriée qui correspond à la décision de l’utilisateur.

### <a name="sample-implementation"></a>Implémentation d'exemple

#### <a name="consent_delegate_implh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consent_delegate_implcpp"></a>consent_delegate_impl.cpp

Lorsque le kit SDK requiert un consentement, la méthode `GetUserConsent` est appelée *par le kit SDK*, et l’URL est transmise en tant que paramètre. Dans l’exemple ci-dessous, l’utilisateur est informé que le kit de développement logiciel (SDK) se connectera à cette URL fournie et fournira à l’utilisateur une option sur la ligne de commande. En fonction du choix de l’utilisateur, l’utilisateur accepte ou rejette le consentement et est transmis au kit de développement logiciel (SDK). Si l’utilisateur refuse de donner son consentement, l’application lèvera une exception et aucun appel n’est effectué au service de protection. 

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  //Print the consent URL, ask user to choose
  std::cout << "SDK will connect to: " << url << std::endl;

  std::cout << "1) Accept Always" << std::endl;
  std::cout << "2) Accept" << std::endl;
  std::cout << "3) Reject" << std::endl;
  std::cout << "Select an option: ";
  char input;
  std::cin >> input;

  switch (input)
  {
  case '1':
    return Consent::AcceptAlways;
    break;
  case '2':
    return Consent::Accept;
    break;
  case '3':
    return Consent::Reject;
    break;
  default:
    return Consent::Reject;
  }  
}
```

À des fins de test et de développement, `ConsentDelegate` il est possible d’implémenter un simple qui ressemble à ceci :

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

Toutefois, dans le code de production, l’utilisateur peut être invité à donner son consentement, en fonction des exigences et des réglementations régionales ou professionnelles. 

## <a name="next-steps"></a>Étapes suivantes

Par souci de simplicité, les exemples qui illustrent le délégué implémenteront l’acquisition du jeton en appelant un script externe. Ce script peut être remplacé par n’importe quel autre type de script, par une bibliothèque OAuth2 open source ou par une bibliothèque OAuth2 personnalisée.

- [Acquérir un jeton d’accès à l’aide de Python](concept-authentication-acquire-token-py.md)
