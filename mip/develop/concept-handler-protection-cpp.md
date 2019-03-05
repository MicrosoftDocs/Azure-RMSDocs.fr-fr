---
title: Concepts – Gestionnaires de protection dans le kit SDK MIP
description: Cet article vous aidera à comprendre comment les gestionnaires de l’API de protection sont créés et utilisés pour appeler des opérations.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: dd38b8e6c9deb45b4ce7df9ec3363ac8036a7ef4
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330183"
---
# <a name="microsoft-information-protection-sdk---protection-handler-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux gestionnaires de protection

Dans l’API de protection du kit SDK MIP, `mip::ProtectionHandler` expose les fonctions permettant de chiffrer et déchiffrer les tampons et flux protégés, d’effectuer des vérifications d’accès, d’obtenir la licence de publication et d’obtenir des attributs à partir des informations protégées. 

## <a name="requirements"></a>Configuration requise

La création d’un `ProtectionHandler` pour utiliser un fichier spécifique nécessite :

- Un `ProtectionProfile`
- L’ajout d’un `ProtectionEngine` au `ProtectionProfile`
- Une classe qui hérite de `mip::ProtectionHandler::Observer`, similaire au modèle indiqué [ici]()
- Un `mip::ProtectionDescriptor` ou une licence de publication

## <a name="create-a-protection-handler"></a>Créer un gestionnaire de protection

Les objets `mip::ProtectionHandler` sont construits en fournissant un `ProtectionDescriptor` ou une licence de publication sérialisée à l’une des deux fonctions `ProtectionEngine`. Le descripteur de protection doit être généré pour la protection des informations de texte en clair n’ayant pas déjà une licence de publication. La **licence de publication** sera utilisée lors du déchiffrement du contenu déjà protégé ou lors de la protection de contenu lorsque la licence a déjà été construite. Le contenu protégé ne peut pas être déchiffré sans la licence de publication associée.

`mip::ProtectionEngine` expose deux fonctions pour la création d’un `ProtectionHandler`. Les paramètres sont les mêmes, à l’exception du premier paramètre indiquant le gestionnaire ou la licence de publication.

- `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync`
  - Nécessite un `ProtectionDescriptor` comme premier paramètre.
- `mip::ProtectionEngine::CreateProtectionHandlerFromPublishingLicenseAsync`
  - Nécessite une licence de publication sérialisée, stockée dans `std::vector<unint8_t>` comme premier paramètre.

### <a name="create-from-descriptor"></a>Créer à partir du descripteur

Si vous protégez du contenu qui n’a pas encore été protégé ou lorsque vous appliquez une nouvelle protection à du contenu, ce qui implique son déchiffrement, un `mip::ProtectionDescriptor` doit être construit. Une fois construit, il est transmis à `mip::ProtectionEngine::CreateProtectionHandlerFromDescriptorAsync()` et le résultat est retourné via `mip::ProtectionHandler::Observer`.

```cpp
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();
auto observer = std::make_shared<ProtectionHandlerObserverImpl>();

//Refer to ProtectionDescriptor docs for details on creating the descriptor
auto descriptor = CreateProtectionDescriptor(); //Stub function

mEngine->CreateProtectionHandlerFromDescriptorAsync(
    descriptor,
    mip::ProtectionHandlerCreationOptions::None,
    observer,
    handlerPromise);

auto handler = handlerFuture.get();
```

Une fois l’objet `ProtectionHandler` créé avec succès, des opérations de fichier (get/set/delete/commit) peuvent être effectuées.

### <a name="create-from-publishing-license"></a>Créer à partir de la licence de publication

Cet exemple suppose que la licence de publication a déjà été lue à partir d’une source et stockée dans `std::vector<uint8_t> serializedPublishingLicense`.

```cpp

//TODO: Implement GetPublishingLicense()
//Snip implies that function reads PL from source file, database, stream, etc.
std::vector<uint8_t> serializedPublishingLicense = GetPublishingLicense(filePath);

auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
auto handlerFuture = handlerPromise->get_future();

shared_ptr<ProtectionHandlerObserverImpl> handleObserver =
    std::make_shared<ProtectionHandlerObserverImpl>();

mEngine->CreateProtectionHandlerFromPublishingLicenseAsync(
    serializedPublishingLicense,
    mip::ProtectionHandlerCreationOptions::None,
    handleObserver,
    handlerPromise);

auto handler = handlerFuture.get();
```

