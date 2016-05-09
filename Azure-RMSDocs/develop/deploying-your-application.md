---
# required metadata

title: Déploiement de votre application | Azure RMS
description: Cette rubrique décrit les options de déploiement pour votre application avec gestion des droits.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 08cb33e0-7df5-4855-a05b-159e6532f3ca

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
# Déploiement de votre application


Cette rubrique décrit les options de déploiement pour votre application avec gestion des droits.

> [!IMPORTANT]
> Nous vous recommandons de tester votre application Rights Management Services SDK 2.1 d’abord avec l’environnement de préproduction RMS sur un serveur RMS. Ensuite, si vous souhaitez que votre client puisse utiliser votre application avec le service Azure RMS, passez aux tests avec cet environnement. Pour plus d’informations, consultez [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

 

## Options d’installation pour Active Directory Rights Management Services Client 2.1

Une fois que vous créez votre fichier manifeste à l’aide d’un certificat de production, votre application est prête à être déployée. Étant donné que vous avez utilisé RMS SDK 2.1, Active Directory Rights Management Services Client 2.1 doit être déployé sur l’ordinateur de l’utilisateur final.

### AD RMS Client 2.1

AD RMS Client 2.1 est un logiciel conçu pour vos ordinateurs clients, qui permet de protéger l’accès aux informations qui circulent dans les applications utilisant RMS, qu’elles soient installées en local ou dans un centre de données Microsoft, ainsi que l’utilisation de ces informations.

AD RMS Client 2.1 n’est pas un composant du système d’exploitation Windows. Il est disponible sous la forme d’un téléchargement facultatif qui, à condition d’en accuser réception et d’accepter son contrat de licence, peut être distribué gratuitement avec votre logiciel tiers, pour permettre l’accès du client à du contenu dont les droits ont été protégés en utilisant et en déployant des serveurs RMS dans votre environnement.

> [!IMPORTANT]
> AD RMS Client 2.1 est spécifique à l’architecture et doit correspondre à celle de votre système d’exploitation cible.


## Choix d’installation d’AD RMS Client 2.1

-   **Redistribution d’AD RMS Client 2.1**

    L’approche recommandée consiste à regrouper le package d’installation du client RMS avec votre application ou solution à l’aide de la technologie d’installation que vous préférez. Le client RMS peut être librement redistribué et regroupé avec d’autres applications et solutions informatiques.

    Vous pouvez choisir d’installer AD RMS Client 2.1 de façon interactive en démarrant le programme d’installation d’AD RMS Client 2.1 ou de l’installer en mode silencieux. Les étapes d’intégration sont les suivantes :

    -   Télécharger le programme d’installation d’AD RMS Client 2.1
    -   Intégrer l’exécution du programme d’installation d’AD RMS Client 2.1 au programme d’installation de votre application

    Deux bons exemples d’intégration d’AD RMS Client 2.1 à votre application sont le package d’installation de RMS SDK 2.1 et le package Right Protected Folder Explorer. Essayez de les installer vous-même pour comprendre l’approche.

-   **Faire d’AD RMS Client 2.1 un composant requis pour l’installation de votre application**

    Dans ce cas, vous allez créer un composant requis de manière à ce que l’installation de votre application échoue si AD RMS Client 2.1 n’est pas présent sur l’ordinateur de l’utilisateur final.

    Si le client n’est pas présent, fournissez un message d’erreur indiquant à l’utilisateur où il peut télécharger une copie d’AD RMS Client 2.1.

    Si le client est présent, poursuivez l’installation de votre application.

## Activation d’Azure Rights Management Services avec votre application

> [!NOTE]
> Si vous avez migré vers le nouveau modèle ADAL pour l’authentification, il est inutile d’installer l’Assistant de connexion. Pour plus d’informations, consultez l’authentification ADAL pour votre application compatible RMS.

- **Certifiez votre application pour Windows 10** : en mettant à jour votre application pour utiliser l’authentification ADAL au lieu de l’Assistant de connexion Microsoft Online, vous et vos clients pouvez :
  - utiliser l’authentification multifacteur ;
  - installer le client RMS 2.1 sans nécessiter de privilèges d’administration sur l’ordinateur.
 
  Pour que votre utilisateur final tire parti des services Azure Rights Management, vous devez déployer l’*Assistant de connexion Online Services*. En tant que développeur de l’application, vous ne savez pas si l’utilisateur final utilisera RMS (en local) ou les services Azure Rights Management (service cloud).

> [!IMPORTANT]
> L’exécution de votre application cliente RMS SDK 2.1 avec Azure RMS nécessite que vous demandiez un locataire Azure RMS. Envoyez un e-mail à <rmcstbeta@microsoft.com> avec votre demande de locataire.

-   Téléchargez l’[Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) à partir du Centre de téléchargement Microsoft.
-   Vérifiez que votre déploiement d’une application avec gestion des droits inclut une vérification des composants requis pour la sélection de ce service.
-   Pour l’utilisation du service en ligne dans le cadre de vos propres tests et par les utilisateurs finaux, consultez la rubrique TechNet [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Pour plus d’informations sur l’activation de votre application pour utiliser RMS pour les services Azure Rights Management, consultez [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Rubriques connexes

* [Utilisation de procédures](how-to-use-msipc.md)
* [Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Apr16_HO3-->


