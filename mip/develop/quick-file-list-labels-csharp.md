---
title: Démarrage rapide – Lister les étiquettes de sensibilité dans un locataire Microsoft Information Protection (MIP) à l’aide du wrapper C# du SDK MIP
description: Guide de démarrage rapide illustrant comment utiliser le wrapper C# du SDK Microsoft Information Protection (MIP) pour lister les étiquettes de sensibilité dans votre locataire.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 9f12ff856e7d70c76e3c89700d05aeb653d030cd
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555277"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Démarrage rapide : Lister les étiquettes de sensibilité (C#)

Ce guide de démarrage rapide vous montre comment utiliser l’API de fichier du SDK MIP afin de lister les étiquettes de sensibilité configurées pour votre organisation.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Initialisation d’une application cliente (C#)](quick-app-initialization-csharp.md) pour créer une solution Visual Studio de démarrage. Ce guide de démarrage rapide « Répertorier les étiquettes de sensibilité » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Éventuellement : passez en revue les concepts liés aux [étiquettes de classification](concept-classification-labels.md).

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Ajouter une logique pour répertorier les étiquettes de sensibilité

Ajoutez une logique pour répertorier les étiquettes de sensibilité de votre organisation, à l’aide de l’objet de moteur de fichier. 

1. Ouvrez la solution Visual Studio que vous avez créée dans l’article précédent « Démarrage rapide : Initialisation d’une application cliente (C#) ».

2. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la méthode `Main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet. 

3. Vers la fin du corps `Main()`, au-dessous de la section d’arrêt d’application de la fonction `Main()` (là où vous vous êtes arrêté dans le démarrage rapide précédent), insérez le code suivant :

  ```csharp
  // List sensitivity labels from fileEngine and display name and id  
  foreach(var label in fileEngine.SensitivityLabels)
  {
      Console.WriteLine(string.Format("{0} : {1}", label.Name, label.Id));

      if (label.Children.Count != 0)
      {
          foreach (var child in label.Children)
          {
              Console.WriteLine(string.Format("{0}{1} : {2}", "\t",child.Name, child.Id));
          }
      }
  }
  ```

## <a name="build-and-test-the-application"></a>Générer et tester l’application

Enfin, générez et testez votre application cliente.

1. Utilisez CTRL-MAJ-B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application *peut* demander une authentification via ADAL chaque fois que le SDK appelle la méthode `AcquireToken()`. Si les informations d’identification ont déjà été mises en cache, vous n’êtes pas invité à vous connecter et à voir la liste des étiquettes. 

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Après l’authentification, la sortie de la console doit afficher les étiquettes de sensibilité, comme dans l’exemple suivant :

  ```console
  Personal : 73c47c6a-eb00-4a6a-8e19-efaada66dee6
  Public : 73254501-3d5b-4426-979a-657881dfcb1e
  General : da480625-e536-430a-9a9e-028d16a29c59
  Confidential : 569af77e-61ea-4deb-b7e6-79dc73653959
        Recipients Only (C) : d98c4267-727b-430e-a2d9-4181ca5265b0
        All Employees (C) : 2096f6a2-d2f7-48be-b329-b73aaa526e5d
        Anyone (not protected) (C) : 63a945ec-1131-420d-80da-2fedd15d3bc0
  Highly Confidential : 905845d6-b548-439c-9ce5-73b2e06be157
        Recipients Only : 05ee72d9-1a75-441f-94e2-dca5cacfe012
        All Employees : 922b06ef-044b-44a3-a8aa-df12509d1bfe
        Anyone (not protected) : c83fc820-961d-40d4-ba12-c63f72a970a3
  Press a key to continue.
  ```

   > [!NOTE]
   > Copiez et enregistrez l’ID d’une ou plusieurs des étiquettes de sensibilité (par exemple, `f42a3342-8706-4288-bd31-ebb85995028z`), car vous les utiliserez dans le guide de démarrage rapide suivant.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="problems-during-execution-of-c-application"></a>Problèmes durant l’exécution de l’application C#

| Résumé | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | *Une exception s’est produite... le jeton d’accès est-il incorrect ou a-t-il expiré ?<br><br>L’appel de l’API a échoué : Échec de profile_add_engine_asyncprofile_add_engine_async avec : [classe mip::PolicySyncException] Échec de l’obtention de la stratégie, Échec de la requête avec le code d’état http : 401, x-ms-diagnostics: [2000001;reason="Le jeton OAuth envoyé avec la requête ne peut pas être analysé.";error_category="invalid_token"], correlationId:[35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br><br>Appuyez sur une touche pour fermer cette fenêtre . . .* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Générer et tester l’application](#build-and-test-the-application) et regénérez le jeton d’accès, mettez à jour `AcquireOAuth2Token()` de nouveau et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |
| Étiquettes de sensibilité non configurées | Non applicable | Si votre projet est généré avec succès, mais que vous n’avez aucune sortie dans la fenêtre de console, assurez-vous que les étiquettes de sensibilité de votre organisation soient correctement configurées. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md), sous « Définir les paramètres de taxonomie et de protection des étiquettes » pour plus d’informations.  |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment répertorier les étiquettes de sensibilité pour votre organisation, consultez le guide de démarrage rapide suivant :

> [!div class="nextstepaction"]
> [Définir et obtenir une étiquette de sensibilité](quick-file-set-get-label-csharp.md)
