---
title: "Planification et implémentation de la clé de locataire Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a80866576dc7d6400bcebc2fc1c37bc0367bcdf3
ms.openlocfilehash: ee7b9b5f251856f102651f1e8f379f7bbacea77e


---

# Planification et implémentation de la clé de locataire Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Utilisez les informations de cet article pour planifier et gérer votre clé de locataire (ou client) Rights Management (RMS) pour Azure RMS. Par exemple, au lieu que Microsoft gère votre clé de locataire (par défaut), vous pouvez gérer votre propre clé de locataire afin de vous conformer à des réglementations spécifiques s'appliquant à votre organisation.  La gestion de votre propre clé de locataire est également appelée BYOK (Bring Your Own Key).

> [!NOTE]
> La clé de locataire RMS est également appelée « clé de certificat de licence serveur » (SLC). Azure RMS gère une ou plusieurs clés pour chaque organisation s'abonnant à Azure RMS. Lorsqu'une clé est utilisée pour RMS au sein d'une organisation (par exemple, clés utilisateur, clés d'ordinateur, clés de chiffrement de document), elle est ajoutée par chiffrement à la clé de locataire RMS.

**Aperçu rapide :** Utilisez le tableau suivant comme guide rapide pour votre topologie de clé de locataire recommandée. Ensuite, utilisez la documentation supplémentaire pour obtenir plus d’informations.

Si vous déployez Azure RMS à l'aide d'une clé de locataire gérée par Microsoft, vous pourrez passer ultérieurement à la solution BYOK. Toutefois, vous ne pouvez pas passer actuellement d'une solution de clé de locataire Azure RMS BYOK à une clé de locataire gérée par Microsoft.

|Besoin de l'entreprise|Topologie de clé de locataire recommandée|
|------------------------|-----------------------------------|
|Déployer Azure RMS rapidement et sans nécessiter un matériel spécial|Géré par Microsoft|
|Besoin de toutes les fonctionnalités IRM dans Exchange Online avec Azure RMS|Gestion par Microsoft|
|Vos clés sont créées par vous, et protégées dans un module de sécurité matériel (HSM)|BYOK<br /><br />Actuellement, cette configuration entraîne une réduction des fonctionnalités IRM dans Exchange Online. Pour plus d’informations, consultez la section [Tarifs et restrictions BYOK](byok-price-restrictions.md) .|

## Choix de la topologie de clé de locataire : gestion Microsoft (par défaut) ou gestion BYOK
Choisissez la topologie de clé de locataire la plus adaptée à votre organisation. Par défaut, Azure RMS génère la clé de locataire et gère la plupart des aspects de son cycle de vie. Il s'agit de l'option la plus simple, avec la charge administrative la plus faible. Dans la plupart des cas, les utilisateurs n'ont même pas conscience de l'existence de cette clé de locataire. Il leur suffit de s'inscrire à Azure RMS ; le reste du processus de gestion de la clé est traité par Microsoft.

Vous pouvez aussi vouloir un contrôle total sur votre clé de locataire en utilisant [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). Ce scénario implique la création de votre clé de locataire et la conservation de la copie principale sur votre serveur local. Il est souvent fait référence à ce scénario sous le terme « Bring your own key » (BYOK). Cette option implique les étapes suivantes :

1.  Générez votre clé de locataire en local, en accord avec vos stratégies informatiques et de sécurité.

2.  Transférez de façon sécurisée la clé de locataire depuis un module de sécurité matériel (HSM) en votre possession vers des modules de sécurité matériels détenus et gérés par Microsoft, en utilisant Azure Key Vault. Notez que tout au long de ce processus, la clé de locataire ne quitte jamais les limites de protection matérielles.

3.  Quand vous transférez votre clé de locataire à Microsoft, celle-ci reste protégée par Azure Key Vault.

Bien que cette action soit facultative, vous pouvez également utiliser les journaux d'utilisation quasiment en temps réel à partir d'Azure RMS pour voir exactement quand et comment votre clé de locataire est utilisée.

