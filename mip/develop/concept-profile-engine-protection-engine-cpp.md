---
title: Concepts – Objet de moteur de l’API de protection
description: Cet article vous aidera à comprendre les concepts liés à l’objet de moteur de protection qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 116bd67298195e66de26ab278802e93644a095dd
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556093"
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

> [!NOTE]
> Si vous utilisez cette méthode pour créer l’objet de paramètres de protection, vous devez également définir manuellement le CloudEndpointBaseUrl sur https://api.aadrm.com ou de TP l’URL du cluster de service Active Directory Rights Management.

En guise de bonne pratique, le premier paramètre, **id**, doit être un élément permettant au moteur d’être facilement connecté à l’utilisateur associé, **ou** un objet `mip::Identity`. Pour initialiser les paramètres avec `mip::Identity` :

```cpp
ProtectionEngine::Settings engineSettings(mip::Identity("Bob@Contoso.com", "");
```

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
