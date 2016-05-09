---
# required metadata

title: Procédure : obtention d’un ID d’application Azure | Azure RMS
description: La création d’une application RMS avec Microsoft Rights Management SDK 4.2 nécessite la création d’un contrat avec l’équipe RMS.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834c5943-a724-4322-9035-060c1112fe22

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# Procédure : obtention d’un ID d’application Azure

La création d’une application RMS avec Microsoft Rights Management SDK 4.2 nécessite la création d’un contrat avec l’équipe RMS.

## Vue d'ensemble

La création et la publication d’une application RMS avec MS RMS SDK 4.2 nécessitent également la création d’un contrat d’utilisation de services avec l’équipe RMS. Ce contrat, également appelé Contrat de licence Rights Management (RMLA, Rights Management License Agreement) vous aide à honorer le contrat pour la protection de contenu que vous allez faire respecter pour le compte de l’utilisateur et/ou du propriétaire du contenu via les comportements (respect des règles d’entreprise) de votre application. En tant que créateur d’une application RMS, votre contrat avec l’équipe RMS sera appliqué via l’existence d’un « ID d’application Azure » qui représente ce contrat et qui permet à votre application de se connecter au service d’authentification Azure AD.

## Traiter

Utilisez les étapes suivantes pour créer votre ID d’application et pour signer votre contrat d’utilisation avec l’équipe RMS.

-   Suivez les instructions de la rubrique [Comment créer un ID d’application sur Azure](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx) pour créer votre ID d’application.
-   Écrivez à l’équipe RMS pour lancer le traitement de votre contrat RMLA, en envoyant votre « ID d’application » à <askipteam@microsoft.com>.
-   Signez le contrat RMLA et renvoyez-le à l’équipe RMS.
-   Maintenant que vous avez un contrat RMLA signé, vous devez passer l’ID d’application lors de l’appel de la bibliothèque d’authentification via le paramètre *clientID*.

    Voici à quoi ressemble l’appel d’authentification dans notre rubrique [Exemples de code iOS/OS X](ios-os-x-code-examples.md).


    // Retrieve token using ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**Remarque** : Si l’équipe RMS ne reçoit pas votre contrat RMLA signé dans les 60 jours, l’authentification de votre application sera bloquée auprès du système d’authentification Azure.

 

 

 


<!--HONumber=Apr16_HO3-->


