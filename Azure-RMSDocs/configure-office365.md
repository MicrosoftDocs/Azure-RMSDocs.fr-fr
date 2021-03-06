---
title: Configuration des services Microsoft 365 à utiliser Azure RMS-AIP
description: Informations et instructions permettant aux administrateurs de configurer Microsoft 365 services pour qu’ils fonctionnent avec le service Azure Rights Management à partir de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2caaf42c764b80f0ccba8b9c74191cbd6bd23c88
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383497"
---
# <a name="microsoft-365-configuration-for-online-services-to-use-the-azure-rights-management-service"></a>Microsoft 365 : configuration pour que services en ligne utilise le service de Rights Management Azure

>S’applique à **: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Utilisez les sections suivantes pour vous aider à configurer Exchange Online, Microsoft SharePoint et Microsoft OneDrive pour utiliser le service Azure Rights Management à partir de Azure Information Protection.

## <a name="exchange-online-irm-configuration"></a>Exchange Online : configuration de la gestion des droits relatifs à l’information

Pour plus d’informations sur le fonctionnement d’Exchange Online avec le service Azure Rights Management, consultez la section [Exchange Online et Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) dans [Comment les applications et services Office prennent en charge Azure Rights Management](office-apps-services-support.md).

Exchange Online est peut-être déjà activé pour utiliser le service Azure Rights Management. Pour le savoir, exécutez les commandes suivantes :

1. Si vous n'avez jamais utilisé Windows PowerShell pour Exchange Online sur votre ordinateur, vous devez configurer Windows PowerShell pour exécuter des scripts signés. Démarrez votre session Windows PowerShell à l'aide de l'option **Exécuter en tant qu'administrateur**, puis tapez :

    ```md
    Set-ExecutionPolicy RemoteSigned
    ```

    Appuyez sur **Y** pour confirmer.

2. Dans votre session Windows PowerShell, connectez-vous à Exchange Online à l'aide d'un compte activé pour l'accès aux environnements distants. Par défaut, tous les comptes créés dans Exchange Online sont activés pour l’accès au shell distant, mais vous pouvez les désactiver (et les activer) à l’aide de la commande [Set-User &lt; UserIdentity &gt; -RemotePowerShellEnabled](/powershell/exchange/disable-access-to-exchange-online-powershell) .

    Pour vous connecter, commencez par taper :

    ```markdown
    $Cred = Get-Credential
    ```

    Ensuite, dans la boîte de dialogue **demande d’informations d’identification Windows PowerShell** , fournissez votre nom d’utilisateur et votre mot de passe Microsoft 365.

