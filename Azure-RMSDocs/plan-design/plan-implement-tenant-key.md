---
# required metadata

title: Planification et implémentation de la clé de locataire Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planification et implémentation de la clé de locataire Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Utilisez les informations de cet article pour planifier et gérer votre clé de locataire (ou client) Rights Management (RMS) pour Azure RMS. Par exemple, au lieu que Microsoft gère votre clé de locataire (par défaut), vous pouvez gérer votre propre clé de locataire afin de vous conformer à des réglementations spécifiques s'appliquant à votre organisation.  La gestion de votre propre clé de locataire est également appelée BYOK (Bring Your Own Key).

> [!NOTE]
> La clé de locataire RMS est également appelée « clé de certificat de licence serveur » (SLC). Azure RMS gère une ou plusieurs clés pour chaque organisation s'abonnant à Azure RMS. Lorsqu'une clé est utilisée pour RMS au sein d'une organisation (par exemple, clés utilisateur, clés d'ordinateur, clés de chiffrement de document), elle est ajoutée par chiffrement à la clé de locataire RMS.

**Aperçu rapide :** Utilisez le tableau suivant comme guide rapide pour votre topologie de clé de locataire recommandée. Ensuite, utilisez la documentation supplémentaire pour obtenir plus d’informations.

Si vous déployez Azure RMS à l'aide d'une clé de locataire gérée par Microsoft, vous pourrez passer ultérieurement à la solution BYOK. Toutefois, vous ne pouvez pas passer actuellement d'une solution de clé de locataire Azure RMS BYOK à une clé de locataire gérée par Microsoft.

|Besoin de l'entreprise|Topologie de clé de locataire recommandée|
|------------------------|-----------------------------------|
|Déployer Azure RMS rapidement et sans nécessiter un matériel spécial|Géré par Microsoft|
|Besoin de toutes les fonctionnalités IRM dans Exchange Online avec Azure RMS|Géré par Microsoft|
|Vos clés sont créées par vous, et protégées dans un module de sécurité matériel (HSM)|BYOK<br /><br />Actuellement, cette configuration entraîne une réduction des fonctionnalités IRM dans Exchange Online. Pour plus d’informations, consultez la section [Tarifs et restrictions BYOK](byok-price-restrictions.md) .|

## Choix de la topologie de clé de locataire : gestion Microsoft (par défaut) ou gestion BYOK
Choisissez la topologie de clé de locataire la plus adaptée à votre organisation. Par défaut, Azure RMS génère la clé de locataire et gère la plupart des aspects de son cycle de vie. Il s'agit de l'option la plus simple, avec la charge administrative la plus faible. Dans la plupart des cas, les utilisateurs n'ont même pas conscience de l'existence de cette clé de locataire. Il leur suffit de s'inscrire à Azure RMS ; le reste du processus de gestion de la clé est traité par Microsoft.

Mais vous pouvez également souhaiter bénéficier d'un contrôle complet sur votre clé de locataire, ce qui implique la création de votre clé et la conservation de la copie principale en local. Il est souvent fait référence à ce scénario sous le terme « Bring your own key » (BYOK). Cette option implique les étapes suivantes :

1.  Vous générez votre clé de locataire en local, en accord avec vos politiques informatiques.

2.  Vous transférez en toute sécurité la clé de locataire à partir d'un module de sécurité matériel en votre possession vers des modules de sécurité matériels possédés et gérés par Microsoft. Notez que tout au long de ce processus, la clé de locataire ne quitte jamais les limites de protection matérielles.

3.  La clé de locataire reste protégée lors de son transfert à Microsoft grâce à des modules de sécurité matériels Thales. Microsoft a collaboré avec Thales pour s'assurer que votre clé de locataire ne puisse pas être extraite de modules de sécurité matériels de Microsoft.

Bien que cette action soit facultative, vous pouvez également utiliser les journaux d'utilisation quasiment en temps réel à partir d'Azure RMS pour voir exactement quand et comment votre clé de locataire est utilisée.

> [!NOTE]
> À des fins de protection supplémentaires, Azure RMS utilise des mondes de sécurité distincts pour ses centres de données en Amérique du Nord, dans la région EMEA (Europe, Moyen-Orient et Afrique) et en Asie. Lorsque vous gérez votre propre clé de locataire, celle-ci est liée au monde de sécurité de la région d'enregistrement de votre locataire RMS. Par exemple, la clé de locataire d'un client européen ne peut pas être utilisée dans des centres de données en Amérique du Nord ou en Asie.

## Cycle de vie d'une clé de locataire
Si vous choisissez de confier à Microsoft la gestion de votre clé de locataire, Microsoft traite la plupart des aspects de son cycle de vie. Cependant, si vous décidez de gérer vous-même votre clé de locataire, vous êtes responsable d'un grand nombre d'opérations et de certaines procédures supplémentaires.

Les schémas ci-dessous présentent et comparent ces deux options. Le premier schéma permet notamment de juger de la faible charge administrative qui vous incombe dans la configuration par défaut, lorsque Microsoft gère la clé de locataire.

