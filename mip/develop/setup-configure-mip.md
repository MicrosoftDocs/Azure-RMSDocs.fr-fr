---
title: Installation et configuration du kit SDK Microsoft Information Protection (MIP)
description: Fournit les conditions préalables d’installation et de configuration permettant d’utiliser les applications générées avec le kit SDK Microsoft Information Protection.
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 06/13/2019
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 5daada951fb888fc7aa01071236af751ec38e002
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215525"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Installation et configuration du kit SDK Microsoft Information Protection (MIP)

Les guides de démarrage rapide et les tutoriels sont centrés sur la création d’applications qui utilisent les API et les bibliothèques du kit SDK MIP. Cet article explique comment installer et configurer votre abonnement Microsoft 365 et votre station de travail cliente, en préparation de l’utilisation du kit SDK.

## <a name="prerequisites"></a>Prérequis

Veillez à consulter les rubriques suivantes avant de commencer :

- [Qu’est-ce que le Centre de sécurité et conformité Office 365 ?](/office365/securitycompliance/security-and-compliance)
- [Qu’est-ce qu’Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection)
- [Comment la protection fonctionne-t-elle dans Azure Information Protection ?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

> [!IMPORTANT]
> **Pour respecter la confidentialité de l’utilisateur, vous devez lui demander son consentement avant d’activer la journalisation automatique.** L’exemple suivant est un message standard que Microsoft utilise pour la notification de journalisation :
>
> *En activant la journalisation des erreurs et des performances, vous acceptez d’envoyer les données des erreurs et des performances à Microsoft. Microsoft collecte les données des erreurs et des performances via Internet (« Données »). Microsoft utilise ces données pour fournir et améliorer la qualité, la sécurité et l’intégrité des produits et des services Microsoft. Par exemple, nous analysons les performances et la fiabilité, comme les fonctionnalités que vous utilisez, la rapidité de réponse des fonctionnalités, les performances de l’appareil, les interactions de l’interface utilisateur et tous les problèmes que vous rencontrez avec le produit. Les données incluent également des informations sur la configuration de votre logiciel, comme le logiciel en cours d’exécution et l’adresse IP.*

## <a name="sign-up-for-an-office-365-subscription"></a>S’abonner à Office 365

De nombreux exemples du kit SDK requièrent l’accès à un abonnement Office 365. Si vous ne l’avez pas encore fait, veillez à souscrire à l’un des types d’abonnement suivants :

| Nom                                               | Inscription                                                                         |
| -------------------------------------------------- | ------------------------------------------------------------------------------- |
| Version d’évaluation d’Office 365 Enterprise E3 (essai gratuit de 30 jours) | https://go.microsoft.com/fwlink/p/?LinkID=403802                                |
| Office 365 Entreprise E3 ou E5                     | https://products.office.com/business/office-365-enterprise-e3-business-software |
| Enterprise Mobility + Security E3 ou E5          | https://www.microsoft.com/cloud-platform/enterprise-mobility-security           |
| Azure Information Protection Premium P1ou P2      | https://azure.microsoft.com/pricing/details/information-protection/             |
| Microsoft 365 E3, E5 ou F1                        | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans         |

## <a name="configure-sensitivity-labels"></a>Configurer les étiquettes de sensibilité

Si vous utilisez actuellement Azure Information Protection, vous devez migrer vos étiquettes vers le Centre de sécurité et conformité Office 365. Pour plus d’informations sur ce processus, consultez [Guide pratique pour migrer les étiquettes Azure Information Protection vers le Centre de sécurité et conformité Office 365](/azure/information-protection/configure-policy-migrate-labels).

## <a name="configure-your-client-workstation"></a>Configurer votre station de travail cliente

Ensuite, exécutez la procédure suivante pour vous assurer que votre ordinateur client est installé et configuré correctement.

1. Si vous utilisez une station de travail Windows 10 :

   - Utilisez Windows Update pour mettre à jour votre machine avec Windows 10 Fall Creators Update (version 1709) ou version ultérieure. Pour vérifier votre version actuelle :
     - Cliquez sur l’icône Windows en bas à gauche.
     - Tapez « À propos de votre PC » et appuyez sur la touche « Entrée ».
     - Faites défiler la page jusqu'à **Spécifications de Windows** et regardez sous **Version**.

   - Vérifiez que le « Mode développeur » est activé sur votre station de travail :
     - Cliquez sur l’icône Windows en bas à gauche.
     - Tapez « Utiliser les fonctionnalités de développement » et appuyez sur la touche « Entrée » lorsque vous voyez l’élément **Utiliser les fonctionnalités de développement** apparaître.
     - Dans la boîte de dialogue **Paramètres**, dans l’onglet **Pour les développeurs**, sous « Utiliser les fonctionnalités de développement », sélectionnez l’option **Mode développeur**.
     - Fermez la boîte de dialogue **Paramètres**.

2. Installez [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/), avec les charges de travail et les composants facultatifs suivants :
   - Charge de travail Windows **Développement pour la plateforme Windows universelle**, ainsi que les composants facultatifs suivants :
     - **Outils de plateforme Windows universelle C++**
     - **SDK Windows 10 (10.0.16299.0)** ou version ultérieure, s’il n’est pas inclus par défaut
   - Charge de travail Windows **Développement Desktop en C++** , ainsi que les composants facultatifs suivants :
     - **SDK Windows 10 (10.0.16299.0)** ou version ultérieure, s’il n’est pas inclus par défaut

     [![Installation de Visual Studio](media/setup-mip-client/visual-studio-install.png)](media/setup-mip-client/visual-studio-install.png#lightbox)

3. Installez le [module PowerShell ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) :

   - Étant donné que les droits d’administrateur sont requis pour installer les modules, vous devez d’abord effectuer, au choix, l’une des opérations suivantes :

     - Connectez-vous à votre ordinateur avec un compte disposant des droits d’administrateur.
     - Exécutez la session Windows PowerShell avec des privilèges élevés (Exécuter en tant qu’administrateur).

   - Ensuite, exécutez l’applet de commande `install-module -name adal.ps` :

     ```powershell
     PS C:\WINDOWS\system32> install-module -name adal.ps

     Untrusted repository
     You are installing the modules from an untrusted repository. If you trust this repository, change its
     InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
     'PSGallery'?
     [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

     PS C:\WINDOWS\system32>
     ```

4. Téléchargez les fichiers du SDK :

   Le SDK MIP est pris en charge sur les plateformes suivantes, avec des téléchargements distincts pour chaque plateforme/langage pris en charge :

   [!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

   **Téléchargements Tar.gz/.Zip**

   Les téléchargements Tar.gz et .Zip contiennent plusieurs fichiers compressés, un pour chaque API. Les fichiers compressés sont nommés comme suit, où \<API\> = `file`, `protection` ou `upe` et \<OS\> = la plateforme : `mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`. Par exemple, le fichier pour les binaires et en-têtes de l’API de protection sur Debian serait : `mip_sdk_protection_debian9_1.0.0.0.tar.gz`. Chaque fichier .tar.gz/.zip contenu se divise en trois répertoires :

   - **Bins** : fichiers binaires compilés pour chaque architecture de plateforme, le cas échéant.
   - **Include** : fichiers d’en-tête (C++).
   - **Samples** : code source des exemples d’applications.

   **Packages NuGet**

   Si vous effectuez le développement Visual Studio, le kit SDK peut être également installé via la console du Gestionnaire de package NuGet :

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```

5. Si vous n’utilisez pas le package NuGet, ajoutez les chemins des binaires du SDK à la variable d’environnement PATH. La variable PATH permet aux applications clientes de trouver les binaires dépendants (DLL) au moment de l’exécution (FACULTATIF) :

   Si vous utilisez une station de travail Windows 10 :

   - Cliquez sur l’icône Windows en bas à gauche.
   - Tapez « Chemin » et appuyez sur la touche « Entrée » lorsque vous voyez l’élément **Modifier les variables d’environnement système** apparaître.
   - Dans la boîte de dialogue **Propriétés système**, cliquez sur **Variables d’environnement**.
   - Dans la boîte de dialogue **Variables d’environnement**, cliquez sur la ligne de la variable **Path** sous **Variables utilisateur pour \<user\>** , puis cliquez sur **Modifier...** .
   - Dans la boîte de dialogue **Modifier la variable d’environnement**, cliquez sur **Nouveau**, ce qui crée une nouvelle ligne d’édition. Ajoutez une nouvelle ligne pour chaque sous-répertoire `file\bins\debug\amd64`, `protection\bins\debug\amd64` et `upe\bins\debug\amd64` en utilisant son chemin complet. Les répertoires du kit SDK sont stockés dans un format `<API>\bins\<target>\<platform>`, où :
     - \<API\> = `file`, `protection`, `upe`
     - \<target\> = `debug`, `release`
     - \<platform\> = `amd64` (x64), `x86`, etc.

   - Une fois la mise à jour de la variable **Path** terminée, cliquez sur **OK**. Ensuite, cliquez sur **OK** lorsque vous revenez à la boîte de dialogue **Variables d’environnement**.

6. Téléchargez les exemples du SDK à partir de GitHub (FACULTATIF) :

   - Si vous n’avez pas de [profil GitHub](https://github.com/join), commencez par en créer un.
   - Ensuite, installez la dernière version des [Outils de client Git de Software Freedom Conservancy (Git Bash)](https://git-scm.com/download/).
   - À l’aide de Git Bash, téléchargez le ou les exemples qui nous intéressent :
     - Utilisez la requête suivante pour afficher les dépôts : https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk.
     - À l’aide de Git Bash, utilisez `git clone https://github.com/azure-samples/<repo-name>` pour télécharger chaque dépôt d’exemples.

## <a name="register-a-client-application-with-azure-active-directory"></a>Inscrire une application cliente auprès d’Azure Active Directory

Dans le cadre du processus de provisionnement de l’abonnement Microsoft 365, un locataire Azure Active Directory (Azure AD) associé est créé. Le locataire Azure AD assure la gestion des identités et des accès pour les *comptes d’utilisateur* et les *comptes d’application* Microsoft 365. Les applications qui requièrent un accès à des API sécurisées (telles que les API MIP) nécessitent un compte d’application.

Pour l’authentification et l’autorisation au moment de l’exécution, les comptes sont représentés par un *principal de sécurité*, qui est dérivé des informations d’identité du compte. Un principal de sécurité qui représente un compte d’application est appelé [*principal de service*](/azure/active-directory/develop/developer-glossary#service-principal-object).

Pour enregistrer un compte d’application dans Azure AD en vue de l’utiliser avec les exemples du kit SDK MIP et des guides de démarrage rapide :

  > [!IMPORTANT]
  > Pour accéder à la gestion du locataire Azure AD pour la création d’un compte, vous devez vous connecter au portail Azure avec un compte d’utilisateur qui est membre du [rôle « Propriétaire » dans le cadre de l’abonnement](/azure/billing/billing-add-change-azure-subscription-administrator). Selon la configuration de votre locataire, vous pouvez également avoir besoin d’être membre du rôle d’annuaire « Administrateur général » pour [inscrire une application](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
  > Nous vous recommandons de tester cela avec un compte limité. Veillez à ce que ce compte dispose uniquement des droits d’accès aux points de terminaison de contrôle de code source nécessaires. Les mots de passe en texte clair transmis via la ligne de commande peuvent être collectés par des systèmes de journalisation.

1. Effectuez les étapes de la section [Inscrire une application auprès d’Azure AD, Inscrire une nouvelle application](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#register-a-new-application-using-the-azure-portal). À des fins de test, utilisez les valeurs suivantes pour les propriétés spécifiées lorsque vous parcourez les étapes du guide :
    - **Types de comptes pris en charge** - Sélectionnez « Comptes dans cet annuaire organisationnel uniquement ».
    - **URI de redirection** - Définissez le type de l’URI de redirection sur « Public client (mobile & desktop) » (Client public (mobile & bureau)). Si votre application utilise la bibliothèque d’authentification Microsoft (MSAL), utilisez `http://localhost`. Dans le cas contraire, utilisez le format `<app-name>://authorize`.

2. Lorsque vous avez terminé, vous êtes ramené à la page **Application inscrite** pour l’inscription de votre nouvelle application. Copiez et enregistrez le GUID dans le champ **ID d’application (client)** , car vous en aurez besoin pour les guides de démarrage rapide.

3. Ensuite, cliquez sur **Autorisations d’API** pour ajouter les API et les autorisations auxquelles le client aura besoin d’accéder. Cliquez sur **Ajouter une autorisation** pour ouvrir le panneau « Demander des autorisations d’API ».

4. Vous allez maintenant ajouter les API MIP et les autorisations que l’application nécessitera au moment de l’exécution :
   - Sur la page **Sélectionner une API**, cliquez sur **Microsoft Rights Management Services**.
   - Sur la page de l’API **Azure Rights Management Services**, cliquez sur **Autorisations déléguées**.
   - Dans la section **Sélectionner des autorisations**, cochez l’autorisation **user_impersonation**. Ce droit permet à l’application de créer un contenu protégé au nom d’un utilisateur et d’y accéder.
   - Cliquez sur **Ajouter des autorisations** pour enregistrer.

5. Répétez l’étape 4 mais, cette fois, lorsque vous accédez à la page **Sélectionner une API**, vous devez rechercher l’API.
   - Dans la page **Sélectionner une API**, cliquez sur **API utilisées par mon organisation** puis, dans la zone de recherche, tapez « **Microsoft Information Protection Sync Service** » et sélectionnez-le.
   - Dans la page de l’API **Microsoft Information Protection Sync Service**, cliquez sur **Autorisations déléguées**.
   - Développez le nœud **UnifiedPolicy** et cochez **UnifiedPolicy.User.Read**
   - Cliquez sur **Ajouter des autorisations** pour enregistrer.

6. Lorsque vous êtes de retour dans la page **Autorisations de l’API**, cliquez sur **Accorder un consentement d’administrateur pour (Nom du client)** , puis sur **Oui**. Cette étape donne un consentement préalable à l’application qui utilise cette inscription pour accéder aux API sous les autorisations spécifiées. Si vous être connecté en tant qu’administrateur général, le consentement est enregistré pour tous les utilisateurs dans le locataire qui exécutent l’application ; sinon, il s’applique uniquement à votre compte d’utilisateur.

Lorsque vous avez terminé, l’inscription de l’application et les autorisations d’API doivent ressembler aux exemples suivants :

   [![Inscription d’application Azure AD](media/setup-mip-client/aad-app-registration-overview.png)](media/setup-mip-client/aad-app-registration-overview.png#lightbox) [![Inscription d’application Azure AD](media/setup-mip-client/aad-app-api-permissions.png)](media/setup-mip-client/aad-app-api-permissions.png#lightbox)

Pour plus d’informations sur l’ajout d’API et d’autorisations à une inscription, consultez [Configurer une application cliente pour accéder aux API web](/azure/active-directory/develop/quickstart-v1-update-azure-ad-app#configure-a-client-application-to-access-web-apis). Vous y trouverez des informations sur l’ajout des API et des autorisations requises par une application cliente.

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Demande d'un IPIA (Information Protection Integration Agreement)

Avant de pouvoir lancer une application développée avec MIP, vous devez obtenir l’accord formel de Microsoft.

1. Obtenez votre IPIA en envoyant un e-mail à [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Requesting%20IPIA%20for%20<company-name>) avec les informations suivantes :

   **Objet :** Demande d’IPIA pour *Nom de la société*

   Dans le corps du message électronique, incluez :
   - Nom de l’application et du produit
   - Nom et prénom du demandeur
   - Adresse de messagerie du demandeur

2. Après réception de votre demande d’IPIA, nous vous enverrons un formulaire (sous forme de document Word). Passez en revue les termes et conditions de l'IPIA et renvoyez le formulaire à l'adresse [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=IPIA%20Response%20for%20<company-name>) avec les informations suivantes :

   - Raison sociale de la société
   - État/Province (États-Unis / Canada) ou pays d'immatriculation
   - URL de l’entreprise
   - Adresse e-mail du contact
   - Adresses supplémentaires de la société (facultatif)
   - Nom de l'application d'entreprise
   - Brève description de l'application
   - *ID de locataire Azure*
   - *ID de l’application* pour l’application
   - Contacts de la société, e-mail et téléphone pour la correspondance en cas de situation critique

3. Après réception de votre formulaire, nous vous enverrons le lien IPIA final à signer numériquement. Après votre signature, il sera signé par le représentant de Microsoft approprié, ce qui finalisera l’accord.

### <a name="already-have-a-signed-ipia"></a>Vous disposez déjà d'un IPIA signé ?

Si vous disposez déjà d'un IPIA signé et souhaitez ajouter un nouvel *ID de l’application* pour une application que vous lancez, envoyez un e-mail à l'adresse [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Updating%20IPIA%20for%20<company-name>) et fournissez-nous les informations suivantes :

- Nom de l'application d'entreprise
- Brève description de l'application
- ID de locataire Azure (même s’il est identique au précédent)
- ID de l’application pour l’application
- Contacts de la société, e-mail et téléphone pour la correspondance en cas de situation critique

Vous recevrez un accusé de réception dans les 72 heures après l’envoi de l’e-mail.

## <a name="ensure-your-app-has-the-required-runtime"></a>Vérifier que l’application utilise le Runtime approprié

> [!NOTE]
> Effectuez cette étape uniquement si vous déployez l’application sur une machine sans Visual Studio, ou si Visual Studio a été installé sans les composants du Runtime Visual C++.

Pour les applications générées avec le SDK MIP, vous devez installer le Runtime Visual C++ 2015 ou Visual C++ 2017 s’il n’est pas déjà présent.
- [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/download/details.aspx?id=53587)
- [Microsoft Visual C++ Redistributable pour Visual Studio 2017](https://visualstudio.microsoft.com/downloads/#microsoft-visual-c-redistributable-for-visual-studio-2017)

Ces composants fonctionnent uniquement si l’application a été générée en tant que version release. Si l’application est générée en tant que version debug, les DLL debug du Runtime Visual C++ doivent être incluses avec l’application, ou installées sur la machine.

## <a name="next-steps"></a>Étapes suivantes

- Si vous développez en C++
  - Veillez à lire les [concepts liés aux observateurs](concept-async-observers.md) avant de commencer la section de démarrage rapide, pour en savoir plus sur la nature asynchrone des API C++.
  - Quand vous êtes prêt à utiliser le SDK, commencez par le [Démarrage rapide : Initialisation d’une application cliente (C++)](quick-app-initialization-cpp.md).
- Si vous développez en C#, quand vous êtes prêt à utiliser le SDK, commencez par le [Démarrage rapide : Initialisation d’une application cliente (C#)](quick-app-initialization-csharp.md).