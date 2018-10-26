---
title: Concepts – Gestionnaires de fichiers dans le kit SDK MIP
description: Cet article vous aidera à comprendre comment les gestionnaires de l’API de fichier sont créés et utilisés pour appeler des opérations.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6b2916a3937892353f4389a59b5e48356deda603
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453365"
---
# <a name="microsoft-information-protection-sdk---file-handler-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux gestionnaires de fichiers

Dans l’API de fichier du kit SDK MIP, `mip::FileHandler` expose toutes les différentes opérations qui peuvent être utilisées pour lire et écrire des étiquettes, ou une protection, sur un ensemble de types de fichiers pour lesquels la prise en charge est intégrée. 

## <a name="supported-file-types"></a>Types de fichiers pris en charge

- Formats de fichier Office basés sur OCP (Office 2010 et versions ultérieures)
- Formats de fichier Office hérités (Office 2007)
- PDF
- Prise en charge PFILE générique
- Fichiers prenant en charge Adobe XMP

## <a name="file-handler-functions"></a>Fonctions de gestionnaire de fichiers

`mip::FileHandler` expose des méthodes pour lire, écrire et supprimer des étiquettes et des informations de protection. Pour obtenir la liste complète, consultez la [référence de l’API](reference/class_mip_filehandler.md).

Dans cet article, nous couvrirons les méthodes suivantes :

- `GetLabelAsync()`
- `SetLabel()`
- `DeleteLabel()`
- `CommitAsync()`

## <a name="requirements"></a>Configuration requise

La création d’un `FileHandler` pour utiliser un fichier spécifique nécessite :

- Un `FileProfile`
- L’ajout d’un `FileEngine` au `FileProfile`
- Une classe qui hérite de `mip::FileHandler::Observer`

## <a name="create-a-file-handler"></a>Créer un gestionnaire de fichiers

La première étape requise dans la gestion de tous les fichiers dans l’API de fichier consiste à créer un objet `FileHandler`. Cette classe implémente toutes les fonctionnalités requises pour obtenir, définir, mettre à jour, supprimer et valider les modifications des étiquettes dans des fichiers.

Pour créer le `FileHandler`, il suffit d’appeler la fonction `CreateFileHandlerAsync` de `FileEngine` en utilisant le modèle de promesse/futur.

`CreateFileHandlerAsync` accepte trois paramètres : le chemin du fichier qui doit être lu ou modifié, le `mip::FileHandler::Observer` pour les notifications d’événements asynchrones et la promesse pour le `FileHandler`.

**Remarque :** La classe `mip::FileHandler::Observer` doit être implémentée dans une classe dérivée, car `CreateFileHandler` nécessite l’objet `Observer`. 

```cpp
auto createFileHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::FileHandler>>>();
auto createFileHandlerFuture = createFileHandlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, std::make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = createFileHandlerFuture.get();
```

Une fois l’objet `FileHandler` créé avec succès, des opérations de fichier (get/set/delete/commit) peuvent être effectuées.

## <a name="read-a-label"></a>Lire une étiquette

### <a name="metadata-requirements"></a>Conditions requises liées aux métadonnées

Il existe quelques conditions requises pour pouvoir lire correctement les métadonnées d’un fichier et les convertir afin de pouvoir les utiliser dans des applications.

- L’étiquette qui est lue doit encore exister dans le service O365. Si elle a été supprimée complètement, le kit SDK ne parviendra pas à obtenir des informations sur cette étiquette et renverra une erreur.
- Les métadonnées du fichier doivent être intactes. Ces métadonnées incluent :
  - Attribute1
  - Attribute2

### <a name="getlabelasync"></a>GetLabelAsync()

Après avoir créé le gestionnaire pour pointer sur un fichier spécifique, nous revenons au modèle de promesse/futur pour lire de façon asynchrone l’étiquette. La promesse est pour un objet `mip::ContentLabel` qui contient toutes les informations sur l’étiquette appliquée.

Après avoir instancié les objets `promise` et `future`, nous lisons l’étiquette en appelant `handler->GetLabelAsync()` et en fournissant `promise` comme paramètre unique. Enfin, l’étiquette peut être stockée dans un objet `mip::ContentLabel` que nous obtiendrons de `future`.

