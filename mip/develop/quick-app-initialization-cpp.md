---
title: Démarrage rapide – Initialisation pour les clients C++ du kit SDK Microsoft Information Protection (MIP)
description: Guide de démarrage rapide vous montrant comment écrire la logique d’initialisation pour des applications clientes du kit SDK Microsoft Information Protection (MIP).
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 49a0588f4f4d91879899fc0ccd906490906250c0
ms.sourcegitcommit: a3f901e479abbe056f8936a96b7253f0826d1415
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "75556076"
---
# <a name="quickstart-client-application-initialization-c"></a>Démarrage rapide : Initialisation d’une application cliente (C++)

Ce guide de démarrage rapide montre comment implémenter le modèle d’initialisation de client utilisé par le SDK MIP C++ au moment de l’exécution. 

> [!NOTE]
> Les étapes décrites dans ce guide de démarrage rapide sont requises pour toute application cliente qui utilise les API MIP de fichier, de stratégie ou de protection. Bien que ce guide de démarrage rapide illustre l’utilisation des API de fichier, ce même modèle s’applique aux clients utilisant les API de stratégie et de protection. Effectuez les autres guides de démarrage rapide dans l’ordre, car chacun s’appuie sur le précédent, celui-ci étant le premier.

## <a name="prerequisites"></a>Configuration requise

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

