---
title: Guide de démarrage rapide - liste des étiquettes de sensibilité d’un client Microsoft Information Protection (MIP) à l’aide du SDK MIP C# Wrapper
description: Un guide de démarrage rapide vous montrant comment utiliser le SDK Microsoft Information Protection C# wrapper pour répertorier les étiquettes de sensibilité dans votre client.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.date: 01/04/2019
ms.author: bryanla
ms.openlocfilehash: 52432a1d6be683d6ed40d95e653ef42353b58400
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651892"
---
# <a name="quickstart-list-sensitivity-labels-c"></a>Démarrage rapide : Liste des étiquettes de sensibilité (C#)

Ce démarrage rapide vous montre comment utiliser l’API de fichier du SDK MIP pour répertorier les étiquettes de sensibilité configurés pour votre organisation.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Complète [Guide de démarrage rapide : Initialisation de l’application cliente (C#)](quick-app-initialization-csharp.md) first, qui génère un solution Visual Studio starter. Ce guide de démarrage rapide « Répertorier les étiquettes de sensibilité » s’appuie sur le précédent, qui permet de créer correctement la solution de démarrage.
- Si vous le souhaitez : Révision [étiquettes de Classification](concept-classification-labels.md) concepts.

## <a name="add-logic-to-list-the-sensitivity-labels"></a>Ajouter une logique pour répertorier les étiquettes de sensibilité

Ajoutez une logique pour répertorier les étiquettes de sensibilité de votre organisation, à l’aide de l’objet de moteur de fichier. 

1. Ouvrez la solution Visual Studio que vous avez créé dans la précédente « Guide de démarrage rapide : Initialisation de l’application cliente (C#) « article.

2. À l’aide de **l’Explorateur de solutions**, ouvrez le fichier .cs dans votre projet qui contient l’implémentation de la `Main()` (méthode). Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet. 

3. Vers la fin de la `Main()` corps, sous l’accolade fermante `}` de la `Main()` (où vous vous êtes arrêté dans le Guide de démarrage rapide précédent) de la fonction, insérez le code suivant :

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

1. Utilisez CTRL-MAJ-B (**générer la Solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet génère et s’exécute correctement, l’application *peut* demander l’authentification via la bibliothèque ADAL chaque fois que les appels de kit de développement logiciel votre `AcquireToken()` (méthode). Si les informations d’identification mises en cache existent déjà, vous ne sont pas invité à se connecter et afficher la liste des étiquettes. 

     [![Acquisition par Visual Studio d’un jeton de connexion](media/quick-file-list-labels-cpp/acquire-token-sign-in.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in.png#lightbox)

   - Vous devrez peut-être également donner votre consentement pour autoriser l’application à accéder aux API MIP, lors de son exécution sous le compte de connexion. Cela se produit lorsque l’inscription de l’application Azure AD n’est pas préalablement consentie (comme indiqué dans « Installation et configuration du kit SDK MIP »), ou que vous vous connectez avec un compte issu d’un autre locataire (autre que celui où votre application est inscrite). Cliquez simplement sur **Accepter** pour enregistrer votre consentement.

     [![Consentement Visual Studio](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png)](media/quick-file-list-labels-cpp/acquire-token-sign-in-consent.png#lightbox)

3. Une fois l’authentification, votre sortie de la console doit afficher les étiquettes de sensibilité, similaires à l’exemple suivant :

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

### <a name="problems-during-execution-of-c-application"></a>Problèmes lors de l’exécution de C# application

| Récapitulatif | Message d'erreur | Solution |
|---------|---------------|----------|
| Jeton d'accès incorrect | *Une exception s’est produite... est le jeton d’accès incorrect/expiré ? <br> <br>Appel d’API a échoué : profile_add_engine_async a échoué avec : [classe mip::PolicySyncException] Échec de la stratégie lors de l’acquisition, la demande a échoué avec le code d’état http : 401, x-ms-diagnostics : [2000001 ; raison = « jeton OAuth envoyée avec la requête ne peut pas être analysée. » ; error_category = « invalid_token »], ID de corrélation : [35bc0023-3727-4eff-8062-000006d5d672]'<br><br>C:\VSProjects\MipDev\Quickstarts\AppInitialization\x64\Debug\AppInitialization.exe (processus 29924) s’est arrêté avec le code 0.<br> <br>Appuyez sur n’importe quelle touche pour fermer cette fenêtre...* | Si votre projet est généré avec succès, mais que vous voyez une sortie similaire à gauche, vous avez probablement un jeton non valide ou expiré dans votre méthode `AcquireOAuth2Token()`. Revenez à [Mettre à jour la logique d’acquisition de jeton](#update-the-token-acquisition-logic-with-a-valid-access-token) et regénérez le jeton d’accès, mettez à jour `AcquireOAuth2Token()` de nouveau et regénérez/retestez. Vous pouvez également examiner et vérifier le jeton et ses revendications, à l’aide de l’application web monopage [jwt.ms](https://jwt.ms/). |
| Étiquettes de sensibilité non configurées | Non applicable | Si votre projet est généré avec succès, mais que vous n’avez aucune sortie dans la fenêtre de console, assurez-vous que les étiquettes de sensibilité de votre organisation soient correctement configurées. Consultez [Installation et configuration du kit SDK MIP](setup-configure-mip.md), sous « Définir les paramètres de taxonomie et de protection des étiquettes » pour plus d’informations.  |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment répertorier les étiquettes de sensibilité pour votre organisation, consultez le guide de démarrage rapide suivant :

> [!div class="nextstepaction"]
> [Définir et obtenir une étiquette de sensibilité](quick-file-set-get-label-csharp.md)
