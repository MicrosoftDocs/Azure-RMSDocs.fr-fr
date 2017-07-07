---
title: "Procédure pour autoriser le fonctionnement de votre application de service avec le service RMS cloud | Azure RMS"
description: "Cette rubrique décrit les étapes qui permettent de configurer votre application de service pour qu’elle utilise Azure Rights Management."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 015a32453a92ab05d3ca99ed462e48ee9f5149eb
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>Comment : permettre à votre application de service de fonctionner avec le service RMS cloud

Cette rubrique décrit les étapes qui permettent de configurer votre application de service pour qu’elle utilise Azure Rights Management. Pour plus d’informations, consultez [Prise en main d’Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

**Important**  
Pour utiliser votre application de service de Rights Management Services SDK 2.1 avec Azure RMS, vous devez créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](../get-started/requirements-subscriptions.md).

## <a name="prerequisites"></a>Conditions préalables

-   RMS SDK 2.1 doit être installé et configuré. Pour plus d’informations, consultez [Prise en main de RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   Vous devez [créer une identité de service par le biais d’ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) à l’aide de l’option de clé symétrique, ou par d’autres moyens, et noter les informations clés de ce processus.

## <a name="connecting-to-the-azure-rights-management-service"></a>Connexion au service Rights Management Azure

-   Appelez [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx).
-   Définissez [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Remarque**  Pour plus d’informations, consultez [Définition du mode de sécurité d’API](setting-the-api-security-mode-api-mode.md)

     
-   Les étapes suivantes permettent de créer une instance de structure [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) avec le membre *pcCredential* ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) rempli avec les informations de connexion du service Azure Rights Management.
-   Utilisez les informations obtenues lors de la création de votre identité de service de clé symétrique (voir la configuration requise plus haut dans cette rubrique) pour définir les paramètres *wszServicePrincipal*, *wszBposTenantId* et *cbKey* quand vous créez une instance de structure [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Remarque** : En raison d’une condition existante avec notre service de découverte, si vous n’êtes pas en Amérique du Nord, les informations d’identification de clé symétrique des autres régions ne sont pas acceptées. Vous devez donc spécifier les URL des locataires directement. Cette opération s’effectue par le biais du paramètre *pConnectionInfo* (type [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx)) des fonctions [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) ou [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx).

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>Générer une clé symétrique et recueillir les informations nécessaires

### <a name="instructions-to-generate-a-symmetric-key"></a>Instructions pour générer une clé symétrique

-   Installez l’[Assistant de connexion Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152).
-   Installez le [Module Powershell Azure AD](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Remarque** : Vous devez être un administrateur client pour utiliser les applets de commande Powershell.

- Démarrez Powershell et exécutez les commandes suivantes pour générer une clé.

    `Import-Module MSOnline`

    `Connect-MsolService`(entrez vos informations d’identification d’administrateur)

    `New-MsolServicePrincipal`(entrez un nom d’affichage)

- Une fois la clé symétrique générée, les informations sur la clé sont transmises, notamment la clé elle-même et *AppPrincipalId*.

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>Instructions pour trouver **TenantBposId** et les **Urls**

-   Installez le [Module Powershell Azure RMS](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Démarrez Powershell et exécutez les commandes suivantes pour obtenir la configuration RMS du locataire.

    `Import-Module aadrm`

    `Connect-AadrmService`(entrez vos informations d’identification d’administrateur)

    `Get-AadrmConfiguration`


- Créez une instance de [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) et définissez quelques membres.

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


Pour plus d’informations, consultez [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

-   Créez une instance de structure [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) contenant votre instance de [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Remarque** : Les membres de *connectionInfo* sont définis avec des URL obtenues à partir de l’appel précédent à `Get-AadrmConfiguration` et notées ici avec ces noms de champs.

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### <a name="identify-a-template-and-then-encrypt"></a>Identifier un modèle, puis procéder au chiffrement

-   Sélectionnez un modèle à utiliser pour le chiffrement.
    Appelez [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) en passant la même instance de [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Avec le modèle indiqué plus haut dans cette rubrique, appelez [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx), en passant la même instance de [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).

Exemple d’utilisation de [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) :

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Exemple d’utilisation de [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx) :

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Vous avez maintenant terminé les étapes nécessaires pour permettre à votre application d’utiliser Azure Rights Management.

## <a name="related-topics"></a>Rubriques connexes

* [Bien démarrer avec Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Bien démarrer avec RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Créer une identité de service via ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]