> [!NOTE]
> En guise de mesure de protection supplémentaire, Azure Key Vault utilise des domaines de sécurité distincts pour ses centres de données dans des régions comme Amérique du Nord, EMEA (Europe, Moyen-Orient et Afrique) et Asie, de même que pour les différentes instances d’Azure, comme Microsoft Azure Allemagne et Azure Government. Quand vous gérez votre propre clé de locataire, celle-ci est liée au domaine de sécurité de la région ou de l’instance où votre locataire RMS est inscrit. Par exemple, la clé de locataire d'un client européen ne peut pas être utilisée dans des centres de données en Amérique du Nord ou en Asie.

## Cycle de vie d'une clé de locataire
Si vous choisissez de confier à Microsoft la gestion de votre clé de locataire, Microsoft traite la plupart des aspects de son cycle de vie. Cependant, si vous décidez de gérer votre clé de locataire, vous êtes responsable d’un grand nombre d’opérations du cycle de vie de la clé et de certaines procédures supplémentaires dans Azure Key Vault.

Les schémas ci-dessous présentent et comparent ces deux options. Le premier schéma permet notamment de juger de la faible charge administrative qui vous incombe dans la configuration par défaut, lorsque Microsoft gère la clé de locataire.

![Cycle de vie de clé de locataire Azure RMS - géré par Microsoft, valeur par défaut](../media/RMS_BYOK_cloud.png)

Le deuxième schéma présente quant à lui les étapes supplémentaires requises lorsque vous gérez votre clé de locataire.

![Cycle de vie de clé de locataire Azure RMS - géré par vous-même, BYOK](../media/RMS_BYOK_onprem4.png)

