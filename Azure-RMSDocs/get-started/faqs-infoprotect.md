---
title: "FAQ sur la classification et l’étiquetage - AIP"
description: "Vous avez une question au sujet de l’utilisation d’Azure Information Protection pour la classification et l’étiquetage ? Vous trouverez peut-être une réponse ici."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 4332b37a3c89cb68d8e090e44666f2620d5b0064
ms.sourcegitcommit: fd3932ab19a00229b56efc3e301abaf9cff3f70b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2017
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Forum aux questions sur la classification et l’étiquetage dans Azure Information Protection

>*S’applique à : Azure Information Protection, Office 365*

Vous avez une question concernant Azure Information Protection qui porte spécifiquement sur la classification et l’étiquetage ?  Vous trouverez peut-être une réponse ici. 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Que puis-je faire avec les fonctionnalités de classification disponibles dans Azure Information Protection ?

Essayez notre didacticiel de démarrage rapide pour obtenir une démonstration en quelques minutes : [Didacticiel de démarrage rapide pour Azure Information Protection](infoprotect-quick-start-tutorial.md).

Pour être informé de la mise à disposition de fonctionnalités de classification supplémentaires, consultez les annonces publiées sur le [blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) et sur notre [site Yammer](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all). La version actuelle présente quelques limites, notamment :

- Les noms des étiquettes et des info-bulles sont pris en charge dans une seule langue uniquement. Cependant, la prise en charge multilingue est actuellement en préversion. Pour plus d’informations, consultez [Guide pratique pour configurer des étiquettes et des modèles dans différentes langues](../deploy-use/configure-policy-languages.md).

- Il n’existe aucun enregistrement centralisé pour la classification et l’étiquetage.

- L’étiquetage n’est pas pris en charge pour les applications Office pour appareils mobiles (iOS et Android) et les ordinateurs Mac, ni pour les applications web Office (Office Online).

- Aucune intégration de classification et d’étiquetage n’est assurée avec Exchange Online ou SharePoint Online.

