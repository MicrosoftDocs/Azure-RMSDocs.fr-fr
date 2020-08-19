---
title: Notes de publication pour le kit de développement logiciel (SDK) Rights Management Services v4. x
description: Découvrez les nouveautés et les notes de publication du kit de développement logiciel (SDK) Microsoft Rights Management Service v4. x juillet 2017 et versions antérieures.
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: has-adal-ref
ms.openlocfilehash: 010ed1f194fd29a9d5e371c296adae5e1e216bea
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563788"
---
# <a name="whats-new-and-release-notes"></a>Nouveautés et notes de publication

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

## <a name="whats-new"></a>Nouveautés

Cette rubrique décrit les modifications et les fonctionnalités importantes de cette nouvelle version de la kit de développement logiciel (SDK) RMS v4. x.

-   [Nouveautés de juillet 2017](#new-for-july-2017)
-   [Mise à jour d’octobre 2016](#october-2016-update)
-   [Mise à jour de juin 2016](#june-2016-update)
-   [Mise à jour de décembre 2015](#december-2015-update)
-   [Mise à jour de juillet 2015 : ajout de la prise en charge du développement Linux/C++](#july-2015-update---adds-support-for-linux--c-development)
-   [Mise à jour de mai 2015-ajout du contrôle d’enregistrement](#may-2015-update---adds-logging-control)
-   [Mise à jour de février 2015 : ajout de la prise en charge de l’application Windows Store](#february-2015-update---adds-windows-store-application-support)
-   [Mise à jour de janvier 2015 : ajout de la prise en charge de la plateforme WinPhone](#january-2015-update---adds-winphone-platform-support)
-   [Mise à jour d’octobre 2014 : mise à niveau vers le kit de développement logiciel (SDK) Microsoft RMS 4.1](#october-2014-update---upgrade-to-microsoft-rms-sdk-41)
-   [Notes de publication](#release-notes)
-   [Forum Aux Questions](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>Nouveautés de juillet 2017

La mise à jour de la version de juillet incluait l’incrémentation de la révision du kit de développement logiciel (SDK), actuellement nommé 4.2.5.

- Android SDK : votre application peut désormais **définir le niveau d’enregistrement à la volée** avec Android SDK. Pour plus d’informations, consultez [Comment : activer la journalisation des erreurs et des performances](https://docs.microsoft.com/information-protection/develop/enabling-logging)
- Le kit de développement logiciel (SDK) iOS ne prend pas en charge le niveau d’enregistrement.
- Le kit de développement logiciel (SDK) retourne désormais une erreur pour un jeton d’accès de valeur NULL.

### <a name="october-2016-update"></a>Mise à jour d’octobre 2016

- Implémentation de quelques correctifs de bogues back-end.
- Activation de Bitcode pour le kit de développement logiciel (SDK) Apple iOS/OSX.

### <a name="june-2016-update"></a>Mise à jour de juin 2016

- **Prise en charge de l’authentification moderne** : introduit la connexion ADAL (Active Directory Authentication Library) dans les applications compatibles avec RMS. Cette mise à jour active les fonctionnalités de connexion telles que Multi-Factor Authentication (MFA), les fournisseurs d’identité tiers SAML avec des applications clientes RMS, mais aussi l’authentification par carte à puce et basée sur un certificat, et elle élimine la nécessité pour les applications compatibles avec RMS d’utiliser le protocole d’authentification de base.
- **Prise en charge du suivi des documents** : les développeurs peuvent désormais activer le suivi des documents lors de la protection des documents dans leurs applications
- Optimisation des performances
- Résolution des bogues

### <a name="december-2015-update"></a>Mise à jour de décembre 2015

Avec cette version, le kit de développement logiciel (SDK) RMS pour les appareils est désormais disponible dans la version 4.2 et ajoute :

-   le suivi des documents, RMS On-line uniquement, pour les systèmes d’exploitation iOS/OS X et Android.

    Pour plus d’informations et de conseils d’utilisation sur iOS/OS X, consultez la classe [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) qui fournit des informations de suivi et la méthode d’enregistrement de suivi des documents supplémentaire sur [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx). Des ajouts similaires ont été effectués pour [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) et [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) sur Android.

    Pour obtenir une description détaillée de la fonctionnalité de suivi des documents, consultez [Procédure : utilisation du suivi des documents](how-to-use-document-tracking.md).

-   Ensemble de méthodes synchrones parallèles aux versions asynchrones de l’API Android :

    [Méthode synchrone CustomProtectedInputStream.create](https://msdn.microsoft.com/library/mt631362.aspx)

    [Méthode synchrone CustomProtectedOutputStream.create](https://msdn.microsoft.com/library/mt631363.aspx)

    [Méthode synchrone ProtectedFileInputStream.create](https://msdn.microsoft.com/library/mt631375.aspx)

    [Méthode synchrone ProtectedFileOutputStream.create](https://msdn.microsoft.com/library/mt631376.aspx)

    [Méthode synchrone TemplateDescriptor.getTemplates](https://msdn.microsoft.com/library/mt631380.aspx)

    [Méthode synchrone UserPolicy.acquire](https://msdn.microsoft.com/library/mt631384.aspx)

    [Méthode synchrone UserPolicy.create (PolicyDescriptor…)**](https://msdn.microsoft.com/library/mt631385.aspx)

    [Méthode synchrone UserPolicy.create (TemplateDescriptor…)](https://msdn.microsoft.com/library/mt631386.aspx)

-   Une nouvelle classe [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) a été ajoutée à l’API Android.
-   Mises à jour visant à améliorer les messages d’erreur et l’expérience de dépannage.
-   Améliorations significatives des performances pour les opérations de chiffrement.

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>Mise à jour de juillet 2015 : ajout de la prise en charge du développement Linux/C++

Cette version ajoute les mises à jour suivantes :

-   Kit de développement logiciel (SDK) RMS 4.1 pour les plateformes Linux

    Pour plus d’informations, consultez [Prise en main](get-started.md).

### <a name="may-2015-update---adds-logging-control"></a>Mise à jour de mai 2015 : ajout du contrôle d’enregistrement

Cette version ajoute la prise en charge pour les mises à jour suivantes :

-   iOS

    Le chiffrement et le déchiffrement des applications peuvent fonctionner de manière indépendante et en parallèle.

    Pour plus d’informations, consultez [MSProtector](https://msdn.microsoft.com/library/mt210993.aspx).

    Paramètres de contrôle d’enregistrement activés.

    Pour plus d’informations, consultez [Comment : activer la journalisation des erreurs et des performances](enabling-logging.md)

    Ajout de la prise en charge de l’effacement du cache.

    Pour plus d’informations, consultez [MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx).

### <a name="february-2015-update---adds-windows-store-application-support"></a>Mise à jour de février 2015 : ajout de la prise en charge de l’application Windows Store

Cette version ajoute la prise en charge des applications du Windows Store et assure la parité fonctionnelle avec la version Windows Phone, Android et iOS/OS X du kit de développement logiciel (SDK) RMS 4.1.

### <a name="january-2015-update---adds-winphone-platform-support"></a>Mise à jour de janvier 2015 : ajout de la prise en charge de la plateforme WinPhone

Cette version ajoute la prise en charge du système d’exploitation Windows Phone et assure la parité fonctionnelle avec la version Android et iOS/OS X du kit de développement logiciel (SDK) RMS 4.1.

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>Mise à jour d’octobre 2014 : mise à niveau vers le kit de développement logiciel (SDK) Microsoft RMS 4.1

La version 4.1 du kit de développement logiciel (SDK) RMS ajoute les fonctionnalités suivantes à Google Android et Apple iOS/OS X.

-   Extensions API du kit de développement logiciel (SDK) Android et iOS/OS X pour le traitement du *consentement de l’utilisateur*, ce qui permet à l’utilisateur de confirmer les comportements du kit de développement logiciel (SDK). Actuellement, le suivi des documents et l’accès à des URL de service AD RMS inconnues constituent les types de consentement pris en charge.

    Pour plus d’informations, consultez par exemple la version de l’API Android de l’[interface ConsentCallback](https://msdn.microsoft.com/library/dn833503.aspx).

-   Les systèmes d’exploitation iOS 8 et OS X 10.10 (Yosemite) sont désormais pris en charge. Quelques modifications de nom de propriété requises par Xcode 6 ont également eu lieu.

    Par exemple, MSUserPolicy.name est devenu [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx).

## <a name="release-notes"></a>Notes de publication

Cette section présente des informations sur les versions actuelles et précédentes des API du kit de développement logiciel (SDK) Microsoft Rights Management 4.x que vous souhaitez connaître en tant que développeur.

**Kit de développement logiciel (SDK) AD RMS 4.1 : version en disponibilité globale des plateformes iOS/OS X et Android**

-   **Prise en charge d’AD RMS** : les administrateurs informatiques peuvent utiliser les applications compatibles avec RMS sur des appareils mobiles avec les extensions d’appareil mobile du nouveau serveur AD RMS.
-   **Consommation hors connexion** : les utilisateurs peuvent accéder aux données protégées par RMS hors connexion.
-   **Authentification séparée** : les développeurs peuvent utiliser leur propre bibliothèque d’authentification pour Azure RMS et AD RMS (ou utiliser la [bibliothèque ADAL (Azure AD Authentication Library)](https://MSDN.Microsoft.Com/library/jj573266.aspx) recommandée).
-   **Interface utilisateur séparée** : les développeurs peuvent créer leur propre interface utilisateur pour protéger et utiliser des documents protégés par RMS.
-   **Reconception de l’API** : les développeurs bénéficient désormais d’une API de chiffrement et de déchiffrement simple et transparente, qui assure la cohérence des comportements RMS et de l’expérience utilisateur avec un minimum d’effort.

**S’applique à toutes les plateformes**

-   Les API du kit de développement logiciel (SDK) RMS 4.x ne sont pas *thread-safe*.

**Android**

-   Lorsque vous utilisez un exemple d’application sur un appareil Amazon® Kindle pour afficher les pièces jointes .ptxt, vous devez d’abord télécharger le fichier avant de l’afficher.

    **Solution** : problème connu qui sera traité ultérieurement.

-   Une application qui utilise le kit de développement logiciel (SDK) peut se bloquer si plusieurs instances sont autorisées.

    **Solution** : vérifiez que l’application n’autorise pas les appels de plusieurs instances vers l’API Android.

-   Lorsque j’utilise la méthode [méthode protectedfileoutputstream](https://msdn.microsoft.com/library/dn790855.aspx). Write (tableau d’octets \[ \] , int offset, int length) avec une longueur différente de la valeur *Array. Length* , je ne peux pas consommer le contenu ultérieurement à l’aide du kit de développement logiciel (SDK).

    **Solution** : il s’agit d’un problème connu. Pour l’atténuer, transmettez toujours un tableau *d' \[ \] octets* avec la même valeur de longueur que le paramètre de longueur, ou utilisez la méthode [méthode protectedfileoutputstream](https://msdn.microsoft.com/library/dn790855.aspx). Write (tableau d’octets \[ \] ).

**iOS et OS X**

-   Nos kits de développement logiciel (SDK) iOS et OS X prennent en charge deux dialectes de portugais. Malheureusement, en raison d’un bogue, nous ne prenons pas en charge la première localisation dans son intégralité pour l’instant. En raison de ce bogue, le portugais n’est pas entièrement pris en charge. La plupart du texte est traduit, mais pas l’interface utilisateur.

    1. Portugais

    2. Portugais (Portugal)

**iOS uniquement**

-   Le kit de développement logiciel (SDK) RMS 4.x n’affiche pas l’indicateur d’activité réseau.

    Il s’agit d’un comportement facultatif connu pour iOS selon les indications relatives à l’interface humaine Apple.

**OS X uniquement**

-   Le kit de développement logiciel (SDK) RMS 4.x n’affiche pas l’indicateur d’activité réseau.

    Il s’agit d’un comportement facultatif connu pour OS X selon les indications relatives à l’interface humaine Apple.

-   **Solution** : pour créer une application d’interface multidocument (MDI) à l’aide de notre kit de développement logiciel (SDK) OS X, suivez les instructions ci-après.

    Les méthodes suivantes ne doivent pas être exécutées simultanément. Pour surveiller l’achèvement de l’exécution, utilisez l’approche de bloc d’achèvement comme indiqué.

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**Remarque**    Les applications MDI ne sont pas prises en charge par notre API iOS.

## <a name="frequently-asked-questions"></a>Forum aux questions

**Toutes les plateformes**

**Q** : Je ne vois pas d’interface utilisateur de sélection des **autorisations personnalisées** dans le flux de travail de protection. Pourquoi ?

**R** : Il s’agit d’un problème connu qui sera traité ultérieurement.

**Q** : Comment amener les nouveaux tenants organisationnels à tester le kit de développement logiciel (SDK) et les exemples d’applications ?

**R** : Si vous souhaitez demander des informations d’identification pour les organisations de test Azure AD RMS, envoyez un e-mail à <rmcstbeta@microsoft.com>.

**Q** : Je ne vois aucune discussion relative à la hiérarchie de test dans la documentation. Pourquoi ?

**R** : Le concept de hiérarchie de test n’existe pas dans les nouveaux kits de développement logiciel (SDK) AD RMS. Vous travaillerez toujours avec la hiérarchie de production.

**Q** : Dans la version 2.1 du kit de développement logiciel (SDK) RMS, un manifeste généré était nécessaire pour chaque application implémentant la protection des informations. Est-ce toujours le cas pour la version 4.0 et les versions ultérieures du kit de développement logiciel (SDK) ?

**R** : Non, les manifestes ne sont plus nécessaires pour la version 3.0 et les versions ultérieures du kit de développement logiciel (SDK) Rights Management.

**Android**

**Q** : Avec quels environnements de développement le kit de développement logiciel (SDK) a-t-il été testé ?

**R** : Eclipse Juno avec l’API Google 15 et versions ultérieures.

**Q** : Puis-je appeler cancel(), une méthode d’annulation à partir du thread d’interface utilisateur ?
**R** : Vous devez appeler cancel() à partir d’un thread autre qu’un thread d’interface utilisateur, sous peine de provoquer l’interruption d’une connexion réseau.

**iOS**

**Q** : Quelles plateformes ont été vérifiées pour le développement du kit de développement logiciel (SDK) ?

**R** : Xcode 5.0 avec iOS 7 et versions ultérieures.

**Q** : J’ai appelé une méthode cancel() sur une opération, mais je reçois toujours une notification indiquant que l’opération est terminée. Pourquoi ?

**R** : Toutes les opérations ne peuvent pas être annulées. Les opérations d’annulation sont donc exécutées dans la mesure du possible.

**OS x**

**Q** : L’infrastructure de l’exemple d’application est adaptée à Xcode 5. Puis-je utiliser Xcode 4.6 ?

**R** : Le kit de développement logiciel (SDK) OS X fonctionne avec Xcode 4.6 et versions ultérieures uniquement, tout comme OS X 10.8 et versions ultérieures.
