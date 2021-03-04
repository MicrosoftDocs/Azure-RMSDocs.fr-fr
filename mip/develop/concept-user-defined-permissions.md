---
title: 'Concepts : concepts de base du kit de développement logiciel MIP-autorisations définies par l’utilisateur.'
description: Cet article vous aidera à comprendre le concept du kit de développement logiciel (SDK) principal, appelé autorisations définies par l’utilisateur.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/02/2021
ms.author: tommos
ms.openlocfilehash: 47939a37616173c456d1588e95e36f8a978ed32d
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844181"
---
# <a name="microsoft-information-protection-sdk---user-defined-permissions"></a>Kit de développement logiciel (SDK) Microsoft Information Protection-autorisations définies par l’utilisateur

Le kit de développement logiciel (SDK) Microsoft Information Protection prend en charge deux types principaux d’autorisations pilotées par étiquette : basées sur un modèle et définies par l’utilisateur.

- **Autorisations basées sur un modèle :** Ces droits sont définis par l’administrateur des libellés dans le centre de sécurité et conformité. Ces étiquettes sont gérées de manière centralisée, et les modifications apportées à la configuration affectent les utilisateurs qui possèdent déjà des copies des fichiers. Par exemple, si l’administrateur supprime un utilisateur de la liste des utilisateurs autorisés, cet utilisateur n’aura plus accès aux données protégées la prochaine fois qu’il tentera de récupérer une licence.

- **Autorisations définies** par l’utilisateur : ces droits sont définis **au moment de l’étiquetage** par l’utilisateur final ou l’application. Les autorisations sont transmises au kit de développement logiciel (SDK) MIP sous la forme d’une collection de mappages utilisateur à rôle ou utilisateurs-droits. Ces droits sont écrits dans la licence de publication du document protégé et, à la différence des autorisations basées sur un modèle, ne peuvent pas être gérés de manière centralisée ni modifiés après le partage sans accès direct et modification du document.

## <a name="users-rights-and-roles"></a>Utilisateurs, droits et rôles

Étant donné que les droits sont censés être définis par l’utilisateur au moment de l’étiquetage, votre application doit fournir une interface pour permettre à l’utilisateur ou au service de fournir une entrée sur les adresses de messagerie et les droits ou les rôles dont dispose l’utilisateur. Cette configuration s’effectue en passant une collection d' `UserRoles` objets ou `UserRights` qui définissent spécifiquement qui doit disposer du niveau d’accès aux documents.

```csharp
// Create a List<string> of the first set of permissions. 
List<string> users = new List<string>()
{
    "alice@contoso.com",
    "bob@contoso.com"
};

// Create a List<string> of the Rights the above users should have. 
List<string> rights = new List<string>()
{
    Rights.View,
    Rights.Edit                
};

// Create a UserRights object containing the defined users and rights.
UserRights userRights = new UserRights(users, rights);

// Add them to a new List<UserRights>
List<UserRights> userRightsList = new List<UserRights>()
{
    userRights
};
```

Le résultat est que vous disposez d’une `List<UserRights>` collection spécifiant que Alice et Bob disposent d’une vue et d’une modification sur le fichier protégé. Pour ajouter d’autres utilisateurs avec un *autre* jeu d’autorisations, répétez le processus de création d’un deuxième `UserRights` objet, en passant les nouveaux utilisateurs et autorisations, puis ajoutez à la `List<UserRights>` collection en appelant `userRightsList.Add(userRights2)` .

Ce modèle est également vrai pour `UserRoles` et peut être implémenté simplement en remplaçant les **droits** par des **rôles** et en créant un `List<UserRoles>` regroupement.

### <a name="apply-protection"></a>Appliquer la protection

La définition de la protection peut être obtenue en créant un `ProtectionDescriptor` objet à partir de l' `List<UserRights>` `List<UserRoles>` objet ou, puis en le passant à `FileHandler.SetProtection()` . Enfin, validez la modification apportée au fichier pour écrire un nouveau fichier. 

### <a name="when-to-apply-protection-to-files"></a>Quand appliquer la protection aux fichiers

Lorsque vous définissez une étiquette via `FileHandler.SetLabel()` le kit de développement logiciel (SDK) MIP, toutes les opérations doivent être appliquées et appliquer une protection. Lorsque l’étiquette est configurée pour des autorisations définies par l’utilisateur (UDP), votre application n’a aucun moyen de savoir à l’avance que l’étiquette est une étiquette UDP. Le SDK MIP surface ces informations en levant une exception du type `Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException` . Votre `FileHandler` code doit intercepter cette exception, puis déclencher votre utilisateur ou votre interface de service pour définir les autorisations personnalisées. Une fois terminé, vous serez en mesure de définir la protection. L’exemple suivant illustre le modèle de bout en bout, mais suppose que vous avez déjà implémenté une fonction pour générer l' `List<UserRights>` objet.

```csharp
try
{
    // Attempt to set the label. If it's a UDP label, this will throw. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());
}

catch (Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException)
{
    // Assumes you've create a function that returns the List<UserRights> as previously detailed. 
    List<UserRights> userRightsList = GetUserRights();

    // Create a ProtectionDescriptor using the set of UserRights.
    ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(userRightsList);
    
    // Apply protection to the file using the new ProtectionDescriptor. 
    handler.SetProtection(protectionDescriptor, new ProtectionSettings());

    // Set the label. This will now succeed as protection has been defined. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());

    // Commit the change. 
    var result = Task.Run(async () => await handler.CommitAsync("myFileOutput.xlsx")).Result;
}
```

## <a name="custom-protection"></a>Protection personnalisée

Ce processus peut également être utilisé pour définir la protection uniquement en définissant la protection et en ignorant l' `SetLabel()` étape. Si votre application n’a pas besoin d’appliquer une étiquette, le gestionnaire d’exceptions n’est pas obligatoire et la protection peut être définie en suivant le `ProtectionDescriptor`  ->  `SetProtection()`  ->  `CommitAsync()` modèle.

## <a name="next-steps"></a>Étapes suivantes

- [Consultez la section Configuration du chiffrement des étiquettes dans la documentation Microsoft 365.](/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide#understand-how-the-encryption-works)