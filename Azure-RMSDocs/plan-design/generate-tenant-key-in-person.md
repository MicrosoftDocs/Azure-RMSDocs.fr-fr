---
title: "Générer et transférer votre clé de locataire en personne | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 8e77298121a84f6feb16a992da81bd9c3bb7b20b


---

# Générer et transférer votre clé de locataire en personne

*S’applique à : Azure Rights Management, Office 365*


Appliquez les procédures de cette section si vous avez décidé de [gérer votre propre clé de locataire](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok) et que vous ne voulez pas la transférer par le biais d’Internet, mais plutôt la transférer en personne.

## Génération de la clé de locataire
Pour générer votre propre clé de locataire, suivez ces 3 étapes :

-   [Étape 1 : préparation d'un poste de travail avec un module de sécurité matériel Thales](#step-1-prepare-a-workstation-with-thales-hsm)

-   [Étape 2 : création d'un monde de sécurité](#step-2-create-a-security-world)

-   [Étape 3 : création d'une nouvelle clé](#step-3-create-a-new-key)

### Étape 1 : préparation d'un poste de travail avec un module de sécurité matériel Thales
Installez le logiciel de support nCipher (Thales) sur un ordinateur Windows, puis joignez un module de sécurité matériel Thales à cet ordinateur. Vérifiez ensuite que les outils Thales apparaissent dans votre chemin. Pour plus d'informations, reportez-vous au guide d'utilisation inclus avec le module de sécurité matériel Thales, ou visitez le site Web de Thales pour Azure RMS à l'adresse [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Étape 2 : création d'un monde de sécurité
Ouvrez une invite de commande et exécutez le programme de nouveau monde Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Ce programme crée un fichier **Security World** à l’emplacement %NFAST_KMDATA%\local\world, qui correspond au dossier C:\ProgramData\nCipher\Key Management Data\local. Vous pouvez utiliser différentes valeurs pour le quorum mais, dans notre exemple, vous êtes invité à entrer trois cartes et codes confidentiels nuls pour chacun. Ainsi, toute association de deux cartes offrira un accès intégral au monde de sécurité.  Ces cartes constituent l' **ensemble de cartes administrateur** du nouveau monde de sécurité.

Ensuite, procédez comme suit :

1.  Installez le fournisseur Thales CNG tel que décrit dans la documentation Thales et configurez-le pour utiliser le nouveau monde de sécurité.

2.  Sauvegardez le fichier de monde. Sécurisez et protégez ensuite le fichier de monde, les cartes administrateur et leurs codes confidentiels. Veillez à ce que personne n'ait accès à plus d'une carte.

Vous pouvez à présent créer une clé qui sera votre clé de locataire RMS.

### Étape 3 : création d'une nouvelle clé
Générez une clé CNG à l'aide des programmes Thales **generatekey** et **cngimport** .

Exécutez la commande suivante pour générer la clé :

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Tenez compte des instructions suivantes pour l'exécution de cette commande :

-   Le paramètre **protect** doit être défini avec la valeur **module**, comme indiqué. Ceci crée une clé protégée par module. L’ensemble d’outils BYOK ne prend pas en charge les clés protégées par OCS.

-   Nous recommandons la taille de clé 2048, mais les clés RSA 1024 bits sont également prises en charge pour les clients AD RMS existants possédant de telles clés et migrant vers Azure RMS.

-   Remplacez la valeur de *contosokey* pour les paramètres **ident** et **plainname** par une valeur de chaîne. Afin de minimiser la charge administrative et de réduire le risque d'erreurs, nous vous recommandons d'utiliser la même valeur pour les deux et d'utiliser des caractères en minuscules.

-   La zone pubexp est vide (par défaut) dans cet exemple, mais vous pouvez indiquer des valeurs spécifiques. Pour plus d'informations, consultez la documentation Thales.

Exécutez ensuite la commande suivante pour importer la clé dans CNG :

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Tenez compte des instructions suivantes pour l'exécution de cette commande :

-   Remplacez *contosokey* à l'aide de la même valeur que celle indiquée à l'étape 1.

-   Utilisez l’option **-M** afin que la clé convienne pour ce scénario. Dans le cas contraire, la clé résultante sera une clé spécifique à l'utilisateur actuel.

Cette commande crée un fichier de clé tokenisée dans votre dossier %NFAST_KMDATA%\local avec un nom commençant par **key_caping`_`** suivi d’un SID. Par exemple : **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Ce fichier contient une clé chiffrée.

Sauvegardez ce fichier de clé tokénisée à un emplacement sûr.

> [!IMPORTANT]
> Lorsque vous transférerez ultérieurement votre clé à Azure RMS, Microsoft disposera d'une copie non récupérable de votre clé. En d'autres termes, votre clé ne peut être récupérée à partir des modules de sécurité matériels utilisés par Microsoft. Ceci vous permet de garder le contrôle exclusif de votre clé de locataire. Il est donc extrêmement important de sauvegarder votre clé et votre monde de sécurité en lieu sûr. Contactez Thales pour connaître les conseils et meilleures pratiques pour sauvegarder votre clé.

Vous pouvez à présent transférer votre clé de locataire à Azure RMS.

## transfert de votre clé de client vers Azure RMS
Une fois la clé générée, vous devez la transférer à Azure RMS pour pouvoir l'utiliser. Afin de bénéficier d'un niveau de sécurité maximum, ce transfert doit se faire manuellement et nécessite donc que vous vous rendiez au bureau Microsoft de Redmond, Washington (États-Unis). Pour ce faire, suivez ces 3 étapes :

-   [Étape 1 : livraison de la clé à Microsoft](#step-1-bring-your-key-to-microsoft)

-   [Étape 2 : transfert de la clé vers le monde de sécurité Azure RMS](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [Étape 3 : procédures de clôture](#step-3-closing-procedures)

### Étape 1 : livraison de la clé à Microsoft

-   Contactez le support technique de Microsoft afin de fixer un rendez-vous de transfert de clé pour Azure RMS. Veillez à apporter les éléments suivants requis par Microsoft :

    -   un quorum de vos cartes administrateur Si vous avez suivi les instructions fournies à l’ [Étape 2 : création d’un monde de sécurité](#step-2-create-a-security-world), il s’agit de deux de vos trois cartes.

    -   le personnel autorisé à porter vos cartes administrateur et codes confidentiels, généralement deux (un pour chaque carte) ;

    -   votre fichier Security World (%NFAST_KMDATA%\local\world) sur une clé USB ;

    -   votre fichier de clé tokénisée sur une clé USB.

### Étape 2 : transfert de la clé vers le monde de sécurité Azure RMS

1.  Lors de votre arrivée chez Microsoft, procédez comme suit :

    -   Microsoft vous fournit un poste de travail hors ligne disposant d'un module de sécurité matériel Thales joint, du logiciel Thales installé et d'un fichier Azure RMS Security World préchargé dans le dossier C:\Temp\Destination.

    -   Sur ce poste de travail, chargez votre fichier Security World et votre fichier de clé tokénisée à partir de votre clé USB dans le dossier C:\Temp\Source.

    -   Les opérateurs Azure RMS transfèrent en toute sécurité votre clé vers le monde de sécurité Azure RMS grâce aux utilitaires Thales.

    Ce processus sera semblable à ce qui suit, avec le dernier paramètre de key-xfer-im de cet exemple remplacé par le nom de votre fichier de clé tokénisée :

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram vous demandera, ainsi qu'aux opérateurs Azure RMS, de connecter vos cartes administrateur et codes confidentiels respectifs. Ces commandes génèrent un fichier de clé tokénisée dans le répertoire C:\Temp\Destination, contenant votre clé protégée par le monde de sécurité Azure RMS.

### Étape 3 : procédures de clôture

-   En votre présence, les opérateurs Azure RMS doivent procéder comme suit :

    -   Ils exécutent un outil développé par Microsoft en collaboration avec Thales, qui supprime deux autorisations : celle permettant de récupérer la clé et celle permettant de modifier les autorisations. Une fois cette action effectuée, la copie de votre clé est verrouillée dans le monde de sécurité Azure RMS. Les modules de sécurité matériels Thales ne permettront pas aux opérateurs Azure RMS dotés de leurs cartes administrateur de récupérer la copie de texte en clair de votre clé.

    -   Ils copient le fichier de clé résultant sur une clé USB à des fins de transfert ultérieur au service Azure RMS.

    -   Ils rétablissent les paramètres d'usine du module de sécurité matériel et nettoient le poste de travail.

Vous avez à présent effectué toutes les instructions nécessaires pour transférer votre propre clé en personne et pouvez revenir à votre organisation pour les étapes suivantes, qui consistent à planifier et à implémenter votre clé de locataire.

> [!div class="button"]
[Étapes suivantes >>](plan-implement-tenant-key.md#next-steps)






<!--HONumber=Jul16_HO3-->


