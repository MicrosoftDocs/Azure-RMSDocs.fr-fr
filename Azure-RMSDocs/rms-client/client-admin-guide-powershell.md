---
title: "Utiliser PowerShell avec le client Azure Information Protection"
description: "Instructions et informations pour que les administrateurs gèrent le client Azure Information Protection à l’aide de PowerShell."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/01/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 04e04f6e3243283b98df94143773e4aa81351f48
ms.sourcegitcommit: b471c20eda011a7b75ee801c34081fb4773b64dc
ms.translationtype: HT
ms.contentlocale: fr-FR
---
# <a name="using-powershell-with-the-azure-information-protection-client"></a>Utiliser PowerShell avec le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Lorsque vous installez le client Azure Information Protection, les commandes PowerShell sont installées automatiquement afin que vous puissiez gérer le client en exécutant des commandes que vous pouvez placer dans des scripts pour l’automatisation.

Les applets de commande sont installées avec le module PowerShell **AzureInformationProtection**, qui remplace le module RMSProtection installé avec l’outil de protection RMS. Si vous disposez de l’outil RMSProtection lorsque vous installez le client Azure Information Protection, le module RMSProtection est automatiquement désinstallé.

Le module AzureInformationProtection inclut toutes les applets de commande Rights Management de l’outil de protection RMS et deux nouvelles applets de commande qui utilisent le service Azure Information Protection (AIP) pour l’étiquetage :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|

Pour obtenir une liste de toutes les cmdlets et de l’aide associée, voir le [module Azure Information Protection](/powershell/azureinformationprotection/vlatest/aip).

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

Comme avec le module RMSProtection, la version actuelle du module AzureInformationProtection présente les limitations suivantes :

- Vous pouvez annuler la protection des dossiers personnels Outlook (fichiers .pst), mais vous ne pouvez pas actuellement protéger en mode natif ces fichiers ou d’autres fichiers de conteneur à l’aide de ce module PowerShell.

- Vous pouvez annuler la protection des e-mails Outlook protégés (fichiers .rpmsg) lorsqu’ils sont dans un dossier personnel Outlook (.pst), mais vous ne pouvez pas annuler la protection de fichiers .rpmsg en dehors d’un dossier personnel.

Avant de commencer à utiliser ces applets de commande, consultez les autres conditions préalables et instructions correspondant à votre déploiement :

