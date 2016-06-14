---
# required metadata

title: Développement de votre application | Azure RMS
description: Instructions de développement d’une application à l’aide de RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Développement de votre application

Cette rubrique contient des conseils essentiels liés aux principaux aspects d’une application compatible RMS. Vous pouvez vous appuyer sur ces conseils pour développer votre propre application.

## Introduction

Les instructions données dans cette rubrique reposent sur l’exemple d’application IPCHelloWorld, lequel vous permet de découvrir les concepts et le code de base d’une application avec gestion des droits. Vous pouvez télécharger l’exemple d’application IPCHellowWorld complet, nommé [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440), à partir de Microsoft Connect.

>AZURE.NOTE Le projet IPCHelloWorld est déjà configuré pour Rights Management Services SDK 2.1. Pour plus d’informations sur la configuration d’un nouveau projet en vue d’utiliser RMS SDK 2.1, consultez [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).

## Chargement du fichier MSIPC.dll

Pour pouvoir appeler des fonctions de RMS SDK 2.1, vous devez d’abord appeler [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) pour charger MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## Énumération des modèles

Un modèle RMS définit la stratégie utilisée pour protéger les données, par exemple, définir les utilisateurs autorisés à accéder aux données et leurs droits. Les modèles RMS sont installés sur le serveur RMS.

La capture de code suivante énumère les modèles RMS disponibles sur le serveur RMS par défaut.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Cet appel récupère les modèles RMS installés sur le serveur par défaut et charge les résultats dans la structure [IPC_TIL](/rights-management/sdk/2.1/api/win/functions#msipc_ipctil) indiquée par la variable *pcTil*, puis affiche les modèles.

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## Sérialisation d’une licence

Avant de pouvoir protéger des données, vous devez sérialiser une licence et obtenir une clé de contenu. La clé de contenu est utilisée pour chiffrer les données sensibles. La licence sérialisée est généralement associée aux données chiffrées et utilisée par l’utilisateur des données protégées. L’utilisateur doit appeler la fonction [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) à l’aide de la licence sérialisée pour obtenir la clé de contenu qui permettra de déchiffrer le contenu ainsi que la stratégie associée à ce contenu.

Pour simplifier, utilisez le premier modèle RMS retourné par [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) pour sérialiser une licence.

Normalement, vous utiliseriez une boîte de dialogue pour permettre à l’utilisateur de sélectionner le modèle souhaité.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Une fois cela effectué, vous disposez de la clé de contenu (*hContentKey*) et de la licence sérialisée (*pSerializedLicense*) que vous devez associer aux données protégées.


## Protection des données

Vous êtes maintenant prêt à chiffrer les données sensibles avec la fonction [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt). Vous devez d’abord demander à la fonction **IpcEncrypt** la taille des données chiffrées.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Ici, wszText contient le texte brut que vous voulez protéger. La fonction [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) retourne la taille des données chiffrées dans le paramètre *cbEncrypted*.

Allouez de la mémoire pour les données chiffrées.

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

Vous pouvez maintenant effectuer le chiffrement.

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Après cette étape, vous disposez des données chiffrées (*pbEncrypted*) et de la licence sérialisée (*pSerializedLicense*) qui sera utilisée par les utilisateurs pour déchiffrer les données.

## Gestion des erreurs

Dans cet exemple d’application, la fonction *DisplayError* est utilisée pour gérer les erreurs.

      C++
      void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
      {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
      }

La fonction *DisplayError* utilise la fonction [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) pour obtenir le message d’erreur à partir du code d’erreur correspondant et l’imprimer dans la sortie standard.

## Nettoyage

Avant de terminer, vous devez également libérer toutes les ressources allouées.

      C++
      if (NULL != pbEncrypted) {
        LocalFree((HLOCAL)pbEncrypted);
      }

      if (NULL != pSerializedLicense) {
        IpcFreeMemory((LPVOID)pSerializedLicense);
      }

      if (NULL != hContentKey) {
        IpcCloseHandle((IPC_HANDLE)hContentKey);
      }

      if (NULL != pcTil) {
        IpcFreeMemory((LPVOID)pcTil);
      }

## Rubriques connexes

- [Guide et informations pour développeurs](developer-notes.md)
- [IpcEncrypt](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
- [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
- [IPC_TIL](/rights-management/sdk/2.1/api/win/functions#msipc_ipctil)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)


<!--HONumber=Jun16_HO2-->


