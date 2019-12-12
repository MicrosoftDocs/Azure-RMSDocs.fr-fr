---
title: 'Gérée par Microsoft : opérations de cycle de vie des clés de locataires AIP'
description: Informations sur les opérations de cycle de vie applicables si Microsoft gère votre clé de locataire pour Azure Information Protection (option par défaut).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ee94f0a4966ce16ae8b87f23bf4a9a734cc015a0
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73444970"
---
# <a name="microsoft-managed-tenant-key-life-cycle-operations"></a>Gérée par Microsoft : opérations de cycle de vie des clés de locataire

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si Microsoft gère votre clé de locataire pour Azure Information Protection (l’option par défaut), utilisez les sections suivantes pour obtenir plus d’informations sur les opérations de cycle de vie qui s’appliquent à cette topologie.

## <a name="revoke-your-tenant-key"></a>Révocation de votre clé de locataire
Quand vous annulez votre abonnement Azure Information Protection, Azure Information Protection arrête d’utiliser votre clé de locataire, et aucune action n’est nécessaire de votre part.

## <a name="rekey-your-tenant-key"></a>Renouvellement de votre clé de locataire
Le renouvellement de la clé est également appelé déploiement de la clé. Quand vous effectuez cette opération, Azure Information Protection cesse d’utiliser la clé de locataire existante pour protéger les documents et les e-mails, et commence à utiliser une autre clé. Les stratégies et les modèles sont immédiatement abandonnés, mais ce changement est progressif pour les clients et les services existants qui utilisent Azure Information Protection. Ainsi, pendant quelque temps, certains nouveaux contenus continuent d’être protégés par l’ancienne clé de locataire.

Pour renouveler la clé, vous devez configurer l’objet de clé de locataire et spécifier la clé de remplacement à utiliser. Ensuite, la clé précédemment utilisée est automatiquement marquée comme archivée pour Azure Information Protection. Cette configuration garantit que le contenu protégé à l’aide de cette clé reste accessible.

Exemples de scénarios dans lesquels il peut être nécessaire de renouveler la clé pour Azure Information Protection :

- Vous avez effectué la migration à partir des services AD RMS (Active Directory Rights Management Services) avec une clé en mode de chiffrement 1. Une fois la migration terminée, vous souhaitez passer à une clé qui utilise le mode de chiffrement 2.

- Votre entreprise s'est divisée en deux sociétés distinctes ou plus. Quand vous renouvelez votre clé de locataire, la nouvelle société n’a pas accès au nouveau contenu publié par vos employés. Elle pourra toujours accéder à l'ancien contenu si elle dispose d'une copie de l'ancienne clé de locataire.

- Vous voulez passer d’une topologie de gestion des clés à une autre.

- Vous pensez que la copie principale de votre clé de locataire a été compromise.

Pour renouveler la clé, vous pouvez sélectionner une autre clé gérée par Microsoft comme clé de locataire, mais vous ne pouvez pas créer une clé gérée par Microsoft. Pour créer une clé, vous devez passer à une topologie de clé gérée par le client (BYOK).

Si vous avez effectué la migration à partir des services AD RMS (Active Directory Rights Management Services) et que vous avez choisi la topologie de clé gérée par Microsoft pour Azure Information Protection, vous disposez de plusieurs clés gérées par Microsoft. Dans ce scénario, vous avez au moins deux clés gérées par Microsoft pour votre locataire. Au moins une clé a été importée à partir d’AD RMS. Vous disposez également de la clé par défaut qui a été automatiquement créée pour votre locataire Azure Information Protection.

Pour sélectionner une autre clé comme clé de locataire active pour Azure Information Protection, utilisez l’applet de commande [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) à partir du module AIPService. Pour vous aider à identifier la clé à utiliser, utilisez l’applet de commande [« obtenir-AipServiceKeys »](/powershell/module/aipservice/get-aipservicekeys) . Vous pouvez identifier la clé par défaut qui a été automatiquement créée pour votre locataire Azure Information Protection en exécutant la commande suivante :

    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

