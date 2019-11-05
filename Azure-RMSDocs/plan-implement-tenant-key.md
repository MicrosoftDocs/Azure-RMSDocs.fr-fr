---
title: Votre clé de locataire Azure Information Protection
description: Au lieu que Microsoft gère la clé racine pour Azure Information Protection, vous souhaiterez peut-être créer et gérer cette clé (appelée « apporter votre propre clé » ou BYOK) pour votre locataire, pour se conformer à des réglementations spécifiques.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/11/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 585b99fa7d6960c0a340b0f63f4d696d2bd4d9ce
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559159"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Planification et implémentation de la clé de locataire Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Utilisez les informations de cet article pour planifier et gérer votre clé de locataire Azure Information Protection. Par exemple, il se peut qu'au lieu de laisser Microsoft gérer votre clé de locataire (par défaut), vous deviez vous en occuper vous-même afin de respecter les politiques de votre organisation. La gestion de votre propre clé de locataire est également appelée BYOK (Bring Your Own Key).

Qu’est-ce la clé de locataire Azure Information Protection ?

- La clé de locataire Azure Information Protection est une clé racine pour votre organisation. D’autres clés peuvent être dérivées de cette clé racine, comme les clés d’utilisateur, les clés d’ordinateur et les clés de chiffrement des documents. Quand Azure Information Protection utilise ces clés pour votre organisation, elles sont chaînées de façon chiffrée à votre clé de locataire Azure Information Protection.

- La clé de locataire Azure Information Protection est l’équivalent en ligne de la clé de certificat de licence serveur d’Active Directory Rights Management Services (AD RMS). 

**Aperçu rapide :** Utilisez le tableau suivant comme guide rapide pour votre topologie de clé de locataire recommandée. Ensuite, utilisez la documentation supplémentaire pour obtenir plus d’informations.

|Exigence professionnelle|Topologie de clé de locataire recommandée :|
|------------------------|-----------------------------------|
|Déployez Azure Information Protection rapidement et sans matériel spécial, sans logiciel supplémentaire et sans abonnement Azure.<br /><br />Par exemple : des environnements de test et quand votre organisation n’a pas de spécifications réglementaires pour la gestion des clés.|Gestion par Microsoft|
|Réglementations en matière de conformité et contrôle de toutes les opérations de cycle de vie. <br /><br />Par exemple : votre clé doit être protégée par un module de sécurité matériel (HSM).|BYOK|


Si nécessaire, vous pouvez modifier la topologie de votre clé de locataire après le déploiement, à l’aide de l’applet de commande [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) .


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Choix de la topologie de clé de locataire : gestion Microsoft (par défaut) ou gestion BYOK

Choisissez la topologie de clé de locataire la plus adaptée à votre organisation :

- **Gérée par Microsoft** : Microsoft génère automatiquement une clé de locataire pour votre organisation, et cette clé est utilisée exclusivement pour Azure Information Protection. Par défaut, Microsoft utilise cette clé pour votre locataire et gère la plupart des aspects du cycle de vie de votre clé de locataire. 
    
    Il s'agit de l'option la plus simple, avec la charge administrative la plus faible. Dans la plupart des cas, les utilisateurs n'ont même pas conscience de l'existence de cette clé de locataire. Il leur suffit de s’inscrire à Azure Information Protection ; le reste du processus de gestion de la clé est traité par Microsoft.

- **Gérée par vous (BYOK)** : pour un contrôle total sur votre clé de locataire, utilisez [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) avec Azure Information Protection. Pour cette topologie de clé de locataire, vous créez la clé, directement dans Key Vault ou localement. Si vous la créez localement, vous transférez ou vous importez ensuite cette clé dans Key Vault. Vous configurez ensuite Azure Information Protection pour utiliser cette clé, et vous la gérez dans Azure Key Vault.
    

### <a name="more-information-about-byok"></a>Plus d’informations sur BYOK
Pour créer votre propre clé, vous disposez des options suivantes :

