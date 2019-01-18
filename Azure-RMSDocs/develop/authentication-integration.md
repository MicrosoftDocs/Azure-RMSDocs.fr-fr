---
title: Procédure d’inscription de votre application dans Azure AD - AIP
description: Décrit les principes fondamentaux de l’authentification utilisateur pour votre application RMS.
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 2cdd5f88edd8cad446ebaecbdd4065fdc18de51e
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54394106"
---
# <a name="how-to-register-and-rms-enable-your-app-with-azure-ad"></a>Procédure d’inscription et d’activation RMS de votre application dans Azure AD

Cette rubrique décrit les concepts de base de l’inscription d’une application et de son activation RMS dans le portail Azure, puis l’authentification utilisateur avec Azure Active Directory Authentication Library (ADAL).

## <a name="what-is-user-authentication"></a>Qu’est-ce que l’authentification utilisateur ?
L’authentification utilisateur est une étape essentielle pour établir la communication entre votre application et l’infrastructure RMS. Ce processus d’authentification utilise le protocole OAuth 2.0 standard qui nécessite les éléments d’information suivants sur l’utilisateur actuel et sur sa demande d’authentification.

## <a name="registration-via-azure-portal"></a>Inscription dans le portail Azure
Commencez par suivre ce guide pour configurer l’inscription de votre application dans le portail Azure, [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md). Copiez et enregistrez **l’ID client** et **l’URI de redirection** de ce processus pour les utiliser plus tard.

## <a name="complete-your-information-protection-integration-agreement-ipia"></a>Signature d'un IPIA (Information Protection Integration Agreement)
Avant de pouvoir déployer votre application, vous devez signer un contrat IPIA avec l’équipe Microsoft Information Protection. Pour plus d’informations, consultez la première section de la rubrique [Déployer en production](deploying-your-application.md).

## <a name="implement-user-authentication-for-your-app"></a>Implémenter l’authentification utilisateur pour votre application
Chacune des API RMS a un rappel qui doit être implémenté pour activer l’authentification de l’utilisateur. RMS SDK 4.2 utilise votre implémentation du rappel quand vous ne fournissez pas de jeton d’accès, quand votre jeton d’accès doit être actualisé ou quand le jeton d’accès a expiré.

- Android - Interfaces [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) et [AuthenticationCompletionCallback](https://msdn.microsoft.com/library/dn758250.aspx).
- iOS/OS X - Protocole [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx).
-  Windows Phone/Windows RT - Interface [IAuthenticationCallback](https://msdn.microsoft.com/library/microsoft.rightsmanagement.iauthenticationcallback.aspx).
- Linux - Interface [IAuthenticationCallback](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

### <a name="what-library-to-use-for-authentication"></a>Bibliothèque à utiliser pour l’authentification
Pour implémenter votre rappel d’authentification, vous devez télécharger une bibliothèque appropriée et de configurer votre environnement de développement pour qu’il l’utilise. Les bibliothèques ADAL pour ces plateformes se trouvent sur GitHub.

Chacune des ressources suivantes contient de l’aide pour la configuration de votre environnement et pour l’utilisation de la bibliothèque.

-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Pour le SDK Linux, la bibliothèque ADAL est fournie avec la source du SDK, disponible via [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

> [!NOTE]
> Nous vous recommandons d’utiliser une des bibliothèques ADAL, même si vous pouvez utiliser d’autres bibliothèques d’authentification.

### <a name="authentication-parameters"></a>Paramètres d’authentification

La bibliothèque ADAL nécessite plusieurs éléments d’information pour authentifier un utilisateur dans Azure RMS (ou AD RMS). Il s’agit de paramètres OAuth 2.0 standard qui sont généralement nécessaires pour toutes les applications Azure AD. Les instructions d’utilisation de la bibliothèque ADAL sont disponibles dans le fichier LISEZ-MOI des dépôts Github correspondants indiqués.

- **Autorité** : l’URL pour le point de terminaison d’authentification, généralement AAD ou ADFS.
- **Ressource** : l’URL/URI de l’application de service à laquelle vous essayez d’accéder, généralement Azure RMS ou AD RMS.
- **ID utilisateur** : l’UPN, généralement une adresse de messagerie, de l’utilisateur qui veut accéder à l’application. Ce paramètre peut être vide si l’utilisateur n’est pas encore connu ; il est également utilisé pour mettre en cache le jeton de l’utilisateur ou pour demander un jeton auprès du cache. Il est aussi généralement utilisé comme *indicateur* pour la confirmation de l’utilisateur.
- **ID de client** : l’ID de votre application cliente. Il doit s’agir d’un ID d’application Azure AD valide.
Il provient de l’étape d’inscription dans le portail Azure.
- **URI de redirection** : fournit la bibliothèque d’authentification avec une cible d’URI pour le code d’authentification. Des formats spécifiques sont nécessaires pour iOS et Android. Ils sont expliqués dans les fichiers LISEZ-MOI des dépôts GitHub correspondants de la bibliothèque ADAL. Cette valeur provient de l’étape d’inscription dans le portail Azure.

> [!NOTE]
> **L’étendue** n’est pas utilisée, mais peut l’être et est donc réservée à une utilisation future.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

> [!NOTE]
> Si votre application ne suit pas ces instructions, les flux de travail Azure RMS et Azure AD risquent d’échouer et ne sont pas pris en charge par Microsoft.com. En outre, il peut se produire une violation du contrat RMLA si un ID de client non valide est utilisé dans une application de production.

### <a name="what-should-an-authentication-callback-implementation-look-like"></a>Exemple d’implémentation d’un rappel d’authentification
**Exemples de code d’authentification** : ce SDK comprend un exemple de code montrant l’utilisation de rappels d’authentification. Pour votre commodité, ces exemples de code sont représentés ici, ainsi que dans chacune des rubriques liées.

**Authentification utilisateur Android** : pour plus d’informations, consultez [Exemples de code Android](android-code.md), **Étape 2** du premier scénario, « Consommation d’un fichier protégé par RMS ».


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**Authentification utilisateur iOS/OS X** : pour plus d’informations, consultez [Exemples de code iOS/OS X](ios-os-x-code-examples.md), *Étape 2 du premier scénario, « Consommation d’un fichier protégé par RMS ».*


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Authentification utilisateur Linux** : pour plus d’informations, consultez [Exemples de code Linux](linux-c-code-examples.md).



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }
