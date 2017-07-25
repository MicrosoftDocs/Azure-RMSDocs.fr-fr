---
title: "Migration de clé protégée par logiciel vers une clé protégée par HSM - AIP"
description: "Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/19/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d942e51994c6db3ee0c3e1127991a7007ed91f92
ms.sourcegitcommit: 52ad844cd42479a56b1ae0e56ba0614f088d8a1a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/20/2017
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>Étape 2 : Migration de clé protégée par logiciel à clé protégée par HSM

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault. 

Si ce n’est pas le scénario de configuration que vous avez choisi, revenez à [l’Étape 4. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une configuration différente.

Cette procédure en quatre parties permet d’importer la configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par l’utilisateur (BYOK) dans Azure Key Vault.

Vous devez d’abord extraire votre clé de certificat de licence serveur des données de configuration AD RMS, transférer la clé vers un module de sécurité matériel (HSM) Thales local, empaqueter et transférer votre clé HSM vers Azure Key Vault, autoriser le service Azure Rights Management d’Azure Information Protection à accéder à votre coffre de clés, puis importer les données de configuration.

Comme votre clé de locataire Azure Information Protection est stockée et gérée par Azure Key Vault, cette partie de la migration nécessite une administration dans Azure Key Vault, en plus d’Azure Information Protection. Si Azure Key Vault est géré par un autre administrateur que celui de votre organisation, vous devez coordonner et travailler avec cet administrateur pour effectuer ces procédures.

Avant de commencer, vérifiez que votre organisation dispose d’un coffre de clés qui a été créé dans Azure Key Vault et qu’il prend en charge les clés protégées par HSM. Bien que ce ne soit pas obligatoire, nous vous recommandons d’avoir un coffre de clés dédié pour Azure Information Protection. Ce coffre de clés doit être configuré de façon à autoriser le service Azure Rights Management d’Azure Information Protection à y accéder : les clés stockées dans ce coffre de clés doivent donc être limitées aux clés Azure Information Protection.


> [!TIP]
> Si vous effectuez les étapes de configuration pour Azure Key Vault et que vous n’êtes pas familiarisé avec ce service Azure, il peut être utile de consulter d’abord [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>Partie 1 : Extraction de votre certificat de licence serveur des données de configuration et importation de la clé dans votre HSM local

1.  Administrateur Azure Key Vault : pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, utilisez les étapes suivantes de la section [Implémentation de BYOK pour Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azurekey-vault) de la documentation d’Azure Key Vault :

    -   **Générer et transférer votre clé vers le HSM d’Azure Key Vault** : [Étape 1 : Préparation de la station de travail connectée à Internet](/azure/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Générer et transférer votre clé de locataire via Internet** : [Étape 2 : Préparation de votre poste de travail déconnecté](/azure/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    Ne suivez pas ces étapes pour générer votre clé de client, car vous avez déjà l'équivalent dans le fichier (.xml) de données de configuration exporté. Exécutez plutôt un outil pour extraire cette clé du fichier et l’importer dans votre HSM local. L’outil crée deux fichiers quand vous l’exécutez :

    - Un nouveau fichier de données de configuration sans la clé, qui est alors prêt à être importé dans votre locataire Azure Information Protection.

    - Un fichier PEM (conteneur de clé) avec la clé, qui est alors prêt à être importé dans votre HSM local.

2. Administrateur Azure Information Protection ou administrateur Azure Key Vault : sur la station de travail déconnectée, exécutez l’outil TpdUtil à partir du [Kit de migration Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Par exemple, si l’outil est installé sur votre lecteur E où vous copiez votre fichier de données de configuration nommé ContosoTPD.xml :

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    Si vous avez plusieurs fichiers de données de configuration RMS, exécutez l’outil pour les autres fichiers.

    Pour consulter l’aide de cet outil, qui comprend sa description, son fonctionnement et des exemples, exécutez TpdUtil.exe sans paramètres.

    Informations supplémentaires sur cette commande :

    - **/tpd** : spécifie le chemin complet et le nom du fichier de données de configuration AD RMS exporté. Le nom complet du paramètre est **TpdFilePath**.

    - **/otpd** : spécifie le nom de fichier de sortie pour le fichier de données de configuration sans la clé. Le nom complet du paramètre est **OutPfxFile**. Si vous ne spécifiez pas ce paramètre, le fichier de sortie a par défaut le nom de fichier d’origine avec le suffixe **_keyless**, et il est stocké dans le dossier actif.

    - **/opem** : spécifie le nom de fichier de sortie pour le fichier PEM, qui contient la clé extraite. Le nom complet du paramètre est **OutPemFile**. Si vous ne spécifiez pas ce paramètre, le fichier de sortie a par défaut le nom de fichier d’origine avec le suffixe **_key**, et il est stocké dans le dossier actif.

    - Si vous ne spécifiez pas le mot de passe quand vous exécutez cette commande (en utilisant le nom complet du paramètre **TpdPassword** ou son nom court **pwd**), vous êtes invité à le spécifier.

3. Sur la même station de travail déconnectée, attachez et configurez votre HSM Thales, conformément à votre documentation Thales. Vous pouvez maintenant importer votre clé dans votre HSM Thales attaché en utilisant la commande suivante, où vous devez remplacer ContosoTPD.pem par votre propre nom de fichier :

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >Si vous avez plusieurs fichiers, choisissez le fichier qui correspond à la clé HSM à utiliser dans Azure RMS pour protéger le contenu après la migration.

    Ceci génère l’affichage d’un résultat similaire au suivant :

    **paramètres de génération de clé :**

    **opération &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Opération à réaliser&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; importer**

    **application &nbsp;&nbsp;&nbsp;&nbsp;Application&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; simple**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Vérifier la sécurité de la clé de configuration&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oui**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Type de clé&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; fichier PEM contenant la clé RSA &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Identificateur de clé &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Nom de la clé &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **La clé a été importée.**

    **Chemin de la clé : C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Ce résultat confirme que la clé privée est maintenant migrée vers votre appareil HSM Thales local avec une copie chiffrée enregistrée dans une clé (dans notre exemple, « key_simple_contosobyok »). 

Maintenant que votre clé de licence serveur a été extraite et importée dans votre HSM local, vous êtes prêt à empaqueter la clé protégée par HSM et à la transférer dans Azure Key Vault.

> [!IMPORTANT]
> Quand vous avez terminé cette étape, pour des raisons de sécurité, effacez ces fichiers PEM sur la station de travail déconnectée pour qu’ils ne soient pas accessibles à des personnes non autorisées. Par exemple, exécutez « cipher /w: E » pour supprimer de façon sûre tous les fichiers du lecteur E:.

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>Partie 2 : Empaquetage et transfert de votre clé HSM vers Azure Key Vault

Administrateur Azure Key Vault : pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, utilisez les étapes suivantes de la section [Implémentation de BYOK pour Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azurekey-vault) de la documentation d’Azure Key Vault :

- [Étape 4 : Préparation de votre clé pour le transfert](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

- [Étape 5 : Transfert de votre clé vers Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azurekey-vault)

Ne suivez pas les étapes pour générer votre paire de clés, car vous avez déjà la clé. Exécutez plutôt une commande pour transférer cette clé (dans notre exemple, notre paramètre KeyIdentifier utilise « contosobyok ») depuis votre HSM local.

Avant de transférer votre clé vers Azure Key Vault, vérifiez que l’utilitaire KeyTransferRemote.exe retourne **Résultat : RÉUSSITE** quand vous créez une copie de votre clé avec des autorisations réduites (étape 4.1) et quand vous chiffrez votre clé (étape 4.3).

Quand la clé se charge dans Azure Key Vault, vous voyez s’afficher les propriétés de la clé, notamment l’ID de clé. Elle ressemble à ceci : **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Prenez note de cette URL, car l’administrateur Azure Information Protection en a besoin pour indiquer au service Azure Rights Management d’Azure Information Protection d’utiliser cette clé pour sa clé de locataire.

Utilisez ensuite l’applet de commande [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) pour autoriser le principal du service Azure Rights Management à accéder au coffre de clés. Les autorisations nécessaires sont déchiffrer, chiffrer, désencapsuler la clé (unwrapkey), encapsuler la clé (wrapkey), vérifier et signer.

Par exemple, si le coffre de clés que vous avez créé pour Azure Information Protection est nommé contosorms-bvok-ky et que votre groupe de ressources est nommé contosorms-byok-rg, exécutez la commande suivante :
    
    Set-AzureRmKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

Maintenant que vous avez transféré votre clé HSM dans Azure Key Vault, vous êtes prêt à importer vos données de configuration AD RMS.

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>Partie 3 : Importer les données de configuration dans Azure Information Protection

1. Administrateur Azure Information Protection : sur le poste de travail connecté à Internet et dans la session PowerShell, copiez vos nouveaux fichiers de données de configuration (.xml) où la clé de certificat de licence serveur (SLC) a été supprimée après l’exécution de l’outil TpdUtil.

2. Chargez chaque fichier .xml en utilisant l’applet de commande [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2.

    Pour exécuter cette applet de commande, vous avez besoin du mot de passe que vous avez spécifié précédemment pour le fichier de données de configuration et de l’URL de la clé qui a été identifiée à l’étape précédente.

    Par exemple, à l’aide d’un fichier de données de configuration de C:\contoso_keyless.xml et de l’URL de notre clé issue de l’étape précédente, exécutez d’abord la commande suivante pour stocker le mot de passe :
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   Entrez le mot de passe que vous avez spécifié pour exporter le fichier de données de configuration. Ensuite, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    Dans le cadre de cette importation, la clé SLC est importée et définie automatiquement comme archivée.

3. Lorsque vous avez chargé chaque fichier, exécutez [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) pour spécifier quelle clé importée correspond à la clé SLC actuellement active dans votre cluster AD RMS.

4. Utilisez l’applet de commande [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) pour vous déconnecter du service Azure Rights Management :

    ```
    Disconnect-AadrmService
    ```

Si vous avez besoin ultérieurement de vérifier quelle clé est utilisée par votre clé de locataire Azure Information Protection dans Azure Key Vault, utilisez l’applet de commande [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) d’Azure RMS.


Vous êtes maintenant prêt à passer à [l’Étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