```cpp
auto loadPromise = std::make_shared<std::promise<std::shared_ptr<mip::ContentLabel>>>();
auto loadFuture = loadPromise->get_future();
handler->GetLabelAsync(loadPromise);
auto label = loadFuture.get();
```

Les données d’étiquette peuvent être lues à partir de l’objet `label` et transmises à n’importe quel(le) autre composant ou fonctionnalité dans l’application.

***

## <a name="set-a-label"></a>Définir une étiquette

La définition d’une étiquette est un processus en deux parties. Tout d’abord, après avoir créé un gestionnaire qui pointe sur le fichier en question, l’étiquette peut être définie en appelant `FileHandler->SetLabel()` avec deux paramètres.

```cpp
handler->SetLabel(label->GetId(), mip::LabelingOptions{ mip::AssignmentMethod::PRIVILEGED, "" });
```

Le premier paramètre est simplement l’identificateur d’étiquette issu de `ListLabelsAsync()`. Cette valeur peut être stockée dans une variable dédiée ou en lisant `mip::Label->GetId()`.

L’exemple ci-dessus suppose que nous avons stocké le `mip::Label` souhaité dans un objet appelé `label`.

### <a name="labeling-options"></a>Options d’étiquetage

Le second paramètre requis pour définir l’étiquette est un objet `mip::LabelingOptions` que nous créons inline lors de l’appel de la fonction `SetLabel()`. Il peut également être créé à l’avance.

`LabelingOptions` spécifie des informations supplémentaires sur l’étiquette comme le `AssignmentMethod` et la justification d’une action.

- `mip::AssignmentMethod` est simplement un énumérateur qui peut prendre trois valeurs : `STANDARD`, `PRIVILEGED` ou `AUTO`. Passez en revue la référence de `mip::AssignmentMethod` pour plus de détails.
- Une justification est nécessaire uniquement si la stratégie de service la requiert *et* lors de la diminution de la sensibilité *existante* d’un fichier.

```cpp
auto labelingOptions = mip::LabelingOptions();
labelingOptions.SetMethod(mip::AssignmentMethod::STANDARD);
labelingOptions.SetJustificationMessage("Because I made an educated decision based upon the contents of this file.");
```

Désormais, au lieu de créer des options d’étiquetage inline, il est possible de les passer à la fonction `SetLabel()`.

```cpp
handler->SetLabel(label->GetId(), labelingOptions);
```

Ayant à présent défini l’étiquette sur le fichier référencé par le gestionnaire, il reste une étape nécessaire pour valider la modification et écrire un fichier sur le disque ou créer un flux de sortie.

### <a name="commit-changes"></a>Valider les modifications

L’étape finale de validation de toute modification dans un fichier dans le kit SDK MIP consiste à **valider** la modification. Cette opération s’effectue à l'aide de la fonction `FileHandler->CommitAsync()`. 

Pour implémenter la fonction de validation, nous revenons à promesse/futur, en créant une promesse pour un `bool`. La fonction `CommitAsync()` retournera la valeur true si l’opération a réussi ou false si elle a échoué pour une raison quelconque. 

Après avoir créé les éléments `promise` et `future`, la fonction `CommitAsync()` est appelée et deux paramètres sont fournis : le chemin du fichier de sortie (`std::string`) et la promesse. Enfin, le résultat est obtenu en obtenant la valeur de l’objet `future`.

```cpp
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
auto wasCommitted = commitFuture.get();
```

**Important :** Le `FileHandler` ne mettra pas à jour et ne remplacera pas les fichiers existants. Il incombe au développeur d’implémenter le **remplacement** du fichier qui est en cours d’étiquetage. 

Si vous écrivez une étiquette pour **FileA.docx**, une copie du fichier, **FileB.docx**, sera créée avec l’étiquette appliquée. Un code doit être écrit pour supprimer/renommer **FileA.docx** et renommer **FileB.docx**.

***

## <a name="delete-a-label"></a>Supprimer une étiquette

```cpp
auto handler = mEngine->CreateFileHandler(filePath, std::make_shared<FileHandlerObserverImpl>());
handler->DeleteLabel(mip::AssignmentMethod::PRIVILEGED, "Label unnecessary.");
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();
handler->CommitAsync(outputFile, commitPromise);
```