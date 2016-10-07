---
title: "Nouveautés et notes de publication | Azure RMS"
description: "Décrit les modifications et les fonctionnalités importantes de cette nouvelle version du kit de développement logiciel (SDK) RMS."
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: da4dce1c44cd79e90e7d232f74f194b734dea0f6


---

# Nouveautés et notes de publication

## Nouveautés
Le kit de développement logiciel (SDK) Microsoft Rights Management 4.2 améliore encore le niveau de simplicité et de flexibilité relatives à l’activation de l’application RMS. Ce sujet décrit les modifications et les fonctionnalités importantes de cette nouvelle version du kit de développement logiciel (SDK) RMS.

-   [Nouveau en juin 2016](#new-for-June-2016)
-   [Mise à jour de décembre 2015](#december-2015-update)
-   [Mise à jour de juillet 2015 : ajout de la prise en charge du développement Linux/C++](#july-2015-update-adds-support-for-linux-c-developm)
-   [Mise à jour de mai 2015 : ajout du contrôle d’enregistrement](#may-2015-update-adds-logging-control)
-   [Mise à jour de février 2015 : ajout de la prise en charge des applications du Windows Store](#february-2015-update-adds-windows-store-application-support)
-   [Mise à jour de janvier 2015 : ajout de la prise en charge de la plate-forme WinPhone](#january-2015-update-adds-winphone-platform-support)
-   [Mise à jour d’octobre 2014 : mise à niveau vers le Kit de développement logiciel (SDK) Microsoft RMS 4.1](#october-2014-update-upgrade-to-microsoft-rms-sdk-4-1)
-   [Notes de publication](#release-notes)
-   [Forum aux questions](#frequently-asked-questions)

### Nouveau en juin 2016

- **Prise en charge de l’authentification moderne** : intègre la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library) aux applications compatibles avec RMS. Elle autorise les fonctionnalités de connexion telles que Multi-Factor Authentication (MFA), les fournisseurs d’identité tiers SAML avec les applications clientes RMS, l’authentification basée sur les cartes à puce et les certificats. Grâce à cette prise en charge, il n’est plus nécessaire d’utiliser le protocole d’authentification de base pour les applications compatibles avec RMS.
- **Prise en charge du suivi des documents** : les développeurs peuvent désormais activer le suivi des documents quand ils protègent des documents dans leurs applications. 
- Améliorations apportées aux performances
- Corrections de bogues


### Mise à jour de décembre 2015

Le Kit de développement logiciel (SDK) passe désormais à la version 4.2 et bénéficie des ajouts suivants :

-   Suivi des documents, RMS On-line uniquement, pour systèmes d’exploitation iOS/OS X et Android.

    Pour plus d’informations et de conseils sur iOS/OS X, reportez-vous à la classe [**MSLicenseMetadata**](/information-protection/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) qui fournit des informations de suivi et à la méthode d’enregistrement de suivi des documents supplémentaire sur [**MSUserPolicy**](/information-protection/sdk/4.2/api/iOS/iOS#msipcthin2_msuserpolicy_interface_objc). Des ajouts similaires ont été effectués pour Android pour [**LicenseMetadata**](/information-protection/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) et [**UserPolicy**](/information-protection/sdk/4.2/api/android/userpolicy).

    Pour obtenir une description détaillée de la fonctionnalité de suivi des documents, voir [**Procédure : utilisation du suivi des documents**](how-to-use-document-tracking.md).

-   Ensemble de méthodes synchrones parallèles aux versions asynchrones de l’API Android :

    [**Méthode synchrone CustomProtectedInputStream.create**](/information-protection/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_create_synchronous_method_java)

    [**Méthode synchrone CustomProtectedOutputStream.create**](/information-protection/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Méthode synchrone ProtectedFileInputStream.create**](/information-protection/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_synchronous_method)

    [**Méthode synchrone ProtectedFileOutputStream.create**](/information-protection/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**Méthode synchrone TemplateDescriptor.getTemplates**](/information-protection/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_gettemplates_synchronous_method_java)

    [**Méthode synchrone UserPolicy.acquire**](/information-protection/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_acquire_synchronous_method_java)

    [**Méthode synchrone UserPolicy.create (PolicyDescriptor...)**](/information-protection/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_policydescriptor_______synchronous_method_java)

    [**Méthode synchrone UserPolicy.create (TempalteDescriptor…...)**](/information-protection/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_templatedescriptor_______synchronous_method_java)

-   Une nouvelle classe [**ProtectedBuffer**](/information-protection/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedbuffer_class) a été ajoutée à l’API Android.
-   Mises à jour pour améliorer les messages d’erreur et le dépannage.
-   Améliorations de performances significatives pour les opérations de chiffrement.

### Mise à jour de juillet 2015 : ajout de la prise en charge du développement Linux/C++

L’élément suivant est ajouté à cette version :

-   Kit de développement logiciel (SDK) RMS 4.1 pour les plateformes Linux

    Pour plus d’informations, consultez [Prise en main](get-started.md).

### Mise à jour de mai 2015 : ajout du contrôle d’enregistrement

Cette version permet la prise en charge des éléments suivants :

-   iOS

    Le chiffrement et le déchiffrement d’une application peuvent fonctionner de manière indépendante et en parallèle.

    Pour plus d’informations, voir [**MSProtector**](/information-protection/sdk/4.2/api/iOS/iOS#msipcthin2_msprotector_class_objc).

    Activation des paramètres de contrôle du niveau de journalisation.

    Pour plus d’informations, voir [Procédure : activation de la journalisation des erreurs et des performances](enabling-logging.md)

    Ajout de la prise en charge de l’effacement du cache.

    Pour plus d’informations, voir [**MSProtection:resetStateWithCompletionBlock**](/information-protection/sdk/4.2/api/iOS/msprotection#msipcthin2_msprotection_resetstatewithcompletionblock_method_objc).

### Mise à jour de février 2015 : ajout de la prise en charge des applications du Windows Store

Cette version ajoute la prise en charge des applications du Windows Store et assure la parité fonctionnelle avec la version Windows Phone, Android et iOS/OS X du kit de développement logiciel (SDK) RMS 4.1.

### Mise à jour de janvier 2015 : ajout de la prise en charge de la plate-forme WinPhone

Cette version ajoute la prise en charge du système d’exploitation Windows Phone et assure la parité fonctionnelle avec la version Android et iOS/OS X du kit de développement logiciel (SDK) RMS 4.1.

### Mise à jour d’octobre 2014 : mise à niveau vers le Kit de développement logiciel (SDK) Microsoft RMS 4.1

La version 4.1 du kit de développement logiciel (SDK) RMS ajoute les nouvelles fonctionnalités suivantes aux systèmes d’exploitation Google Android et Apple iOS/OS X.

-   Extensions de l’API du kit de développement logiciel (SDK) Android et iOS/OS X pour le traitement du *consentement de l’utilisateur* pour permettre à l’utilisateur de confirmer les comportements du kit de développement logiciel. Actuellement, le suivi des documents et l’accès à des URL de service AD RMS inconnues sont les types de consentements pris en charge.

    Pour plus d’informations, consultez à titre d’exemple, la version de l’API Android de l’[**interface ConsentCallback**](/information-protection/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_consentcallback_interface_java).

-   Les systèmes d’exploitation iOS 8 et OS X 10.10 (Yosemite) sont désormais pris en charge. Quelques modifications de noms de propriétés requises par Xcode 6 ont également eu lieu.

    Exemple : modification de MSUserPolicy.name en [**MSUserPolicy.policyName**](/information-protection/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_name_property_objc).

## Notes de publication

Cette section donne des informations sur les versions actuelles et précédentes du kit de développement logiciel (SDK) Microsoft Rights Management 4.x que vous souhaitez connaître en tant que développeur.

**Kit de développement logiciel (SDK) AD RMS 4.1 - Version en disponibilité globale des plateformes iOS/OS X et Android**

-   **Prise en charge d’AD RMS** : les administrateurs informatiques peuvent utiliser des applications compatibles avec RMS sur des appareils mobiles avec les nouvelles extensions pour appareils mobiles du serveur AD RMS.
-   **Consommation en mode hors connexion** : les utilisateurs finaux peuvent accéder hors connexion aux données protégées par RMS.
-   **Authentification séparée** : les développeurs peuvent utiliser leur propre bibliothèque d’authentification pour Azure RMS et AD RMS (ou utiliser la [bibliothèque d’authentification Azure AD (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx)).
-   **Interface utilisateur séparée** : les développeurs peuvent créer leur interface utilisateur afin de protéger et d’utiliser des documents protégés par RMS.
-   **Reconception de l’API** : les développeurs peuvent bénéficier désormais d’une API de chiffrement et de déchiffrement, qui assure la cohérence des comportements RMS et de l’expérience utilisateur avec un minimum d’effort.

**Commun à toutes les plates-formes**

-   Les API du Kit de développement logiciel (SDK) RMS 4.x ne sont pas *thread-safe*.

**Android**

-   Lorsque vous utilisez un exemple d’application sur un appareil Amazon® Kindle pour afficher des pièces jointes .ptxt, vous devez d’abord télécharger le fichier avant de l’afficher.

    **Solution** : il s’agit d’un problème connu qui sera traité ultérieurement.

-   Une application qui utilise le kit de développement logiciel peut se bloquer si plusieurs instances sont autorisées.

    **Solution** : vérifiez que l’application n’autorise pas l’appel de plusieurs instances vers l’API Android.

-   Lorsque j’utilise la méthode [**ProtectedFileOutputStream**](/information-protection/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array, int offset, int length)** avec une longueur différente de la valeur *array.length*, je ne suis pas en mesure d’utiliser le contenu ultérieurement à l’aide du SDK.

    **Solution** : il s’agit d’un problème connu. Pour l’atténuer, transmettez toujours un tableau **byte \[\]** ayant la même valeur de longueur que le paramètre de longueur, ou utilisez la méthode [**ProtectedFileOutputStream**](/information-protection/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array)**.

**iOS et OS X**

-   Nos kits de développement logiciel iOS et OS X prennent en charge deux dialectes de Portugais. Malheureusement, en raison d’un bogue, la prise en charge de la première localisation n’est pas complètement assurée. En raison de ce bogue, le portugais n’est pas entièrement pris en charge. La plupart du texte est traduit, mais pas l’interface utilisateur.

    1. Portugais

    2. Portugais (Portugal)

**iOS uniquement**

-   Le kit de développement logiciel (SDK) RMS 4.x n’affiche pas le voyant d’activité réseau.

    Il s’agit d’un comportement facultatif connu pour iOS selon les instructions relatives à l’interface humaine Apple.

**OS X uniquement**

-   Le kit de développement logiciel (SDK) RMS 4.x n’affiche pas le voyant d’activité réseau.

    Il s’agit d’un comportement facultatif connu pour OS X selon les instructions relatives à l’interface humaine Apple.

-   **Solution** : pour créer une application MDI à l’aide de notre kit de développement logiciel (SDK) OS X, utilisez les instructions suivantes.

    Les méthodes suivantes ne doivent pas être exécutées simultanément. Afin de vérifier que l’exécution est terminée, utilisez l’approche de fin comme indiqué.

    - [**protectedDataWithProtectedFile**](/information-protection/sdk/4.2/api/iOS/msprotecteddata#msipcthin2_msprotecteddata_protecteddatawithprotectedfile_completionblock_method_objc)
    - [**customProtectedDataWithPolicy**](/information-protection/sdk/4.2/api/iOS/mscustomprotecteddata#msipcthin2_mscustomprotecteddata_customprotecteddatawithpolicy_protecteddata_contentstartposition_contentsize_completionblock_method_objc)



**Remarque** : les applications MDI ne sont pas prises en charge par notre API iOS.

## Forum aux questions

**Toutes les plateformes**

**Q** : Je ne vois pas d’interface utilisateur de sélection des **autorisations personnalisées** dans le workflow de protection. Pourquoi ?

**R** : Il s’agit d’un problème connu qui sera traité ultérieurement.

**Q** : Comment obtenir de nouveaux locataires d’organisation pour essayer le Kit de développement logiciel (SDK) et les exemples d’applications ?

**R** : Pour demander des informations d’identification pour les organisations de test Azure AD RMS, envoyez un courrier électronique à <rmcstbeta@microsoft.com>.

**Q** : Je ne vois aucune discussion relative à la hiérarchie de test dans la documentation. Pourquoi ?

**R** : Le concept de hiérarchie de test n’existe pas dans les nouveaux kits de développement logiciel (SDK) AD RMS. Vous travaillerez toujours avec la hiérarchie de production.

**R** : Dans la version 2.1 du kit de développement logiciel (SDK) RMS un manifeste généré était nécessaire pour chaque application mettant en œuvre la protection des informations. Est ce toujours vrai pour les versions 4.0 et ultérieures de ce kit de développement logiciel ?

**R** : Non, les manifestes ne sont plus nécessaires pour les versions 3.0 et ultérieures du kit de développement logiciel (SDK) Rights Management.

**Android**

**Q** : Avec quels environnements de développement le kit de développement logiciel a-t-il été testé ?

**R** : Eclipse Juno avec l’API Google 15 et version ultérieure.

**Q** : Puis-je appeler cancel(), une méthode d’annulation à partir du thread d’interface utilisateur ?
**R** : vous devez appeler cancel() à partir d’un thread autre qu’un thread d’interface utilisateur, sous peine de provoquer l’interruption d’une connexion réseau.

**iOS**

**Q** : Quelles plates-formes ont été vérifiées pour le développement du kit de développement logiciel ?

**R** : Xcode 5.0 avec iOS 7 et versions ultérieures.

**Q** : J’ai appelé une méthode cancel() sur une opération, toutefois, j’obtiens toujours la notification m’indiquant que l’opération est terminée. Pourquoi ?

**R** : Toutes les opérations ne peuvent pas être annulées. Une opération d’annulation est exécutée dans les meilleures conditions possible.

**OS X**

**Q** : L’infrastructure de l’exemple d’application est adaptée à Xcode 5. Puis-je travailler avec Xcode 4.6 ?

**R** : Le kit de développement logiciel (SDK) du système d’exploitation OS X fonctionne avec Xcode 4.6 et versions ultérieures uniquement et OS X 10.8 et versions ultérieures.

 

 



<!--HONumber=Sep16_HO5-->