Si vous choisissez de confier à Microsoft la gestion de votre clé de locataire, aucune autre action n’est nécessaire de votre part et vous n’avez pas à générer la clé. Vous pouvez passer directement à la rubrique [Étapes suivantes](plan-implement-tenant-key.md#next-steps).

Si vous décidez de gérer vous-même votre clé de locataire, lisez les sections suivantes pour plus d'informations.

## Implémentation de la clé de locataire Azure Rights Management

Utilisez les informations et les procédures de cette section si vous souhaitez générer et gérer vous-même votre clé de locataire (solution BYOK) :


> [!IMPORTANT]
> Si vous avez déjà commencé à utiliser [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (le service est activé) et que certains de vos utilisateurs exécutent Office 2010, [contactez le support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) avant d’appliquer ces procédures. Selon votre scénario et vos exigences, vous devrez peut-être appliquer la solution BYOK avec certaines limitations ou étapes supplémentaires.
> 
> Vous pouvez aussi [contacter le support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) si votre organisation applique des stratégies spécifiques en matière de gestion des clés.

### Conditions requises pour la solution BYOK
Reportez-vous au tableau suivant pour connaître les conditions requises pour la solution Bring your own key (BYOK).

|Condition requise|Plus d'informations|
|---------------|--------------------|
|Abonnement prenant en charge Azure RMS.|Pour plus d’informations sur les abonnements disponibles, consultez [Abonnements au cloud prenant en charge Azure RMS](../get-started/requirements-subscriptions.md).|
|Vous n'utilisez pas RMS for Individuals ou Exchange Online. Ou, si vous utilisez Exchange Online, vous comprenez et acceptez les limitations liées à l'utilisation de la solution BYOK avec cette configuration.|Pour plus d’informations sur les restrictions et limitations actuelles relatives à la solution BYOK, consultez [Tarifs et restrictions BYOK](byok-price-restrictions.md).<br /><br />**Important** : Actuellement, la solution BYOK n’est pas compatible avec Exchange Online.|
|Toutes les conditions préalables répertoriées pour BYOK dans Key Vault.|Consultez [Conditions préalables pour BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) dans la documentation d’Azure Key Vault. <br /><br />**Remarque** : Si vous migrez d’AD RMS vers Azure RMS en passant d’une clé logicielle à une clé matérielle, vous devez disposer au minimum de la version 11.62 pour le microprogramme Thales.|
|Le module d’administration Azure RMS pour Windows PowerShell.|Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](../deploy-use/install-powershell.md). <br /><br />Si vous avez déjà installé ce module Windows PowerShell, exécutez la commande suivante pour vérifier que le numéro de votre version est au minimum **2.5.0.0** : `(Get-Module aadrm -ListAvailable).Version`|

Pour plus d’informations sur les modules de sécurité matériels Thales et comment ils sont utilisés avec Azure Key Vault, consultez le [site web de Thales](https://www.thales-esecurity.com/msrms/cloud).

Pour générer et transférer votre propre clé de locataire dans Azure Key Vault, suivez les procédures de la rubrique [Comment générer et transférer les clés protégées par HSM pour Azure Ket Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) dans la documentation d’Azure Key Vault.

Quand la clé est transférée vers Key Vault, elle reçoit un ID de clé dans Key Vault. Il s’agit d’une URL contenant le nom du coffre, le conteneur de clés, le nom de la clé et la version de la clé. Par exemple : **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Vous devez indiquer à Azure RMS d’utiliser cette clé en spécifiant cette URL.

Mais avant qu’Azure RMS puisse utiliser la clé, il doit être autorisé à utiliser la clé dans le coffre de clés de votre organisation. Pour cela, l’administrateur d’Azure Key Vault utilise l’applet de commande PowerShell de Key Vault, [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx) et accorde des autorisations au principal du service Azure RMS, **Microsoft.Azure.RMS**. Exemple :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign 

Vous êtes maintenant prêt à configurer Azure RMS pour utiliser cette clé comme clé de locataire Azure RMS de votre organisation. En utilisant des applets de commande Azure RMS, connectez-vous d’abord à Azure RMS :

    Connect-AadrmService

Ensuite, exécutez l’applet de commande [Add-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx) en spécifiant l’URL de la clé. Exemple :

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

Si vous devez vérifier que l’URL de la clé est définie correctement dans Azure RMS, vous pouvez exécuter [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) dans Azure Key Vault pour voir l’URL de la clé.


## Étapes suivantes

Maintenant que vous avez planifié et, le cas échéant, généré votre clé de locataire, procédez comme suit :

1.  Commencez à utiliser votre clé de locataire :

    -   Si ce n'est déjà fait, vous devez maintenant activer Rights Management pour que votre organisation puisse utiliser RMS. Les utilisateurs peuvent commencer immédiatement à utiliser votre clé de locataire (gérée par Microsoft ou par vous dans Azure Key Vault).

        Pour plus d’informations sur l’activation, consultez [Activation d’Azure Rights Management](../deploy-use/activate-service.md).

    -   Si vous avez déjà activé Rights Management et avez décidé de gérer vous-même vote clé de locataire, les utilisateurs passent graduellement de l'ancienne clé de locataire à la nouvelle. Cette transition progressive s'effectue en quelques semaines. Les documents et fichiers protégés par l'ancienne clé de locataire restent accessibles pour les utilisateurs autorisés.

2.  Envisagez l’activation de la journalisation de l’utilisation, qui consigne chaque transaction effectuée par Azure Rights Management.

    Si vous avez décidé de gérer vous-même votre clé de locataire, la journalisation inclut des informations utiles sur son utilisation. Consultez l’extrait de code suivant, tiré d’un fichier journal affiché dans Excel, où les types de requête **KeyVaultDecryptRequest** et **KeyVaultSignRequest** montrent que la clé de locataire est utilisée.

    ![fichier journal dans Excel où la clé de locataire est utilisée](../media/RMS_Logging.png)

    Pour plus d’informations sur la journalisation de l’utilisation, consultez [Journalisation et analyse de l’utilisation d’Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Gérez votre clé de locataire.

    Pour plus d’informations, consultez [Opérations pour votre clé de locataire Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Aug16_HO3-->


