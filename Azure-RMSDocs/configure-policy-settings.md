---
title: Configurer les paramètres de la stratégie Azure Information Protection - AIP
description: Configurez les paramètres dans la stratégie Azure Information Protection qui s’appliquent à tous les utilisateurs et à tous les appareils.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/29/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: b85cf3fc1a1f78732c928b40cb09b4781dc42168
ms.sourcegitcommit: 8fa7d2e6b3e900fec128af57105995d5fb0cc761
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58617820"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Guide pratique pour configurer les paramètres de stratégie pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

En plus du titre de la barre et de l’info-bulle Information Protection, il existe certains paramètres dans la stratégie Azure Information Protection que vous pouvez configurer indépendamment des étiquettes :

![Paramètres globaux de la stratégie Azure Information Protection](./media/info-protect-policy-default-settingsv3.png)

Notez que les paramètres de stratégie peuvent avoir des valeurs par défaut différentes, selon la date à laquelle vous avez acheté votre abonnement pour Azure Information Protection. Certains paramètres peuvent également être définis par un [paramètre client personnalisé](./rms-client/client-admin-guide-customizations.md).

Pour configurer ces paramètres :

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **Classifications** > **Stratégies** : Dans le panneau **Azure Information Protection - Stratégies**, sélectionnez **Globale** si les paramètres que vous souhaitez configurer s’appliquent à tous les utilisateurs.
    
    Si les paramètres à configurer se trouvent dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, sélectionnez votre stratégie délimitée à la place.

