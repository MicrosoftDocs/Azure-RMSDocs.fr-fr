---
title: Déploiement de votre application - AIP
description: En savoir plus sur le processus de déploiement de votre application Azure Information Protection (AIP)/Rights Management Services (RMS).
keywords: déployer, RMS, AIP
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: c600f6e332ec230d73c90faafe8fb602e1d3dd88
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568331"
---
# <a name="deploy-into-production"></a>Déployer en production

Cette rubrique vous guide au travers du processus de déploiement de votre application avec Azure Information Protection (AIP) / Rights Management Services (RMS).

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Demande d'un IPIA (Information Protection Integration Agreement)
Avant de pouvoir publier une application développée avec AIP/RMS, vous devez demander et conclure un accord formel avec Microsoft.

### <a name="begin-the-process"></a>Commencer le processus
Obtenez votre IPIA en envoyant un e-mail à <strong>IPIA@microsoft.com</strong> avec les informations suivantes :

**Objet :** Demande d’IPIA pour *Nom de la société*

Dans le corps du message électronique, incluez :
- Nom de l’application et du produit
- Nom et prénom du demandeur
- Adresse de messagerie du demandeur

### <a name="next-steps"></a>Étapes suivantes
Après réception de votre demande d'IPIA, nous vous enverrons un formulaire (sous forme de document Word).
Passez en revue les termes et conditions de l'IPIA et renvoyez le formulaire à l'adresse <strong>IPIA@microsoft.com</strong> avec les informations suivantes :
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

### <a name="completing-the-agreement"></a>Établissement de l’accord
Après réception de votre formulaire, nous vous enverrons le lien IPIA final à signer numériquement. Après votre signature, il sera signé par le représentant de Microsoft approprié, ce qui finalisera l’accord.

### <a name="already-have-a-signed-ipia"></a>Vous disposez déjà d'un IPIA signé ?
Si vous disposez déjà d'un IPIA signé et souhaitez ajouter un nouvel *ID de l’application* pour une application que vous lancez, envoyez un e-mail à l'adresse <strong>IPIA@microsoft.com</strong> et fournissez-nous les informations suivantes :
- Nom de l'application d'entreprise
- Brève description de l'application
- ID de locataire Azure (même si c’est le même que précédemment)
- ID de l’application pour l’application
- Contacts de la société, e-mail et téléphone pour la correspondance en cas de situation critique

Après l’envoi de l’e-mail, attendez jusqu’à 72 heures pour recevoir un accusé de réception.

## <a name="deploying-to-the-client-environment"></a>Déploiement dans l’environnement client

Pour déployer votre application créée avec des outils Azure Information Protection (AIP) / Rights Management Services (RMS), vous devez déployer le client RMS 2.1 sur l’ordinateur de l’utilisateur final.

### <a name="rmsclient21"></a>Client RMS 2.1
Le client RMS 2.1 est conçu pour protéger l’accès et l’utilisation des informations qui transitent par des applications fonctionnant avec AIP/RMS, qu’elles soient installées dans vos locaux ou dans un centre de données Microsoft.

Le client RMS 2.1 n’est pas un composant du système d’exploitation Windows. Le client est fourni comme un téléchargement facultatif pouvant être distribué gratuitement avec votre application, après l’accusé de réception et l’acceptation de son contrat de licence.

> [!IMPORTANT]
> Le client RMS Client 2.1 est spécifique à l’architecture et doit correspondre à celle de votre système d’exploitation cible.


## <a name="rmsclient21-installation-options"></a>Options d’installation du client RMS 2.1

### <a name="creating-your-deployment-package"></a>Création de votre package de déploiement

Nous vous recommandons de regrouper le package d’installation du client RMS avec votre application ou solution, en utilisant la technologie d’installation que vous préférez. Le client RMS peut être librement redistribué avec d’autres applications et solutions.

Vous pouvez choisir d’installer le client RMS 2.1 de façon interactive en démarrant le programme d’installation du client RMS 2.1 ou bien de l’installer en mode silencieux. Les étapes d’intégration seront :

-   Télécharger le programme d’installation du client RMS 2.1
-   Intégrer l’exécution du programme d’installation du client RMS 2.1 au programme d’installation de votre application

Le package [Rights Protected Folder Explorer](/previous-versions/orphan-topics/ws.10/hh538204(v=ws.10)) est un exemple d’intégration du client RMS 2.1 à votre application. Essayez de l’installer vous-même pour comprendre l’approche.

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>Faire du client RMS 2.1 un prérequis pour l’installation de votre application

Dans ce cas, vous allez créer un prérequis entraînant l’échec de l’installation de votre application si le client RMS 2.1 n’est pas présent sur la machine de l’utilisateur final.

Si le client n’est pas présent, fournissez un message d’erreur indiquant à l’utilisateur où il peut télécharger une copie du client RMS 2.1

Si le client est présent, poursuivez l’installation de votre application.

## <a name="enabling-azure-information-protection-services-with-your-application"></a>Activation des services de Azure Information Protection Services avec votre application

> [!NOTE]
> Si vous avez migré vers le nouveau modèle ADAL pour l’authentification, vous n’êtes pas obligé d’installer **SIA**. Pour plus d’informations, consultez [Authentification ADAL pour votre application sous RMS](adal-auth.md).
> En outre, vous pouvez **certifier votre application pour Windows 10**. En mettant à jour votre application pour utiliser l’authentification ADAL plutôt que l’assistant de connexion Microsoft Online, vous et vos clients pourrez : Utiliser l’authentification multifacteur Installer le client RMS 2.1 sans avoir besoin des privilèges Administrateur sur la machine

Pour que votre utilisateur final puisse tirer parti des services Information Protection, vous devez déployer *l’Assistant de connexion Online Services (SIA)*. En tant que développeur d’applications, vous ne savez pas si l’utilisateur final utilisera Information Protection avec RMS (sur site) ou avec Azure Information Protection.


> [!IMPORTANT]
> Si vous comptez exécuter votre application cliente avec RMS basé sur Azure, vous devez créer vos propres locataires. Pour plus d’informations, consultez [Conditions requises pour Azure RMS : abonnements cloud qui prennent en charge Azure RMS](../requirements.md).
> Pour plus d’informations sur l’exécution avec Azure RMS, consultez [Configurer votre application de service pour fonctionner avec RMS basé sur le cloud](how-to-use-file-api-with-aadrm-cloud.md).

-   Téléchargez [l’assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177) à partir du centre de téléchargement Microsoft.
-   Vérifiez que votre déploiement d’une application comprenant la gestion des droits inclut une vérification des composants requis pour la sélection de ce service.
-   Pour vos propres tests et l’utilisation par vos utilisateurs finaux du service en ligne, consultez la rubrique TechNet, [Configuration de Rights Management](../deployment-roadmap.md).

Vous devrez également utiliser ce guide pour configurer votre application - [Comment configurer votre application App Service pour utiliser la connexion de Azure Active Directory](/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication).

Pour plus d’informations sur la configuration de votre application afin d’utiliser RMS pour les services Azure Rights Management, consultez [Configurer votre application pour fonctionner avec RMS basé sur le cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="related-topics"></a>Rubriques connexes

* [Assistant de connexion Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=28177)
* [Configuration de Rights Management](../deployment-roadmap.md)
* [Configurer votre application pour fonctionner avec RMS basé sur le cloud](how-to-use-file-api-with-aadrm-cloud.md)