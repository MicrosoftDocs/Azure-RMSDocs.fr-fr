---
title: Configurer les conditions d’une étiquette Azure Information Protection – AIP
description: Les conditions permettent d’affecter automatiquement une étiquette à un document ou à un e-mail. Vous pouvez également inviter les utilisateurs à sélectionner une étiquette recommandée.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: c91ad278b9ce4e699a9756cc228fd8bccd4b65e2
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75742912"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


> [!NOTE]
> Ces instructions s’appliquent au client Azure Information Protection (classique) et pas au client d’étiquetage unifié Azure Information Protection. Vous ne connaissez pas trop la différence entre ces clients ? Consultez ce [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client).
> 
> Si vous recherchez des informations pour configurer la classification automatique et recommandée pour le client d’étiquetage unifié, consultez la documentation Office. Par exemple, [appliquez automatiquement une étiquette de sensibilité au contenu](/microsoft-365/compliance/apply-sensitivity-label-automatically).

Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez. 

Quand vous configurez ces conditions, vous pouvez utiliser des modèles prédéfinis, comme **Numéro de carte de crédit** ou **Numéro de sécurité sociale (USA)** . Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique. Ces conditions s’appliquent au corps de texte dans les documents et les e-mails, ainsi qu’aux en-têtes et pieds de page. Pour plus d’informations sur les conditions, consultez l’étape 5 de la [procédure suivante](#to-configure-recommended-or-automatic-classification-for-a-label).

Pour bénéficier de la meilleure expérience utilisateur possible et pour assurer la continuité des activités, nous vous recommandons de commencer avec la classification recommandée par l’utilisateur plutôt que par la classification automatique. Cette configuration permet à vos utilisateurs d’accepter la classification et toute protection associée, ou de modifier ces suggestions si elles ne sont pas adaptées à leur document ou à leur e-mail.

Un exemple d’invite s’affiche lorsque vous configurez une condition d’application d’une étiquette en tant qu’action recommandée, avec un conseil de stratégie personnalisé :

![Détection et recommandations Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

Dans cet exemple, l’utilisateur peut cliquer sur **Modifier maintenant** pour appliquer l’étiquette recommandée ou remplacer la recommandation en sélectionnant **Ignorer**. Si l’utilisateur choisit d’ignorer la recommandation et que la condition s’applique toujours quand le document est ensuite ouvert, la recommandation de l’étiquette est réaffichée.

Si vous configurez la classification automatique au lieu de la classification recommandée, l’étiquette est appliquée automatiquement et l’utilisateur continue de voir une notification dans Word, Excel et PowerPoint. Toutefois, les boutons **modifier maintenant** et **Ignorer** sont remplacés par **OK**. Dans Outlook, il n’existe pas de notification pour la classification automatique, et l’étiquette est appliquée au moment de que l’e-mail est envoyé.

> [!IMPORTANT]
>Ne configurez pas une étiquette pour la classification automatique et une autorisation définie par l’utilisateur. L’option de configuration des autorisations définies par l’utilisateur est un [paramètre de protection](configure-policy-protection.md) qui permet aux utilisateurs de spécifier qui doit avoir des autorisations.
>
>Lorsqu’une étiquette est configurée pour la classification automatique alors que des autorisations sont définies par l’utilisateur, les conditions sont vérifiées dans le contenu et le paramètre de configuration des autorisations définies par l’utilisateur n’est pas appliqué. Vous pouvez utiliser la classification et les autorisations définies par l’utilisateur recommandées.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Manière d’appliquer des étiquettes automatiques ou recommandées

- La classification automatique s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents et s’applique à Outlook quand vous envoyez des e-mails. 
    
    Vous ne pouvez pas utiliser la classification automatique pour des documents et e-mails qui ont été déjà été étiquetés manuellement ou automatiquement avec une classification plus élevée. 

- La classification recommandée s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents. Vous ne pouvez pas utiliser la classification recommandée pour Outlook si vous ne configurez pas un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook), qui est actuellement en préversion.
    
    Vous ne pouvez pas utiliser la classification recommandée pour des documents qui ont préalablement été étiquetés avec une classification plus élevée. 

Vous pouvez changer ce comportement afin que le client Azure Information Protection vérifie régulièrement les règles des conditions que vous spécifiez dans les documents. C’est le cas, par exemple, si vous utilisez l' [enregistrement](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) automatique avec les applications Office qui sont automatiquement enregistrées dans SharePoint Online, OneDrive ou onedrive entreprise. Pour prendre en charge ce scénario, vous pouvez configurer un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) qui est actuellement en version préliminaire. Le paramètre active la classification pour qu’elle s’exécute en continu en arrière-plan.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Évaluation de plusieurs conditions lorsqu’elles s’appliquent à plusieurs étiquettes

1. Les étiquettes sont triées en vue de leur évaluation, en fonction de leur position que vous spécifiez dans la stratégie : l’étiquette positionnée en premier a la position la plus basse (la moins sensible) et l’étiquette positionnée en dernier a la position la plus élevée (la plus sensible).

2. L’étiquette la plus sensible est appliquée.
 
3. La dernière sous-étiquette est appliquée.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Pour configurer la classification automatique ou recommandée pour une étiquette

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. À partir de l’option de menu **classifications** > **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez l’étiquette à configurer.

3. Dans le volet **étiquette** , dans la section **configurer des conditions pour appliquer automatiquement cette étiquette** , cliquez sur **Ajouter une nouvelle condition**.

4. Dans le volet **condition** , sélectionnez **types d’informations** si vous souhaitez utiliser une condition prédéfinie, ou **personnalisé** si vous souhaitez spécifier les vôtres :
    - Pour **Types d’informations** : sélectionnez une condition dans la liste des conditions disponibles, puis sélectionnez le nombre minimal d’occurrences et déterminez si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les types d’informations utilisent les types d’informations sensibles et la détection de modèle de protection contre la perte de données (DLP) d’Office 365. Vous avez le choix entre les nombreux types courants d’informations sensibles, dont certains sont spécifiques à certaines régions. Pour plus d’informations, voir [Éléments recherchés par les types d’informations sensibles](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) dans la documentation d’Office 365.
        
        La liste des types d’informations que vous pouvez sélectionner à partir du portail Azure est régulièrement mise à jour pour inclure les nouveaux ajouts DLP Office. Toutefois, elle exclut tous les types d’informations sensibles personnalisés que vous avez définis et téléchargés sous la forme d’un package de règles dans le Centre de sécurité et conformité Office 365.
        
        > [!IMPORTANT]
        > Certains types d’informations nécessitent une version minimale du client. [Informations complémentaires](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Quand Azure Information Protection évalue les types d’informations que vous sélectionnez, il n’utilise pas le paramètre de niveau de confiance DLP d’Office, mais recherche celui avec le niveau de confiance le plus faible.
    
    - Pour **Personnalisé** : spécifiez un nom et une expression pour la correspondance, sans guillemets ni caractères spéciaux. Spécifiez ensuite s’il s’agit d’une expression régulière, si la casse doit être respectée, le nombre minimal d’occurrences, et si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les expressions régulières utilisent les modèles regex d’Office 365. Pour vous aider à spécifier des expressions régulières pour vos conditions personnalisées, consultez la version spécifique suivante de la [syntaxe des expressions régulières Perl](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) dans Boost.
        
5. Si nécessaire, changez les options **Nombre minimal d’occurrences** et **Comptabiliser seulement les occurrences avec des valeurs uniques**, puis sélectionnez **Enregistrer**. 
    
    Exemple d’options occurrences : Vous sélectionnez le numéro de sécurité sociale (USA) comme type d’informations et affectez au nombre minimal d’occurrences la valeur 2, et un document contient deux fois le même numéro de sécurité sociale. Si vous définissez **Comptabiliser seulement les occurrences avec des valeurs uniques** sur **Activé**, la condition n’est pas remplie. Si vous définissez cette option sur **Désactivé**, la condition est remplie.

6. De retour dans le volet **étiquette** , configurez les éléments suivants, puis cliquez sur **Enregistrer**:
    
    - Choisissez la classification automatique ou recommandée : pour l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur**, sélectionnez **Automatique** ou **Recommandée**.
    
    - Spécifiez le texte de l’invite utilisateur ou du conseil de stratégie : conservez le texte par défaut ou spécifiez votre propre chaîne.

Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>Types d’informations sensibles nécessitant une version minimale du client

Les types d’informations sensibles suivants requièrent une version minimale de [1.48.204.0](./rms-client/client-version-release-history.md#version-1482040) du client Azure information protection :

- **Chaîne de connexion Azure Service Bus**
- **Chaîne de connexion Azure IoT**
- **Compte de stockage Azure**
- **Chaîne de connexion de la base de données Azure IAAS et chaîne de connexion SQL Azure**
- **Chaîne de connexion du Cache Redis Azure**
- **Azure SAS**
- **Chaîne de connexion SQL Server**
- **Clé d’authentification Azure DocumentDB**
- **Mot de passe de paramètre de publication Azure**
- **Clé de compte de stockage Azure (générique)**

Pour plus d’informations sur ces types d’informations sensibles, consultez le billet de blog suivant : [Azure information protection vous aide à être plus sûr en détectant automatiquement les informations d’identification](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-helps-you-to-be-more-secure-by/ba-p/360181)

En outre, à partir de 1.48.204.0 du client Azure Information Protection, les types d’informations sensibles suivants ne sont pas pris en charge et ne s’affichent plus dans le Portail Azure. Si vous avez des étiquettes qui utilisent ces types d’informations sensibles, nous vous recommandons de les supprimer, car nous ne pouvons pas garantir une détection correcte pour eux et les références à celles-ci dans les rapports du scanneur doivent être ignorées :

- **Numéro de téléphone dans l’UE**
- **Coordonnées GPS dans l’UE**

## <a name="next-steps"></a>Étapes suivantes

Envisagez de déployer le [scanneur Azure Information Protection](deploy-aip-scanner.md), qui peut utiliser vos règles de classification automatique pour découvrir, classifier et protéger des fichiers situés dans les partages réseau et les magasins de fichiers locaux.  

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).
