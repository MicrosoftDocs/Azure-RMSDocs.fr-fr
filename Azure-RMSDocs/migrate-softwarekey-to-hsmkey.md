---
title: Migration de clé protégée par logiciel vers une clé protégée par HSM - AIP
description: Instructions qui font partie du chemin de migration d’AD RMS vers Azure Information Protection. Celles-ci s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: df049f9071c05c1e1a25e57ecb96730aedd5646f
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049069"
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>Étape 2 : Migration de clé protégée par logiciel à clé protégée par HSM

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). Elles s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Information Protection avec une clé de locataire protégée par HSM dans Azure Key Vault. 

S’il ne s’agit pas du scénario de configuration que vous avez choisi, revenez à l' [étape 4. Exportez les données de configuration de AD RMS, puis importez-les dans Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) et choisissez une autre configuration.

Cette procédure en quatre parties permet d’importer la configuration AD RMS dans Azure Information Protection pour que votre clé de locataire Azure Information Protection soit gérée par l’utilisateur (BYOK) dans Azure Key Vault.

Vous devez d’abord extraire votre clé de certificat de licence serveur à partir des données de configuration AD RMS et transférer la clé vers un HSM nCipher local, le package suivant et transférer votre clé HSM vers Azure Key Vault, puis autoriser le service de Rights Management Azure à partir de Azure Information Protection pour accéder à votre coffre de clés, puis importer les données de configuration.

Comme votre clé de locataire Azure Information Protection est stockée et gérée par Azure Key Vault, cette partie de la migration nécessite une administration dans Azure Key Vault, en plus d’Azure Information Protection. Si Azure Key Vault est géré par un autre administrateur que celui de votre organisation, vous devez coordonner et travailler avec cet administrateur pour effectuer ces procédures.

Avant de commencer, vérifiez que votre organisation dispose d’un coffre de clés qui a été créé dans Azure Key Vault et qu’il prend en charge les clés protégées par HSM. Bien que ce ne soit pas obligatoire, nous vous recommandons d’avoir un coffre de clés dédié pour Azure Information Protection. Ce coffre de clés doit être configuré de façon à autoriser le service Azure Rights Management d’Azure Information Protection à y accéder : les clés stockées dans ce coffre de clés doivent donc être limitées aux clés Azure Information Protection.


