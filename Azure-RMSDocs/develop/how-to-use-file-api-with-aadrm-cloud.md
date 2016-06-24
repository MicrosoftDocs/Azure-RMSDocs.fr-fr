---
# required metadata

title: Procédure pour autoriser le fonctionnement de votre application de service avec le service RMS cloud | Azure RMS
description: Cette rubrique décrit les étapes qui permettent de configurer votre application de service pour qu’elle utilise Azure Rights Management.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Comment : permettre à votre application de service de fonctionner avec le service RMS cloud

Cette rubrique décrit les étapes qui permettent de configurer votre application de service pour qu’elle utilise Azure Rights Management. Pour plus d’informations, consultez [Prise en main d’Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx).

**Important**  
Pour utiliser votre application de service de Rights Management Services SDK 2.1 avec Azure RMS, vous devez créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](/rights-management/get-started/requirements-subscriptions.md).

## Conditions préalables

-   RMS SDK 2.1 doit être installé et configuré. Pour plus d’informations, consultez [Prise en main de RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   Vous devez [créer une identité de service par le biais d’ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) à l’aide de l’option de clé symétrique, ou par d’autres moyens, et noter les informations clés de ce processus.

## Connexion au service Rights Management Azure

-   Appelez [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize).
-   Définissez [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Remarque**  Pour plus d’informations, consultez [Définition du mode de sécurité d’API](setting-the-api-security-mode-api-mode.md)

     
-   Les étapes suivantes permettent de créer une instance de structure [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) avec le membre **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) rempli avec les informations de connexion du service Azure Rights Management.
-   Utilisez les informations obtenues lors de la création de votre identité de service de clé symétrique (voir la configuration requise plus haut dans cette rubrique) pour définir les paramètres **wszServicePrincipal**, **wszBposTenantId** et **cbKey** quand vous créez une instance de structure [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Remarque** En raison d’une condition existante avec notre service de découverte, si vous n’êtes pas en Amérique du Nord, les informations d’identification de clé symétrique d’autres régions ne sont pas acceptées. Vous devez donc spécifier les URL des locataires directement. Cette opération s’effectue par le biais du paramètre [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) de [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) ou [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist).

## Générer une clé symétrique et recueillir les informations nécessaires

### Instructions pour générer une clé symétrique

-   Installez l’[Assistant de connexion Microsoft Online](http://go.microsoft.com/fwlink/p/?LinkID=286152).
-   Installez le [Module Powershell Azure AD](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Remarque**  Vous devez être un administrateur de clients pour utiliser les applets de commande Powershell.

-   Démarrez Powershell et exécutez les commandes suivantes pour générer une clé         `Import-Module MSOnline`
            `Connect-MsolService` (entrez vos informations d’identification d’administrateur)         `New-MsolServicePrincipal` (entrez un nom complet)
-   Une fois la clé symétrique générée, les informations sur la clé sont transmises, notamment la clé elle-même et **AppPrincipalId**.


    La clé symétrique suivante a été créée car aucune n’a été fournie : ZYbF/lTtwE28qplQofCpi2syWd11D83 + A3DRlb2Jnv8 =

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### Instructions pour trouver **TenantBposId** et les **Urls**

-   Installez le [Module Powershell Azure RMS](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Démarrez Powershell et exécutez les commandes suivantes pour obtenir la configuration RMS du locataire.

    `Import-Module aadrm`

    `Connect-AadrmService` (entrez vos informations d’identification d’administrateur)

    `Get-AadrmConfiguration`


-   Créez une instance de  [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) et définissez quelques membres.

    // Créer une structure de clés.
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // Définir chaque membre avec les informations obtenues lors de la création du service.
    symKey.wszBase64Key = "votre_clé_de_principal_du_service"; symKey.wszAppPrincipalId = "votre_identificateur_de_principal_d’application"; symKey.wszBposTenantId = "votre_identificateur_de_locataire";


Pour plus d’informations, consultez [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

-   Créez une instance de structure [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) contenant votre instance de [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Remarque** Les membres de *connectionInfo* sont définis avec des URL obtenues à partir de l’appel précédent à `Get-AadrmConfiguration` et notées ici avec ces noms de champs.

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

### Identifier un modèle, puis procéder au chiffrement

-   Sélectionnez un modèle à utiliser pour le chiffrement.
    Appelez [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) en passant la même instance de [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Avec le modèle indiqué plus haut dans cette rubrique, appelez [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile), en passant la même instance de [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).

Exemple d’utilisation de [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) :

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Exemple d’utilisation de [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile) :

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Vous avez maintenant terminé les étapes nécessaires pour permettre à votre application d’utiliser Azure Rights Management.

## Rubriques connexes

* [Prise en main d’Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Prise en main de RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Créer une identité de service à l’aide d’ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 


<!--HONumber=Jun16_HO2-->


