---
title: Azure Information Protection l’historique des versions du client & la stratégie de support
description: Découvrez les nouveautés et les changements d’une version du client Azure Information Protection pour Windows, ainsi que la politique du cycle de vie du support.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: abb96a7d86bddea671230fbd033d9c940cf982a3
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79404740"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client Azure Information Protection : historique des versions et politique du support


>*S’applique à : services AD RMS (Active Directory Rights Management Services), [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows server 2012 R2, windows server 2012*
>
> *Instructions pour : [Azure information protection client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*



Vous pouvez télécharger la dernière version en disponibilité générale (GA) et la préversion actuelle (si elle est disponible) à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Après un bref délai de quelques semaines, la dernière version de la disponibilité générale est également incluse dans le catalogue Microsoft Update avec le nom de produit **Microsoft Azure Information Protection** > **client Microsoft Azure information protection**, ainsi que la classification des **mises à jour**. Cette inclusion dans le catalogue signifie que vous pouvez mettre à niveau le client à l’aide de WSUS ou de Configuration Manager, ou d’autres mécanismes de déploiement de logiciels qui utilisent Microsoft Update.

Pour plus d’informations, consultez [Mise à niveau et maintenance du client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

> [!TIP]
> Vous souhaitez utiliser le client d’étiquetage unifié Azure Information Protection, car vos étiquettes sont publiées à partir d’Office 365 Centre de sécurité et de conformité, Microsoft 365 Security Center ou Microsoft 365 Compliance Center ? Lorsque vous téléchargez, puis installez le client d’étiquetage unifié à partir du centre de téléchargement Microsoft, vous pouvez mettre à niveau votre client Azure Information Protection vers le [client d’étiquetage unifié](unifiedlabelingclient-version-release-history.md).

### <a name="servicing-information-and-timelines"></a>Informations de maintenance et chronologies

Chaque version en disponibilité générale (GA) du client Azure Information Protection est prise en charge jusqu'à six mois après la publication de la version GA suivante. À l’exception de cette section, la documentation n’inclut pas d’informations sur les versions du client non prises en charge. Les correctifs et les nouvelles fonctionnalités sont toujours appliqués à la dernière version GA, pas aux anciennes versions GA.

Les préversions ne doivent pas être déployées pour des utilisateurs finaux sur les réseaux de production. Utilisez plutôt la dernière préversion pour tester les nouvelles fonctionnalités ou les correctifs à paraître dans la prochaine version GA. Les préversions qui ne sont pas actuelles ne sont pas prises en charge.

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>Versions de la disponibilité générale qui ne sont plus prises en charge :

|Version du client|Date de publication|
|--------------|-------------|
|1.48.204.0|04/16/2019|
|1.41.51.0|27/11/2018|
|1.37.19.0|17/09/2018|
|1.29.5.0|26/06/2018|
|1.27.48.0|30/05/2018|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

Le format de date utilisé sur cette page est *mois/jour/année*.

À compter du 6/2/2019, le service d’étiquetage pour Azure Information Protection nécessite des connexions qui utilisent TLS 1,2.

Toutes les versions du client de 1.4.21.0 publiées 03/15/2017 prennent en charge TLS 1,2. Les versions clientes **1.3.155.2**, **1.2.4.0**et **1.1.23.0** n’utilisent pas TLS 1,2 et ne peuvent donc plus télécharger la stratégie de Azure information protection.

### <a name="release-history"></a>Historique des versions

Utilisez les informations suivantes pour découvrir les nouveautés et les changements d’une version prise en charge du client Azure Information Protection pour Windows. La dernière version est la première sur la liste.

> [!NOTE]
> Les correctifs mineurs ne sont pas listés. Par conséquent, si vous rencontrez un problème avec le client Azure Information Protection, nous vous recommandons de vérifier s’il n’est pas résolu dans la toute dernière version GA. Si le problème persiste, vérifiez la version préliminaire actuelle (si disponible).
>  
> Pour le support technique, consultez les informations dans [Options de support technique et ressources de la communauté](../information-support.md#support-options-and-community-resources). Nous vous invitons également à contacter l’équipe Azure Information Protection sur son [site Yammer](https://www.yammer.com/askipteam/).

## <a name="version-154590"></a>Version 1.54.59.0

**Publication**: 12/02/2020

Cette version comprend uniquement des correctifs. 

**Correctifs** :

- Problème dans lequel les fichiers protégés par IQP affichent les options de **récupération** et/ou d' **enregistrement sous** après la suppression de la protection, sont résolus. 

- De nombreux textes d’info-bulles de fonctionnalités de produit ont été améliorés pour plus de clarté et de compréhension. 

- Les problèmes de stabilité du client lors de l’utilisation de fichiers PDF protégés sont résolus. 

- Les étiquettes de protection sont maintenant supprimées comme prévu si l’étiquette est supprimée de l’e-mail pendant le processus de création de l’e-mail. 

## <a name="version-154330"></a>Version 1.54.33.0

**Publication**: 10/23/2019

Pris en charge jusqu’à 08/12/2020

Cette version comprend la version MSIPC 1.0.4008.0813 du client RMS.

Cette version propose des correctifs généraux pour la stabilité et les performances.

## <a name="version-153100"></a>Version 1.53.10.0

**Publication**: 07/15/2019

Pris en charge jusqu’à 04/23/2020

Cette version comprend la version MSIPC 1.0.3889.0419 du client RMS.

**Nouvelles fonctionnalités :**

- Nouveau paramètre de client avancé pour exempter les messages Outlook du paramètre de stratégie **tous les documents et e-mails doivent avoir une étiquette**. [Plus d’informations](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- Nouveau paramètre de client avancé pour personnaliser davantage les paramètres qui implémentent des messages contextuels dans Outlook qui avertissent, justifient ou bloquent les courriers électroniques envoyés. Avec ce nouveau paramètre avancé, vous pouvez définir une action différente pour les messages électroniques sans pièce jointe. [Plus d’informations](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**Correctifs** :

- Lorsque vous utilisez l’Explorateur de fichiers, cliquez avec le bouton droit pour étiqueter un fichier dont la protection est appliquée indépendamment d’une étiquette, cette protection est conservée. Par exemple, un utilisateur a appliqué des autorisations personnalisées à un fichier.

- Lorsque vous remplacez l’option ne pas transférer sur un thread de courrier électronique par une étiquette qui est configurée pour les autorisations définies par l’utilisateur et ne pas transférer, les destinataires d’origine peuvent toujours ouvrir le message électronique.

- Dans le scénario suivant, un utilisateur ne voit plus dans l’info-bulle de l’étiquette que l’étiquette a été automatiquement définie par lui : un utilisateur reçoit un e-mail protégé avec un document joint qui n’est pas étiqueté, mais qui est automatiquement protégé. Lorsque l’utilisateur de la même organisation que l’expéditeur ouvre le document, l’étiquette correspondante pour les paramètres de protection est appliquée au document.

- Le [droit d’utilisation](../configure-usage-rights.md#usage-rights-and-descriptions) minimal pour exécuter l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) est maintenant **Enregistrer sous, exporter** (exporter) au lieu de **copier** (extraire).

## <a name="next-steps"></a>Étapes suivantes :

Vous ne savez pas s’il s’agit du bon client à installer ?  Consultez [choisir le client d’étiquetage à utiliser pour les ordinateurs Windows](use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

Pour plus d’informations sur l’installation et l’utilisation du client : 

- Pour les utilisateurs : [Télécharger et installer le client](install-client-app.md)

- Pour les administrateurs : [Guide de l’administrateur du client Azure Information Protection](client-admin-guide.md)
