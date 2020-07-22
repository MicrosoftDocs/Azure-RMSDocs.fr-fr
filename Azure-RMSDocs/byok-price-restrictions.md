---
title: Détails de Bring Your Own Key (BYOK)-Azure Information Protection
description: Comprenez les détails et les restrictions lorsque vous utilisez des clés gérées par le client (appelées « apportez votre propre clé » ou BYOK) avec Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3e6b5be8751e01c47b066963ef5ce3588b43cb86
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86868958"
---
# <a name="bring-your-own-key-byok-details-for-azure-information-protection"></a>BYOK les détails de votre propre clé pour Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Les organisations disposant d’un abonnement Azure Information Protection peuvent choisir de configurer leur locataire avec leur propre clé au lieu d’une clé par défaut générée par Microsoft. Cette configuration est souvent appelée Bring Your Own Key (BYOK).

BYOK et la [journalisation de l’utilisation](log-analyze-usage.md) fonctionnent de façon transparente avec les applications qui s’intègrent au service Azure Rights Management utilisé par Azure information protection.

Les applications prises en charge sont les suivantes :

- **Services Cloud,** tels que Microsoft SharePoint ou Office 365

- **Services locaux exécutant des** applications Exchange et SharePoint qui utilisent le service Azure Rights Management via le connecteur RMS

- **Applications clientes,** telles qu’Office 2019, Office 2016 et Office 2013

