---
title: Utiliser PowerShell avec le client d’étiquetage unifié Azure Information Protection
description: Instructions et informations permettant aux administrateurs de gérer le Azure Information Protection client d’étiquetage unifié à l’aide de PowerShell.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/14/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a0fe31a92d97ebacf8ab0fed45198086079051fa
ms.sourcegitcommit: 5e5631e03959034f37705b4f61aead3d35e8cd8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2021
ms.locfileid: "98540188"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guide de l’administrateur : utilisation de PowerShell avec le client unifié Azure Information Protection

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP pour Windows et les versions d’Office dans support étendu](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support).*
>
>***Concerne :** [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez le [Guide d’administration du client classique](client-admin-guide-powershell.md). *

Lorsque vous installez le client d’étiquetage unifié Azure Information Protection, les commandes PowerShell sont installées automatiquement dans le cadre du module [AzureInformationProtection](/powershell/module/azureinformationprotection) , avec des applets de commande pour l’étiquetage. 

Le module **AzureInformationProtection** vous permet de gérer le client en exécutant des commandes pour les scripts d’automatisation.

Exemple :

- [Obtenir-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus): obtient le Azure information protection étiquette et les informations de protection pour un fichier ou des fichiers spécifiés.
- [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification): analyse un fichier pour définir automatiquement une étiquette de Azure information protection pour un fichier, en fonction des conditions configurées dans la stratégie.
- [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel): définit ou supprime une étiquette Azure information protection pour un fichier, et définit ou supprime la protection en fonction de la configuration de l’étiquette ou des autorisations personnalisées.
- [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication): définit les informations d’authentification pour le client Azure information protection.

Le module **AzureInformationProtection** est installé dans le dossier **\programfiles (x86) \Microsoft Azure information protection** , puis il ajoute ce dossier à la variable système **PSModulePath** . Le fichier .dll de ce module est nommé **AIP.dll**.

> [!IMPORTANT]
> Le module **AzureInformationProtection** ne prend pas en charge la configuration de paramètres avancés pour les étiquettes ou les stratégies d’étiquette. 
>
>Pour ces paramètres, vous avez besoin d’Office 365 Security & Compliance Center PowerShell. Pour plus d’informations, consultez [configurations personnalisées pour le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-customizations.md).

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) disponible à compter de la version 1607 de Windows 10 :<br /> Stratégie de l' **ordinateur local**  >  Configuration de l' **ordinateur**  >  **Modèles d’administration**  >  **Tous les paramètres**  >  **Activer les chemins d’accès longs Win32** 
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

## <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Conditions préalables à l’utilisation du module AzureInformationProtection

Outre la configuration requise pour l’installation du module **AzureInformationProtection** , il existe des conditions préalables supplémentaires pour l’utilisation des applets de commande d’étiquetage pour Azure information protection :

- **Le service de Rights Management Azure doit être activé**.

    Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions relatives à l' [activation du service de protection à partir de Azure information protection](../activate-service.md).

- **Pour supprimer la protection des fichiers pour d’autres utilisateurs à l’aide de votre propre compte**:

    - La fonctionnalité de [super utilisateur](../configure-super-users.md) doit être activée pour votre organisation.
    - Votre compte doit être configuré pour être un super utilisateur pour Azure Rights Management.

    Par exemple, vous souhaiterez peut-être supprimer la protection pour d’autres personnes dans le cadre de la découverte ou de la récupération des données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer cette protection en définissant une nouvelle étiquette qui n’applique pas la protection, ou vous pouvez supprimer l’étiquette.

    Pour supprimer la protection, utilisez l’applet de commande [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) avec le paramètre *RemoveProtection* . La fonction de suppression de la protection est désactivée par défaut et doit d’abord être activée à l’aide de l’applet de commande [Set-LabelPolicy](/powershell/module/azureinformationprotection/set-labelpolicy) .

