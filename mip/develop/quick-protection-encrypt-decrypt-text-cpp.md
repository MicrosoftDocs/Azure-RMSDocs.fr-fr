---
title: 'Démarrage rapide : chiffrer/déchiffrer du texte à l’aide de l’API Protection du SDK C++ MIP'
description: Ce démarrage rapide vous montre comment utiliser l’API Protection du SDK Microsoft Information Protection C++ pour chiffrer et déchiffrer le texte ad hoc à l’aide d’un modèle de protection.
services: information-protection
author: Pathak-Aniket
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: v-anikep
ms.openlocfilehash: 24d52a73620a7f186c425532f5132cac2a46f405
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766335"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>Démarrage rapide : Chiffrer/déchiffrer le texte à l’aide du SDK MIP (C++)

Ce guide de démarrage rapide vous montre comment utiliser plus d’API Protection MIP. À l’aide de l’un des modèles de protection que vous avez indiqués dans le démarrage rapide précédent, vous utilisez un gestionnaire de protection pour chiffrer le texte ad hoc. La classe du gestionnaire de protection expose différentes opérations pour l’application et la suppression de la protection.

## <a name="prerequisites"></a>Prérequis

Si vous ne l’avez pas encore fait, veillez à remplir les prérequis suivants avant de poursuivre :

- Effectuez d’abord les étapes du [Démarrage rapide : Commencez par répertorier les modèles de protection (C++)](quick-protection-list-templates-cpp.md), ce qui génère une solution de démarrage Visual Studio, afin de répertorier les modèles de protection disponibles pour un utilisateur authentifié. Ce guide de démarrage rapide « Chiffrer/déchiffrer le texte » s’appuie sur le précédent.
- Éventuellement : Passez en revue les concepts [Gestionnaires de protection dans le kit SDK MIP](concept-handler-protection-cpp.md).

## <a name="implement-an-observer-class-to-monitor-the-protection-handler-object"></a>Implémenter une classe d’observateur pour superviser l’objet de gestionnaire de protection

Comme avec l’observateur que vous avez implémenté (pour le profil et le moteur de protection) dans Démarrage rapide – Initialisation de l’application, vous implémentez maintenant une classe d’observateur pour des objets de gestionnaire de protection.

Créez une implémentation de base pour un observateur de gestionnaire de protection, en étendant la classe `mip::ProtectionHandler::Observer` du SDK. L’observateur est instancié et utilisé plus tard pour suivre les opérations du gestionnaire de protection.

1. Ouvrez la solution Visual Studio que vous avez utilisée dans l’article précédent, « Démarrage rapide : Répertorier les modèles de protection (C++) ».

2. Ajoutez une nouvelle classe dans votre projet, ce qui génère les fichiers header/.h et implementation/.cpp pour vous :

   - Dans l’**Explorateur de solutions**, recliquez avec le bouton droit sur le nœud du projet, sélectionnez **Ajouter**, puis sélectionnez **Classe**.
   - Dans la boîte de dialogue **Ajouter une classe** :
     - Dans le champ **Nom de la classe**, entrez « handler_observer ». Notez que les champs **Fichier .h** et **Fichier .cpp** sont remplis automatiquement en fonction du nom que vous entrez.
     - Une fois terminé, cliquez sur le bouton **OK**.

