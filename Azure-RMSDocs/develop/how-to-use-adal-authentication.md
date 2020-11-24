---
title: Authentification ADAL pour votre application compatible RMS | Azure RMS
description: Consultez Comment authentifier votre application avec Azure RMS à l’aide de la bibliothèque d’authentification Azure Active Directory (ADAL).
keywords: authentification, RMS, ADAL
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: a7cf207b0976db31ffa4df83d20e172876c7ee88
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568314"
---
# <a name="how-to-use-adal-authentication"></a>Comment : utiliser l’authentification ADAL

Authentification auprès d’Azure RMS pour votre application à l’aide de la bibliothèque d’authentification ADAL (Azure Active Directory Authentication Library).

En mettant à jour votre application pour utiliser l’authentification ADAL au lieu de l’Assistant de connexion Microsoft Online, vous et vos clients pouvez :

- utiliser l’authentification multifacteur ;
- Installer le client RMS 2.1 sans nécessiter de privilèges d’administration sur l’ordinateur.
- Certifier votre application pour Windows 10

## <a name="two-approaches-to-authentication"></a>Deux approches de l’authentification

Cette rubrique contient deux approches de l’authentification avec des exemples de code correspondant.

- **Authentification interne** : authentification OAuth gérée par le SDK RMS.

  Adoptez cette approche si vous souhaitez que le client RMS affiche une invite d’authentification ADAL quand l’authentification est nécessaire. Pour plus d’informations sur la façon de configurer votre application, consultez la section « Authentification interne ».

  > [!Note]
  > Si votre application utilise actuellement AD RMS SDK 2.1 avec l’Assistant de connexion, nous vous recommandons d’utiliser la méthode d’authentification interne comme chemin de migration d’application.

- **Authentification externe** : authentification OAuth gérée par votre application.

  Adoptez cette approche si vous souhaitez que votre application gère sa propre authentification OAuth. Avec cette approche, le client RMS exerce un rappel défini par l’application quand l’authentification est nécessaire. Pour obtenir un exemple détaillé, consultez « Authentification externe » à la fin de cette rubrique.

  > [!Note]
  > L’authentification externe n’implique pas la possibilité de modifier les utilisateurs. Le client RMS utilise toujours l’utilisateur par défaut pour un client RMS donné.

## <a name="internal-authentication"></a>Authentification interne

1. Suivez les étapes de configuration d’Azure indiquées dans [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md), puis revenez à l’étape d’initialisation de l’application suivante.
2. Vous êtes maintenant prêt à configurer votre application pour utiliser l’authentification ADAL interne fournie par RMS SDK 2.1.

Pour configurer votre client RMS, ajoutez un appel à [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty) juste après l’appel à [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize). Utilisez l’extrait de code suivant en guise d’exemple.

```cpp
IpcInitialize();

IPC_AAD_APPLICATION_ID applicationId = { 0 };
applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
if (FAILED(hr)) {
  //Handle the error
}
```

## <a name="external-authentication"></a>Authentification externe

Utilisez ce code en tant qu’exemple du mode de gestion de vos propres jetons d’authentification.

```cpp
extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

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
```

## <a name="related-topics"></a>Rubriques connexes

- [Types de données](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-data-types)
- [Propriétés de l’environnement](/previous-versions/windows/desktop/msipc/environment-properties)
- [IpcCreateOAuth2Token](/previous-versions/windows/desktop/msipc/ipccreateoauth2token)
- [IpcGetKey](/previous-versions/windows/desktop/msipc/ipcgetkey)
- [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
- [IPC_CREDENTIAL](/previous-versions/windows/desktop/msipc/ipc-credential)
- [IPC_NAME_VALUE_LIST](/previous-versions/windows/desktop/msipc/ipc-name-value-list)
- [IPC_OAUTH2_CALLBACK_INFO](/previous-versions/windows/desktop/msipc/ipc-oath2-callback-info)
- [IPC_PROMPT_CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
- [IPC_AAD_APPLICATION_ID](/previous-versions/windows/desktop/msipc/ipc-aad-application-id)