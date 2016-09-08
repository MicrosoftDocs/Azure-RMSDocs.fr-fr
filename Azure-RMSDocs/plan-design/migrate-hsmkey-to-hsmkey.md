---
title: "Étape 2 &colon; Migration de clé protégée par HSM à clé protégée par HSM | Azure RMS"
description: "Ces instructions font partie du chemin de migration d’AD RMS vers Azure Rights Management. Elles s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous voulez migrer vers Azure Rights Management avec une clé de locataire protégée avec HSM dans Azure Key Vault."
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 690729d16358b7b997d9cd1fd8cabed22ce78df4


---

# Étape 2 : Migration de clé protégée par HSM à clé protégée par HSM

>*S’applique à : Active Directory Rights Management Services, Azure Rights Management*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), et s’appliquent uniquement si votre clé AD RMS est protégée par HSM et que vous voulez migrer vers Azure Rights Management avec une clé de locataire protégée avec HSM dans Azure Key Vault. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) et choisissez une configuration différente.

> [!NOTE]
> Ces instructions supposent que votre clé AD RMS est protégée par module. Il s’agit du cas le plus classique. 

Cette procédure en deux parties permet d'importer votre clé HSM et la configuration d'AD RMS dans Azure RMS pour que votre clé de client Azure RMS soit gérée par vous (scénario BYOK).

Comme votre clé de locataire Azure RMS est stockée et gérée par Azure Key Vault, cette partie de la migration nécessite une administration dans Azure Key Vault, en plus d’Azure RMS. Si Azure Key Vault est géré par un autre administrateur que celui de votre organisation, vous devez coordonner et travailler avec cet administrateur pour effectuer ces procédures.

Avant de commencer, vérifiez que votre organisation dispose d’un coffre de clés qui a été créé dans Azure Key Vault et qu’il prend en charge les clés protégées par HSM. Bien que ce ne soit pas obligatoire, nous vous recommandons d’avoir un coffre de clés dédié pour Azure RMS. Ce coffre de clés doit être configuré de façon à autoriser Azure RMS à y accéder : les clés stockées dans ce coffre de clés doivent donc être limitées uniquement aux clés Azure RMS.


> [!TIP]
> Si vous voulez effectuer les étapes de configuration pour Azure Key Vault et que vous n’êtes pas familiarisé avec ce service Azure, il peut être utile de consulter d’abord [Prise en main d’Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## Partie 1 : Transfert de votre clé HSM vers Azure Key Vault

Ces procédures sont effectuées par l’administrateur d’Azure Key Vault.

1.  Suivez les instructions de la documentation d’Azure Key Vault en utilisant [Implémentation de BYOK pour Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) avec l’exception suivante :

    - N’effectuez pas les étapes pour **Générer votre clé de locataire** car vous avez déjà l’équivalent dans votre déploiement AD RMS. Identifiez plutôt la clé utilisée par votre serveur AD RMS dans l’installation Thales et utilisez cette clé lors de la migration. Les fichiers de clés chiffrées Thales sont généralement nommés **key<*nom_application_clé*><*identificateur_clé*>** localement sur le serveur.

    Quand la clé se charge sur Azure Key Vault, vous voyez s’afficher les propriétés de la clé, notamment l’ID de clé. Elle est similaire à ceci : https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Prenez note de cette URL car l’administrateur Azure RMS en a besoin pour indiquer à Azure RMS d’utiliser cette clé pour sa clé de locataire.

2. Sur la station de travail connectée à Internet, dans une session PowerShell, utilisez l’applet de commande [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx ) pour autoriser le principal du service Azure RMS (Microsoft.Azure.RMS) à accéder au coffre de clés qui stocke la clé de locataire Azure RMS. Les autorisations nécessaires sont déchiffrer, chiffrer, désencapsuler la clé (unwrapkey), encapsuler la clé (wrapkey), vérifier et signer.
    
    Par exemple, si le coffre de clés que vous avez créé pour Azure RMS est nommé contoso-byok-ky et que votre groupe de ressources est nommé contoso-byok-rg, exécutez la commande suivante :
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign


Maintenant que vous avez préparé votre clé HSM dans Azure Key Vault pour Azure RMS, vous êtes prêt à importer vos données de configuration AD RMS.

## Partie 2 : Importation des données de configuration dans Azure RMS

Ces procédures sont effectuées par l’administrateur d’Azure RMS.

1.  Sur la station de travail connectée à Internet et dans la session PowerShell, connectez-vous à Azure RMS en utilisant l’applet de commande [Connnect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx ).
    
    Ensuite, chargez le premier fichier exporté de domaine de publication approuvé (.xml) en utilisant l’applet de commande [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté correspondant à la clé HSM que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. 
    
    Pour exécuter cette applet de commande, vous avez besoin de l’URL de la clé qui a été identifiée à l’étape précédente.
    
    Par exemple, en utilisant notre valeur d’URL de clé de l’étape précédente et un fichier de domaine de publication approuvé C:\contoso-tpd1.xml, vous exécutez :
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

2.  Une fois la commande exécutée, répétez l'étape 1 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import.  

3.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Si vous avez besoin ultérieurement de vérifier quelle clé de locataire est utilisée par Azure RMS dans Azure Key Vault, utilisez l’applet de commande [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) d’Azure RMS.

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).




<!--HONumber=Aug16_HO4-->


