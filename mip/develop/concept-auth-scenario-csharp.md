---
title: Concepts-scénarios d’authentification pour les clients C# du SDK MIP (Microsoft Information Protection)
description: Détails techniques sur les scénarios d’authentification pour les applications clientes C# du SDK Microsoft Information Protection.
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 10d6f5ce615373f0955c42f2573b7ddd59629734
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2020
ms.locfileid: "95567918"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>Démarrage rapide : clients publics et confidentiels (C#)

Deux scénarios courants sont utilisés lors de la création d’applications avec le kit de développement logiciel (SDK) MIP. Un scénario montre que l’utilisateur s’authentifie directement auprès de Azure AD, où comme dans l’autre l’authentification, l’application utilise une clé ou un certificat de principal du service de secret.

## <a name="public-client-applications"></a>Applications clientes publiques

Il s’agit généralement d’applications de bureau ou mobiles où l’application en cours d’exécution sur l’appareil invite l’utilisateur à s’authentifier et l’utilisateur se connecte directement aux principaux services MIP. Dans ce scénario, les bibliothèques d’authentification doivent être utilisées pour s’assurer que l’utilisateur est en mesure de se connecter à Azure AD, répond à des exigences d’accès conditionnel ou à plusieurs facteurs et obtient un jeton OAuth2 pour la ressource appropriée.

Pour plus d’informations, reportez-vous à Azure AD [documentation relative à l’authentification des clients publics](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)

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

Locataire-GUID représente le GUID du locataire pour le Azure AD locataire, tandis que l’ID d’application est l’ID d’application dans l’inscription de l’application sur Azure AD portail.

## <a name="confidential-client-applications"></a>Applications clientes confidentielles

Il s’agit généralement d’applications Cloud ou basées sur les services où l’utilisateur ne se connecte pas directement aux services MIP principaux du backend, mais le service a besoin d’étiqueter, de protéger ou de ôter la protection du contenu compatible MIP. Dans ce scénario, l’application doit stocker un certificat ou un secret d’application à utiliser pour l’authentification pour Azure AD et utiliser ce secret pour récupérer les jetons pour les services MIP principaux du backend. Il peut ensuite utiliser les fonctionnalités de délégation du kit de développement logiciel (SDK) MIP pour protéger ou consommer du contenu pour le compte de l’utilisateur authentifié.

Pour plus d’informations, reportez-vous à Azure AD documentation sur le [Workflow d’authentification de client confidentiel](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)

Voici une capture de code rapide illustrant le déroulement de l’authentification du client confidentiel pour l’application cliente du kit de développement logiciel (SDK) Microsoft Information Protection à l’aide de Microsoft Authentication Library (MSAL). Une application peut s’authentifier à l’aide du certificat Active Directory ou de la clé secrète client.

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

Locataire-GUID représente le GUID du locataire pour le Azure AD locataire, tandis que l’ID d’application est l’ID d’application dans l’inscription de l’application sur Azure AD portail.