3. Connectez-vous au service Exchange Online en définissant d’abord une variable :

    ```md
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    Exécutez ensuite la commande suivante :

    ```md
    Import-PSSession $Session
    ```

4. Exécutez la commande [Get-IRMConfiguration](/powershell/module/exchange/get-irmconfiguration) pour voir votre configuration Exchange Online du service de protection :

    ```md
    Get-IRMConfiguration
    ```

    Dans la sortie, recherchez la valeur **AzureRMSLicensingEnabled** :

    - Si AzureRMSLicensingEnabled est défini sur **True**, Exchange Online est déjà activé pour le service Azure Rights Management.

    - Si AzureRMSLicensingEnabled a la valeur **False**, exécutez la commande suivante pour activer Exchange Online pour le service Azure Rights Management : `Set-IRMConfiguration -AzureRMSLicensingEnabled $true`

5. Pour tester si Exchange Online est configuré correctement, exécutez la commande suivante :

    ```md
    Test-IRMConfiguration -Sender <user email address>
    ```

    Par exemple : **test-IRMConfiguration-sender adams \@ contoso.com**

    Cette commande exécute une série de vérifications qui inclut la vérification de la connectivité au service, l'extraction de la configuration, ainsi que l'extraction d'URI, de licences et de modèles. La session Windows PowerShell indique les résultats de chaque vérification et, à la fin, si tous les contrôles ont été concluants : **OVERALL RESULT: PASS**

Quand Exchange Online est activé pour utiliser le service Azure Rights Management, vous pouvez configurer des fonctionnalités qui appliquent automatiquement la protection des informations, comme des [règles de flux de messages](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8), des [stratégies de protection contre la perte des données (DLP)](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) et la [messagerie vocale protégée](/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/protect-voice-mail) (messagerie unifiée).

## <a name="sharepoint-in-microsoft-365-and-onedrive-irm-configuration"></a>SharePoint dans Microsoft 365 et OneDrive : configuration IRM

Pour plus d’informations sur le fonctionnement de l’IRM SharePoint avec le service Azure Rights Management, consultez [SharePoint dans Microsoft 365 et SharePoint Server](office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) dans la section protection de la **Rights Management** de cette documentation.

Pour configurer SharePoint dans Microsoft 365 et OneDrive pour prendre en charge le service Azure Rights Management, vous devez d’abord activer le service de gestion des droits relatifs à l’information (IRM) pour SharePoint à l’aide du centre d’administration SharePoint. Ensuite, les propriétaires de sites peuvent protéger par IRM leurs listes et bibliothèques de documents SharePoint, et les utilisateurs peuvent protéger leur bibliothèque OneDrive de manière à ce que les documents qui y sont enregistrés et partagés avec d’autres utilisateurs soient automatiquement protégés par le service Azure Rights Management.

> [!NOTE]
> Les bibliothèques protégées par IRM pour SharePoint dans Microsoft 365 et OneDrive nécessitent la dernière version du nouveau client de synchronisation OneDrive (OneDrive.exe) et la version du [client RMS à partir du centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=38396). Installez cette version du client RMS même si vous avez installé le client Azure Information Protection. Pour plus d’informations sur ce scénario de déploiement, consultez [Déployer le nouveau client de synchronisation OneDrive dans un environnement d’entreprise](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668).

Pour activer le service gestion des droits relatifs à l’information (IRM) pour SharePoint, reportez-vous aux instructions suivantes de la documentation Office :

- [Configurer les informations Rights Management (IRM) dans le centre d’administration SharePoint](/microsoft-365/compliance/set-up-irm-in-sp-admin-center)

Cette configuration est effectuée par l’administrateur Microsoft 365.

### <a name="configuring-irm-for-libraries-and-lists"></a>Configuration de l’IRM pour les bibliothèques et les listes

Une fois que vous avez activé le service IRM pour SharePoint, les propriétaires de sites peuvent protéger par IRM leurs bibliothèques de documents et listes SharePoint. Pour obtenir des instructions, consultez les ressources suivantes sur le site web Office :

- [Activation de la gestion des droits relatifs à l’information pour une liste ou une bibliothèque](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Cette configuration est effectuée par l’administrateur du site SharePoint.

### <a name="configuring-irm-for-onedrive"></a>Configuration d’IRM pour OneDrive

Une fois que vous avez activé le service IRM pour SharePoint, la bibliothèque de documents OneDrive des utilisateurs ou des dossiers individuels peut ensuite être configuré pour la protection de Rights Management. Les utilisateurs peuvent configurer cela pour eux-mêmes à l’aide de leur site web OneDrive. Si des administrateurs ne peuvent pas configurer cette protection pour eux à l'aide du Centre d'administration SharePoint, vous pouvez le faire en utilisant Windows PowerShell.

> [!NOTE]
> Pour plus d’informations sur la configuration de OneDrive, consultez la documentation [onedrive](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb) .

#### <a name="configuration-for-users"></a>Configuration pour les utilisateurs

Donnez aux utilisateurs les instructions suivantes pour qu’ils puissent configurer leur OneDrive pour protéger leurs fichiers d’entreprise.

1. Connectez-vous à Microsoft 365 avec votre compte professionnel ou scolaire, puis accédez au [site Web OneDrive](https://admin.microsoft.com/onedrive).

2. Dans le volet de navigation, en bas, sélectionnez **Revenir à l’expérience OneDrive classique**.

3. Sélectionnez l’icône **paramètres** . Dans le volet **Paramètres**, si le paramètre **Ruban** a la valeur **Désactivé**, sélectionnez ce paramètre pour activer le ruban.

4. Pour configurer tous les fichiers OneDrive à protéger, sélectionnez l’onglet **bibliothèque** dans le ruban, puis sélectionnez Paramètres de la **bibliothèque**.

5. Dans la page **Documents > Paramètres**, dans la section **Autorisations et gestion**, sélectionnez **Gestion des droits relatifs à l'information**.

6. Dans la page **Paramètres de la Gestion des droits relatifs à l'information**, cochez la case **Restreindre les autorisations sur cette bibliothèque lors du téléchargement**. Spécifiez votre choix de nom et une description pour les autorisations. En outre, si vous le souhaitez, cliquez sur **AFFICHER LES OPTIONS** pour définir des configurations facultatives, puis cliquez sur **OK**.

    Pour plus d’informations sur les options de configuration, consultez les instructions de la rubrique [Appliquer la Gestion des droits relatifs à l’information à une liste ou à une bibliothèque](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) dans la documentation d’Office.

Étant donné que cette configuration s’appuie sur les utilisateurs plutôt que sur un administrateur pour protéger leurs fichiers OneDrive, informez les utilisateurs des avantages de la protection de leurs fichiers et de la procédure à suivre. Par exemple, expliquez que lorsqu’ils partagent un document à partir de OneDrive, seules les personnes qu’ils autorisent peuvent y accéder avec des restrictions qu’ils configurent, même si le fichier est renommé et copié ailleurs.

#### <a name="configuration-for-administrators"></a>Configuration pour les administrateurs

Bien que vous ne puissiez pas configurer IRM pour OneDrive utilisateur à l’aide du centre d’administration SharePoint, vous pouvez le faire à l’aide de Windows PowerShell. Pour activer IRM pour ces bibliothèques, procédez comme suit :

1. Téléchargez et installez le [Kit de développement logiciel (SDK) des composants clients SharePoint](https://www.microsoft.com/download/details.aspx?id=42038).

2. Téléchargez et installez [SharePoint Management Shell](https://www.microsoft.com/download/details.aspx?id=35588).

3. Copiez le contenu du script suivant et nommez le fichier Set-IRMOnOneDriveForBusiness.ps1 sur votre ordinateur.

   *&#42;&#42;Exclusion de responsabilité&#42;&#42;* : cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d’aucune sorte.

   ```ps
   # Requires Windows PowerShell version 3

   <#
     Description:

       Configures IRM policy settings for OneDrive and can also be used for SharePoint libraries and lists

    Script Installation Requirements:

      SharePoint Client Components SDK
      https://www.microsoft.com/download/details.aspx?id=42038

      SharePoint Management Shell
      https://www.microsoft.com/download/details.aspx?id=35588

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
                   Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                           Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

   # Add the credentials to the client context and SharePoint service connection

       # check for cached credentials to use
       $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

       if(-not $o365TenantAdminCredential)
       {
           # when credentials are not cached, prompt for the tenant admin credentials
           $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Microsoft 365 admin"

           if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
           {
               Write-Error -Message "Could not validate the supplied tenant admin credentials"
               return
           }

           # add the credentials to the cache
           Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
       }

   # connect to Office365 first, required for SharePoint cmdlets to run

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