![Cycle de vie de clé de locataire Azure RMS - géré par Microsoft, valeur par défaut](../media/RMS_BYOK_cloud.png)

Le deuxième schéma présente quant à lui les étapes supplémentaires requises lorsque vous gérez votre clé de locataire.

![Cycle de vie de clé de locataire Azure RMS - géré par vous-même, BYOK](../media/RMS_BYOK_onprem.png)

Si vous choisissez de confier à Microsoft la gestion de votre clé de locataire, aucune autre action n’est nécessaire de votre part et vous n’avez pas à générer la clé. Vous pouvez passer directement à la rubrique [Étapes suivantes](plan-implement-tenant-key.md#next-steps).

Si vous décidez de gérer vous-même votre clé de locataire, lisez les sections suivantes pour plus d'informations.

## Implémentation de la clé de locataire Azure Rights Management

Utilisez les informations et les procédures de cette section si vous souhaitez générer et gérer vous-même votre clé de locataire (solution BYOK) :


> [!IMPORTANT]
> Si vous avez déjà commencé à utiliser [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (le service est activé) et que certains de vos utilisateurs exécutent Office 2010, [contactez le support Microsoft](../get-started/information-support#to-contact-microsoft-support) avant d’appliquer ces procédures. Selon votre scénario et vos exigences, vous devrez peut-être appliquer la solution BYOK avec certaines limitations ou étapes supplémentaires.
> 
> Vous pouvez aussi [contacter le support Microsoft](../get-started/information-support#to-contact-microsoft-support) si votre organisation applique des stratégies spécifiques en matière de gestion des clés.

### Conditions requises pour la solution BYOK
Reportez-vous au tableau suivant pour connaître les conditions requises pour la solution Bring your own key (BYOK).

|Condition requise|Plus d'informations|
|---------------|--------------------|
|Abonnement prenant en charge Azure RMS.|Pour plus d’informations sur les abonnements disponibles, consultez [Abonnements au cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md).|
|Vous n'utilisez pas RMS for Individuals ou Exchange Online. Ou, si vous utilisez Exchange Online, vous comprenez et acceptez les limitations liées à l'utilisation de la solution BYOK avec cette configuration.|Pour plus d’informations sur les restrictions et limitations actuelles relatives à la solution BYOK, consultez [Tarifs et restrictions BYOK](byok-price-restrictions.md).<br /><br />**Important** : Actuellement, la solution BYOK n’est pas compatible avec Exchange Online.|
|Module de sécurité matériel Thales, cartes à puce et logiciel de support.<br /><br />**Remarque** : Si vous migrez d’AD RMS vers Azure RMS en passant d’une clé logicielle à une clé matérielle, vous devez disposer au minimum de la version 11.62 pour les pilotes Thales.|Vous devez avoir accès à un module de sécurité matériel Thales et posséder des connaissances de base concernant le fonctionnement de ce type de module. Reportez-vous à la page relative aux [modules de sécurité matériels Thales](http://www.thales-esecurity.com/msrms/buy) pour obtenir la liste des modèles compatibles ou pour acheter un module de sécurité matériel si vous n'en avez pas.|
|Si vous souhaitez transférer votre clé de locataire par Internet au lieu de vous présenter à Redmond, aux États-Unis, vous devez remplir trois conditions :<br /><br />1 : Une station de travail x64 hors connexion dotée au minimum de Windows 7 et du logiciel nShield de Thales version 11.62.<br /><br />Si cette station de travail exécute Windows 7, vous devez [installer Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />2 : Un poste de travail connecté à Internet, doté de Windows 7 au minimum.<br /><br />3 : Une clé USB ou tout autre dispositif de stockage portable avec au moins 16 Mo d’espace libre.|Ces éléments ne sont pas obligatoires si vous vous rendez à Redmond pour transférer votre clé de locataire en personne.<br /><br />Pour des questions de sécurité, il est recommandé que le premier poste de travail ne soit connecté à aucun réseau. Cependant, il ne s'agit pas d'une obligation forcée par programmation.<br /><br />Remarque : Dans les instructions ci-après, cette première station de travail est désignée sous le terme **station de travail déconnectée**.<br /><br />De plus, si votre clé de locataire est destinée à un réseau de production, nous vous recommandons d'utiliser un deuxième poste de travail pour télécharger l'ensemble d'outils et envoyer la clé. Cependant, dans le cadre de tests, vous pouvez utiliser le même poste de travail.<br /><br />Remarque : Dans les instructions ci-après, cette deuxième station de travail est désignée sous le terme **station de travail connectée à Internet**.|

Les procédures de génération et d'utilisation de la clé de locataire varient selon que vous préférez les effectuer par Internet ou en personne :

-   **Par Internet :** cette option implique des étapes de configuration supplémentaires, telles que le téléchargement et l'utilisation d'un ensemble d'outils et d'applets de commande Windows PowerShell. Mais elle présente l'avantage de vous éviter de vous déplacer jusqu'au bureau Microsoft pour pouvoir transférer votre clé de locataire. La sécurité est assurée comme suit :

    -   Vous générez la clé de locataire à partir d'un poste de travail hors ligne, ce qui réduit la surface d'attaque.

    -   La clé de locataire est chiffrée à l'aide d'une clé d'échange de clés, qui reste chiffrée jusqu'à son transfert aux modules de sécurité matériels Azure RMS. Seule une version chiffrée de votre clé de locataire quitte le poste de travail d'origine.

    -   Un outil définit des propriétés sur votre clé de locataire, qui la lient au monde de sécurité Azure RMS. Ainsi, une fois que les modules de sécurité matériels Azure RMS ont reçu et déchiffré votre clé de locataire, seuls ceux-ci peuvent les utiliser. Votre clé de locataire ne peut pas être exportée. Cette liaison est appliquée par les modules de sécurité matériels Thales.

    -   La clé d'échange de clés utilisée pour chiffrer votre clé de locataire est générée au sein des modules de sécurité matériels Azure RMS et n'est pas exportable. Les modules de sécurité matériels veillent à ce qu'il n'existe pas de version claire de la clé d'échange de clés à l'extérieur. De plus, l'ensemble d'outils inclut une attestation de Thales indiquant que la clé d'échange de clés n'est pas exportable et qu'elle a été générée au sein d'un module de sécurité matériel authentique conçu par Thales.

    -   L'ensemble d'outils inclut également une attestation de Thales indiquant que le monde de sécurité Azure RMS a été généré au sein d'un module de sécurité matériel authentique conçu par Thales, cela afin de garantir que Microsoft utilise du matériel authentique.

    -   Microsoft utilise des clés d'échange de clés et des mondes de sécurité distincts pour chaque zone géographique. Ainsi, votre clé de locataire ne peut être utilisée que dans les centres de données de la zone dans laquelle elle a été chiffrée. Par exemple, la clé de locataire d'un client européen ne peut pas être utilisée dans des centres de données en Amérique du Nord ou en Asie.

    > [!NOTE]
    > Votre clé de locataire peut transiter en toute sécurité via des ordinateurs et des réseaux non sécurisés, car elle est chiffrée et sécurisée à l'aide d'autorisations de niveau de contrôle d'accès. Ainsi, elle ne peut être utilisée qu'au sein de vos modules de sécurité matériels et dans ceux de Microsoft pour Azure RMS. Vous pouvez utiliser les scripts de l'ensemble d'outils pour vérifier ces mesures de sécurité. Pour plus d'informations, consultez la documentation Thales relative à la [gestion de clé matérielle dans le cloud RMS](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **En personne :** vous devez [contacter le support Microsoft](../get-started/information-support#to-contact-microsoft-support) pour planifier un rendez-vous de transfert de clé pour Azure RMS. Vous devez en effet vous rendre au bureau Microsoft de Redmond, Washington (États-Unis) pour transférer votre clé de locataire dans le monde de sécurité Azure RMS.

Pour obtenir des instructions, précisez si vous allez générer et transférer votre clé de locataire par Internet ou en personne : 

- [Par Internet](generate-tenant-key-internet.md)
- [En personne](generate-tenant-key-in-person.md)


## Étapes suivantes

Maintenant que vous avez planifié et, le cas échéant, généré votre clé de locataire, procédez comme suit :

1.  Commencez à utiliser votre clé de locataire :

    -   Si ce n'est déjà fait, vous devez maintenant activer Rights Management pour que votre organisation puisse utiliser RMS. Les utilisateurs peuvent exploiter immédiatement la clé de locataire (gérée par Microsoft ou par vous).

        Pour plus d’informations sur l’activation, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

    -   Si vous avez déjà activé Rights Management et avez décidé de gérer vous-même vote clé de locataire, les utilisateurs passent graduellement de l'ancienne clé de locataire à la nouvelle. Cette transition progressive s'effectue en quelques semaines. Les documents et fichiers protégés par l'ancienne clé de locataire restent accessibles pour les utilisateurs autorisés.

2.  Envisagez l’activation de la journalisation de l’utilisation, qui consigne chaque transaction effectuée par RMS.

    Si vous avez décidé de gérer vous-même votre clé de locataire, la journalisation inclut des informations utiles sur son utilisation. Consultez l'exemple suivant de fichier journal affiché dans Excel, où les types de requête **Decrypt** et **SignDigest** montrent que la clé de locataire est utilisée.

    ![fichier journal dans Excel où la clé de locataire est utilisée](../media/RMS_Logging.gif)

    Pour plus d’informations sur la journalisation de l’utilisation, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Gérez votre clé de locataire.

    Pour plus d’informations, consultez [Opérations pour votre clé de locataire Azure Rights Management](../deploy-use/operations-tenant-key.md).



<!--HONumber=Jun16_HO2-->