> [!TIP]
> Si vous effectuez les étapes de configuration pour Azure Key Vault et que vous n’êtes pas familiarisé avec ce service Azure, il peut être utile de consulter d’abord [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>Partie 1 : Extraction de votre certificat de licence serveur des données de configuration et importation de la clé dans votre HSM local

1.  Administrateur Azure Key Vault : pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, utilisez les étapes suivantes de la section [Implémentation de BYOK pour Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) de la documentation d’Azure Key Vault :

    -   **Génération et transfert de votre clé vers Azure Key Vault HSM**: [étape 1 : préparer votre station de travail connectée à Internet](/azure/key-vault/key-vault-hsm-protected-keys#step-1-prepare-your-internet-connected-workstation)

    -   **Génération et transfert de votre clé de locataire – via Internet**: [étape 2 : préparer votre station de travail déconnectée](/azure/key-vault/key-vault-hsm-protected-keys#step-2-prepare-your-disconnected-workstation)

    Ne suivez pas ces étapes pour générer votre clé de client, car vous avez déjà l'équivalent dans le fichier (.xml) de données de configuration exporté. Exécutez plutôt un outil pour extraire cette clé du fichier et l’importer dans votre HSM local. L’outil crée deux fichiers quand vous l’exécutez :

    - Un nouveau fichier de données de configuration sans la clé, qui est alors prêt à être importé dans votre locataire Azure Information Protection.

    - Un fichier PEM (conteneur de clé) avec la clé, qui est alors prêt à être importé dans votre HSM local.

2. Administrateur Azure Information Protection ou administrateur Azure Key Vault : sur la station de travail déconnectée, exécutez l’outil TpdUtil à partir du [Kit de migration Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Par exemple, si l’outil est installé sur votre lecteur E où vous copiez votre fichier de données de configuration nommé ContosoTPD.xml :

    ```ps
    E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    Si vous avez plusieurs fichiers de données de configuration RMS, exécutez l’outil pour les autres fichiers.

    Pour consulter l’aide de cet outil, qui comprend sa description, son fonctionnement et des exemples, exécutez TpdUtil.exe sans paramètres.

    Informations supplémentaires sur cette commande :

    - **/tpd** : spécifie le chemin complet et le nom du fichier de données de configuration AD RMS exporté. Le nom complet du paramètre est **TpdFilePath**.

    - **/otpd** : spécifie le nom de fichier de sortie pour le fichier de données de configuration sans la clé. Le nom complet du paramètre est **OutPfxFile**. Si vous ne spécifiez pas ce paramètre, le fichier de sortie a par défaut le nom de fichier d’origine avec le suffixe **_keyless**, et il est stocké dans le dossier actif.

    - **/opem** : spécifie le nom de fichier de sortie pour le fichier PEM, qui contient la clé extraite. Le nom complet du paramètre est **OutPemFile**. Si vous ne spécifiez pas ce paramètre, le fichier de sortie a par défaut le nom de fichier d’origine avec le suffixe **_key**, et il est stocké dans le dossier actif.

    - Si vous ne spécifiez pas le mot de passe quand vous exécutez cette commande (en utilisant le nom complet du paramètre **TpdPassword** ou son nom court **pwd**), vous êtes invité à le spécifier.

3. Sur la même station de travail déconnectée, attachez et configurez votre HSM nCipher, en fonction de votre documentation nCipher. Vous pouvez maintenant importer votre clé dans votre HSM nCipher attaché à l’aide de la commande suivante, où vous devez remplacer votre propre nom de fichier par ContosoTPD. pem :

    ```sh
    generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA
    ```

    > [!NOTE]
    >Si vous avez plusieurs fichiers, choisissez le fichier qui correspond à la clé HSM à utiliser dans Azure RMS pour protéger le contenu après la migration.

    Ceci génère l’affichage d’un résultat similaire au suivant :

    **paramètres de génération de clé :**

    **opération &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; d’opération pour effectuer l' &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; importation**

    **application d’application &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; simple**

    **vérifier la &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; sécurité de la clé de configuration &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Oui**

    **type de clé de type &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; RSA**

    **&nbsp; &nbsp; fichier PEM pemreadfile contenant la clé RSA &nbsp; &nbsp; e:\ContosoTPD.pem**

    **ident &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Key identifier &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; contosobyok**

    **nom de la &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; clé plainname &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ContosoBYOK**

    **La clé a été importée avec succès.**

    **Chemin de la clé : C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Cette sortie confirme que la clé privée est maintenant migrée vers votre appareil nCipher HSM local avec une copie chiffrée enregistrée dans une clé (dans notre exemple, « key_simple_contosobyok »). 

Maintenant que votre clé de licence serveur a été extraite et importée dans votre HSM local, vous êtes prêt à empaqueter la clé protégée par HSM et à la transférer dans Azure Key Vault.

> [!IMPORTANT]
> Quand vous avez terminé cette étape, pour des raisons de sécurité, effacez ces fichiers PEM sur la station de travail déconnectée pour qu’ils ne soient pas accessibles à des personnes non autorisées. Par exemple, exécutez « cipher /w: E » pour supprimer de façon sûre tous les fichiers du lecteur E:.

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>Partie 2 : Empaquetage et transfert de votre clé HSM vers Azure Key Vault

Administrateur Azure Key Vault : pour chaque clé SLC exportée que vous voulez stocker dans Azure Key Vault, utilisez les étapes suivantes de la section [Implémentation de BYOK pour Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) de la documentation d’Azure Key Vault :

- [Étape 4 : Préparer votre clé pour le transfert](/azure/key-vault/key-vault-hsm-protected-keys#step-4-prepare-your-key-for-transfer)

- [Étape 5 : Transférer votre clé vers Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#step-5-transfer-your-key-to-azure-key-vault)

Ne suivez pas les étapes pour générer votre paire de clés, car vous avez déjà la clé. Exécutez plutôt une commande pour transférer cette clé (dans notre exemple, notre paramètre KeyIdentifier utilise « contosobyok ») depuis votre HSM local.

Avant de transférer votre clé vers Azure Key Vault, vérifiez que l’utilitaire KeyTransferRemote.exe retourne **Résultat : RÉUSSITE** quand vous créez une copie de votre clé avec des autorisations réduites (étape 4.1) et quand vous chiffrez votre clé (étape 4.3).

Quand la clé se charge dans Azure Key Vault, vous voyez s’afficher les propriétés de la clé, notamment l’ID de clé. Elle doit ressembler à **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** . Prenez note de cette URL, car l’administrateur Azure Information Protection en a besoin pour indiquer au service Azure Rights Management d’Azure Information Protection d’utiliser cette clé pour sa clé de locataire.

Utilisez ensuite l’applet de commande [Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) pour autoriser le principal du service Azure Rights Management à accéder au coffre de clés. Les autorisations nécessaires sont déchiffrer, chiffrer, désencapsuler la clé (unwrapkey), encapsuler la clé (wrapkey), vérifier et signer.

Par exemple, si le coffre de clés que vous avez créé pour Azure Information Protection est nommé contosorms-bvok-ky et que votre groupe de ressources est nommé contosorms-byok-rg, exécutez la commande suivante :

```sh
Set-AzKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get
```

Maintenant que vous avez transféré votre clé HSM dans Azure Key Vault, vous êtes prêt à importer vos données de configuration AD RMS.

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>Partie 3 : Importer les données de configuration dans Azure Information Protection

1. Azure Information Protection administrateur : sur la station de travail connectée à Internet et dans la session PowerShell, copiez vos nouveaux fichiers de données de configuration (. Xml) dont la clé de licence est supprimée après l’exécution de l’outil TpdUtil.

2. Téléchargez chaque fichier. XML à l’aide de l’applet de commande [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) . Par exemple, vous devez disposer d’au moins un fichier supplémentaire à importer si vous avez mis à niveau votre cluster AD RMS pour le Mode de chiffrement 2.

    Pour exécuter cette applet de commande, vous avez besoin du mot de passe que vous avez spécifié précédemment pour le fichier de données de configuration et de l’URL de la clé qui a été identifiée à l’étape précédente.

    Par exemple, à l’aide d’un fichier de données de configuration de C:\contoso_keyless.xml et de l’URL de notre clé issue de l’étape précédente, exécutez d’abord la commande suivante pour stocker le mot de passe :
    
    ```ps
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   Entrez le mot de passe que vous avez spécifié pour exporter le fichier de données de configuration. Ensuite, exécutez la commande suivante et confirmez que vous souhaitez effectuer cette action :

    ```ps
    Import-AipServiceTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    Dans le cadre de cette importation, la clé SLC est importée et définie automatiquement comme archivée.

3. Une fois que vous avez chargé chaque fichier, exécutez [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) pour spécifier la clé importée qui correspond à la clé de licence en tant que actuellement active dans votre cluster AD RMS.

4. Utilisez l’applet de commande [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice) pour vous déconnecter du service Azure Rights Management :

    ```ps
    Disconnect-AipServiceService
    ```

Si vous devez ensuite confirmer la clé que votre clé de locataire Azure Information Protection utilise dans Azure Key Vault, utilisez l’applet de commande [AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) Azure RMS.


Vous êtes maintenant prêt à passer à l' [étape 5. Activez le service Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