Pour passer à une topologie de clé gérée par le client (BYOK), consultez [Implémentation de BYOK pour votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

## <a name="backup-and-recover-your-tenant-key"></a>Sauvegarde et récupération de votre clé de locataire
Microsoft se charge de sauvegarder votre clé de locataire. Aucune action n'est requise de votre part.

## <a name="export-your-tenant-key"></a>Exportation de votre clé de locataire
Vous pouvez exporter votre clé de locataire et votre configuration Azure Information Protection en suivant les instructions contenues dans les trois étapes suivantes :

### <a name="step-1-initiate-export"></a>Étape 1 : initiation d'une exportation

- [Contactez le support Microsoft](information-support.md#to-contact-microsoft-support) pour ouvrir un **dossier de support Azure Information Protection dans lequel vous demandez l’exportation d’une clé Azure Information Protection**. Vous devez prouver que vous êtes un administrateur global pour votre locataire et comprenez que ce processus prend plusieurs jours pour confirmer. Des frais de prise en charge standard s’appliquent. L’exportation de votre clé de locataire n’est pas un service de support technique gratuit.

### <a name="step-2-wait-for-verification"></a>Étape 2 : attente de la vérification

- Microsoft vérifie la légitimité de votre demande d’émission de votre clé de locataire Azure Information Protection. Cela peut prendre jusqu’à trois semaines.

### <a name="step-3-receive-key-instructions-from-css"></a>Étape 3 : réception d'instructions concernant la clé de la part du support technique

- Les services de support technique Microsoft vous envoient votre clé de locataire et votre configuration Azure Information Protection sous forme chiffrée dans un fichier protégé par mot de passe. L’extension de nom de fichier est **.tpd**. Pour ce faire, le support technique vous envoie (vous, la personne ayant demandé un export) tout d'abord un outil par e-mail. Vous devez exécuter cet outil à partir d'une invite de commande, comme suit :

    ```
    AadrmTpd.exe -createkey
    ```
    Cette opération génère une paire de clés RSA et enregistre les moitiés publique et privée sous forme de fichiers dans le dossier actuel. Par exemple : **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** et **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Répondez à l’e-mail que vous a envoyé le support technique et joignez à celui-ci le fichier portant un nom commençant par **PublicKey**. Le support technique vous envoie ensuite un fichier TPD au format .xml, chiffré à l’aide de votre clé RSA. Copiez ce fichier dans le dossier dans lequel vous avez initialement exécuté l’outil AadrmTpd, puis réexécutez l’outil à l’aide de votre fichier dont le nom commence par **PrivateKey** et du fichier reçu du support technique. Exemple :

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    Cette commande doit générer deux fichiers : l’un contient le mot de passe en clair pour le TPD protégé par mot de passe, tandis que l’autre contient le TPD protégé par mot de passe en question. Les fichiers ont un nouveau GUID, par exemple :
     
  - Password-5E4C2018-8C8C-4548-8705-E3218AA1544E.txt

  - ExportedTPD-5E4C2018-8C8C-4548-8705-E3218AA1544E.xml

    Sauvegardez ces fichiers et stockez-les dans un emplacement sécurisé de façon à pouvoir continuer à déchiffrer le contenu protégé par cette clé de locataire. De plus, si vous migrez vers AD RMS, vous pouvez importer ce fichier de TPD (dont le nom commence par **ExportedTDP**) sur votre serveur AD RMS.

### <a name="step-4-ongoing-protect-your-tenant-key"></a>Étape 4 : En cours : Protection de votre clé de locataire

Après avoir reçu votre clé de locataire, conservez-la en lieu sûr, car toute personne y ayant accès peut déchiffrer tous les documents qu'elle protège.

Si vous exportez votre clé de locataire parce que vous ne voulez plus utiliser Azure Information Protection, nous vous conseillons de désactiver le service Azure Rights Management à partir de votre locataire Azure Information Protection. Ne reportez pas cela à plus tard après avoir reçu votre clé de locataire, car cette précaution vous permet de minimiser les conséquences éventuelles d’un accès à votre clé de locataire par une personne non autorisée. Pour obtenir des instructions, consultez [Mise hors service et désactivation d’Azure Rights Management](decommission-deactivate.md).

## <a name="respond-to-a-breach"></a>Réponse à une violation
Un système de sécurité est incomplet sans un processus de réponse aux violations. Votre clé de locataire peut être compromise ou volée. Même si elle est bien protégée, des vulnérabilités peuvent être détectées dans la technologie actuelle de clé ou dans les longueurs et algorithmes actuels des clés.

Microsoft dispose d'une équipe chargée de répondre aux incidents de sécurité survenant dans ses produits et services. Dès la réception d'un rapport d'incident avéré, cette équipe met tout en œuvre pour analyser la portée, la cause première et les actions de correction à mettre en place. Si cet incident affecte vos ressources, Microsoft informe les administrateurs généraux de votre locataire par courrier électronique.

En cas de violation, la meilleure mesure que vous ou Microsoft puissiez prendre dépend de la portée de la violation. Microsoft vous accompagnera dans ce processus. Le tableau suivant présente des situations type et les réponses que vous pouvez mettre en place. Toutefois, la réponse exacte que vous apporterez dépend des informations obtenues lors de l’analyse.

|Description de l'incident|Réponse possible|
|------------------------|-------------------|
|Votre clé de locataire a fait l'objet d'une fuite.|Renouvelez votre clé de locataire. Consultez la section [Renouvellement de votre clé de locataire](#rekey-your-tenant-key) dans cet article.|
|Une personne non autorisée ou un programme malveillant a obtenu le droit d'utiliser votre clé de locataire, sans que celle-ci ait fait l'objet d'une fuite.|Dans ce cas, le renouvellement de votre clé de locataire n’est pas utile et une analyse de la cause première est obligatoire. Si un bogue au niveau d'un processus ou d'un logiciel est responsable de l'accès de l'individu non autorisé, cette situation doit être résolue.|
|Une vulnérabilité a été découverte dans l'algorithme RSA ou la longueur de la clé, ou des attaques en force brute peuvent être envisagées au niveau informatique.|Microsoft doit mettre à jour Azure Information Protection pour prendre en charge de nouveaux algorithmes et des clés plus longues qui sont résilientes. Il est aussi demandé à tous les clients de recréer leur clé de locataire.|