- [Service Azure Information Protection et service Azure Rights Management](#azure-information-protection-service-and-azure-rights-management-service)

    - Applicable si vous utilisez la classification uniquement ou la classification avec la protection Rights Management : vous avez un abonnement qui inclut Azure Information Protection (par exemple, Enterprise Mobility + Security).
    - S’applique si vous utilisez la protection uniquement avec le service Azure Rights Management : vous avez un abonnement qui inclut le service Azure Rights Management (par exemple, Office 365 E3 et Office 365 E5).

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - S’applique si vous utilisez la protection uniquement avec la version locale d’Azure Rights Management ; Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Service Azure Information Protection et service Azure Rights Management

Lisez cette section avant de commencer à utiliser les commandes PowerShell lorsque votre organisation utilise Azure Information Protection et le service de protection de données Azure Rights Management, ou seulement le service Azure Rights Management.


### <a name="prerequisites"></a>Prérequis

Outre la configuration requise pour l’installation du module AzureInformationProtection, des conditions préalables supplémentaires existent pour le service Azure Information Protection et le service de protection de données Azure Rights Management :

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 
    
    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

3. Pour protéger ou ôter la protection des fichiers directement sans intervention de l’utilisateur : 
    
    - Créez un compte de principal de service, exécutez Set-RMSServerAuthentication et envisagez de faire de ce principal de service un super utilisateur pour Azure Rights Management.

4. Pour les régions en dehors de l’Amérique du Nord : 
    
    - Modifiez le Registre pour l’authentification auprès du service.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Condition préalable 1 : le service Azure Rights Management doit être activé

Cette condition préalable s’applique si vous appliquez la protection des données à l’aide d’étiquettes ou en vous connectant directement au service Azure Rights Management.

Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions [d’activation d’Azure Rights Management](../deploy-use/activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Condition préalable 2 : supprimer la protection de fichiers pour les autres utilisateurs à l’aide de votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette. Toutefois, il est plus probable que vous vous connectiez directement au service Azure Rights Management pour supprimer la protection.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Condition préalable 3 : protéger ou annuler la protection des fichiers sans intervention de l’utilisateur

Actuellement, vous ne pouvez pas appliquer d’étiquettes en mode non interactif, mais vous pouvez vous connecter directement au service Azure Rights Management en mode non interactif pour protéger ou annuler la protection de fichiers.

Vous devez utiliser un principal du service pour vous connecter au service Azure Rights Management en mode non interactif, en utilisant l’applet de commande `Set-RMSServerAuthentication`. Vous devez effectuer cette opération pour chaque session Windows PowerShell exécutant des applets de commande qui se connectent directement au service Azure Rights Management. Avant d’exécuter cette applet de commande, assurez-vous que vous disposez des trois identificateurs suivants :

- BposTenantId

- AppPrincipalId

- Clé symétrique

Les sections suivantes expliquent comment obtenir ces identificateurs.

##### <a name="to-get-the-bpostenantid"></a>Pour obtenir le BposTenantId

Exécutez l’applet de commande Get-AadrmConfiguration à partir du module Azure RMS Windows PowerShell :

1. Si ce module n’est pas déjà installé sur votre ordinateur, consultez la page [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. Démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Utilisez l’applet de commande `Connect-AadrmService` pour la connexion au service Azure Rights Management :
    
        Connect-AadrmService
    
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client Azure Information Protection (en général, vous utilisez un compte d’administrateur global pour Azure Active Directory ou Office 365).
    
4. Exécutez `Get-AadrmConfiguration` et copiez la valeur BPOSId.
    
    Voici un exemple de sortie de Get-AadrmConfiguration :
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. Déconnectez-vous du service :
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Pour obtenir l’AppPrincipalId et la clé symétrique

Créez un principal de service en exécutant l’applet de commande `New-MsolServicePrincipal` à partir du module MSOnline PowerShell pour Azure Active Directory et suivez les instructions ci-dessous. 

> [!IMPORTANT]
> N’utilisez pas l’applet de commande Azure AD PowerShell la plus récente, New-AzureADServicePrincipal, pour créer ce principal de service. Le service Azure Rights Management ne prend pas en charge New-AzureADServicePrincipal. 

1. Si le module MSOnline n’est pas déjà installé sur votre ordinateur, exécutez `Install-Module MSOnline`.

2. Démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Utilisez l’applet de commande **Connect-MsolService** pour vous connecter à Azure AD :
    
        Connect-MsolService
    
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur client Azure AD (en général, vous utilisez un compte d’administrateur global pour Azure Active Directory ou Office 365).

4. Exécutez l’applet de commande New-MsolServicePrincipal pour créer un principal du service :
    
        New-MsolServicePrincipal
    
    Lorsque vous y êtes invité, entrez le nom d’affichage de votre choix pour ce principal du service, qui vous aidera à identifier son objectif ultérieurement en tant que compte de connexion au service Azure Rights Management afin que vous puissiez protéger et annuler la protection de fichiers.
    
    Un exemple de la sortie de New-MsolServicePrincipal :
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. À partir de cette sortie, notez la clé symétrique et l’AppPrincipalId.

    Il est particulièrement important de copier la clé symétrique, car vous ne pourrez pas la récupérer complètement ultérieurement. Si vous ne le connaissez pas, vous devez créer un principal du service lors de votre prochaine authentification auprès du service Azure Rights Management.

À partir de ces instructions et de nos exemples, trois identificateurs sont nécessaires à l’exécution de Set-RMSServerAuthentication :

- ID de locataire : **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Clé symétrique : **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId : **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

Notre exemple de commande ressemblerait à ceci :

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

Comme indiqué dans la commande précédente, vous pouvez fournir les valeurs avec une seule commande, ou simplement saisir Set-RMSServerAuthentication et fournir les valeurs une par une lorsque vous y êtes invité. Quand la commande est terminée, vous voyez un message de type « **RmsServerAuthentication a la valeur ON** », ce qui signifie que le client fonctionne maintenant en « mode serveur ». Ce message ne confirme pas que l’authentification a abouti en utilisant les valeurs que vous avez fournies, mais que le passage au mode serveur a réussi.

Envisagez de faire de ce principal du service un super utilisateur : pour vous assurer que ce principal du service peut toujours annuler la protection de fichiers pour d’autres utilisateurs, il peut être configuré comme un super utilisateur. De la même façon, lorsque vous configurez un compte d’utilisateur standard comme un super utilisateur, vous utilisez l’applet de commande Azure RMS [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md), mais vous spécifiez le paramètre **- ServicePrincipalId** avec votre valeur AppPrincipalId.

Pour plus d’informations sur les super utilisateurs, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

> [!NOTE]
> Pour utiliser votre propre compte pour vous authentifier auprès du service Azure Rights Management, inutile d’exécuter Set-RMSServerAuthentication avant de protéger ou d’annuler la protection de fichiers, ou d’obtenir des modèles.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Condition préalable 4 : pour les régions en dehors de l’Amérique du Nord

Pour l’authentification en dehors de la région Amérique du Nord Azure, vous devez modifier le Registre comme suit. Si votre locataire Azure Information Protection est en Amérique du Nord, n’effectuez pas cette étape :

1. Exécutez de nouveau l’applet de commande Get-AadrmConfiguration et notez les valeurs pour **CertificationExtranetDistributionPointUrl** et **LicensingExtranetDistributionPointUrl**.

2. Sur chaque ordinateur sur lequel vous allez exécuter les applets de commande AzureInformationProtection, ouvrez l’Éditeur du Registre et accédez à : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. Si vous ne voyez pas de clé **ServiceLocation**, créez-en une afin que le chemin d’accès du Registre soit **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. Pour la clé **ServiceLocation**, créez deux clés, le cas échéant, nommées **EnterpriseCertification** et **EnterprisePublishing**. 
    
    Lorsque vous créez ces clés REG_SZ, ne modifiez pas le nom (« Par défaut »), mais définissez les données Valeur :

    - Pour **EnterpriseCertification**, collez votre valeur CertificationExtranetDistributionPointUrl.
    
    - Pour **EnterprisePublishing**, collez votre valeur LicensingExtranetDistributionPointUrl.

5. Fermez l'éditeur du Registre. Il est inutile de redémarrer votre ordinateur. Toutefois, si vous utilisez un compte de principal du service au lieu de votre propre compte d’utilisateur, vous devez exécuter la commande Set-RMSServerAuthentication après avoir effectué cette modification de Registre.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Exemples de scénarios d’utilisation des applets de commande pour Azure Information Protection et le service Azure Rights Management

Il est plus efficace d’utiliser des étiquettes pour classifier et protéger les fichiers, car il existe deux applets de commande dont vous avez besoin. Elles peuvent être exécutées seules ou ensemble : [Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus) et [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Consultez l’aide de ces deux applets de commande pour plus d’informations et d’exemples.

Toutefois, pour protéger ou annuler la protection de fichiers en vous connectant directement au service Azure Rights Management, vous devez généralement exécuter une série d’applets de commande comme décrit ci-après.

Tout d’abord, si vous avez besoin de vous authentifier auprès du service Azure Rights Management avec un principal du service au lieu d’utiliser votre propre compte, dans une session PowerShell, saisissez :

    Set-RMSServerAuthentication

Lorsque vous y êtes invité, entrez les trois identificateurs, comme décrit dans [Condition préalable 3 : protéger ou annuler la protection des fichiers sans intervention de l’utilisateur](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Avant de pouvoir protéger les fichiers, vous devez télécharger les modèles Rights Management sur votre ordinateur, puis identifier celui à utiliser ainsi que le numéro d’identification correspondant. À partir du résultat, vous pouvez alors copier l’ID du modèle :

    Get-RMSTemplate
    
Votre résultat peut ressembler à ce qui suit :

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Si vous n’avez pas exécuté la commande Set-RMSServerAuthentication, vous serez authentifié au service Azure Rights Management à l’aide de votre propre compte d’utilisateur. Si vous êtes sur un ordinateur joint au domaine, vos informations d’identification en cours seront toujours utilisées automatiquement. Si vous êtes sur un ordinateur de groupe de travail, vous serez invité à vous connecter à Azure, et ces informations d’identification seront ensuite mises en cache pour les commandes suivantes. Dans ce scénario, si vous avez besoin de vous connecter plus tard avec le compte d’un autre utilisateur, utilisez l’applet de commande `Clear-RMSAuthentication`.

Maintenant que vous connaissez l’ID du modèle, vous pouvez l’utiliser avec l’applet de commande `Protect-RMSFile` pour protéger un seul fichier ou tous les fichiers d’un dossier. Par exemple, si vous souhaitez protéger un seul fichier et remplacer l’original, en utilisant le modèle « Contoso, Ltd - Confidential » :

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

Votre résultat peut ressembler à ce qui suit :

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

Pour protéger tous les fichiers d’un dossier, utilisez le paramètre **-Folder** avec une lettre de lecteur et un chemin d’accès, ou le chemin d’accès UNC. Exemple :

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

Votre résultat peut ressembler à ce qui suit :

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

Lorsque l’extension du nom de fichier n’est pas modifiée après l’application de la protection, vous pouvez toujours utiliser l’applet de commande `Get-RMSFileStatus` plus tard pour vérifier si le fichier est protégé. Exemple :

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

Votre résultat peut ressembler à ce qui suit :

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

Pour annuler la protection d’un fichier, vous devez disposer de droits de propriétaire ou d’extraction à partir du moment où le fichier a été protégé, ou vous devez exécuter les applets de commande en tant que super utilisateur. Ensuite, utilisez l’applet de commande de suppression de la protection Unprotect. Exemple :

    Unprotect-RMSFile C:\test.docx -InPlace

Votre résultat peut ressembler à ce qui suit :

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

Notez que si les modèles Rights Management sont modifiés, vous devez les télécharger à nouveau à l’aide de `Get-RMSTemplate -force`. 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management Services

Lisez cette section avant de commencer à utiliser les commandes PowerShell pour protéger ou annuler la protection des fichiers, lorsque votre organisation utilise simplement Active Directory Rights Management Services.


### <a name="prerequisites"></a>Prérequis

Outre la configuration requise pour l’installation du module AzureInformationProtection, votre compte doit disposer des autorisations de lecture et d’exécution pour accéder à ServerCertification.asmx :

1. Connectez-vous à un serveur AD RMS.

2. Cliquez sur **Démarrer**, puis sur **Ordinateur**.

3. Dans l’Explorateur de fichiers, accédez à %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Cliquez avec le bouton droit sur **ServerCertification.asmx**, puis sur **Propriétés**.

5. Dans la boîte de dialogue **Propriétés de ServerCertification.asmx**, cliquez sur l’onglet **Sécurité**. 

6. Cliquez sur le bouton **Continuer** ou sur le bouton **Modifier**. 

7. Dans la boîte de dialogue **Autorisations de ServerCertification.asmx**, cliquez sur **Ajouter**. 

8. Ajoutez le nom de votre compte. Si d’autres administrateurs AD RMS vont également utiliser ces applets de commande pour protéger et annuler la protection de fichiers, ajoutez leurs noms également.

9. Dans la colonne **Autoriser**, assurez-vous que les cases à cocher **Lecture et exécution** et **Lecture** sont sélectionnées.

10.Cliquez deux fois sur **OK**.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Exemples de scénarios d’utilisation des applets de commande pour les services Active Directory Rights Management Services

Un scénario standard pour ces applets de commande consiste à protéger tous les fichiers dans un dossier à l’aide d’un modèle de stratégie de droits, ou à annuler la protection d’un fichier. 

Tout d’abord, si vous comptez plus d’un déploiement d’AD RMS, vous devez disposer des noms de vos serveurs AD RMS. Utilisez l’applet de commande Get-RMSServer pour afficher une liste des serveurs disponibles :

    Get-RMSServer

Votre résultat peut ressembler à ce qui suit :

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

Avant de pouvoir protéger des fichiers, vous devez obtenir une liste des modèles RMS pour identifier celui à utiliser et le numéro d’identification correspondant. Vous devrez spécifier le serveur RMS également uniquement si vous comptez plus d’un déploiement d’AD RMS. 

À partir du résultat, vous pouvez alors copier l’ID du modèle :

    Get-RMSTemplate -RMSServer RmsContoso

Votre résultat peut ressembler à ce qui suit :

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Maintenant que vous connaissez l’ID du modèle, vous pouvez l’utiliser avec l’applet de commande Protect-RMSFile pour protéger un seul fichier ou tous les fichiers d’un dossier. Par exemple, si vous souhaitez protéger un seul fichier et remplacer l’original, en utilisant le modèle « Contoso, Ltd - Confidential » :

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

Votre résultat peut ressembler à ce qui suit :

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

Pour protéger tous les fichiers d’un dossier, utilisez le paramètre -Folder avec une lettre de lecteur et un chemin d’accès, ou le chemin d’accès UNC. Exemple :

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

Votre résultat peut ressembler à ce qui suit :

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

Lorsque l’extension du nom de fichier n’est pas modifiée après l’application de la protection RMS, vous pouvez toujours utiliser l’applet de commande Get-RMSFileStatus plus tard pour vérifier si le fichier est protégé. Exemple : 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

Votre résultat peut ressembler à ce qui suit :

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

Pour annuler la protection d’un fichier, vous devez disposer de droits de propriétaire ou d’extraction à partir du moment où le fichier a été protégé, ou être super utilisateur AD RMS. Ensuite, utilisez l’applet de commande de suppression de la protection Unprotect. Exemple :

    Unprotect-RMSFile C:\test.docx -InPlace

Votre résultat peut ressembler à ce qui suit :

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir l’aide de l’applet de commande lorsque vous êtes dans une session PowerShell, utilisez l’applet de commande Get-Help <cmdlet name>, où <cmdlet name> est le nom de l’applet de commande que vous souhaitez rechercher. Exemple : 

    Get-Help Get-RMSTemplate

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
