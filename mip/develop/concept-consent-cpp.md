---
title: Concepts-consentement dans le kit de développement logiciel (SDK) MIP.
description: Cet article vous aidera à comprendre comment le kit de développement logiciel MIP met en œuvre des flux de consentement pour permettre aux utilisateurs de se connecter au service RMS.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 7025e042d0ded7164b26efbe9b453b4546c5ca05
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766539"
---
# <a name="microsoft-information-protection-sdk---consent"></a>Microsoft Information Protection SDK-consentement

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

À des fins de test et de développement `ConsentDelegate` , il est possible d’implémenter un simple qui ressemble à ceci :

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

Toutefois, dans le code de production, l’utilisateur peut être invité à donner son consentement, en fonction des exigences et des réglementations régionales ou professionnelles. 