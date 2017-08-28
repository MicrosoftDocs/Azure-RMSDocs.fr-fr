---
title: "Utiliser PowerShell avec le client Azure Information Protection"
description: "Instructions et informations pour que les administrateurs gèrent le client Azure Information Protection à l’aide de PowerShell."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6077b9eba8ee04bf22c17612183f3d41b6b71e35
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2017
---
# <a name="using-powershell-with-the-azure-information-protection-client"></a>Utiliser PowerShell avec le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Quand vous installez le client Azure Information Protection, des commandes PowerShell sont installés automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installées avec le module PowerShell **AzureInformationProtection**. Ce module remplace le module de protection RMS installé avec l’outil de protection RMS. Si vous disposez de l’outil RMSProtection lorsque vous installez le client Azure Information Protection, le module RMSProtection est automatiquement désinstallé.

Le module AzureInformationProtection inclut toutes les applets de commande Rights Management de l’outil de protection RMS et trois nouvelles applets de commande qui utilisent le service Azure Information Protection (AIP) pour l’étiquetage :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|

Pour obtenir une liste de toutes les applets de commande et de l’aide associée, voir le [module Azure Information Protection](/powershell/module/azureinformationprotection). Dans une session PowerShell, saisissez `Get-Help <cmdlet name> -online` pour afficher l’aide la plus récente, ainsi que les langues prises en charge autres que l’anglais.  

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

Comme avec le module RMSProtection, la version actuelle du module AzureInformationProtection présente les limitations suivantes :

- Vous pouvez annuler la protection des dossiers personnels Outlook (fichiers .pst), mais vous ne pouvez pas actuellement protéger en mode natif ces fichiers ou d’autres fichiers de conteneur à l’aide de ce module PowerShell.

- Vous pouvez annuler la protection des e-mails Outlook protégés (fichiers .rpmsg) lorsqu’ils sont dans un dossier personnel Outlook (.pst), mais vous ne pouvez pas annuler la protection de fichiers .rpmsg en dehors d’un dossier personnel.

Avant de commencer à utiliser ces applets de commande, consultez les autres conditions préalables et instructions correspondant à votre déploiement :