4. Examinez le script et apportez les modifications suivantes :

   1. Recherchez `$sharepointAdminCenterUrl` et remplacez la valeur de l’exemple par l’URL de votre propre Centre d’administration SharePoint.

      Vous trouverez cette valeur en tant qu’URL de base lorsque vous accédez au centre d’administration SharePoint et au format suivant : https://*&lt; tenant_name &gt;*-admin.SharePoint.com

      Par exemple, si le nom du locataire est « contoso », vous devez spécifier : **https://contoso-admin.sharepoint.com**

   2. Recherchez `$tenantAdmin` et remplacez la valeur de l’exemple par votre propre compte d’administrateur général complet pour Microsoft 365.

      Cette valeur est identique à celle que vous utilisez pour vous connecter au centre d’administration Microsoft 365 en tant qu’administrateur général. son format est le suivant : user_name@*&lt; nom &gt; de domaine du locataire*. com

      Par exemple, si le nom d’utilisateur de l’administrateur général Microsoft 365 est « admin » pour le domaine de locataire « contoso.com », vous devez spécifier : **admin@contoso.com**

   3. Recherchez `$webUrls` et remplacez les valeurs d’exemple par les URL Web OneDrive de vos utilisateurs, en ajoutant ou en supprimant le nombre d’entrées dont vous avez besoin.

      Vous pouvez également lire dans le script les commentaires concernant la façon de remplacer ce tableau en important un fichier .CSV contenant toutes les URL à configurer.  Nous avons fourni un autre exemple de script pour rechercher et extraire automatiquement les URL à insérer dans ce fichier .CSV. Quand vous êtes prêt à le faire, utilisez le [script supplémentaire pour générer toutes les URL OneDrive dans un. Section du fichier CSV](#additional-script-to-output-all-onedrive-urls-to-a-csv-file) immédiatement après ces étapes.

      L’URL Web du OneDrive de l’utilisateur est au format suivant : https://*&lt; nom &gt; du locataire*-My.SharePoint.com/Personal/*&lt; user_name &gt;* _ *&lt; nom &gt; du locataire* _com

      Par exemple, si l’utilisateur du locataire Contoso a un nom d’utilisateur « rsimone », vous devez spécifier : **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

   4. Étant donné que nous utilisons le script pour configurer OneDrive, ne modifiez pas la valeur des **documents** pour la `$listTitle` variable.

   5. Recherchez `ADMIN INSTRUCTIONS`. Si vous n’apportez aucune modification à cette section, le OneDrive de l’utilisateur sera configuré pour IRM avec le titre de la stratégie « fichiers protégés » et la description « cette stratégie restreint l’accès aux utilisateurs autorisés ».  Aucune autre option d’IRM n’est définie, ce qui convient probablement pour la plupart des environnements. Vous pouvez cependant changer le titre et la description de stratégie proposés, ainsi qu’ajouter des options d’IRM appropriées pour votre environnement. Pour savoir comment construire votre propre jeu de paramètres pour la commande Set-IrmConfiguration, voir l’exemple commenté dans le script.

5. Enregistrez le script et signez-le. Si vous ne signez pas le script (plus sécurisé), Windows PowerShell doit être configuré sur votre ordinateur pour exécuter des scripts non signés. Par exemple, exécutez une session Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**, puis tapez : **Set-ExecutionPolicy Unrestricted**. Toutefois, cette configuration laisse tous les scripts non signés s’exécuter (moins sécurisé).

   Pour plus d’informations sur la signature des scripts Windows PowerShell, voir [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) dans la bibliothèque de documentation PowerShell.

6. Exécutez le script et, si vous y êtes invité, fournissez le mot de passe du compte d’administrateur Microsoft 365. Si vous modifiez le script et l’exécutez dans la même session Windows PowerShell, vous n’êtes pas invité à fournir des informations d’identification.

> [!TIP]
> Vous pouvez également utiliser ce script pour configurer IRM pour une bibliothèque SharePoint. Pour cette configuration, il se peut que vous vouliez activer l'option supplémentaire **Interdire aux utilisateurs de télécharger des documents qui ne prennent pas en charge IRM** pour vous assurer que la bibliothèque ne contient que des documents protégés.    Pour ce faire, ajoutez le paramètre `-IrmReject` à la commande Set-IrmConfiguration dans le script.
>
> Vous devez également modifier la `$webUrls` variable (par exemple, **https : \/ /contoso.SharePoint.com**) et la  `$listTitle` variable (par exemple, **$reports**).

Si vous devez désactiver IRM pour les bibliothèques OneDrive de l’utilisateur, consultez la section [script pour désactiver IRM pour onedrive](#script-to-disable-irm-for-onedrive) .

##### <a name="additional-script-to-output-all-onedrive-urls-to-a-csv-file"></a>Script supplémentaire pour générer toutes les URL OneDrive dans un. Fichier CSV

Pour l’étape 4c ci-dessus, vous pouvez utiliser le script Windows PowerShell suivant pour extraire les URL des bibliothèques OneDrive des utilisateurs, que vous pouvez ensuite vérifier, modifier si nécessaire, puis importer dans le script principal.

Ce script nécessite également le [Kit de développement logiciel (SDK) des composants clients SharePoint](https://www.microsoft.com/download/details.aspx?id=42038) et [SharePoint Management Shell](https://www.microsoft.com/download/details.aspx?id=35588). Suivez les mêmes instructions pour le copier et le coller, enregistrez le fichier localement (par exemple, sous « Report-OneDriveForBusinessSiteInfo.ps1 »), modifiez les valeurs `$sharepointAdminCenterUrl` et `$tenantAdmin` comme précédemment, puis exécutez le script.

*&#42;&#42;Exclusion de responsabilité&#42;&#42;* : cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d’aucune sorte.

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of a Microsoft 365 tenant to retrieve all OneDrive sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint service connection

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

# run a query against the Microsoft 365 tenant search service to retrieve all OneDrive URLs

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

##### <a name="script-to-disable-irm-for-onedrive"></a>Script pour désactiver IRM pour OneDrive

Utilisez l’exemple de script suivant si vous devez désactiver IRM pour les utilisateurs OneDrive.

Ce script nécessite également le [Kit de développement logiciel (SDK) des composants clients SharePoint](https://www.microsoft.com/download/details.aspx?id=42038) et [SharePoint Management Shell](https://www.microsoft.com/download/details.aspx?id=35588). Copiez et collez le contenu, enregistrez le fichier localement (par exemple, sous « Disable-IRMOnOneDriveForBusiness.ps1 »), puis modifiez les valeurs `$sharepointAdminCenterUrl` et `$tenantAdmin`. Spécifiez manuellement les URL OneDrive ou utilisez le script de la section précédente afin de pouvoir les importer, puis exécutez le script.

*&#42;&#42;Exclusion de responsabilité&#42;&#42;* : cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple de script est fourni TEL QUEL sans garantie d’aucune sorte.

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive and can also be used for SharePoint libraries and lists

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint service connection

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

# connect to Office365 first, required for SharePoint cmdlets to run

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