- **Une clé que vous créez localement, et que vous transférez ou que vous importez dans Key Vault** :
    
    - Une clé protégée par module HSM que vous créez localement et que vous transférez dans Key Vault comme clé protégée par module HSM.
    
    - Une clé protégée par logiciel que vous créez localement, que vous convertissez et que vous transférez dans Key Vault comme clé protégée par module HSM. Cette option est prise en charge seulement quand vous [migrez depuis Active Directory Rights Management Services (AD RMS)](migrate-from-ad-rms-to-azure-rms.md).
    
    - Une clé protégée par logiciel que vous créez localement et que vous importez dans Key Vault comme clé protégée par logiciel. Cette option nécessite un fichier de certificat .PFX.
    
- **Une clé que vous créez dans Key Vault** :
    
    - Une clé protégée par module HSM que vous créez dans Key Vault.
    
    - Une clé protégée par logiciel que vous créez dans Key Vault.

Parmi ces options BYOK, la plus courante est une clé protégée par module HSM que vous créez localement et que vous transférez dans Key Vault comme clé protégée par module HSM. Bien que cette option nécessite le plus gros travail d’administration, elle peut être nécessaire pour permettre à votre organisation de se conformer à des réglementations spécifiques. Les modules de sécurité matériels qui sont utilisés par Azure Key Vault sont validés pour FIPS 140-2 Niveau 2.

Cette option implique les étapes suivantes :

1. Générez votre clé de locataire en local, en accord avec vos stratégies informatiques et de sécurité. Cette clé est la copie maître. Elle reste sur le site local et vous êtes responsable de sa sauvegarde.

2. Vous créez une copie de cette clé et vous transférez de façon sécurisée cette copie de votre module HSM vers Azure Key Vault. Notez que tout au long de ce processus, la copie maître de cette clé ne quitte jamais les limites de la protection matérielle.

3. La copie de la clé est protégée par Azure Key Vault.

> [!NOTE]
> 
> Par mesure de protection, Azure Key Vault utilise des domaines de sécurité distincts pour ses centres de données dans des régions comme l’Amérique du Nord, l’EMEA (Europe, Moyen-Orient et Afrique) et l’Asie. Azure Key Vault utilise aussi différentes instances d’Azure, comme Microsoft Azure Allemagne et Azure Government. 

Bien que cette action soit facultative, vous pouvez également utiliser les journaux d’utilisation quasiment en temps réel à partir d’Azure Information Protection pour voir exactement quand et comment votre clé de locataire est utilisée.

Lorsque vous utilisez BYOK pour votre clé de locataire Azure Information Protection, vous ne pouvez pas exporter votre trusted publishing domain (TPD). Le TPD est nécessaire si vous décidez de ne plus utiliser Azure Information Protection mais que vous devez toujours être en mesure de déchiffrer le contenu qui a été protégé par Azure Information Protection. Pour préparer ce scénario en créant un TPD approprié à l’avance, reportez-vous aux instructions suivantes : [préparation d’un plan de sortie du Cloud Azure information protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631).

### <a name="when-you-have-decided-your-tenant-key-topology"></a>Quand vous avez décidé de votre topologie de clé de locataire

Si vous décidez de laisser Microsoft gérer votre clé de locataire : 

