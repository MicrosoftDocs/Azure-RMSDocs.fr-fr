---
title: Configurer les conditions d’une étiquette Azure Information Protection – AIP
description: Les conditions permettent d’affecter automatiquement une étiquette à un document ou à un e-mail. Vous pouvez également inviter les utilisateurs à sélectionner une étiquette recommandée.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: da76767b7538706f596653b77f3f29f8717e1442
ms.sourcegitcommit: 2c90f5bf11ec34ab94824a39ccab75bde71fc3aa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314796"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez. 

Quand vous configurez ces conditions, vous pouvez utiliser des modèles prédéfinis, comme **Numéro de carte de crédit** ou **Numéro de sécurité sociale (USA)**. Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique. Ces conditions s’appliquent au corps de texte dans les documents et les e-mails, ainsi qu’aux en-têtes et pieds de page. Pour plus d’informations sur les conditions, consultez l’étape 5 de la [procédure suivante](#to-configure-recommended-or-automatic-classification-for-a-label).

Pour bénéficier de la meilleure expérience utilisateur possible et pour assurer la continuité des activités, nous vous recommandons de commencer avec la classification recommandée par l’utilisateur plutôt que par la classification automatique. Cette configuration permet à vos utilisateurs d’accepter la classification et toute protection associée, ou de modifier ces suggestions si elles ne sont pas adaptées à leur document ou à leur e-mail.

Un exemple d’invite s’affiche lorsque vous configurez une condition d’application d’une étiquette en tant qu’action recommandée, avec un conseil de stratégie personnalisé :

![Détection et recommandations Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

Dans cet exemple, l’utilisateur peut cliquer sur **Modifier maintenant** pour appliquer l’étiquette recommandée ou remplacer la recommandation en sélectionnant **Ignorer**. Si l’utilisateur choisit d’ignorer la recommandation et que la condition s’applique toujours quand le document est ensuite ouvert, la recommandation de l’étiquette est réaffichée. 

> [!IMPORTANT]
>Ne configurez pas une étiquette pour la classification automatique et une autorisation définie par l’utilisateur. L’option de configuration des autorisations définies par l’utilisateur est un [paramètre de protection](configure-policy-protection.md) qui permet aux utilisateurs de spécifier qui doit avoir des autorisations.
>
>Lorsqu’une étiquette est configurée pour la classification automatique alors que des autorisations sont définies par l’utilisateur, les conditions sont vérifiées dans le contenu et le paramètre de configuration des autorisations définies par l’utilisateur n’est pas appliqué. Vous pouvez utiliser la classification et les autorisations définies par l’utilisateur recommandées.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Manière d’appliquer des étiquettes automatiques ou recommandées

- La classification automatique s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents tandis qu’elle s’applique à Outlook lors de l’envoi d’e-mails. 
    
    Vous ne pouvez pas utiliser la classification automatique pour des documents et e-mails qui ont été déjà été étiquetés manuellement ou automatiquement avec une classification plus élevée. 

- La classification recommandée s’applique à Word, Excel et PowerPoint lors de l’enregistrement de documents. Vous ne pouvez pas utiliser la classification recommandée pour Outlook si vous ne configurez pas un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook), qui est actuellement en préversion.
    
    Vous ne pouvez pas utiliser la classification recommandée pour des documents qui ont préalablement été étiquetés avec une classification plus élevée. 

Vous pouvez changer ce comportement afin que le client Azure Information Protection vérifie régulièrement les règles des conditions que vous spécifiez dans les documents. Cette configuration nécessite un [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) qui est disponible en préversion.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Évaluation de plusieurs conditions lorsqu’elles s’appliquent à plusieurs étiquettes

1. Les étiquettes sont triées pour l’évaluation, en fonction de leur position que vous spécifiez dans la stratégie : L’étiquette en premier a la position la plus faible (moins sensible) et l’étiquette en dernier a la position la plus élevée (plus sensible).

2. L’étiquette la plus sensible est appliquée.
 
3. La dernière sous-étiquette est appliquée.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Pour configurer la classification automatique ou recommandée pour une étiquette

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **Classifications** > **Étiquettes** : Dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez l’étiquette à configurer.

3. Dans le panneau **Étiquette**, dans la section **Configurer des conditions pour appliquer automatiquement cette étiquette**, cliquez sur **Ajouter une condition**.

4. Dans le panneau **Condition**, sélectionnez **Types d’informations** pour utiliser une condition prédéfinie ou **Personnalisé** pour spécifier votre propre condition :
    - Pour **Types d’informations** : Sélectionnez une condition dans la liste des conditions disponibles, puis sélectionnez le nombre minimal d’occurrences et déterminez si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les types d’informations utilisent les types d’informations sensibles et la détection de modèle de protection contre la perte de données (DLP) d’Office 365. Vous avez le choix entre les nombreux types courants d’informations sensibles, dont certains sont spécifiques à certaines régions. Pour plus d’informations, voir [Éléments recherchés par les types d’informations sensibles](/office365/securitycompliance/what-the-sensitive-information-types-look-for) dans la documentation d’Office 365.
        
        La liste des types d’informations que vous pouvez sélectionner à partir du portail Azure est régulièrement mise à jour pour inclure les nouveaux ajouts DLP Office. Toutefois, elle exclut tous les types d’informations sensibles personnalisés que vous avez définis et téléchargés sous la forme d’un package de règles dans le Centre de sécurité et conformité Office 365.
        
        > [!IMPORTANT]
        > Certains types d’informations nécessitent une version minimale du client. [Plus d’informations](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Quand Azure Information Protection évalue les types d’informations que vous sélectionnez, il n’utilise pas le paramètre de niveau de confiance DLP d’Office, mais recherche celui avec le niveau de confiance le plus faible.
    
    - Pour **Personnalisé** : Spécifiez un nom et une expression pour la correspondance, sans guillemets ni caractères spéciaux. Spécifiez ensuite s’il s’agit d’une expression régulière, si la casse doit être respectée, le nombre minimal d’occurrences, et si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Les expressions régulières utilisent les modèles regex d’Office 365. Pour vous aider à spécifier des expressions régulières pour vos conditions personnalisées, consultez la version spécifique suivante de la [syntaxe des expressions régulières Perl](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) dans Boost.
        
5. Si nécessaire, changez les options **Nombre minimal d’occurrences** et **Comptabiliser seulement les occurrences avec des valeurs uniques**, puis sélectionnez **Enregistrer**. 
    
    Exemples d’options d’occurrences : Vous sélectionnez le type d’information pour le numéro de sécurité sociale, définissez le nombre minimal d’occurrences sur 2 et un document a le même numéro de sécurité sociale répertorié deux fois : Si vous définissez l’option **Comptabiliser seulement les occurrences avec des valeurs uniques** à **Activé**, la condition n’est pas remplie. Si vous définissez cette option sur **Désactivé**, la condition est remplie.

6. Dans le panneau **Étiquette**, configurez les options suivantes, puis cliquez sur **Enregistrer** :
    
    - Choisissez la classification automatique ou recommandée : Pour l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur**, sélectionnez **Automatique** ou **Recommandée**.
    
    - Spécifiez le texte de l’invite utilisateur ou du conseil de stratégie : Conservez le texte par défaut ou spécifiez votre propre chaîne.

Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>Types d’informations sensibles nécessitant une version minimale du client

Les types d’informations sensibles suivants nécessitent au minimum la version 1.37.19.0 pour le client Azure Information Protection :

- **Numéro de téléphone mobile dans l’UE**
- **Numéro de passeport dans l’UE**
- **Numéro de permis de conduire dans l’UE**
- **Numéro d’identification nationale dans l’UE**
- **Numéro de sécurité sociale ou équivalent dans l’UE**
- **Numéro de T.V.A. intra-communautaire dans l’UE**
- **Code d’identification des personnes en Thaïlande**
- **Numéro d’identification nationale en Turquie**
- **Numéro de carte de résidence au Japon**


Les types d’informations sensibles suivants nécessitent la préversion actuelle du client Azure Information Protection :

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

En outre, les types d’informations sensibles suivants ne sont pas pris en charge pour la préversion actuelle du client Azure Information Protection et n’apparaissent plus dans le portail Azure :

- **Numéro de téléphone dans l’UE**
- **Coordonnées GPS dans l’UE**

## <a name="next-steps"></a>Étapes suivantes

Envisagez de déployer le [scanneur Azure Information Protection](deploy-aip-scanner.md), qui peut utiliser vos règles de classification automatique pour découvrir, classifier et protéger des fichiers situés dans les partages réseau et les magasins de fichiers locaux.  

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).


