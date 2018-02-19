---
title: "Migration à partir du portail Azure Classic - AIP"
description: "Récapitulatif des tâches d’administration dans le portail Azure que vous aviez l’habitude d’effectuer dans le portail Azure Classic"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/13/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 5f160d766abb4a81864ac1ff466362b8ae24027d
ms.sourcegitcommit: c157636577db2e2a2ba5df81eb985800cdb82054
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2018
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Tâches que vous aviez l’habitude d’effectuer dans le portail Azure Classic

>*S’applique à : Azure Information Protection, Office 365*

Jusqu’à présent, vous utilisiez le portail Azure Classic pour gérer le service Azure Rights Management et vous avez besoin d’aide pour passer au portail Azure ?

Le portail Azure Classic a été mis hors service le **8 janvier 2018**. Après cette date, vous n’êtes plus en mesure de gérer le service Azure Rights Management et les modèles personnalisés du portail Classic. Si vous essayez d’accéder au portail Classic, vous voyez un lien qui vous redirige vers le nouveau portail Azure.

Pour plus d’informations sur le retrait du portail Classic, consultez le billet de blog [Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/) faisant suite à cette annonce. Pour plus d’informations sur la prolongation temporaire jusqu’à la date de mise hors service d’origine, consultez [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/).

## <a name="how-to-do-your-familiar-admin-tasks"></a>Comment effectuer les tâches d’administration courantes

Utilisez les informations suivantes pour vous aider à passer rapidement au portail actuel.

Toutefois, les clients qui ont un abonnement pour Office 365 US Government (Government Community Cloud) ne peuvent pas utiliser le portail Azure et doivent utiliser [PowerShell](configure-templates-with-powershell.md) à la place pour gérer leurs modèles.