- [Azure Information Protection et le service Azure Rights Management](#azure-information-protection-service-and-azure-rights-management-service)

    - Applicable si vous utilisez la classification uniquement ou la classification avec la protection Rights Management : vous avez un abonnement qui inclut Azure Information Protection (par exemple, Enterprise Mobility + Security).
    - S’applique si vous utilisez la protection uniquement avec le service Azure Rights Management : vous avez un abonnement qui inclut le service Azure Rights Management (par exemple, Office 365 E3 et Office 365 E5).

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - S’applique si vous utilisez la protection uniquement avec la version locale d’Azure Rights Management ; Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-and-azure-rights-management-service"></a>Azure Information Protection et le service Azure Rights Management

Lisez cette section avant de commencer à utiliser les commandes PowerShell quand votre organisation utilise Azure Information Protection pour la classification et la protection, ou seulement le service Azure Rights Management pour la protection des données.


### <a name="prerequisites"></a>Prérequis

En plus des prérequis pour l’installation du module Azure Information Protection, il existe d’autres prérequis pour l’étiquetage Azure Information Protection et pour le service de protection de données Azure Rights Management :

1. Le service Azure Rights Management doit être activé.

2. Pour supprimer la protection des fichiers pour les autres utilisateurs à l’aide de votre propre compte : 
    
    - La fonctionnalité de super utilisateur doit être activée pour votre organisation et votre compte doit être configuré pour être un super utilisateur d’Azure Rights Management.

3. Pour protéger ou ôter la protection des fichiers directement sans intervention de l’utilisateur : 
    
    - Créez un compte de principal de service, exécutez Set-RMSServerAuthentication et envisagez de faire de ce principal de service un super utilisateur pour Azure Rights Management.

4. 4. Pour les régions en dehors des États-Unis : 
    
    - Modifier le Registre pour la découverte de service.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Condition préalable 1 : le service Azure Rights Management doit être activé

Cette condition préalable s’applique si vous appliquez la protection des données à l’aide d’étiquettes ou en vous connectant directement au service Azure Rights Management.

Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions [d’activation d’Azure Rights Management](../deploy-use/activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Condition préalable 2 : supprimer la protection de fichiers pour les autres utilisateurs à l’aide de votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette. Toutefois, il est plus probable que vous vous connectiez directement au service Azure Rights Management pour supprimer la protection.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Condition préalable 3 : protéger ou annuler la protection des fichiers sans intervention de l’utilisateur

Vous pouvez vous connecter directement au service Azure Rights Management en mode non interactif pour protéger ou déprotéger des fichiers.

Vous devez utiliser un principal du service pour vous connecter au service Azure Rights Management en mode non interactif, en utilisant l’applet de commande `Set-RMSServerAuthentication`. Vous devez effectuer cette opération pour chaque session Windows PowerShell exécutant des applets de commande qui se connectent directement au service Azure Rights Management. Avant d’exécuter cette applet de commande, vous devez disposer de ces trois identificateurs :

- BposTenantId

- AppPrincipalId

- Clé symétrique

Vous pouvez utiliser les commandes PowerShell et les instructions commentées suivantes pour obtenir automatiquement les valeurs des identificateurs et exécuter l’applet de commande Set-RMSServerAuthentication. Vous pouvez aussi obtenir et spécifier manuellement les valeurs.

Pour obtenir les valeurs et exécuter Set-RMSServerAuthentication automatiquement :

````
# Make sure that you have the AADRM and MSOnline modules installed

$newServicePrincipalName="<new service principal name>"
Connect-AadrmService
$bposTenantID=(Get-AadrmConfiguration).BPOSId
Disconnect-AadrmService
New-MsolServicePrincipal -DisplayName $servicePrincipalName

# Copy the value of the generated symmetric key

$symmetricKey="<value from the display of the New-MsolServicePrincipal command>"
$appPrincipalID=(Get-MsolServicePrincipal | Where { $_.DisplayName -eq $servicePrincipalName }).AppPrincipalId
Set-RMSServerAuthentication -Key $symmetricKey -AppPrincipalId $appPrincipalID -BposTenantId $bposTenantID

````

Les sections suivantes expliquent comment obtenir et spécifier ces valeurs manuellement, avec plus d’informations sur chacune d’elles.

##### <a name="to-get-the-bpostenantid"></a>Pour obtenir le BposTenantId

Exécutez l’applet de commande Get-AadrmConfiguration à partir du module Azure RMS Windows PowerShell :

1. Si ce module n’est pas déjà installé sur votre ordinateur, consultez la page [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md).

2. Démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**.

3. Utilisez l’applet de commande `Connect-AadrmService` pour la connexion au service Azure Rights Management :
    
        Connect-AadrmService
    
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur du locataire Azure Information Protection. Normalement, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Office 365.
    
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
    
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur du locataire Azure AD (normalement, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Office 365).

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

    Il est important d’effectuer maintenant une copie de cette clé symétrique. Vous ne pourrez pas récupérer cette clé plus tard : si vous ne la connaissez pas lors de votre prochaine authentification auprès du service Azure Rights Management, vous devrez créer un nouveau principal du service.

À partir de ces instructions et de nos exemples, trois identificateurs sont nécessaires à l’exécution de Set-RMSServerAuthentication :

- ID de locataire : **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Clé symétrique : **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId : **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

Notre exemple de commande ressemblerait à ceci :

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

Comme indiqué dans la commande précédente, vous pouvez fournir les valeurs avec une seule commande, ou simplement saisir Set-RMSServerAuthentication et fournir les valeurs une par une lorsque vous y êtes invité. Quand la commande est terminée, vous voyez un message de type « **RmsServerAuthentication a la valeur ON** », ce qui signifie que le client fonctionne maintenant en « mode serveur ». Ce message ne confirme pas que l’authentification a abouti en utilisant les valeurs que vous avez fournies, mais que le passage au mode serveur a réussi.

Envisagez de faire de ce principal du service un super utilisateur : pour vous assurer que ce principal du service peut toujours annuler la protection de fichiers pour d’autres utilisateurs, il peut être configuré comme un super utilisateur. De la même façon que quand vous configurez un compte d’utilisateur standard comme super utilisateur, vous utilisez l’applet de commande Azure RMS [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md), mais vous spécifiez le paramètre **- ServicePrincipalId** avec votre valeur AppPrincipalId.

Pour plus d’informations sur les super utilisateurs, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../deploy-use/configure-super-users.md).

> [!NOTE]
> Pour utiliser votre propre compte pour vous authentifier auprès du service Azure Rights Management, inutile d’exécuter Set-RMSServerAuthentication avant de protéger ou d’annuler la protection de fichiers, ou d’obtenir des modèles.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Condition préalable 4 : pour les régions en dehors de l’Amérique du Nord

Quand vous utilisez un compte de principal de service pour protéger des fichiers et télécharger des modèles à l’extérieur de la région Azure Amérique du Nord, vous devez modifier le Registre : 

1. Exécutez de nouveau l’applet de commande Get-AadrmConfiguration et notez les valeurs pour **CertificationExtranetDistributionPointUrl** et **LicensingExtranetDistributionPointUrl**.

2. Sur tous les ordinateurs où vous allez exécuter les applets de commande AzureInformationProtection, ouvrez l’Éditeur du Registre et accédez à : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. Si vous ne voyez pas de clé **ServiceLocation**, créez-en une afin que le chemin d’accès du Registre soit **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. Pour la clé **ServiceLocation**, créez deux clés, le cas échéant, nommées **EnterpriseCertification** et **EnterprisePublishing**. 
    
    Pour la valeur de chaîne qui est automatiquement créée pour ces clés, ne modifiez pas le nom de « (Par défaut) », mais modifiez la chaîne pour définir les données de la valeur :

    - Pour **EnterpriseCertification**, collez votre valeur CertificationExtranetDistributionPointUrl.
    
    - Pour **EnterprisePublishing**, collez votre valeur LicensingExtranetDistributionPointUrl.
    
    Par exemple, votre entrée de Registre pour EnterpriseCertification doit être similaire à ceci :
    
    ![Modification du Registre pour le module PowerShell d’Azure Information Protection pour les régions en dehors de l’Amérique du Nord](../media/registry-example-rmsprotection.png)

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

Si vous n’avez pas exécuté la commande Set-RMSServerAuthentication, vous serez authentifié au service Azure Rights Management à l’aide de votre propre compte d’utilisateur. Si vous êtes sur un ordinateur joint au domaine, vos informations d’identification actuelles seront utilisées automatiquement. Si vous êtes sur un ordinateur de groupe de travail, vous serez invité à vous connecter à Azure, et ces informations d’identification seront ensuite mises en cache pour les commandes suivantes. Dans ce scénario, si vous avez besoin de vous connecter plus tard avec le compte d’un autre utilisateur, utilisez l’applet de commande `Clear-RMSAuthentication`.

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

Pour déprotéger un fichier, vous devez disposer des droits Propriétaire ou Extraction correspondant au moment où le fichier a été protégé, ou vous devez exécuter les applets de commande en tant que super utilisateur. Ensuite, utilisez l’applet de commande de suppression de la protection Unprotect. Exemple :

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

Tout d’abord, si vous comptez plus d’un déploiement d’AD RMS, vous devez disposer des noms de vos serveurs AD RMS. Utilisez l’applet de commande Get-RMSServer pour afficher la liste des serveurs disponibles :

    Get-RMSServer

Votre résultat peut ressembler à ce qui suit :

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

Avant de pouvoir protéger des fichiers, vous devez obtenir une liste des modèles RMS pour identifier celui à utiliser et le numéro d’identification correspondant. Vous devrez spécifier le serveur RMS également uniquement si vous comptez plus d’un déploiement d’AD RMS. 

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

Quand l’extension du nom de fichier n’est pas modifiée après l’application de la protection, vous pouvez toujours utiliser l’applet de commande Get-RMSFileStatus ultérieurement pour vérifier si le fichier est protégé. Exemple : 

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

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

À partir de la version 1.8.41.0 du client Azure Information Protection (actuellement en préversion), vous pouvez exécuter les applets de commande d’étiquetage de manière non interactive à l’aide de l’applet de commande **Set-AIPAuthentication**.

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive. Pour les exécuter sans assistance, créez un compte d’utilisateur Azure AD à cet effet. Ensuite, dans le contexte de cet utilisateur, exécutez l’applet de commande Set-AIPAuthentication pour définir et stocker les informations d’identification à l’aide d’un jeton d’accès Azure AD. Ce compte d’utilisateur est ensuite authentifié et initialisé pour le service Azure Rights Management. Le compte télécharge la stratégie Azure Information Protection et tous les modèles Rights Management utilisés par les étiquettes.

La première fois que vous exécutez cette applet de commande, vous êtes invité à vous connecter à Azure Information Protection. Spécifiez le nom et le mot de passe du compte d’utilisateur que vous avez créé pour l’utilisateur sans assistance. Ce compte peut alors exécuter les applets de commande d’étiquetage de manière non interactive jusqu’à ce que le jeton d’authentification expire. Lorsque le jeton expire, exécutez l’applet de commande pour acquérir un nouveau jeton :

Si vous exécutez cette applet de commande sans paramètres, le compte acquiert un jeton d’accès qui est valide 90 jours ou jusqu’à ce que votre mot de passe expire.  

Pour contrôler à quel moment le jeton d’accès expire, exécutez cette applet de commande avec des paramètres. Vous pouvez ainsi configurer le jeton d’accès pour qu’il expire au bout d’un an, de deux ans ou jamais. Cette configuration nécessite que vous disposiez de deux applications inscrites dans Azure Active Directory : une application de type **application web/API** et une **application native**. Les paramètres de cette applet de commande utilisent les valeurs de ces applications.

Après avoir exécuté cette applet de commande, vous pouvez exécuter les applets de commande d’étiquetage dans le contexte du compte d’utilisateur que vous avez créé.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Pour créer et configurer les applications Azure AD pour Set-AIPAuthentication

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure AD que vous utilisez avec Azure Information Protection, accédez à **Azure Active Directory** > **Inscriptions des applications**. 

3. Sélectionnez **Nouvelle inscription d’application** pour créer votre application web/API. Dans l’étiquette **Créer**, spécifiez les valeurs suivantes, puis cliquez sur **Créer** :
    
    - Nom : **AIPOnBehalfOf**
    
    Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - Type d’application : **Application/API web**
    
    - URL de connexion : **http://localhost**

4. Sélectionnez l’application que vous venez de créer, par exemple **AIPOnBehalfOf**. Ensuite, dans le panneau **Paramètres**, sélectionnez **Propriétés**. Dans le panneau **Propriétés**, copiez la valeur du champ **ID d’application**, puis fermez ce panneau. 
    
    Cette valeur est utilisée pour le paramètre `WebAppId` lorsque vous exécutez l’applet de commande Set-AIPAuthentication.

5. Dans le panneau **Paramètres**, sélectionnez **Clés**. Ajoutez une nouvelle clé en spécifiant une description et la durée de votre choix (1 an, 2 ans ou sans expiration). Ensuite, sélectionnez **Enregistrer**, puis copiez la chaîne correspondant à la **Valeur** qui s’affiche. Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toute autre clé que vous utilisez, stockez la valeur enregistrée dans un endroit sûr et limitez l’accès à cette valeur.
    
    Cette valeur est utilisée pour le paramètre `WebAppKey` lorsque vous exécutez l’applet de commande Set-AIPAuthentication.

6. Dans le panneau **Inscriptions des applications**, sélectionnez **Nouvelle inscription d’application** pour créer votre application native. Dans l’étiquette **Créer**, spécifiez les valeurs suivantes, puis cliquez sur **Créer** :
    
    - Nom : **AIPClient**
    
    Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - Type d’application : **Native**
    
    - URL de connexion : **http://localhost**

7. Sélectionnez l’application que vous venez de créer, par exemple **AIPClient**. Ensuite, dans le panneau **Paramètres**, sélectionnez **Propriétés**. Dans le panneau **Propriétés**, copiez la valeur du champ **ID d’application**, puis fermez ce panneau.
    
    Cette valeur est utilisée pour le paramètre `NativeAppId` lorsque vous exécutez l’applet de commande Set-AIPAuthentication.

8. Dans le panneau **Paramètres**, sélectionnez **Autorisations nécessaires**. 

9. Dans le panneau **Autorisations nécessaires**, cliquez sur **Ajouter**, puis cliquez sur **Sélectionner une API**. Dans la zone de recherche, tapez **AIPOnBehalfOf**. Sélectionnez cette valeur dans la zone de liste, puis cliquez sur **Sélectionner**.

10. Dans le panneau **Activer l’accès**, sélectionnez **AIPOnBehalfOf**, cliquez sur **Sélectionner**, puis cliquez sur **Terminé**.
    
    Vous venez de terminer la configuration des deux applications, et vous disposez des valeurs dont vous avez besoin pour exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec des paramètres.


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir de l’aide concernant les applets de commande lorsque vous avez ouvert une session PowerShell, tapez `Get-Help <cmdlet name> cmdlet`, puis utilisez le paramètre -online pour lire les informations les plus récentes. Exemple : 

    Get-Help Get-RMSTemplate -online

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichier pris en charge](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