## <a name="rms-to-unified-labeling-cmdlet-mapping"></a>Mappage des applets de commande d’étiquetage de RMS à Unified

Si vous avez migré à partir de Azure RMS, Notez que les applets de commande associées à RMS sont dépréciées pour une utilisation dans l’étiquetage unifié. 

Certaines des applets de commande héritées ont été remplacées par de nouvelles applets de commande pour l’étiquetage unifié. Par exemple, si vous avez utilisé **New-RMSProtectionLicense** avec la protection RMS et que vous avez effectué la migration vers l’étiquetage unifié, utilisez **New-AIPCustomPermissions** à la place.

Le tableau suivant mappe les applets de commande associées à RMS avec les applets de commande mises à jour utilisées pour l’étiquetage unifié :

|Applet de commande RMS  |Applet de commande Unified Labeling  |
|---------|---------|
|[RMSFileStatus](/powershell/module/azureinformationprotection/get-rmsfilestatus)     |  [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)        |
|[RMSServer](/powershell/module/azureinformationprotection/get-rmsserver)     |  Non pertinent pour l’étiquetage unifié.      |
|[RMSServerAuthentication](/powershell/module/azureinformationprotection/get-rmsserverauthentication)      |   [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Clear-RMSAuthentication](/powershell/module/azureinformationprotection/clear-rmsauthentication)     | [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication)     |  [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)      |
|[RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate)     |       Non pertinent pour l’étiquetage unifié  |
|[New-RMSProtectionLicense](/powershell/module/azureinformationprotection/new-rmsprotectionlicense)     |  [New-AIPCustomPermissions](/powershell/module/azureinformationprotection/new-aipcustompermissions)et [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), avec le paramètre **CustomPermissions**      |
|[Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) |[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), avec le paramètre **RemoveProtection** |
| | |


## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive.

Pour plus d’informations, consultez :

