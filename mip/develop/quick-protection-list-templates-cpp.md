---
title: Démarrage rapide - Répertorier les modèles de protection disponibles pour l’utilisateur authentifié dans un locataire Microsoft Information Protection (MIP) à l’aide du SDK MIP C++
description: Guide de démarrage rapide vous montrant comment utiliser l’API Protection du SDK C++ Microsoft Information Protection pour répertorier les modèles de protection disponibles pour un utilisateur (C++).
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/18/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 62f694248da10c7663c551240b204711b52163d5
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865067"
---
# <a name="quickstart-list-protection-templates-c"></a>Démarrage rapide : Répertorier les modèles de protection (C++)

Ce guide de démarrage rapide vous montre comment utiliser l’API Protection MIP pour répertorier les modèles de protection disponibles pour l’utilisateur.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Commencez par suivre le guide [Démarrage rapide : Initialisation d’une application cliente - API Protection (C++)](quick-protection-app-initialization-cpp.md), qui génère une solution Visual Studio de démarrage. Ce guide de démarrage rapide « Répertorier les modèles de protection » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Éventuellement : Passez en revue les concepts [Modèles RMS](/azure/information-protection/configure-policy-templates).

## <a name="add-logic-to-list-the-protection-templates"></a>Ajouter une logique pour répertorier les modèles de protection

Ajoutez une logique pour répertorier les modèles de protection disponibles pour un utilisateur, à l’aide de l’objet de moteur de protection.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application cliente - API Protection (C++) ».

2. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Ajoutez la directive suivante `using` après `using mip::ProtectionEngine;`, dans la partie supérieure du fichier :

   ```cpp
   using std::endl;
   ```

4. Vers la fin du corps `main()`, au-dessous de l’accolade fermante `}` du dernier bloc `catch` et au-dessus de `return 0;` (là où vous vous êtes arrêté dans le guide de démarrage rapide précédent), insérez le code suivant :

   ```cpp
    // List protection templates
    const shared_ptr<ProtectionEngineObserver> engineObserver = std::make_shared<ProtectionEngineObserver>();
    // Create a context to pass to 'ProtectionEngine::GetTemplateListAsync'. That context will be forwarded to the
    // corresponding ProtectionEngine::Observer methods. In this case, we use promises/futures as a simple way to detect
    // the async operation completes synchronously.
    auto loadPromise = std::make_shared<std::promise<vector<shared_ptr<mip::TemplateDescriptor>>>>();
    std::future<vector<shared_ptr<mip::TemplateDescriptor>>> loadFuture = loadPromise->get_future();
    engine->GetTemplatesAsync(engineObserver, loadPromise);
    auto templates = loadFuture.get();

    cout << "**_ Template List: " << endl;

    for (const auto& protectionTemplate : templates) {
        cout << "Name: " << protectionTemplate->GetName() << " : " << protectionTemplate->GetId() << endl;
    }

   ```

## <a name="create-a-powershell-script-to-generate-access-tokens"></a>Créer un script PowerShell pour générer des jetons d’accès

Utilisez le script PowerShell suivant pour générer les jetons d’accès demandés par le SDK dans votre implémentation de `AuthDelegateImpl::AcquireOAuth2Token`. Le script utilise l’applet de commande `Get-ADALToken` à partir du module ADAL.PS que vous avez installé précédemment, dans « Installation et configuration du kit SDK MIP ».

1. Créez un fichier de script PowerShell (extension .ps1) et copiez/collez le script suivant dans ce fichier :

   - `$authority` et `$resourceUrl` sont mises à jour plus tard, dans la section suivante.
   - Mettez à jour `$appId` et `$redirectUri` avec les valeurs que vous avez spécifiées dans l’inscription de votre application Azure AD.

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token()
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '<app-ID>'                              # App ID of the Azure AD app registration
   $redirectUri = '<redirect-uri>'                  # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Enregistrez le fichier de script afin de pouvoir l’exécuter ultérieurement, quand votre application cliente le demandera.

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Enfin, générez et testez votre application cliente.

1. Utilisez Ctrl+Maj+b (_*Générer la solution **) pour générer votre application cliente. Si vous n’obtenez pas d’erreur de génération, utilisez F5 (** Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Vous pouvez réutiliser un jeton précédemment généré, si vous y êtes invité plusieurs fois et que les valeurs demandées sont les mêmes :

3. Pour générer un jeton d’accès en réponse à l’invite, revenez à votre script PowerShell et :

   - Mettez à jour les variables `$authority` et `$resourceUrl`. Elles doivent correspondre aux valeurs qui sont spécifiées dans la sortie de la console à l’étape 2.
   - Exécutez le script PowerShell. L’applet de commande `Get-ADALToken` déclenche une invite d’authentification Azure AD similaire à l’exemple ci-dessous. Spécifiez le même compte que celui fourni dans la sortie de console à l’étape 2. Une fois la connexion réussie, le jeton d’accès sera placé dans le Presse-papiers.

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Après avoir collé le jeton d’accès dans l’invite de l’étape 2, la sortie de la console doit afficher les modèles de protection, comme dans l’exemple suivant :

   ```console
   **_ Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720

   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.

   Press any key to continue . . .
   ```

   > [!NOTE]
   > Copiez et enregistrez l’ID d’un ou plusieurs des modèles de protection (par exemple, `f42a3342-8706-4288-bd31-ebb85995028z`), car vous les utiliserez dans le guide de démarrage rapide suivant.

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C++

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | _Une exception s’est produite… Le jeton d’accès est-il incorrect ou a-t-il expiré ?<br><br>Échec de l’appel d’API : Échec de profile_add_engine_async avec : [classe mip::PolicySyncException] Échec de la récupération de la stratégie, Échec de la requête avec le code de statut HTTP : 401, x-ms-diagnostics : [2000001;reason="Impossible d’analyser le jeton OAuth soumis avec la requête.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br><br>Appuyez sur n’importe quelle touche pour fermer cette fenêtre. . .* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Créer un script PowerShell pour générer des jetons d’accès](#create-a-powershell-script-to-generate-access-tokens) et regénérez le jeton d’accès, mettez de nouveau à jour `AcquireOAuth2Token()` et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris à répertorier les modèles de protection disponibles pour un utilisateur authentifié, passez au prochain démarrage rapide :

> [!div class="nextstepaction"]
> [Chiffrer et déchiffrer du texte](quick-protection-encrypt-decrypt text-cpp.md)