---
title: Démarrage rapide - Répertorier les modèles de protection disponibles pour l’utilisateur authentifié dans un locataire Microsoft Information Protection (MIP) à l’aide du wrapper C# SDK MIP
description: Ce démarrage rapide vous montre comment utiliser le wrapper C# de l’API Protection du SDK Microsoft Information Protection pour répertorier les modèles de protection disponibles pour un utilisateur.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.custom: has-adal-ref
ms.openlocfilehash: ec6439747b7a826a09851739a96ccdec3f5705f4
ms.sourcegitcommit: 298843953f9792c5879e199fd1695abf3d25aa70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2020
ms.locfileid: "82972116"
---
# <a name="quickstart-list-templates-c"></a>Démarrage rapide : Répertorier les modèles (C#)

Ce guide de démarrage rapide vous montre comment utiliser l’API Protection du SDK MIP pour répertorier les modèles de protection disponibles pour l’utilisateur.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation d’une application cliente - API Protection (C#)](quick-protection-app-initialization-csharp.md) pour créer une solution Visual Studio de démarrage. Ce guide de démarrage rapide « Répertorier les modèles de protection » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Éventuellement : Passez en revue les concepts [Modèles RMS](https://docs.microsoft.com/azure/information-protection/configure-policy-templates).

## <a name="add-logic-to-list-the-protection-templates"></a>Ajouter une logique pour répertorier les modèles de protection

Ajoutez une logique pour répertorier les modèles de protection disponibles pour un utilisateur, à l’aide de l’objet de moteur de protection.

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application cliente - API Protection (C#) ».

2. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

3. Vers la fin du corps `Main()`, au-dessous de la section d’arrêt d’application de la fonction `Main()` (là où vous vous êtes arrêté dans le démarrage rapide précédent), insérez le code suivant :

  ```csharp
  // List protection templates using protectionEngine and display the list

  var templates=protectionEngine.GetTemplates();

  for(int i = 0; i < templates.Count; i++)
  {
      Console.WriteLine("{0}: {1}", i.ToString(), templates[i].Name + " : " + templates[i].Id);
  }

  Console.WriteLine("Press a key to continue...");
  ```

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Enfin, générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application *peut* demander une authentification via ADAL chaque fois que le SDK appelle la méthode `AcquireToken()`. Si les informations d’identification ont déjà été mises en cache, vous n’êtes pas invité à vous connecter et à voir la liste des étiquettes.

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Après l’authentification, la sortie de la console doit afficher les modèles de protection pour l’utilisateur authentifié, comme dans l’exemple suivant :

  ```console
  0: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
  1: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
  2: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
  3: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
  Press a key to continue.
  ```

   > [!NOTE]
   > Copiez et enregistrez l’ID d’un ou plusieurs des modèles de protection (par exemple, `bb7ed207-046a-4caf-9826-647cff56b990`), car vous les utiliserez dans le guide de démarrage rapide suivant.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C#

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | *Une exception s’est produite... le jeton d’accès est-il incorrect ou a-t-il expiré ?<br><br>L’appel de l’API a échoué : Échec de profile_add_engine_asyncprofile_add_engine_async avec : [classe mip::PolicySyncException] Échec de l’obtention de la stratégie, Échec de la requête avec le code d’état http : 401, x-ms-diagnostics: [2000001;reason="Le jeton OAuth envoyé avec la requête ne peut pas être analysé.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br><br>Appuyez sur une touche pour fermer cette fenêtre . . .* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Générer et tester l’application](#build-and-test-the-application) et regénérez le jeton d’accès, mettez à jour `AcquireOAuth2Token()` de nouveau et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris à répertorier les modèles de protection disponibles pour l’utilisateur authentifié, passez au prochain démarrage rapide :

> [!div class="nextstepaction"]
> [Démarrage rapide - Chiffrer et déchiffrer du texte](quick-protection-encrypt-decrypt-text-csharp.md)
