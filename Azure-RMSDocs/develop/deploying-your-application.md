---
title: "Déploiement de votre application"
description: "Cette rubrique vous guide dans le déploiement de votre application"
keywords: "déployer, RMS, AIP"
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 0c16b7c6bd494a0350a511a3b415f781aecf613d


---
# <a name="deploy-into-production"></a>Déployer en production

Cette rubrique vous guide à travers le processus de déploiement de votre application Azure Information Protection (AIP) / Rights Management Services (RMS) activée.

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Demande d'un IPIA (Information Protection Integration Agreement)
Avant de pouvoir lancer une application développée avec AIP/RMS, vous devez passer un accord formel avec Microsoft.

### <a name="begin-the-process"></a>Lancement du processus
Obtenez votre IPIA en envoyant un e-mail à **IPIA@microsoft.com** avec les informations suivantes :

**Objet :** demande d'IPIA pour *Nom de la société*

Dans le corps du message électronique, incluez :
- Nom de l’application et du produit
- Nom et prénom du demandeur
- Adresse de messagerie du demandeur

### <a name="next-steps"></a>Étapes suivantes
Après réception de votre demande d'IPIA, nous vous enverrons un formulaire (sous forme de document Word).
Passez en revue les termes et conditions de l'IPIA et renvoyez le formulaire à l'adresse **IPIA@microsoft.com** avec les informations suivantes :
- Raison sociale de la société
- État/Province (États-Unis / Canada) ou pays d'immatriculation
- URL de l’entreprise
- Adresse e-mail du contact
- Adresses supplémentaires de la société (facultatif)
- Nom de l'application d'entreprise
- Brève description de l'application
- *ID de locataire Azure*
- *ID de l’application* pour l’application
- Contacts de la société, e-mail et téléphone pour la correspondance en cas de situation critique

### <a name="completing-the-agreement"></a>Finalisation de l'accord
Après réception de votre formulaire, nous vous enverrons le lien IPIA final à signer numériquement. Après votre signature, il sera signé par le représentant de Microsoft approprié, ce qui finalisera l’accord.

### <a name="already-have-a-signed-ipia"></a>Vous disposez déjà d'un IPIA signé ?
Si vous disposez déjà d'un IPIA signé et souhaitez ajouter un nouvel *ID de l’application* pour une application que vous lancez, envoyez un e-mail à l'adresse **IPIA@microsoft.com** et fournissez-nous les informations suivantes :
- Nom de l'application d'entreprise
- Brève description de l'application
- ID de client Azure (même s'il est identique au précédent)
- ID de l’application pour l’application
- Contacts de la société, e-mail et téléphone pour la correspondance en cas de situation critique

Patientez jusqu'à 72 heures après l'envoi de l'e-mail pour recevoir un accusé de réception.

## <a name="deploying-to-the-client-environment"></a>Déploiement dans l’environnement client

Pour déployer votre application créée avec des outils Azure Information Protection (AIP) / Rights Management Services (RMS), vous devez déployer le client RMS 2.1 sur l’ordinateur de l’utilisateur final.

### <a name="rms-client-21"></a>Client RMS 2.1
Le client RMS 2.1 est conçu pour protéger l’accès aux informations qui circulent à travers des applications compatibles AIP/RMS, qu’elles soient installées en local ou dans un centre de données Microsoft, ainsi que leur utilisation.

Le client RMS 2.1 n’est pas un composant du système d’exploitation Windows. Le client envoie un téléchargement facultatif qui peut être distribué gratuitement avec votre application, avec accusé de réception et acceptation du contrat de licence.

> [!IMPORTANT]
> Le client RMS Client 2.1 est spécifique à l’architecture et doit correspondre à celle de votre système d’exploitation cible.


## <a name="rms-client-21-installation-options"></a>Options d’installation du client RMS 2.1

### <a name="creating-your-deployment-package"></a>Création de votre package de déploiement

Nous recommandons de regrouper le package d’installation du client RMS avec votre application ou solution à l’aide de la technologie d’installation que vous préférez. Le client RMS peut être librement redistribué avec d'autres applications et solutions.

Vous pouvez choisir d’installer le client RMS 2.1 sans assistance ou de façon interactive en démarrant son programme d’installation. Les étapes d’intégration sont les suivantes :

-   Télécharger le programme d’installation d’AD RMS Client 2.1
-   Intégrer l’exécution du programme d’installation du client RMS 2.1 au programme d’installation de votre application

Un exemple d’intégration du client RMS 2.1 à votre application est le package [Rights Protected Folder Explorer](https://technet.microsoft.com/en-us/library/rights-protected-folder-explorer(v=ws.10).aspx). Essayez de l'installer vous-même pour comprendre l’approche.

### <a name="make-rms-client-21-a-pre-requisite-for-your-application-install"></a>Faire du client RMS 2.1 un composant requis pour l’installation de votre application

Ici, vous allez créer un composant requis de manière à ce que l’installation de votre application échoue si le client RMS 2.1 n’est pas présent sur l’ordinateur de l’utilisateur final.

Si le client n’est pas présent, fournissez un message d’erreur indiquant à l’utilisateur où il peut télécharger une copie du client RMS 2.1.

Si le client est présent, poursuivez l’installation de votre application.

## <a name="enabling-azure-information-protection--rights-management-services-with-your-application"></a>Activation des services Azure Information Protection / Rights Management dans votre application

> [!NOTE]
> Si vous avez migré vers le nouveau modèle ADAL pour l’authentification, il est inutile d’installer le **SIA**. Pour plus d’informations, consultez [Authentification ADAL pour votre application compatible RMS](adal-auth.md).
> Vous pouvez également **certifier votre application pour Windows 10**. En mettant à jour votre application pour utiliser l’authentification ADAL plutôt que l’Assistant de connexion Microsoft Online, vous et vos clients pouvez : utiliser l’authentification multifacteur, installer le client RMS 2.1 sans avoir besoin de privilèges d’administration sur l’ordinateur.


Pour que votre utilisateur final tire parti des services Information Protection / Rights Management, vous devez déployer *l'Assistant de connexion Online Services (SIA)*. En tant que développeur d’applications, vous ne savez pas si l’utilisateur final doit utiliser Information Protection via RMS (localement) ou Azure Information Protection.


> [!IMPORTANT]
> Si vous devez exécuter votre application cliente avec Azure RMS, vous devez créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](../get-started/requirements-subscriptions.md).
> Pour plus d’informations sur l’exécution d’Azure RMS, consultez [Permettre à votre application de service de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

-   Téléchargez l’[Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177) à partir du Centre de téléchargement Microsoft.
-   Vérifiez que votre déploiement d’une application avec gestion des droits inclut une vérification des composants requis pour la sélection de ce service.
-   Pour l’utilisation du service en ligne dans le cadre de vos propres tests et par les utilisateurs finaux, consultez la rubrique TechNet [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx).

Pour plus d’informations sur l’activation de votre application pour utiliser RMS pour les services Azure Rights Management, consultez [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="related-topics"></a>Rubriques connexes

* [Assistant de connexion Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Configuration de Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [Permettre à votre application de fonctionner avec le service RMS cloud](how-to-use-file-api-with-aadrm-cloud.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO4-->


