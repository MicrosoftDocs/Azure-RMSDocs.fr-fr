---
title: "Gérée par le client - opérations de cycle de vie des clés de locataires | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 496edca2e2323e17216858e2ab4844fdb0aa1fb0


---


# Gérée par le client : opérations de cycle de vie des clés de locataires

*S’applique à : Azure Rights Management, Office 365*

Si vous gérez votre clé de locataire pour Azure Rights Management (dans le cadre d’un scénario BYOK, ou Bring Your Own Key), utilisez les sections suivantes pour obtenir plus d’informations sur les opérations de cycle de vie qui s’appliquent à cette topologie.

## Révocation de votre clé de locataire
Lorsque vous annulez votre abonnement aux services Azure RMS, ces derniers arrêtent d'utiliser votre clé de locataire et aucune autre action n'est requise de votre part.

## Renouvellement de votre clé de locataire
Le renouvellement de la clé est également appelé déploiement de la clé. Ne renouvelez pas votre clé de locataire à moins que ce soit vraiment nécessaire. Les clients plus anciens, tels qu'Office 2010, n'ont pas été conçu pour gérer naturellement les changements de clés. Dans ce scénario, vous devez effacer l'état RMS des ordinateurs à l'aide d'une stratégie de groupe ou d'un mécanisme similaire. Toutefois, certains événements légitimes peuvent vous obliger à renouveler votre clé de locataire. Par exemple :

-   Votre entreprise s'est divisée en deux sociétés distinctes ou plus. Lorsque vous renouvelez votre clé de locataire, la nouvelle société n'aura pas accès au nouveau contenu publié par vos employés. Elle pourra toujours accéder à l'ancien contenu si elle dispose d'une copie de l'ancienne clé de locataire.

-   Vous pensez que la copie principale de votre clé de locataire (celle en votre possession) a été compromise.

Lorsque vous renouvelez votre clé de locataire, le nouveau contenu est protégé à l'aide de la nouvelle clé de locataire. Vous obtenez ce résultat en plusieurs étapes. Ainsi, pendant un certain temps, certains nouveaux contenus continueront d'être protégés par l'ancienne clé de locataire. Le contenu précédemment protégé reste protégé par l'ancienne clé de locataire. Pour prendre en charge ce scénario, les services Azure RMS conservent votre ancienne clé de locataire afin qu'ils puissent émettre des licences pour l'ancien contenu.

Pour renouveler votre clé de locataire, générez et créez une clé sur Internet ou en personne, en appliquant les procédures décrites dans la section [Implémentation de la solution Bring Your Own Key (BYOK)](..\plan-design\plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) de la rubrique [Planification et implémentation de la clé de locataire Azure Rights Management](..\plan-design\plan-implement-tenant-key.md).

## Sauvegarde et récupération de votre clé de locataire
Vous êtes responsable de la sauvegarde de votre clé de locataire. Si vous avez généré votre clé de locataire dans un module de sécurité matériel Thales, pour sauvegarder la clé, il vous suffit de sauvegarder le fichier de clé tokénisée, le fichier Word ainsi que les cartes Administrateur.

Si vous avez transféré votre clé en apliquant les procédures décrites dans la section [Implémentation de la solution Bring Your Own Key (BYOK)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) de l’article [Planification et implémentation de la clé de locataire Azure Rights Management](../plan-design/plan-implement-tenant-key.md), Azure RMS conserve le fichier de clé tokénisée pour fournir une protection contre les défaillances de nœuds Azure RMS. Cependant, il ne s'agit pas là d'une sauvegarde complète. Par exemple, si vous avez besoin d'une copie en clair de votre clé afin d'utiliser celle-ci en dehors d'un module de sécurité matériel Thales, les services Azure RMS ne pourront pas le récupérer à votre place, car ils ne disposent que d'une copie non récupérable.

## Exportation de votre clé de locataire
Si vous utilisez une solution BYOK, vous ne pouvez pas exporter votre clé de locataire à partir d'Azure RMS. La copie se trouvant dans Azure RMS est non récupérable. Si vous souhaitez supprimer cette clé afin qu'elle soit inutilisable, contactez le service clientèle Microsoft.

## Réponse à une violation
Un système de sécurité est incomplet sans un processus de réponse aux violations. Votre clé de locataire peut être compromise ou volée. Même si elle est bien protégée, des vulnérabilités peuvent être détectées dans la technologie actuelle du module de sécurité matériel (HSM), ou dans les longueurs et les algorithmes des clés.

Microsoft dispose d'une équipe chargée de répondre aux incidents de sécurité survenant dans ses produits et services. Dès la réception d'un rapport d'incident avéré, cette équipe met tout en œuvre pour analyser la portée, la cause première et les actions de correction à mettre en place. Si ces incidents affectent vos ressources, Microsoft enverra une notification par courrier électronique (à l'adresse fournie lors de la création de l'abonnement) aux administrateurs de votre client Azure RMS.

En cas de violation, la meilleure action que vous ou Microsoft pourra mettre en place dépend de la portée de la violation. Microsoft vous accompagnera lors de ce processus. Le tableau suivant présente des situations type et les réponses que vous pouvez mettre en place. Toutefois, la réponse exacte que vous apporterez dépendra des informations obtenues lors de l'analyse.

|Description de l'incident|Réponse possible|
|------------------------|-------------------|
|Votre clé de locataire a fait l'objet d'une fuite.|Renouvelez votre clé de locataire. Consultez [Renouvellement de votre clé de locataire](#re-key-your-tenant-key).|
|Une personne non autorisée ou un programme malveillant a obtenu le droit d'utiliser votre clé de locataire, sans que celle-ci ait fait l'objet d'une fuite.|Dans ce cas, le renouvellement de votre clé de locataire ne sera pas utile et une analyse de la cause première sera obligatoire. Si un bogue au niveau d'un processus ou d'un logiciel est responsable de l'accès de l'individu non autorisé, cette situation doit être résolue.|
|Vulnérabilité détectée dans la technologie HSM actuelle.|Microsoft doit mettre à jour les modules de sécurité matériel. S'il y a des raisons de penser que les clés ont été exposées via cette vulnérabilité, Microsoft demandera à tous les clients de renouveler leur clé de locataire.|
|Une vulnérabilité a été découverte dans l'algorithme RSA ou la longueur de la clé, ou des attaques en force brute peuvent être envisagées au niveau informatique.|Microsoft doit mettre à jour les services Azure RMS pour prendre en charge de nouveaux algorithmes et longueurs de clé plus élevées qui sont résilients, mais également informer tous les clients qu'ils doivent renouveler leur clé de locataire.|





<!--HONumber=Jul16_HO3-->


