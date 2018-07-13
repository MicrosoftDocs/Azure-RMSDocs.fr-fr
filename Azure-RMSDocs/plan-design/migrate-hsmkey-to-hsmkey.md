---
title: Migration de clé protégée par HSM vers une autre clé protégée par HSM - AIP
description: Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 757b3af36fb15c3069c5bef7ca4509ff92cee1f9
ms.sourcegitcommit: 0fda9ea4a7b91d4bb3a9e4f9d5cc4106ce1e2d43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38973322"
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>Étape 2 : Migration de clé protégée par HSM à clé protégée par HSM

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault. 

Si ce n’est pas le scénario de configuration que vous avez choisi, revenez à [l’Étape 4. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une configuration différente.

> [!NOTE]
> Ces instructions supposent que votre clé AD RMS est protégée par module. Il s’agit du cas le plus classique. 

Cette procédure en deux parties permet d’importer votre clé HSM et votre configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par l’utilisateur (BYOK).

Comme votre clé de locataire Azure Information Protection est stockée et gérée par Azure Key Vault, cette partie de la migration nécessite une administration dans Azure Key Vault, en plus d’Azure Information Protection. Si Azure Key Vault est géré par un autre administrateur que celui de votre organisation, vous devez coordonner et travailler avec cet administrateur pour effectuer ces procédures.

Avant de commencer, vérifiez que votre organisation dispose d’un coffre de clés qui a été créé dans Azure Key Vault et qu’il prend en charge les clés protégées par HSM. Bien que ce ne soit pas obligatoire, nous vous recommandons d’avoir un coffre de clés dédié pour Azure Information Protection. Ce coffre de clés doit être configuré de façon à autoriser le service Azure Rights Management à y accéder : les clés stockées dans ce coffre de clés doivent donc être limitées aux clés Azure Information Protection.


> [!TIP]
> Si vous effectuez les étapes de configuration pour Azure Key Vault et que vous n’êtes pas familiarisé avec ce service Azure, il peut être utile de consulter d’abord [Prise en main d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Partie 1 : Transfert de votre clé HSM vers Azure Key Vault

Ces procédures sont effectuées par l’administrateur d’Azure Key Vault.

1. Pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, suivez les instructions de la documentation d’Azure Key Vault, notamment [Implémentation de BYOK pour Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azurekey-vault) avec l’exception suivante :

    - N’effectuez pas les étapes pour **Générer votre clé de locataire** car vous avez déjà l’équivalent dans votre déploiement AD RMS. Identifiez plutôt la clé utilisée par votre serveur AD RMS dans l’installation Thales et utilisez cette clé lors de la migration. Les fichiers de clés chiffrées Thales sont généralement nommés **key<*nom_application_clé*><*identificateur_clé*>** localement sur le serveur.

    Quand la clé se charge dans Azure Key Vault, vous voyez s’afficher les propriétés de la clé, notamment l’ID de clé. Cela doit ressembler à https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Prenez note de cette URL, car l’administrateur Azure Information Protection en a besoin pour indiquer au service Azure Rights Management d’utiliser cette clé pour sa clé de locataire.

2. Sur la station de travail connectée à Internet, dans une session PowerShell, utilisez l’applet de commande [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) pour autoriser le principal du service Azure Rights Management à accéder au Key Vault qui stocke la clé de locataire Azure Information Protection. Les autorisations nécessaires sont déchiffrer, chiffrer, désencapsuler la clé (unwrapkey), encapsuler la clé (wrapkey), vérifier et signer.
    
    Par exemple, si le coffre de clés que vous avez créé pour Azure Information Protection est nommé contoso-byok-ky et que votre groupe de ressources est nommé contoso-byok-rg, exécutez la commande suivante :
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


Maintenant que vous avez préparé votre clé HSM dans Azure Key Vault pour le service Azure Rights Management d’Azure Information Protection, vous êtes prêt à importer vos données de configuration AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Partie 2 : Importer les données de configuration dans Azure Information Protection

Ces procédures sont effectuées par l’administrateur d’Azure Information Protection.

1. Sur la station de travail connectée à Internet et dans la session PowerShell, connectez-vous au service Azure Rights Management en utilisant l’applet de commande [Connnect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice).
    
    Ensuite, chargez chaque fichier exporté de domaine de publication approuvé (.xml) en utilisant l’applet de commande [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2.
    
    Pour exécuter cette applet de commande, vous avez besoin du mot de passe que vous avez spécifié précédemment pour chaque fichier de données de configuration et de l’URL de la clé qui a été identifiée à l’étape précédente.
    
    Par exemple, à l’aide d’un fichier de données de configuration de C:\contoso_tpd1.xml et de l’URL de notre clé issue de l’étape précédente, exécutez d’abord la commande suivante pour stocker le mot de passe :
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    Entrez le mot de passe que vous avez spécifié pour exporter le fichier de données de configuration. Ensuite, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    Dans le cadre de cette importation, la clé SLC est importée et définie automatiquement comme archivée.

2.  Lorsque vous avez chargé chaque fichier, exécutez [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) pour spécifier quelle clé importée correspond à la clé SLC actuellement active dans votre cluster AD RMS. Cette clé devient la clé de locataire active pour votre service Azure Rights Management.

3.  Utilisez l’applet de commande [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) pour vous déconnecter du service Azure Rights Management :

    ```
    Disconnect-AadrmService
    ```

Si vous avez besoin ultérieurement de vérifier quelle clé est utilisée par votre clé de locataire Azure Information Protection dans Azure Key Vault, utilisez l’applet de commande [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) d’Azure RMS.

Vous êtes maintenant prêt à passer à [l’Étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

