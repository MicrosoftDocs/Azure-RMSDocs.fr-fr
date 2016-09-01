---
title: "Migration d’AD RMS vers Azure Rights Management - Phase 4 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 437afd88efebd9719a3db98f8ab0ae07403053f7
ms.openlocfilehash: 21fac7d684f2d544ab97f5ca6eb7faaaca3e9d26


---

# Phase de migration 4 - Tâches de post-migration

*S’applique à : Active Directory Rights Management Services, Azure Rights Management*


Utilisez les informations suivantes pour la Phase 4 de la migration d’AD RMS vers Azure Rights Management (Azure RMS). Ces procédures couvrent les étapes 8 à 9 de [Migration d’AD RMS vers Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Étape 8. Désaffecter AD RMS

Facultatif : Supprimez le point de connexion de service d’Active Directory pour empêcher des ordinateurs de découvrir votre infrastructure Rights Management locale. Cela est facultatif en raison de la redirection que vous avez configurée dans le Registre (par exemple, en exécutant le script de migration). Pour supprimer le point de connexion de service, utilisez l'outil AD SCP Register de la [Boîte à outil d'Administration des services Rights Management](http://www.microsoft.com/download/details.aspx?id=1479).

Surveillez l’activité de vos serveurs AD RMS, par exemple, en vérifiant [les demandes dans le rapport d’intégrité système](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [Table ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) ou [l’audit de l’accès utilisateur au contenu protégé](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Après avoir confirmé que les clients RMS ne communiquent plus avec ces serveurs, et que les clients utilisent avec succès Azure RMS, vous pouvez supprimer le rôle serveur AD RMS de ces serveurs. Si vous utilisez des serveurs dédiés, vous pouvez prendre la précaution de les arrêter pendant un certain temps pour vous assurer qu'aucun problème n'est signalé, qui pourrait nécessiter un redémarrage de ces serveurs pour garantir la continuité de service pendant que vous étudiez la raison pour laquelle les clients n'utilisent pas Azure RMS.

Après la désaffectation de vos serveurs AD RMS, vous pouvez réviser vos modèles dans le portail Azure Classic et les consolider afin que les utilisateurs aient moins de choix, les reconfigurer ou même ajouter de nouveaux modèles. Il serait également judicieux de publier les modèles par défaut. Pour plus d’informations, consultez [Configuration de modèles personnalisés pour Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Étape 9. Renouveler votre clé de locataire Azure RMS
Cette étape s’applique seulement si vous avez choisi une topologie de clé de locataire Gérée par Microsoft et non pas Gérée par le client (BYOK avec Azure Key Vault).

Cette étape est facultative, mais elle est recommandée quand votre clé de locataire Azure RMS est gérée par Microsoft et a été migrée depuis AD RMS. La recréation de clé dans ce scénario permet de protéger votre clé de locataire Azure RMS contre des failles de sécurité de votre clé AD RMS.

Quand vous renouvelez votre clé de locataire Azure RMS (« déploiement de la clé »), une nouvelle clé est créée et la clé d'origine est archivée. Toutefois, étant donné que le basculement d’une clé à l’autre ne se produit pas immédiatement mais sur plusieurs semaines, n’attendez pas de soupçonner une violation de votre clé d’origine et renouvelez votre clé de locataire Azure RMS dès la fin de la migration.

Pour recréer votre clé de locataire Azure RMS gérée par Microsoft : [contactez le support Microsoft](../get-started/information-support.md#to-contact-microsoft-support) et ouvrez un **dossier de support Azure Rights Management avec une demande de recréation de votre clé RMS après une migration depuis AD RMS**. Vous devez prouver que vous êtes administrateur de votre locataire Azure RMS et comprendre que la confirmation de ce processus prend plusieurs jours. Des frais de prise en charge standard s’appliquent. Le renouvellement de votre clé de locataire n’est pas un service de support gratuit.


## Étapes suivantes

Pour plus d’informations sur la gestion de votre clé de locataire RMS, consultez [Opérations pour votre clé de locataire Azure Rights Management](../deploy-use/operations-tenant-key.md).

Maintenant que vous avez terminé la migration, passez en revue la [feuille de route de déploiement](deployment-roadmap.md) pour identifier les autres tâches de déploiement éventuellement nécessaires.




<!--HONumber=Aug16_HO3-->


