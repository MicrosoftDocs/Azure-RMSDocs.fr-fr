---
title: Concepts-délégation
description: Cet article vous aidera à comprendre les concepts relatifs à la délégation dans le kit de développement logiciel MIP.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 848b0752f6158ade4fd61b562163e2e641454773
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224945"
---
# <a name="concept---delegation-in-the-mip-sdk"></a>Concept-délégation dans le kit de développement logiciel (SDK) MIP

Le kit de développement logiciel (SDK) Microsoft Information Protection fournit deux chemins d’accès pour les applications basées sur les services afin d’agir au nom d’un autre utilisateur. La délégation peut être nécessaire lorsque des fichiers doivent être étiquetés, protégés ou consommés dans le contexte d’une identité d’utilisateur différente de l’identité de service. Cette identité déléguée peut être définie au niveau du **moteur** ou du **Gestionnaire** et où elle est définie dépend du cas d’usage.

## <a name="engine-settings-based-delegation"></a>Délégation basée sur les paramètres du moteur

Le SDK MIP prend en charge la fourniture d’une adresse de messagerie d’utilisateur déléguée dans l’objet Settings pour tous les kits de développement logiciel (SDK); Fichier, protection et stratégie. Cela est possible en définissant la `DelegatedUserEmail` propriété sur l’objet de paramètres. Le résultat est que le moteur initialisé avec cet objet de paramètres effectuera **toutes les opérations MIP** comme s’il s’agissait de l’utilisateur fourni à la `DelegatedUserEmail` propriété. La stratégie sera extraite pour cet utilisateur spécifique et toutes les opérations de protection seront exécutées en tant qu’utilisateur, notamment en tant que propriétaire des fichiers protégés.

Ce modèle est utile lorsque votre application basée sur les services doit fonctionner entièrement en tant qu’utilisateur ; la stratégie doit être extraite uniquement pour l’utilisateur spécifié, et toutes les opérations de déchiffrement doivent être effectuées dans le contexte de l’identité de l’utilisateur. Lors de la création de ce moteur, il est important que l’application spécifie un ID de moteur propre à cet utilisateur, souvent l’adresse de messagerie. Cela garantit que les avantages de la mise en cache seront atteints. Si un ID de moteur unique n’est pas fourni, votre application peut présenter des performances médiocres.

### <a name="file-sdk"></a>SDK de fichiers

L’exemple suivant montre comment définir l’identité déléguée pour une application de kit de développement logiciel (SDK) de fichier en C++ et C#. Le même modèle peut être utilisé pour le kit de développement logiciel (SDK) de stratégie.

Cet exemple montre comment créer un **moteur délégué** dans le kit de développement logiciel (SDK) de fichier dans .net.

```csharp
// C# Example for creating a delegated file engine
string delegatedUserEmail = "alice@contoso.com";
var engineSettings = new PolicyEngineSettings(delegatedUserEmail, authDelegate, "", "en-US")
{
    // Provide the identity for service discovery.
    Identity = identity,
    // Set the identity for which all MIP operations will be performed.
    DelegatedUserEmail = delegatedUserEmail
};

var engine = Task.Run(async () => await profile.AddEngineAsync(engineSettings)).Result;
```

Cet exemple montre comment créer un **moteur délégué** dans le kit de développement logiciel (SDK) de fichier en C++.

```c++
// C++ Example for creating a delegated file engine
std::string delegatedUserEmail = "alice@contoso.com";
FileEngine::Settings engineSettings(delegatedUserEmail, mAuthDelegate, "", "en-US", false);
// Set the identity for which all MIP operations will be performed. 
engineSettings.SetDelegatedUserEmail(delegatedUserEmail);

auto enginePromise = std::make_shared<std::promise<std::shared_ptr<FileEngine>>>();
auto engineFuture = enginePromise->get_future();

mProfile->AddEngineAsync(engineSettings, enginePromise);
mEngine = engineFuture.get();
```

Le résultat est que tous les moteurs de fichiers seront créés pour le compte de l’utilisateur spécifié.


## <a name="handler-based-delegation"></a>Délégation basée sur un gestionnaire

Dans les scénarios où nous avons besoin uniquement de **protéger** des fichiers dans le contexte d’une identité d’utilisateur spécifique, le `FileHandler` fournit une méthode pour transmettre l’identité de l’utilisateur via un `ProtectionSettings` objet. La stratégie et les opérations de déchiffrement sont exécutées en tant qu' **identité de service** authentifiée. L’action de protection sera effectuée pour le compte de l’utilisateur spécifié ; cet utilisateur est le **propriétaire** de la protection MIP sur le document.

