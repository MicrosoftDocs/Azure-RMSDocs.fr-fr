---
title: Concepts – Objet de moteur de l’API de stratégie
description: Cet article vous aidera à comprendre les concepts liés à l’objet de moteur de stratégie, qui est créé pendant l’initialisation de l’application.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 6cfd75a3f56ebe12dc0c1caa3bd4e56438827af4
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764068"
---
# <a name="microsoft-information-protection-sdk---policy-api-engine-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au moteur de l’API de stratégie

`mip::PolicyEngine` implémente toutes les opérations que l’API de stratégie peut effectuer, à l’exception du chargement du profil.

## <a name="implementation-add-a-policy-engine"></a>Implémentation : Ajouter un moteur de stratégie

### <a name="implementation-create-policy-engine-settings"></a>Implémentation : Créer les paramètres du moteur de stratégie

De façon similaire à un profil, le moteur nécessite également un objet de paramètres, `mip::PolicyEngine::Settings`. Cet objet stocke l’identificateur unique du moteur, un objet de `mip::AuthDelegate` votre implémentation, des données clientes personnalisables qui peuvent être utilisés pour le débogage ou la télémétrie, et, éventuellement, les paramètres régionaux.

Ici, nous créons `FileEngine::Settings` un objet appelé *engineSettings* à l’aide de l’identité de l’utilisateur de l’application :

```cpp
PolicyEngine::Settings engineSettings(
  mip::Identity(mUsername), // mip::Identity.  
  authDelegateImpl,         // Auth delegate object
  "",                       // Client data. Customizable by developer, stored with engine.
  "en-US",                  // Locale.
  false);                   // Load sensitive information types for driving classification.
```

Un ID de moteur personnalisé est également fourni :

```cpp
PolicyEngine::Settings engineSettings(
  "myEngineId",     // String
  authDelegateImpl, // Auth delegate object
  "",               // Client data in string format. Customizable by developer, stored with engine.
  "en-US",          // Locale. Default is en-US
  false);           // Load sensitive information types for driving classification. Default is false.
```

En guise de bonne pratique, le premier paramètre, **id**, doit être un élément permettant au moteur d’être facilement connecté à l’utilisateur associé, de préférence le nom d’utilisateur principal.

### <a name="implementation-add-the-policy-engine"></a>Implémentation : Ajouter le moteur de stratégie

Pour ajouter ce moteur, nous allons revenir au modèle futur/promesse utilisé pour charger le profil. Au lieu de créer la promesse pour `mip::Profile`, nous allons utiliser `mip::PolicyEngine`.

```cpp

  // Auto profile will be std::shared_ptr<mip::Profile>.
  auto profile = profileFuture.get();

  // Create the delegate
  auto authDelegateImpl = std::make_shared<sample::auth::AuthDelegateImpl>(appInfo, userName, password);


  // Create the PolicyEngine::Settings object.
  PolicyEngine::Settings engineSettings("UniqueID", authDelegateImpl, "");

  // Create a promise for std::shared_ptr<mip::PolicyEngine>.
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyEngine>>>();

  // Instantiate the future from the promise.
  auto engineFuture = enginePromise->get_future();

  // Add the engine using AddEngineAsync, passing in the engine settings and the promise.
  profile->AddEngineAsync(engineSettings, enginePromise);

  // Get the future value and store in std::shared_ptr<mip::PolicyEngine>.
  auto engine = engineFuture.get();
```

Le résultat final du code ci-dessus est que nous avons ajouté avec succès un moteur pour l’utilisateur authentifié au profil.

## <a name="implementation-list-sensitivity-labels"></a>Implémentation : Répertorier les étiquettes de sensibilité

En utilisant le moteur ajouté, il est maintenant possible de répertorier toutes les étiquettes de sensibilité disponibles pour l’utilisateur authentifié en appelant `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` extrait la liste des étiquettes et les attributs de ces étiquettes pour un utilisateur spécifique à partir du service. Le résultat est stocké dans un vecteur de `std::shared_ptr<mip::Label>`.

### <a name="implementation-listsensitivitylabels"></a>Implémentation : ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

### <a name="implementation-print-the-labels"></a>Implémentation : Imprimer les étiquettes

```cpp
//Iterate through all labels in the vector
for (const auto& label : labels) {
  //print the label name
  cout << label->GetName() << endl;
  //Iterate through all child labels
  for (const auto& child : label->GetChildren()) {
    //Print the label with some formatting
    cout << "->  " << child->GetName() << endl;
  }
}
```

L’impression des noms est un moyen simple de montrer que nous avons correctement extrait la stratégie à partir du service et que nous avons pu obtenir les étiquettes. Pour appliquer l’étiquette, l’identificateur d’étiquette est requis. La modification de l’extrait ci-dessus pour retourner l’ID d’étiquette donne :

```cpp
for (const auto& label : labels) {
  //Print label name and GUID
  cout << label->GetName() << " : " << label->GetId() << endl;

  //Print child label name and GUID
  for (const auto& child : label->GetChildren()) {
    cout << "->  " << child->GetName() <<  " : " << child->GetId() << endl;
  }
}
```

La collection de `mip::Label` retournée par `GetSensitivityLabels()` peut être utilisée pour afficher toutes les étiquettes disponibles pour l’utilisateur, puis, une fois sélectionnée, utilisez l’ID pour appliquer des étiquettes dans un fichier.
