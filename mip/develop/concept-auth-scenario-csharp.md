---
title: Concepts-scénarios d’authentification pour les clients C# du SDK MIP (Microsoft Information Protection)
description: Détails techniques sur les scénarios d’authentification pour les applications clientes C# du SDK Microsoft Information Protection.
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: bee7cb6854aa58f6d5c3c6781984875c8ee347a1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212618"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>Démarrage rapide : clients publics et confidentiels (C#)

Deux scénarios courants sont utilisés lors de la création d’applications avec le kit de développement logiciel (SDK) MIP. Le premier scénario voit l’utilisateur s’authentifier directement auprès de Azure AD. Dans le second, l’application s’authentifie à l’aide d’une clé ou d’un certificat du principal du service secret.

## <a name="public-client-applications"></a>Applications clientes publiques

Il s’agit d’applications de bureau ou mobiles dans lesquelles l’application en cours d’exécution sur l’appareil invite l’utilisateur à s’authentifier. L’utilisateur se connecte directement aux principaux services MIP. Dans ce scénario, les bibliothèques d’authentification doivent être utilisées pour s’assurer que l’utilisateur peut se connecter à Azure AD, répond à des exigences d’accès conditionnel ou à plusieurs facteurs et obtient un jeton OAuth2 pour la ressource appropriée.

Pour plus d’informations, consultez la [documentation relative au workflow d’authentification de client public](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options) .

Voici une capture de code rapide illustrant le déroulement de l’authentification du client public pour l’application cliente du kit de développement logiciel (SDK) Microsoft Information Protection à l’aide de Microsoft Authentication Library (MSAL).

```csharp

public string AcquireToken(Identity identity, string authority, string resource, string claims)
{
     var authorityUri = new Uri(authority);
     authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     _app = PublicClientApplicationBuilder.Create("<Application-Id>").WithAuthority(authority).WithDefaultRedirectUri().Build();

     var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
     var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                    .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

     return result.AccessToken;
}
```

**Locataire-GUID** est le GUID du client unique pour le locataire Azure ad.
L' **ID** d’application est l’ID de l’application dans l’inscription de l’application sur Azure ad portail.

## <a name="confidential-client-applications"></a>Applications clientes confidentielles

Ces applications sont des applications Cloud ou basées sur des services, où l’utilisateur ne se connecte pas directement aux services MIP principaux. Le service doit étiqueter, protéger ou ôter la protection du contenu compatible MIP. Dans ce scénario, l’application doit stocker un certificat ou une clé secrète d’application. Ces secrets seront utilisés pour l’authentification pour Azure AD et utiliser ce secret pour extraire des jetons pour les services MIP principaux du backend. Il peut ensuite utiliser les fonctionnalités de délégation du kit de développement logiciel (SDK) MIP pour protéger ou consommer du contenu pour le compte de l’utilisateur authentifié.

L’intégration du kit de développement logiciel MIP avec les applications basées sur des services requiert l’utilisation du workflow d’octroi d’informations d’identification du client. La bibliothèque d’authentification Microsoft (MSAL) peut être utilisée pour implémenter cela dans un modèle similaire à ce que nous verrions dans une application cliente publique. Cet article explique brièvement comment mettre à jour le kit de développement logiciel (SDK) MIP `IAuthDelegate` dans .net pour effectuer l’authentification pour les applications basées sur les services à l’aide de ce processus. Au moment de la publication, il n’existe aucune version de MSAL pour C++. Toutefois, il est possible d’implémenter ce processus par le biais d' [appels Rest directs](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow#get-a-token).

Pour plus d’informations, consultez la documentation sur le [Workflow d’authentification de client confidentiel](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)

Voici une capture de code rapide illustrant le workflow d’authentification du client confidentiel pour l’application cliente du kit de développement logiciel (SDK) Microsoft Information Protection à l’aide de Microsoft Authentication Library (MSAL). Une application peut s’authentifier à l’aide du certificat Active Directory ou de la clé secrète client.

> [!NOTE]
> Portez une attention particulière à cette ligne dans l’exemple suivant. 
>
> ```csharp
> string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
> ```
> Cela construit les étendues MSAL à partir de la ressource fournie à la `AcquireToken()` méthode. 

### <a name="msal-confidential-client-example"></a>Exemple de client confidentiel MSAL

```csharp
public string AcquireToken(Identity identity, string authority, string resource, string claim)
{
     AuthenticationResult result;
     var authorityUri = new Uri(authority);
     authority = string.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     // Certification Based Auth
     if (doCertAuth)
     {
          // Build ConfidentialClientApplication using certificate.
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithCertificate(certificate) //Assumption here is Application passes a certificate created using certificate thumbprint
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Client secret based Auth
     else
     {
          // Build ConfidentialClientApplication using app secret
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithClientSecret(clientSecret)
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };

     try{
          result = _app.AcquireTokenForClient(scopes).ExecuteAsync().Result;
     }
     catch (MsalServiceException ex) when (ex.Message.Contains("AADSTS70011"))
     {
          // Invalid scope. The scope has to be of the form "https://resourceurl/.default"
          // Mitigation: change the scope to be as expected
          Console.WriteLine("Scope provided is not supported");
          return null;
     }
            return result.AccessToken;
}

```
**Locataire-GUID** est le GUID du client unique pour le locataire Azure ad.
L' **ID** d’application est l’ID de l’application dans l’inscription de l’application sur Azure ad portail.