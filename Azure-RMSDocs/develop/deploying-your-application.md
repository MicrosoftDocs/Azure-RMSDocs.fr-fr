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
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Déployer en préproduction


Cette rubrique décrit les options de déploiement pour votre application avec gestion des droits.

## Demander un contrat de licence de production

 Avant de pouvoir publier une application développée avec Rights Management Services SDK 2.1, vous devez demander un contrat de licence de production pour obtenir un certificat de production.

> [!IMPORTANT]
> Si vous devez exécuter votre application cliente avec Azure RMS, vous devez créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](../get-started/requirements-subscriptions.md).
> Pour plus d’informations sur l’exécution d’Azure RMS, consultez [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

Vous pouvez obtenir le certificat en demandant un contrat de licence de production.

Envoyez un e-mail à [RMLA@microsoft.com](mailto:rmla@microsoft.com) en spécifiant les informations suivantes :

- Nom complet de l’entreprise
- Adresse physique de l’entreprise (inclure la ville, le département, le pays ou la région et le code postal)
- Adresse de correspondance de l’entreprise (inclure la ville, le département, le pays ou la région et le code postal)
- Numéros de téléphone et de télécopie de l’entreprise
- URL de l’entreprise
- Pays ou région où l’entreprise a été créée
- Nom de l’application ou du produit
- Nom et prénom du demandeur
- Titre du demandeur
- Adresse de messagerie du demandeur

Un compte de messagerie n’est pas strictement obligatoire, mais le processus d’application s’appuie généralement sur la messagerie pour la communication. Vous pouvez obtenir un compte de messagerie gratuitement sur Microsoft Outlook.com. Si vous n’avez pas de compte et que vous ne souhaitez pas en créer, vous pouvez envoyer une application à l’adresse suivante :

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

Lors de la demande de contrat, procédez comme suit :
- Envoyez les informations (en anglais) telles qu’elles doivent apparaître sur le contrat.
- Envoyez toutes les informations demandées. Toute information manquante ou incomplète peut retarder le traitement de votre demande.

L’équipe ADRMLA (Active Directory Rights Management Licensing Agreement) répondra à votre demande dans les trois jours ouvrables suivant la réception de votre e-mail (ou plus si vous avez envoyé la demande par voie postale). La réponse contiendra le formulaire de contrat de licence et d’autres instructions. Lisez, signez et renvoyez toutes les pages du contrat à l’équipe ADRMLA. Veuillez ne pas modifier les polices ou la mise forme des paragraphes du contrat de licence.

Suivez bien les instructions envoyées par l’équipe ADRMLA. Ces instructions mentionnent les informations numériques nécessaires pour répondre à votre demande de certificat. En suivant les instructions pas à pas, vous réduirez tout risque de retard.

L’équipe ADRMLA vous transmettra votre certificat de production dès qu’il aura été créé. Notez que le délai d’envoi du certificat par e-mail par l’équipe ADRMLA peut aller jusqu’à 15 jours, voire plus en cas de communication par voie postale.


## Options d’installation et configuration requise pour le client RMS (Rights Management Services) 2.1

Étant donné que vous avez utilisé RMS SDK 2.1, Active Directory Rights Management Services Client 2.1 doit être déployé sur l’ordinateur de l’utilisateur final.

### Client RMS 2.1

Le client RMS 2.1 est un logiciel conçu pour vos ordinateurs clients, qui permet de protéger l’accès aux informations qui circulent dans les applications utilisant RMS, qu’elles soient installées en local ou dans un centre de données Microsoft, ainsi que l’utilisation de ces informations.

Le client RMS 2.1 n’est pas un composant du système d’exploitation Windows. Il est disponible sous la forme d’un téléchargement facultatif qui, à condition d’en accuser réception et d’accepter son contrat de licence, peut être distribué gratuitement avec votre logiciel tiers, pour permettre l’accès du client à du contenu dont les droits ont été protégés en utilisant et en déployant des serveurs RMS dans votre environnement.


> [!IMPORTANT] AD RMS Client 2.1 est propre à l’architecture et doit correspondre à celle de votre système d’exploitation cible.


## Choix d’installation du client RMS 2.1

-   **Redistribution du client RMS 2.1**

    L’approche recommandée consiste à regrouper le package d’installation du client RMS avec votre application ou solution à l’aide de la technologie d’installation que vous préférez. Le client RMS peut être librement redistribué et regroupé avec d’autres applications et solutions informatiques.

    Vous pouvez choisir d’installer le client RMS 2.1 sans assistance ou de façon interactive en démarrant son programme d’installation. Les étapes d’intégration sont les suivantes :

    -   Télécharger le programme d’installation d’AD RMS Client 2.1
    -   Intégrer l’exécution du programme d’installation du client RMS 2.1 au programme d’installation de votre application

    Deux bons exemples d’intégration du client RMS 2.1 à votre application sont le package d’installation de RMS SDK 2.1 et le package Right Protected Folder Explorer. Essayez de les installer vous-même pour comprendre l’approche.

-   **Faire du client RMS 2.1 un composant requis pour l’installation de votre application**

    Ici, vous allez créer un composant requis de manière à ce que l’installation de votre application échoue si le client RMS 2.1 n’est pas présent sur l’ordinateur de l’utilisateur final.

    Si le client n’est pas présent, fournissez un message d’erreur indiquant à l’utilisateur où il peut télécharger une copie du client RMS 2.1.

    Si le client est présent, poursuivez l’installation de votre application.

## Activation d’Azure Rights Management Services avec votre application

> [!NOTE]
> Si vous avez migré vers le nouveau modèle ADAL pour l’authentification, il est inutile d’installer l’Assistant de connexion. Pour plus d’informations, consultez [Authentification ADAL pour votre application compatible RMS](adal-auth.md).
> Vous pouvez également **certifier votre application pour Windows 10**. En mettant à jour votre application pour utiliser l’authentification ADAL plutôt que l’Assistant de connexion Microsoft Online, vous et vos clients pouvez : utiliser l’authentification multifacteur, installer le client RMS 2.1 sans avoir besoin de privilèges d’administration sur l’ordinateur.


Pour que votre utilisateur final tire parti des services Azure Rights Management, vous devez déployer l’*Assistant de connexion Online Services*. En tant que développeur de l’application, vous ne savez pas si l’utilisateur final utilisera RMS (en local) ou les services Azure Rights Management (service cloud).


> [!IMPORTANT]
> L’exécution de votre application cliente de RMS SDK 2.1 avec Azure RMS vous oblige à créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](../get-started/requirements-subscriptions.md).

-   Téléchargez l’[Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) à partir du Centre de téléchargement Microsoft.
-   Vérifiez que votre déploiement d’une application avec gestion des droits inclut une vérification des composants requis pour la sélection de ce service.
-   Pour l’utilisation du service en ligne dans le cadre de vos propres tests et par les utilisateurs finaux, consultez la rubrique TechNet [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Pour plus d’informations sur l’activation de votre application pour utiliser RMS pour les services Azure Rights Management, consultez [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Rubriques connexes

* [Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)
 

 


<!--HONumber=Jun16_HO2-->


