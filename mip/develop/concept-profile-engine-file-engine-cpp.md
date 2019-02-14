---
title: Concepts – Objet de moteur de l’API de fichier
description: Cet article vous aidera à comprendre les concepts liés à l’objet de moteur de fichier, qui est créé pendant l’initialisation de l’application.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 09b4db10523539f093a54c54d1fc6b7de8f7ddb0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259284"
---
# <a name="microsoft-information-protection-sdk---file-api-engine-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés au moteur de l’API de fichier

L’objet `mip::FileEngine` figurant dans l’API de fichier du kit SDK MIP fournit une interface pour toutes les opérations effectuées au nom d’une identité donnée. Un seul moteur est ajouté pour chaque utilisateur qui se connecte à l’application et toutes les opérations que le moteur effectue sont effectuées dans le contexte de cette identité.

Le `FileEngine` a deux principales responsabilités : Liste des étiquettes pour un utilisateur authentifié et création de gestionnaires de fichier pour effectuer des opérations de fichier pour le compte de l’utilisateur. 

- [`mip::FileEngine`](reference/class_mip_fileengine.md)
- `ListSensitivityLabels()`: Obtient la liste des étiquettes pour le moteur chargé.
- `CreateFileHandler()`: Crée un `mip::FileHandler` pour un fichier spécifique ou un flux.

## <a name="add-a-file-engine"></a>Ajouter un moteur de fichier

Tel qu’indiqué dans [Objets de profil et de moteur](concept-profile-engine-cpp.md), un moteur peut avoir deux états : `CREATED` ou `LOADED`. S’il ne possède aucun de ces deux états, il n’existe pas. Pour créer et charger un état, il suffit d’effectuer un appel unique à `FileProfile::LoadAsync`. Si le moteur existe déjà dans l’état mis en cache, il aura l’état `LOADED`. S’il n’existe pas, il aura les états `CREATED` et `LOADED`. `CREATED` implique que l’application dispose de toutes les informations issues du service requis pour charger le moteur. `LOADED` implique que toutes les structures de données nécessaires pour tirer parti du moteur ont été créées en mémoire.

### <a name="create-file-engine-settings"></a>Créer les paramètres du moteur de fichier

De façon similaire à un profil, le moteur nécessite également un objet de paramètres, `mip::FileEngine::Settings`. Cet objet stocke l’identificateur de moteur unique, les données client personnalisables qui peuvent être utilisées pour le débogage ou la télémétrie et, éventuellement, les paramètres régionaux.

Ici, nous créons un objet `FileEngine::Settings` appelé *engineSettings*. 

```cpp
FileEngine::Settings engineSettings("UniqueID", "");
```

En guise de bonne pratique, le premier paramètre, `id`, doit être un élément permettant au moteur d’être facilement connecté à l’utilisateur associé. Un élément tel qu’une adresse de messagerie, un nom d'utilisateur principal ou un GUID d’objet AAD garantit que l’ID est unique et peut être chargé à partir de l’état local sans appeler le service.

### <a name="add-the-file-engine"></a>Ajouter le moteur de fichier

Pour ajouter ce moteur, nous allons revenir au modèle de promesse/futur utilisé pour charger le profil. Au lieu de créer la promesse pour `mip::FileProfile`, elle est créée à l’aide de `mip::FileEngine`.

```cpp
  //auto profile will be std::shared_ptr<mip::FileProfile>
  auto profile = profileFuture.get();

  //Create the FileEngine::Settings object
  FileEngine::Settings engineSettings("UniqueID", "");

  //Create a promise for std::shared_ptr<mip::FileEngine>
  auto enginePromise = std::make_shared<std::promise<std::shared_ptr<mip::FileEngine>>>();

  //Instantiate the future from the promise
  auto engineFuture = enginePromise->get_future();

  //Add the engine using AddEngineAsync, passing in the engine settings and the promise
  profile->AddEngineAsync(engineSettings, enginePromise);

  //get the future value and store in std::shared_ptr<mip::FileEngine>
  auto engine = engineFuture.get();
```

Le résultat final du code ci-dessus est que le moteur pour l’utilisateur authentifié sera ajouté au profil.

## <a name="list-sensitivity-labels"></a>Répertorier les étiquettes de sensibilité

En utilisant le moteur ajouté, il est maintenant possible de répertorier toutes les étiquettes de sensibilité disponibles pour l’utilisateur authentifié en appelant `engine->ListSensitivityLabels()`.

`ListSensitivityLabels()` extrait la liste des étiquettes et les attributs de ces étiquettes pour un utilisateur spécifique à partir du service. Le résultat est stocké dans un vecteur de `std::shared_ptr<mip::Label>`.

Apprenez-en plus [ici]() sur `mip::Label`.

### <a name="listsensitivitylabels"></a>ListSensitivityLabels()

```cpp
std::vector<shared_ptr<mip::Label>> labels = engine->ListSensitivityLabels();
```

Ou, plus simplement :

```cpp
auto labels = engine->ListSensitivityLabels();
```

### <a name="print-the-labels-and-ids"></a>Imprimer les étiquettes et les ID

L’impression des noms est un moyen simple de montrer que nous avons correctement extrait la stratégie à partir du service et que nous avons pu obtenir les étiquettes. Pour appliquer l’étiquette, l’identificateur d’étiquette est requis. Le code ci-dessous effectue une itération sur toutes les étiquettes, affichant les objets `name` et `id` pour chaque étiquette parent et enfant.

```cpp
//Iterate through all labels in the vector
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

## <a name="next-steps"></a>Étapes suivantes

Maintenant que le profil est chargé, le moteur ajouté et que nous avons des étiquettes, nous pouvons ajouter un gestionnaire pour commencer à lire, écrire et supprimer des étiquettes à partir des fichiers. Consultez [Gestionnaires de fichier dans le kit SDK MIP](concept-handler-file-cpp.md).

