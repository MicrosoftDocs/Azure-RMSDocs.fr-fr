---
title: "Configurer les conditions d’une étiquette Azure Information Protection"
description: "Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: ef84f3ceb8f732dd475b4db8eae489e715d4b7da
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez : 

- La classification automatique s’applique à Word, Excel et PowerPoint lorsque les fichiers sont enregistrés et s’applique à Outlook lors de l’envoi d’e-mails. Vous ne pouvez pas utiliser la classification automatique des fichiers qui ont déjà été étiquetés manuellement.
 
- La classification recommandée s’applique à Word, Excel et PowerPoint lors de l’enregistrement de fichiers.

Quand vous configurez des conditions, vous pouvez utiliser des modèles prédéfinis, comme **Numéro de carte de crédit** ou **Numéro de sécurité sociale (USA)**. Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique. Ces conditions s’appliquent au corps de texte dans les documents et les e-mails, ainsi qu’aux en-têtes et pieds de page. Pour plus d’informations sur les conditions, consultez la section [Détails des types d’informations](#details-about-the-information-types).

Évaluation de plusieurs conditions lorsqu’elles s’appliquent à plusieurs étiquettes :

1. Les étiquettes sont triées en vue de leur évaluation, en fonction de leur position que vous spécifiez dans la stratégie : l’étiquette positionnée en premier a la position la plus basse (la moins sensible) et l’étiquette positionnée en dernier a la position la plus élevée (la plus sensible).

2. L’étiquette la plus sensible est appliquée.
 
3. La dernière sous-étiquette est appliquée.

> [!TIP]
>Pour bénéficier de la meilleure expérience utilisateur possible et pour assurer la continuité des activités, nous vous recommandons de commencer avec la classification recommandée par l’utilisateur plutôt que par la classification automatique. Cette configuration permet à vos utilisateurs d’accepter l’action d’étiquetage ou de protection, ou de modifier ces suggestions si elles ne sont pas adaptées à leur document ou à leur e-mail.

Un exemple d’invite s’affiche lorsque vous configurez une condition d’application d’une étiquette en tant qu’action recommandée, avec un conseil de stratégie personnalisé :

![Détection et recommandations Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

Dans cet exemple, l’utilisateur peut cliquer sur **Modifier maintenant** pour appliquer l’étiquette recommandée ou remplacer la recommandation en sélectionnant **Ignorer**.

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Pour configurer la classification automatique ou recommandée pour une étiquette

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**.
    
    Si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Dans le panneau **Azure Information Protection - Stratégie globale** ou le panneau **Stratégie :\<nom>**, sélectionnez l’étiquette à configurer. 

4. Dans le panneau **Étiquette**, dans la section **Configurer des conditions pour appliquer automatiquement cette étiquette**, cliquez sur **Ajouter une condition**.

5. Dans le panneau **Condition**, sélectionnez **Types d’informations** si vous voulez utiliser une condition prédéfinie, ou **Personnalisé** si vous voulez spécifier votre propre condition, puis cliquez sur **Enregistrer** :
    - Pour **Types d’informations** : sélectionnez une condition dans la liste des conditions disponibles, puis sélectionnez le nombre minimal d’occurrences et déterminez si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Pour utiliser la liste complète des conditions, vous devez avoir la préversion actuelle du client Azure Information Protection. Si vous avez la version actuelle de disponibilité générale du client, seules les cinq conditions suivantes sont prises en charge : **Code SWIFT**, **Numéro de carte de crédit**, **Numéro d’acheminement ABA**, **Numéro de sécurité sociale (USA)** et **Numéro de compte bancaire international (IBAN)**. [Plus d’informations](#details-about-the-information-types)
    
    - Pour **Personnalisé** : spécifiez un nom et une expression pour la correspondance, sans guillemets ni caractères spéciaux. Spécifiez ensuite s’il s’agit d’une expression régulière, si la casse doit être respectée, le nombre minimal d’occurrences, et si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Si vous avez la préversion actuelle du client Azure Information Protection, les expressions régulières utilisent les modèles regex d’Office 365. Pour plus d’informations, consultez [Définition de correspondances basées sur des expressions régulières](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) dans la documentation Office. 
        
    **Exemple d’options occurrences** : vous sélectionnez l’option de numéro de sécurité sociale (USA) intégrée et définissez le nombre minimal d’occurrences sur 2, et un document contient deux fois le même numéro de sécurité sociale (USA) : si vous définissez **Compter les occurrences avec des valeurs uniques uniquement** sur **Activé**, la condition n’est pas remplie. Si vous définissez cette option sur **Désactivé**, la condition est remplie.

6. Dans le panneau **Étiquette**, configurez les options suivantes, puis cliquez sur **Enregistrer** :
    
    - Choisissez la classification automatique ou recommandée : pour l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur**, sélectionnez **Automatique** ou **Recommandée**.
    
    - Spécifiez le texte de l’invite utilisateur ou du conseil de stratégie : conservez le texte par défaut ou spécifiez votre propre chaîne.

7. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** initial sur **Publier**.

## <a name="details-about-the-information-types"></a>Détails des types d’informations

Si vous avez la préversion actuelle du client Azure Information Protection, la liste complète des types d’informations est prise en charge et utilise les types d’informations sensibles et la détection de modèle de prévention de perte de données (DLP) d’Office 365. Vous avez le choix entre les nombreux types courants d’informations sensibles, dont certains sont spécifiques à certaines régions. Pour plus d’informations, consultez [Éléments recherchés par les types d’informations sensibles](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) dans la documentation Office. Quand Azure Information Protection évalue ces types d’informations, il n’utilise pas le paramètre de niveau de confiance DLP d’Office, mais recherche celui avec le niveau de confiance le plus faible.  

Si vous avez la version actuelle de disponibilité générale du client, seuls les types d’informations suivants sont pris en charge :

- [Code SWIFT](#swift-code )

- [Numéro de carte de crédit](#credit-card-number )

- [Numéro d’acheminement ABA](#aba-routing-number )

- [Numéro de sécurité sociale (SSN) (USA)](#usa-social-security-number-ssn)

- [Numéro de compte bancaire international (IBAN)](#international-banking-account-number-iban)

Consultez les sections suivantes pour plus de détails sur chaque type d’informations de la version de disponibilité générale du client.

### <a name="swift-code"></a>Code SWIFT

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

1. L’une des expressions suivantes : **swift**, **swiftnumber**, **swiftroutingnumber** 

2. Un code Swift dans un schéma mis en forme :  

    a. 4 lettres (code bancaire)  

    b. 2 lettres (indicatif de pays)  

    c. 2 lettres ou chiffres (code d’emplacement)  

    d. 3 lettres ou chiffres en option (code de succursale)  


Exemples de test :

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### <a name="credit-card-number"></a>Numéro de carte de crédit

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

- Un numéro de carte de crédit valide dans un schéma mis en forme ou non, qui transmet la [somme de contrôle Luhn](https://wikipedia.org/wiki/Luhn_algorithm). Ce type d’information détecte les cartes de grandes marques dans le monde entier, notamment Visa, MasterCard, Discover Card, American Express et Diners.

    - **Avec mise en forme** :
    
        - 16 chiffres: (cccc-cccc-cccc-cccc)  
        
    - **Sans mise en forme** :
    
        - (cccccccccccccccc)  


Exemples de test :

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### <a name="aba-routing-number"></a>Numéro d’acheminement ABA

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

1. Au moins l’une des expressions suivantes : **aba**, **rtn**, **numéro d’acheminement** 

2. Un numéro d’acheminement ABA, qui comprend 9 chiffres pouvant être mis en forme ou non : 

    - **Avec mise en forme** : 
        
        a. Quatre chiffres commençant par 0, 1, 2, 3, 6, 7 ou 8 
        
        b. Un trait d’union 
        
        c. Quatre chiffres 
        
        d. Un trait d’union 
        
        e. Un chiffre 
        
        Exemple : 3456-9876-1 ABA 
        
    - **Sans mise en forme** : 
        
        9 chiffres consécutifs commençant par 0, 1, 2, 3, 6, 7 ou 8 
        
        Exemple : 345698761 RTN 
 

Exemples de test :

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### <a name="usa-social-security-number-ssn"></a>Numéro de sécurité sociale (SSN) (USA)

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

1. Au moins l’une des expressions suivantes : **ssn**, **social security**, **ssid**, **ss#** 

2. Un numéro de sécurité sociale : 9 chiffres mis en forme ou non :

    - **Avec mise en forme** : 
    
        - Neuf chiffres au format suivant : ccc-cc-cccc OU ccc cc cccc 
        
    - **Sans mise en forme** : 
    
        - Neuf chiffres au format suivant : ccccccccc 


Exemples de test :

- **SSN 123-45-6789**

- **SS# 123456789** 


----

### <a name="international-banking-account-number-iban"></a>Numéro de compte bancaire international (IBAN)

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

1. L’expression suivante : **IBAN** 

2. Un numéro IBAN : commence par un code de pays (deux lettres), suivi par des chiffres de contrôle (deux chiffres), puis par un numéro IBAN (jusqu’à 30 chiffres).


Exemples de test :

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


