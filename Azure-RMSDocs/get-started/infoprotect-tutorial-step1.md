---
title: Didacticiel de démarrage rapide, étape 1 - AIP
description: 'Étape 1 d’un didacticiel de présentation expliquant comment tester rapidement Azure Information Protection : Activer le service de protection.'
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/28/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: f5daff0083e653a9a4a4b2bdeb96daa85075428b
ms.sourcegitcommit: 1bc4c9d6e773809893d02a6abb09aeb4ae28cb03
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2018
ms.locfileid: "34562056"
---
# <a name="step-1-activate-protection"></a>Étape 1 : Activer la protection
 
>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
>Même si la protection est activée pour votre locataire, effectuez cette étape pour confirmer l’état d’activation. Les instructions incluent la connexion au portail Azure et la création du panneau Azure Information Protection, en préparation de l’étape 2.

Quand la protection est activée pour Azure Information Protection, vous pouvez protéger les documents et e-mails les plus sensibles de votre organisation. Vous pouvez également suivre l’utilisation de ces documents protégés quand vous les partagez avec d’autres utilisateurs. 

Il existe différentes manières d’activer la protection. Vous pouvez utiliser PowerShell et les portails d’administration. Mais pour ce didacticiel, nous utilisons le portail Azure, où vous configurez également les étiquettes pour les utilisateurs. 

## <a name="to-activate-protection"></a>Pour activer la protection

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec le compte Administrateur général de votre locataire. 
    
    Si vous n’êtes pas l’administrateur général, vous pouvez utiliser l’un des [rôles d’administration](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) suivants : **Administrateur Information Protection** ou **Administrateur de sécurité**.

2. Dans le menu hub, sélectionnez **Créer une ressource**, puis, à partir de la zone de recherche pour la Place de marché, tapez **Azure Information Protection**. 
    
3. Dans la liste des résultats, sélectionnez **Azure Information Protection**. Dans le panneau **Azure Information Protection**, cliquez sur **Créer**.
    
    > [!TIP] 
    > Ou sélectionnez **Épingler au tableau de bord** pour créer une vignette **Azure Information Protection** sur votre tableau de bord. Vous n’avez ainsi pas besoin d’accéder au service lors de votre prochaine connexion au portail.
    
    Cliquez sur **Créer** à nouveau.

4. Notez les informations sur la page **Démarrage rapide** qui s’ouvre automatiquement la première fois que vous vous connectez au service. Vous pouvez y revenir plus tard. Pour ce tutoriel, sélectionnez **GÉRER** > **Activation de la protection**. 

5. Vous voyez maintenant si la protection est activée pour votre locataire. 
    
    - Si la protection est activée, la confirmation suivante s’affiche :
        
        ![État d’Azure Information Protection pour Azure RMS](../media/info-protect-azurerms-activated.png)
        
    - Si la protection n’est pas activée, les informations d’état vous l’indiquent, et l’option d’activation est affichée :
        
        ![État d’Azure Information Protection pour Azure RMS](../media/info-protect-azurerms-deactivated.png)

6. Si la protection n’est pas activée, sélectionnez **Activer**. 

    Quand l’activation est terminée, la barre d’informations affiche **Activation terminée**.

C’est tout ce que vous avez à faire pour cette première étape du didacticiel. Vous êtes maintenant prêt à passer à l’étape 2.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’activation de la protection|[Activation d’Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introduction](infoprotect-quick-start-tutorial.md)
[Étape 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