> [!TIP]
> Si nécessaire, appliquez une sécurité supplémentaire à des documents spécifiques à l’aide d’une clé locale supplémentaire. Pour plus d’informations, consultez la page protection [hyok (blocage de votre propre clé](configure-adrms-restrictions.md) ) ou protection à [double clé (DKE)](plan-implement-tenant-key.md#double-key-encryption-dke-aip-unified-labeling-client-only).
> 

## <a name="azure-key-vault-key-storage"></a>Stockage de clé de Azure Key Vault

Les clés générées par le client doivent être stockées dans le Azure Key Vault pour la protection BYOK.

> [!NOTE]
> L’utilisation de clés protégées par HSM dans le Azure Key Vault nécessite un [niveau de service Azure Key Vault Premium](https://azure.microsoft.com/pricing/details/key-vault/), ce qui entraîne des frais d’abonnement mensuels supplémentaires.

### <a name="sharing-key-vaults-and-subscriptions"></a>Partage de coffres de clés et d’abonnements

Nous vous recommandons d’utiliser un **coffre de clés dédié** pour votre clé de locataire. Les coffres de clés dédiés permettent de s’assurer que les appels effectués par d’autres services n’entraînent pas le dépassement des [limites du service](https://docs.microsoft.com/azure/key-vault/general/service-limits) . Le dépassement des limites de service sur le coffre de clés dans lequel votre clé de locataire est stockée peut entraîner une limitation du temps de réponse pour Azure Rights Management Service.

Étant donné que les différents services ont des exigences de gestion clés différentes, Microsoft recommande également d’utiliser **un abonnement Azure dédié** à votre coffre de clés. Abonnements Azure dédiés :

- Contribuer à la protection contre les inconfigurations

- Sont plus sécurisées quand différents services ont des administrateurs différents

Pour partager un abonnement Azure avec d’autres services qui utilisent Azure Key Vault, assurez-vous que l’abonnement partage un ensemble commun d’administrateurs. En confirmant que tous les administrateurs qui utilisent l’abonnement ont une compréhension solide de chaque clé à laquelle ils peuvent accéder, cela signifie qu’ils sont moins susceptibles de mal configurer vos clés.

**Exemple :** Utilisation d’un abonnement Azure partagé lorsque les administrateurs de votre Azure Information Protection clé de locataire sont les mêmes que ceux qui gèrent vos clés pour la clé de client Office 365 et CRM Online. Si les administrateurs clés de ces services sont différents, nous vous recommandons d’utiliser des abonnements dédiés.

### <a name="benefits-of-using-azure-key-vault"></a>Avantages de l’utilisation d’Azure Key Vault

Azure Key Vault fournit une solution de gestion de clés centralisée et cohérente pour de nombreux services Cloud et locaux qui utilisent le chiffrement.

Outre la gestion des clés, Azure Key Vault offre à vos administrateurs de sécurité la même expérience de gestion pour stocker, utiliser et gérer les certificats et les secrets (comme les mots de passe) pour d’autres services et applications qui utilisent le chiffrement.

Le stockage de votre clé de locataire dans le Azure Key Vault offre les avantages suivants :

|Avantage  |Description  |
|---------|---------|
|**Interfaces intégrées**| Azure Key Vault prend en charge plusieurs interfaces intégrées pour la gestion de clés, notamment PowerShell, CLI, les API REST et le portail Azure. </br></br>D’autres services et outils ont été intégrés à Key Vault pour des fonctionnalités optimisées pour des tâches spécifiques, telles que la surveillance. </br></br>Par exemple, analysez vos journaux d’utilisation de clé avec Operations Management Suite log Analytics, définissez des alertes lorsque les critères spécifiés sont remplis, et ainsi de suite.        |
|**Séparation des rôles**| Azure Key Vault fournit une séparation des rôles comme meilleure pratique de sécurité reconnue. </br></br>La séparation des rôles permet de s’assurer que Azure Information Protection administrateurs peuvent se concentrer sur leurs priorités les plus élevées, y compris la gestion de la classification et de la protection des données, ainsi que des clés de chiffrement et des stratégies pour des exigences de sécurité ou de conformité |
|**Emplacement de la clé principale**| Azure Key Vault est disponible dans divers emplacements et prend en charge les organisations avec des restrictions qui peuvent résider dans les clés principales. </br></br>Pour plus d’informations, consultez la page [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) sur le site Azure.|
|**Domaines de sécurité séparés**|Azure Key Vault utilise des domaines de sécurité distincts pour ses centres de données dans des régions comme Amérique du Nord, la zone EMEA (Europe, Moyen-Orient et Afrique) et l’Asie. </br></br>Azure Key Vault utilise aussi différentes instances d’Azure, comme Microsoft Azure Allemagne et Azure Government. |
|**Expérience unifiée**| Azure Key Vault permet également aux administrateurs de sécurité de stocker, d’accéder et de gérer les certificats et les secrets, tels que les mots de passe, pour les autres services qui utilisent le chiffrement. <br></br>L’utilisation de Azure Key Vault pour vos clés de locataire offre une expérience utilisateur transparente pour les administrateurs qui gèrent tous ces éléments.|

Pour obtenir les dernières mises à jour et découvrir comment d’autres services utilisent [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/basic-concepts), visitez le blog de l' [équipe Azure Key Vault](https://blogs.technet.microsoft.com/kv/).

## <a name="usage-logging-for-byok"></a>Journalisation de l’utilisation pour BYOK

Les journaux d’utilisation sont générés par chaque application qui effectue des demandes au service Azure Rights Management.

Bien que la journalisation de l’utilisation soit facultative, nous vous recommandons d’utiliser les journaux d’utilisation quasiment en temps réel à partir de Azure Information Protection pour voir exactement comment et quand votre clé de locataire est utilisée.

Pour plus d’informations sur la journalisation de l’utilisation de la clé pour BYOK, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](log-analyze-usage.md).

> [!TIP]
> Pour des assurances supplémentaires, Azure Information Protection la journalisation de l’utilisation peut être référencée avec la [journalisation Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/logging). Les journaux de Key Vault fournissent une méthode fiable pour surveiller indépendamment que votre clé est utilisée uniquement par le service Azure Rights Management.
>
> Si nécessaire, révoquez immédiatement l’accès à votre clé en supprimant les autorisations sur le coffre de clés.

## <a name="options-for-creating-and-storing-your-key"></a>Options pour la création et le stockage de votre clé

BYOK prend en charge les clés créées dans Azure Key Vault ou localement.

Si vous créez votre clé localement, vous devez ensuite la transférer ou l’importer dans votre Key Vault et configurer Azure Information Protection pour utiliser la clé. Effectuez une gestion des clés supplémentaire à partir de Azure Key Vault.

Options pour créer et stocker votre propre clé :

- **Créé dans Azure Key Vault.** Créez et stockez votre clé dans Azure Key Vault en tant que clé protégée par HSM ou clé protégée par logiciel.

- **Créé localement.** Créez votre clé locale et transférez-la vers Azure Key Vault à l’aide de l’une des options suivantes :

    - **Clé protégée par HSM, transférée en tant que clé protégée par HSM.** Méthode la plus courante choisie.

        Bien que cette méthode présente la surcharge administrative la plus importante, votre organisation peut être amenée à suivre des réglementations spécifiques. Les modules HSM utilisés par Azure Key Vault sont validés par le niveau 2 de FIPS 140-2.

    - **Clé protégée par logiciel qui est convertie et transférée vers Azure Key Vault en tant que clé protégée par HSM.** Cette méthode est prise en charge uniquement lors [de la migration à partir de services AD RMS (Active Directory Rights Management Services) (AD RMS)](migrate-from-ad-rms-to-azure-rms.md).

    - **Créé en local en tant que clé protégée par logiciel et transféré vers Azure Key Vault en tant que clé protégée par logiciel.** Cette méthode requiert un. Fichier de certificat PFX.

Par exemple, procédez comme suit pour utiliser une clé créée localement :

1. Générez votre clé de locataire dans vos locaux, conformément aux stratégies informatiques et de sécurité de votre organisation. Cette clé est la copie maître. Il reste en local et vous êtes requis pour sa sauvegarde.

1. Créez une copie de la clé principale et transférez-la en toute sécurité de votre HSM vers Azure Key Vault. Tout au long de ce processus, la copie principale de la clé ne laisse jamais la limite de protection matérielle.

Une fois le transfert effectué, la copie de la clé est protégée par Azure Key Vault.

## <a name="exporting-your-trusted-publishing-domain"></a>Exportation de votre trusted publishing domain

Si vous décidez de ne plus utiliser Azure Information Protection, vous aurez besoin d’un trusted publishing domain (TPD) pour déchiffrer le contenu protégé par Azure Information Protection.

Toutefois, l’exportation de votre TPD n’est pas prise en charge si vous utilisez BYOK pour votre clé de Azure Information Protection.

Pour préparer ce scénario, veillez à créer un TPD approprié à l’avance. Pour plus d’informations, consultez [la section Préparation d’un plan de sortie du Cloud Azure information protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/How-to-prepare-an-Azure-Information-Protection-Cloud-Exit-plan/ba-p/382631).

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Implémentation de BYOK pour votre clé de locataire Azure Information Protection

Utilisez les étapes suivantes pour implémenter BYOK :

1. [Passer en revue les conditions préalables BYOK](#prerequisites-for-byok)
1. [Choisir un emplacement de Key Vault](#choosing-your-key-vault-location)
1. [Créer et configurer votre clé](#create-and-configure-your-key)

### <a name="prerequisites-for-byok"></a>Configuration requise pour BYOK

Les conditions préalables de BYOK varient en fonction de la configuration de votre système. Vérifiez que votre système est conforme aux conditions préalables suivantes, si nécessaire :

|Condition requise  |Description  |
|---------|---------|
|**Abonnement Azure**     |Obligatoire pour toutes les configurations. </br>Pour plus d’informations, consultez [vérifier que vous disposez d’un abonnement Azure compatible avec BYOK](#verifying-that-you-have-a-byok-compatible-azure-subscription).         |
|**Module PowerShell AIPService pour Azure Information Protection**|Obligatoire pour toutes les configurations. </br>Pour plus d’informations, consultez [installation du module PowerShell AIPService](./install-powershell.md).|
|**Conditions préalables Azure Key Vault pour BYOK** | Si vous utilisez une clé protégée par HSM qui a été créée en local, assurez-vous que vous êtes également conforme aux [prérequis pour les BYOK](https://docs.microsoft.com/azure/key-vault/keys/hsm-protected-keys-byok#prerequisites) répertoriés dans la documentation Azure Key Vault.         |
|**Microprogramme Thales version 11,62**    |Vous devez disposer de la version 11,62 du microprogramme de Thales si vous effectuez une migration à partir de AD RMS vers Azure Information Protection en utilisant une clé logicielle pour la clé matérielle et que vous utilisez le microprogramme Thales pour votre HSM.
|**Contournement du pare-feu pour les services Microsoft approuvés** |Si le coffre de clés qui contient votre clé de locataire utilise des points de terminaison de service de réseau virtuel pour Azure Key Vault, vous devez autoriser les services Microsoft approuvés à contourner ce pare-feu. </br>Pour plus d’informations, consultez [Points de terminaison du service de réseau virtuel pour Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/overview-vnet-service-endpoints).       |

<!--
>[!NOTE]
> For more information about nCipher nShield hardware security module (HSM) and how they are used with Azure Key Vault, see the [nCipher website](https://www.ncipher.com/products/key-management/cloud-microsoft-azure/how-to-buy).-->

#### <a name="verifying-that-you-have-a-byok-compatible-azure-subscription"></a>Vérification que vous disposez d’un abonnement Azure compatible avec BYOK

Votre locataire Azure Information Protection doit avoir un abonnement Azure. Si vous n’en avez pas encore, vous pouvez vous inscrire pour obtenir un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/). Toutefois, pour utiliser une clé protégée par HSM, vous devez disposer de la Azure Key Vault niveau de service Premium.

L’abonnement Azure gratuit qui fournit l’accès à la configuration de Azure Active Directory et à la configuration du modèle personnalisé Azure Rights Management n’est *pas* suffisant pour l’utilisation de Azure Key Vault.

Pour vérifier si vous disposez d’un abonnement Azure compatible avec BYOK, procédez comme suit pour vérifier, à l’aide des applets de commande [Azure PowerShell](https://docs.microsoft.com/powershell/azure/) :

1. Démarrez une session Azure PowerShell en tant qu’administrateur.

1. Connectez-vous en tant qu’administrateur général pour votre locataire Azure Information Protection à l’aide de `Connect-AzAccount` .

1. Copiez le jeton affiché dans le presse-papiers. Ensuite, dans un navigateur, accédez à https://microsoft.com/devicelogin et entrez le jeton copié.

    Pour plus d’informations, consultez [se connecter avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps).

1. Dans votre session PowerShell, entrez `Get-AzSubscription` et vérifiez que les valeurs suivantes s’affichent :

    - Le nom et l’ID de votre abonnement
    - Votre ID de locataire Azure Information Protection
    - Confirmation que l’État est activé

    Si aucune valeur n’est affichée et que vous revenez à l’invite, vous ne disposez pas d’un abonnement Azure qui peut être utilisé pour BYOK.

### <a name="choosing-your-key-vault-location"></a>Choix de l’emplacement de votre coffre de clés

Quand vous créez un coffre de clés pour contenir la clé à utiliser comme votre clé de locataire pour Azure Information Protection, vous devez spécifier un emplacement. Cet emplacement est une région Azure ou une instance Azure.

Faites votre choix en tenant d’abord compte de la conformité, et ensuite pour minimiser la latence réseau :

- Si vous avez choisi la méthode de clé BYOK pour des raisons de conformité, ces exigences de conformité peuvent également imposer la région ou l’instance Azure qui peut être utilisée pour stocker votre clé de locataire Azure Information Protection.

- Tous les appels de chiffrement de la chaîne de protection à votre clé de Azure Information Protection. Par conséquent, vous souhaiterez peut-être réduire la latence réseau requise par ces appels en créant votre coffre de clés dans la même région ou instance Azure que votre locataire Azure Information Protection.

Pour identifier l’emplacement de votre locataire Azure Information Protection, utilisez l’applet de commande PowerShell [AipServiceConfiguration](https://docs.microsoft.com/powershell/module/aipservice/get-aipserviceconfiguration) et identifiez la région à partir des URL. Par exemple :

```ps
LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing
```
    
La région est identifiable dans **rms.na.aadrm.com** et pour cet exemple, elle est North America (Amérique du Nord).

Le tableau suivant répertorie les régions et les instances Azure recommandées pour minimiser la latence du réseau :

|Région ou instance Azure|Emplacement recommandé pour votre coffre de clés|
|---------------|--------------------|
|rms.**na**.aadrm.com|**USA Centre Nord** ou **USA Est**|
|rms.**eu**.aadrm.com|**Europe du Nord** ou Europe de l' **Ouest**|
|rms.**ap**.aadrm.com|**Asie est** ou **Asie du Sud** -est|
|rms.**sa**.aadrm.com|**USA Ouest** ou **USA Est**|
|rms.**govus**.aadrm.com|**USA Centre** ou **USA Est 2**|
|RMS.**aadrm.us**|**US gov Virginie** ou **US gov Arizona**|
|RMS.**aadrm.CN**|**Chine est 2** ou **Chine Nord 2**|

### <a name="create-and-configure-your-key"></a>Créer et configurer votre clé

Créez un Azure Key Vault et la clé que vous souhaitez utiliser pour Azure Information Protection. Pour plus d’informations, consultez la [documentation Azure Key Vault](https://docs.microsoft.com/azure/key-vault/).

Notez les points suivants pour configurer votre Azure Key Vault et votre clé pour BYOK :

- [Exigences relatives à la longueur de clé](#key-length-requirements)
- [Création d’une clé protégée par HSM localement et transfert de celle-ci vers votre coffre de clés](#creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault)
- [Configuration de Azure Information Protection avec votre ID de clé](#configuring-azure-information-protection-with-your-key-id)
- [Autorisation du service Azure Rights Management pour utiliser votre clé](#authorizing-the-azure-rights-management-service-to-use-your-key)

#### <a name="key-length-requirements"></a>Exigences relatives à la longueur de clé

Lors de la création de votre clé, assurez-vous que la longueur de la clé est soit 2048 bits (recommandé), soit 1024 bits. Les autres longueurs de clé ne sont pas prises en charge par Azure Information Protection.

> [!NOTE]
> les clés 1024 bits ne sont pas considérées comme offrant un niveau de protection adéquat pour les clés de locataire actives.
>
>Microsoft n’approuve pas l’utilisation de longueurs de clé inférieures, telles que les clés RSA 1024 bits, et l’utilisation associée de protocoles qui offrent des niveaux de protection inadéquats, tels que SHA-1.
>

#### <a name="creating-an-hsm-protected-key-on-premises-and-transferring-it-to-your-key-vault"></a>Création d’une clé protégée par HSM localement et transfert de celle-ci vers votre coffre de clés

Pour créer une clé protégée par HSM localement et la transférer vers votre coffre de clés en tant que clé protégée par HSM, suivez les procédures décrites dans la documentation de Azure Key Vault : [génération et transfert de clés protégées par HSM pour les Azure Key Vault](https://docs.microsoft.com/azure/key-vault/keys/hsm-protected-keys-byok).

Pour que Azure Information Protection utilise la clé transférée, toutes les opérations de Key Vault doivent être autorisées pour la clé, notamment :

- encrypt
- decrypt
- wrapKey
- unwrapKey
- sign
- verify

Par défaut, toutes les opérations de Key Vault sont autorisées.

Pour vérifier les opérations autorisées pour une clé spécifique, exécutez la commande PowerShell suivante :

```ps
(Get-AzKeyVaultKey -VaultName <key vault name> -Name <key name>).Attributes.KeyOps
```

Si nécessaire, ajoutez des opérations autorisées à l’aide de [Update-AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/update-azkeyvaultkey) et du paramètre *KeyOps* .

#### <a name="configuring-azure-information-protection-with-your-key-id"></a>Configuration de Azure Information Protection avec votre ID de clé

Les clés stockées dans le Azure Key Vault ont chacune un ID de clé.

L’ID de clé est une URL qui contient le nom du coffre de clés, le conteneur de clés, le nom de la clé et la version de la clé. Par exemple :

**https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**.

Configurez Azure Information Protection pour utiliser votre clé en spécifiant son URL de coffre de clés.

#### <a name="authorizing-the-azure-rights-management-service-to-use-your-key"></a>Autorisation du service Azure Rights Management pour utiliser votre clé

Le service de Rights Management Azure doit être autorisé à utiliser votre clé. Azure Key Vault administrateurs peuvent activer cette autorisation à l’aide de l’Portail Azure ou Azure PowerShell.

##### <a name="enabling-key-authorization-using-the-azure-portal"></a>Activation de l’autorisation de clé à l’aide de l’Portail Azure

1. Connectez-vous au portail Azure et accédez à **clés coffres**d'  >  **\<*your key vault name*>**  >  **accès stratégies d’accès**  >  **Ajouter nouveau**.

1. Dans le volet **Ajouter une stratégie d’accès** , dans la zone de liste **configurer à partir d’un modèle (facultatif)** , sélectionnez **Azure information protection BYOK**, puis cliquez sur **OK**.

    Le modèle sélectionné a la configuration suivante :

    - La valeur de l' **entité de sélection** est définie sur **services Microsoft Rights Management.**
    - Les **autorisations de clé** sélectionnées incluent les autorisations d' **extraction,** de **déchiffrement** et de **signature.**

##### <a name="enabling-key-authorization-using-powershell"></a>Activation de l’autorisation de clé à l’aide de PowerShell

Exécutez l’applet de commande PowerShell Key Vault, [Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)et accordez des autorisations au principal du service Azure Rights Management à l’aide du GUID **00000012-0000-0000-C000-000000000000**.

Par exemple :

```ps
Set-AzKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get
```

### <a name="configure-azure-information-protection-to-use-your-key"></a>Configurer Azure Information Protection pour utiliser votre clé

Une fois que vous avez terminé toutes les étapes ci-dessus, vous êtes prêt à configurer Azure Information Protection pour utiliser cette clé comme clé de locataire de votre organisation.

À l’aide des applets de commande Azure RMS, exécutez les commandes suivantes :

1. Connectez-vous au service Azure Rights Management et connectez-vous :
    ```ps
    Connect-AipService
    ```

1. Exécutez l' [applet de commande use-AipServiceKeyVaultKey](https://docs.microsoft.com/powershell/module/aipservice/use-aipservicekeyvaultkey), en spécifiant l’URL de la clé. Par exemple :

    ```ps
    Use-AipServiceKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/<key-version>"
    ```

    > [!IMPORTANT]
    > Dans cet exemple, `<key-version>` est la version de la clé que vous souhaitez utiliser. Si vous ne spécifiez pas la version, la version actuelle de la clé est utilisée par défaut, et la commande peut sembler fonctionner. Toutefois, si votre clé est mise à jour ou renouvelée ultérieurement, le service Azure Rights Management cessera de fonctionner pour votre locataire, même si vous exécutez à nouveau la commande **use-AipServiceKeyVaultKey** .
    >
    > Utilisez la commande [AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/get-azkeyvaultkey) en fonction des besoins pour connaître le numéro de version de la clé actuelle.
    >
    > Par exemple : `Get-AzKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

    Pour confirmer que l’URL de la clé est définie correctement pour Azure Information Protection, exécutez la commande [AzKeyVaultKey](https://docs.microsoft.com/powershell/module/az.keyvault/get-azkeyvaultkey) dans le Azure Key Vault pour afficher l’URL de la clé.

1. Si le service Azure Rights Management est déjà activé, exécutez [Set-AipServiceKeyProperties](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicekeyproperties) pour indiquer à Azure information protection d’utiliser cette clé comme clé de locataire active pour le service de Rights Management Azure.

Azure Information Protection est maintenant configurée pour utiliser votre clé au lieu de la clé créée par défaut par Microsoft qui a été créée automatiquement pour votre locataire.

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez configuré la protection BYOK, passez à la section prise en main de [votre clé racine de locataire](get-started-tenant-root-keys.md) pour plus d’informations sur l’utilisation et la gestion de votre clé.