2. Ajoutez le package Nuget pour l’API de fichier du kit SDK MIP dans votre projet :
   - Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet (directement sous le nœud supérieur/de solution), puis sélectionnez **Gérer les packages NuGet...**  :
   - Lorsque l’onglet **Gestionnaire de Package NuGet** s’ouvre dans la zone des onglets du groupe d’éditeurs :
     - Sélectionnez **Parcourir**.
     - Dans la zone de recherche, entrez « Microsoft.InformationProtection ».
     - Sélectionnez le package « Microsoft.InformationProtection.File ».
     - Cliquez sur « Installer », puis cliquez sur « OK » lorsque la boîte de dialogue de confirmation **Aperçu des modifications** apparaît.
   
     [![Ajout du package NuGet dans Visual Studio](media/quick-app-initialization-cpp/add-nuget-package.png)](media/quick-app-initialization-cpp/add-nuget-package.png#lightbox)
 
## <a name="implement-an-observer-class-to-monitor-the-file-profile-and-engine-objects"></a>Implémenter une classe d’observateur pour superviser les objets de profil et de moteur de fichier

Créez maintenant une implémentation de base pour une classe d’observateur de profil de fichier, en étendant la classe `mip::FileProfile::Observer` du kit SDK. L’observateur est instancié et utilisé plus tard, pour superviser le chargement de l’objet de profil de fichier et l’ajout de l’objet de moteur au profil.

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
     #include "mip/file/file_profile.h"

     class ProfileObserver final : public mip::FileProfile::Observer {
     public:
          ProfileObserver() { }
          void OnLoadSuccess(const std::shared_ptr<mip::FileProfile>& profile, const std::shared_ptr<void>& context) override;
          void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
          void OnAddEngineSuccess(const std::shared_ptr<mip::FileEngine>& engine, const std::shared_ptr<void>& context) override;
          void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context) override;
     };
     ```

   - Mettez à jour « profile_observer.h » en sélectionnant/supprimant l’implémentation de classe `profile_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <future>

     using std::promise;
     using std::shared_ptr;
     using std::static_pointer_cast;
     using mip::FileEngine;
     using mip::FileProfile;

     void ProfileObserver::OnLoadSuccess(const shared_ptr<FileProfile>& profile, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_value(profile);
     }

     void ProfileObserver::OnLoadFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileProfile>>>(context);
          promise->set_exception(error);
     }

     void ProfileObserver::OnAddEngineSuccess(const shared_ptr<FileEngine>& engine, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_value(engine);
     }

     void ProfileObserver::OnAddEngineFailure(const std::exception_ptr& error, const shared_ptr<void>& context) {
          auto promise = static_pointer_cast<std::promise<shared_ptr<FileEngine>>>(context);
          promise->set_exception(error);
     }
     ```

3. Si vous le souhaitez, utilisez la touche F6 (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="implement-an-authentication-delegate"></a>Implémenter un délégué d’authentification

Le kit SDK MIP implémente l’authentification en utilisant l’extensibilité de classe, qui fournit un mécanisme pour partager le travail d’authentification avec l’application cliente. Le client doit acquérir un jeton d’accès OAuth2 approprié et le fournir au kit SDK MIP au moment de l’exécution. 

Maintenant, créez une implémentation pour un délégué d’authentification, en étendant la classe `mip::AuthDelegate` du kit SDK et en remplaçant/implémentant la pure fonction virtuelle `mip::AuthDelegate::AcquireOAuth2Token()`. Le délégué de l’authentification est instancié et utilisé plus tard par les objets de profil de fichier et de moteur de fichier.

1. À l’aide de la même fonctionnalité « Ajouter une classe » de Visual Studio que nous avons utilisée à l’étape 1 de la section précédente, ajoutez une autre classe dans votre projet. Cette fois, entrez « auth_delegate » dans le champ **Nom de la classe**. 

2. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe de délégué d’authentification :

   - Mettez à jour « auth_delegate.h » en remplaçant l’ensemble du code de la classe `auth_delegate` générée par la source suivante. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include) :

     ```cpp
     #include <string>
     #include "mip/common_types.h"

     class AuthDelegateImpl final : public mip::AuthDelegate {
     public:
          AuthDelegateImpl() = delete;        // Prevents default constructor

          AuthDelegateImpl(
            const std::string& appId)         // AppID for registered AAD app
            : mAppId(appId) {};

          bool AcquireOAuth2Token(            // Called by MIP SDK to get a token
            const mip::Identity& identity,    // Identity of the account to be authenticated, if known
            const OAuth2Challenge& challenge, // Authority (AAD tenant issuing token), and resource (API being accessed; "aud" claim).
            OAuth2Token& token) override;     // Token handed back to MIP SDK

     private:
          std::string mAppId;
          std::string mToken;
          std::string mAuthority;
          std::string mResource;
     };
     ```

   - Mettez à jour « auth_delegate.cpp » en remplaçant l’ensemble de l’implémentation de la classe `auth_delegate` générée par la source suivante. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). 

     > [!IMPORTANT]
     > Le code d’acquisition de jeton suivant n’est pas approprié à une utilisation en production. En production, il doit être remplacé par le code qui acquiert dynamiquement un jeton, en utilisant :
     > - L’appId et l’URI de réponse/redirection spécifiés dans votre inscription d’application Azure AD (l’URI de réponse/redirection **doit** correspondre à l’inscription de votre application)
     > - L’URL de ressource et d’autorité transmise par le kit SDK dans l’argument `challenge` (l’URL de ressource **doit** correspondre aux autorisations/API d’inscription de votre application)
     > - Des informations d’identification valides d’application/d’utilisateur, où le compte correspond à l’argument `identity` transmis par le kit SDK. Les clients « natifs » OAuth2 doivent demander les informations d’identification de l’utilisateur et utiliser le flux « code d’autorisation ». Les « clients confidentiels » OAuth2 peuvent utiliser leurs propres informations d’identification sécurisées avec le flux « informations d’identification du client » (par exemple, un service) ou demander les informations d’identification de l’utilisateur à l’aide du flux « code d’autorisation » (par exemple, une application web). 
     >
     > L’acquisition de jeton OAuth2 est un protocole complexe qui s’effectue normalement en utilisant une bibliothèque. TokenAcquireOAuth2Token() est appelée **uniquement** par le kit SDK MIP, en fonction des besoins.

     ```cpp
     #include <iostream>
     using std::cout;
     using std::cin;
     using std::string;

     bool AuthDelegateImpl::AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) 
     {
          // Acquire a token manually, reuse previous token if same authority/resource. In production, replace with token acquisition code.
          string authority = challenge.GetAuthority();
          string resource = challenge.GetResource();
          if (mToken == "" || (authority != mAuthority || resource != mResource))
          {
              cout << "\nRun the PowerShell script to generate an access token using the following values, then copy/paste it below:\n";
              cout << "Set $authority to: " + authority + "\n";
              cout << "Set $resourceUrl to: " + resource + "\n";
              cout << "Sign in with user account: " + identity.GetEmail() + "\n";
              cout << "Enter access token: ";
              cin >> mToken;
              mAuthority = authority;
              mResource = resource;
              system("pause");
          }

          // Pass access token back to MIP SDK
          token.SetAccessToken(mToken);

          // True = successful token acquisition; False = failure
          return true;
     }
     ```

3. Si vous le souhaitez, utilisez la touche F6 (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="implement-a-consent-delegate"></a>Implémenter un délégué de consentement

Maintenant, créez une implémentation pour un délégué de consentement, en étendant la classe `mip::ConsentDelegate` du kit SDK et en remplaçant/implémentant la pure fonction virtuelle `mip::AuthDelegate::GetUserConsent()`. Le délégué de consentement est instancié et utilisé plus tard par les objets de profil de fichier et de moteur de fichier.

1. À l’aide de la même fonctionnalité « Ajouter une classe » de Visual Studio que nous avons utilisée précédemment, ajoutez une autre classe dans votre projet. Cette fois, entrez « consent_delegate » dans le champ **Nom de la classe**. 

2. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe de délégué de consentement :

   - Mettez à jour « consent_delegate.h » en remplaçant l’ensemble du code de la classe `consent_delegate` générée par la source suivante. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include) :

     ```cpp
     #include "mip/common_types.h"
     #include <string>

     class ConsentDelegateImpl final : public mip::ConsentDelegate {
     public:
          ConsentDelegateImpl() = default;
          virtual mip::Consent GetUserConsent(const std::string& url) override;
     };
     ```

   - Mettez à jour « consent_delegate.cpp » en remplaçant l’ensemble de l’implémentation de la classe `consent_delegate` générée par la source suivante. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). 

     ```cpp
     #include <iostream>
     using mip::Consent;
     using std::string;

     Consent ConsentDelegateImpl::GetUserConsent(const string& url) 
     {
          // Accept the consent to connect to the url
          std::cout << "SDK will connect to: " << url << std::endl;
          return Consent::AcceptAlways;
     }
     ``` 
     
3. Si vous le souhaitez, utilisez la touche F6 (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="construct-a-file-profile-and-engine"></a>Construire un moteur et un profil de fichier

Comme nous l’avons mentionné précédemment, des objets de profil et de moteur sont nécessaires pour les clients du SDK utilisant des API MIP. Exécutez la partie de codage de ce guide de démarrage rapide, en ajoutant du code pour instancier les objets de profil et de moteur : 

1. À partir de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`. Par défaut, il a le même nom que le projet qui le contient, et que vous avez spécifié lors de la création du projet.