Demandez de nouvelles fonctionnalités et votez pour les demandes en visitant le [site User Voice](https://msip.uservoice.com/) pour Azure Information Protection.

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>Dois-je être un administrateur global pour configurer la classification et les étiquettes ?

Pour configurer la stratégie Azure Information Protection, vous n’avez plus besoin de vous connecter au portail Azure en tant qu’administrateur général pour Azure Active Directory. Vous pouvez aussi maintenant utiliser un compte ayant un rôle d’administrateur de la sécurité.

Toutefois, si vous sélectionnez cette option pour installer la stratégie de démonstration au moment de l’installation du [client Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018), vous n’êtes pas obligé de vous connecter au portail pour voir et tester la fonctionnalité d’étiquetage. La stratégie de démonstration installe localement une stratégie par défaut pour Azure Information Protection. Vous pouvez donc essayer l’étiquetage des documents et des e-mails, mais vous ne pouvez pas modifier ni ajouter de nouvelles étiquettes sans vous connecter au portail Azure. 

## <a name="which-options-in-the-azure-portal-are-p2"></a>Quelles options dans le portail Azure sont des options P2 ?

Les options dans le portail Azure qui nécessitent un abonnement **Azure Information Protection Premium 2** (P2) comportent maintenant un message contextuel d’informations pour les identifier. Pour plus d’informations sur les fonctionnalités des abonnements P1 et P2, consultez la [liste des fonctionnalités](https://www.microsoft.com/cloud-platform/azure-information-protection-features) du site Azure Information Protection.

## <a name="can-a-file-have-more-than-one-classification"></a>Un fichier peut-il avoir plusieurs classifications ?

Les utilisateurs ne peuvent sélectionner qu’une seule étiquette à la fois pour chaque document ou e-mail, ce qui aboutit la plupart du temps à une classification unique pour chaque élément. Vous avez toutefois la possibilité d’appliquer une étiquette principale et une étiquette secondaire (ou sous-étiquette) à chaque document ou e-mail. Les étiquettes secondaires permettent d’attribuer à un fichier deux classifications ayant une relation parent\enfant afin d’obtenir un niveau de contrôle supplémentaire.

Par exemple, l’étiquette **Confidentiel** peut contenir des sous-étiquettes comme **Juridique** et **Finance**. Vous pouvez appliquer différents marquages de classification visuels et différents modèles Rights Management à ces sous-étiquettes. Un utilisateur ne peut pas sélectionner l’étiquette **Confidentiel** elle-même. Il peut seulement sélectionner une de ses sous-étiquettes, comme **Juridique**. L’étiquette qui s’affiche est donc **Confidentiel \ Juridique**. Les métadonnées de ce fichier incluent une propriété de texte personnalisée pour **Confidentiel**, une propriété de texte personnalisée pour **Juridique** et une autre qui contient les deux valeurs (**Confidentiel Juridique**). 

Lorsque vous utilisez des étiquettes secondaires, ne configurez pas de marquages visuels, de protection ou de conditions pour l’étiquette principale. Ces paramètres doivent uniquement être définis pour l’étiquette secondaire. Si vous configurez ces paramètres pour l’étiquette principale et l’étiquette secondaire, ce sont les paramètres de l’étiquette secondaire qui seront prioritaires.

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>Quand un e-mail est étiqueté, les pièces jointes reçoivent-elles automatiquement le même étiquetage ?

Non. Quand vous étiquetez un e-mail comportant des pièces jointes, ces dernières n’héritent pas de la même étiquette. Les pièces jointes peuvent rester sans étiquette ou conserver une étiquette appliquée séparément. Toutefois, si l’étiquette de l’e-mail applique une protection, cette protection est appliquée aux pièces jointes.

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>Comment faire pour intégrer les solutions DLP et autres applications avec Azure Information Protection ?

Azure Information Protection utilisant des métadonnées persistantes pour la classification, notamment une étiquette de texte en clair, ces informations peuvent être lues par les solutions DLP et d’autres applications. 

- Pour les documents Word (.doc et .docx), les feuilles de calcul Excel (.xls et .xlsx), les présentations PowerPoint (.ppt et .pptx) et les documents PDF (.pdf), ces métadonnées sont stockées dans la propriété personnalisée suivante : **MSIP_Label_\<GUID>_Enabled=True**  

- Dans les e-mails, ces informations sont stockées dans l’en-tête x- : **msip_labels: MSIP_Label_\<GUID>_Enabled=True;**  

Pour identifier le GUID d’une étiquette, recherchez la valeur de l’ID de l’étiquette dans le panneau Étiquette quand vous affichez ou configurez la stratégie Azure Information Protection dans le portail Azure. Pour les fichiers auxquels des étiquettes sont appliquées, vous pouvez également exécuter l’applet de commande PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) pour identifier le GUID (MainLabelId ou SubLabelId). Si une étiquette comprend des sous-étiquettes, spécifiez toujours le GUID de la sous-étiquette et non celui de l’étiquette parent.

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>En quoi la classification Azure Information Protection pour les e-mails est-elle différente de celle des messages Exchange ?

La classification des messages Exchange est une ancienne fonctionnalité permettant de classer des e-mails. Elle est mise en œuvre indépendamment de la classification Azure Information Protection. 

Toutefois, vous pouvez intégrer les deux solutions pour que, quand les utilisateurs classifient un e-mail à l’aide de la version web d’Outlook et de certaines applications de messagerie mobile, la classification Azure Information Protection et ses marquages d’étiquette correspondants soient automatiquement ajoutés. 

Vous pouvez utiliser cette même technique pour utiliser vos étiquettes avec Outlook sur le web et les applications de messagerie mobile.

Pour les étapes de configuration, consultez [Intégration de la classification des messages Exchange avec Azure Information Protection pour une solution d’étiquetage sur appareil mobile](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution). 



[!INCLUDE[Commenting house rules](../includes/houserules.md)]
