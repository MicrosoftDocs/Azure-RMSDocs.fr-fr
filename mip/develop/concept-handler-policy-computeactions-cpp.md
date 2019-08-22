---
title: Concepts - Utilisation du kit SDK Microsoft Information Protection pour générer des événements d’audit
description: Cet article vous aidera à comprendre comment utiliser le kit de développement logiciel (SDK) Microsoft Information Protection pour le calcul.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 8ade287531ee9f1c18678d42ef5e51a4c70ee13f
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886196"
---
# <a name="compute-an-action"></a>Calculer une action

Comme cela a déjà été indiqué, les principales fonctions de l’API de stratégie sont les suivantes :

- Lister les étiquettes disponibles
- retourner un ensemble d’actions à entreprendre, en fonction de l’état actuel et souhaité

La dernière étape du processus consiste à fournir un identificateur d’étiquette et, éventuellement, des métadonnées sur l’étiquette existante à la fonction `ComputeActions()`.

Un exemple de code pour cet article est disponible sur GitHub.

- [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>Calculer une action pour une nouvelle étiquette

Le calcul `mip::Actions` du pour une nouvelle étiquette peut être effectué à l’aide `ExecutionStateImpl` du défini dans [ExecutionState](concept-handler-policy-executionstate-cpp.md).

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Resolve desired label id to mip::Label and set in ExecutionStateOptions.
options.newLabel = mEngine->GetLabelById(newLabelId);

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

L’écriture uniquement du `mip::MetadataActions` retourné dans le cadre de `actions` indique :

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

`PolicyHandler` calcule les actions et retourne un `std::vector` de `mip::Action`. Il revient au développeur d’applications d’appliquer ces métadonnées au fichier ou aux données.

> [!NOTE]
> L’exemple ci-dessus affiche uniquement la sortie de `mip::MetadataAction`. Pour obtenir un exemple d’affichage de types d’action supplémentaires, consultez les exemples de bundles fournis avec le [téléchargement de l’API de stratégie](https://aka.ms/mipsdkbins).

## <a name="compute-actions-with-an-existing-label"></a>Calculer des actions avec une étiquette existante

Lors de l’utilisation de l’API de stratégie, il est à l’application de lire les métadonnées à partir du contenu. Ces métadonnées sont fournies à l’API dans le cadre de `mip::ExecutionState`. `ComputeActions()` peut prendre en charge des opérations plus complexes que l’application d’une nouvelle étiquette à un document qui n’en a pas. L’exemple ci-dessous illustre la rétrogradation d’une étiquette d’une étiquette plus sensible à une étiquette moins sensible. Ce processus est simulé en lisant une chaîne de métadonnées séparées par des virgules et en fournissant l’API `mip::ExecutionState`via.

> [!NOTE]
> L’exemple utilise une fonction utilitaire appelée `SplitString()`. Vous pouvez trouver un exemple [ici](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/utils.cpp)

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and resolve newLabelId to mip::Label
sample::policy::ExecutionStateOptions options;
options.newLabel = mEngine->GetLabelById(newLabelId);

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

L’exemple ci-dessus peut entraîner plusieurs actions. Ces actions dépendent des étiquettes fournies en entrée et de leur configuration. Au minimum, il en résulte un seul `mip::MetadataAction` contenant les données à supprimer via `GetMetadataToRemove()`, ainsi que les données à ajouter via `GetMetadataToAdd()`.

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment [passer des événements d’audit à Azure information protection Analytics](concept-handler-policy-auditing-cpp.md)
- Téléchargez les [exemples d’API de stratégie à partir de GitHub et essayez l’API de stratégie](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
