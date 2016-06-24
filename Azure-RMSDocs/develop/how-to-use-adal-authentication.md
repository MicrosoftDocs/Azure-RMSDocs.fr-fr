---
# required metadata

title: Authentification ADAL pour votre application compatible RMS | Azure RMS
description: Décrit le processus d’authentification avec la bibliothèque ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Comment : utiliser l’authentification ADAL

Authentification auprès d’Azure RMS pour votre application à l’aide de la bibliothèque d’authentification ADAL (Azure Active Directory Authentication Library).

En mettant à jour votre application pour utiliser l’authentification ADAL au lieu de l’Assistant de connexion Microsoft Online, vous et vos clients pouvez :

- Utiliser l’authentification multifacteur.
- Installer le client RMS 2.1 sans nécessiter de privilèges d’administration sur l’ordinateur.
- Certifier votre application pour Windows 10

## Deux approches de l’authentification

Cette rubrique contient deux approches de l’authentification avec des exemples de code correspondant.

- **Authentification interne** : authentification OAuth gérée par le SDK RMS.

  Adoptez cette approche si vous souhaitez que le client RMS affiche une invite d’authentification ADAL quand l’authentification est nécessaire. Pour plus d’informations sur la façon de configurer votre application, consultez la section « Authentification interne ».

  > [!Note] Si votre application utilise actuellement AD RMS SDK 2.1 avec l’Assistant de connexion, nous vous recommandons d’utiliser la méthode d’authentification interne comme chemin de migration d’application.

- **Authentification externe** : authentification OAuth gérée par votre application.

  Adoptez cette approche si vous souhaitez que votre application gère sa propre authentification OAuth. Avec cette approche, le client RMS exerce un rappel défini par l’application quand l’authentification est nécessaire. Pour obtenir un exemple détaillé, consultez « Authentification externe » à la fin de cette rubrique.

  > [!Note] L’authentification externe n’implique pas la possibilité de modifier les utilisateurs. Le client RMS utilise toujours l’utilisateur par défaut pour un client RMS donné.

## Authentification interne

1. Suivez les étapes de configuration d’Azure indiquées dans [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md), puis revenez à l’étape d’initialisation de l’application suivante.
2. Vous êtes maintenant prêt à configurer votre application pour utiliser l’authentification ADAL interne fournie par RMS SDK 2.1.

Pour configurer votre client RMS, ajoutez un appel à [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) juste après l’appel à [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize). Utilisez l’extrait de code suivant en guise d’exemple.

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## Authentification externe

Utilisez ce code en tant qu’exemple du mode de gestion de vos propres jetons d’authentification.
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

          IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
          {
              sizeof(IPC_OAUTH2_CALLBACK_INFO),
              pfGetADALToken,
              pContextForAdal
          };

          IPC_CREDENTIAL credentialContext =
          {
              IPC_CREDENTIAL_TYPE_OAUTH2,
              NULL
          };
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## Rubriques connexes

* [Types de données](/rights-management/sdk/2.1/api/win/datatypes)
* [Propriétés d’environnement](/rights-management/sdk/2.1/api/win/environmentproperties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IIPC_OAUTH2_CALLBACK_INFO)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IIPC_AAD_APPLICATION_ID)


<!--HONumber=Jun16_HO2-->


