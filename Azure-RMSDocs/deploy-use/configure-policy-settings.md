---
title: "Configurer les paramètres de la stratégie Azure Information Protection"
description: "Configurez les paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/29/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: f78de628ab82f8b41001c0c70c8e4ecc52cf20ca
ms.sourcegitcommit: 7b773ca5bf1abf30e527c34717ecb2dc96f88033
translationtype: HT
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Guide pratique pour configurer les paramètres de stratégie pour Azure Information Protection

>*S’applique à : Azure Information Protection*

En plus du titre de la barre et de l’info-bulle Information Protection, il existe certains paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils :

![Paramètres globaux de la stratégie Azure Information Protection](../media/info-protect-policy-default-settingsv2.png)


Pour configurer ces paramètres :

1. Si ce n’est déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général, puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si ces paramètres à configurer s’appliquent à tous les utilisateurs, configurez les paramètres globaux suivants à partir du panneau **Stratégie : Globale** :
    
    - **Tous les documents et e-mails doivent avoir une étiquette** : lorsque vous paramétrez cette option sur **Activé**, tous les documents et e-mails envoyés enregistrés doivent avoir une étiquette appliquée. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**. 
        
        Si aucune étiquette n’est affectée quand un utilisateur enregistre un document ou envoie un e-mail, il est invité à en sélectionner une. Exemple :
        
        ![Invite d’Azure Information Protection si un étiquetage est appliqué](../media/info-protect-enforce-labelv2.png)
        
    - **Sélectionner l’étiquette par défaut** : lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes. 
        
    - **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection** : si cette option est définie sur **Activée** et qu’un utilisateur effectue une de ces actions (par exemple, s’il change le niveau de l’étiquette **Public** en **Personnel**), il est invité à justifier cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Application** > **Microsoft Azure Information Protection**.  
        
        ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-lower-justification.png)
        
        Cette option n’est pas applicable pour les sous-étiquettes.
        
    - **Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes** : quand vous définissez cette option sur **Recommandé**, les utilisateurs sont invités à appliquer une étiquette à leur e-mail. L’étiquette est choisie dynamiquement en fonction des étiquettes de classification qui sont appliquées aux pièces jointes, et l’étiquette de classification la plus élevée est sélectionnée. La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur SharePoint ou OneDrive Entreprise). Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Quand vous définissez cette option sur **Activé**, l’étiquette est appliquée automatiquement, mais les utilisateurs peuvent la supprimer ou sélectionner une autre étiquette avant d’envoyer l’e-mail.  

    - **Fournir une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection** : les utilisateurs voient ce lien dans la section **Aide et commentaires**de la boîte de dialogue **Microsoft Azure Information Protection** quand ils sélectionnent **Protéger** > **Aide et commentaires** sous l’onglet **Accueil** de leurs applications Office. Par défaut, ce lien pointe vers le site web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Si vous souhaitez faire pointer ce lien vers une autre page web, vous pouvez entrer une URL HTTP ou HTTPS (recommandé). Aucun contrôle n’est effectué pour vérifier si l’URL personnalisée entrée est accessible ou si elle s’affiche correctement sur tous les appareils.
        
        Par exemple, pour votre support technique, vous pouvez entrer la page de documentation de Microsoft contenant des informations sur l’installation et l’utilisation du client (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) ou sur les versions (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). Vous pouvez également publier votre propre page web comprenant des informations sur la façon de contacter votre support technique ou une vidéo qui explique pas à pas comment utiliser les étiquettes configurées.
        
         Ces paramètres peuvent être remplacés pour des utilisateurs spécifiés quand vous créez une [stratégie délimitée](configure-policy-scope.md). Pour configurer ces paramètres dans une stratégie délimitée, commencez par sélectionner cette stratégie dans le panneau **Azure Information Protection** initial.

3. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** initial sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