### <a name="file-sdk"></a>SDK de fichiers

Seule l’opération d’application de la protection soit directement, soit par le biais de l’étiquette, en tant qu’utilisateur fourni à l' `ProtectionSettings` objet. Cet objet est passé aux `SetLabel()` `SetProtection()` fonctions ou dans le kit de développement logiciel (SDK) du fichier.

Cet exemple montre comment effectuer une **opération de protection par déléguer** dans le kit de développement logiciel (SDK) de fichier dans .net.

```csharp
string delegatedUserEmail = "bob@contoso.com";
ProtectionSettings protectionSettings = new ProtectionSettings()
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, protectionSettings);
// Similar pattern for SetProtection()
// handler.SetProtection(protectionDescriptor, protectionSettings);
```

Cet exemple montre comment effectuer une **opération de protection par déléguer** dans le kit de développement logiciel (SDK) de fichier en C++.

```c++
mip::ProtectionSettings protectionSettings;
// Set the delegated mail address 
protectionSettings.SetDelegatedUserEmail(delegatedUserEmail);
handler->SetLabel(mEngine->GetLabelById(labelId), labelingOptions, protectionSettings);
```

Le résultat est que toutes les opérations d' **écriture** de gestionnaire où la protection est appliquée seront exécutées en tant qu’utilisateur délégué. 

### <a name="protection-sdk"></a>SDK protection

Le kit de développement logiciel (SDK) de protection fonctionne différemment du SDK file. Il existe **deux types de gestionnaires** qui peuvent être créés : un pour la publication et un pour la consommation. Comme pour le kit de développement logiciel (SDK) file, l’adresse de messagerie déléguée est définie via l’objet Settings pour chaque type de gestionnaire.

#### <a name="net"></a>.NET

Cet exemple montre comment effectuer une **publication déléguée**.

```csharp
string delegatedUserEmail = "bob@contoso.com";
PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor)
{
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};          
var protectionHandler = engine.CreateProtectionHandlerForPublishing(publishingSettings);
```

Cet exemple montre comment effectuer une **consommation déléguée**.

```csharp
string delegatedUserEmail = "bob@contoso.com";
ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo)
{                
    ContentName = "A few bytes.",
    // Set the delegated mail address 
    DelegatedUserEmail = delegatedUserEmail
};
var protectionHandler = engine.CreateProtectionHandlerForConsumption(consumptionSettings);
```

#### <a name="c"></a>C++

Cet exemple montre comment effectuer une **consommation déléguée**.

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);
// Set the delegated mail address 
publishingSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

Cet exemple montre comment effectuer une **publication déléguée**.

```c++
string delegatedUserEmail = "bob@contoso.com";
mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
// Set the delegated mail address 
consumptionSettings.SetDelegatedUserEmail(delegatedUserEmail);
mEngine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, handlerObserver, handlerPromise);
auto handler = handlerFuture.get(); 
```

## <a name="required-permissions"></a>Autorisations requises

Chacun des scénarios ci-dessus requiert un jeu d’autorisations différent. 

| Scénario                             | Autorisations requises                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| Moteur de fichiers du SDK délégué            | UnifiedPolicy. locataire. Read<br>Contenu. DelegatedReader<br>Contenu. DelegatedWriter |
| Moteur délégué du SDK de stratégie          | UnifiedPolicy. locataire. Read                                                       |
| Gestionnaire délégué du kit de développement logiciel (SDK)           | Contenu. DelegatedWriter                                                         |
| Publication déléguée du kit de développement logiciel de protection     | Contenu. DelegatedWriter                                                         |
| Consommation déléguée du kit de développement logiciel de protection | Contenu. DelegatedReader                                                         |

Pour une évaluation complète des autorisations et l’emplacement de leur définition, consultez [autorisations d’API pour le kit de développement logiciel (SDK) Microsoft information protection](concept-api-permissions.md)

## <a name="next-steps"></a>Étapes suivantes

- Examiner les [autorisations de l’API pour le kit de développement logiciel (SDK) Microsoft information protection](concept-api-permissions.md)
- Passez en revue la <TODO> référence d’authentification du principal de service.