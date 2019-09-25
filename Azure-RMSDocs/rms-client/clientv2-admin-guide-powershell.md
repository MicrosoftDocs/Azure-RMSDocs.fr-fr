---
title: Utiliser PowerShell avec le client d’étiquetage unifié Azure Information Protection
description: Instructions et informations permettant aux administrateurs de gérer le Azure Information Protection client d’étiquetage unifié à l’aide de PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1db49d2a6033301b5922e66bc76be190b6162af
ms.sourcegitcommit: 437143e1f7f33aba46ffcc3900c31a763a2105c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227793"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guide de l’administrateur : Utilisation de PowerShell avec le client unifié Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque vous installez le client d’étiquetage unifié Azure Information Protection, les commandes PowerShell sont installées automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installées avec le module PowerShell **AzureInformationProtection**, qui possède des applets de commande pour l’étiquetage. Exemple :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Étiquetez les fichiers de manière non interactive, par exemple à l’aide d’un script qui s’exécute selon une planification.|

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) disponible à compter de la version 1607 de Windows 10 :<br /> **Stratégie** >  >  >  de l’ordinateur local Configuration ordinateur modèles d’administration tous les paramètres activer les chemins longs Win32 >  
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

> [!IMPORTANT]
> Le module AzureInformationProtection ne prend pas en charge la configuration de paramètres avancés pour les étiquettes ou les stratégies d’étiquette. Pour ces paramètres, vous avez besoin d’Office 365 Centre de sécurité et de conformité PowerShell. Pour plus d’informations, consultez [configurations personnalisées pour le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Conditions préalables à l’utilisation du module AzureInformationProtection

Outre la configuration requise pour l’installation du module AzureInformationProtection, il existe d’autres conditions préalables à l’utilisation des applets de commande d’étiquetage pour Azure Information Protection:

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 

    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prérequis 1 : Le service Azure Rights Management doit être activé

Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions pour [[activation du service de protection à partir de Azure information protection](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prérequis 2 : Pour supprimer la protection des fichiers pour les autres utilisateurs en utilisant votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

Vous pouvez exécuter les applets de commande d’étiquetage de manière non interactive à l’aide de l’applet de commande **Set-AIPAuthentication**.

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive. Pour les exécuter sans assistance, créez un compte d’utilisateur Azure AD à cet effet. Ensuite, dans le contexte de cet utilisateur, exécutez l’applet de commande Set-AIPAuthentication pour définir et stocker les informations d’identification à l’aide d’un jeton d’accès Azure AD. Ce compte d’utilisateur est ensuite authentifié et amorcé pour le service de protection à partir de Azure Information Protection. Le compte télécharge la stratégie de Azure Information Protection et tous les modèles de protection utilisés par les étiquettes.

> [!NOTE]
> Si vous utilisez des stratégies d’étiquette pour différents utilisateurs, n’oubliez pas que vous devrez peut-être ajouter ce compte à une stratégie d’étiquette spécifique.

La première fois que vous exécutez cette applet de commande, vous êtes invité à vous connecter à Azure Information Protection. Spécifiez le nom et le mot de passe du compte d’utilisateur que vous avez créé pour le compte sans assistance. Après cela, ce compte peut ensuite exécuter les applets de commande d’étiquetage de manière non interactive jusqu’à l’expiration du jeton d’authentification dans Azure AD. 

Pour que le compte d’utilisateur puisse se connecter de manière interactive pour la première fois, le compte doit avoir l’attribution **de droits d’utilisateur ouvrir une session localement** . Ce droit est standard pour les comptes d’utilisateur, mais vos stratégies d’entreprise peuvent interdire cette configuration pour les comptes de service. Si c’est le cas, vous pouvez exécuter Set-AIPAuthentication avec le paramètre *OnBehalfOf* afin que l’authentification se termine sans l’invite de connexion.

Lorsque le jeton de Azure AD expire, réexécutez l’applet de commande pour acquérir un nouveau jeton.

Si vous exécutez cette applet de commande sans paramètres, le compte acquiert un jeton d’accès qui est valide 90 jours ou jusqu’à ce que votre mot de passe expire.  

Pour contrôler à quel moment le jeton d’accès expire, exécutez cette applet de commande avec des paramètres. Cette configuration vous permet de configurer le jeton d’accès dans Azure AD pendant un an, deux ans ou pour ne jamais expirer. Les paramètres de Set-AIPAuthentication utilisent les valeurs d’un processus d’inscription d’application dans Azure AD.

Après avoir exécuté cette applet de commande, vous pouvez exécuter les applets de commande d’étiquetage dans le contexte du compte de service que vous avez créé.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Pour créer et configurer les applications Azure AD pour Set-AIPAuthentication

> [!NOTE]
> Si vous utilisez la préversion actuelle du client d’étiquetage unifié n’utilisez pas cette procédure mais, à la place, consultez [pour créer et configurer les applications Azure AD pour le client set-AIPAuthentication-Preview](#to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client).

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure ad que vous utilisez avec Azure information protection, accédez à **Azure Active Directory** > **gérer** > les**inscriptions d’applications**. 

3. Sélectionnez **+ nouvelle inscription**pour créer votre application Web App/API. Dans le panneau **inscrire une application** , spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

   - **Nom**:`AIPOnBehalfOf`
        
        Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - **Types de comptes pris en charge**: **Comptes dans ce répertoire d’organisation uniquement**
    
    - **URI de redirection (facultatif)** : **Web** et`http://localhost`

4. Dans le panneau **AIPOnBehalfOf** , copiez la valeur de l’ID de l' **application (client)** . La valeur ressemble à l’exemple suivant: `57c3c1c3-abf9-404e-8b2b-4652836c8c66`. Cette valeur est utilisée pour le paramètre *WebAppId* lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

5. Toujours dans le panneau **AIPOnBehalfOf** , dans l’encadré **gérer** , sélectionnez **authentification**.

6. Dans le panneau **AIPOnBehalfOf-Authentication** , dans la section **Paramètres avancés** , activez la case à cocher **ID Tokens** , puis sélectionnez **Enregistrer**.

7. Toujours dans le panneau **AIPOnBehalfOf-Authentication** , dans l’encadré **gérer** , sélectionnez **certificats & secrets**.

8. Dans le panneau **AIPOnBehalfOf-certificats & secrets** , dans la section **secrets client** , sélectionnez **+ nouvelle clé secrète client**. 

9. Pour **Ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **Ajouter**:
    
    - **Description**:`Azure Information Protection client`
    - **Expire**le: Spécifiez votre choix de durée (1 an, 2 ans ou n’expire jamais)

9. De retour dans le panneau **AIPOnBehalfOf-certificats & secrets** , dans la section **secrets clients** , copiez la chaîne correspondant à la **valeur**. Cette chaîne ressemble à l’exemple suivant: `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`. Pour être sûr de copier tous les caractères, sélectionnez l’icône à **copier dans le presse-papiers**. 
    
    Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreignez l’accès à celle-ci.

10. Toujours dans le panneau **AIPOnBehalfOf-certificats & secrets** , dans l’encadré **gérer** , sélectionnez **exposer une API**.

11. Dans le panneau **AIPOnBehalfOf-exposer une API** , sélectionnez **Set** pour l’option URI de l' **ID d’application** , et dans la valeur URI de l’ID d' **application** , remplacez **API** par **http**. Cette chaîne ressemble à l’exemple suivant: `http://d244e75e-870b-4491-b70d-65534953099e`. 
    
    Sélectionnez **Enregistrer**.

12. De retour sur le panneau **AIPOnBehalfOf-exposer une API** , sélectionnez **+ Ajouter une étendue**.

13. Dans le panneau **Ajouter une étendue** , spécifiez les éléments suivants, en utilisant les chaînes suggérées comme exemples, puis sélectionnez **Ajouter une étendue**:
    - **Nom**de l’étendue:`user-impersonation`
    - **Qui peut donner son consentement?** : **Administrateurs et utilisateurs**
    - **Nom d’affichage du consentement**de l’administrateur:`Access Azure Information Protection scanner`
    - **Description du consentement**de l’administrateur:`Allow the application to access the scanner for the signed-in user`
    - **Nom complet du consentement**de l’utilisateur:`Access Azure Information Protection scanner`
    - **Description du consentement**de l’utilisateur:`Allow the application to access the scanner for the signed-in user`
    - **État**: **Activé** (valeur par défaut)

14. De retour dans le panneau **AIPOnBehalfOf-exposer une API** , fermez ce panneau.

15. Dans le panneau **inscriptions d’applications** , sélectionnez **+ nouvelle inscription d’application** pour créer votre application native.

16. Dans le panneau **inscrire une application** , spécifiez les paramètres suivants, puis sélectionnez **inscrire**:
    - **Nom**:`AIPClient`
    - **Types de comptes pris en charge**: **Comptes dans ce répertoire d’organisation uniquement**
    - **URI de redirection (facultatif)** : **Client public (mobile & Desktop)** et`http://localhost`

17. Dans le panneau **AIPClient** , copiez la valeur de l’ID de l' **application (client)** . La valeur ressemble à l’exemple suivant: `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`. 
    
    Cette valeur est utilisée pour le paramètre NativeAppId lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

18. Toujours dans le panneau **AIPClient** , dans l’encadré **gérer** , sélectionnez **authentification**.

19. Dans le panneau **AIPClient-Authentication** , spécifiez les éléments suivants, puis sélectionnez **Enregistrer**:
    - Dans la section **Paramètres avancés** , sélectionnez **ID jetons**.
    - Dans la section **type de client par défaut** , sélectionnez **Oui**.

20. Toujours dans le panneau **AIPClient-Authentication** , dans le volet **gérer** , sélectionnez **autorisations API**.

21. Dans le panneau **AIPClient-autorisations** , sélectionnez **+ Ajouter une autorisation**.

22. Dans le panneau **demander des autorisations d’API** , sélectionnez **mes API**.

23. Dans la section **Sélectionner une API** , sélectionnez **APIOnBehalfOf**, puis activez la case à cocher **User-emprunt d’identité**comme autorisation. Sélectionnez **Ajouter des autorisations**. 

24. De retour dans le panneau autorisations de l' **API** , dans la section **accorder** le consentement, sélectionnez **accorder le consentement de l’administrateur pour \<le nom> de *votre locataire***  et sélectionnez **Oui** pour l’invite de confirmation.

Vous venez de terminer la configuration des deux applications, et vous disposez des valeurs dont vous avez besoin pour exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *WebAppId*, *WebAppKey* and *NativeAppId*. À partir de nos exemples:

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

Exécutez cette commande dans le contexte du compte qui étiquettera et protégera les documents de manière non interactive. Par exemple, un compte d’utilisateur pour vos scripts PowerShell ou le compte de service pour exécuter le scanneur Azure Information Protection.

Lorsque vous exécutez cette commande pour la première fois, vous êtes invité à vous connecter, ce qui crée et stocke en toute sécurité le jeton d’accès de votre compte dans %localappdata%\Microsoft\MSIP. Après cette première connexion, vous pouvez étiqueter et protéger les fichiers de manière non interactive sur l’ordinateur. Toutefois, si vous utilisez un compte de service pour étiqueter et protéger des fichiers, et que ce compte de service ne peut pas se connecter de manière interactive, utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication:

1. Créez une variable pour stocker les informations d’identification d’un compte Active Directory disposant de l’attribution de droits d’utilisateur pour se connecter de manière interactive. Exemple :
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Exécutez l’applet de commande Set-AIPAuthentication avec le paramètre *OnBeHalfOf* , en spécifiant comme valeur la variable que vous venez de créer. Exemple :
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds


#### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client"></a>Pour créer et configurer les applications Azure AD pour le client set-AIPAuthentication-preview

Utilisez la procédure suivante comme autre instruction uniquement si vous avez installé la version préliminaire du client d’étiquetage unifié. 

Pour cette version du client, vous devez créer une nouvelle inscription d’application pour les paramètres *AppID* et *AppSecret* pour Set-AIPAuthentication. Si vous avez effectué une mise à niveau à partir d’une version précédente du client et créé une inscription d’application pour les paramètres *WebAppId* et *NativeAppId* précédents, ceux-ci ne fonctionneront pas avec cette version du client.

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure ad que vous utilisez avec Azure information protection, accédez à **Azure Active Directory** > **gérer** > les**inscriptions d’applications**. 

3. Sélectionnez **+ nouvel enregistrement**. Dans le panneau **inscrire une application** , spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

   - **Nom**:`AIPv2OnBehalfOf`
        
        Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - **Types de comptes pris en charge**: **Comptes dans ce répertoire d’organisation uniquement**
    
    - **URI de redirection (facultatif)** : **Web** et`https://localhost`

4. Dans le panneau **AIPv2OnBehalfOf** , copiez la valeur de l’ID de l' **application (client)** . La valeur ressemble à l’exemple suivant: `77c3c1c3-abf9-404e-8b2b-4652836c8c66`. Cette valeur est utilisée pour le paramètre *AppID* lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

5. Toujours dans le panneau **AIPv2OnBehalfOf** , dans l’encadré **gérer** , sélectionnez **certificats & secrets**.

6. Dans le panneau **AIPv2OnBehalfOf-certificats & secrets** , dans la section **secrets client** , sélectionnez **+ nouvelle clé secrète client**.

7. Pour **Ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **Ajouter**:
    
    - **Description**:`Azure Information Protection unified labeling client`
    - **Expire**le: Spécifiez votre choix de durée (1 an, 2 ans ou n’expire jamais)

8. De retour dans le panneau **AIPv2OnBehalfOf-certificats & secrets** , dans la section **secrets clients** , copiez la chaîne correspondant à la **valeur**. Cette chaîne ressemble à l’exemple suivant: `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4`. Pour être sûr de copier tous les caractères, sélectionnez l’icône à **copier dans le presse-papiers**. 
    
    Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreignez l’accès à celle-ci.

9. Dans **gérer** dans la barre latérale, sélectionnez **autorisations API**.

10. Dans le panneau **autorisations AIPv2OnBehalfOf-API** , sélectionnez **+ Ajouter une autorisation**.

11. Dans le panneau **demander des autorisations d’API** , vérifiez que vous êtes sous l’onglet **API Microsoft** , puis sélectionnez **Azure Rights Management Services**. Lorsque vous êtes invité à entrer le type d’autorisations dont votre application a besoin, sélectionnez autorisations de l' **application**.

12. Pour **Sélectionner des autorisations**, développez **contenu** , puis sélectionnez les éléments suivants :
    
    -  **Content. DelegatedWriter** (toujours obligatoire)
    -  **Content.** superutilisateur (obligatoire si la [fonctionnalité de super utilisateur](../configure-super-users.md) est nécessaire)
    -  **Content. Writer** (toujours obligatoire)
    
    La fonctionnalité de super utilisateur permet au compte de toujours déchiffrer le contenu. Par exemple, pour reprotéger des fichiers et inspecter des fichiers protégés par d’autres utilisateurs.

13. Sélectionnez **Ajouter des autorisations**.

14. Dans le panneau **autorisations AIPv2OnBehalfOf-API** , sélectionnez **+ Ajouter une nouvelle autorisation** .

15. Dans le panneau **demander des autorisations AIP** , sélectionnez les **API utilisées par mon organisation**et recherchez **service de synchronisation Microsoft information protection**.

16. Dans le panneau **demander des autorisations d’API** , sélectionnez autorisations de l' **application**.

17. Pour les **autorisations SELECT**, développez **UnifiedPolicy** , puis sélectionnez les éléments suivants :
    
    -  **UnifiedPolicy. locataire. Read**

18. Sélectionnez **Ajouter des autorisations**.

19. De retour dans le panneau autorisations d’API, sélectionnez **accorder le \<consentement de l’administrateur pour le *nom* > de votre locataire** et sélectionnez **Oui** pour l’invite de confirmation.

Vous avez maintenant terminé l’inscription de cette application avec un secret, vous êtes prêt à exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *AppID*et *AppSecret*. En outre, vous aurez besoin de votre ID de locataire. 

> [!TIP]
>Vous pouvez copier rapidement votre ID de locataire à l’aide de Portail Azure : **Azure Active Directory** > gérerl’IDderépertoiredespropriétés > . > 

Dans notre exemple, avec l’ID de locataire 9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a :

`Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a"`

Lorsque vous exécutez cette commande pour la première fois, vous êtes invité à vous connecter, ce qui crée et stocke en toute sécurité le jeton d’accès de votre compte dans %localappdata%\Microsoft\MSIP. Après cette première connexion, vous pouvez étiqueter et protéger les fichiers de manière non interactive sur l’ordinateur. Toutefois, si vous utilisez un compte de service pour étiqueter et protéger des fichiers, et que ce compte de service ne peut pas se connecter de manière interactive, utilisez le paramètre *OnBehalfOf* avec set-AIPAuthentication:

1. Créez une variable pour stocker les informations d’identification d’un compte Active Directory disposant de l’attribution de droits d’utilisateur pour se connecter de manière interactive. Exemple :
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Exécutez l’applet de commande Set-AIPAuthentication avec le paramètre *OnBeHalfOf* , en spécifiant comme valeur la variable que vous venez de créer. Exemple :
    
        Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir de l’aide sur les applets de commande lorsque `Get-Help <cmdlet name> -online`vous êtes dans une session PowerShell, tapez. Exemple : 

    Get-Help Set-AIPFileLabel -online

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)
