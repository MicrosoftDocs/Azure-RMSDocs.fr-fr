---
title: "Didacticiel de démarrage rapide, étape 1 - AIP"
description: "Étape 1 d’un didacticiel de présentation expliquant comment tester rapidement Azure Information Protection : Activer le service de protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 952431771e89e934be4a725ece4f3d9cd47165fe
ms.sourcegitcommit: 67750454f8fa86d12772a0075a1d01a69f167bcb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/23/2018
---
# <a name="step-1-activate-protection"></a>Étape 1 : Activer la protection
 
>*S’applique à : Azure Information Protection*

> [!NOTE]
>Même si le service Azure Rights Management est activé pour votre locataire, effectuez cette étape pour confirmer l’état d’activation. Les instructions incluent la connexion au portail Azure et la création du panneau Azure Information Protection, en préparation de l’étape 2.

Quand le service Azure Rights Management est activé, vous pouvez protéger les documents et e-mails les plus sensibles de votre entreprise. Vous pouvez également suivre l’utilisation de ces documents protégés quand vous les partagez avec d’autres utilisateurs. 

Il existe différentes manières d’activer la protection. Vous pouvez utiliser PowerShell et les portails d’administration. Mais pour ce didacticiel, nous utilisons le portail Azure, où vous configurez également les étiquettes pour les utilisateurs. 

## <a name="to-activate-the-azure-rights-management-service"></a>Pour activer le service Azure Rights Management

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec le compte Administrateur général de votre locataire. 
    
    Si vous n’êtes pas l’administrateur général, vous pouvez utiliser l’un des [rôles d’administration](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants : **Administrateur Information Protection** ou **Administrateur de sécurité**.

2. Dans le menu Hub, cliquez sur **Créer une ressource**, puis, dans la liste **PLACE DE MARCHÉ**, sélectionnez **Sécurité + Identité**. 
    
3.  Dans le panneau **Sécurité + Identité**, dans la liste **APPLICATIONS PROPOSÉES**, sélectionnez **Azure Information Protection**. Ensuite, dans le panneau **Azure Information Protection**, cliquez sur **Créer**.
    
    Cette action crée le panneau **Azure Information Protection**. De cette façon, vous pouvez sélectionner le service dans la liste **Tous les services** du hub lors de votre prochaine connexion au portail. 
    
    > [!TIP] 
    > Sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.

4. Notez les informations sur la page **Démarrage rapide** qui s’ouvre automatiquement la première fois que vous vous connectez au service. Vous pouvez y revenir plus tard. Pour ce didacticiel, sélectionnez **Activation de la protection**. 

5. Vous pouvez maintenant vérifier si le service Azure Rights Management est activé pour votre locataire. 
    
    - Si le service est activé, la confirmation suivante s’affiche :
        
        ![État d’Azure Information Protection pour Azure RMS](../media/info-protect-azurerms-activated.png)
        
    - Les informations d’état vous indiquent quand le service n’est pas activé et l’option d’activation est disponible :
        
        ![État d’Azure Information Protection pour Azure RMS](../media/info-protect-azurerms-deactivated.png)

6. Si le service n’est pas activé, sélectionnez **Activer**. 

    Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

C’est tout ce que vous avez à faire pour cette première étape du didacticiel. Vous êtes maintenant prêt à passer à l’étape 2.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’activation de Rights Management|[Activation d’Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introduction](infoprotect-quick-start-tutorial.md)
[Étape 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