|Portail Azure Classic|Comment effectuer cette tâche dans le portail Azure
|-----------|--------------------|
|Accéder aux paramètres de configuration pour la première fois|1. [Connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal).<br /><br />2. Dans le menu Hub, cliquez sur **Nouveau**, puis, dans la liste **MARKETPLACE**, sélectionnez **Sécurité + Identité**.<br /><br />3. Dans le panneau **Sécurité + Identité**, dans la liste **APPLICATIONS PROPOSÉES**, sélectionnez **Azure Information Protection**. Ensuite, dans le panneau **Azure Information Protection**, cliquez sur **Créer**.<br /><br />Cette action crée le panneau **Azure Information Protection**. De cette façon, vous pouvez sélectionner le service dans la liste **Autres services** du hub lors de votre prochaine connexion au portail.
|Créer un modèle|Créez une étiquette qui applique une protection et utilisez **Définir des autorisations** pour définir les autorisations, l’expiration et l’accès hors connexion. <br /><br />En pratique, cette configuration crée un modèle personnalisé qui est ensuite accessible aux services et aux applications intégrés aux modèles Rights Management.<br /><br />Pour plus d’informations, consultez [Créer un modèle](configure-policy-templates.md#to-create-a-new-template).
|Modifiez les propriétés du modèle : <br /><br />- Nom et description du modèle<br /><br />- Droits d’utilisation, expiration du contenu et paramètres d’accès hors connexion|Si vous ne l’avez pas encore fait, [convertissez le modèle en étiquette](configure-policy-templates.md#to-convert-templates-to-labels), puis effectuez les étapes suivantes :<br /><br />1. Changez le nom et la description de l’étiquette.<br /><br />2. Changez les paramètres de protection sur l’étiquette pour mettre à jour les autorisations, l’expiration et les paramètres d’accès hors connexion.<br /><br />Pour en savoir plus, consultez [Configurer une étiquette pour la protection Rights Management](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection).
|Archiver un modèle|Affectez à l’étiquette l’état **Désactivé**.
|Créer un modèle délimité|Créez une stratégie délimitée, puis créez une étiquette dans cette étendue qui applique une protection. <br /><br />Pour plus d’informations, consultez [Guide pratique pour configurer la stratégie Azure Information Protection pour des utilisateurs spécifiques avec des stratégies délimitées](configure-policy-scope.md).
|Copier un modèle|Vous ne pouvez pas copier un modèle dans le portail Azure. Pour que deux étiquettes aient les mêmes paramètres de protection, vous devez définir les autorisations sur chaque étiquette. <br /><br />Pour en savoir plus, consultez [Configurer une étiquette pour la protection Rights Management](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection).
|suppression d'un modèle|Le portail Azure ne prend pas en charge la suppression de modèles, car cette action peut rendre les données inaccessibles. Vous pouvez toutefois supprimer l’étiquette, puis utiliser l’applet de commande PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) pour supprimer le modèle. <br /><br />Pour plus d’informations, consultez [Guide pratique pour supprimer ou réorganiser une étiquette pour Azure Information Protection](configure-policy-delete-reorder.md).
|Prise en charge multilingue|Dans le menu **GÉRER**, sélectionnez **Langues** pour exporter les champs personnalisables qui incluent le nom et la description du modèle. Traduisez les chaînes, puis importez-les dans le portail. <br /><br />Pour plus d’informations, consultez [Guide pratique pour configurer des étiquettes et des modèles pour différentes langues dans Azure Information Protection](configure-policy-languages.md).
|Rapports web Rights Management|Utilisez l’applet de commande PowerShell [Get-AadrmUsageLog](/powershell/module/aadrm/Get-AadrmUsageLog) pour télécharger les journaux d’utilisation du service Azure Rights Management. Vous pouvez ensuite utiliser ces données pour créer des rapports personnalisés. <br /><br />Pour plus d’informations, consultez [Journalisation et analyse de l’utilisation du service Azure Rights Management](log-analyze-usage.md).<br /><br />Conseil : Consultez le [blog Enterprise Mobility and Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection) où seront postées des annonces sur la nouvelle solution de création de rapports centralisée pour Azure Information Protection.
|Activer et désactiver le service Rights Management|Dans les options du menu **GÉRER**, sélectionnez **Paramètres RMS** ou **Activation de la protection**. Le nom de cette option est en cours de modification.<br /><br />Pour plus d’informations, consultez [Comment activer Azure Rights Management à partir du portail Azure](activate-azure.md).

Avant de modifier vos modèles ou de les convertir en étiquettes dans le portail Azure, consultez [Considérations relatives aux modèles dans le portail Azure](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal).


## <a name="what-else-has-changed"></a>Autres changements

Nouvelles fonctionnalités dans le portail Azure :

- Vous pouvez modifier les [modèles par défaut](configure-policy-templates.md#default-templates) qui sont créés automatiquement pour votre organisation.

- Au lieu de gérer un modèle et une étiquette séparément, la conversion de modèles en étiquettes vous permet de gérer un seul objet. Pour obtenir des instructions, consultez [Convertir des modèles en étiquettes](configure-policy-templates.md#to-convert-templates-to-labels).

- Prise en charge d’autres rôles d’administrateur : Dans le portail Azure Classic, vous deviez vous connecter comme Administrateur général pour configurer Azure Rights Management. Pour configurer Azure Information Protection dans le portail Azure, vous pouvez vous connecter à l’aide d’un compte ayant l’un des rôles d’administration suivants : Administrateur général, Administrateur de sécurité ou Administrateur Information Protection. Pour plus d’informations sur chacun de ces rôles, consultez la section [Rôles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) dans la documentation d’Azure Active Directory.

Les applets de commande PowerShell utilisées pour créer et gérer des modèles et pour activer ou désactiver le service restent inchangées.

## <a name="see-also"></a>Voir aussi
Pour plus d’informations, consultez [Configuration et gestion des modèles dans la stratégie Azure Information Protection](../deploy-use/configure-policy-templates.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
