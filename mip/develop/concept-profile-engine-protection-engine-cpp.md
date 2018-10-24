---
title: Concepts – Objet de moteur de l’API de protection
description: Cet article vous aidera à comprendre les concepts liés à l’objet de moteur de protection qui est créé pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: da0c50de6a818fcd8beda0483696ba433ce22149
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453314"
---
# <a name="microsoft-information-protection-sdk---protection-api-engine-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au moteur de l’API de protection

## <a name="implementation-add-a-protection-engine"></a>Implémentation : Ajouter un moteur de protection

Dans l’API de fichier, la classe `mip::ProtectionProfile` est la classe racine pour toutes les opérations du kit SDK. Ayant déjà créé le profil, nous pouvons maintenant ajouter un moteur au profil.

L’exemple ci-dessous illustre l’utilisation d’un moteur unique pour un seul utilisateur authentifié.

### <a name="implementation-create-protection-engine-settings"></a>Implémentation : Créer les paramètres du moteur de protection

De façon similaire à un profil, le moteur nécessite également un objet de paramètres, `mip::ProtectionEngine::Settings`. Cet objet stocke l’identificateur de moteur unique, les données client personnalisables qui peuvent être utilisées pour le débogage ou la télémétrie et, éventuellement, les paramètres régionaux.

Ici, nous créons un objet `ProtectionEngine::Settings` appelé *engineSettings*. 

```cpp
ProtectionEngine::Settings engineSettings("UniqueID", "");
```

**Remarque** : Si vous utilisez cette méthode pour créer l’objet des paramètres de protection, vous devez également définir manuellement CloudEndpointBaseUrl sur https://api.aadrm.com

En guise de bonne pratique, le premier paramètre, **id**, doit être un élément permettant au moteur d’être facilement connecté à l’utilisateur associé, **ou** un objet `mip::Identity`. Pour initialiser les paramètres avec `mip::Identity` :

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

Même si, généralement, vous transmettriez une variable à l’identité plutôt qu’un code en dur.

### <a name="implementation-add-the-protection-engine"></a>Implémentation : Ajouter le moteur de protection

Pour ajouter le moteur, nous allons revenir au modèle futur/promesse utilisé pour charger le profil. Au lieu de créer la promesse pour `mip::ProtectionProfile`, nous allons utiliser `mip::ProtectionEngine`.

```cpp

  //auto profile will be std::shared_ptr<mip::ProtectionProfile>
  auto profile = profileFuture.get();

  //Create the ProtectionEngine::Settings object
  ProtectionEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::ProtectionEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::ProtectionEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::ProtectionEngine>
  auto engine = engineFuture.get();
```

Le résultat final du code ci-dessus est que nous avons ajouté avec succès un moteur pour l’utilisateur authentifié au profil.

## <a name="implementation-list-templates"></a>Implémentation : Répertorier les modèles

En utilisant le moteur ajouté, il est maintenant possible de répertorier tous les modèles de sensibilité disponibles pour l’utilisateur authentifié en appelant `engine->GetTemplatesAsync()`. 

`GetTemplatesAsync()` extrait la liste des identificateurs de modèles. Le résultat est stocké dans un vecteur de `std::shared_ptr<std::string>`.

### <a name="implementation-listsensitivitytemplates"></a>Implémentation : ListSensitivityTemplates()

```cpp
auto loadPromise = std::make_shared<std::promise<shared_ptr<vector<string>>>>();
std::future<std::shared_ptr<std::vector<std::string>>> loadFuture = loadPromise->get_future();
mEngine->GetTemplatesAsync(engineObserver, loadPromise);
auto templates = loadFuture.get();
```

### <a name="implementation-print-the-template-ids"></a>Implémentation : Imprimer les ID des modèles

```cpp
//Iterate through all template IDs in the vector
for (const auto& temp : *templates) {
  cout << "Template:" << "\n\tId: " << temp << endl;
}
```

L’impression des noms est un moyen simple de montrer que nous avons correctement extrait la stratégie à partir du service et que nous avons pu obtenir les modèles. Pour appliquer le modèle, l’identificateur de modèle est requis.

Le mappage des modèles aux étiquettes n’est possible que via l’API de stratégie en examinant le résultat de `ComputeActions()`.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil est chargé, le moteur ajouté et que nous avons des modèles, nous pouvons ajouter un gestionnaire pour commencer à lire, écrire et supprimer des modèles à partir des fichiers. Consultez [Concepts liés aux gestionnaires de protection](concept-handler-protection-cpp.md).