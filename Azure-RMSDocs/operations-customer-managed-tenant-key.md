---
title: 'Gérée par le client : opérations de cycle de vie des clés de locataires AIP'
description: Informations sur les opérations de cycle de vie applicables si vous gérez votre clé de locataire pour Azure Information Protection (dans le cadre d’un scénario BYOK, ou Bring Your Own Key).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 682ed03cfafa9dad1d9696d51e0b64c71dea6fa3
ms.sourcegitcommit: fbd1834eaacb17857e59421d7be0942a9a0eefb2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445055"
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>Gérée par le client : opérations de cycle de vie des clés de locataires

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si vous gérez votre clé de locataire pour Azure Information Protection (dans le cadre d’un scénario BYOK, ou Bring Your Own Key), utilisez les sections suivantes pour obtenir plus d’informations sur les opérations de cycle de vie qui s’appliquent à cette topologie.

## <a name="revoke-your-tenant-key"></a>Révocation de votre clé de locataire
Dans Azure Key Vault, vous pouvez modifier les autorisations sur le coffre de clés qui contient votre clé de locataire Azure Information Protection pour que le service Azure Rights Management ne puisse plus accéder à la clé. Cependant, si vous effectuez cette opération, personne ne peut ouvrir les documents et les e-mails que vous avez précédemment protégés à l’aide du service Azure Rights Management.

Quand vous annulez votre abonnement Azure Information Protection, Azure Information Protection arrête d’utiliser votre clé de locataire, et aucune action n’est nécessaire de votre part.

## <a name="rekey-your-tenant-key"></a>Renouvellement de votre clé de locataire
Le renouvellement de la clé est également appelé déploiement de la clé. Quand vous effectuez cette opération, Azure Information Protection cesse d’utiliser la clé de locataire existante pour protéger les documents et les e-mails, et commence à utiliser une autre clé. Les stratégies et les modèles sont immédiatement abandonnés, mais ce changement est progressif pour les clients et les services existants qui utilisent Azure Information Protection. Ainsi, pendant quelque temps, certains nouveaux contenus continuent d’être protégés par l’ancienne clé de locataire.

Pour renouveler la clé, vous devez configurer l’objet de clé de locataire et spécifier la clé de remplacement à utiliser. Ensuite, la clé précédemment utilisée est automatiquement marquée comme archivée pour Azure Information Protection. Cette configuration garantit que le contenu protégé à l’aide de cette clé reste accessible.

Exemples de scénarios dans lesquels il peut être nécessaire de renouveler la clé pour Azure Information Protection :

- Votre entreprise s'est divisée en deux sociétés distinctes ou plus. Quand vous renouvelez votre clé de locataire, la nouvelle société n’a pas accès au nouveau contenu publié par vos employés. Elle pourra toujours accéder à l'ancien contenu si elle dispose d'une copie de l'ancienne clé de locataire.

- Vous voulez passer d’une topologie de gestion des clés à une autre. 

- Vous pensez que la copie principale de votre clé de locataire (celle en votre possession) est compromise.

Pour renouveler la clé et obtenir ainsi une autre clé que vous gérez, vous pouvez créer une clé dans Azure Key Vault ou utiliser une autre clé déjà présente dans Azure Key Vault. Suivez ensuite les mêmes procédures que celles que vous avez effectuées pour implémenter BYOK pour Azure Information Protection. 

1. Uniquement si la nouvelle clé se trouve dans un coffre de clés différent de celui que vous utilisez déjà pour Azure Information Protection : autorisez Azure Information Protection à utiliser le coffre de clés à l’aide de l’applet de commande [Set-AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) .

2. Si Azure Information Protection ne connaît pas déjà la clé que vous souhaitez utiliser, exécutez l’applet [de commande use-AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) .

3. Configurez l’objet de clé de locataire à l’aide de l’applet de commande [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) .

Pour plus d’informations sur chacune de ces étapes :

- Pour renouveler la clé et obtenir ainsi une autre clé que vous gérez, consultez [Implémentation de BYOK pour votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).
    
    Si vous renouvelez une clé protégée par HSM que vous créez en local et transférez à Key Vault, vous pouvez utiliser le même univers de sécurité et les mêmes cartes d’accès que pour votre clé actuelle.

