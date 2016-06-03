---
# required metadata

title: Présentation des chaînes de certificats | Azure RMS
description: Une application avec gestion des droits nécessite une paire de clés publiques et une chaîne de certificats qui renvoie à un certificat Microsoft à la racine de confiance
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6AEA2162-82BF-4867-9285-111CD3FCD2F6
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Présentation des chaînes de certificats

Le développement d’une application avec gestion des droits nécessite une paire de clés publiques et une chaîne de certificats qui renvoie à un certificat Microsoft à la racine de confiance.

## Types de certificats

Les licences et les certificats utilisés dans un environnement RMS (Rights Management Services) se composent tous d’une chaîne de certificats qui renvoie à un certificat d’autorité de certification Microsoft. Microsoft fournit deux chaînes dans lesquelles une licence ou un certificat peut être imbriqué, une chaîne de certificats de préproduction et une chaîne de production. Quand vous développez une application, nous vous recommandons d’utiliser la hiérarchie de préproduction, celle-ci vous permettant de travailler sans signer un *contrat de licence de production* avec Microsoft. Notez que le serveur RMS doit également être configuré pour la préproduction.

Vous devez basculer vers une chaîne de production avant de publier votre application. Le contenu protégé par un certificat de préproduction est moins sécurisé qu’un contenu protégé par un certificat de production.

Les clés publiques et privées et le certificat de préproduction sont inclus avec le SDK dans les fichiers suivants situés dans le dossier `%MsipcSDKDir%\Bin`.

- **ISVTier5AppSigningPrivKey.dat** contient la clé privée utilisée pour signer un manifeste à utiliser durant le développement d’applications.
- **ISVTier5AppSigningPubKey.dat** contient la clé publique connectée à la hiérarchie de certification de préproduction.
- **ISVTier5AppSignSDK_Client.xml** contient le certificat de préproduction utilisé pour générer un manifeste à utiliser durant le développement d’applications.

 

Le certificat et la clé privée associée servent à créer et à signer un manifeste qui identifie les fichiers qui peuvent ou doivent être chargés dans l’espace de processus de votre application et ceux qui ne doivent pas être chargés. Le manifeste est ensuite chargé par la plateforme.

Que vous ayez ou non utilisé un certificat de préproduction pendant le développement de votre application, vous devez, au moment de la publier, générer une nouvelle paire de clés, acquérir un certificat de production auprès de Microsoft et utiliser la nouvelle clé privée et le nouveau certificat pour créer et signer un manifeste d’application.

Pour plus d’informations sur l’utilisation de chaînes de certificats et la signature d’applications, consultez [Basculement vers l’environnement de production](switching-to-the-production-environment.md).

## Rubriques connexes

* [Concepts de développement](ad-rms-concepts-nav.md)
* [Basculement vers l’environnement de production](switching-to-the-production-environment.md)
 

 


<!--HONumber=May16_HO2-->


