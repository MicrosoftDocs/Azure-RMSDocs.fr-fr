---
title: Script PowerShell pour Azure RMS et l’infrastructure ICF - AIP
description: Exemple de script à copier et à modifier, comme indiqué dans les instructions Protection RMS avec l’infrastructure de classification des fichiers de Windows Server.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/19/2017
ms.topic: article
ms.service: information-protection
ms.assetid: ae6d8d0f-4ebc-43fe-a1f6-26b690fd83d0
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f9bbb0e9a1206caaf7319da5d96b8ad08e308664
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42806492"
---
# <a name="windows-powershell-script-for-azure-rms-protection-by-using-file-server-resource-manager-fci"></a>Script Windows PowerShell pour la protection Azure RMS à l’aide de l’ICF des outils de gestion de ressources pour serveur de fichiers

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012, Windows Server 2012 R2*

Cette page contient l’exemple de script à copier et à modifier, comme indiqué dans [Protection RMS avec l’infrastructure de classification des fichiers de Windows Server](configure-fci.md).

Ce script utilise **1.3.155.2** comme version minimale pour le module AzureInformationProtection. Exécutez la commande suivante pour vérifier la version : `(Get-Module AzureInformationProtection -ListAvailable).Version` 

*&#42;&#42;Exclusion de responsabilité&#42;&#42; : Cet exemple de script n’est pris en charge dans le cadre d’aucun programme ou service de support standard de Microsoft. Cet exemple*
*de script est fourni TEL QUEL sans garantie d’aucune sorte.*

```
<#
.SYNOPSIS 
     Helper script to protect all file types using the Azure Rights Management service and FCI.
.DESCRIPTION
     Protect files with the Azure Rights Management service and Windows Server FCI, using an RMS template ID and AzureInformationProtection module minimum version 1.3.155.2.   
#>
param(
            [Parameter(Mandatory = $false)]
            [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })]
            [string]$File,

            [Parameter(Mandatory = $false)]
            [string]$TemplateID,

            [Parameter(Mandatory = $false)]
            [string]$OwnerMail,

            [Parameter(Mandatory = $false)]
            [string]$AppPrincipalId = "<enter your AppPrincipalId here>",

            [Parameter(Mandatory = $false)]
            [string]$SymmetricKey = "<enter your key here>",

            [Parameter(Mandatory = $false)]
            [string]$BposTenantId = "<enter your BposTenantId here>"
) 

# script information
[String] $Script:Version = 'version 3.3' 
[String] $Script:Name = "RMS-Protect-FCI.ps1"

#global working variables
[switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running.

#**Functions (general helper)***************************************
function Get-ScriptName(){ 

    return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1)
}

#**Functions (script specific)**************************************

function Check-Module{

    param ([String]$Module = $(Throw "Module name not specified"))

    [bool]$isResult = $False

    #try to load the module
    if ((get-module -list -name $Module) -ne $nil)
        {

            $isResult = $True
        } else 
        
        {
            $isResult = $False
        } 

    return $isResult
}

function Protect-File ($ffile, $ftemplateId, $fownermail) {

    [bool] $returnValue = $false
    try {
        If ($OwnerMail -eq $null -or $OwnerMail -eq "") {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -DoNotPersistEncryptionKey All -TemplateID $ftemplateId
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId")
        } else {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -DoNotPersistEncryptionKey All -TemplateID $ftemplateId -OwnerEmail $fownermail
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail")
        }
    } catch {
        Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId")
            }
    return $returnValue
}

function Set-RMSConnection ($fappId, $fkey, $fbposId) {

    [bool] $returnValue = $false
    try {
               Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId
        Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")
        $returnValue = $true
    } catch {
        Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")

    }
    return $returnValue
}

#**Main Script (Script)*********************************************
Write-Host ("-== " + $Script:Name + " " + $Version + " ==-")

$Script:isScriptProcess = $True

# Validate Azure RMS connection by checking the module and then connection
if ($Script:isScriptProcess) {
        if (Check-Module -Module AzureInformationProtection){
        $Script:isScriptProcess = $True
    } else {

        Write-Host ("The AzureInformationProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black"           
        $Script:isScriptProcess = $False
    }
}

if ($Script:isScriptProcess) {
    #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" )  
    if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) {
        Write-Host ("Connected to Azure RMS")

    } else {
        Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black"
        $Script:isScriptProcess = $False
    }
}

#  Start working loop
if ($Script:isScriptProcess) {
    if ( !(($File -eq $null) -or ($File -eq "")) ) {
        if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) {
            $Script:isScriptProcess = $False           
        }
    }
}

# Closing
if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"}
write-host ("-== " + $Script:Name + " " + $Version + "  ==-")
if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

---

Retour à [Protection RMS avec l’infrastructure de classification des fichiers de Windows Server](configure-fci.md).