- [Conditions préalables à l’exécution sans assistance des applets de commande d’étiquetage AIP](#prerequisites-for-running-aip-labeling-cmdlets-unattended)
- [Créer et configurer des applications Azure AD pour Set-AIPAuthentication](#create-and-configure-azure-ad-applications-for-set-aipauthentication)
- [Exécution de l’applet de commande Set-AIPAuthentication](#running-the-set-aipauthentication-cmdlet)

> [!NOTE]
> Si l’ordinateur ne peut pas accéder à Internet, il n’est pas nécessaire de créer l’application dans Azure AD et d’exécuter l’applet de commande **Set-AIPAuthentication** . Au lieu de cela, suivez les instructions pour les [ordinateurs déconnectés](clientv2-admin-guide-customizations.md#support-for-disconnected-computers).  

### <a name="prerequisites-for-running-aip-labeling-cmdlets-unattended"></a>Conditions préalables à l’exécution sans assistance des applets de commande d’étiquetage AIP

Pour exécuter Azure Information Protection applets de commande d’étiquetage sans assistance, utilisez les informations d’accès suivantes :

- **Un compte Windows** qui peut se connecter de manière interactive.

- **Un compte Azure ad**, pour l’accès délégué. Pour faciliter l’administration, utilisez un compte unique qui est synchronisé à partir de Active Directory vers Azure AD.

    Pour le compte d’utilisateur délégué :

    |Condition requise  |Détails  |
    |---------|---------|
    |**Stratégie d’étiquette**     |  Vérifiez que vous disposez d’une stratégie d’étiquette affectée à ce compte et que la stratégie contient les étiquettes publiées que vous souhaitez utiliser.   <br><br>Si vous utilisez des stratégies d’étiquette pour différents utilisateurs, vous devrez peut-être créer une nouvelle stratégie d’étiquette qui publie toutes vos étiquettes et publier la stratégie sur ce compte d’utilisateur délégué uniquement.    |
    |**Déchiffrement du contenu**     |    Si ce compte doit déchiffrer du contenu, par exemple pour reprotéger des fichiers et inspecter des fichiers protégés par d’autres utilisateurs, faites-en un [super utilisateur](../configure-super-users.md) pour Azure information protection et assurez-vous que la fonctionnalité de super utilisateur est activée.     |
    |**Contrôles d’intégration**     |    Si vous avez implémenté des [contrôles d’intégration](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans vos contrôles d’intégration que vous avez configurés.     |
    |     |         |

- **Un jeton d’accès Azure ad**, qui définit et stocke les informations d’identification de l’utilisateur délégué pour s’authentifier auprès de Azure information protection. Lorsque le jeton de Azure AD expire, vous devez exécuter à nouveau l’applet de commande pour acquérir un nouveau jeton. 

    Les paramètres de **Set-AIPAuthentication** utilisent les valeurs d’un processus d’inscription d’application dans Azure ad. Pour plus d’informations, consultez [créer et configurer des applications Azure AD pour Set-AIPAuthentication](#create-and-configure-azure-ad-applications-for-set-aipauthentication).

Exécutez les applets de commande d’étiquetage de manière non interactive en exécutant d’abord l’applet de commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) .

L’ordinateur qui exécute l’applet de commande **AIPAuthentication** télécharge la stratégie d’étiquetage qui est affectée à votre compte d’utilisateur délégué dans votre centre de gestion d’étiquetage, comme le centre de conformité Microsoft 365 Security &.

### <a name="create-and-configure-azure-ad-applications-for-set-aipauthentication"></a>Créez et configurez des applications Azure AD pour Set-AIPAuthentication

L’applet de commande **Set-AIPAuthentication** nécessite une inscription d’application pour les paramètres *AppID* et *AppSecret* . 

Pour les utilisateurs qui ont récemment migré depuis le client classique, et ont créé une inscription d’application pour les paramètres *WebAppID* et *NativeAppId* précédents, vous devrez créer une nouvelle inscription d’application pour le client d’étiquetage unifié.

**Pour créer une inscription d’application pour le client d’étiquetage unifié Set-AIPAuthentication applet de** commande :

1. Dans une nouvelle fenêtre de navigateur, connectez le [portail Azure](https://portal.azure.com/) au locataire Azure ad que vous utilisez avec Azure information protection.

1. Accédez à **Azure Active Directory**  >  **gérer**  >  **inscriptions d’applications** et sélectionnez **nouvelle inscription**. 

1. Dans le volet **inscrire une application** , spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

    |Option  |Valeur  |
    |---------|---------|
    |**Nom**     |  `AIP-DelegatedUser` <br>Spécifiez un autre nom si nécessaire. Le nom doit être unique par locataire.       |
    |**Types de comptes pris en charge**     |   Sélectionnez **Comptes dans ce répertoire organisationnel uniquement**.      |
    |**URI de redirection (facultatif)**     |     Sélectionnez **Web**, puis entrez `https://localhost` .    |
    |     |         |

1. Dans le volet **AIP-DelegatedUser** , copiez la valeur de l’ID de l' **application (client)**. 

    La valeur ressemble à l’exemple suivant : `77c3c1c3-abf9-404e-8b2b-4652836c8c66` . 

    Cette valeur est utilisée pour le paramètre *AppID* lorsque vous exécutez l' **applet de commande Set-AIPAuthentication**. Collez et enregistrez la valeur pour référence ultérieure.

1. Dans la barre latérale, sélectionnez **gérer** les  >  **certificats & les secrets**.

    Ensuite, sur le volet **AIP-DelegatedUser-certificats & secrets** , dans la section **secrets client** , sélectionnez **nouvelle clé secrète client**.

1. Pour **Ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **Ajouter**:

    |Champ  |Valeur  |
    |---------|---------|
    |**Description**     |  `Azure Information Protection unified labeling client`       |
    |**Expire**     |   Spécifiez votre choix de durée (1 an, 2 ans ou n’expire jamais)     |
    |     |         |

1. De retour sur le volet **AIP-DelegatedUser-certificates & secrets** , dans la section **secrets client** , copiez la chaîne correspondant à la **valeur**. 

    Cette chaîne ressemble à l’exemple suivant : `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` . 

    Pour être sûr de copier tous les caractères, sélectionnez l’icône à **copier dans le presse-papiers**. 
    
    > [!IMPORTANT]
    > Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreignez l’accès à celle-ci.
    > 

1. Dans la barre latérale, sélectionnez **gérer** les  >  **autorisations d’API**.

    Dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **Ajouter une autorisation**.

1. Dans le volet **demander des autorisations d’API** , vérifiez que vous êtes sous l’onglet **API Microsoft** , puis sélectionnez **Azure Rights Management Services**. 

    Lorsque vous êtes invité à entrer le type d’autorisations dont votre application a besoin, sélectionnez autorisations de l' **application**.

1. Pour les **autorisations SELECT**, développez **contenu** et sélectionnez les éléments suivants, puis sélectionnez **Ajouter des autorisations**.
    
    -  **Contenu. DelegatedReader** 
    -  **Contenu. DelegatedWriter**

1. De retour dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **rajouter une autorisation** .

    Dans le volet **demander des autorisations AIP** , sélectionnez les **API utilisées par mon organisation** et recherchez **service de synchronisation Microsoft information protection**.

1. Dans le volet **demander des autorisations d’API** , sélectionnez autorisations de l' **application**.
    
    Pour les **autorisations SELECT**, développez **UnifiedPolicy**, sélectionnez **UnifiedPolicy. locataire. Read**, puis sélectionnez **Ajouter des autorisations**.

1. De retour dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **accorder le \<*your tenant name*> consentement de l’administrateur pour** et sélectionnez **Oui** pour l’invite de confirmation.
    
    Vos autorisations d’API doivent ressembler à l’image suivante :

    :::image type="content" source="../media/api-permissions-app.png" alt-text="Autorisations d’API pour l’application inscrite dans Azure AD":::

Maintenant que vous avez terminé l’inscription de cette application avec un secret, vous êtes prêt à exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *AppID* et *AppSecret*. En outre, vous aurez besoin de votre ID de locataire. 

> [!TIP]
>Vous pouvez copier rapidement votre ID de locataire à l’aide de portail Azure : **Azure Active Directory**  >  **gérer** l’ID de répertoire des  >  **Propriétés**  >  .

### <a name="running-the-set-aipauthentication-cmdlet"></a>Exécution de l’applet de commande Set-AIPAuthentication

1. Ouvrez Windows PowerShell avec l' **option Exécuter en tant qu’administrateur**. 

1. Dans votre session PowerShell, créez une variable pour stocker les informations d’identification du compte d’utilisateur Windows qui s’exécuteront de manière non interactive. Par exemple, si vous avez créé un compte de service pour le scanneur :

    ```PowerShell
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    Vous êtes invité à entrer le mot de passe de ce compte.

1. Exécutez l’applet de commande **Set-AIPAuthentication** avec le paramètre *OnBeHalfOf* , en spécifiant comme valeur la variable que vous avez créée. 

    Spécifiez également les valeurs d’inscription de votre application, votre ID de locataire et le nom du compte d’utilisateur délégué dans Azure AD. Par exemple :
    
    ```PowerShell
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```
## <a name="next-steps"></a>Étapes suivantes

Pour obtenir de l’aide sur les applets de commande lorsque vous êtes dans une session PowerShell, tapez `Get-Help <cmdlet name> -online` . Par exemple : 

```PowerShell
Get-Help Set-AIPFileLabel -online
```

Pour plus d'informations, consultez les pages suivantes :

- [Personnalisations du client d’étiquetage unifié](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichiers pris en charge](clientv2-admin-guide-file-types.md)