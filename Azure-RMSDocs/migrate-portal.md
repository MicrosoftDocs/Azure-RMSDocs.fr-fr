---
title: Migration à partir du portail Azure Classic - AIP
description: Récapitulatif des tâches d’administration dans le portail Azure que vous aviez l’habitude d’effectuer dans le portail Azure Classic
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ROBOTS: NOINDEX
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a2e2bcc505155188d41574fbc1d67fc4d3d09866
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806122"
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Tâches que vous aviez l’habitude d’effectuer dans le portail Azure Classic

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) dans la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>

Jusqu’à présent, vous utilisiez le portail Azure Classic pour gérer le service Azure Rights Management et vous avez besoin d’aide pour passer au portail Azure ?

Le portail Azure Classic a été mis hors service le **8 janvier 2018**. Après cette date, vous n’êtes plus en mesure de gérer le service Azure Rights Management et les modèles personnalisés du portail Classic. Si vous essayez d’accéder au portail Classic, vous voyez un lien qui vous redirige vers le nouveau portail Azure.

Pour plus d’informations sur le retrait du portail Classic, consultez le billet de blog [Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/) faisant suite à cette annonce. Pour plus d’informations sur la prolongation temporaire jusqu’à la date de mise hors service d’origine, consultez [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/).

## <a name="how-to-do-your-familiar-admin-tasks"></a>Comment effectuer les tâches d’administration courantes

Utilisez les informations suivantes pour vous aider à passer rapidement au portail actuel.

|Portail Azure Classic|Comment effectuer cette tâche dans le portail Azure
|-----------|--------------------|
|Accéder aux paramètres de configuration pour la première fois|1. [Connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal).<br /><br />2. Suivez les instructions pour [accéder au volet de Azure information protection pour la première fois](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time).
|Créer un modèle|Créez une étiquette qui applique une protection et utilisez **Définir des autorisations** pour définir les autorisations, l’expiration et l’accès hors connexion. <br /><br />En pratique, cette configuration crée un modèle personnalisé qui est ensuite accessible aux services et aux applications intégrés aux modèles Rights Management.<br /><br />Pour plus d’informations, consultez [Créer un modèle](configure-policy-templates.md#to-create-a-new-template).
|Modifiez les propriétés du modèle : <br /><br />- Nom et description du modèle<br /><br />- Droits d’utilisation, expiration du contenu et paramètres d’accès hors connexion|Si vous ne l’avez pas encore fait, [convertissez le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels), puis effectuez les étapes suivantes :<br /><br />1. modifier le nom et la description de l’étiquette<br /><br />2. modifiez les paramètres de protection sur l’étiquette pour mettre à jour les autorisations, l’expiration et les paramètres d’accès hors connexion.<br /><br />Pour en savoir plus, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|Archiver un modèle|Affectez à l’étiquette l’état **Désactivé**.
|Créer un modèle délimité|Créez une stratégie délimitée, puis créez une étiquette dans cette étendue qui applique une protection. <br /><br />Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md).
|Copier un modèle|Vous ne pouvez pas copier un modèle dans le portail Azure. Pour que deux étiquettes aient les mêmes paramètres de protection, vous devez définir les autorisations sur chaque étiquette. <br /><br />Pour en savoir plus, consultez [Configurer une étiquette pour les paramètres de protection](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|suppression d'un modèle|Le portail Azure ne prend pas en charge la suppression de modèles, car cette action peut rendre les données inaccessibles. Toutefois, vous pouvez supprimer l’étiquette, puis utiliser l’applet de commande PowerShell [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) pour supprimer le modèle. <br /><br />Pour plus d’informations, consultez [Guide pratique pour supprimer ou réorganiser une étiquette pour Azure Information Protection](configure-policy-delete-reorder.md).
|Prise en charge multi-langage|Dans la sélection de menu **Gérer**, sélectionnez **Langues** pour exporter les champs personnalisables qui incluent le nom et la description du modèle. Traduisez les chaînes, puis importez-les dans le portail. <br /><br />Pour plus d’informations, consultez [Guide pratique pour configurer des étiquettes et des modèles pour différentes langues dans Azure Information Protection](configure-policy-languages.md).
|Rapports web Rights Management|La fonctionnalité de [création de rapports centralisés pour Azure Information Protection](reports-aip.md) est actuellement en préversion.<br /><br />Vous pouvez également utiliser l’applet de commande PowerShell [-AipServiceUsageLog](/powershell/module/aipservice/get-aipserviceuserlog) pour télécharger les journaux d’utilisation du service Azure Rights Management. Vous pouvez ensuite utiliser ces données pour créer des rapports personnalisés. Pour plus d’informations, consultez [journalisation et analyse de l’utilisation de la protection à partir de Azure information protection](log-analyze-usage.md).
|Activer et désactiver le service Rights Management|Dans les options du menu **Gérer**, sélectionnez **Activation de la protection**.<br /><br />Pour plus d’informations, voir [How to Activate the Rights Management protection service from the portail Azure](activate-azure.md).

Avant de modifier vos modèles ou de les convertir en étiquettes dans le portail Azure, consultez [Considérations relatives aux modèles dans le portail Azure](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal).


## <a name="what-else-has-changed"></a>Autres changements

Nouvelles fonctionnalités dans le portail Azure :

- Vous pouvez modifier les [modèles par défaut](configure-policy-templates.md#default-templates) qui sont créés automatiquement pour votre organisation.

- Au lieu de gérer un modèle et une étiquette séparément, la conversion de modèles en étiquettes vous permet de gérer un seul objet. Pour obtenir des instructions, consultez [Convertir des modèles en étiquettes](configure-policy-templates.md#to-convert-templates-to-labels).

- Prise en charge d’autres rôles d’administrateur : alors que vous deviez vous connecter au portail Azure Classic en tant qu’administrateur général pour configurer Azure Rights Management, vous pouvez vous connecter au Portail Azure pour gérer les Azure Information Protection à l’aide de nombreux autres rôles d’administration qui incluent l’administrateur de **conformité** et l' **administrateur des données de conformité**. La liste complète des rôles pris en charge est incluse dans la section [connexion au portail Azure](configure-policy.md#signing-in-to-the-azure-portal) .

Les applets de commande PowerShell utilisées pour créer et gérer des modèles et pour activer ou désactiver le service restent inchangées.

## <a name="see-also"></a>Voir aussi
Pour plus d’informations, consultez [Configuration et gestion des modèles dans la stratégie Azure Information Protection](configure-policy-templates.md).

