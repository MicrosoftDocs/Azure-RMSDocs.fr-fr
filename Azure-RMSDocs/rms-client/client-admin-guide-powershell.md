---
title: Utiliser PowerShell avec le client Azure Information Protection Classic
description: Instructions et informations permettant aux administrateurs de gérer le client Azure Information Protection Classic à l’aide de PowerShell.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/31/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ROBOTS: NOINDEX
ms.subservice: v1client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7df480389741a900326477e8d6088ac9dc6da596
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98808666"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-classic-client"></a>Guide de l’administrateur : utilisation de PowerShell avec le client Azure Information Protection Classic

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Concerne :** [Azure information protection client classique pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez le [Guide d’administration du client d’étiquetage unifié](clientv2-admin-guide-powershell.md). *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Lorsque vous installez le client Azure Information Protection Classic, les commandes PowerShell sont installées automatiquement. Vous pouvez ainsi gérer le client en exécutant des commandes que vous pouvez placer dans des scripts d’automatisation.

Les applets de commande sont installées avec le module PowerShell **AzureInformationProtection**. Ce module comprend toutes les applets de commande Rights Management de l’outil de protection RMS (qui n’est plus pris en charge). Il propose également des applets de commande qui utilisent Azure Information Protection pour l’étiquetage. Par exemple :

|Étiquetage des applets de commande|Exemple d’utilisation|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|Dans le cas d’un dossier partagé, identifiez tous les fichiers avec une étiquette spécifique.|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|Pour un dossier partagé, inspectez le contenu du fichier puis étiquetez automatiquement les fichiers sans étiquette, selon les conditions que vous avez spécifiées.|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|Pour un dossier partagé, appliquez une étiquette spécifiée à tous les fichiers dépourvus d’étiquette.|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|Étiquetez les fichiers de manière non interactive, par exemple à l’aide d’un script qui s’exécute selon une planification.|

> [!TIP]
> Pour utiliser des applets de commande avec des chemins comprenant plus de 260 caractères, utilisez le [paramètre de stratégie de groupe](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) disponible à compter de la version 1607 de Windows 10 :<br /> Stratégie de l' **ordinateur local**  >  Configuration de l' **ordinateur**  >  **Modèles d’administration**  >  **Tous les paramètres**  >  **Activer les chemins d’accès longs Win32** 
> 
> Pour Windows Server 2016, vous pouvez utiliser le même paramètre de stratégie de groupe lorsque vous installez les derniers modèles d’administration (.admx) pour Windows 10.
>
> Pour plus d’informations, consultez la section consacréee à la [longueur maximale des chemins](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation) dans la documentation pour développeurs Windows 10.

Le [scanneur Azure Information Protection](../deploy-aip-scanner.md) utilise les applets de commande du module AzureInformationProtection pour installer et configurer un service sur Windows Server. Ce scanneur vous permet de découvrir, classifier et protéger des fichiers sur des magasins de données.

Pour obtenir une liste de toutes les cmdlets et de l’aide associée, voir le [module Azure Information Protection](/powershell/module/azureinformationprotection). Dans une session PowerShell, tapez `Get-Help <cmdlet name> -online` pour afficher l’aide la plus récente.  

Ce module s’installe dans **\ProgramFiles (x86)\Microsoft Azure Information Protection** et ajoute ce dossier à la variable système **PSModulePath**. Le fichier .dll de ce module est nommé **AIP.dll**.

Actuellement, si vous installez le module en tant qu’un certain utilisateur et que vous exécutez les applets de commande sur le même ordinateur en tant qu’un autre utilisateur, vous devez d’abord exécuter la commande `Import-Module AzureInformationProtection`. Dans ce scénario, le module ne se charge pas automatiquement quand vous exécutez d’abord une applet de commande.

Avant de commencer à utiliser ces applets de commande, consultez les autres conditions préalables et instructions correspondant à votre déploiement :

- [Azure Information Protection et le service Azure Rights Management](#azure-information-protection-and-azure-rights-management-service)

    - Applicable si vous utilisez la classification uniquement ou la classification avec la protection Rights Management : vous avez un abonnement qui inclut Azure Information Protection (par exemple, Enterprise Mobility + Security).
    - S’applique si vous utilisez la protection uniquement avec le service Azure Rights Management : vous avez un abonnement qui inclut le service Azure Rights Management (par exemple, Office 365 E3 et Office 365 E5).

- [Services AD RMS (Active Directory Rights Management Services)](#active-directory-rights-management-services)

    - S’applique si vous utilisez la protection uniquement avec la version locale d’Azure Rights Management ; Active Directory Rights Management Services (AD RMS).

Pour plus d’informations, consultez la collection appropriée de [Azure information protection problèmes connus](../known-issues.md#powershell-support-for-the-azure-information-protection-client).

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

Si votre locataire Azure Information Protection n’est pas activé, consultez les instructions relatives à l' [activation du service de protection à partir de Azure information protection](../activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Condition préalable 2 : supprimer la protection de fichiers pour les autres utilisateurs à l’aide de votre propre compte

Les scénarios classiques de suppression de la protection des fichiers pour les autres utilisateurs incluent la détection de données ou la récupération de données. Si vous utilisez des étiquettes pour appliquer la protection, vous pouvez supprimer la protection en définissant une nouvelle étiquette qui n’applique pas la protection ou en supprimant l’étiquette. Toutefois, il est plus probable que vous vous connectiez directement au service Azure Rights Management pour supprimer la protection.

Pour supprimer la protection des fichiers, vous devez disposer d’un droit d’utilisation Rights Management ou être un super utilisateur. Pour la découverte de données ou la récupération de données, la fonctionnalité de super utilisateur est généralement utilisée. Pour activer cette fonctionnalité et configurer votre compte pour un super utilisateur, consultez [Configuration de super utilisateurs pour Azure Rights Management et les services de découverte ou la récupération de données](../configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Condition préalable 3 : protéger ou annuler la protection des fichiers sans intervention de l’utilisateur

Vous pouvez vous connecter directement au service Azure Rights Management en mode non interactif pour protéger ou déprotéger des fichiers.

Vous devez utiliser un principal de service pour vous connecter au service Azure Rights Management de manière non interactive (à l’aide de l’applet de commande `Set-RMSServerAuthentication`). Vous devez effectuer cette opération pour chaque session Windows PowerShell exécutant des applets de commande qui se connectent directement au service Azure Rights Management. Avant d’exécuter cette applet de commande, vous devez disposer de ces trois identificateurs :

- BposTenantId

- AppPrincipalId

- Clé symétrique

Vous pouvez utiliser les commandes PowerShell et les instructions commentées suivantes pour obtenir automatiquement les valeurs des identificateurs et exécuter l’applet de commande Set-RMSServerAuthentication. Vous pouvez aussi obtenir et spécifier manuellement les valeurs.

Pour obtenir les valeurs et exécuter Set-RMSServerAuthentication automatiquement :

```ps
# Make sure that you have the AIPService and MSOnline modules installed

$ServicePrincipalName="<new service principal name>"
Connect-AipService
$bposTenantID=(Get-AipServiceConfiguration).BPOSId
Disconnect-AipService
Connect-MsolService
New-MsolServicePrincipal -DisplayName $ServicePrincipalName

# Copy the value of the generated symmetric key

$symmetricKey="<value from the display of the New-MsolServicePrincipal command>"
$appPrincipalID=(Get-MsolServicePrincipal | Where { $_.DisplayName -eq $ServicePrincipalName }).AppPrincipalId
Set-RMSServerAuthentication -Key $symmetricKey -AppPrincipalId $appPrincipalID -BposTenantId $bposTenantID
```

Les sections suivantes expliquent comment obtenir et spécifier ces valeurs manuellement, avec plus d’informations sur chacune d’elles.

##### <a name="to-get-the-bpostenantid"></a>Pour obtenir le BposTenantId

Exécutez l’applet de commande Get-AipServiceConfiguration à partir du module Azure RMS Windows PowerShell :

1. Si ce module n’est pas déjà installé sur votre ordinateur, consultez [installation du module PowerShell AIPService](../install-powershell.md).

2. Démarrez Windows PowerShell avec l’option **exécuter en tant qu’administrateur** .

3. Utilisez l’applet de commande `Connect-AipService` pour la connexion au service Azure Rights Management :
   ```ps 
    Connect-AipService
    ```

    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur du locataire Azure Information Protection. En règle générale, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Microsoft 365.
    
4. Exécutez `Get-AipServiceConfiguration` et copiez la valeur BPOSId.
    
    Exemple de sortie de la AipServiceConfiguration :

    ```ps    
    BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
    RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
    LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
    LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
    CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
    CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
    ```

5. Déconnectez-vous du service :

    ```
    Disconnect-AipService
    ```

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Pour obtenir l’AppPrincipalId et la clé symétrique

Créez un principal de service en exécutant l’applet de commande `New-MsolServicePrincipal` à partir du module MSOnline PowerShell pour Azure Active Directory et suivez les instructions ci-dessous. 

> [!IMPORTANT]
> N’utilisez pas l’applet de commande Azure AD PowerShell la plus récente, New-AzureADServicePrincipal, pour créer ce principal de service. Le service Azure Rights Management ne prend pas en charge New-AzureADServicePrincipal. 

1. Si le module MSOnline n’est pas déjà installé sur votre ordinateur, exécutez `Install-Module MSOnline`.

2. Démarrez Windows PowerShell avec l’option **exécuter en tant qu’administrateur** .

3. Utilisez l’applet de commande **Connect-MsolService** pour vous connecter à Azure AD :

    ```ps
    Connect-MsolService
    ```

    Lorsque vous y êtes invité, entrez vos informations d’identification d’administrateur client Azure AD (en général, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Microsoft 365).

4. Exécutez l’applet de commande New-MsolServicePrincipal pour créer un principal du service :

    ```ps
    New-MsolServicePrincipal
    ```

    Lorsque vous y êtes invité, entrez le nom d’affichage de votre choix pour ce principal du service, qui vous aidera à identifier son objectif ultérieurement en tant que compte de connexion au service Azure Rights Management afin que vous puissiez protéger et annuler la protection de fichiers.

    Un exemple de la sortie de New-MsolServicePrincipal :

    ```ps
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
    ```

5. À partir de cette sortie, notez la clé symétrique et l’AppPrincipalId.

    Il est important d’effectuer maintenant une copie de cette clé symétrique. Vous ne pourrez pas récupérer cette clé plus tard : si vous ne la connaissez pas lors de votre prochaine authentification auprès du service Azure Rights Management, vous devrez créer un nouveau principal du service.

À partir de ces instructions et de nos exemples, trois identificateurs sont nécessaires à l’exécution de Set-RMSServerAuthentication :

- ID de locataire : **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Clé symétrique : **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId : **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

Notre exemple de commande ressemblerait à ceci :

```ps
Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42
```

Comme indiqué dans la commande précédente, vous pouvez fournir les valeurs avec une seule commande en utilisant un script à exécuter en mode non interactif. Mais pour les besoins du test, vous pouvez simplement taper Set-RMSServerAuthentication et fournir les valeurs une par une quand vous y êtes invité. Quand la commande est terminée, le client fonctionne en « mode serveur », qui convient à une utilisation non interactive comme les scripts et l’infrastructure de classification des fichiers Windows Server.

Envisagez de faire de ce compte de principal de service un super utilisateur : pour vérifier que ce compte peut toujours déprotéger des fichiers pour d’autres utilisateurs, vous pouvez le configurer comme super utilisateur. De la même façon que vous configurez un compte d’utilisateur standard comme super utilisateur, vous utilisez la même applet de commande Azure RMS, [Add-AipServiceSuperUser](/powershell/module/aipservice/add-aipservicesuperuser), mais vous spécifiez le paramètre **ServicePrincipalId** avec votre valeur AppPrincipalId.

Pour plus d’informations sur les super utilisateurs, consultez [configuration de super utilisateurs pour les Azure information protection et les services de découverte ou la récupération de données](../configure-super-users.md).

> [!NOTE]
> Pour utiliser votre propre compte pour vous authentifier auprès du service Azure Rights Management, inutile d’exécuter Set-RMSServerAuthentication avant de protéger ou d’annuler la protection de fichiers, ou d’obtenir des modèles.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Condition préalable 4 : pour les régions en dehors de l’Amérique du Nord

Quand vous utilisez un compte de principal de service pour protéger des fichiers et télécharger des modèles à l’extérieur de la région Azure Amérique du Nord, vous devez modifier le Registre : 

1. Exécutez à nouveau l’applet de commande Get-AipServiceConfiguration et prenez note des valeurs pour **CertificationExtranetDistributionPointUrl** et **LicensingExtranetDistributionPointUrl**.

2. Sur tous les ordinateurs où vous allez exécuter les applets de commande AzureInformationProtection, ouvrez l’Éditeur du Registre.

3. Accédez à la clé de Registre suivante : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation`. 

    Si vous ne voyez pas la clé **MSIPC** ni la clé **ServiceLocation**, créez-les.

4. Pour la clé **ServiceLocation**, créez deux clés, le cas échéant, nommées **EnterpriseCertification** et **EnterprisePublishing**. 

    Pour la valeur de chaîne qui est automatiquement créée pour ces clés, ne modifiez pas le nom de « (Par défaut) », mais modifiez la chaîne pour définir les données de la valeur :

   - Pour **EnterpriseCertification**, collez votre valeur CertificationExtranetDistributionPointUrl.

   - Pour **EnterprisePublishing**, collez votre valeur LicensingExtranetDistributionPointUrl.

     Par exemple, votre entrée de Registre pour EnterpriseCertification doit être similaire à ceci :

     ![Modification du Registre pour le module PowerShell d’Azure Information Protection pour les régions en dehors de l’Amérique du Nord](../media/registry-example-rmsprotection.png)

5. Fermez l'éditeur du Registre. Il est inutile de redémarrer votre ordinateur. Toutefois, si vous utilisez un compte de principal du service au lieu de votre propre compte d’utilisateur, vous devez exécuter la commande Set-RMSServerAuthentication après avoir effectué cette modification de Registre.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Exemples de scénarios d’utilisation des applets de commande pour Azure Information Protection et le service Azure Rights Management

Il est plus efficace d’utiliser des étiquettes pour classifier et protéger des fichiers, car il n’y a que deux cmdlets dont vous avez besoin, qui peuvent être exécutées de manière autonome ou conjointe : [AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) et [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Consultez l’aide de ces deux applets de commande pour plus d’informations et d’exemples.

Toutefois, pour protéger ou annuler la protection de fichiers en vous connectant directement au service Azure Rights Management, vous devez généralement exécuter une série d’applets de commande comme décrit ci-après.

Tout d’abord, si vous avez besoin de vous authentifier auprès du service Azure Rights Management avec un compte de principal de service au lieu d’utiliser votre propre compte, dans une session PowerShell, tapez :

```ps
Set-RMSServerAuthentication
```

Lorsque vous y êtes invité, entrez les trois identificateurs, comme décrit dans [Condition préalable 3 : protéger ou annuler la protection des fichiers sans intervention de l’utilisateur](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Avant de pouvoir protéger les fichiers, vous devez télécharger les modèles Rights Management sur votre ordinateur, puis identifier celui à utiliser ainsi que le numéro d’identification correspondant. À partir du résultat, vous pouvez alors copier l’ID du modèle :

```ps
Get-RMSTemplate
```
Votre résultat peut ressembler à ce qui suit :

```ps
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
```

Si vous n’avez pas exécuté la commande Set-RMSServerAuthentication, vous serez authentifié au service Azure Rights Management à l’aide de votre propre compte d’utilisateur. Si vous êtes sur un ordinateur joint au domaine, vos informations d’identification actuelles seront utilisées automatiquement. Si vous êtes sur un ordinateur de groupe de travail, vous serez invité à vous connecter à Azure, et ces informations d’identification seront ensuite mises en cache pour les commandes suivantes. Dans ce scénario, si vous avez besoin de vous connecter plus tard avec le compte d’un autre utilisateur, utilisez l’applet de commande `Clear-RMSAuthentication`.

Maintenant que vous connaissez l’ID du modèle, vous pouvez l’utiliser avec l’applet de commande `Protect-RMSFile` pour protéger un seul fichier ou tous les fichiers d’un dossier. Par exemple, si vous souhaitez protéger un seul fichier et remplacer l’original, en utilisant le modèle « Contoso, Ltd - Confidential » :

```ps
Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile             EncryptedFile
---------             -------------
C:\Test.docx          C:\Test.docx
```

Pour protéger tous les fichiers d’un dossier, utilisez le paramètre **-Folder** avec une lettre de lecteur et un chemin d’accès, ou le chemin d’accès UNC. Par exemple :

```ps
Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile                          EncryptedFile
---------                          -------------
\Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
\Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
\Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
\Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx
```

Lorsque l’extension du nom de fichier n’est pas modifiée après l’application de la protection, vous pouvez toujours utiliser l’applet de commande `Get-RMSFileStatus` plus tard pour vérifier si le fichier est protégé. Par exemple :

```ps
Get-RMSFileStatus -File \Server1\Documents\Test1.docx
```

Votre résultat peut ressembler à ce qui suit :

```ps
FileName                              Status
--------                              ------
\Server1\Documents\Test1.docx         Protected
```

Pour déprotéger un fichier, vous devez disposer des droits Propriétaire ou Extraction correspondant au moment où le fichier a été protégé, ou vous devez exécuter les applets de commande en tant que super utilisateur. Ensuite, utilisez l’applet de commande de suppression de la protection Unprotect. Par exemple :

```ps
Unprotect-RMSFile C:\test.docx -InPlace
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile                             DecryptedFile
---------                             -------------
C:\Test.docx                          C:\Test.docx
```

Notez que si les modèles Rights Management sont modifiés, vous devez les télécharger à nouveau à l’aide de `Get-RMSTemplate -force`. 

## <a name="active-directory-rights-management-services"></a>Services AD RMS (Active Directory Rights Management Services)

Lisez cette section avant de commencer à utiliser les commandes PowerShell pour protéger ou annuler la protection des fichiers, lorsque votre organisation utilise simplement Active Directory Rights Management Services.


### <a name="prerequisites"></a>Prérequis

Outre les prérequis pour l’installation du module AzureInformationProtection, le compte utilisé pour protéger ou déprotéger des fichiers doit disposer des autorisations de lecture et d’exécution pour accéder à ServerCertification.asmx :

1. Connectez-vous à un serveur AD RMS.

2. Cliquez sur **Démarrer**, puis sur **Ordinateur**.

3. Dans l’Explorateur de fichiers, accédez à %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Cliquez avec le bouton droit sur **ServerCertification.asmx**, puis sur **Propriétés**.

5. Dans la boîte de dialogue **Propriétés de ServerCertification.asmx**, cliquez sur l’onglet **Sécurité**. 

6. Cliquez sur le bouton **Continuer** ou sur le bouton **Modifier**. 

7. Dans la boîte de dialogue **Autorisations de ServerCertification.asmx**, cliquez sur **Ajouter**. 

8. Ajoutez le nom de votre compte. Si d’autres administrateurs AD RMS ou comptes de service vont également utiliser ces applets de commande pour protéger et déprotéger les fichiers, ajoutez aussi ces comptes. 

    Pour protéger ou déprotéger des fichiers de manière non interactive, ajoutez le ou les comptes d’ordinateur appropriés. Par exemple, ajoutez le compte de l’ordinateur Windows Server qui est configuré pour l’infrastructure de classification des fichiers et qui utilise un script PowerShell pour protéger les fichiers.

9. Dans la colonne **Autoriser**, assurez-vous que les cases à cocher **Lecture et exécution** et **Lecture** sont sélectionnées.

10.Cliquez deux fois sur **OK**.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Exemples de scénarios d’utilisation des applets de commande pour les services Active Directory Rights Management Services

Un scénario standard pour ces applets de commande consiste à protéger tous les fichiers dans un dossier à l’aide d’un modèle de stratégie de droits, ou à annuler la protection d’un fichier. 

Tout d’abord, si vous comptez plus d’un déploiement d’AD RMS, vous devez disposer des noms de vos serveurs AD RMS. Utilisez l’applet de commande Get-RMSServer pour afficher la liste des serveurs disponibles :

```ps
Get-RMSServer
```
Votre résultat peut ressembler à ce qui suit :

```ps
Number of RMS Servers that can provide templates: 2 
ConnectionInfo             DisplayName          AllowFromScratch
--------------             -------------        ----------------
Microsoft.InformationAnd…  RmsContoso                       True
Microsoft.InformationAnd…  RmsFabrikam                      True
```

Avant de pouvoir protéger des fichiers, vous devez obtenir une liste des modèles RMS pour identifier celui à utiliser et le numéro d’identification correspondant. Vous devrez spécifier le serveur RMS également uniquement si vous comptez plus d’un déploiement d’AD RMS. 

À partir du résultat, vous pouvez alors copier l’ID du modèle :

```ps
Get-RMSTemplate -RMSServer RmsContoso
```

Votre résultat peut ressembler à ce qui suit :

```ps
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
```

Maintenant que vous connaissez l’ID du modèle, vous pouvez l’utiliser avec l’applet de commande Protect-RMSFile pour protéger un seul fichier ou tous les fichiers d’un dossier. Par exemple, si vous souhaitez protéger un seul fichier et remplacer l’original, en utilisant le modèle « Contoso, Ltd - Confidential » :

```ps
Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile             EncryptedFile
---------             -------------
C:\Test.docx          C:\Test.docx   
```

Pour protéger tous les fichiers d’un dossier, utilisez le paramètre -Folder avec une lettre de lecteur et un chemin d’accès, ou le chemin d’accès UNC. Par exemple :

```ps
Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile                          EncryptedFile
---------                          -------------
\\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
\\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
\\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
\\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   
```

Quand l’extension du nom de fichier n’est pas modifiée après l’application de la protection, vous pouvez toujours utiliser l’applet de commande Get-RMSFileStatus ultérieurement pour vérifier si le fichier est protégé. Par exemple : 

```ps
Get-RMSFileStatus -File \\Server1\Documents\Test1.docx
```

Votre résultat peut ressembler à ce qui suit :

```ps
FileName                              Status
--------                              ------
\\Server1\Documents\Test1.docx        Protected
```

Pour déprotéger un fichier, vous devez disposer de droits d’utilisation de propriétaire ou d’extraction à compter du moment où le fichier a été protégé, ou être un super utilisateur AD RMS. Ensuite, utilisez l’applet de commande de suppression de la protection Unprotect. Par exemple :

```ps
Unprotect-RMSFile C:\test.docx -InPlace
```

Votre résultat peut ressembler à ce qui suit :

```ps
InputFile                             DecryptedFile
---------                             -------------
C:\Test.docx                          C:\Test.docx
```

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>Comment étiqueter des fichiers de manière non interactive pour Azure Information Protection

Vous pouvez exécuter les applets de commande d’étiquetage de manière non interactive à l’aide de l’applet de commande **Set-AIPAuthentication**. L’opération non interactive est également nécessaire pour le scanneur Azure Information Protection.

Par défaut, lorsque vous exécutez les applets de commande d’étiquetage, les commandes s’exécutent dans votre propre contexte utilisateur dans une session PowerShell interactive. Pour les exécuter sans assistance, créez un compte d’utilisateur Azure AD à cet effet. Ensuite, dans le contexte de cet utilisateur, exécutez l’applet de commande Set-AIPAuthentication pour définir et stocker les informations d’identification à l’aide d’un jeton d’accès Azure AD. Ce compte d’utilisateur est ensuite authentifié et initialisé pour le service Azure Rights Management. Le compte télécharge la stratégie Azure Information Protection et tous les modèles Rights Management utilisés par les étiquettes.

> [!NOTE]
> Si vous utilisez des [stratégies délimitées](../configure-policy-scope.md), n’oubliez pas que vous devrez peut-être ajouter ce compte à vos stratégies délimitées.

La première fois que vous exécutez cette applet de commande, vous êtes invité à vous connecter à Azure Information Protection. Spécifiez le nom et le mot de passe du compte d’utilisateur que vous avez créé pour l’utilisateur sans assistance. Ce compte peut alors exécuter les applets de commande d’étiquetage de manière non interactive jusqu’à ce que le jeton d’authentification expire. 

Pour que le compte d’utilisateur puisse se connecter interactivement cette première fois, le compte doit avoir le droit d’**Ouvrir une session locale**. Ce droit est standard pour les comptes d’utilisateur, mais vos stratégies d’entreprise peuvent interdire cette configuration pour les comptes de service. Si tel est le cas, vous pouvez exécuter Set-AIPAuthentication avec le paramètre *Jeton* afin que l’authentification se termine sans l’invite de connexion. Vous pouvez exécuter cette commande comme une tâche planifiée et accorder au compte le droit inférieur qui consiste à **Ouvrir une session comme programme de traitement par lots**. Pour plus d’informations, consultez les sections suivantes. 

Lorsque le jeton expire, exécutez l’applet de commande pour acquérir un nouveau jeton.

Si vous exécutez cette applet de commande sans paramètres, le compte acquiert un jeton d’accès qui est valide 90 jours ou jusqu’à ce que votre mot de passe expire.  

Pour contrôler à quel moment le jeton d’accès expire, exécutez cette applet de commande avec des paramètres. Vous pouvez ainsi configurer le jeton d’accès pour qu’il expire au bout d’un an, de deux ans ou jamais. Cette configuration nécessite que vous disposiez de deux applications inscrites dans Azure Active Directory : une application de type **application web/API** et une **application native**. Les paramètres de cette applet de commande utilisent les valeurs de ces applications.

Après avoir exécuté cette cmdlet, vous pouvez exécuter les cmdlets d’étiquetage dans le contexte du compte d’utilisateur que vous avez créé.

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Pour créer et configurer les applications Azure AD pour Set-AIPAuthentication

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com/).

2. Pour le locataire Azure ad que vous utilisez avec Azure information protection, accédez à **Azure Active Directory**  >  **gérer** les  >  **inscriptions d’applications**. 

3. Sélectionnez **+ nouvelle inscription** pour créer votre application Web App/API. Dans le volet **inscrire une application** , spécifiez les valeurs suivantes, puis cliquez sur **inscrire**:

   - **Nom** : `AIPOnBehalfOf`
        
        Si vous le souhaitez, spécifiez un autre nom. Il doit être unique pour chaque locataire.
    
    - **Types de comptes pris en charge**: **comptes dans ce répertoire d’organisation uniquement**
    
    - **URI de redirection (facultatif)**: **Web** et `http://localhost`

4. Dans le volet **AIPOnBehalfOf** , copiez la valeur de l’ID de l' **application (client)**. La valeur ressemble à l’exemple suivant : `57c3c1c3-abf9-404e-8b2b-4652836c8c66` . Cette valeur est utilisée pour le paramètre *WebAppId* lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

5. Toujours dans le volet **AIPOnBehalfOf** , dans le menu **gérer** , sélectionnez **authentification**.

6. Dans le volet **authentification AIPOnBehalfOf** , dans la section **Paramètres avancés** , activez la case à cocher **ID Tokens** , puis sélectionnez **Enregistrer**.

7. Toujours dans le volet **AIPOnBehalfOf-Authentication** , dans le menu **gérer** , sélectionnez **certificats & secrets**.

8. Dans le volet **AIPOnBehalfOf-certificats & secrets** , dans la section **secrets client** , sélectionnez **+ nouvelle clé secrète client**. 

9. Pour **Ajouter une clé secrète client**, spécifiez les éléments suivants, puis sélectionnez **Ajouter**:
    
    - **Description**: `Azure Information Protection client`
    - **Expires**: spécifiez votre choix de durée (1 an, 2 ans ou n’expire jamais)

9. De retour dans le volet **AIPOnBehalfOf-certificats & secrets** , dans la section **secrets clients** , copiez la chaîne correspondant à la **valeur**. Cette chaîne ressemble à l’exemple suivant : `+LBkMvddz?WrlNCK5v0e6_=meM59sSAn` . Pour être sûr de copier tous les caractères, sélectionnez l’icône à **copier dans le presse-papiers**. 
    
    Il est important d’enregistrer cette chaîne, car elle ne sera plus affichée et ne pourra pas être récupérée. Comme pour toutes les informations sensibles que vous utilisez, stockez la valeur enregistrée en toute sécurité et restreignez l’accès à celle-ci.

10. Toujours dans le volet **AIPOnBehalfOf-certificats & secrets** , dans le menu **gérer** , sélectionnez **exposer une API**.

11. Dans le volet **AIPOnBehalfOf-exposer une API** , sélectionnez **Set** pour l’option URI de l' **ID d’application** , et dans la valeur URI de l’ID d' **application** , remplacez **API** par **http**. Cette chaîne ressemble à l’exemple suivant : `http://d244e75e-870b-4491-b70d-65534953099e` . 
    
    Sélectionnez **Enregistrer**.

12. De retour sur le **AIPOnBehalfOf-exposer un volet API** , sélectionnez **+ Ajouter une étendue**.

13. Dans le volet **Ajouter une étendue** , spécifiez les éléments suivants, en utilisant les chaînes suggérées comme exemples, puis sélectionnez **Ajouter une étendue**:
    - **Nom de l’étendue** : `user-impersonation`
    - **Qui peut donner son consentement ?**  : **Administrateurs et utilisateurs**
    - **Nom d’affichage du consentement administrateur** : `Access Azure Information Protection scanner`
    - **Description du consentement de l’administrateur** : `Allow the application to access the scanner for the signed-in user`
    - **Nom d’affichage du consentement utilisateur** : `Access Azure Information Protection scanner`
    - **Description du consentement de l’utilisateur** : `Allow the application to access the scanner for the signed-in user`
    - **État**: **activé** (valeur par défaut)


14. De retour sur le **AIPOnBehalfOf-exposer un volet API** , fermez ce volet.

15. Sélectionnez **Autorisations de l’API**.

16. Dans le   |  volet **autorisations** de l’API AIPOnBehalfOf, sélectionnez **+ Ajouter une autorisation**.

17. Choisissez **Azure Right Management**, sélectionnez **autorisations déléguées** , puis sélectionnez **créer et accéder au contenu protégé pour les utilisateurs**.

18. Cliquez sur **Ajouter une autorisation**.

19. De retour dans le volet autorisations de l' **API** , dans la section **accorder** un consentement, sélectionnez **accorder le consentement de l’administrateur pour <your tenant name>** et sélectionnez **Oui** pour l’invite de confirmation.

20. Dans le volet **inscriptions d’applications** , sélectionnez **+ nouvelle inscription d’application** pour créer votre application native maintenant.

21. Dans le volet **inscrire une application** , spécifiez les paramètres suivants, puis sélectionnez **inscrire**:
    - **Nom** : `AIPClient`
    - **Types de comptes pris en charge**: **comptes dans ce répertoire d’organisation uniquement**
    - **URI de redirection (facultatif)**: **client Public (mobile & Desktop)** et `http://localhost`

22. Dans le volet **AIPClient** , copiez la valeur de l’ID de l' **application (client)**. La valeur ressemble à l’exemple suivant : `8ef1c873-9869-4bb1-9c11-8313f9d7f76f` . 
    
    Cette valeur est utilisée pour le paramètre NativeAppId lorsque vous exécutez l’applet de commande Set-AIPAuthentication. Collez et enregistrez la valeur pour référence ultérieure.

23. Toujours dans le volet **AIPClient** , dans le menu **gérer** , sélectionnez **authentification**.

24. Dans le volet **AIPClient-Authentication** , dans le menu **gérer** , sélectionnez **autorisations d’API**.

25. Dans le volet **AIPClient-autorisations** , sélectionnez **+ Ajouter une autorisation**.

26. Dans le volet **demander des autorisations d’API** , sélectionnez **mes API**.

27. Dans la section **Sélectionner une API** , sélectionnez **APIOnBehalfOf**, puis activez la case à cocher **User-emprunt d’identité** comme autorisation. Sélectionnez **Ajouter des autorisations**. 

28. De retour dans le volet autorisations de l' **API** , dans la section **accorder** un consentement, sélectionnez **accorder le consentement de l’administrateur pour \<*your tenant name*>** et sélectionnez **Oui** pour l’invite de confirmation.

Vous avez maintenant terminé la configuration des deux applications et vous disposez des valeurs dont vous avez besoin pour exécuter [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) avec les paramètres *WebAppId*, *WebAppKey* et *NativeAppId*. À partir de nos exemples :

```ps
Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"
```

Exécutez cette commande dans le contexte du compte qui étiquettera et protégera les documents de manière non interactive. Par exemple, un compte d’utilisateur pour vos scripts PowerShell ou le compte de service pour exécuter le scanneur Azure Information Protection.  

Lorsque vous exécutez cette commande pour la première fois, vous êtes invité à vous connecter, ce qui crée et stocke en toute sécurité le jeton d’accès de votre compte dans %localappdata%\Microsoft\MSIP. Après cette première connexion, vous pouvez étiqueter et protéger les fichiers de manière non interactive sur l’ordinateur. Toutefois, si vous utilisez un compte de service pour étiqueter et protéger les fichiers, et que ce compte de service ne peut pas vous connecter de manière interactive, suivez les instructions dans la section suivante afin que le compte de service puisse authentifier à l’aide d’un jeton.

### <a name="specify-and-use-the-token-parameter-for-set-aipauthentication"></a>Spécifier et utiliser le paramètre Jeton pour Set-AIPAuthentication

Suivez les étapes et instructions supplémentaires suivantes afin d’éviter la première connexion interactive pour un compte qui étiquette et protège des fichiers. En règle générale, ces étapes supplémentaires ne sont nécessaires que si ce compte ne peut pas obtenir le droit d’**Ouvrir une session localement**, mais qu’il obtient le droit **Ouvrir une session en tant que programme de traitement par lots**. Par exemple, cela peut être le cas pour votre compte de service qui exécute le scanneur Azure Information Protection.

Procédure générale :

1. Créez un script PowerShell sur votre ordinateur local.

2. Exécutez Set-AIPAuthentication pour obtenir un jeton d’accès et copiez-le dans le Presse-papiers.

3. Modifiez le script PowerShell pour inclure le jeton.

4. Créer une tâche qui exécute le script PowerShell dans le contexte du compte de service qui étiquettera et protégera les fichiers.

5. Vérifiez que le jeton est enregistré pour le compte de service, et supprimez le script PowerShell.

#### <a name="step-1-create-a-powershell-script-on-your-local-computer"></a>Étape 1 : créer un script PowerShell sur votre ordinateur local

1. Sur votre ordinateur, créez un nouveau script PowerShell nommé Aipauthentication.ps1.

2. Copiez et collez les commandes suivantes dans ce script :

    ```ps
    Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application> -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application > -Token <token value>
    ```

3. En suivant les instructions de la section précédente, modifiez cette commande en spécifiant vos propres valeurs pour les paramètres **WebAppId**, **WebAppkey**, et **NativeAppId**. À ce stade, vous n’avez pas encore la valeur pour le paramètre **Jeton**, que vous spécifierez plus tard. 

    Par exemple : 

    ```ps
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f -Token <token value>
    ```

#### <a name="step-2-run-set-aipauthentication-to-get-an-access-token-and-copy-it-to-the-clipboard"></a>Étape 2 : exécuter Set-AIPAuthentication pour obtenir un jeton d’accès et le copier dans le Presse-papiers

1. Ouvrez une session Windows PowerShell.

2. En utilisant les mêmes valeurs que vous avez spécifiées dans le script, exécutez la commande suivante :

    ```ps
    (Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application>  -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application >).token | clip
    ```

    Par exemple : 

    ```ps
    (Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip`
    ```

#### <a name="step-3-modify-the-powershell-script-to-supply-the-token"></a>Étape 3 : modifier le script PowerShell pour fournir le jeton

1. Dans votre script PowerShell, spécifiez la valeur du jeton en collant la chaîne depuis le Presse-papiers, puis enregistrez le fichier.

2. Exécutez le script. Si vous ne vous signez pas le script (plus sécurisé), vous devez configurer Windows PowerShell sur l’ordinateur qui exécutera les commandes d’étiquetage. Par exemple, exécutez une session Windows PowerShell à l’aide de l’option **Exécuter en tant qu’administrateur**, puis tapez : `Set-ExecutionPolicy RemoteSigned`. Toutefois, cette configuration laisse s’exécuter tous les scripts non signés quand ils sont stockés sur cet ordinateur (moins sécurisé).

    Pour plus d’informations sur la signature des scripts Windows PowerShell, voir [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) dans la bibliothèque de documentation PowerShell.

3. Copiez ce script PowerShell sur l’ordinateur qui étiquettera et protégera les fichiers, puis supprimez la version d’origine sur votre ordinateur. Par exemple, vous copiez le script PowerShell sur **C:\Scripts\Aipauthentication.ps1** sur un ordinateur Windows Server.

#### <a name="step-4-create-a-task-that-runs-the-powershell-script"></a>Étape 4 : créer une tâche qui exécute le script PowerShell

1. Assurez-vous que le compte de service qui étiquettera et protégera les fichiers a le droit d’**Ouvrir une session en tant que programme de traitement par lots**.

2. Sur l’ordinateur qui étiquettera et protégera les fichiers, ouvrez le Planificateur de tâches et créez une nouvelle tâche. Configurez cette tâche pour qu’elle s’exécute en tant que le compte de service qui étiquettera et protégera les fichiers, puis configurez les valeurs suivantes pour les **Actions** :

   - **Action**: `Start a program`
   - **Programme/script**: `Powershell.exe`
   - **Ajouter des arguments (facultatif)**: `-NoProfile -WindowStyle Hidden -command "&{C:\Scripts\Aipauthentication.ps1}"` 

     Pour la ligne d’argument, spécifiez vos propres noms de chemin d’accès et de fichier, s’ils sont différents de ceux de l’exemple.

3. Exécuter cette tâche manuellement.

#### <a name="step-5-confirm-that-the-token-is-saved-and-delete-the-powershell-script"></a>Étape 5 : vérifier que le jeton est enregistré et supprimer le script PowerShell

1. Vérifiez que le jeton est maintenant stocké dans le dossier **%LocalAppData%\Microsoft\MSIP** pour le profil du compte de service. Cette valeur est protégée par le compte de service.

2. Supprimez le script PowerShell qui contient la valeur de jeton (par exemple, **Aipauthentication.ps1)**.

    Vous pouvez supprimer la tâche si vous le souhaitez. Si votre jeton expire, vous devez répéter ce processus, auquel cas il peut être plus pratique de laisser la tâche configurée afin qu’elle soit prête à s’exécuter à nouveau lorsque vous copierez le nouveau script PowerShell avec la nouvelle valeur du jeton.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir de l’aide concernant les applets de commande lorsque vous avez ouvert une session PowerShell, tapez `Get-Help <cmdlet name> cmdlet`, puis utilisez le paramètre -online pour lire les informations les plus récentes. Par exemple : 

```ps
Get-Help Get-RMSTemplate -online
```

Pour des informations supplémentaires nécessaires pour la prise en charge du client Azure Information Protection, consultez les éléments suivants :

- [Personnalisations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Types de fichiers pris en charge](client-admin-guide-file-types.md)