3. Après avoir généré les fichiers .cpp et .h pour la classe, ces deux fichiers sont ouverts dans les onglets du groupe d’éditeurs. Maintenant, mettez à jour chaque fichier pour implémenter votre nouvelle classe d’observateur :

   - Mettez à jour « handler_observer.h » en sélectionnant/supprimant la classe `handler_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include <memory>
     #include "mip/protection/protection_engine.h"
     using std::shared_ptr;
     using std::exception_ptr;

     class ProtectionHandlerObserver final : public mip::ProtectionHandler::Observer {
          public:
          ProtectionHandlerObserver() { }
          void OnCreateProtectionHandlerSuccess(const shared_ptr<mip::ProtectionHandler>& protectionHandler, const shared_ptr<void>& context) override;
          void OnCreateProtectionHandlerFailure(const exception_ptr& Failure, const shared_ptr<void>& context) override;
          };

     ```

   - Mettez à jour « handler_observer.cpp » en sélectionnant/supprimant l’implémentation de classe `handler_observer` générée. **Ne supprimez pas** les directives de préprocesseur générées par l’étape précédente (#pragma, #include). Ensuite, copiez/collez la source suivante dans le fichier, après toute directive de préprocesseur existante :

     ```cpp
     #include "handler_observer.h"
     using std::shared_ptr;
     using std::promise;
     using std::exception_ptr;

     void ProtectionHandlerObserver::OnCreateProtectionHandlerSuccess(
          const shared_ptr<mip::ProtectionHandler>& protectionHandler,const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get());
               createProtectionHandlerPromise->set_value(protectionHandler);
               };

     void ProtectionHandlerObserver::OnCreateProtectionHandlerFailure(
          const exception_ptr& Failure, const shared_ptr<void>& context) {
               auto createProtectionHandlerPromise = static_cast<promise<shared_ptr<mip::ProtectionHandler>>*>(context.get())
               createProtectionHandlerPromise->set_exception(Failure);
               };

     ```

4. Si vous le souhaitez, utilisez Ctrl+Maj+B (**Générer la solution**) pour exécuter un test de compilation/liaison de votre solution, pour vous assurer qu’elle est correctement générée avant de continuer.

## <a name="add-logic-to-encrypt-and-decrypt-ad-hoc-text"></a>Ajouter une logique pour chiffrer et déchiffrer le texte ad hoc

Ajoutez une logique pour chiffrer et déchiffrer le texte ad hoc à l’aide de l’objet de moteur de protection.

1. À l’aide de l’**Explorateur de solutions**, ouvrez le fichier .cpp dans votre projet qui contient l’implémentation de la méthode `main()`.

2. Ajoutez les directives #include et using suivantes, sous les directives existantes correspondantes, en haut du fichier :

   ```cpp
     #include "mip/protection/protection_descriptor_builder.h"
     #include "mip/protection_descriptor.h"
     #include "handler_observer.h"

     using mip::ProtectionDescriptor;
     using mip::ProtectionDescriptorBuilder;
     using mip::ProtectionHandler;
   ```

3. Vers la fin du corps `Main()`, où vous vous êtes arrêté dans le guide de démarrage rapide précédent, insérez le code suivant :

   ```cpp
   //Encrypt/Decrypt text:
   string templateId = "<Template-ID>";//Template ID from previous QuickStart e.g. "bb7ed207-046a-4caf-9826-647cff56b990"
   string inputText = "<Sample-Text>";//Sample Text

   //Refer to ProtectionDescriptor docs for details on creating the descriptor
   auto descriptorBuilder = mip::ProtectionDescriptorBuilder::CreateFromTemplate(templateId);
   const std::shared_ptr<mip::ProtectionDescriptor>& descriptor = descriptorBuilder->Build();

   //Create Publishing settings using a descriptor
   mip::ProtectionHandler::PublishingSettings publishingSettings = mip::ProtectionHandler::PublishingSettings(descriptor);

   //Create a publishing protection handler using Protection Descriptor
   auto handlerObserver = std::make_shared<ProtectionHandlerObserver>();
   engine->CreateProtectionHandlerForPublishingAsync(publishingSettings, handlerObserver, pHandlerPromise);
   auto publishingHandler = pHandlerFuture.get();

   std::vector<uint8_t> inputBuffer(inputText.begin(), inputText.end());

   //Show action plan
   cout << "Applying Template ID " + templateId + " to: " << endl << inputText << endl;

   //Encrypt buffer using Publishing Handler
   std::vector<uint8_t> encryptedBuffer;
   encryptedBuffer.resize(static_cast<size_t>(publishingHandler->GetProtectedContentLength(inputText.size(), true)));

   publishingHandler->EncryptBuffer(0,
                         &inputBuffer[0],
                         static_cast<int64_t>(inputBuffer.size()),
                         &encryptedBuffer[0],
                         static_cast<int64_t>(encryptedBuffer.size()),
                         true);

   std::string encryptedText(encryptedBuffer.begin(), encryptedBuffer.end());
   cout << "Encrypted Text :" + encryptedText;

   //Show action plan
   cout << endl << "Decrypting string: " << endl << endl;

   //Generate publishing licence, so it can be used later to decrypt text.
   auto serializedPublishingLicense = publishingHandler->GetSerializedPublishingLicense();

   //Use same PL to decrypt the encryptedText.
   auto cHandlerPromise = std::make_shared<std::promise<std::shared_ptr<ProtectionHandler>>>();
   auto cHandlerFuture = cHandlerPromise->get_future();
   shared_ptr<ProtectionHandlerObserver> cHandlerObserver = std::make_shared<ProtectionHandlerObserver>();

   //Create consumption settings using serialised publishing licence.
   mip::ProtectionHandler::ConsumptionSettings consumptionSettings = mip::ProtectionHandler::ConsumptionSettings(serializedPublishingLicense);
   engine->CreateProtectionHandlerForConsumptionAsync(consumptionSettings, cHandlerObserver, cHandlerPromise);

   auto consumptionHandler = cHandlerFuture.get();

   //Use consumption handler to decrypt the text.
   std::vector<uint8_t> decryptedBuffer(static_cast<size_t>(encryptedText.size()));

   int64_t decryptedSize = consumptionHandler->DecryptBuffer(
        0,
        &encryptedBuffer[0],
        static_cast<int64_t>(encryptedBuffer.size()),
        &decryptedBuffer[0],
        static_cast<int64_t>(decryptedBuffer.size()),
        true);

   decryptedBuffer.resize(static_cast<size_t>(decryptedSize));

   std::string decryptedText(decryptedBuffer.begin(), decryptedBuffer.end());

   // Output decrypted content. Should match original input text.
   cout << "Decrypted Text :" + decryptedText << endl;

   ```

4. Vers la fin de `main()`, identifiez le bloc d’arrêt d’application créé lors du premier démarrage rapide et ajoutez les lignes ci-dessous pour libérer les ressources du gestionnaire :

   ```cpp
    publishingHandler = nullptr;
    consumptionHandler = nullptr;
   ```

5. Remplacez les valeurs d’espace réservé que vous venez de coller dans le code source par des constantes de chaîne :

   | Espace réservé | Valeur |
   |:----------- |:----- |
   | \<sample-text\> | Exemple de texte que vous souhaitez protéger, par exemple : `"cipher text"`. |
   | \<Template-Id\> | ID de modèle que vous souhaitez utiliser pour protéger le texte. Par exemple : `"bb7ed207-046a-4caf-9826-647cff56b990"` |
  
## <a name="build-and-test-the-application"></a>Générer et tester l’application

Générez et testez votre application cliente.

1. Utilisez Ctrl+Maj+B (**Générer la solution**) pour générer votre application cliente. Si vous n’avez aucune erreur de génération, utilisez F5 (**Démarrer le débogage**) pour exécuter votre application.

2. Si votre projet est généré et s’exécute correctement, l’application demande un jeton d’accès chaque fois que le kit SDK appelle votre méthode `AcquireOAuth2Token()`. Comme vous l’avez fait précédemment dans le guide de démarrage rapide « Répertorier les modèles de protection », exécutez votre script PowerShell pour obtenir le jeton chaque fois, en utilisant les valeurs fournies pour $authority et $resourceUrl.

   ```console
   *** Template List:
   Name: Confidential \ All Employees : a74f5027-f3e3-4c55-abcd-74c2ee41b607
   Name: Highly Confidential \ All Employees : bb7ed207-046a-4caf-9826-647cff56b990
   Name: Confidential : 174bc02a-6e22-4cf2-9309-cb3d47142b05
   Name: Contoso Employees Only : 667466bf-a01b-4b0a-8bbf-a79a3d96f720
   Applying Template ID bb7ed207-046a-4caf-9826-647cff56b990 to:
   <Sample-Text>
   Encrypted Text :y¬╩$Ops7Γ╢╖¢t
   Decrypting string:

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/common/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
   Set $authority to: https://login.windows.net/94f69844-8d34-4794-bde4-3ac89ad2b664/oauth2/authorize
   Set $resourceUrl to: https://aadrm.com
   Sign in with user account: user1@tenant.onmicrosoft.com
   Enter access token: <paste-access-token-here>
   Press any key to continue . . .

   Decrypted Text :<Sample-Text>
   C:\MIP Sample Apps\ProtectionQS\Debug\ProtectionQS.exe (process 8252) exited with code 0.
   To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
   Press any key to close this window . . .
   ```
