---
title: "Didacticiel de démarrage rapide, étape 1 - AIP"
description: "Didacticiel de présentation expliquant comment tester rapidement Azure Information Protection, étape 1 : activation du service Azure Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 1779eb6f2bcf31ce3515b58b6ed955208fafb237
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2017
---
# <a name="step-1-activate-the-rights-management-service"></a>Étape 1 : activation du service Rights Management
 
>*S’applique à : Azure Information Protection*

> [!NOTE]
>Si vous savez que le service Azure Rights Management pour votre locataire est déjà actif, vous pouvez passer directement à [l’étape suivante](infoprotect-tutorial-step2.md). 
>
>Si vous ne savez pas si ce service est activé ou non, utilisez les instructions de cette étape pour le déterminer.

Quand le service Azure Rights Management est activé, vous pouvez protéger les documents et e-mails les plus sensibles de votre entreprise et suivre l’utilisation des documents protégés quand vous les partagez avec d’autres utilisateurs. Vous pouvez activer ce service de différentes façons, notamment en utilisant Windows PowerShell et par le biais des portails d’administration.

Pour ce didacticiel, nous allons passer directement à la page d’activation dans le portail d’administration pour les administrateurs Office 365. Cependant, si vous préférez accéder à cette page à partir de votre portail d’administration d’Office 365 plutôt que directement, consultez les instructions complètes dans [Activation d’Azure Rights Management](../deploy-use/activate-service.md). En outre, utilisez ces instructions complètes si vous avez accès au portail Azure, mais pas au portail d’administration d’Office 365.

## <a name="to-activate-the-rights-management-service"></a>Pour activer le service Rights Management

1. Ouvrez une nouvelle fenêtre de navigateur et accédez directement à la [page d’activation de Rights Management](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx) pour les administrateurs Office 365.
    
    Si vous êtes invité à vous connecter, utilisez un compte qui est administrateur général pour Office 365.

2. Dans la page **Rights Management**, cliquez sur **Activer**. Si ce bouton affiche **Désactiver**, c’est que le service est déjà activé et vous pouvez passer directement à [l’étape suivante](infoprotect-tutorial-step2.md). 

    ![Didacticiel de démarrage rapide Azure Information Protection - Étape 1 : Activer le service](../media/info-protect-activate.png)

3. À l’invite **Voulez-vous activer Rights Management ?**, cliquez sur **Activer** pour confirmer.

    Vous devriez maintenant voir **Rights management est activé** , ainsi que l’option de désactivation (vous devrez peut-être actualiser la page manuellement).

    À ce stade, ne cliquez pas sur **fonctionnalités avancées**. À la place, vous pouvez fermer cette page.

C’est tout ce que vous avez à faire pour cette première étape du didacticiel. Vous êtes maintenant prêt à passer à l’étape 2.

|Pour en savoir plus|Informations supplémentaires|
|--------------------------------|--------------------------|
|À propos de l’activation de Rights Management|[Activation d’Azure Rights Management](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; Introduction](infoprotect-quick-start-tutorial.md)
[Étape 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
