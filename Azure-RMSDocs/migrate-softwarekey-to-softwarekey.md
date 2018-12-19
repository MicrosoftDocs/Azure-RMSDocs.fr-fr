---
title: Migrer une clé protégée par logiciel vers une autre clé protégée par logiciel - AIP
description: Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/11/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 959df427bc9424eea526ef09c00fbcecdef5a878
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53305061"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Étape 2 : Migration de clé protégée par logiciel à clé protégée par logiciel

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par logiciel. 

Si ce n’est pas le scénario de configuration que vous avez choisi, revenez à [l’Étape 4. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une configuration différente.

La procédure suivante permet d’importer la configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Pour importer les données de configuration dans Azure Information Protection

1. Sur une station de travail connectée à Internet, utilisez l’applet de commande [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) pour vous connecter au service Azure Rights Management :

    ```
    Connect-AadrmService
    ```
    Quand vous y êtes invité, entrez vos informations d’identification d’administrateur locataire Azure Rights Management (en général, vous utilisez un compte d’administrateur général pour Azure Active Directory ou Office 365).

2. Utilisez l’applet de commande [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) pour charger chaque fichier (.xml) de domaine de publication approuvé exporté. Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2. 
    
    Pour exécuter cette applet de commande, vous aurez besoin du mot de passe que vous avez spécifié précédemment pour chaque fichier de données de configuration. 
    
    Par exemple, exécutez tout d’abord la commande suivante pour stocker le mot de passe :
    
        $TPD_Password = Read-Host -AsSecureString
    
    Entrez le mot de passe que vous avez spécifié pour exporter le premier fichier de données de configuration. Ensuite, à l’aide de E:\contosokey1.xml comme exemple pour ce fichier de configuration, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :
    ```
    Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Lorsque vous avez chargé chaque fichier, exécutez [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) pour identifier la clé importée qui correspond à la clé SLC actuellement active dans AD RMS. Cette clé devient la clé de locataire active pour votre service Azure Rights Management.

4.  Utilisez l’applet de commande [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) pour vous déconnecter du service Azure Rights Management :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à [l’Étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


