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

# Authentification ADAL pour votre application compatible RMS

L’authentification avec Azure RMS pour votre application à l’aide de la bibliothèque ADAL Azure fait désormais partie du client RMS 2.1.

En mettant à jour votre application pour utiliser l’authentification ADAL au lieu de l’Assistant de connexion Microsoft Online, vous et vos clients pouvez :

- Utiliser l’authentification multifacteur.
- Installer le client RMS 2.1 sans nécessiter de privilèges d’administration sur l’ordinateur.
- Certifier votre application pour Windows 10

## Deux approches de l’authentification

Cette rubrique contient deux approches de l’authentification avec des exemples de code correspondant.

- **Authentification interne** : authentification OAuth gérée par le SDK RMS. Adoptez cette approche si vous souhaitez que le client RMS affiche une invite d’authentification ADAL quand l’authentification est nécessaire. Pour plus d’informations sur la façon de configurer votre application, consultez la section « Authentification interne ».

> [!NOTE] Si votre application utilise actuellement AD RMS SDK 2.1 avec l’Assistant de connexion, nous vous recommandons d’utiliser la méthode d’authentification interne comme chemin de migration d’application.

- **Authentification externe** : authentification OAuth gérée par votre application. Adoptez cette approche si vous souhaitez que votre application gère sa propre authentification OAuth. Avec cette approche, le client RMS exerce un rappel défini par l’application quand l’authentification est nécessaire. Pour obtenir un exemple détaillé, consultez « Authentification externe » à la fin de cette rubrique.

> [!NOTE] L’authentification externe n’implique pas la possibilité de modifier les utilisateurs. Le client RMS utilise toujours l’utilisateur par défaut pour un client RMS donné.

### Authentification interne

Vous avez besoin des éléments suivants :

- Un [abonnement à Microsoft Azure](https://azure.microsoft.com/en-us/) (une version d’évaluation gratuite suffit).
- Un abonnement à Microsoft Azure Rights Management (un compte [RMS for Individuals](https://technet.microsoft.com/en-us/library/dn592127.aspx) gratuit suffit).

> [!NOTE] Vérifiez auprès de votre administrateur informatique si vous avez un abonnement Microsoft Azure Rights Management et demandez-lui d’effectuer les étapes ci-dessous. Si votre organisation n’a pas d’abonnement, demandez à votre administrateur informatique d’en créer un. En outre, votre administrateur informatique doit s’abonner avec un compte professionnel ou scolaire, et non un compte Microsoft (tel que Hotmail).

Après vous être inscrit à Microsoft Azure :

- Connectez-vous au [portail de gestion Azure](https://manage.windowsazure.com) de votre organisation à l’aide d’un compte disposant de privilèges d’administrateur.

![Connexion Azure](../media/AzurePortalLogin.png)

- Naviguez jusqu’à l’application **Active Directory** sur le côté gauche du portail.

![Sélectionnez Active Directory](../media/AzureADPick.png)

- Si vous n’avez pas encore créé d’annuaire, cliquez sur le bouton **Nouveau** dans le coin inférieur gauche du portail.

![Sélectionnez NOUVEAU](../media/AzureNewBtn.png)

- Sélectionnez l’onglet **Rights Management** et vérifiez que **Statut de Rights Management** est **Actif**, **Inconnu** ou **Non autorisé**. Si le statut est **Inactif**, cliquez sur le bouton **Activer** situé en bas au milieu du portail et confirmez votre sélection.

![Choisissez ACTIVER](../media/RMTab.png)

- Maintenant, créez une *Application native* dans votre annuaire en le sélectionnant et en choisissant Applications.

![Sélectionnez APPLICATIONS](../media/CreateNativeApp.png)

- Ensuite, cliquez sur le bouton **Ajouter** situé en bas au milieu du portail.

![Sélectionnez AJOUTER](../media/AddAppBtn.png)

- À l’invite, choisissez **Ajouter une application développée par mon organisation**.

![Sélectionnez Ajouter une application développée par mon organisation](../media/AddAnAppPick.png)

- Nommez votre application en sélectionnant **APPLICATION CLIENTE NATIVE** et en cliquant sur le bouton **Suivant**.

![Nommez votre application](../media/TellUsInput.png)

- Ajoutez une URI de redirection et cliquez sur Suivant. L’URI de redirection doit être un URI valide et unique dans votre annuaire. Par exemple, vous pouvez utiliser quelque chose comme `com.mycompany.myapplication://authorize`.

![Ajoutez un URI de redirection](../media/RedirectURI.png)

- Sélectionnez votre application dans l’annuaire et choisissez **CONFIGURER**.

![Choisissez CONFIGURER](../media/ConfigYourApp.png)

>[!NOTE] Copiez l’**ID CLIENT** et l’**URI de redirection** et stockez-les pour une utilisation ultérieure lors de la configuration du client RMS.

- Accédez au bas de vos paramètres d’application et cliquez sur le bouton **Ajouter une application** sous **Autorisations pour d’autres applications**.

![Sélectionnez Ajouter une application](../media/PermissionsToOtherBtn.png)

- Maintenant, ajoutez ce GUID `00000012-0000-0000-c000-000000000000` à la zone d’édition **COMMENÇANT PAR** et cliquez sur la coche.

![Ajoutez le GUID](../media/AddGUID.png)

- Cliquez sur le signe plus (+) situé en regard de **Microsoft Rights Management**.

![Sélectionnez le bouton +](../media/ChoosePlusBtn.png)

- Maintenant, cliquez sur la coche située dans le coin inférieur gauche de la boîte de dialogue.

![Cliquez sur la coche](../media/ChooseCheck.png)

- Vous êtes maintenant prêt à ajouter une dépendance à votre application pour Azure RMS. Pour ajouter la dépendance, sélectionnez la nouvelle entrée **Microsoft Rights Management Services** sous **Autorisations pour d’autres applications** et cochez la case **Créer et accéder au contenu protégé pour les utilisateurs** dans la liste déroulante **Autorisations déléguées**.

![Configurez les autorisations](../media/AddDependency.png)

- Enregistrez votre application pour conserver les modifications en cliquant sur l’icône **Enregistrer** située en bas au milieu du portail.

![Sélectionnez ENREGISTRER](../media/SaveApplication.png)

- Vous êtes maintenant prêt à configurer votre application pour utiliser l’authentification ADAL interne fournie par RMS SDK 2.1. Pour configurer votre client RMS, ajoutez un appel à [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) juste après l’appel à [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) pour configurer le client RMS. Utilisez l’extrait de code suivant en guise d’exemple.


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID_fourni_par_AAD_pour_votre_application(pas_de_parenthèses)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### Authentification externe

- Utilisez ce code comme exemple illustrant comment gérer vos propres jetons d’authentification.


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey)   {     IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT     {         wstring wstrToken;         HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);         return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;     };

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
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### Rubriques connexes
- [Types de données](/rights-management/sdk/2.1/api/win/Data%20types)
- [Propriétés d’environnement](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=May16_HO2-->


