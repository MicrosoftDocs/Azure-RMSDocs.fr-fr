---
# required metadata

title: Office 365 &colon; configuration pour les clients et services en ligne | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Office 365 : configuration pour les clients et services en ligne

*S’applique à : Azure Rights Management, Office 365*

Office 365 prenant en charge Azure RMS en mode natif, aucune configuration d'ordinateur client n'est requise pour la prise en charge des fonctionnalités de gestion des droits relatifs à l'information pour les applications telles que Word, Excel, PowerPoint, Outlook et Outlook Web App. Les utilisateurs doivent simplement se connecter à leurs applications Office avec leurs informations d’identification [!INCLUDE[o365_1](../includes/o365_1_md.md)] pour pouvoir protéger des fichiers et e-mails, et accéder à des fichiers et e-mails protégés par d’autres.

Cependant, nous vous recommandons de compléter ces applications par l'application de partage Rights Management, afin que les utilisateurs puissent bénéficier du complément Office. Pour plus d’informations, consultez [Application de partage Rights Management : installation et configuration pour les clients](configure-sharing-app.md).

## Exchange Online : configuration de la gestion des droits relatifs à l'information
Pour configurer Exchange Online pour la prise en charge d'Azure RMS, vous devez activer la gestion des droits relatifs à l'information pour Exchange Online. Pour ce faire, utilisez Windows PowerShell (inutile d’installer un module séparé) et exécutez des [commandes PowerShell pour Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Actuellement, vous ne pouvez pas configurer Exchange Online pour prendre en charge Azure RMS si vous utilisez une clé de locataire gérée par le client (BYOK) pour Azure RMS au lieu de la configuration par défaut de clé de locataire gérée par Microsoft. Pour plus d’informations, consultez la section [Tarifs et restrictions BYOK](../plan-design/byok-price-restrictions.md).
>
> Si vous essayez de configurer Exchange Online quand Azure RMS utilise BYOK, la commande pour importer la clé (étape 5 de la procédure suivante) échoue avec le message d’erreur **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

Les étapes suivantes décrivent un ensemble spécifique de commandes à exécuter pour permettre à Exchange Online d'utiliser Azure RMS :

1.  Si vous n'avez jamais utilisé Windows PowerShell pour Exchange Online sur votre ordinateur, vous devez configurer Windows PowerShell pour exécuter des scripts signés. Démarrez votre session Windows PowerShell à l'aide de l'option **Exécuter en tant qu'administrateur** , puis tapez :

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Dans votre session Windows PowerShell, connectez-vous à Exchange Online à l'aide d'un compte activé pour l'accès aux environnements distants. Par défaut, tous les comptes créés dans Exchange Online sont activés pour l’accès aux environnements distants, mais il est possible de les désactiver (et activer) à l’aide de la commande  [Set-User &lt;identité_utilisateur&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Pour vous connecter, tapez :

    ```
    $Cred = Get-Credential
    ```
    Dans la boîte de dialogue **Demande d'informations d'identification Windows PowerShell** , entrez vos nom d'utilisateur et mot de passe Office 365.

3.  Connectez-vous au service Exchange Online en exécutant les deux commandes suivantes :

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Spécifiez l’emplacement de la clé de client Azure RMS, selon l’emplacement où le client de votre organisation a été créé :

    Pour l'Amérique du Nord (et les abonnements de gouvernement) :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Europe :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Asie :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Pour l'Amérique du Sud :

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importez les données de configuration d'Azure RMS dans Exchange Online, sous la forme du domaine de publication approuvé (TPD). Cela inclut la clé de locataire Azure RMS et les modèles Azure RMS :

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    Dans cette commande, nous avons utilisé le nom **RMS Online** comme nom de base du TPD pour Azure RMS dans Exchange Online. Une fois le TPD importé, il est nommé **RMS Online - 1** dans Exchange Online.

6.  Activez la fonctionnalité Azure RMS afin que les fonctionnalités IRM soient disponibles pour Exchange Online :

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Après l'exécution de cette commande, Rights Management est automatiquement activé pour le client Outlook, Outlook Web App et Exchange Active Sync.

7.  Vous pouvez également tester la réussite de cette configuration à l'aide de la commande suivante :

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Par exemple : **Test-IRMConfiguration -Sender  adams@contoso.com**

    Cette commande exécute une série de vérifications qui inclut la vérification de la connectivité au service, l'extraction de la configuration, ainsi que l'extraction d'URI, de licences et de modèles. La session Windows PowerShell indique les résultats de chaque vérification et, à la fin, si tous les contrôles ont été concluants : **OVERALL RESULT: PASS**

8.  Déconnectez votre session PowerShell distante :

    ```
    Remove-PSSession $Session
    ```

Les utilisateurs peuvent maintenant protéger leurs messages électroniques en utilisant Azure RMS. Par exemple, dans Outlook Web App,  dans le menu étendu, sélectionnez **Définir les autorisations** (**...**), puis choisissez **Ne pas transférer** ou l’un des modèles disponibles pour appliquer la protection des informations au message électronique et aux éventuelles pièces jointes. Toutefois, étant donné qu'Outlook Web App met en cache l'interface utilisateur pendant une journée, attendez l'expiration de cette période avant de tenter d'appliquer la protection des informations au messages électroniques après avoir exécuté ces commandes de configuration. Tant que l'interface utilisateur n'a pas été actualisée pour refléter la nouvelle configuration, aucune option du menu **Définir les autorisations** n'est visible.

> [!IMPORTANT]
> Si vous créez des [modèles personnalisés](configure-custom-templates.md) pour Azure RMS ou mettez à jour les modèles, vous devez chaque fois exécuter la commande Exchange Online PowerShell suivante (si nécessaire, exécutez d’abord les étapes 2 et 3) pour synchroniser ces modifications sur Exchange Online : `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

En tant qu’administrateur Exchange, vous pouvez maintenant configurer des fonctionnalités qui appliquent automatiquement la protection des informations, telles que les [règles de transport](https://technet.microsoft.com/library/dd302432.aspx), les [stratégies de protection contre la perte des données (DLP)](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) et la [messagerie vocale protégée](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (messagerie unifiée).

Pour obtenir des instructions détaillées concernant la configuration d'Exchange Online afin d'activer la fonctionnalité IRM, consultez la documentation dans la bibliothèque Exchange. Par exemple :

-   [Connexion à Exchange Online à l'aide de Remote PowerShell](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Configurer IRM pour utiliser Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Chiffrement de messages Office 365
Exécutez les étapes décrites dans la section précédente mais, si vous ne souhaitez pas que les modèles soient affichés, avant l’étape 6, exécutez la commande suivante pour empêcher que les modèles IRM soient disponibles dans Outlook Web App et le client Outlook : `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Ensuite, vous êtes prêt à configurer les [règles de transport](https://technet.microsoft.com/library/dd302432.aspx) pour modifier automatiquement la sécurité des messages quand les destinataires sont situés en dehors de l'organisation, puis sélectionnez l'option **Appliquer le chiffrement des messages Office 365** .

Pour plus d'informations sur le chiffrement des messages, consultez [Chiffrement dans Office 365](https://technet.microsoft.com/library/dn569286.aspx) dans la bibliothèque Exchange.

## SharePoint Online et OneDrive Entreprise : configuration de la gestion des droits relatifs à l'information
Pour configurer SharePoint Online et OneDrive Entreprise pour la prise en charge d'Azure RMS, vous devez commencer par activer la gestion des droits relatifs à l'information (IRM) pour SharePoint Online dans le Centre d'administration SharePoint. Ensuite, les propriétaires de sites peuvent protéger par IRM leurs listes et bibliothèques de documents SharePoint, ainsi que leur bibliothèque OneDrive Entreprise, afin que les documents qui y sont enregistrés et partagés avec d'autres utilisateurs soient automatiquement protégés par Azure RMS.

Pour activer l'IRM pour SharePoint Online, consultez les instructions suivantes sur le site web Office :

-   [Configuration de la gestion des droits relatifs à l'information dans le centre d'administration SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Cette configuration est effectuée par l'administrateur Office 365.

### Configuration de l'IRM pour les bibliothèques et listes
Après avoir activé le service IRM pour SharePoint, les propriétaires de sites peuvent protéger par IRM leurs bibliothèques de documents et listes SharePoint. Pour obtenir des instructions, consultez les ressources suivantes sur le site web Office :

-   [Application de la Gestion des droits relatifs à l'information à une liste ou à une bibliothèque](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Cette configuration est effectuée par l'administrateur du site SharePoint.

### Configuration de l'IRM pour OneDrive Entreprise
Après que vous avez activé le service IRM pour SharePoint Online, la bibliothèque de documents OneDrive Entreprise des utilisateurs peut être configurée pour la protection Rights Management.  Les utilisateurs peuvent configurer cela pour eux-mêmes à l’aide de l’icône **Paramètres** dans leur OneDrive. Si des administrateurs ne peuvent pas configurer Rights Management pour le OneDrive Entreprise d'utilisateurs à l'aide du Centre d'administration SharePoint, vous pouvez le faire en utilisant Windows PowerShell.

> [!NOTE]
> Pour plus d’informations sur la configuration de OneDrive Entreprise, consultez [Configuration de OneDrive Entreprise dans Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb) dans la documentation Office.

#### Configuration pour les utilisateurs
Donnez aux utilisateurs ces instructions pour qu'ils puissent configurer leur OneDrive Entreprise et protéger par IRM leurs fichiers d'entreprise.

1.  Dans OneDrive, cliquez sur l’icône **Paramètres** pour ouvrir le menu Paramètres, puis cliquez sur **Contenu du site**.

2.  Pointez sur la vignette **Documents**, choisissez les points de suspension (**...**), puis cliquez sur **PARAMÈTRES.**

3.  Dans la page **Paramètres**, dans la section **Autorisations et gestion**, cliquez sur **Gestion des droits relatifs à l’information**.

4.  Dans la page **Paramètres de la Gestion des droits relatifs à l’information**, cochez la case **Restreindre les autorisations sur cette bibliothèque lors du téléchargement**, spécifiez votre choix de nom et de description pour les autorisations, cliquez éventuellement sur **AFFICHER LES OPTIONS** pour définir des configurations facultatives, puis cliquez sur **OK**.

    Pour plus d'informations sur les options de configuration, consultez les instructions de la rubrique [Appliquer la Gestion des droits relatifs à l'information à une liste ou à une bibliothèque](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) dans la documentation d'Office.

Étant donné que cette configuration dépend de la capacité des utilisateurs plutôt que de celle d'un administrateur, à protéger leur bibliothèque OneDrive Entreprise, informez-les des avantages de la protection de leurs fichiers et de la manière de procéder. Par exemple, expliquez que, quand ils partagent un document à partir de OneDrive Entreprise, seules les personnes qu'ils autorisent peuvent y accéder avec des restrictions qu'ils configurent, même si le fichier est renommé et copié ailleurs.

#### Configuration pour les administrateurs
Si vous ne pouvez pas configurer IRM pour le OneDrive Entreprise d'utilisateurs à l'aide du Centre d'administration SharePoint, vous pouvez le faire en utilisant Windows PowerShell. Pour activer IRM pour ces bibliothèques, procédez comme suit :

1.  Téléchargez et installez le [SDK des composants du client SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Téléchargez et installez [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Copiez le contenu du script suivant et nommez le fichier Set-IRMOnOneDriveForBusiness.ps1 sur votre ordinateur.

    *&#42;&#42;Exclusion de responsabilité&#42;&#42;* : cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d'aucune sorte.

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

    ======
    #>

    # URL will be in the format https://<tenant-name>-admin.sharepoint.com
    $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

    $tenantAdmin = "admin@contoso.com"

    $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

    <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
       Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

    #>

    $listTitle = "Documents"

    function Load-SharePointOnlineClientComponentAssemblies
    {
        [cmdletbinding()]
        param()

        process
        {
            # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
            try
            {
                Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                return $true
            }
            catch
            {
                if($_.Exception.Message -match "Could not load file or assembly")
                {
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
                }
                else
                {
                    Write-Error -Exception $_.Exception
                }
                return $false
            }
        }
    }

    function Load-SharePointOnlineModule
    {
        [cmdletbinding()]
        param()

        process
        {
            do
            {
                # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
                $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

                if(-not $spoModule)
                {
                    try
                    {
                        Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                        return $true
                    }
                    catch
                    {
                        if($_.Exception.Message -match "Could not load file or assembly")
                        {
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                        }
                        else
                        {
                            Write-Error -Exception $_.Exception
                        }
                        return $false
                    }
                }
                else
                {
                    return $true
                }
            }
            while(-not $spoModule)
        }
    }

    function Set-IrmConfiguration
    {
        [cmdletbinding()]
        param(
            [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
            [parameter(Mandatory=$true)][string]$PolicyTitle,
            [parameter(Mandatory=$true)][string]$PolicyDescription,
            [parameter(Mandatory=$false)][switch]$IrmReject,
            [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
            [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
            [parameter(Mandatory=$false)][switch]$AllowPrint,
            [parameter(Mandatory=$false)][switch]$AllowScript,
            [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
            [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
            [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
            [parameter(Mandatory=$false)][string]$GroupName
        )

        process
        {
            Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

            # reset the value to the default settings
            $list.InformationRightsManagementSettings.Reset()

            $list.IrmEnabled = $true

            # IRM Policy title and description

                $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
                $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

            # Set additional IRM library settings

                # Do not allow users to upload documents that do not support IRM
                $list.IrmReject = $IrmReject.IsPresent

                $parsedDate = Get-Date
                if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
                {
                    # Stop restricting access to the library at <date>
                    $list.IrmExpire = $true
                    $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
                }

                # Prevent opening documents in the browser for this Document Library
                $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

            # Configure document access rights

                # Allow viewers to print
                $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

                # Allow viewers to run script and screen reader to function on downloaded documents
                $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

                # Allow viewers to write on a copy of the downloaded document
                $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

                if($DocumentAccessExpireDays)
                {
                    # After download, document access rights will expire after these number of days (1-365)
                    $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                    $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
                }

            # Set group protection and credentials interval

                if($LicenseCacheExpireDays)
                {
                    # Users must verify their credentials using this interval (days)
                    $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                    $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
                }

                if($GroupName)
                {
                    # Allow group protection. Default group:
                    $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                    $list.InformationRightsManagementSettings.GroupName             = $GroupName
                }
        }
        end
        {
            if($list)
            {
                Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
                $list.InformationRightsManagementSettings.Update()
                $list.Update()
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()
            }
        }
    }

    function Get-CredentialFromCredentialCache
    {
        [cmdletbinding()]
        param([string]$CredentialName)

        #if( Test-Path variable:\global:CredentialCache )
        if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
        {
            if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
            {
                Write-Verbose "Credential Cache Hit: $CredentialName"
                return $global:O365TenantAdminCredentialCache[$CredentialName]
            }
        }
        Write-Verbose "Credential Cache Miss: $CredentialName"
        return $null
    }

    function Add-CredentialToCredentialCache
    {
        [cmdletbinding()]
        param([System.Management.Automation.PSCredential]$Credential)

        if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
        {
            Write-Verbose "Initializing the Credential Cache"
            $global:O365TenantAdminCredentialCache = @{}
        }

        Write-Verbose "Adding Credential to the Credential Cache"
        $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
    }

    # load the required assemblies and Windows PowerShell modules

        if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

    # Add the credentials to the client context and SharePoint Online service connection

        # check for cached credentials to use
        $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

        if(-not $o365TenantAdminCredential)
        {
            # when credentials are not cached, prompt for the tenant admin credentials
            $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

            if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
            {
                Write-Error -Message "Could not validate the supplied tenant admin credentials"
                return
            }

            # add the credentials to the cache
            Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
        }

    # connect to Office365 first, required for SharePoint Online cmdlets to run

        Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

    # enumerate each of the specified site URLs

        foreach($webUrl in $webUrls)
        {
            $grantedSiteCollectionAdmin = $false

            try
            {
                # establish the client context and set the credentials to connect to the site
                $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
                $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

                # initialize the site and web context
                $script:clientContext.Load($script:clientContext.Site)
                $script:clientContext.Load($script:clientContext.Web)
                $script:clientContext.ExecuteQuery()

                # load and ensure the tenant admin user account if present on the target SharePoint site
                $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
                $script:clientContext.Load($tenantAdminUser)
                $script:clientContext.ExecuteQuery()

                # check if the tenant admin is a site admin
                if( -not $tenantAdminUser.IsSiteAdmin )
                {
                    try
                    {
                        # grant the tenant admin temporary admin rights to the site collection
                        Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                        $grantedSiteCollectionAdmin = $true
                    }
                    catch
                    {
                        Write-Error $_.Exception
                        return
                    }
                }

                try
                {
                    # load the list orlibrary using CSOM

                    $list = $null
                    $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                    $script:clientContext.Load($list)
                    $script:clientContext.ExecuteQuery()

                    # **************  ADMIN INSTRUCTIONS  **************
                    # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                    # The supplied options and values are for example only
                    # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                    Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
                }
                catch
                {
                    Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
                }
           }
           finally
           {
                if($grantedSiteCollectionAdmin)
                {
                    # remove the temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
                }
           }
        }

    Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Examinez le script et apportez les modifications suivantes :

    1.  Recherchez `$sharepointAdminCenterUrl` et remplacez la valeur de l’exemple par l’URL de votre propre Centre d’administration SharePoint.

        Cette valeur est l’URL de base quand vous accédez au Centre d’administration SharePoint. Son format est le suivant : https://*&lt;nom_client&gt;*-admin.sharepoint.com.

        Par exemple, si le nom du client est « contoso », vous devez spécifier : **https://contoso-admin.sharepoint.com**.

    2.  Recherchez `$tenantAdmin` et remplacez la valeur de l’exemple par votre propre compte d’administrateur général complet pour Office 365.

        Cette valeur est identique à celle que vous utilisez pour vous connecter au portail d’administration d’Office 365 en tant qu’administrateur général. Son format est le suivant : nom_utilisateur@*&lt;nom de domaine du client&gt;*.com

        Par exemple, si le nom d’utilisateur de l’administrateur général d’Office 365 est « admin » pour le domaine du client « contoso.com », vous devez spécifier **admin@contoso.com**.

    3.  Recherchez `$webUrls` et remplacez les valeurs de l’exemple par les URL des sites web OneDrive Entreprise de vos utilisateurs, en ajoutant ou en supprimant le nombre d’entrées nécessaires.

        Vous pouvez également lire dans le script les commentaires concernant la façon de remplacer ce tableau en important un fichier .CSV contenant toutes les URL à configurer.  Nous avons fourni un autre exemple de script pour rechercher et extraire automatiquement les URL à insérer dans ce fichier .CSV. Quand vous êtes prêt, développez la section [Script supplémentaire pour répertorier toutes les URL de OneDrive Entreprise dans un fichier .CSV](#BKMK_Script_OD4B_URLS) située juste après ces étapes.

        L’URL web du OneDrive Entreprise de l’utilisateur est au format suivant : https://*&lt;nom_client&gt;*-my.sharepoint.com/personal/*&lt;nom_utilisateur&gt;*_*&lt;nom_client&gt;*_com.

        Par exemple, si l’utilisateur dans le client contoso a le nom d’utilisateur « rsimone », vous devez spécifier **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**.

    4.  Étant donné que nous utilisons le script pour configurer OneDrive Entreprise, ne changez pas la valeur de **Documents** pour la variable `$listTitle`.

    5.  Recherchez `ADMIN INSTRUCTIONS`. Si vous n'apportez aucune modification à cette section, le OneDrive Entreprise de l'utilisateur est configuré pour IRM avec le titre de stratégie « Protected Files » et la description « This policy restricts access to authorized users ».  Aucune autre option d'IRM n'est définie, ce qui convient probablement pour la plupart des environnements. Vous pouvez cependant changer le titre et la description de stratégie proposés, ainsi qu'ajouter de options d'IRM appropriées pour votre environnement. Pour savoir comment construire votre propre jeu de paramètres pour la commande Set-IrmConfiguration, voir l'exemple commenté dans le script.

5.  Enregistrez le script et signez-le. Si vous ne signez pas le script (plus sécurisé), Windows PowerShell doit être configuré sur votre ordinateur pour exécuter des scripts non signés. Par exemple, exécutez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**, puis tapez : **Set-ExecutionPolicy Unrestricted**. Toutefois, cette configuration laisse tous les scripts non signés s'exécuter (moins sécurisé).

    Pour plus d'informations sur la signature des scripts Windows PowerShell, voir [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) dans la bibliothèque de documentation PowerShell.

6.  Exécutez le script et, si vous y êtes invité, fournissez le mot de passe du compte d'administrateur Office 365. Si vous modifiez le script et l'exécutez dans la même session Windows PowerShell, vous n'êtes pas invité à fournir des informations d'identification.

> [!TIP]
> Vous pouvez également utiliser ce script pour configurer IRM pour une bibliothèque SharePoint Online. Pour cette configuration, il est préférable d’activer l’option supplémentaire **Interdire aux utilisateurs de télécharger des documents qui ne prennent pas en charge IRM** pour vous assurer que la bibliothèque ne contient que des documents protégés.    Pour ce faire, ajoutez le paramètre `-IrmReject` à la commande Set-IrmConfiguration dans le script.
>
> Vous devez également modifier les variables `$webUrls` (par exemple, **https://contoso.sharepoint.com**) et `$listTitle` (par exemple, **$Reports**)).

Si vous devez désactiver IRM pour les bibliothèques OneDrive Entreprise de l’utilisateur, consultez la section [Script pour désactiver IRM pour OneDrive entreprise](#script-to-disable-irm-for-onedrive-for-business).

##### Script supplémentaire pour insérer toutes les URL de OneDrive Entreprise dans un fichier .CSV
Pour l'étape 4c ci-dessus, vous pouvez utiliser le script Windows PowerShell suivant pour extraire les URL des bibliothèques OneDrive Entreprise de tous les utilisateurs, que vous pouvez ensuite vérifier, modifier si nécessaire et importer dans le script principal.

Ce script nécessite également le [SDK des composants du client SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) et [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Suivez les mêmes instructions pour le copier et le coller, enregistrez le fichier localement (par exemple, sous « Report-OneDriveForBusinessSiteInfo.ps1 »), modifiez les valeurs `$sharepointAdminCenterUrl` et `$tenantAdmin` comme précédemment, puis exécutez le script.

*&#42;&#42;Exclusion de responsabilité&#42;&#42;* : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d'aucune sorte.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### Script pour désactiver IRM pour OneDrive Entreprise
Si vous devez désactiver IRM pour le OneDrive Entreprise d'un utilisateur, utilisez l'exemple de script suivant.

Ce script nécessite également le [SDK des composants du client SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) et [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Copiez et collez le contenu, enregistrez le fichier localement (par exemple, sous « Disable-IRMOnOneDriveForBusiness.ps1 »), puis modifiez les valeurs `$sharepointAdminCenterUrl` et `$tenantAdmin`. Spécifiez manuellement les URL de OneDrive Entreprise ou utilisez le script de la section précédente pour les importer, puis exécutez le script.

*&#42;&#42;Exclusion de responsabilité&#42;&#42;* : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d'aucune sorte.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint Online cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```



<!--HONumber=Apr16_HO4-->


