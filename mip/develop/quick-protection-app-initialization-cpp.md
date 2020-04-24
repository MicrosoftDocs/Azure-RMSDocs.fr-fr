---
title: Démarrage rapide – Initialisation pour les clients C++ du kit SDK Microsoft Information Protection (MIP)
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes du kit SDK Microsoft Information Protection (MIP).
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: e0f77c27c38b8b2f1baf4385efce1ee7336c8f9d
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766386"
---
# <a name="quickstart-client-application-initialization-for-protection-apis-c"></a>Démarrage rapide : Initialisation d’une application cliente pour les API Protection (C++)

Ce guide de démarrage rapide montre comment implémenter le modèle d’initialisation de client utilisé par le SDK MIP C++ au moment de l’exécution.

> [!NOTE]
> Les étapes décrites dans ce guide de démarrage rapide sont requises pour toute application cliente qui utilise les API Protection MIP. Ces démarrages rapides doivent être effectués en série après l’initialisation de l’application et l’implémentation des classes de délégué d’authentification et de délégué de consentement.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas déjà fait, veillez à :

- Exécuter la procédure fournie dans [Installation et configuration du kit SDK Microsoft Information Protection (MIP)](setup-configure-mip.md). Ce guide de démarrage rapide « initialisation d’une application cliente » s’appuie sur une installation et une configuration correctes du kit SDK.
- Éventuellement :
  - Passez en revue [Objets de profil et moteur](concept-profile-engine-cpp.md). Les objets de profil et moteur sont des concepts universels, requis par les clients qui utilisent les API MIP de fichier/stratégie/protection.
  - Passez en revue les [concepts d’authentification](concept-authentication-cpp.md) pour savoir comment l’authentification et le consentement sont implémentés par le SDK et l’application cliente.
  - Passez en revue les [concepts liés aux observateurs](concept-async-observers.md) pour en savoir plus sur les observateurs et la manière dont ils sont implémentés. Le SDK MIP utilise le modèle d’observateur pour implémenter des notifications d’événements asynchrones.

## <a name="create-a-visual-studio-solution-and-project"></a>Créer une solution et un projet Visual Studio

Tout d’abord, créez et configurez la solution et le projet Visual Studio initiaux, qui seront utilisés dans les guides de démarrage rapide suivants.

