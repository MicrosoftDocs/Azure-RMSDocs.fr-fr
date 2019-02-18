---
title: Comment déployer une application - AIP
description: Cet article décrit le processus de déploiement d’une application de service sur un locataire autre que celui avec lequel elle a été développée à l’origine.
keywords: ''
author: kkanakas
ms.author: kartikka
manager: barbkess
ms.date: 02/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 34dc6d6f-cfe4-4848-9b11-8d90c4b38ef7
audience: developer
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: 5be6785c86cfeb104acc7f12d4cb7b830e9c9d36
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251873"
---
# <a name="deploying-a-service-application-into-a-different-tenant"></a>Déploiement d’une application de service sur un autre locataire

Cet article décrit le processus de déploiement d’une application de service. Dans ce scénario, nous transférons l’application inscrite avec son locataire AD de développement initial sur un locataire AD de production appartenant à une société différente.

> [!Note]
> Ce scénario est pertinent uniquement si l’application de service utilise l’authentification par clé symétrique.

## <a name="scenario"></a>Scénario
La société *CoolApp* a développé une application de service utilisant Azure Information Protection (AIP) qui chiffre, étiquette et protège les documents lorsque les utilisateurs les exportent à partir d’une application professionnelle comme Dynamics, SAP ou Salesforce. Dans ce scénario, une grande entreprise *ABC* achète la nouvelle application de *CoolApp* et l’équipe de *CoolApp* a besoin de déployer les solutions dans l’environnement *d’ABC*. 

![Exemple de flux pour la création d’une clé symétrique dans un autre locataire](../media/develop/service-app-provision.jpg)

## <a name="flow-1-coolapp-provides-a-ui-dialog-to-abc-to-implement-the-deployment"></a>Flux 1 : *CoolApp* fournit une boîte de dialogue d’interface utilisateur à *ABC* pour mettre en œuvre le déploiement

À partir du moment où *ABC* achète la solution de *CoolApp*, l’administrateur informatique *d’ABC* doit créer le principal du service *CoolApp* et inscrire l’application dans le locataire Azure AD *d’ABC*. 

Les étapes de cette procédure sont décrites dans la section **Créer un principal du service**, dans [Développement de votre application](developing-your-application.md).

![Exemple d’interface utilisateur que l’administrateur informatique doit fournir pour votre application](../media/develop/how-to-deploy-app-UI.png)

> [!Note]
> Pour créer un principal du service dans un locataire, vous avez besoin de droits d’administration sur ce locataire.

L’administrateur informatique *d’ABC* exécute ensuite l’application de *CoolApp* en tant que service dans l’environnement. Il intègre les informations pour que l’application de *CoolApp* puisse fonctionner : par exemple, l’identifiant de l’application, l’identifiant du locataire et la clé symétrique.

Si l’expérience souhaitée n’est pas de fournir à l’administrateur informatique *d’ABC* une boîte de dialogue d’interface utilisateur pour les informations du principal de service, mieux vaut suivre les indications du **Flux 2**.

## <a name="flow-2-abc-it-administrator-provides-the-key-to-the-coolapp-team"></a>Flux 2 : L’administrateur informatique *d’ABC* fournit la clé à l’équipe de *CoolApp*

Une fois que l’administrateur informatique *d’ABC* crée le principal du service, comme indiqué dans la **Figure 1**, *ABC* transfère les informations à l’équipe de *CoolApp*. L’équipe de *CoolApp* continue ensuite en intégrant les informations dans l’application *CoolApp* pour pouvoir les utiliser dans le locataire *d’ABC*.
