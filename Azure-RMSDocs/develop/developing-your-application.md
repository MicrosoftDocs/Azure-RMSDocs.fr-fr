---
title: "Développement de votre application | Azure RMS"
description: "Instructions de développement d’une application à l’aide de RMS SDK 2.1."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 11/01/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4560a1cf3424ae4dddd3a0675b62e9c5e55de9fa
ms.openlocfilehash: 1f46d93a47fae3b7e7de334db73b7e7b65ea6eea


---

# <a name="developing-your-application"></a>Développement de votre application

Cette rubrique contient des conseils essentiels liés aux principaux aspects d’une application compatible RMS. Vous pouvez vous appuyer sur ces conseils pour développer votre propre application.

## <a name="introduction"></a>Introduction

Les instructions données dans cette rubrique reposent sur l’exemple d’application *IPCHelloWorld*, lequel vous permet de découvrir les concepts et le code de base d’une application avec gestion des droits. Le projet *IPCHelloWorld* est déjà configuré pour Rights Management Services SDK 2.1.

### <a name="download-sample"></a>Télécharger l’exemple
- Vérifiez que vous vous êtes inscrit auprès du site Connect :
  - Pour vous inscrire, accédez à [Connect](http://connect.microsoft.com)
  - Connectez-vous avec votre compte Microsoft.
  - Accédez au [site Connect Rights Management](https://connect.microsoft.com/site1170)
  - Inscrivez-vous 
- Téléchargez l’exemple d’application *IPCHellowWorld* complet qui se trouve dans le fichier [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)

Pour plus d’informations sur la configuration d’un nouveau projet en vue d’utiliser RMS SDK 2.1, consultez [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).



## <a name="loading-msipcdll"></a>Chargement du fichier MSIPC.dll

Pour pouvoir appeler des fonctions de RMS SDK 2.1, vous devez d’abord appeler [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) pour charger MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## <a name="enumerating-templates"></a>Énumération des modèles

Un modèle RMS définit la stratégie utilisée pour protéger les données, par exemple, définir les utilisateurs autorisés à accéder aux données et leurs droits. Les modèles RMS sont installés sur le serveur RMS.

La capture de code suivante énumère les modèles RMS disponibles sur le serveur RMS par défaut.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Cet appel récupère les modèles RMS installés sur le serveur par défaut et charge les résultats dans la structure [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx) indiquée par la variable *pcTil*, puis affiche les modèles.

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

## <a name="serializing-a-license"></a>Sérialisation d’une licence

Avant de pouvoir protéger des données, vous devez sérialiser une licence et obtenir une clé de contenu. La clé de contenu est utilisée pour chiffrer les données sensibles. La licence sérialisée est généralement associée aux données chiffrées et utilisée par l’utilisateur des données protégées. L’utilisateur doit appeler la fonction [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx) à l’aide de la licence sérialisée pour obtenir la clé de contenu qui permettra de déchiffrer le contenu ainsi que la stratégie associée à ce contenu.

Pour simplifier, utilisez le premier modèle RMS retourné par [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) pour sérialiser une licence.

Normalement, vous utiliseriez une boîte de dialogue pour permettre à l’utilisateur de sélectionner le modèle souhaité.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Une fois cela effectué, vous disposez de la clé de contenu (*hContentKey*) et de la licence sérialisée (*pSerializedLicense*) que vous devez associer aux données protégées.


## <a name="protecting-data"></a>Protection des données

Vous êtes maintenant prêt à chiffrer les données sensibles avec la fonction [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx). Vous devez d’abord demander à la fonction **IpcEncrypt** la taille des données chiffrées.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Ici, *wszText* contient le texte brut que vous voulez protéger. La fonction [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx) retourne la taille des données chiffrées dans le paramètre *cbEncrypted*.

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

## <a name="error-handling"></a>Gestion des erreurs

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

La fonction *DisplayError* utilise la fonction [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx) pour obtenir le message d’erreur à partir du code d’erreur correspondant et l’imprimer dans la sortie standard.

## <a name="cleaning-up"></a>Nettoyage

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

## <a name="related-topics"></a>Rubriques connexes

- [Guide et informations pour les développeurs](developer-notes.md)
- [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx)
- [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Nov16_HO1-->


