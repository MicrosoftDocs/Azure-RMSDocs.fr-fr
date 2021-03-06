---
title: Démarrage rapide – Répertorier les étiquettes de sensibilité dans un locataire Microsoft Information Protection (MIP) à l’aide du kit SDK MIP C++
description: Guide de démarrage rapide illustrant comment utiliser le kit SDK C++ Microsoft Information Protection pour répertorier les étiquettes de sensibilité dans votre locataire.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 14b36ecee7fc49c5b50d627e6ef1ab95d436d7ee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865261"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Démarrage rapide : Lister les étiquettes de sensibilité (C++)

Ce guide de démarrage rapide vous montre comment utiliser l’API de fichier MIP pour répertorier les étiquettes de sensibilité configurées pour votre organisation.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation d’une application cliente (C++)](quick-app-initialization-cpp.md) pour créer une solution Visual Studio de démarrage. Ce guide de démarrage rapide « Répertorier les étiquettes de sensibilité » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Éventuellement : passez en revue les concepts liés aux [étiquettes de classification](concept-classification-labels.md).

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Ajouter une logique pour répertorier les étiquettes de sensibilité

Ajoutez une logique pour répertorier les étiquettes de sensibilité de votre organisation, à l’aide de l’objet de moteur de fichier.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application cliente (C++) ».

2. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Ajoutez la directive suivante `using` après `using mip::FileEngine;`, dans la partie supérieure du fichier :

   ```cpp
   using std::endl;
   ```

4. Vers la fin du corps `main()`, au-dessous de l’accolade fermante `}` du dernier bloc `catch` et au-dessus de `return 0;` (là où vous vous êtes arrêté dans le guide de démarrage rapide précédent), insérez le code suivant :

   ```cpp
   // List sensitivity labels
   cout << "\nSensitivity labels for your organization:\n";
   auto labels = engine->ListSensitivityLabels();
   for (const auto& label : labels)
   {
      cout << label->GetName() << " : " << label->GetId() << endl;

      for (const auto& child : label->GetChildren())
      {
        cout << "->  " << child->GetName() << " : " << child->GetId() << endl;
      }
   }
   system("pause");
   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>Créer un script PowerShell pour générer des jetons d’accès

Utilisez le script PowerShell suivant pour générer les jetons d’accès demandés par le SDK dans votre implémentation de `AuthDelegateImpl::AcquireOAuth2Token`. Le script utilise l’applet de commande `Get-ADALToken` à partir du module ADAL.PS que vous avez installé précédemment, dans « Installation et configuration du kit SDK MIP ».

1. Créez un fichier de script PowerShell (extension .ps1) et copiez/collez le script suivant dans ce fichier :

   - `$authority` et `$resourceUrl` sont mises à jour plus tard, dans la section suivante.
   - Mettez à jour `$appId` et `$redirectUri` avec les valeurs que vous avez spécifiées dans l’inscription de votre application Azure AD.

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Enregistrez le fichier de script afin de pouvoir l’exécuter ultérieurement, quand votre application cliente le demandera.

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Enfin, générez et testez votre application cliente.

1. Utilisez la touche F6 (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Vous pouvez réutiliser un jeton déjà généré, si vous y êtes invité plusieurs fois et que les valeurs demandées sont identiques.

3. Pour générer un jeton d’accès en réponse à l’invite, revenez à votre script PowerShell et :

   - Mettez à jour les variables `$authority` et `$resourceUrl`. Elles doivent correspondre aux valeurs qui sont spécifiées dans la sortie de la console à l’étape 2. Ces valeurs sont fournies par le kit SDK MIP dans le paramètre `challenge` de `AcquireOAuth2Token()` :
   - Exécutez le script PowerShell. L’applet de commande `Get-ADALToken` déclenche une invite d’authentification Azure AD similaire à l’exemple ci-dessous. Spécifiez le même compte que celui fourni dans la sortie de console à l’étape 2. Une fois la connexion réussie, le jeton d’accès sera placé dans le Presse-papiers.

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Après avoir collé le jeton d’accès dans l’invite de l’étape 2, la sortie de la console doit afficher les étiquettes de sensibilité, comme dans l’exemple suivant :

   ```console
   Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
   Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
   General : f42a3342-8706-4288-bd31-ebb85995028z
   Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
   Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z

   Press any key to continue . . .
   ```

   > [!NOTE]
   > Copiez et enregistrez l’ID d’une ou plusieurs des étiquettes de sensibilité (par exemple, `f42a3342-8706-4288-bd31-ebb85995028z`), car vous les utiliserez dans le guide de démarrage rapide suivant.

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C++

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | *Une exception s’est produite... le jeton d’accès est-il incorrect ou a-t-il expiré ?<br><br>L’appel de l’API a échoué : Échec de profile_add_engine_asyncprofile_add_engine_async avec : [classe mip::PolicySyncException] Échec de l’obtention de la stratégie, Échec de la requête avec le code d’état http : 401, x-ms-diagnostics: [2000001;reason="Le jeton OAuth envoyé avec la requête ne peut pas être analysé.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br><br>Appuyez sur une touche pour fermer cette fenêtre . . .* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Créer un script PowerShell pour générer des jetons d’accès](#create-a-powershell-script-to-generate-access-tokens) et regénérez le jeton d’accès, mettez de nouveau à jour `AcquireOAuth2Token()` et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |
| Étiquettes de sensibilité non configurées | Non applicable | Si votre projet est généré avec succès, mais que vous n’avez aucune sortie dans la fenêtre de console, assurez-vous que les étiquettes de sensibilité de votre organisation soient correctement configurées. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md), sous « Définir les paramètres de taxonomie et de protection des étiquettes » pour plus d’informations.  |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment répertorier les étiquettes de sensibilité pour votre organisation, consultez le guide de démarrage rapide suivant :

> [!div class="nextstepaction"]
> [Définir et obtenir une étiquette de sensibilité](quick-file-set-get-label-cpp.md)
