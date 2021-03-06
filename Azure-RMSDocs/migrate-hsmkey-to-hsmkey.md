---
title: Migration de clé protégée par HSM vers une autre clé protégée par HSM - AIP
description: Les instructions qui font partie du chemin de migration de AD RMS à Azure Information Protection, et s’appliquent uniquement si votre clé de AD RMS est protégée par HSM et que vous souhaitez migrer vers Azure Information Protection à l’aide d’une clé de locataire protégée par HSM dans Azure Key Vault.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1ce00be84ddde6493c5b8851fa8473024e08dc00
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382052"
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>Étape 2 : Migration de clé protégée par HSM à clé protégée par HSM

>***S’applique à**: services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault. 

S’il ne s’agit pas du scénario de configuration que vous avez choisi, revenez à l' [étape 4. Exportez les données de configuration de AD RMS, puis importez-les dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une autre configuration.

> [!NOTE]
> Ces instructions supposent que votre clé AD RMS est protégée par module. Il s’agit du cas le plus classique. 

Cette procédure en deux parties permet d’importer votre clé HSM et votre configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par l’utilisateur (BYOK).

Comme votre clé de locataire Azure Information Protection est stockée et gérée par Azure Key Vault, cette partie de la migration nécessite une administration dans Azure Key Vault, en plus d’Azure Information Protection. Si Azure Key Vault est géré par un autre administrateur que celui de votre organisation, vous devez coordonner et travailler avec cet administrateur pour effectuer ces procédures.

Avant de commencer, vérifiez que votre organisation dispose d’un coffre de clés qui a été créé dans Azure Key Vault et qu’il prend en charge les clés protégées par HSM. Bien que ce ne soit pas obligatoire, nous vous recommandons d’avoir un coffre de clés dédié pour Azure Information Protection. Ce coffre de clés doit être configuré de façon à autoriser le service Azure Rights Management à y accéder : les clés stockées dans ce coffre de clés doivent donc être limitées aux clés Azure Information Protection.


> [!TIP]
> Si vous effectuez les étapes de configuration pour Azure Key Vault et que vous n’êtes pas familiarisé avec ce service Azure, il peut être utile de consulter d’abord [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Partie 1 : Transfert de votre clé HSM vers Azure Key Vault

Ces procédures sont effectuées par l’administrateur d’Azure Key Vault.

1. Pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, suivez les instructions de la documentation d’Azure Key Vault, notamment [Implémentation de BYOK pour Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) avec l’exception suivante :

   - N’effectuez pas les étapes pour **Générer votre clé de locataire** car vous avez déjà l’équivalent dans votre déploiement AD RMS. Au lieu de cela, identifiez les clés utilisées par votre serveur AD RMS à partir de l’installation nCipher et préparez ces clés pour le transfert, puis transférez-les vers Azure Key Vault. 
        
        Les fichiers de clé chiffrés pour nCipher sont nommés **key_<<em>keyAppName</em>>_<<em>KeyIdentifier</em> >** localement sur le serveur. Par exemple, `C:\Users\All Users\nCipher\Key Management Data\local\key_mscapi_f829e3d888f6908521fe3d91de51c25d27116a54`. Vous aurez besoin de la valeur **mscapi** comme keyAppName, ainsi que de votre propre valeur pour l’identificateur de clé lorsque vous exécutez la commande KeyTransferRemote pour créer une copie de la clé avec des autorisations réduites.
        
        Quand la clé se charge dans Azure Key Vault, vous voyez s’afficher les propriétés de la clé, notamment l’ID de clé. Elle doit ressembler à https \: //ContosoRMS-kV.vault.Azure.net/Keys/ContosoRMS-Byok/aaaabbbbcccc111122223333. Prenez note de cette URL, car l’administrateur Azure Information Protection en a besoin pour indiquer au service Azure Rights Management d’utiliser cette clé pour sa clé de locataire.

2. Sur la station de travail connectée à Internet, dans une session PowerShell, utilisez l’applet de commande [Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) pour autoriser le principal du service Azure Rights Management à accéder au coffre de clés qui stocke la clé de locataire Azure information protection. Les autorisations nécessaires sont déchiffrer, chiffrer, désencapsuler la clé (unwrapkey), encapsuler la clé (wrapkey), vérifier et signer.
    
    Par exemple, si le coffre de clés que vous avez créé pour Azure Information Protection est nommé contoso-byok-ky et que votre groupe de ressources est nommé contoso-byok-rg, exécutez la commande suivante :

    ```sh
    Set-AzKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get
    ```

Maintenant que vous avez préparé votre clé HSM dans Azure Key Vault pour le service Azure Rights Management d’Azure Information Protection, vous êtes prêt à importer vos données de configuration AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Partie 2 : Importer les données de configuration dans Azure Information Protection

Ces procédures sont effectuées par l’administrateur d’Azure Information Protection.

1. Sur la station de travail connectée à Internet et dans la session PowerShell, connectez-vous au service Azure Rights Management à l’aide de l’applet de commande [Connect-AipService](/powershell/module/aipservice/connect-aipservice) .
    
    Téléchargez ensuite chaque fichier trusted publishing domain (. Xml) à l’aide de l’applet de commande [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) . Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2.
    
    Pour exécuter cette applet de commande, vous avez besoin du mot de passe que vous avez spécifié précédemment pour chaque fichier de données de configuration et de l’URL de la clé qui a été identifiée à l’étape précédente.
    
    Par exemple, à l’aide d’un fichier de données de configuration de C:\contoso_tpd1.xml et de l’URL de notre clé issue de l’étape précédente, exécutez d’abord la commande suivante pour stocker le mot de passe :
    
    ```ps
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    Entrez le mot de passe que vous avez spécifié pour exporter le fichier de données de configuration. Ensuite, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :
    
    ```ps
    Import-AipServiceTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultKeyUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    Dans le cadre de cette importation, la clé SLC est importée et définie automatiquement comme archivée.

2.  Une fois que vous avez chargé chaque fichier, exécutez [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) pour spécifier la clé importée qui correspond à la clé de licence en tant que actuellement active dans votre cluster AD RMS. Cette clé devient la clé de locataire active pour votre service Azure Rights Management.

3.  Utilisez l’applet de commande [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice) pour vous déconnecter du service Azure Rights Management :

    ```ps
    Disconnect-AipServiceService
    ```

Si vous devez ensuite confirmer la clé que votre clé de locataire Azure Information Protection utilise dans Azure Key Vault, utilisez l’applet de commande [AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) Azure RMS.

Vous êtes maintenant prêt à passer à l' [étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


