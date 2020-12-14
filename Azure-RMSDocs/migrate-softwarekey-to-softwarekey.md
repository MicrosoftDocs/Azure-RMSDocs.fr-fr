---
title: Migrer une clé protégée par logiciel vers une autre clé protégée par logiciel - AIP
description: Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a9ef31330b5bc0039ad01f76134ebb5075edd1e6
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383735"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel

>**S’applique à*: services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel. 

S’il ne s’agit pas du scénario de configuration que vous avez choisi, revenez à l' [étape 4. Exportez les données de configuration de AD RMS, puis importez-les dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une autre configuration.

La procédure suivante permet d’importer la configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Pour importer les données de configuration dans Azure Information Protection

1. Sur une station de travail connectée à Internet, utilisez l’applet de commande [Connect-AipService](/powershell/module/aipservice/connect-aipservice) pour vous connecter au service Azure Rights Management :

    ```PowerShell
    Connect-AipService
    ```
    
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur de locataires Azure Rights Management (en général, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Office 365).

2. Utilisez l’applet de commande [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) pour télécharger chaque fichier Trusted Publishing Domain (. Xml) exporté. Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2. 
    
    Pour exécuter cette applet de commande, vous aurez besoin du mot de passe que vous avez spécifié précédemment pour chaque fichier de données de configuration. 
    
    Par exemple, exécutez tout d’abord la commande suivante pour stocker le mot de passe :
    
    ```PowerShell
    $TPD_Password = Read-Host -AsSecureString
    ```

    Entrez le mot de passe que vous avez spécifié pour exporter le premier fichier de données de configuration. Ensuite, à l’aide de E:\contosokey1.xml comme exemple pour ce fichier de configuration, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :

    ```PowerShell
    Import-AipServiceTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Une fois que vous avez chargé chaque fichier, exécutez [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) pour identifier la clé importée qui correspond à la clé de licence en tant que actuellement active dans AD RMS. Cette clé devient la clé de locataire active pour votre service Azure Rights Management.

4.  Utilisez l’applet de commande [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice) pour vous déconnecter du service Azure Rights Management :

    ```PowerShell
    Disconnect-AipServiceService
    ```

Vous êtes maintenant prêt à passer à l' [étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