3. Dans le panneau **Stratégie**, configurez les paramètres suivants :
    
   - **Sélectionner l’étiquette par défaut** : Lorsque vous définissez cette option, sélectionnez l’étiquette à attribuer à des documents et des e-mails qui n’ont pas d’étiquette. Vous ne pouvez pas définir une étiquette par défaut si elle a des sous-étiquettes.
        
        Ce paramètre s’applique aux applications Office et au scanneur. Il ne s’applique pas à l’Explorateur de fichiers ou à PowerShell.
    
    - **Envoyer des données d’audit à l’analytique Azure Information Protection** : avant la création d’un espace de travail Azure Log Analytics pour [l’analytique Azure Information](reports-aip.md), les valeurs de ce paramètre indiquent **Désactivé** et **Non configuré**. Après la création de l’espace de travail, elles deviennent **Désactivé** et **Activé**.
        
        Lorsque le paramètre est **Activé**, les points de terminaison qui prennent en charge la création centralisée de rapports envoient leurs données d’audit au service Azure Information Protection. Pour plus d’informations sur les informations envoyées et stockées, voir la section [Informations collectées et envoyées à Microsoft](reports-aip.md#information-collected-and-sent-to-microsoft). Définissez cette option sur **Désactivé** pour empêcher l’envoi de ces données.
    
    - **Tous les documents et e-mails doivent avoir une étiquette** : Lorsque vous paramétrez cette option sur **Activé**, une étiquette doit être appliquée à tous les documents et e-mails envoyés enregistrés. L’étiquetage peut être affecté manuellement par un utilisateur, automatiquement à la suite d’une [condition](configure-policy-classification.md), ou être attribué par défaut (en définissant l’option **Sélectionner l’étiquette par défaut**.
        
       Si aucune étiquette n’est affectée quand les utilisateurs enregistrent un document ou envoient un e-mail, ils sont invités à sélectionner une étiquette. Par exemple :
        
       ![Invite d’Azure Information Protection si un étiquetage est appliqué](./media/info-protect-enforce-labelv2.png)
        
       Cette option ne s’applique pas lorsque vous supprimez une étiquette à l’aide de la cmdlet PowerShell [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) avec le paramètre *RemoveLabel*.
        
   - **Les utilisateurs doivent fournir une justification pour définir une étiquette de classification moins élevée, supprimer une étiquette ou supprimer la protection** : Si cette option est définie sur **Activé** et qu’un utilisateur effectue une de ces actions (par exemple, s’il change le niveau de l’étiquette **Public** en **Personnel**), il est invité à justifier cette action. Par exemple, l’utilisateur peut expliquer que le document ne contient plus d’informations sensibles. L’action et sa justification sont enregistrées dans leur journal des événements Windows local : **Journaux des applications et des services** > **Azure Information Protection**.  
        
       ![Azure Information Protection génère une invite si la nouvelle classification est inférieure](./media/info-protect-lower-justification.png)
        
       Cette option n’est pas applicable pour abaisser le niveau de classification des sous-étiquettes sous la même étiquette parente.
        
   - **Pour les e-mails contenant des pièces jointes, appliquez une étiquette correspondant à la classification la plus élevée de ces pièces jointes** : Lorsque vous définissez cette option sur **Recommandé**, les utilisateurs sont invités à appliquer une étiquette à leur e-mail. L’étiquette est choisie dynamiquement en fonction des étiquettes de classification qui sont appliquées aux pièces jointes, et l’étiquette de classification la plus élevée est sélectionnée. La pièce jointe doit être un fichier physique et ne peut pas être un lien vers un fichier (par exemple, un lien vers un fichier sur SharePoint ou OneDrive Entreprise). Les utilisateurs peuvent accepter la recommandation ou l’ignorer. Quand vous définissez cette option sur **Automatique**, l’étiquette est appliquée automatiquement, mais les utilisateurs peuvent la supprimer ou sélectionner une autre étiquette avant d’envoyer l’e-mail.
        
        Pour prendre le classement des sous-étiquettes en compte lorsque vous utilisez ce paramètre de stratégie, vous devez [configurer un paramètre client avancé](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments).
        
        Quand la pièce jointe avec l’étiquette de classification la plus élevée est configurée pour la protection avec le paramètre en préversion des autorisations définies par l’utilisateur : - Pour la version en disponibilité générale du client : L’e-mail est étiqueté avec la même classification, mais la protection n’est pas appliquée.
            - Pour la préversion du client : Quand les autorisations définies par l’utilisateur de l’étiquette incluent Outlook (Ne pas transférer), cette étiquette est appliquée et la protection Ne pas transférer est appliquée à l’e-mail. Quand les autorisations définies par l’utilisateur de l’étiquette sont seulement pour Word, Excel, PowerPoint et l’Explorateur de fichiers, cette étiquette n’est pas appliquée à l’e-mail, tout comme la protection.
    
   - **Afficher la barre Information Protection dans les applications Office** : Lorsque ce paramètre est désactivé, les utilisateurs ne peuvent pas sélectionner d’étiquettes depuis une barre dans Word, Excel, PowerPoint et Outlook. En revanche, les utilisateurs peuvent sélectionner des étiquettes au moyen du bouton **Protéger** dans le ruban. Lorsque ce paramètre est activé, les utilisateurs peuvent sélectionner des étiquettes par le biais de la barre et du bouton.
        
       Lorsque ce paramètre est activé, il peut être utilisé conjointement avec un paramètre client avancé, afin que les utilisateurs puissent [masquer définitivement la barre Azure Information Protection](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar) s’ils choisissent de ne pas l’afficher. Ils peuvent le faire en désactivant l’option **Afficher la barre** à partir du bouton **Protéger**.
    
   - **Ajouter le bouton Ne pas transférer au ruban Outlook** : Lorsque ce paramètre est activé, les utilisateurs peuvent sélectionner ce bouton à partir du groupe **Protection** dans le ruban Outlook en plus de sélectionner l’option **Ne pas transférer** à partir des menus Outlook. Pour vous assurer que les utilisateurs classent et protègent leurs e-mails, vous pouvez choisir de ne pas ajouter ce bouton mais de préférer [configurer une étiquette pour la protection](configure-policy-protection.md) ainsi qu’une autorisation définie par l’utilisateur pour Outlook. Du point de vue fonctionnel, ce paramètre de protection revient à sélectionner le bouton **Ne pas transférer**, mais lorsque cette fonctionnalité est incluse dans une étiquette, les e-mails sont classés en même temps qu’ils sont protégés.
    
       Ce paramètre de stratégie peut également être configuré avec un paramètre client avancé en tant que [personnalisation du client](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook).
    
   - **Activer les options d’autorisations personnalisées pour les utilisateurs** : Lorsque ce paramètre est activé, les utilisateurs voient les options permettant de définir leurs propres paramètres de protection qui peuvent remplacer les paramètres de protection que vous avez peut-être inclus avec une configuration d’étiquette. Les utilisateurs peuvent voir également une option pour supprimer la protection. Lorsque ce paramètre est désactivé, les utilisateurs ne voient pas ces options.
        
       Notez que ce paramètre de stratégie n’a aucun effet sur les autorisations personnalisées que les utilisateurs peuvent configurer à l’aide des options de menu Office. Ce paramètre de stratégie peut également être configuré avec un paramètre client avancé en tant que [personnalisation du client](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users).
        
       Les options des autorisations personnalisées se trouvent aux emplacements suivants :
        
       - Dans les applications Office : À partir du ruban, onglet **Accueil** > groupe **Protection** > **Protéger** > **Autorisations personnalisées**
        
       - Depuis l'Explorateur de fichiers : Cliquez avec le bouton droit sur > **Classifier et protéger** > **Autorisations personnalisées**
    
   - **Fournir une URL personnalisée pour la page web « En savoir plus » du client Azure Information Protection** : Les utilisateurs voient ce lien à la section **Aide et commentaires** dans la boîte de dialogue **Microsoft Azure Information Protection** lorsqu’ils sélectionnent **Protéger** > **Aide et commentaires** sous l’onglet **Accueil** de leurs applications Office. Par défaut, ce lien pointe vers le site web [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection). Si vous souhaitez faire pointer ce lien vers une autre page web, vous pouvez entrer une URL HTTP ou HTTPS (recommandé). Aucun contrôle n’est effectué pour vérifier si l’URL personnalisée entrée est accessible ou si elle s’affiche correctement sur tous les appareils.
        
       Par exemple, pour le support technique, vous pouvez entrer la page de documentation de Microsoft qui inclut des informations sur l’installation et l’utilisation du client (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**) ou publier des informations de version (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**). Vous pouvez également publier votre propre page web comprenant des informations sur la façon de contacter votre support technique ou une vidéo qui explique pas à pas comment utiliser les étiquettes configurées.

4. Pour enregistrer vos modifications et les rendre disponibles pour les utilisateurs, cliquez sur **Enregistrer**.

Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

## <a name="next-steps"></a>Étapes suivantes

Pour voir comment certains de ces paramètres de stratégie peuvent fonctionner ensemble, essayez le tutoriel [Configurer des paramètres Azure Information Protection qui fonctionnent ensemble](infoprotect-settings-tutorial.md).

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

