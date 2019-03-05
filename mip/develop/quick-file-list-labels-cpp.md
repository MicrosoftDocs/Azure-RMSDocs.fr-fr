---
title: Démarrage rapide – Répertorier les étiquettes de sensibilité dans un locataire Microsoft Information Protection (MIP) à l’aide du kit SDK MIP C++
description: Guide de démarrage rapide illustrant comment utiliser le kit SDK C++ Microsoft Information Protection pour répertorier les étiquettes de sensibilité dans votre locataire.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/18/2019
ms.author: mbaldwin
ms.openlocfilehash: 27b6c9039277feca033298520cc0fc18d239f037
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330982"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Démarrage rapide : Lister les étiquettes de sensibilité (C++)

Ce guide de démarrage rapide vous montre comment utiliser l’API de fichier MIP pour répertorier les étiquettes de sensibilité configurées pour votre organisation.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Complète [Guide de démarrage rapide : Initialisation de l’application cliente (C++)](quick-app-initialization-cpp.md) first, qui génère un solution Visual Studio starter. Ce guide de démarrage rapide « Répertorier les étiquettes de sensibilité » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Si vous le souhaitez : Révision [étiquettes de Classification](concept-classification-labels.md) concepts.

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Ajouter une logique pour répertorier les étiquettes de sensibilité

Ajoutez une logique pour répertorier les étiquettes de sensibilité de votre organisation, à l’aide de l’objet de moteur de fichier. 

1. Ouvrez la solution Visual Studio que vous avez créé dans la précédente « Guide de démarrage rapide : Initialisation de l’application cliente (C++) « article.

2. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet. 

3. Ajoutez la directive suivante `using` après `using mip::FileEngine;`, dans la partie supérieure du fichier :

   ```cpp
   using std::endl;
   ```

4. Vers la fin de la `main()` corps, sous l’accolade fermante `}` du dernier `catch` bloc et versions ultérieures `return 0;` (où vous vous êtes arrêté dans le Guide de démarrage rapide précédent), insérez le code suivant :

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

Utilisez le script PowerShell suivant pour générer des jetons d’accès, qui sont demandés par le SDK dans votre `AuthDelegateImpl::AcquireOAuth2Token` implémentation. Le script utilise l’applet de commande `Get-ADALToken` à partir du module ADAL.PS que vous avez installé précédemment, dans « Installation et configuration du kit SDK MIP ». 

1. Créez un fichier de script PowerShell (extension .ps1) et copiez/collez le script suivant dans ce fichier :

   - `$authority` et `$resourceUrl` sont mises à jour plus tard, dans la section suivante.
   - Mise à jour `$appId` et `$redirectUri`, pour faire correspondre les valeurs que vous avez spécifié dans l’inscription de votre application Azure AD. 

   ```powershell
   $authority = '<authority-url>'                   # Specified when SDK calls AcquireOAuth2Token() 
   $resourceUrl = '<resource-url>'                  # Specified when SDK calls AcquireOAuth2Token()
   $appId = '0edbblll-8773-44de-b87c-b8c6276d41eb'  # App ID of the Azure AD app registration
   $redirectUri = 'bltest://authorize'              # Redirect URI of the Azure AD app registration
   $response = Get-ADALToken -Resource $resourceUrl -ClientId $appId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:RefreshSession 
   $response.AccessToken | clip                     # Copy the access token text to the clipboard
   ```

2. Enregistrez le fichier de script afin de pouvoir l’exécuter ultérieurement, lorsque demandé par votre application cliente.

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Enfin, générez et testez votre application cliente. 