- Pour renouveler la clé en la remplaçant par une clé que Microsoft gère pour vous, consultez la section [Renouveler votre clé de locataire](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key) pour les opérations gérées par Microsoft.

## <a name="backup-and-recover-your-tenant-key"></a>Sauvegarde et récupération de votre clé de locataire
Étant donné que vous gérez votre clé de locataire, vous êtes responsable de la sauvegarde de la clé utilisée par Azure Information Protection. 

Si vous avez généré votre clé de locataire localement, dans un HSM nCipher : pour sauvegarder la clé, sauvegardez le fichier de clé, le fichier World et les cartes administrateur. Quand vous transférez votre clé vers Azure Key Vault, le service enregistre le fichier de clé tokenisée pour se protéger des défaillances des nœuds de service. Ce fichier est lié à la sécurité de l’instance ou de la région Azure spécifique. Cependant, ce fichier de clé tokenisée n’est pas une sauvegarde complète. Par exemple, si vous avez besoin d’une copie en texte brut de votre clé pour l’utiliser en dehors d’un HSM nCipher, Azure Key Vault ne pouvez pas la récupérer pour vous, car elle n’a qu’une copie non récupérable.

Azure Key Vault dispose d’une [applet de commande de sauvegarde](/powershell/module/az.keyvault/backup-azkeyvaultkey) que vous pouvez utiliser pour sauvegarder une clé en la téléchargeant et en la stockant dans un fichier. Le contenu téléchargé étant chiffré, il ne peut pas être utilisé à l’extérieur d’Azure Key Vault. 

## <a name="export-your-tenant-key"></a>Exportation de votre clé de locataire
Si vous utilisez BYOK, vous ne pouvez pas exporter votre clé de locataire à partir d’Azure Key Vault ou d’Azure Information Protection. La copie dans Azure Key Vault est non récupérable. 

## <a name="respond-to-a-breach"></a>Réponse à une violation
Un système de sécurité est incomplet sans un processus de réponse aux violations. Votre clé de locataire peut être compromise ou volée. Même si elle est bien protégée, des vulnérabilités peuvent être détectées dans la technologie actuelle de clé ou dans les longueurs et algorithmes actuels des clés.

Microsoft dispose d'une équipe chargée de répondre aux incidents de sécurité survenant dans ses produits et services. Dès la réception d'un rapport d'incident avéré, cette équipe met tout en œuvre pour analyser la portée, la cause première et les actions de correction à mettre en place. Si cet incident affecte vos ressources, Microsoft informe vos administrateurs généraux de locataire par e-mail.

En cas de violation, la meilleure mesure que vous ou Microsoft puissiez prendre dépend de la portée de la violation. Microsoft vous accompagnera dans ce processus. Le tableau suivant présente des situations type et les réponses que vous pouvez mettre en place. Toutefois, la réponse exacte que vous apporterez dépend des informations obtenues lors de l’analyse.

|Description de l'incident|Réponse possible|
|------------------------|-------------------|
|Votre clé de locataire a fait l'objet d'une fuite.|Renouvelez votre clé de locataire. Consultez [Renouvellement de votre clé de locataire](#rekey-your-tenant-key).|
|Une personne non autorisée ou un programme malveillant a obtenu le droit d'utiliser votre clé de locataire, sans que celle-ci ait fait l'objet d'une fuite.|Dans ce cas, le renouvellement de votre clé de locataire n’est pas utile et une analyse de la cause première est obligatoire. Si un bogue au niveau d'un processus ou d'un logiciel est responsable de l'accès de l'individu non autorisé, cette situation doit être résolue.|
|Vulnérabilité détectée dans la technologie HSM actuelle.|Microsoft doit mettre à jour les modules de sécurité matériel. S’il y a des raisons de penser que les clés ont été exposées à cause de cette vulnérabilité, Microsoft demande à tous les clients de recréer leur clé de locataire.|
|Une vulnérabilité a été découverte dans l'algorithme RSA ou la longueur de la clé, ou des attaques en force brute peuvent être envisagées au niveau informatique.|Microsoft doit mettre à jour Azure Key Vault ou Azure Information Protection pour prendre en charge de nouveaux algorithmes et des clés plus longues qui sont résilientes. Il est aussi demandé à tous les clients de recréer leur clé de locataire.|
