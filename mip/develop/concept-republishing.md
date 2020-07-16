---
title: Republication dans le kit de développement logiciel MIP
description: Cet article vous aidera à comprendre le scénario de réutilisation du gestionnaire de protection pour les scénarios de republication.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: v-anikep
ms.openlocfilehash: 499e4881175920fdf3127856fa9056b10ae22b79
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86405212"
---
# <a name="republishing-c"></a>Republication (C++)

## <a name="overview"></a>Vue d’ensemble

Cette vue d’ensemble porte sur la republication dans le kit de développement logiciel MIP. il s’agit d’un scénario spécifique qui se produit lorsqu’une application doit autoriser un utilisateur à modifier le fichier, mais souhaite conserver les informations de [licence de publication](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/licenses-and-certificates-and-how-ad-rms-protects-and-consumes/ba-p/247309) d’origine concernant le propriétaire, les droits, la clé de contenu, etc.

Le modèle peut ressembler à ceci :

- Un utilisateur ouvre un document protégé pour le modifier.
- L’utilisateur doit uniquement être autorisé à modifier le fichier s’il dispose des droits appropriés.
- L’utilisateur modifie le document, puis l’enregistre.

Le pseudocode du SDK MIP pour accomplir cette tâche peut se présenter comme suit :

- Créez un `mip::FileHandler` qui pointe vers le fichier cible.
- Stocke le `mip::ProtectionHandler` exposé par `mip::FileHandler` la `GetProtection()` méthode de.
- Vérifiez que l’utilisateur dispose des droits d' **édition** en appelant la `AccessCheck()` méthode.
- Utilisez `mip::FileHandler` `GetDecryptedTemporaryFileAsync()` ou `GetDecryptedTemporaryStreamAsync()` pour obtenir une sortie déchiffrée temporaire.
- Modifiez le contenu du fichier temporaire ou du flux, puis enregistrez.
- Créez une instance de qui `mip::FileHandler` pointe vers le fichier temporaire et utilisez la `SetProtection()` méthode, en fournissant le stocké `mip::ProtectionHandler` en tant que paramètre.
- Validez la modification.

L’utilisation du `mip::ProtectionHandler` à partir du fichier d’origine, le propriétaire, l’ID de contenu, la clé de contenu, etc., seront conservées dans le document modifié. Ce scénario de republication nécessite que l’application gère une référence à l’original `mip::ProtectionHandler` .

## <a name="implementation"></a>Implémentation

Comme nous l’avons vu précédemment, la `mip::FileHandler` classe expose des méthodes pour la lecture, l’écriture et la suppression des étiquettes et des informations de protection. Pour obtenir la liste complète des opérations prises en charge, consultez les informations de référence sur les [API](./reference/class_mip_filehandler.md#summary).

Ce scénario utilise les méthodes suivantes `mip::FileHandler` :

- `GetProtection()`
- `CommitAsync()`
- `GetDecryptedTemporaryFileAsync()`
- `SetProtection()`

Le scénario utilise également `mip::ProtectionHandler` , qui expose les fonctions pour le chiffrement et le déchiffrement de flux et de mémoires tampons protégés, l’exécution de contrôles d’accès, l’obtention de la licence de publication et l’obtention d’attributs à partir des informations protégées. La `AccessCheck()` méthode sera utilisée pour valider le fait que l’utilisateur dispose des droits nécessaires pour modifier le fichier.

Pour mener à bien ce scénario de reprotection, passez en revue les Démarrages rapides sous « étapes suivantes » et assurez-vous que l’application est générée et peut répertorier correctement les étiquettes.

## <a name="create-a-protection-handler-from-the-file-and-decrypt-the-file"></a>Créer un gestionnaire de protection à partir du fichier et déchiffrer le fichier

`mip::ProtectionHandler`expose les fonctions pour le chiffrement et le déchiffrement de flux et de mémoires tampons protégés, l’exécution de contrôles d’accès, l’obtention de la licence de publication et l’obtention d’attributs à partir des informations protégées. `mip::ProtectionHandler`les objets sont construits en fournissant un ProtectionDescriptor ou une licence de publication sérialisée. Pour ce cas d’usage, nous utiliserons implicitement la licence de publication, car la licence de publication sera utilisée lors du déchiffrement de contenu déjà protégé ou de la protection du contenu où la licence a déjà été construite.

`mip::FileHandler`expose une méthode nommée `GetProtection()` qui récupère `mip::ProtectionHandler` à partir du fichier associé à `mip::FileHandler` . Une fois que l' `mip::ProtectionHandler` objet est récupéré, le même peut être utilisé pour valider les niveaux d’accès de l’utilisateur pour le fichier, déchiffrer le fichier et chiffrer ultérieurement le fichier une fois qu’il est modifié.

`mip::ProtectionHandler``AccessCheck()`est utilisé pour valider le fait que l’utilisateur dispose d’un droit spécifique au fichier et retourne une réponse booléenne, en fonction du résultat. Par exemple, pour vérifier que l’utilisateur dispose des droits de modification, appelez la méthode en passant la valeur « EDIT ». Si le résultat est *true*, autorisez l’utilisateur à modifier le fichier. Une fois le droit de **modification** vérifié, `mip::FileHandler` Utilisez `GetDecryptedTemporaryFileAsync()` pour récupérer le fichier déchiffré temporaire.

Pour plus d’informations sur les différents droits d’utilisateur, consultez [droits d’utilisateur pour Azure information protection](/azure/information-protection/configure-usage-rights).

 > [!IMPORTANT]
 > Les vérifications d’accès et l’application sont purement et simplement le développeur de l’application. Un utilisateur disposant des droits d’affichage peut déchiffrer les informations protégées. C’est à l’application de valider l’ensemble des droits accordés à l’utilisateur et d’appliquer ces droits par le biais de contrôles information protection tels que l’interdiction de copier, de modifier ou de créer des captures d’écran. L’impossibilité d’implémenter correctement des contrôles de protection peut entraîner l’exposition d’informations sensibles.

## <a name="save-and-publish-the-edited-file-by-applying-protection"></a>Enregistrer et publier le fichier modifié en appliquant la protection

Une fois le fichier déchiffré, le fichier peut être modifié. Une fois l’opération de modification terminée, les modifications peuvent être validées. Créez un `IFileHandler` objet à l’aide du fichier temporaire ci-dessus pour gérer le fichier validé. Le fichier temporaire peut ensuite être protégé à l’aide de l' `IProtectionHandler` objet récupéré à partir du fichier d’origine.

## <a name="next-steps"></a>Étapes suivantes

- [Passer en revue le démarrage rapide de republication pour C++](quick-file-republishing-cpp.md)
- [Passer en revue le démarrage rapide de republication pour C #](quick-file-republishing-csharp.md)