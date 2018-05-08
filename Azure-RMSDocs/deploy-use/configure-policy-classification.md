---
title: Configurer les conditions d’une étiquette Azure Information Protection
description: Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/30/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: 053d8dfd51d8c79cdc733f4395226c12ab6e2102
ms.sourcegitcommit: 87d73477b7ae9134b5956d648c390d2027a82010
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez. 

Quand vous configurez ces conditions, vous pouvez utiliser des modèles prédéfinis, comme **Numéro de carte de crédit** ou **Numéro de sécurité sociale (USA)**. Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique. Ces conditions s’appliquent au corps de texte dans les documents et les e-mails, ainsi qu’aux en-têtes et pieds de page. Pour plus d’informations sur les conditions, consultez l’étape 5 de la [procédure suivante](#to-configure-recommended-or-automatic-classification-for-a-label).

Pour bénéficier de la meilleure expérience utilisateur possible et pour assurer la continuité des activités, nous vous recommandons de commencer avec la classification recommandée par l’utilisateur plutôt que par la classification automatique. Cette configuration permet à vos utilisateurs d’accepter la classification et toute protection associée, ou de modifier ces suggestions si elles ne sont pas adaptées à leur document ou à leur e-mail.

Un exemple d’invite s’affiche lorsque vous configurez une condition d’application d’une étiquette en tant qu’action recommandée, avec un conseil de stratégie personnalisé :

![Détection et recommandations Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

Dans cet exemple, l’utilisateur peut cliquer sur **Modifier maintenant** pour appliquer l’étiquette recommandée ou remplacer la recommandation en sélectionnant **Ignorer**. Si l’utilisateur choisit d’ignorer la recommandation et que la condition s’applique toujours quand le document est ensuite ouvert, la recommandation de l’étiquette est réaffichée. 

> [!IMPORTANT]
>Ne configurez pas une étiquette pour la classification automatique et une autorisation définie par l’utilisateur. L’option de configuration des autorisations définies par l’utilisateur est un [paramètre de protection](configure-policy-protection.md) qui permet aux utilisateurs de spécifier qui doit avoir des autorisations.
>
>Lorsqu’une étiquette est configurée pour la classification automatique alors que des autorisations sont définies par l’utilisateur, les conditions sont vérifiées dans le contenu et le paramètre de configuration des autorisations définies par l’utilisateur n’est pas appliqué. Vous pouvez utiliser la classification et les autorisations définies par l’utilisateur recommandées.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Manière d’appliquer des étiquettes automatiques ou recommandées

- La classification automatique s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents tandis qu’elle s’applique à Outlook lors de l’envoi d’e-mails. 
    
    Vous ne pouvez pas utiliser la classification automatique pour des documents et e-mails qui ont été déjà été étiquetés manuellement ou automatiquement avec une classification plus élevée. 

- La classification recommandée s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents. Vous ne pouvez pas utiliser la classification recommandée pour Outlook.
    
    Vous ne pouvez pas utiliser la classification recommandée pour des documents qui ont préalablement été étiquetés avec une classification plus élevée. 

Vous pouvez changer ce comportement afin que le client Azure Information Protection vérifie régulièrement les règles des conditions que vous spécifiez dans les documents. Cette configuration nécessite un [paramètre client avancé](../rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) qui est disponible en préversion.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Évaluation de plusieurs conditions lorsqu’elles s’appliquent à plusieurs étiquettes

1. Les étiquettes sont triées en vue de leur évaluation, en fonction de leur position que vous spécifiez dans la stratégie : l’étiquette positionnée en premier a la position la plus basse (la moins sensible) et l’étiquette positionnée en dernier a la position la plus élevée (la plus sensible).

2. L’étiquette la plus sensible est appliquée.
 
3. La dernière sous-étiquette est appliquée.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Pour configurer la classification automatique ou recommandée pour une étiquette

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette que vous souhaitez configurer.

3. Dans le panneau **Étiquette**, dans la section **Configurer des conditions pour appliquer automatiquement cette étiquette**, cliquez sur **Ajouter une condition**.

4. Dans le panneau **Condition**, sélectionnez **Types d’informations** pour utiliser une condition prédéfinie ou **Personnalisé** pour spécifier votre propre condition :
    - Pour **Types d’informations** : sélectionnez une condition dans la liste des conditions disponibles, puis sélectionnez le nombre minimal d’occurrences et déterminez si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les types d’informations utilisent les types d’informations sensibles et la détection de modèle de protection contre la perte de données (DLP) d’Office 365. Vous avez le choix entre les nombreux types courants d’informations sensibles, dont certains sont spécifiques à certaines régions. Pour plus d’informations, consultez [Éléments recherchés par les types d’informations sensibles](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) dans la documentation Office.
        
        La liste des types d’informations que vous pouvez sélectionner à partir du portail Azure est régulièrement mise à jour pour inclure les nouveaux ajouts DLP Office. Toutefois, elle exclut tous les types d’informations sensibles personnalisés que vous avez définis et téléchargés sous la forme d’un package de règles dans le Centre de sécurité et conformité Office 365. 
        
        Quand Azure Information Protection évalue les types d’informations que vous sélectionnez, il n’utilise pas le paramètre de niveau de confiance DLP d’Office, mais recherche celui avec le niveau de confiance le plus faible.
    
    - Pour **Personnalisé** : spécifiez un nom et une expression pour la correspondance, sans guillemets ni caractères spéciaux. Spécifiez ensuite s’il s’agit d’une expression régulière, si la casse doit être respectée, le nombre minimal d’occurrences, et si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les expressions régulières utilisent les modèles regex d’Office 365. Pour plus d’informations, consultez [Définition de correspondances basées sur des expressions régulières](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) dans la documentation Office. En outre, vous trouverez peut-être utile de consulter la page [Syntaxe des expressions régulières Perl](http://www.boost.org/doc/libs/1_66_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) de Boost.
        
5. Si nécessaire, changez les options **Nombre minimal d’occurrences** et **Comptabiliser seulement les occurrences avec des valeurs uniques**, puis sélectionnez **Enregistrer**. 
    
    Exemple d’options occurrences : Vous sélectionnez le numéro de sécurité sociale (USA) comme type d’informations et affectez au nombre minimal d’occurrences la valeur 2, et un document contient deux fois le même numéro de sécurité sociale. Si vous définissez **Comptabiliser seulement les occurrences avec des valeurs uniques** sur **Activé**, la condition n’est pas remplie. Si vous définissez cette option sur **Désactivé**, la condition est remplie.

6. Dans le panneau **Étiquette**, configurez les options suivantes, puis cliquez sur **Enregistrer** :
    
    - Choisissez la classification automatique ou recommandée : pour l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur**, sélectionnez **Automatique** ou **Recommandée**.
    
    - Spécifiez le texte de l’invite utilisateur ou du conseil de stratégie : conservez le texte par défaut ou spécifiez votre propre chaîne.

Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

## <a name="next-steps"></a>Étapes suivantes

Envisagez de déployer le [scanneur Azure Information Protection](deploy-aip-scanner.md), qui peut utiliser vos règles de classification automatique pour découvrir, classifier et protéger des fichiers situés dans les partages réseau et les magasins de fichiers locaux.  

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

