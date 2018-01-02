---
title: "Configurer les paramètres de la stratégie Azure Information Protection"
description: "Configurez les paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: 49eb10a999f541cb9979576faac55ca28ff35a0b
ms.sourcegitcommit: e089661f23f199b122b0ca9ba4748792b349bc27
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/13/2017
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Guide pratique pour configurer les paramètres de stratégie pour Azure Information Protection

>*S’applique à : Azure Information Protection*

En plus du titre de la barre et de l’info-bulle Information Protection, il existe certains paramètres dans la stratégie Azure Information Protection que vous pouvez configurer indépendamment des étiquettes :

![Paramètres globaux de la stratégie Azure Information Protection](../media/info-protect-policy-default-settingsv3.png)

Notez que les paramètres de stratégie peuvent avoir des valeurs par défaut différentes, selon la date à laquelle vous avez acheté votre abonnement pour Azure Information Protection. Certains paramètres peuvent également être définis par un [paramètre client personnalisé](../rms-client/client-admin-guide-customizations.md).

Pour configurer ces paramètres :

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si les paramètres à configurer s’appliquent à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**.
    
    Si les paramètres à configurer se trouvent dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Dans le panneau **Azure Information Protection - Stratégie globale** ou le panneau **Stratégie :\<nom>**, configurez les paramètres :
    
    - **Sélectionner l’étiquette par défaut** : lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes. 
    
    - **Tous les documents et e-mails doivent avoir une étiquette** : lorsque vous paramétrez cette option sur **Activé**, tous les documents et e-mails envoyés enregistrés doivent avoir une étiquette appliquée. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**.
        
        Si aucune étiquette n’est affectée quand les utilisateurs enregistrent un document ou envoient un e-mail, ils sont invités à sélectionner une étiquette. Exemple :
        
        ![Invite d’Azure Information Protection si un étiquetage est appliqué](../media/info-protect-enforce-labelv2.png)
        
    - **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection** : si cette option est définie sur **Activée** et qu’un utilisateur effectue une de ces actions (par exemple, s’il change le niveau de l’étiquette **Public** en **Personnel**), il est invité à justifier cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans le journal des événements Windows local de l’utilisateur : **Journaux des applications et des services** > **Azure Information Protection**.  
        
        ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](../media/info-protect-lower-justification.png)
        
        Cette option n’est pas applicable pour les sous-étiquettes.
        
    - **Pour les e-mails avec des pièces jointes, appliquez une étiquette qui correspond à la classification la plus élevée de ces pièces jointes** : quand vous définissez cette option sur **Recommandé**, les utilisateurs sont invités à appliquer une étiquette à leur e-mail. L’étiquette est choisie dynamiquement en fonction des étiquettes de classification qui sont appliquées aux pièces jointes, et l’étiquette de classification la plus élevée est sélectionnée. La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur SharePoint ou OneDrive Entreprise). Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Quand vous définissez cette option sur **Activé**, l’étiquette est appliquée automatiquement, mais les utilisateurs peuvent la supprimer ou sélectionner une autre étiquette avant d’envoyer l’e-mail.  
    
    - **Afficher la barre Information Protection dans les applications Office** : lorsque ce paramètre est désactivé, les utilisateurs ne peuvent pas sélectionner d’étiquettes depuis une barre dans Word, Excel, PowerPoint et Outlook. En revanche, les utilisateurs peuvent sélectionner des étiquettes au moyen du bouton **Protéger** dans le ruban. Lorsque ce paramètre est activé, les utilisateurs peuvent sélectionner des étiquettes par le biais de la barre et du bouton.
        
        > [!IMPORTANT]
        > Ce paramètre est en préversion et nécessite la préversion actuelle du client Azure Information Protection.
        
        Lorsque ce paramètre est activé, il peut être utilisé conjointement avec un paramètre client avancé, afin que les utilisateurs puissent [masquer définitivement la barre Azure Information Protection](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar) s’ils choisissent de ne pas l’afficher. Ils peuvent le faire en désactivant l’option **Afficher la barre** à partir du bouton **Protéger**.
    
    - **Ajouter le bouton Ne pas transférer au ruban Outlook**: lorsque ce paramètre est activé, les utilisateurs peuvent sélectionner ce bouton à partir du groupe **Protection** dans le ruban Outlook en plus de sélectionner l’option **Ne pas transférer** à partir des menus Outlook. Pour vous assurer que les utilisateurs classent et protègent leurs e-mails, vous pouvez choisir de ne pas ajouter ce bouton mais de préférer [configurer une étiquette pour la protection](configure-policy-protection.md) ainsi qu’une autorisation définie par l’utilisateur pour Outlook. Du point de vue fonctionnel, ce paramètre de protection revient à sélectionner le bouton **Ne pas transférer**, mais lorsque cette fonctionnalité est incluse dans une étiquette, les e-mails sont classés en même temps qu’ils sont protégés.
    
        Ce paramètre de stratégie peut également être configuré avec un paramètre client avancé en tant que [personnalisation du client](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook).
    
    - **Activer les options d’autorisations personnalisées pour les utilisateurs** : lorsque ce paramètre est activé, les utilisateurs peuvent définir leurs propres paramètres de protection et remplacer les paramètres de protection que vous avez peut-être inclus avec une configuration d’étiquette. Lorsque ce paramètre est désactivé, les options des autorisations personnalisées ne sont pas sélectionnables par les utilisateurs.
        
        > [!IMPORTANT]
        > À moins de disposer de la préversion actuelle du client, n’utilisez pas ce paramètre **Désactivé** si vous avez des étiquettes configurées pour des autorisations définies par l’utilisateur pour Word, Excel, PowerPoint et l’Explorateur de fichiers. Si vous le faites, quand l’étiquette est appliquée, les utilisateurs ne sont pas invités à configurer les autorisations personnalisées. Par conséquent, le document est étiqueté, mais n’est pas protégé comme prévu.
        
        Notez que ce paramètre de stratégie n’a aucun effet sur les autorisations personnalisées que les utilisateurs peuvent configurer à l’aide des options de menu Office. Ce paramètre de stratégie peut également être configuré avec un paramètre client avancé en tant que [personnalisation du client](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users).
        
        Les options des autorisations personnalisées se trouvent aux emplacements suivants :
        
        - Dans les applications Office : à partir du ruban, onglet **Accueil** > groupe **Protection** > **Protéger** > **Autorisations personnalisées**
        
        - Dans l’Explorateur de fichiers : cliquez avec le bouton droit sur > **Classifier et protéger** > **Autorisations personnalisées**
    
    - **Fournir une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection** : les utilisateurs voient ce lien à la section **Aide et commentaires** dans la boîte de dialogue **Microsoft Azure Information Protection** quand ils sélectionnent **Protéger** > **Aide et commentaires** sous l’onglet **Accueil** de leurs applications Office. Par défaut, ce lien pointe vers le site web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Si vous souhaitez faire pointer ce lien vers une autre page web, vous pouvez entrer une URL HTTP ou HTTPS (recommandé). Aucun contrôle n’est effectué pour vérifier si l’URL personnalisée entrée est accessible ou si elle s’affiche correctement sur tous les appareils.
        
        Par exemple, pour votre support technique, vous pouvez entrer la page de documentation de Microsoft contenant des informations sur l’installation et l’utilisation du client (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) ou sur les versions (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). Vous pouvez également publier votre propre page web comprenant des informations sur la façon de contacter votre support technique ou une vidéo qui explique pas à pas comment utiliser les étiquettes configurées.

3. Pour enregistrer vos modifications, cliquez sur **Enregistrer**.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** initial sur **Publier**.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
