---
title: "Exemple d’application IPCHelloWorld | Azure RMS"
description: "Cette rubrique contient des instructions pour créer un exemple d’application avec gestion des droits."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 581451A2-9558-4D0D-9D01-BEAB282C5A83
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ac6afddc2b39d6209ef1b89d8d84011942cdba5a
ms.openlocfilehash: e75ec6c04afd171552697f79deb33ad2cfe2c4e1


---
** Ce contenu de SDK n’est pas à jour. Vous trouverez temporairement la [version actuelle](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentation sur MSDN. **
# Exemple d’application IPCHelloWorld

Cette rubrique contient des instructions pour créer un exemple d’application avec gestion des droits.

IPCHelloWorld est une application simple qui vous aidera à comprendre les concepts de base et le code d’une application avec gestion des droits.

Téléchargez l’exemple d’application [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440) sur Microsoft Connect. Les autres éléments téléchargeables du site sont intégrés ici par commodité.

**Remarque** Le projet IPCHelloWorld est déjà configuré pour RMS SDK 2.1. Pour plus d’informations sur la configuration d’un nouveau projet en vue d’utiliser RMS SDK 2.1, consultez [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md).

 
Les sections suivantes abordent les étapes d’application clés et les concepts à connaître.

## Chargement du fichier MSIPC.dll

Avant de pouvoir appeler les fonctions de RMS SDK 2.1, vous devez d’abord appeler [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) pour charger le fichier MSIPC.dll.



    hr = IpcInitialize();

    if (FAILED(hr))
    {
      wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
      goto exit;
    }



## Énumération des modèles

Un modèle RMS définit la stratégie utilisée pour protéger les données, par exemple, définir les utilisateurs autorisés à accéder aux données et leurs droits. Les modèles RMS sont installés sur le serveur RMS.

La capture de code suivante énumère les modèles RMS disponibles sur le serveur RMS par défaut.



    hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

    if (FAILED(hr))
    {
      DisplayError(L"IpcGetTemplateList failed", hr);
      goto exit;
    }



Cet appel récupère les modèles RMS installés sur le serveur par défaut et charge les résultats dans la structure [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) indiquée par la variable *pcTil*, puis affiche les modèles.



    if (0 == pcTil->cTi)
    {
      wprintf(L"* No templates configured for your RMS server * \n\n");
      wprintf(L"\\------------------------------------------------------\n\n");
      goto exit;
    }

    for (DWORD dw = 0; dw < pcTil->cTi; dw++)
    {
      wprintf(L"Template #%d:\n", dw);
      wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
      wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
      wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
      wprintf(L"\n");
    }



## Sérialisation d’une licence

Avant de pouvoir protéger des données, vous devez sérialiser une licence et obtenir une clé de contenu. La clé de contenu est utilisée pour chiffrer les données sensibles. La licence sérialisée est généralement associée aux données chiffrées et utilisée par l’utilisateur des données protégées. L’utilisateur doit appeler la fonction [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) à l’aide de la licence sérialisée pour obtenir la clé de contenu qui permettra de déchiffrer le contenu et obtenir la stratégie associée au contenu.

Par souci de simplicité, utilisez le premier modèle RMS retourné par [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) pour sérialiser une licence.

Normalement, vous utiliseriez une boîte de dialogue pour permettre à l’utilisateur de sélectionner le modèle souhaité.



    hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
    0, NULL, &hContentKey, &pSerializedLicense);

    if (FAILED(hr))
    {
      DisplayError(L"IpcSerializeLicense failed", hr);
      goto exit;
    }



Une fois cela effectué, vous disposez de la clé de contenu (*hContentKey*) et de la licence sérialisée (*pSerializedLicense*) que vous devez associer aux données protégées.

## Protection des données

Vous êtes maintenant prêt à chiffrer les données sensibles avec la fonction [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt). Vous devez d’abord demander à la fonction **IpcEncrypt** la taille des données chiffrées.



    cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    NULL, 0, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }



Ici, *wszText* contient le texte brut que vous voulez protéger. La fonction [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) retourne la taille des données chiffrées dans le paramètre *cbEncrypted*.

Allouez de la mémoire pour les données chiffrées.



    pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

    if (NULL == pbEncrypted) {
      wprintf(L"Out of memory\n");
      goto exit;
    }


Vous pouvez maintenant effectuer le chiffrement.



    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    pbEncrypted, cbEncrypted, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }


Après cette étape, vous disposez des données chiffrées (*pbEncrypted*) et de la licence sérialisée (*pSerializedLicense*) qui sera utilisée par les utilisateurs pour déchiffrer les données.

## Gestion des erreurs

Dans cet exemple d’application, la fonction **DisplayError** est utilisée pour gérer les erreurs.



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


La fonction **DisplayError** utilise la fonction [**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) pour obtenir le message d’erreur à partir du code d’erreur correspondant et l’imprimer dans la sortie standard.

## Nettoyage

Avant de terminer, vous devez également libérer toutes les ressources allouées.



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

* [Notes du développeur](developer-notes.md)
* [Configurer Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
* [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
* [**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
* [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
 

 



<!--HONumber=Jun16_HO4-->


