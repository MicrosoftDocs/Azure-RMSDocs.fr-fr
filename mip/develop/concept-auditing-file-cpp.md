---
title: Concepts - Audit dans l’API de fichier du kit SDK Microsoft Information Protection
description: Cet article vous aide à comprendre comment utiliser le kit SDK Microsoft Information Protection pour envoyer les événements d’audit de l’API de fichier aux fonctionnalités d’analyse Azure Information Protection.
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: df67886f53d697e47f6e812cdcbbac394acaa98d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "69884754"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>Audit dans l’API de fichier du kit SDK MIP

Le portail d’administration Azure Information Protection permet d’accéder aux rapports de l’administrateur. Ces rapports fournissent une visibilité sur les étiquettes que les utilisateurs appliquent, manuellement ou automatiquement, sur les applications ou services qui ont intégré le kit de développement logiciel (SDK) MIP. Les partenaires de développement qui utilisent le kit de développement logiciel (SDK) peuvent activer cette fonctionnalité pour exposer les informations de leurs applications dans les rapports des clients.

## <a name="event-types"></a>Types d'événement

Il existe trois types d’événement pouvant être envoyés via le kit SDK aux fonctionnalités d’analyse Azure Information Protection. **Événements de pulsation**, **événements de détection** et **événements de changement**

### <a name="heartbeat-events"></a>Événements de pulsation

Les événements de pulsation sont générés automatiquement pour toutes les applications auxquelles l’API de fichier a été intégrée. Les événements de pulsation sont les suivants :

* TenantId
* Heure de la génération
* Nom d'utilisateur principal
* Nom de la machine sur laquelle l’audit a été généré
* Nom du processus
* Plate-forme
* ID d’application - Correspond à l’ID d’application Azure AD.

Ces événements permettent de détecter les applications de votre entreprise qui utilisent le kit SDK Microsoft Information Protection.

### <a name="discovery-events"></a>Événements de détection

Les événements de détection fournissent des détails sur les informations étiquetées qui sont lues ou consommées par l’API de fichier. Ces événements sont utiles, car ils indiquent les appareils et leur localisation, ainsi que les utilisateurs qui accèdent aux informations d’une organisation.

Vous pouvez envoyer ces événements aux fonctionnalités d’analyse Azure Information Protection en affectant la valeur true au paramètre `AuditDiscoveryEnabled` durant la création de `mip::FileHandler`. De plus, un identificateur de contenu qui identifie le fichier dans un format lisible est fourni. Il est recommandé d’utiliser le chemin de fichier pour cet identificateur.

Dans l’exemple ci-dessous, `mip::FileHandler` est créé, et la détection d’audit est activée. La méthode `CreateFileHandler()` est appelée sur `mip::FileEngine`, et `AuditDiscoveryEnabled` prend la valeur true. Une fois que `FileHanlder` a lu l’étiquette, un événement de détection d’audit est généré.

```cpp
// Create FileHandler with discovery enabled
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(inputFilePath, actualFilePath, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>Événements de changement

Les événements de changement fournissent des informations sur le fichier, l’étiquette appliquée ou changée, ainsi que les justifications fournies par l’utilisateur. Les événements de changement sont générés via l’appel de `NotifyCommitSuccessful()` sur `mip::FileHandler`, une fois qu’un changement a été correctement validé dans un fichier.

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
handler->SetLabel(labelId, labelingOptions, mip::ProtectionSettings());
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();

// CommitAsync() returns a bool. If the change was successful, call NotifyCommitSuccessful().
fileHandler->CommitAsync(outputFile, commitPromise);
if(commitFuture.get()) {

    // Submit audit event.
    handler->NotifyCommitSuccessful(contentId);
}
```

## <a name="audit-dashboard"></a>Tableau de bord d’audit

Les événements envoyés au pipeline d’audit Azure Information Protection apparaissent dans les rapports sur https://portal.azure.com. 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’expérience d’audit dans Azure Information Protection, consultez le [blog de l’annonce préliminaire sur la communauté Tech](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854).