2. Supprimez l’implémentation générée de `main()`. **Ne supprimez pas** les directives de préprocesseur générées par Visual Studio lors de la création du projet (#pragma, #include). Ajoutez le code suivant après les éventuelles directives de préprocesseur :

   ```cpp
   #include "mip/mip_init.h"
   #include "mip/mip_context.h"  
   #include "auth_delegate.h"
   #include "consent_delegate.h"
   #include "profile_observer.h"

   using std::promise;
   using std::future;
   using std::make_shared;
   using std::shared_ptr;
   using std::string;
   using std::cout;
   using mip::ApplicationInfo;
   using mip::FileProfile;
   using mip::FileEngine;

   int main()
   {
     // Construct/initialize objects required by the application's profile object
     ApplicationInfo appInfo{"<application-id>",                    // ApplicationInfo object (App ID, name, version)
                 "<application-name>",
                 "<application-version>"};

     auto mipContext = mip::MipContext::Create(appInfo,
                         "file_sample",
                         mip::LogLevel::Trace,
                         nullptr /*loggerDelegateOverride*/,
                         nullptr /*telemetryOverride*/);

     auto profileObserver = make_shared<ProfileObserver>();         // Observer object
     auto authDelegateImpl = make_shared<AuthDelegateImpl>(         // Authentication delegate object (App ID)
                 "<application-id>");
     auto consentDelegateImpl = make_shared<ConsentDelegateImpl>(); // Consent delegate object
 
     // Construct/initialize profile object
     FileProfile::Settings profileSettings(
       mipContext,
       mip::CacheStorageType::OnDisk,
       authDelegateImpl,
       consentDelegateImpl,
       profileObserver);

     // Set up promise/future connection for async profile operations; load profile asynchronously
     auto profilePromise = make_shared<promise<shared_ptr<FileProfile>>>();
     auto profileFuture = profilePromise->get_future();
    try
    { 
        mip::FileProfile::LoadAsync(profileSettings, profilePromise);
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
     FileEngine::Settings engineSettings(
       mip::Identity("<engine-account>"),         // Engine identity (account used for authentication)
       "<engine-state>",                          // User-defined engine state
       "en-US");                                  // Locale (default = en-US)

     // Set up promise/future connection for async engine operations; add engine to profile asynchronously
     auto enginePromise = make_shared<promise<shared_ptr<FileEngine>>>();
     auto engineFuture = enginePromise->get_future();
     profile->AddEngineAsync(engineSettings, enginePromise);
     std::shared_ptr<FileEngine> engine; 
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
   // handler = nullptr; // This will be used in later quick starts.
   engine = nullptr;
   profile = nullptr;   
   mipContext = nullptr;

   return 0;
   }
   ``` 

3. Remplacez toutes les valeurs d’espace réservé que vous venez de coller dans le code source par des constantes de chaîne :

   | Espace réservé | valeur | Exemple |
   |:----------- |:----- |:--------|
   | \<application-id\> | L’ID d’application Azure AD (GUID) attribué à l’application qui a été inscrite à l’[étape 2 de l’article « Installation et configuration du kit SDK MIP »](/information-protection/develop/setup-configure-mip#register-a-client-application-with-azure-active-directory). Remplacez les deux instances. | `"0edbblll-8773-44de-b87c-b8c6276d41eb"` |
   | \<application-name\> | Un nom convivial défini par l’utilisateur pour votre application. Doit contenir des caractères ASCII valides (à l’exclusion de « ; ») et, si possible, correspondre au nom d’application que vous avez utilisé dans votre inscription Azure AD. | `"AppInitialization"` |
   | \<application-version\> | Informations de version définies par l’utilisateur pour votre application. Doit contenir des caractères ASCII valides (à l’exclusion de « ; »). | `"1.1.0.0"` |
   | \<engine-account\> | Le compte utilisé pour l’identité du moteur. Lorsque vous vous authentifiez avec un compte d’utilisateur lors de l’acquisition du jeton, il doit correspondre à cette valeur. | `"user1@tenant.onmicrosoft.com"` |
   | \<engine-state\> | L’état défini par l’utilisateur à associer au moteur. | `"My App State"` |


4. À présent, effectuez une build finale de l’application et corrigez les erreurs éventuelles. Votre code doit être généré avec succès, mais ne s’exécutera pas correctement tant que vous n’aurez pas terminé le guide de démarrage rapide suivant. Si vous exécutez l’application, vous voyez une sortie similaire à ce qui suit. Vous n’aurez pas de jeton d’accès à fournir tant que vous n’aurez pas terminé le guide de démarrage rapide suivant.

   ```console
   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://syncservice.o365syncservice.com/
   Sign in with user account:
   Enter access token:
   ```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre code d’initialisation est terminé, vous êtes prêt pour le guide de démarrage rapide suivant, où vous découvrirez les API de fichier MIP.

> [!div class="nextstepaction"]
> [Répertorier les étiquettes de sensibilité](quick-file-list-labels-cpp.md)
