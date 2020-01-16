---
title: Utiliser PowerShell avec le client d’étiquetage unifié Azure Information Protection
description: Instructions et informations permettant aux administrateurs de gérer le Azure Information Protection client d’étiquetage unifié à l’aide de PowerShell.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 344932883ea0f614ee442ece113f118d4827ac91
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/15/2020
ms.locfileid: "75959972"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>Guide de l’administrateur : utilisation de PowerShell avec le client unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012, windows Server 2008 R2*
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Lorsque vous installez le client d’étiquetage unifié Azure Information Protection, les commandes PowerShell sont installées automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installées avec le module PowerShell **AzureInformationProtection**, qui possède des applets de commande pour l’étiquetage. Exemple :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Étiquetez les fichiers de manière non interactive, par exemple à l’aide d’un script qui s’exécute selon une planification.|

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/) disponible à compter de la version 1607 de Windows 10 :<br /> **Stratégie de l’ordinateur Local** > **configuration** de l’ordinateur > **Modèles d’administration** > **tous les paramètres** > **activer les chemins longs Win32** 
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

> [!IMPORTANT]
> Le module AzureInformationProtection ne prend pas en charge la configuration de paramètres avancés pour les étiquettes ou les stratégies d’étiquette. Pour ces paramètres, vous avez besoin d’Office 365 Centre de sécurité et de conformité PowerShell. Pour plus d’informations, consultez [configurations personnalisées pour le client d’étiquetage unifié Azure information protection](clientv2-admin-guide-customizations.md).

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>Conditions préalables à l’utilisation du module AzureInformationProtection

