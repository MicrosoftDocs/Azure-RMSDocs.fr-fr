---
title: Tutoriel - Migration depuis le client classique Azure Information Protection (AIP) vers la solution d’étiquetage unifié
description: Tutoriel pas à pas pour la migration depuis le client classique Azure Information Protection (AIP) vers le client d’étiquetage unifié.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/19/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 177c877cc1963d40be336bf8ec979a03b7e890c1
ms.sourcegitcommit: e8e4ca39278f1557e14cc8586fe357d8ebce2072
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240833"
---
# <a name="tutorial-migrating-from-the-azure-information-protection-aip-classic-client-to-unified-labeling-solution"></a>Tutoriel : Migration depuis le client classique Azure Information Protection (AIP) vers la solution d’étiquetage unifié

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Concerne** : [Client classique Azure Information Protection pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Pour fournir une expérience client unifiée et homogène, le client classique Azure Information Protection client et la gestion des étiquettes dans le portail Azure seront dépréciés à compter du 31 mars 2021.
> 
> Ce laps de temps permet à toutes les organisations utilisant actuellement le client Azure Information Protection de passer à l’étiquetage unifié AIP, qui utilise la solution d’étiquetage unifié de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>

Ce tutoriel explique comment migrer le déploiement Azure Information Protection de votre organisation à partir du client classique, ainsi que la gestion des étiquettes/stratégies d’étiquette dans le portail Azure, vers la solution d’étiquetage unifié et les [étiquettes de sensibilité Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

**Temps nécessaire** : Le temps nécessaire pour effectuer une migration dépend de la complexité de vos stratégies et des fonctionnalités AIP que vous utilisez. Vous pouvez continuer à travailler avec le client classique pendant que vous effectuez la migration en arrière-plan.

Ce tutoriel fournit une description générale de chaque étape, puis référence la section appropriée qui se trouve ailleurs dans la documentation Microsoft et qui donne plus d’informations.

Dans ce didacticiel, vous allez :
> [!div class="checklist"]
> * Découvrir comment planifier votre migration
> * Migrer vos étiquettes vers la plateforme d’étiquetage unifié
> * Découvrir comment configurer des paramètres avancés dans votre nouveau Centre d’administration d’étiquetage
> * Copier vos stratégies vers la plateforme d’étiquetage unifié
> * Déployer le client d’étiquetage unifié

## <a name="why-migrate-to-the-unified-labeling-solution"></a>Pourquoi migrer vers la solution d’étiquetage unifié ?

En plus de la [dépréciation planifiée du client classique](https://aka.ms/aipclassicsunset), la migration vers la solution d’étiquetage unifié vous permet de protéger efficacement les données sensibles dans votre patrimoine numérique. Une fois que vous avez effectué la migration, utilisez Microsoft Information Protection (MIP) dans les services cloud Microsoft 365, localement, dans des applications SaaS de tiers, etc.

MIP prend en charge les services d’étiquetage intégrés pour de nombreuses fonctionnalités basiques de protection des informations, ce qui vous permet de réserver l’utilisation du client seulement pour les fonctionnalités supplémentaires non prises en charge par l’étiquetage intégré.

- **Réduisez les coûts de maintenance** en déployant et en conservant moins de logiciels supplémentaires
- **Améliorez les performances d’Office** sans avoir besoin d’autres compléments
- **Rationalisez votre gestion des stratégies de protection et d’étiquetage** dans AIP, Office 365 et Windows en utilisant votre Centre d’administration d’étiquetage. 

    Les centres d’administration pris en charge incluent le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité Microsoft 365.

Pour plus d’informations, consultez le [blog Understanding Unified Labeling migration](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185).

## <a name="planning-your-migration"></a>Planification de votre migration

Si la plupart des fonctionnalités disponibles pour le client classique AIP sont également disponibles pour le client d’étiquetage unifié, certaines fonctionnalités ne sont pas encore entièrement disponibles et d’autres sont configurées différemment pour l’étiquetage unifié.

Consultez les articles suivants pour comprendre comment les fonctionnalités Information Protection que vous utilisez peuvent différer lors de l’utilisation du client d’étiquetage unifié :

- [En savoir plus sur les fonctionnalités d’étiquetage intégrées dans Microsoft 365](/microsoft-365/compliance/sensitivity-labels-office-apps)
- [Comparer les solutions d’étiquetage pour les ordinateurs Windows](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [Découvrir comment gérer les paramètres d’étiquette qui ne sont pas pris en charge d’origine dans les centres d’administration d’étiquetage unifié](configure-policy-migrate-labels.md#label-settings-that-are-not-supported-in-the-admin-centers)

> [!TIP]
> S’il existe des différences documentées entre les clients qui ont un impact sur le comportement de vos utilisateurs finaux, nous vous recommandons de bien communiquer ces changements à vos utilisateurs avant de déployer le client d’étiquetage unifié et de publier votre nouvelle stratégie.

Une fois que vous avez planifié votre migration et compris les changements qui vont se produire, poursuivez avec [Migration des étiquettes vers la plateforme d’étiquetage unifié](#migrating-labels-to-the-unified-labeling-platform).

## <a name="migrating-labels-to-the-unified-labeling-platform"></a>Migration des étiquettes vers la plateforme d’étiquetage unifié

Une fois que vous avez planifié la migration et pris en compte la façon dont vous allez gérer les différences entre les clients, vous êtes prêt à activer l’étiquetage unifié et à migrer vos étiquettes.

Pendant la migration, vous pouvez continuer à utiliser le client classique AIP et les stratégies dans la zone Azure Information Protection du portail Azure. Les deux clients peuvent fonctionner côte à côte sans aucune configuration supplémentaire.

1. Connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur avec un des rôles suivants :

    - **Administrateur de conformité**
    - **Administrateur des données de conformité**
    - **Administrateur de sécurité**
    - **Administrateur général**
    

1. Dans la zone Azure Information Protection, sous **Gérer** sur la gauche, sélectionnez **Étiquetage unifié**.

    En haut de la page, sélectionnez :::image type="icon" source="media/qs-tutor/activate.PNG" border="false"::: **Activer** pour activer l’étiquetage unifié.

    Vos étiquettes sont copiées depuis Azure Information Protection vers la plateforme d’étiquetage unifié et sont maintenant stockées dans les deux systèmes.

    Ouvrez votre Centre d’administration d’étiquetage pour comparer les étiquettes qui y sont affichées et celles qui apparaissent dans la zone Azure Information Protection. Les deux listes doivent être identiques. Par exemple, lors de la comparaison avec le Centre de sécurité et de conformité Microsoft 365 :

    :::image type="content" source="media/qs-tutor/compare-migrated-labels-small.png" alt-text="Comparer les étiquettes migrées entre le portail Azure et le Centre de sécurité et de conformité" lightbox="media/qs-tutor/compare-migrated-labels.png":::

    > [!NOTE]
    > Si nécessaire, continuez à utiliser les étiquettes dans les deux systèmes jusqu’à la fin de la migration. Pour plus d’informations, consultez [Synchronisation des modifications de l’étiquetage](#synchronizing-labeling-edits).

Poursuivez avec [Copier vos stratégies vers la plateforme d’étiquetage unifié](#copy-policies-to-the-unified-labeling-platform).

### <a name="synchronizing-labeling-edits"></a>Synchronisation des modifications de l’étiquetage

Une fois que vous avez migré vos étiquettes dans votre centre d’administration de l’étiquetage (Centre de sécurité Microsoft 365, Centre de conformité Microsoft 365 ou Centre Sécurité et conformité Microsoft 365), toutes les nouvelles modifications que vous apportez aux étiquettes migrées sur le Portail Azure sont synchronisées automatiquement avec la même étiquette dans le centre d’administration dans une optique d’étiquetage unifié.

Cependant, les modifications apportées aux étiquettes migrées dans votre Centre d’administration ne sont *pas* resynchronisées vers le portail Azure. Si vous effectuez des modifications dans le Centre d’administration et que vous voulez qu’elles soient mises à jour dans le portail Azure, revenez au portail pour publier la mise à jour.

**Pour publier une étiquette mise à jour dans le portail Azure** :

1. Dans la zone Azure Information Protection, sous **Gérer** sur la gauche, sélectionnez **Étiquetage unifié**.

1. Sélectionnez :::image type="icon" source="media/i-publish.PNG" border="false"::: **Publier**. 

> [!NOTE]
> Cette étape est nécessaire uniquement si vous avez apporté des modifications à vos étiquettes migrées dans la plateforme d’étiquetage unifié et que vous avez besoin que ces modifications soient resynchronisées avec le portail Azure. 

### <a name="migrating-labels-via-powershell"></a>Migration d’étiquettes via PowerShell

Vous pouvez également utiliser PowerShell pour migrer vos étiquettes existantes, comme dans le cas d’un environnement GCC High.

Utilisez l’applet de commande [New-Label](/powershell/module/exchange/new-label) pour migrer vos étiquettes de sensibilité existantes.

Par exemple, si votre étiquette de sensibilité a un chiffrement, vous pouvez utiliser l’applet de commande **New-Label** comme suit :

```PowerShell
New-Label -Name 'aipscopetest' -Tooltip 'aipscopetest' -Comment 'admin notes' -DisplayName 'aipscopetest' -Identity 'b342447b-eab9-ea11-8360-001a7dda7113' -EncryptionEnabled $true -EncryptionProtectionType 'template' -EncryptionTemplateId 'a32027d7-ea77-4ba8-b2a9-7101a4e44d89' -EncryptionAipTemplateScopes "['allcompany@labelaction.onmicrosoft.com','admin@labelaction.onmicrosoft.com']"
```

Pour plus d’informations sur l’utilisation des environnements GCC, GCC-High et DoD, consultez la [Description du service Azure Information Protection Premium Government](/enterprise-mobility-security/solutions/ems-aip-premium-govt-service-description#label-migration). 

## <a name="copy-policies-to-the-unified-labeling-platform"></a>Copier les stratégies vers la plateforme d’étiquetage unifié

Copiez les stratégies que vous avez stockées dans le portail Azure et dont vous voulez qu’elles soient disponibles dans la plateforme d’étiquetage unifié.

Cette fonctionnalité est actuellement en PRÉVERSION. Les [Conditions d’utilisation supplémentaires des préversions Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) incluent des conditions légales supplémentaires qui s’appliquent aux fonctionnalités Azure en version bêta, en préversion ou pas encore disponibles dans la version en disponibilité générale.

> [!NOTE]
> La copie des stratégies a certaines limitations. Vous pouvez également commencer à partir de zéro et créer vos stratégies manuellement dans le Centre d’administration d’étiquetage. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).
> 

**Pour copier vos stratégies** : 

1. Prenez en compte les éléments suivants et décidez si vous voulez copier vos stratégies maintenant :

    |Considération  |Description  |
    |---------|---------|
    |**La copie des stratégies copie *toutes*  vos stratégies**     |     La copie des stratégies ne prend pas en charge la copie de stratégies spécifiques uniquement : pour l’instant, c’est toutes vos stratégies ou aucune d’elles.   |
    |**La copie publie automatiquement vos stratégies**     |  La copie de vos stratégies vers le client d’étiquetage unifié les publie automatiquement sur tous les clients pris en charge par l’étiquetage unifié. <br /><br />   **Important** : Ne copiez pas vos stratégies si vous ne voulez pas les publier.     |
    |**La copie remplace les stratégies existantes du même nom**     |   Si une stratégie portant le même nom existe déjà dans votre Centre d’administration, la copie de vos stratégies va remplacer tous les paramètres définis dans cette stratégie.   <br /><br />Toutes les stratégies copiées depuis le portail Azure sont nommées avec la syntaxe suivante : `AIP_<policy name>`.    |
    |**Certains paramètres du client ne sont pas copiés**     | Certains paramètres du client ne sont pas copiés vers la plateforme d’étiquetage unifié et doivent être configurés manuellement après la migration. <br /><br />Pour plus d’informations, consultez [Configuration des options d’étiquetage avancées](#configuring-advanced-labeling-settings).|
    | | |

1. Connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur avec un des rôles suivants :

    - **Administrateur de conformité**
    - **Administrateur des données de conformité**
    - **Administrateur de sécurité**
    - **Administrateur général**


1. Dans la zone Azure Information Protection, sous **Gérer** sur la gauche, sélectionnez **Étiquetage unifié**.

1. Sélectionnez :::image type="icon" source="media/i-copy-policies.PNG" border="false"::: **Copier les stratégies (préversion)** . Toutes les stratégies que vous avez stockées dans le portail Azure sont copiées vers votre Centre d’administration.

    Si des stratégies existent déjà dans le Centre d’administration avec le même nom, elles sont remplacées par les paramètres du portail Azure.

    > [!IMPORTANT]
    > Si vous utilisez actuellement des étiquettes Microsoft Cloud App Security et Azure Information Protection, vérifiez que vous avez publié au moins une stratégie avec un ensemble minimal d’étiquettes sur votre Centre d’administration d’étiquetage, même si la stratégie est limitée à un seul utilisateur. 
    >
    > Cette stratégie est nécessaire pour que Microsoft Cloud App Security identifie toutes les étiquettes dans le Centre d’administration d’étiquetage et les montre dans le portail Microsoft Cloud App Security.

Maintenant que vous avez migré vos étiquettes et vos stratégies, poursuivez avec [Configuration des paramètres d’étiquetage avancés](#configuring-advanced-labeling-settings) pour couvrir toutes les configurations avancées qui n’ont pas été migrées.

## <a name="configuring-advanced-labeling-settings"></a>Configuration des paramètres d’étiquetage avancés

Comme expliqué dans la [phase de planification](#planning-your-migration), certains paramètres d’étiquetage avancés ne sont pas migrés automatiquement et doivent être reconfigurés pour la plateforme d’étiquetage unifié.

Pour plus d’informations, consultez :

- [Configurer les paramètres d’étiquetage avancés dans PowerShell](#configure-advanced-labeling-settings-in-powershell)
- [Définir des conditions d’étiquette dans le Centre d’administration d’étiquetage](#define-label-conditions-in-the-labeling-admin-center)

### <a name="configure-advanced-labeling-settings-in-powershell"></a>Configurer les paramètres d’étiquetage avancés dans PowerShell

1. Connectez-vous au module Centre de sécurité et de conformité Office 365 de PowerShell. Pour plus d’informations, consultez la [documentation du Centre de sécurité et de conformité de PowerShell](/powershell/exchange/connect-to-scc-powershell).

1. Pour définir un paramètre d’étiquette avancé, utilisez l’applet de commande **Set-Label**, en spécifiant le paramètre **AdvancedSettings**, l’étiquette à laquelle vous voulez appliquer le paramètre et les paires clé/valeur pour définir votre paramètre.
    
    Utilisez la syntaxe suivante :

    ```PowerShell
    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{<Key>="<value1>,<value2>"}
    ```

    Où :
    - **`<LabelGUIDorName>`** identifie votre étiquette en utilisant le nom ou le GUID de l’étiquette
    - **`<Key>`** est la clé ou le nom du paramètre avancé que vous voulez définir
    - **`<Value>`** est la valeur du paramètre que vous voulez définir. Entourez votre valeur de guillemets et séparez les valeurs multiples par des virgules. Les espaces ne sont pas pris en charge.

1. Commencez par configurer les paramètres avancés suivants :

    - [Spécifier une couleur pour l’étiquette](rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)
    - [Spécifier une sous-étiquette par défaut pour une étiquette parent](rms-client/clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Configurer une étiquette pour appliquer la protection S/MIME dans Outlook](rms-client/clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Définir des étiquettes en utilisant des propriétés personnalisées](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions) 
    - [Définir des traductions d’étiquette](/powershell/module/exchange/set-label). 

    Pour plus d’informations sur les configurations avancées disponibles, consultez [Guide de l’administrateur : Configurations personnalisées pour le client d’étiquetage unifié Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).

> [!NOTE]
> Pour tirer parti des paramètres que vous avez définis pour la plateforme d’étiquetage unifié, les utilisateurs finaux doivent avoir le client d’étiquetage unifié installé sur leur machine. 
>
> Ces paramètres avancés ne sont pas disponibles pour les utilisateurs qui ont seulement l’étiquetage intégré fourni par Office 365.
> 

### <a name="define-label-conditions-in-the-labeling-admin-center"></a>Définir des conditions d’étiquette dans le Centre d’administration d’étiquetage

Les conditions de l’étiquetage unifié offrent une plus grande flexibilité et une meilleure précision que leurs équivalents qui ont été créés dans le portail Azure. 

Pour tirer parti des fonctionnalités des conditions de l’étiquetage unifié, créez vos conditions d’étiquetage manuellement dans votre Centre d’administration d’étiquetage, y compris :

- Centre de conformité Microsoft 365
- Centre de sécurité Microsoft 365
- Centre de sécurité et de conformité Microsoft 365

Pour plus d’informations, consultez [Ce que peuvent faire les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) dans la documentation Microsoft 365.

> [!TIP]
> Si vous avez créé des types d’informations sensibles personnalisés pour une utilisation avec Office 365 DLP ou Microsoft Cloud App Security, appliquez-les en l’état à l’étiquetage unifié. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/apply-sensitivity-label-automatically).
>  

## <a name="deploy-a-unified-labeling-client"></a>Déployer un client d’étiquetage unifié

Déployez un client qui prend en charge l’étiquetage unifié sur les machines de vos utilisateurs pour faire en sorte qu’ils puissent utiliser vos étiquettes et vos stratégies d’étiquetage unifié. 

Les utilisateurs doivent disposer d’un client pris en charge qui peut se connecter à votre Centre d’administration d’étiquetage et extraire la stratégie d’étiquetage unifié. 

Pour plus d’informations, consultez :
- [Plateformes non-Windows](#non-windows-platforms)
- [Windows (plateformes)](#windows-platforms)
- [Qu’est-ce qui change pour les utilisateurs finaux du client classique ?](#what-changes-for-classic-client-end-users)

### <a name="non-windows-platforms"></a>Plateformes non-Windows

Pour les utilisateurs sur des plateformes non-Windows, les fonctionnalités d’étiquetage unifié sont intégrées directement dans les clients Office, qui peuvent utiliser immédiatement les étiquettes que vous avez publiées. 

Les clients Office avec des fonctionnalités d’étiquetage unifié intégrées sont les suivants : 

- Clients Office pour macOS
- Office pour le web (préversion)
- Outlook Web App
- Outlook pour mobile

Pour plus d’informations sur l’étiquetage unifié dans ces plateformes, consultez [Appliquer des étiquettes de sensibilité à vos fichiers et à votre courrier électronique dans Office](https://support.microsoft.com/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) sur le site de support technique Microsoft. 

### <a name="windows-platforms"></a>Windows (plateformes)

Pour les machines Windows avec Microsoft 365 Apps for Enterprise, utilisez la prise en charge intégrée de l’étiquetage fournie dans les versions d’Office 1910 et ultérieures, ou installez le client d’étiquetage unifié Azure Information Protection pour étendre les fonctionnalités d’AIP à l’Explorateur de fichiers ou à PowerShell.

Pour plus d’informations, consultez : 

- [Comparer les solutions d’étiquetage pour les ordinateurs Windows](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [Démarrage rapide : Déploiement du client d’étiquetage unifié Azure Information Protection (AIP)](quickstart-deploy-client.md)

Vous pouvez télécharger le client d’étiquetage unifié Azure Information Protection depuis le [Centre de téléchargement Microsoft](https://aka.ms/aipclient). 

Veillez à utiliser le fichier **AzInfoProtection_UL** pour déployer le client. Si le client classique est actuellement installé sur votre machine, l’installation du client d’étiquetage unifié effectue une mise à niveau sur place.

> [!NOTE]
> Prenez en compte les fonctionnalités AIP actuellement requises par votre organisation pour déterminer quand utiliser l’étiquetage intégré et quand utiliser le client d’étiquetage unifié. 
>> 

### <a name="what-changes-for-classic-client-end-users"></a>Qu’est-ce qui change pour les utilisateurs finaux du client classique ?

La différence principale et la plus visible pour les utilisateurs finaux qui utilisaient le client classique Azure Information Protection est que le bouton **Protéger** dans les applications Office est remplacé par le bouton **Sensibilité**. 

Quand vous tirez parti des fonctionnalités supplémentaires prises en charge par les étiquettes de sensibilité et l’étiquetage unifié, les utilisateurs finaux voient également ces modifications dans leurs applications Office.

Exemple :

- **Client classique AIP Windows**

    :::image type="content" source="media/infoprotect-protectbutton-pulldown.png" alt-text="Bouton de protection dans le client classique":::

- **Client d’étiquetage unifié AIP Windows**

    :::image type="content" source="media/qs-tutor/sample-aip-client-office.PNG" alt-text="Exemple de bouton pour le client d’étiquetage unifié dans Microsoft Office":::

> [!TIP]
> Si vous avez publié vos étiquettes et que les clients qui ont la prise en charge intégrée ne montrent pas le bouton **Sensibilité**, consultez le guide de dépannage approprié.
>
 
## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez migré vos étiquettes et vos stratégies, et que vos clients sont déployés selon les besoins, poursuivez en [gérant les étiquettes et les stratégies d’étiquetage uniquement dans le Centre d’administration d’étiquetage](/microsoft-365/compliance/create-sensitivity-labels), notamment le Centre de conformité Microsoft 365, le Centre de sécurité Microsoft 365 ou le Centre de sécurité et de conformité Microsoft 365.

Avec la plateforme d’étiquetage unifié, vous devez revenir à la zone Azure Information Protection du portail Azure seulement pour :

- [Utiliser le scanneur AIP](deploy-aip-scanner.md)
- [Superviser les activités d’étiquetage en utilisant l’analytique AIP](reports-aip.md)

Nous recommandons aux utilisateurs finaux d’utiliser les fonctionnalités d’étiquetage intégrées dans les applications Office les plus récentes pour le web, Mac, iOS et Android ainsi que dans Microsoft 365 Apps for Enterprise. 

Pour utiliser des fonctionnalités AIP supplémentaires qui ne sont pas encore prises en charge par l’étiquetage intégré, nous vous recommandons d’utiliser le client d’étiquetage unifié le plus récent pour Windows.