- Sauf si vous migrez depuis AD RMS, aucune autre action n’est nécessaire de votre part pour générer la clé pour votre locataire. Vous pouvez passer directement à [Étapes suivantes](plan-implement-tenant-key.md#next-steps).

- Si vous avez AD RMS et que vous voulez migrer AD RMS vers Azure Information Protection, utilisez les instructions de migration : [Migration d’AD RMS vers Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md). 

Si vous décidez de gérer vous-même votre clé de locataire, lisez les sections suivantes pour plus d'informations.

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Implémentation de BYOK pour votre clé de locataire Azure Information Protection

Utilisez les informations et les procédures de cette section si vous souhaitez générer et gérer vous-même votre clé de locataire (solution BYOK) :

> [!NOTE]
> Si vous avez commencé à utiliser Azure Information Protection avec une clé de locataire gérée par Microsoft et que vous souhaitez à présent la gérer vous-même (c’est-à-dire passer à un scénario BYOK), les documents et e-mails précédemment protégés restent accessibles à l’aide d’une clé archivée. 

### <a name="prerequisites-for-byok"></a>Conditions requises pour la solution BYOK
Reportez-vous au tableau suivant pour connaître les conditions requises pour la solution Bring your own key (BYOK).

|Condition requise|Autres informations|
|---------------|--------------------|
|Votre locataire Azure Information Protection doit avoir un abonnement Azure. Si vous n’en avez pas, vous pouvez vous inscrire pour un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/). <br /><br /> Pour utiliser une clé protégée par module HSM, vous devez avoir le niveau de service Azure Key Vault Premium.|L’abonnement Azure gratuit qui fournit l’accès pour configurer Azure Active Directory et la configuration de modèles personnalisés Azure Rights Management (**Accès à Azure Active Directory**) n’est pas suffisant pour utiliser Azure Key Vault. Pour confirmer que vous disposez d’un abonnement Azure que vous pouvez utiliser pour BYOK, utilisez les applets de commande [Azure PowerShell](/powershell/azure/overview) : <br /><br /> 1. Démarrez une session Azure PowerShell avec l’option **exécuter en tant qu’administrateur** , puis connectez-vous en tant qu’administrateur général pour votre locataire Azure information protection en utilisant `Connect-AzAccount` puis copiez et collez la chaîne de jeton résultante dans `https://microsoft.com/devicelogin`à l’aide d’un navigateur. <br /><br /> Pour plus d’informations, consultez [se connecter avec Azure PowerShell](/powershell/azure/authenticate-azureps). <br /><br />2. tapez ce qui suit et vérifiez que les valeurs affichées pour le nom et l’ID de votre abonnement s’affichent, votre ID de locataire Azure Information Protection et que l’État est activé : `Get-AzSubscription`<br /><br />Si aucune valeur n’est affichée et que vous revenez simplement à l’invite, vous n’avez pas d’abonnement Azure utilisable pour la solution BYOK. <br /><br />**Remarque**: en plus des prérequis BYOK, si vous effectuez une migration à partir de AD RMS vers Azure information protection à l’aide de la clé logicielle pour la clé matérielle, vous devez disposer d’une version minimale de 11,62 si vous utilisez le microprogramme de Thales pour votre HSM.|
|Pour utiliser une clé protégée par module HSM que vous créez localement : <br /><br />- Tous les prérequis répertoriés pour BYOK dans Key Vault. |Consultez [Prérequis pour la solution BYOK](/azure/key-vault/key-vault-hsm-protected-keys#prerequisites-for-byok) dans la documentation d’Azure Key Vault. <br /><br /> **Remarque**: en plus des prérequis BYOK, si vous effectuez une migration à partir de AD RMS vers Azure information protection à l’aide de la clé logicielle pour la clé matérielle, vous devez disposer d’une version minimale de 11,62 si vous utilisez le microprogramme de Thales pour votre HSM.|
|Si le coffre de clés qui doit contenir votre clé de locataire utilise des points de terminaison de service de réseau virtuel pour Azure Key Vault : <br /><br />- Autorisez les services Microsoft approuvés pour contourner ce pare-feu.|Pour plus d’informations, consultez [Points de terminaison du service de réseau virtuel pour Azure Key Vault](/azure/key-vault/key-vault-overview-vnet-service-endpoints).|
|Module PowerShell AIPService pour Azure Information Protection.|Pour obtenir des instructions d’installation, consultez [installation du module PowerShell AIPService](./install-powershell.md).|

Pour plus d’informations sur le module de sécurité matériel (HSM) nCipher nShield et sur son utilisation avec Azure Key Vault, consultez le [site Web nCipher](https://www.ncipher.com/products/key-management/cloud-microsoft-azure/how-to-buy).

### <a name="choosing-your-key-vault-location"></a>Choix de l’emplacement de votre coffre de clés

Quand vous créez un coffre de clés pour contenir la clé à utiliser comme votre clé de locataire pour Azure Information Protection, vous devez spécifier un emplacement. Cet emplacement est une région Azure ou une instance Azure.

Faites votre choix en tenant d’abord compte de la conformité, et ensuite pour minimiser la latence réseau :

- Si vous avez choisi la topologie de clé BYOK pour des raisons de conformité, les spécifications de conformité peuvent imposer la région Azure ou l’instance Azure qui stocke votre clé de locataire Azure Information Protection.

- Étant donné que tous les appels de chiffrement pour la protection sont chaînés à votre clé de locataire Azure Information Protection, vous souhaitez minimiser la latence réseau subie par ces appels. Pour cela, créez votre coffre de clés dans la même région ou la même instance Azure que votre locataire Azure Information Protection.

Pour identifier l’emplacement de votre locataire Azure Information Protection, utilisez l’applet de commande PowerShell [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) et identifiez la région à partir des URL. Exemple :

    LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

La région est identifiable dans **rms.na.aadrm.com** et pour cet exemple, elle est North America (Amérique du Nord).

Utilisez le tableau suivant pour identifier la région ou l’instance Azure recommandée pour minimiser la latence réseau.

|Région ou instance Azure|Emplacement recommandé pour votre coffre de clés|
|---------------|--------------------|
|rms.**na**.aadrm.com|**USA Centre Nord** ou **USA Est**|
|rms.**eu**.aadrm.com|**Europe Nord** ou **Europe Ouest**|
|rms.**ap**.aadrm.com|**Asie Est** ou **Asie Sud-Est**|
|rms.**sa**.aadrm.com|**USA Ouest** ou **USA Est**|
|rms.**govus**.aadrm.com|**USA Centre** ou **USA Est 2**|
|RMS.**aadrm.us**|**US gov Virginie** ou **US gov Arizona**|
|RMS.**aadrm.CN**|**Chine est 2** ou **Chine Nord 2**|


### <a name="instructions-for-byok"></a>Instructions pour BYOK

Utilisez la documentation d’Azure Key Vault pour créer un coffre de clés et la clé que vous voulez utiliser pour Azure Information Protection. Par exemple, consultez [Bien démarrer avec Azure Key Vault](/azure/key-vault/key-vault-get-started).

Vérifiez que la longueur de clé est de 2 048 bits (recommandé) ou de 1 024 bits. Les autres longueurs de clé ne sont pas prises en charge par Azure Information Protection. 

N’utilisez pas une clé de 1024 bits comme clé de locataire active, car elle est considérée comme offrant un niveau de protection inadéquat. Microsoft n’approuve pas l’utilisation de longueurs de clé inférieures telles que les clés RSA 1024 bits et l’utilisation associée de protocoles qui offrent des niveaux de protection inadéquats, tels que SHA-1. Nous vous recommandons de passer à une longueur de clé supérieure.

Pour créer une clé locale protégée par module HSM et la transférer à votre coffre de clés comme clé protégée par module HSM, suivez les procédures décrites dans [Génération et transfert de clés protégées par HSM pour Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys).

Pour qu’Azure Information Protection utilise la clé, toutes les opérations Key Vault doivent être autorisées pour cette clé. Il s’agit de la configuration par défaut et les opérations sont chiffrer, déchiffrer, wrapKey, unwrapKey, signer et vérifier. Vous pouvez vérifier les opérations autorisées d’une clé à l’aide de la commande PowerShell suivante : `(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps`. Si nécessaire, ajoutez des opérations autorisées à l’aide de [Update-AzKeyVaultKey](/powershell/module/az.keyvault/update-azkeyvaultkey) et du paramètre *KeyOps* .

Une clé qui est stockée dans Key Vault a un ID de clé. Cet ID de clé est une URL contenant le nom du coffre de clés, le conteneur de clés, le nom de la clé et la version de la clé. Par exemple : **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333** . Vous devez configurer Azure Information Protection pour l’utilisation de cette clé en spécifiant son URL Key Vault.

Avant qu’Azure Information Protection puisse utiliser la clé, le service Azure Rights Management doit être autorisé à utiliser la clé dans le coffre de clés de votre organisation. Pour ce faire, l’administrateur Azure Key Vault peut utiliser le portail Azure ou Azure PowerShell :

Configuration à l’aide du portail Azure :

1. Accédez à **Coffres de clés** >  **\<*nom de votre coffre de clés Key Vault*>**  > **Stratégies d’accès** > **Ajouter nouveau**.

2. Dans le volet **Ajouter une stratégie d’accès** , sélectionnez **Azure information protection BYOK** dans la zone de liste **configurer à partir d’un modèle (facultatif)** , puis cliquez sur **OK**.
    
    Le modèle sélectionné a la configuration suivante :
    
    - Les **services Microsoft Rights Management** sont automatiquement attribués pour **Sélectionner le principal**.
    - Les autorisations **Get**, **Decrypt** et **Sign** sont automatiquement sélectionnées pour les clés. 

Configuration à l’aide de PowerShell :

- Exécutez l’applet de commande PowerShell Key Vault, [Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)et accordez des autorisations au principal du service Azure Rights Management à l’aide du GUID **00000012-0000-0000-C000-000000000000**. Exemple :
    
        Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

Vous êtes maintenant prêt à configurer Azure Information Protection pour utiliser cette clé comme clé de locataire Azure Information Protection de votre organisation. En utilisant des applets de commande Azure RMS, établissez d’abord une connexion au service Azure Rights Management, puis connectez-vous :

    Connect-AipService

Exécutez ensuite l' [applet de commande use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey), en spécifiant l’URL de la clé. Exemple :

    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> Dans cet exemple, « aaaabbbbcccc111122223333 » est la version de la clé à utiliser. Si vous ne spécifiez pas la version, la version actuelle de la clé est utilisée sans avertissement, et la commande semble fonctionner. Toutefois, si votre clé dans Key Vault est mise à jour (renouvelée) par la suite, le service Azure Rights Management cessera de fonctionner pour votre locataire, même si vous exécutez à nouveau la commande use-AipServiceKeyVaultKey.
> 
> Veillez à spécifier la version de clé en plus du nom de clé quand vous exécutez cette commande. Vous pouvez utiliser l’Azure Key Vault cmd, [AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey)pour connaître le numéro de version de la clé actuelle. Par exemple : `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

Si vous devez vérifier que l’URL de la clé est définie correctement pour Azure Information Protection : dans Azure Key Vault, exécutez la [AzKeyVaultKey](/powershell/module/az.keyvault/get-azkeyvaultkey) pour voir l’URL de la clé.

Enfin, si le service Azure Rights Management est déjà activé, exécutez [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) pour indiquer à Azure information protection d’utiliser cette clé comme clé de locataire active pour le service de Rights Management Azure. Si vous n’exécutez pas cette étape, Azure Information Protection continuera d’utiliser la clé managée par Microsoft par défaut créée automatiquement pour votre locataire.


## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez planifié et, le cas échéant, créé et configuré votre clé de locataire, procédez comme suit :

1.  Commencez à utiliser votre clé de locataire :
    
    - Si le service de protection n’est pas encore activé, vous devez maintenant activer le service Rights Management pour que votre organisation puisse commencer à utiliser Azure Information Protection. Les utilisateurs peuvent commencer immédiatement à utiliser votre clé de locataire (gérée par Microsoft ou par vous dans Azure Key Vault).
    
        Pour plus d’informations sur l’activation, consultez [activation du service de protection à partir de Azure information protection](./activate-service.md).
        
    - Si vous avez déjà activé le service Rights Management et que vous avez décidé de gérer votre propre clé de locataire, les utilisateurs passent graduellement de l’ancienne clé de locataire à la nouvelle. Cette transition progressive s’effectue en quelques semaines. Les documents et fichiers protégés par l'ancienne clé de locataire restent accessibles pour les utilisateurs autorisés.
        
2. Envisagez l’activation de la journalisation de l’utilisation, qui consigne chaque transaction effectuée par le service Azure Rights Management.
    
    Si vous avez décidé de gérer vous-même votre clé de locataire, la journalisation inclut des informations utiles sur son utilisation. Consultez l’extrait de code suivant, tiré d’un fichier journal affiché dans Excel, où les types de requête **KeyVaultDecryptRequest** et **KeyVaultSignRequest** montrent que la clé de locataire est utilisée.
    
    ![fichier journal dans Excel où la clé de locataire est utilisée](./media/RMS_Logging.png)
    
    Pour plus d’informations sur la journalisation de l’utilisation, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](./log-analyze-usage.md).
    
3.  Gérez votre clé de locataire.
    
    Pour plus d’informations sur les opérations du cycle de vie de votre clé de locataire, consultez [Opérations pour votre clé de locataire Azure Information Protection](./operations-tenant-key.md).