1. Utilisez la touche F6 (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute avec succès, l’application demande un jeton d’accès, chaque fois que le Kit de développement logiciel appelle votre `AcquireOAuth2Token()` (méthode). Vous pouvez réutiliser un jeton précédemment généré, si vous y êtes invité plusieurs fois et que les valeurs demandées sont les mêmes :

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token:
   ```

3. Pour générer un jeton d’accès de l’invite, revenez à votre script PowerShell et :

   - Mettez à jour les variables `$authority` et `$resourceUrl`. Elles doivent correspondre aux valeurs qui sont spécifiées dans la sortie de la console à l’étape 2. Ces valeurs sont fournies par le kit SDK MIP dans le paramètre `challenge` de `AcquireOAuth2Token()` :
     - `$authority` doit avoir la valeur `https://login.windows.net/common/oauth2/authorize`
     - `$resourceUrl` doit avoir la valeur `https://syncservice.o365syncservice.com/` ou `https://aadrm.com`
   - Exécutez le script PowerShell. Le `Get-ADALToken` applet de commande déclenche une invite d’authentification Azure AD, comme dans l’exemple ci-dessous. Spécifiez le même compte que celui fourni dans la sortie de console à l’étape 2. Une fois la connexion réussie, le jeton d’accès sera placé dans le Presse-papiers.

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

4. Après avoir collé le jeton d’accès dans l’invite de l’étape #2, votre sortie de la console doit afficher les étiquettes de sensibilité, similaires à l’exemple suivant :

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

### <a name="problems-during-execution-of-powershell-script"></a>Problèmes durant l’exécution du script PowerShell 

| Récapitulatif | Message d'erreur | Solution |
|---------|---------------|----------|
| URI de redirection incorrecte dans l’inscription de l’application ou un script PowerShell (AADSTS50011) |*AADSTS50011: La réponse à l’url spécifiée dans la demande ne correspond pas à l’URL de réponse configurées pour l’application : 'ac6348d6-0d2f-4786-af33-07ad46e69bfc'.* | Vérifiez l’URI de redirection utilisé, en effectuant l’une des opérations suivantes :<br><br><li>Mettez à jour l’URI de redirection dans la configuration de votre application Azure AD, pour qu’il corresponde à votre script PowerShell. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md#register-a-client-application-with-azure-active-directory) pour vérifier que vous avez correctement configuré la propriété de l’URI de redirection.<br><li>Mettez à jour la variable `redirectUri` dans votre script PowerShell, pour qu’elle corresponde à l’inscription de votre application. |
| Compte de connexion incorrect (AADSTS50020) | *AADSTS50020 : Compte d’utilisateur 'user@domain.com« fournisseur d’identité 'https://sts.windows.net/72f988bl-86f1-41af-91ab-2d7cd011db47/' n’existe pas dans le client, nom de l’organisation et ne peut pas accéder à l’application '0edbblll-8773-44de-b87c-b8c6276d41eb » dans ce locataire.* | Effectuez l'une des opérations suivantes :<br><br><li>Réexécutez le script PowerShell, mais veillez à utiliser un compte issu du même locataire où votre application Azure AD est inscrite.<br><li>Si votre compte de connexion était correct, votre session hôte PowerShell peut être déjà authentifiée sous un compte différent. Dans ce cas, quittez l’hôte de script, puis rouvrez-le et essayez de l’exécuter de nouveau.<br><li>Si vous utilisez ce guide de démarrage rapide avec une application web (au lieu d’une application native) et que vous avez besoin de vous connecter à l’aide d’un compte issu d’un autre locataire, veillez à ce que l’inscription de votre application Azure AD soit activée pour une utilisation multilocataire. Vous pouvez vérifier à l’aide de la fonctionnalité « Modifier le manifeste » dans l’inscription de l’application et vous assurer qu’elle spécifie `"availableToOtherTenants": true,`. |
| Autorisations incorrectes dans l’inscription de l’application (AADSTS65005) | *AADSTS65005 : Ressource non valide. Le client a demandé l’accès à une ressource qui n’est pas listée dans les autorisations demandées dans l’inscription d’application du client. ID d’application cliente : 0edbblll-8773-44de-b87c-b8c6276d41eb. Valeur de la ressource à partir de la demande : https://syncservice.o365syncservice.com/. ID d’application de ressource : 870c4f2e-85b6-4d43-bdda-6ed9a579b725. Liste de ressources valides à partir de l’inscription de l’application : 00000002-0000-0000-c000-000000000000.* | Mettez à jour les demandes d’autorisation dans la configuration de votre application Azure AD. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md#register-a-client-application-with-azure-active-directory) pour vérifier que vous avez correctement configuré les demandes d’autorisation dans l’inscription de votre application. |

### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C++

| Récapitulatif | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | *Une exception s’est produite... est le jeton d’accès incorrect/expiré ? <br> <br>Appel d’API a échoué : profile_add_engine_async a échoué avec : [classe mip::PolicySyncException] Échec de la stratégie lors de l’acquisition, la demande a échoué avec le code d’état http : 401, x-ms-diagnostics : [2000001 ; raison = « jeton OAuth envoyée avec la requête ne peut pas être analysée. » ; error_category = « invalid_token »], ID de corrélation : [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br> <br>Appuyez sur n’importe quelle touche pour fermer cette fenêtre...* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Mettre à jour la logique d’acquisition de jeton](#update-the-token-acquisition-logic-with-a-valid-access-token) et regénérez le jeton d’accès, mettez à jour `AcquireOAuth2Token()` de nouveau et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |
| Étiquettes de sensibilité non configurées | Non applicable | Si votre projet est généré avec succès, mais que vous n’avez aucune sortie dans la fenêtre de console, assurez-vous que les étiquettes de sensibilité de votre organisation soient correctement configurées. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md), sous « Définir les paramètres de taxonomie et de protection des étiquettes » pour plus d’informations.  |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment répertorier les étiquettes de sensibilité pour votre organisation, consultez le guide de démarrage rapide suivant :

> [!div class="nextstepaction"]
> [Définir et obtenir une étiquette de sensibilité](quick-file-set-get-label-cpp.md)
