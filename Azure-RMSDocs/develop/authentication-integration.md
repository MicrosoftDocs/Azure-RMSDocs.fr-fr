---
# required metadata

title: Procédure : ajout de l’authentification à votre application | Azure RMS
description: Décrit les principes fondamentaux de l’authentification utilisateur pour votre application RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 94697eb5-1fab-4591-bd40-b5646daac8a3

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Procédure : ajout de l’authentification à votre application

Cette rubrique décrit les principes fondamentaux de l’authentification utilisateur pour votre application RMS.

## Qu’est-ce que l’authentification utilisateur ?
L’authentification utilisateur est une étape essentielle pour établir la communication entre votre application et l’infrastructure RMS. Le processus d’authentification utilise le protocole OAuth 2.0 standard qui requiert les éléments d’information suivants sur l’utilisateur actuel et sur sa demande d’authentification :**autorité**, **ressource** et **ID utilisateur**.

**Remarque** : L’étendue n’est pas utilisée actuellement, mais elle peut l’être et est donc réservée à une utilisation future.

 

**Rappel d’authentification utilisateur** : Microsoft Rights Management SDK 4.2 utilise votre implémentation d’un rappel d’authentification quand vous ne fournissez pas un jeton d’accès, quand votre jeton d’accès doit être actualisé ou quand le jeton d’accès a expiré.

Chacune des API RMS de la plateforme a un rappel qui doit être implémenté afin d’activer l’authentification de l’utilisateur.

-   L’API Android utilise les interfaces [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) et [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java).
-   L’API iOS/OS X utilise le protocole [**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc).
-   L’API WinPhone utilise l’interface [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback).
-   L’API Linux utilise l’interface [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

## Bibliothèque à utiliser pour l’authentification

Pour implémenter votre rappel d’authentification, vous devez télécharger une bibliothèque appropriée et de configurer votre environnement de développement pour qu’il l’utilise. Les bibliothèques ADAL pour ces plateformes se trouvent sur GitHub. Chacune des ressources suivantes contient de l’aide pour la configuration de votre environnement et pour l’utilisation de la bibliothèque.

-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Bibliothèque d’authentification Windows Azure Active Directory (ADAL) pour dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Pour le SDK Linux, la bibliothèque ADAL est fournie avec la source du SDK, disponible via [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

**Remarque** : Nous vous recommandons d’utiliser une des bibliothèques d’authentification Active Directory (ADAL) ci-dessus, même si vous pouvez utiliser d’autres bibliothèques d’authentification.

## Entrées pour l’authentification avec la bibliothèque d’authentification Azure Active Directory (ADAL)

La bibliothèque ADAL nécessite plusieurs paramètres pour authentifier un utilisateur avec succès auprès d’Azure RMS (ou AD RMS). Voici les paramètres OAuth 2.0 standard qui sont généralement requis d’une application Azure AD, comme avec les applications RMS. Vous trouverez les instructions d’utilisation de la bibliothèque ADAL dans le fichier LISEZMOI des dépôts Github correspondants précédemment répertoriés.

Ces paramètres et ces instructions sont requises pour les flux de travail RMS :

-   **Autorité** : l’URL pour le point de terminaison d’authentification, généralement AAD ou ADFS. Ce paramètre est fourni à votre application par le rappel d’authentification de RMS SDK.
-   **Ressource** : l’URL/URI de l’application de service à laquelle vous essayez d’accéder, généralement Azure RMS ou AD RMS. Ce paramètre est fourni à votre application par le rappel d’authentification de RMS SDK.
-   **ID utilisateur** : l’UPN, généralement une adresses de messagerie, de l’utilisateur qui veut accéder à l’application. Ce paramètre peut être vide si l’utilisateur n’est pas encore connu ; il est également utilisé pour mettre en cache le jeton de l’utilisateur ou pour demander un jeton auprès du cache. Ceci est généralement utilisé comme un « indicateur » pour la confirmation de l’utilisateur.
-   **ID de client** : l’ID de votre application cliente. Il doit s’agir d’un ID d’application Azure AD valide. Pour plus d’informations, consultez Procédure : obtention d’un ID d’application Azure.
-   **URI de redirection** : fournit la bibliothèque d’authentification avec une cible d’URI pour le code d’authentification. Notez que des formats spécifiques sont requis pour iOS et Android. Ils sont expliqués dans les fichiers LISEZMOI des dépôts GitHub correspondants de la bibliothèque ADAL.

    Android : `msauth://packagename/Base64UrlencodedSignature`

    iOS : `<app-scheme>://<bundle-id>`

**Remarque** : Si votre application ne suit pas ces instructions, les flux de travail Azure RMS et Azure AD risquent d’échouer et ne sont pas prise en charge par Microsoft.com. En outre, il peut se produire une violation du contrat RMLA si un ID de client non valide est utilisé dans une application de production.

## Exemple d’implémentation d’un rappel d’authentification

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


**Authentification utilisateur iOS/OS X** : pour plus d’informations, consultez [Exemples de code iOS/OS X](ios-os-x-code-examples.md),

**Étape 2** du premier scénario, « Consommation d’un fichier protégé par RMS ».


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



**Authentification utilisateur Linux / C++** : pour plus d’informations, consultez [Exemples de code Linux](linux-c-code-examples.md).



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



 

 


<!--HONumber=Apr16_HO3-->


