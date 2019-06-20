---
title: Utiliser PowerShell avec le client d’étiquetage unifié Azure Information Protection
description: Instructions et informations destinées aux administrateurs de gérer le client d’étiquetage unifié Azure Information Protection à l’aide de PowerShell.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f90697e1e4df90ab8876843b45957b93c8ba8b07
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236886"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guide de l’administrateur : À l’aide de PowerShell avec le client unifié d’Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque vous installez le client d’étiquetage unifié Azure Information Protection, les commandes PowerShell sont installées automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installés avec le module PowerShell **AzureInformationProtection**, qui a des applets de commande pour l’étiquetage. Exemple :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Étiqueter des fichiers de manière interactive, à l’aide d’un autre compte d’utilisateur dans votre propre.|

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) disponible à compter de la version 1607 de Windows 10 :<br /> **Stratégie de l’ordinateur local** > **Configuration ordinateur** > **modèles d’administration** > **tous les paramètres**  >  **Win32 activer les chemins d’accès longs** 
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

> [!IMPORTANT]
> Le module AzureInformationProtection ne prend pas en charge la configuration des paramètres avancés pour les étiquettes ou les stratégies de l’étiquette. Pour ces paramètres, vous avez besoin de la sécurité et Office 365 PowerShell du centre de conformité. Pour plus d’informations, consultez [configurations personnalisées pour Azure Information Protection unifiée client étiquetage](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Configuration requise pour l’utilisation du module AzureInformationProtection

Outre la configuration requise pour l’installation du module AzureInformationProtection, il existe des conditions préalables supplémentaires pour lorsque vous utilisez les applets de commande étiquetage pour Azure Information Protection :

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 

    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Prérequis 1 : Le service Azure Rights Management doit être activé

Si votre client Azure Information Protection n’est pas activé pour appliquer la protection, consultez les instructions pour [activation d’Azure Rights Management](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Prérequis 2 : Pour supprimer la protection des fichiers pour les autres utilisateurs en utilisant votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

Remarque : Les informations contenues dans cette section concerne la préversion uniquement du client Azure Information Protection unifiée étiquetage.

Vous pouvez exécuter les applets de commande d’étiquetage de manière non interactive à l’aide de l’applet de commande **Set-AIPAuthentication**.

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive. Pour les exécuter sans assistance, créez un compte d’utilisateur Azure AD à cet effet. Ensuite, dans le contexte de cet utilisateur, exécutez l’applet de commande Set-AIPAuthentication pour définir et stocker les informations d’identification à l’aide d’un jeton d’accès Azure AD. Ce compte d’utilisateur est ensuite authentifié et initialisé pour le service de protection d’Azure Information Protection. Le compte télécharge la stratégie Azure Information Protection et tous les modèles de protection qui utilisent les étiquettes.

> [!NOTE]
> Si vous utilisez des [stratégies délimitées](../configure-policy-scope.md), n’oubliez pas que vous devrez peut-être ajouter ce compte à vos stratégies délimitées.

La première fois que vous exécutez cette applet de commande, vous êtes invité à vous connecter à Azure Information Protection. Spécifiez le nom de compte d’utilisateur et le mot de passe que vous avez créé pour le compte sans assistance. Après cela, ce compte peut alors exécuter les applets de commande étiquetage en mode non interactif jusqu'à expiration du jeton d’authentification dans Azure AD. 

Le compte d’utilisateur pouvoir se connecter interactivement cette première fois, le compte doit avoir le **ouvrir une session localement** attribution des droits utilisateur. Ce droit est standard pour les comptes d’utilisateur, mais vos stratégies d’entreprise peuvent interdire cette configuration pour les comptes de service. Si tel est le cas, vous pouvez exécuter Set-AIPAuthentication avec le *OnBehalfOf* paramètre afin que l’authentification se termine sans l’invite de connexion.

Expiration du jeton dans Azure AD, exécutez l’applet de commande pour acquérir un nouveau jeton.

Si vous exécutez cette applet de commande sans paramètres, le compte acquiert un jeton d’accès qui est valide 90 jours ou jusqu’à ce que votre mot de passe expire.  

Pour contrôler à quel moment le jeton d’accès expire, exécutez cette applet de commande avec des paramètres. Cette configuration vous permet de configurer le jeton d’accès dans Azure AD pendant un an, deux ans, ou pour ne jamais expirer. Vous avez besoin de deux applications inscrites dans Azure Active Directory : Une application **Web / API** et une **application native**. Les paramètres de Set-AIPAuthentication utilisent les valeurs de ces applications.

Après avoir exécuté cette applet de commande, vous pouvez exécuter les applets de commande étiquetage dans le contexte du compte de service que vous avez créé.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Pour créer et configurer les applications Azure AD pour Set-AIPAuthentication

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure AD que vous utilisez avec Azure Information Protection, accédez à **Azure Active Directory** > **gérer** > **inscriptions**. 

3. Sélectionnez **+ nouvelle inscription**, pour créer votre application Web/API. Sur le **inscrire une application** panneau, spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

   - **Nom**: `AIPOnBehalfOf`
        
        Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - **Prise en charge des types de comptes**: **Comptes dans ce répertoire d’organisation uniquement**
    
    - **(Facultatif) des URI de redirection**: **Web** et `http://localhost`

4. Sur le **AIPOnBehalfOf** panneau, copiez la valeur de la **ID d’Application (client)** . La valeur est similaire à l’exemple suivant : `57c3c1c3-abf9-404e-8b2b-4652836c8c66`. Cette valeur est utilisée pour le *WebAppId* paramètre lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

5. Toujours dans le **AIPOnBehalfOf** panneau, à partir de la **gérer** menu, sélectionnez **authentification**.

6. Sur le **AIPOnBehalfOf - authentification** panneau, dans le **paramètres avancés** section, sélectionnez le **les jetons d’ID** case à cocher, puis sélectionnez **enregistrer**.

7. Toujours dans le **AIPOnBehalfOf - authentification** panneau, à partir de la **gérer** menu, sélectionnez **certificats et clés secrètes**.

8. Sur le **AIPOnBehalfOf - certificats et clés secrètes** panneau, dans le **clés secrètes de Client** section, sélectionnez **+ nouvelle clé secrète client**. 

9. Pour **ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **ajouter**:
    
    - **Description**: `Azure Information Protection client`
    - **Expiration**: Spécifiez la durée de votre choix (1 an, 2 ans ou jamais expire)

9. Sur le **AIPOnBehalfOf - certificats et clés secrètes** panneau, dans le **clés secrètes de Client** section, copiez la chaîne pour le **valeur**. Cette chaîne est similaire à l’exemple suivant : `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`. Pour vous assurer que vous copiez tous les caractères, sélectionnez l’icône pour **copier dans le Presse-papiers**. 
    
    Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme avec toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreindre l’accès.

10. Toujours dans le **AIPOnBehalfOf - certificats et clés secrètes** panneau, à partir de la **gérer** menu, sélectionnez **exposer une API**.

11. Sur le **AIPOnBehalfOf - exposent une API** panneau, sélectionnez **définir** pour le **URI ID d’Application** option, puis, dans le **URI ID d’Application** valeur, modifier **api** à **http**. Cette chaîne est similaire à l’exemple suivant : `http://d244e75e-870b-4491-b70d-65534953099e`. 
    
    Sélectionnez **Enregistrer**.

12. Sur le **AIPOnBehalfOf - exposent une API** panneau, sélectionnez **+ ajouter une étendue**.

13. Sur le **ajouter une étendue** panneau, spécifiez les informations suivantes, en utilisant les chaînes suggérées comme exemples et sélectionnez **ajouter une étendue**:
    - **Nom de l’étendue**: `user-impersonation`
    - **Qui peut accepter ?** : **Les administrateurs et utilisateurs**
    - **Nom complet de consentement administrateur**: `Access Azure Information Protection scanner`
    - **Description du consentement administrateur**: `Allow the application to access the scanner for the signed-in user`
    - **Nom complet de consentement utilisateur**: `Access Azure Information Protection scanner`
    - **Description du consentement utilisateur**: `Allow the application to access the scanner for the signed-in user`
    - **état**: **Activé** (la valeur par défaut)

14. Sur le **AIPOnBehalfOf - exposent une API** panneau, fermez ce panneau.

15. Sur le **inscriptions** panneau, sélectionnez **+ nouvelle inscription d’application** pour créer votre application native.

16. Sur le **inscrire une application** panneau, spécifiez les paramètres suivants, puis sélectionnez **inscrire**:
    - **Nom**: `AIPClient`
    - **Prise en charge des types de comptes**: **Comptes dans ce répertoire d’organisation uniquement**
    - **(Facultatif) des URI de redirection**: **Un client public (mobile et bureau)** et `http://localhost`

17. Sur le **AIPClient** panneau, copiez la valeur de la **ID d’Application (client)** . La valeur est similaire à l’exemple suivant : `8ef1c873-9869-4bb1-9c11-8313f9d7f76f`. 
    
    Cette valeur est utilisée pour le paramètre NativeAppId lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

18. Toujours dans le **AIPClient** panneau, à partir de la **gérer** menu, sélectionnez **authentification**.

19. Sur le **AIPClient - authentification** panneau, spécifiez les éléments suivants, puis sélectionnez **enregistrer**:
    - Dans le **paramètres avancés** section, sélectionnez **les jetons d’ID**.
    - Dans le **type de client par défaut** section, sélectionnez **Oui**.

20. Toujours dans le **AIPClient - authentification** panneau, à partir de la **gérer** menu, sélectionnez **autorisations d’API**.

21. Sur le **AIPClient - autorisations** panneau, sélectionnez **+ ajouter une autorisation**.

22. Sur le **autorisations d’API demande** panneau, sélectionnez **mes API**.

23. Dans le **sélectionner une API** , sélectionnez **APIOnBehalfOf**, puis sélectionnez la case à cocher pour **-emprunt d’identité**, que l’autorisation. Sélectionnez **ajouter des autorisations**. 

24. Sur le **autorisations d’API** panneau, dans le **donner leur consentement** section, sélectionnez **accorder le consentement de l’administrateur pour \< *nom de votre client* >**  et sélectionnez **Oui** pour l’invite de confirmation.

Vous venez de terminer la configuration des deux applications, et vous disposez des valeurs dont vous avez besoin pour exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *WebAppId*, *WebAppKey* and *NativeAppId*. À partir de nos exemples :

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

Exécutez cette commande dans le contexte du compte qui étiquettera et protégera les documents de manière non interactive. Par exemple, un compte d’utilisateur pour vos scripts PowerShell ou le compte de service pour exécuter le scanneur Azure Information Protection.

Lorsque vous exécutez cette commande pour la première fois, vous êtes invité à vous connecter, ce qui crée et stocke en toute sécurité le jeton d’accès de votre compte dans %localappdata%\Microsoft\MSIP. Après cette première connexion, vous pouvez étiqueter et protéger les fichiers de manière non interactive sur l’ordinateur. Toutefois, si vous utilisez un compte de service à l’étiquette et protégez les fichiers, et ce compte de service ne peut pas connectez-vous de manière interactive, utilisez le *OnBehalfOf* paramètre avec Set-AIPAuthentication :

1. Créez une variable pour stocker les informations d’identification d’un compte Active Directory disposant de l’attribution des droits utilisateur pour vous connecter manière interactive. Exemple :
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Exécutez l’applet de commande Set-AIPAuthentication avec le *OnBeHalfOf* paramètre en spécifiant comme valeur de la variable que vous venez de créer. Exemple :
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>Étapes suivantes
Pour l’aide d’applet de commande lorsque vous êtes dans une session PowerShell, tapez `Get-Help <cmdlet name> -online`. Exemple : 

    Get-Help Set-AIPFileLabel -online

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)
