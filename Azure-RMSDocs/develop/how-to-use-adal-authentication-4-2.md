---
title: "Utiliser le portail Azure pour configurer l’authentification RMS | Azure RMS"
description: "Décrit le processus d’authentification avec la bibliothèque ADAL"
keywords: authentification, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3f43f5605b1c341d7be618327038d1a86a305a5b
ms.openlocfilehash: cb82f0333ed17ee2994608baa3bbb50d42f19073


---

# Procédure : Utilisation du portail Azure pour configurer l’authentification RMS

Authentification auprès d’Azure RMS pour votre application à l’aide de la bibliothèque d’authentification ADAL (Azure Active Directory Authentication Library).

Pour utiliser cette approche, votre application doit gérer sa propre authentification OAuth. Avec cette approche, le client RMS exerce un rappel défini par l’application quand l’authentification est nécessaire.

## Configuration dans le portail Azure
Commencez par suivre ce guide pour effectuer la configuration dans le portail Azure, [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md). Copiez et enregistrez *l’ID client* et *l’URI de redirection* de ce processus pour les utiliser plus tard.

## Exemple de code
Voici un extrait de code de l’exemple de code client mobile permettant d’activer Azure ADAL. Pour plus d’informations, consultez l’exemple complet dans [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## Rubriques connexes

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Configurer Azure RMS pour l’authentification ADAL](adal-auth.md)



<!--HONumber=Jul16_HO3-->


