---
# required metadata

title: Étape 2 &colon; Migration de clé protégée par logiciel à clé protégée par HSM | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Étape 2 : Migration de clé protégée par logiciel à clé protégée par HSM

*S’applique à : Active Directory Rights Management Services, Azure Rights Management*


Ces instructions font partie du [chemin de migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md), et s’appliquent uniquement si votre clé AD RMS est protégée par logiciel et que vous souhaitez procéder à la migration vers Azure Rights Management avec une clé de locataire protégée par HSM. 

Si ce n’est pas votre scénario de configuration choisi, revenez à l’[Étape 2. Exporter les données de configuration d’AD RMS, puis les importer dans Azure RMS](migrate-from-ad-rms-to-azure-rms.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms) et choisissez une configuration différente.

Cette procédure en trois parties permet d'importer la configuration d'AD RMS dans Azure RMS pour que votre clé de client Azure RMS soit gérée par vous (scénario BYOK).

Vous devez extraire votre clé de certificat de licence serveur (SLC) des données de configuration, transférer la clé vers un HSM Thales local, empaqueter et transférer votre clé HSM vers Azure RMS, puis importer les données de configuration.

## Première partie : Extraction de votre SLC à partir des données de configuration et importation de la clé dans votre HSM local

1.  Utilisez les étapes suivantes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md) :

    -   **Générer et transférer votre clé de client par Internet** : **préparation de la station de travail connectée à Internet**

    -   **Générer et transférer votre clé de client par Internet**: **préparation du poste de travail déconnecté**

    Ne suivez pas ces étapes pour générer votre clé de client, car vous avez déjà l'équivalent dans le fichier (.xml) de données de configuration exporté. Au lieu de cela, vous allez exécuter une commande pour extraire cette clé du fichier et l'importer dans votre HSM local.

2.  Sur la station de travail déconnectée, exécutez la commande suivante :

    ```
    KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath <TPD> -ProtectionPassword -KeyIdentifier <KeyID> -ExchangeKeyPackage <BYOK-KEK-pka-Region> -NewSecurityWorldPackage <BYOK-SecurityWorld-pkg-Region>
    ```
    Par exemple, pour l’Amérique du Nord : **KeyTransferRemote.exe -ImportRmsCentrallyManagedKey -TpdFilePath E:\contosokey1.xml -ProtectionPassword -KeyIdentifier contosorms1key –- -ExchangeKeyPackage &lt;BYOK-KEK-pka-NA-1&gt; -NewSecurityWorldPackage &lt;BYOK-SecurityWorld-pkg-NA-1&gt;**

    Informations supplémentaires :

    -   le paramètre ImportRmsCentrallyManagedKey indique que l'opération consiste à importer la clé SLC.

    -   Si vous n'avez pas spécifié le mot de passe dans la commande, vous êtes invité à l'entrer.

    -   Le paramètre KeyIdentifier est un nom convivial de clé, qui crée le nom de fichier de clé. Vous devez utiliser uniquement des caractères ASCII minuscules.

    -   Le paramètre ExchangeKeyPackage spécifie un package de clé d'échange de clés (KEK) spécifique d'une région, dont le nom commence par BYOK-KEK-pkg-.

    -   Le paramètre NewSecurityWorldPackage spécifie un package de monde de sécurité spécifique d'une région, dont le nom commence par BYOK-SecurityWorld-pkg-.

    Cette commande renvoie les éléments suivants :

    -   Un fichier de clé HSM : %NFAST_KMDATA%\local\key_mscapi_&lt;KeyID&gt;

    -   Fichier de données de configuration RMS avec le certificat de licence serveur supprimé : %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml

3.  Si vous avez plusieurs fichiers de données de configuration RMS, répétez l'étape 2 pour les autres fichiers.

Maintenant que votre SLC a été extrait et converti en clé basée sur HSM, vous êtes prêt à empaqueter et à transférer celle-ci vers Azure RMS.

## Partie 2 : empaquetage et transfert de votre clé HSM vers Azure RMS

1.  Utilisez les étapes suivantes de la section [Implémentation de la solution Bring Your Own Key (BYOK)](plan-implement-tenant-key.md#BKMK_ImplementBYOK) de la rubrique [Planification et implémentation de votre clé de client Azure Rights Management](plan-implement-tenant-key.md) :

    -   **Générer et transférer votre clé de client par Internet**: **préparation de la clé de client pour le transfert**

    -   **Générer et transférer votre clé de client par Internet**: **transfert de votre clé de client vers Azure RMS**

Maintenant que vous avez transféré votre clé HSM vers Azure RMS, vous êtes prêt à importer vos données de configuration AD RMS, qui contiennent uniquement un pointeur vers la clé de client qui vient d'être transférée.

## Partie 3 : importation des données de configuration dans Azure RMS

1.  Toujours sur la station de travail connectée à Internet et dans la session Windows PowerShell, recopiez les fichiers de configuration RMS avec le SLC supprimé (à partir de la station de travail déconnectée, %NFAST_KMDATA%\local\no_key_tpd_&lt;KeyID&gt;.xml)

2.  Téléchargez le premier fichier. Si vous avez plusieurs fichiers .xml parce que vous aviez plusieurs domaines de publication approuvés, sélectionnez le fichier contenant le domaine de publication approuvé exporté correspondant à la clé HSM que vous souhaitez utiliser dans Azure RMS pour protéger le contenu après la migration. Utilisez la commande suivante :

    ```
    Import-AadrmTpd -TpdFile <PathToNoKeyTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToKeyTransferPackage> -Active $true -Verbose
    ```
    Par exemple : **Import -TpdFile E:\no_key_tpd_contosorms1key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $true -Verbose**

    Lorsque vous y êtes invité, entrez le mot de passe que vous avez spécifié précédemment, puis confirmez cette action.

3.  Une fois la commande exécutée, répétez l'étape 2 pour chaque fichier .xml que vous avez créé en exportant vos domaines de publication approuvés. Toutefois, pour ces fichiers, définissez **-Active** avec la valeur **false** quand vous exécutez la commande Import. Par exemple : **Import -TpdFile E:\no_key_tpd_contosorms2key.xml -ProtectionPassword -HsmKeyFile E:\KeyTransferPackage-contosorms1key.byok -Active $false -Verbose**

4.  Utilisez l’applet de commande [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) pour vous déconnecter du service Azure RMS :

    ```
    Disconnect-AadrmService
    ```

Vous êtes maintenant prêt à passer à l’[Étape 3. Activer votre client RMS](migrate-from-ad-rms-to-azure-rms.md#BKMK_Step3Migration).




<!--HONumber=Apr16_HO4-->


