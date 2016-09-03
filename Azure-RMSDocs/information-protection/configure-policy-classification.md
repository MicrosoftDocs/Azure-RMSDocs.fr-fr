---
title: "Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection | Azure Rights Management"
description: "Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez."
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 0e6baca43c7a4f2e91f45222f5f6f233b3eeb438


---

# Comment configurer des conditions pour la classification automatique et recommandée pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Lorsque vous configurez des conditions pour une étiquette, vous pouvez affecter automatiquement une étiquette à un document ou à un e-mail. Ou vous pouvez inviter les utilisateurs à sélectionner l’étiquette que vous recommandez : 

- La classification automatique s’applique à Word, Excel et PowerPoint lorsque les fichiers sont enregistrés et s’applique à Outlook lors de l’envoi d’e-mails. Vous ne pouvez pas utiliser la classification automatique des fichiers qui ont déjà été étiquetés manuellement.
 
- La classification recommandée s’applique à Word, Excel et PowerPoint lors de l’enregistrement de fichiers.

Lorsque vous configurez des conditions, vous pouvez utiliser des modèles prédéfinis, tels que « Numéros de carte de crédit » ou « Numéro de sécurité sociale (USA) ». Vous pouvez aussi définir une chaîne ou un modèle personnalisé comme condition de classification automatique. Pour plus d’informations sur les conditions, consultez la section [Informations sur les conditions intégrées](#information-about-the-built-in-conditions).

Évaluation de plusieurs conditions lorsqu’elles s’appliquent à plusieurs étiquettes :

1. Les étiquettes sont triées en vue de leur évaluation, en fonction de leur position que vous spécifiez dans la stratégie : l’étiquette positionnée en premier a la position la plus basse (la moins sensible) et l’étiquette positionnée en dernier a la position la plus élevée (la plus sensible).

2. L’étiquette la plus sensible est appliquée.
 
3. La dernière sous-étiquette est appliquée.

> [!TIP]
>Pour bénéficier de la meilleure expérience utilisateur possible et pour assurer la continuité des activités, nous vous recommandons de commencer avec la classification recommandée par l’utilisateur plutôt que par la classification automatique. Cette configuration permet à vos utilisateurs d’accepter l’action d’étiquetage ou de protection, ou de modifier ces suggestions si elles ne sont pas adaptées à leur document ou à leur e-mail.

Un exemple d’invite s’affiche lorsque vous configurez une condition d’application d’une étiquette en tant qu’action recommandée, avec un conseil de stratégie personnalisé :

![Détection et recommandations Azure Information Protection](../media/info-protect-recommend-callouts.png)

Dans cet exemple, l’utilisateur peut cliquer sur **Modifier maintenant** pour appliquer l’étiquette recommandée ou remplacer la recommandation en fermant la barre.

## Pour configurer la classification automatique ou recommandée pour une étiquette

1. Si vous ne l’avez pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, sélectionnez l’étiquette que vous souhaitez configurer pour la classification automatique ou recommandée.

3. Dans le panneau **Étiquette**, dans la section **Configurer des conditions pour appliquer automatiquement cette étiquette**, cliquez sur **Ajouter une condition**.

4. Dans le panneau **Condition**, sélectionnez **Intégré** si vous souhaitez utiliser une condition prédéfinie, ou **Personnalisé** si vous souhaitez spécifier votre propre condition, puis cliquez sur **Enregistrer** :

    - Pour **Intégré** : faites votre sélection dans la liste des conditions disponibles, puis sélectionnez le nombre minimal d’occurrences et déterminez si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
        Pour obtenir plus d’informations sur les règles de détection pour ces conditions et des exemples, consultez la section [Informations sur les conditions intégrées](#information-about-the-built-in-conditions).

    - Pour **Personnalisé** : spécifiez un nom et une expression pour la correspondance, sans guillemets ni caractères spéciaux. Spécifiez ensuite s’il s’agit d’une expression régulière, si la casse doit être respectée, le nombre minimal d’occurrences, et si l’occurrence doit avoir une valeur unique pour être incluse dans le nombre d’occurrences.
        
    **Exemple d’options occurrences** : vous sélectionnez l’option de numéro de sécurité sociale intégrée et définissez le nombre minimal d’occurrences sur 2, et si le même numéro de sécurité sociale est répertorié deux fois dans un document : si vous définissez **Compter les occurrences avec des valeurs uniques uniquement** sur **Activé**, la condition n’est pas remplie. Si vous définissez cette option sur **Désactivé**, la condition est remplie.

5. Dans le panneau **Étiquette**, configurez les options suivantes, puis cliquez sur **Enregistrer** :

    - Choisissez la classification automatique ou recommandée : pour l’option **Sélectionner comment cette étiquette est appliquée : automatiquement ou recommandée à l’utilisateur**, sélectionnez **Automatique** ou **Recommandée**.

    - Spécifiez le texte de l’invite utilisateur ou du conseil de stratégie : conservez le texte par défaut ou spécifiez votre propre chaîne.

6. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Informations sur les conditions intégrées

Pendant la période d’évaluation, vous pouvez sélectionner les conditions suivantes :

- [Code SWIFT](#swift-code )

- [Numéro de carte de crédit](#credit-card-number )

- [Numéro d’acheminement ABA](#aba-routing-number )

- [Numéro de sécurité sociale (SSN) (USA)](#usa-social-security-number-ssn)

- [Numéro de compte bancaire international (IBAN)](#international-banking-account-number-iban)


### Code SWIFT

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


### Numéro de carte de crédit

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

### Numéro d’acheminement ABA

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

### Numéro de sécurité sociale (SSN) (USA)

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

### Numéro de compte bancaire international (IBAN)

Faire correspondre ce type d’information lorsque le contenu inclut les éléments suivants :  

1. L’expression suivante : **IBAN** 

2. Un numéro IBAN : commence par un code de pays (deux lettres), suivi par des chiffres de contrôle (deux chiffres), puis par un numéro IBAN (jusqu’à 30 chiffres).


Exemples de test :

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  






<!--HONumber=Aug16_HO4-->