Outre la configuration requise pour l’installation du module AzureInformationProtection, il existe d’autres conditions préalables à l’utilisation des applets de commande d’étiquetage pour Azure Information Protection :

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 

    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Condition préalable 1 : le service Azure Rights Management doit être activé

Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions pour [[activation du service de protection à partir de Azure information protection](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Condition préalable 2 : supprimer la protection de fichiers pour les autres utilisateurs à l’aide de votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte comme super utilisateur, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](../configure-super-users.md).

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

Vous pouvez exécuter les applets de commande d’étiquetage de manière non interactive à l’aide de l’applet de commande [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication).

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive. Pour les exécuter sans assistance, utilisez un compte Windows qui peut se connecter de manière interactive et utilisez un compte dans Azure AD qui sera utilisé pour l’accès délégué. Pour faciliter l’administration, utilisez un compte unique qui est synchronisé à partir de Active Directory vers Azure AD.

Vous devez également demander un jeton d’accès à partir de Azure AD, qui définit et stocke les informations d’identification de l’utilisateur délégué pour s’authentifier auprès de Azure Information Protection.

L’ordinateur qui exécute l’applet de commande AIPAuthentication télécharge les stratégies d’étiquette avec des étiquettes qui sont affectées au compte d’utilisateur délégué à l’aide de votre centre de gestion d’étiquetage, tel que le Centre de sécurité et de conformité Office 365.

> [!NOTE]
> Si vous utilisez des stratégies d’étiquette pour différents utilisateurs, vous devrez peut-être créer une nouvelle stratégie d’étiquette qui publie toutes vos étiquettes et publier la stratégie sur ce compte d’utilisateur délégué uniquement.

Lorsque le jeton de Azure AD expire, vous devez exécuter à nouveau l’applet de commande pour acquérir un nouveau jeton. Vous pouvez configurer le jeton d’accès dans Azure AD pendant un an, deux ans ou pour ne jamais expirer. Les paramètres de Set-AIPAuthentication utilisent des valeurs d’un processus d’inscription d’application dans Azure AD, comme décrit dans la section suivante.

Pour le compte d’utilisateur délégué :

- Vérifiez que vous disposez d’une stratégie d’étiquette affectée à ce compte et que la stratégie contient les étiquettes publiées que vous souhaitez utiliser.

- Si ce compte doit déchiffrer du contenu, par exemple pour reprotéger des fichiers et inspecter des fichiers protégés par d’autres utilisateurs, faites-en un [super utilisateur](../configure-super-users.md) pour Azure information protection et assurez-vous que la fonctionnalité de super utilisateur est activée.

- Si vous avez implémenté des [contrôles d’intégration](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) pour un déploiement échelonné, assurez-vous que ce compte est inclus dans vos contrôles d’intégration que vous avez configurés.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Pour créer et configurer les applications Azure AD pour Set-AIPAuthentication

> [!IMPORTANT]
> Ces instructions concernent la version actuelle de la disponibilité générale du client d’étiquetage unifié et s’appliquent également à la version préliminaire du scanneur pour ce client.

Set-AIPAuthentication nécessite une inscription d’application pour les paramètres *AppID* et *AppSecret* . Si vous avez effectué une mise à niveau à partir d’une version précédente du client et créé une inscription d’application pour les paramètres *WebAppId* et *NativeAppId* précédents, ceux-ci ne fonctionneront pas avec le client d’étiquetage unifié. Vous devez créer une nouvelle inscription d’application comme suit :

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure AD que vous utilisez avec Azure Information Protection, accédez à **Azure Active Directory** > **gérer** > **inscriptions d’applications**. 

3. Sélectionnez **+ nouvel enregistrement**. Dans le volet **inscrire une application** , spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

   - **Nom** : `AIP-DelegatedUser`
        
        Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - **Types de comptes pris en charge**: **comptes dans ce répertoire d’organisation uniquement**
    
    - **URI de redirection (facultatif)** : **Web** et `https://localhost`

4. Dans le volet **AIP-DelegatedUser** , copiez la valeur de l’ID de l' **application (client)** . La valeur ressemble à l’exemple suivant : `77c3c1c3-abf9-404e-8b2b-4652836c8c66`. Cette valeur est utilisée pour le paramètre *AppID* lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

5. Dans la barre latérale, sélectionnez **gérer** les **certificats > & les secrets**.

6. Sur le volet **AIP-DelegatedUser-certificats & secrets** , dans la section **secrets client** , sélectionnez **+ nouvelle clé secrète client**.

7. Pour **Ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **Ajouter**:
    
    - **Description**: `Azure Information Protection unified labeling client`
    - **Expires**: spécifiez votre choix de durée (1 an, 2 ans ou n’expire jamais)

8. De retour sur le volet **AIP-DelegatedUser-certificates & secrets** , dans la section **secrets client** , copiez la chaîne correspondant à la **valeur**. Cette chaîne ressemble à l’exemple suivant : `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4`. Pour être sûr de copier tous les caractères, sélectionnez l’icône à **copier dans le presse-papiers**. 
    
    Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreignez l’accès à celle-ci.

9. Dans la barre latérale, sélectionnez **gérer** les **autorisations d’API** > .

10. Dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **+ Ajouter une autorisation**.

11. Dans le volet **demander des autorisations d’API** , vérifiez que vous êtes sous l’onglet **API Microsoft** , puis sélectionnez **Azure Rights Management Services**. Lorsque vous êtes invité à entrer le type d’autorisations dont votre application a besoin, sélectionnez autorisations de l' **application**.

12. Pour **Sélectionner des autorisations**, développez **contenu** , puis sélectionnez les éléments suivants :
    
    -  **Contenu. DelegatedReader** 
    -  **Contenu. DelegatedWriter**

13. Sélectionnez **Ajouter des autorisations**.

14. De retour dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **+ Ajouter une nouvelle autorisation** .

15. Dans le volet **demander des autorisations AIP** , sélectionnez les **API utilisées par mon organisation**et recherchez **service de synchronisation Microsoft information protection**.

16. Dans le volet **demander des autorisations d’API** , sélectionnez autorisations de l' **application**.

17. Pour les **autorisations SELECT**, développez **UnifiedPolicy** , puis sélectionnez les éléments suivants :
    
    -  **UnifiedPolicy. locataire. Read**

18. Sélectionnez **Ajouter des autorisations**.

19. De retour dans le volet d' **autorisations AIP-DelegatedUser-API** , sélectionnez **accorder le consentement de l’administrateur pour \<*le nom de votre locataire*>** et sélectionnez **Oui** pour l’invite de confirmation.
    
    Vos autorisations d’API doivent ressembler à ce qui suit :
    
    ![Autorisations d’API pour l’application inscrite dans Azure AD](../media/api-permissions-app.png)

Maintenant que vous avez terminé l’inscription de cette application avec un secret, vous êtes prêt à exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *AppID*et *AppSecret*. En outre, vous aurez besoin de votre ID de locataire. 

> [!TIP]
>Vous pouvez copier rapidement votre ID de locataire à l’aide de Portail Azure : **Azure Active Directory** > **gérer** les **Propriétés** de >  > **ID de répertoire**.

1. Ouvrez Windows PowerShell avec l' **option Exécuter en tant qu’administrateur**. 

2. Dans votre session PowerShell, créez une variable pour stocker les informations d’identification du compte d’utilisateur Windows qui s’exécuteront de manière non interactive. Par exemple, si vous avez créé un compte de service pour le scanneur :
    
        $pscreds = Get-Credential "CONTOSO\srv-scanner"
    
    Vous êtes invité à entrer le mot de passe de ce compte.

2. Exécutez l’applet de commande Set-AIPAuthentication avec le paramètre *OnBeHalfOf* , en spécifiant comme valeur la variable que vous venez de créer. Spécifiez également les valeurs d’inscription de votre application, votre ID de locataire et le nom du compte d’utilisateur délégué dans Azure AD. Exemple :
    
        Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds

> [!NOTE]
> Si l’ordinateur ne peut pas accéder à Internet, il n’est pas nécessaire de créer l’application dans Azure AD et d’exécuter Set-AIPAuthentication. Au lieu de cela, suivez les instructions pour les [ordinateurs déconnectés](clientv2-admin-guide-customizations.md#support-for-disconnected-computers).  

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir de l’aide sur les applets de commande lorsque vous êtes dans une session PowerShell, tapez `Get-Help <cmdlet name> -online`. Exemple : 

    Get-Help Set-AIPFileLabel -online

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Types de fichier pris en charge](clientv2-admin-guide-file-types.md)