1. Ouvrez Visual Studio 2017, sélectionnez le menu **Fichier**, **Nouveau**, **Projet**. Dans la boîte de dialogue **Nouveau projet** :
   - Dans le volet gauche, sous **Installé**, **Autres langages**, sélectionnez **Visual C++** .
   - Dans le volet central, sélectionnez **Application console Windows**.
   - Dans le volet inférieur, mettez à jour les champs **Nom**, **Emplacement** et **Nom de la solution** contenante du projet en conséquence.
   - Lorsque vous avez terminé, cliquez sur le bouton **OK** dans le coin inférieur droit.

     [![Création d’une solution dans Visual Studio](media/quick-app-initialization-cpp/create-vs-solution.png)](media/quick-app-initialization-cpp/create-vs-solution.png#lightbox)

2. Ajoutez le package Nuget pour l’API Protection du SDK MIP dans votre projet :
   - Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet (directement sous le nœud supérieur/de solution), puis sélectionnez **Gérer les packages NuGet...**  :
   - Lorsque l’onglet **Gestionnaire de Package NuGet** s’ouvre dans la zone des onglets du groupe d’éditeurs :
     - Sélectionnez **Parcourir**.
     - Dans la zone de recherche, entrez « Microsoft.InformationProtection ».
     - Sélectionnez le package « Microsoft.InformationProtection.Protection ».
     - Cliquez sur « Installer », puis cliquez sur « OK » lorsque la boîte de dialogue de confirmation **Aperçu des modifications** apparaît.

     [![Ajout du package NuGet dans Visual Studio](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)

## <a name="implement-observer-classes-to-monitor-the-protection-profile-and-engine-objects"></a>Implémenter des classes d’observateur pour superviser les objets de profil et de moteur de protection

Créez maintenant une implémentation de base pour une classe d’observateur de profil de protection, en étendant la classe `mip::ProtectionProfile::Observer` du kit SDK. L’observateur est instancié et utilisé plus tard, pour superviser le chargement de l’objet de profil de protection et l’ajout de l’objet de moteur au profil.

1. Ajoutez une nouvelle classe dans votre projet, ce qui génère les fichiers header/.h et implementation/.cpp pour vous :

   - Dans l’**Explorateur de solutions**, recliquez avec le bouton droit sur le nœud du projet, sélectionnez **Ajouter**, puis sélectionnez **Classe**.
   - Dans la boîte de dialogue **Ajouter une classe** :
     - Dans le champ **Nom de la classe**, entrez « profile_observer ». Notez que les champs **Fichier .h** et **Fichier .cpp** sont remplis automatiquement en fonction du nom que vous entrez.
     - Une fois terminé, cliquez sur le bouton **OK**.

     [![Ajout d’une classe dans Visual Studio](media/quick-app-initialization-cpp/add-class.png)](media/quick-app-initialization-cpp/add-class.png#lightbox)

2. Après avoir généré les fichiers .cpp et .h pour la classe, ces deux fichiers sont ouverts dans les onglets du groupe d’éditeurs. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe d’observateur :

   - Mettez à jour « profile_observer.h » en sélectionnant/supprimant la classe `profile_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <memory>
     #include "mip/protection/protection_profile.h"
     using std::exception_ptr;
     using std::shared_ptr;


     class ProtectionProfileObserver final : public mip::ProtectionProfile::Observer {
     public:
          ProtectionProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::ProtectionProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::ProtectionEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& Failure, const std::shared_ptr<void>& context) override;
     };
     ```

   - Mettez à jour « profile_observer.h » en sélectionnant/supprimant l’implémentation de classe `profile_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::ProtectionEngine;
     using mip::ProtectionProfile;

     void ProtectionProfileObserver::OnLoadSuccess(const shared_ptr<ProtectionProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_value(profile);
     }

     void ProtectionProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionProfile>>>(context);
          promise->set_exception(error);
     }

     void ProtectionProfileObserver::OnAddEngineSuccess(const shared_ptr<ProtectionEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_value(engine);
     }

     void ProtectionProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<ProtectionEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. Suivez les étapes sous 1. Ajoutez une nouvelle classe pour l’observateur d’objet de protection, « engine_observer », dans votre projet, ce qui génère les fichiers header/.h et implementation/.cpp pour vous.

4. Après avoir généré les fichiers .cpp et .h pour la classe, ces deux fichiers sont ouverts dans les onglets du groupe d’éditeurs. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe d’observateur :

   - Mettez à jour « engine_observer.h » en sélectionnant/supprimant la classe `engine_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::vector;
     using std::exception_ptr;
     using std::shared_ptr;

     class ProtectionEngineObserver final : public mip::ProtectionEngine::Observer {
       public:
       ProtectionEngineObserver() {}
       void OnGetTemplatesSuccess(const vector<std::shared_ptr<mip::TemplateDescriptor>>& templateDescriptors, const shared_ptr<void>& context) override;
       void OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;

     };
     ```

   - Mettez à jour « engine_observer.cpp » en sélectionnant/supprimant l’implémentation de classe `engine_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include "mip/protection/protection_profile.h"
     #include "engine_observer.h"

     using std::promise;
     void ProtectionEngineObserver::OnGetTemplatesSuccess(const vector<shared_ptr<mip::TemplateDescriptor>>& templateDescriptors,const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<vector<shared_ptr<mip::TemplateDescriptor>>>*>(context.get());
         loadPromise->set_value(templateDescriptors);
       };

       void ProtectionEngineObserver::OnGetTemplatesFailure(const exception_ptr& Failure, const shared_ptr<void>& context) {
         auto loadPromise = static_cast<promise<shared_ptr<mip::ProtectionProfile>>*>(context.get());
         loadPromise->set_exception(Failure);
       };
     ```

5. Si vous le souhaitez, utilisez Ctrl+Maj+B (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="implement-an-authentication-delegate-and-a-consent-delegate"></a>Implémenter un délégué d’authentification et un délégué de consentement

Le kit SDK MIP implémente l’authentification en utilisant l’extensibilité de classe, qui fournit un mécanisme pour partager le travail d’authentification avec l’application cliente. Le client doit acquérir un jeton d’accès OAuth2 approprié et le fournir au kit SDK MIP au moment de l’exécution.

Créez une implémentation pour un délégué d’authentification, en étendant la classe `mip::AuthDelegate` du kit SDK et en remplaçant/implémentant la pure fonction virtuelle `mip::AuthDelegate::AcquireOAuth2Token()`. **Suivez les étapes détaillées dans [Guide de démarrage rapide - Initialisation d’application API de fichier](quick-app-initialization-cpp.md).** Le délégué de l’authentification est instancié et utilisé plus tard par les objets de profil de protection et de moteur de protection.

## <a name="implement-a-consent-delegate"></a>Implémenter un délégué de consentement

Maintenant, créez une implémentation pour un délégué de consentement, en étendant la classe `mip::ConsentDelegate` du kit SDK et en remplaçant/implémentant la pure fonction virtuelle `mip::AuthDelegate::GetUserConsent()`.  **Suivez les étapes détaillées dans [Guide de démarrage rapide - Initialisation d’application API de fichier](quick-app-initialization-cpp.md).** Le délégué de consentement est instancié et utilisé plus tard par les objets de profil de protection et de moteur de protection.

## <a name="construct-a-protection-profile-and-engine"></a>Construire un moteur et un profil de protection

Comme nous l’avons mentionné précédemment, des objets de profil et de moteur sont nécessaires pour les clients du SDK utilisant des API MIP. Exécutez la partie de codage de ce guide de démarrage rapide, en ajoutant du code pour instancier les objets de profil et de moteur :

1. À partir de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Supprimez l’implémentation générée de `main()`. **Ne supprimez pas** les directives de préprocesseur générées par Visual Studio lors de la création du projet (#pragma, #include). Ajoutez le code suivant après les éventuelles directives de préprocesseur :

  ```cpp
  #include "mip/mip_init.h"
  #include "mip/mip_context.h"  
  #include "auth_delegate.h"
  #include "consent_delegate.h"
  #include "profile_observer.h"
  #include"engine_observer.h"

  using std::promise;
  using std::future;
  using std::make_shared;
  using std::shared_ptr;
  using std::string;
  using std::cout;
  using mip::ApplicationInfo;
  using mip::ProtectionProfile;
  using mip::ProtectionEngine;

  int main(){
    // Construct/initialize objects required by the application's profile object
    ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                            "<application-name>",
                            "<application-version>"};

    auto mipContext = mip::MipContext::Create(appInfo,
                                              "file_sample",
                                              mip::LogLevel::Trace,
                                              false,
                                              nullptr /*loggerDelegateOverride*/,
                                              nullptr /*telemetryOverride*/);


    auto profileObserver = make_shared<ProtectionProfileObserver>(); // Observer object
    auto authDelegateImpl = make_shared<AuthDelegateImpl>("<application-id>"); // Authentication delegate object (App ID)
    auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object

    // Construct/initialize profile object
    ProtectionProfile::Settings profileSettings(
      mipContext,
      mip::CacheStorageType::OnDisk,      
      consentDelegateImpl,
      profileObserver);

    // Set up promise/future connection for async profile operations; load profile asynchronously
    auto profilePromise = make_shared<promise<shared_ptr<ProtectionProfile>>>();
    auto profileFuture = profilePromise->get_future();
    try
    {
      mip::ProtectionProfile::LoadAsync(profileSettings, profilePromise);
    }
    catch (const std::exception& e)
    {
      cout << "An exception occurred... are the Settings and ApplicationInfo objects populated correctly?\n\n"
            << e.what() << "'\n";
      system("pause");
      return 1;
    }

    auto profile = profileFuture.get();

    // Construct/initialize engine object
    ProtectionEngine::Settings engineSettings(
       authDelegateImpl,                          // Reference to mip::AuthDelegate implementation
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state
       "en-US");                                  // Locale (default = en-US)

    // Set up promise/future connection for async engine operations; add engine to profile asynchronously
    auto enginePromise = make_shared<promise<shared_ptr<ProtectionEngine>>>();
    auto engineFuture = enginePromise->get_future();
    profile->AddEngineAsync(engineSettings, enginePromise);
    std::shared_ptr<ProtectionEngine> engine;

    try
    {
      engine = engineFuture.get();
    }
    catch (const std::exception& e)
    {
      cout << "An exception occurred... is the access token incorrect/expired?\n\n"
           << e.what() << "'\n";
      system("pause");
      return 1;
    }

    // Application shutdown. Null out profile and engine, call ReleaseAllResources();
    // Application may crash at shutdown if resources aren't properly released.
    engine = nullptr;
    profile = nullptr;
    mipContext = nullptr;

    return 0;
  }
   ```

3. Remplacez toutes les valeurs d’espace réservé que vous venez de coller dans le code source par des constantes de chaîne :

   | Espace réservé | Valeur | Exemple |
   |:----------- |:----- |:--------|
   | \<application-id\> | ID d’application Azure AD (GUID) attribué à l’application enregistrée à l’étape 2 de l’article « Installation et configuration du SDK MIP » (setup-configure-mip.md). Remplacez les deux instances. | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | Un nom convivial défini par l’utilisateur pour votre application. Doit contenir des caractères ASCII valides (à l’exclusion de « ; ») et, si possible, correspondre au nom d’application que vous avez utilisé dans votre inscription Azure AD. | `"AppInitialization"` |
   | \<application-version\> | Informations de version définies par l’utilisateur pour votre application. Doit contenir des caractères ASCII valides (à l’exclusion de « ; »). | `"1.1.0.0"` |
   | \<engine-account\> | Le compte utilisé pour l’identité du moteur. Lorsque vous vous authentifiez avec un compte d’utilisateur lors de l’acquisition du jeton, il doit correspondre à cette valeur. | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | L’état défini par l’utilisateur à associer au moteur. | `"My App State"` |

4. À présent, effectuez une build finale de l’application et corrigez les erreurs éventuelles. Votre code doit être généré avec succès, mais ne s’exécutera pas correctement tant que vous n’aurez pas terminé le guide de démarrage rapide suivant. Si vous exécutez l’application, vous voyez une sortie similaire à ce qui suit. L’application crée le profil de protection et le moteur de protection avec succès, mais n’active pas le module d’authentification et vous n’avez pas encore de jeton d’accès, jusqu’à ce que vous ayez terminé le démarrage rapide suivant.

   ```console
    C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
    To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
    Press any key to close this window . . .
   ```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre code d’initialisation est terminé, vous êtes prêt pour le guide de démarrage rapide suivant, où vous découvrirez l’API Protection MIP.

> [!div class="nextstepaction"]
> [Répertorier les modèles de protection](quick-protection-list-templates-cpp.md)
