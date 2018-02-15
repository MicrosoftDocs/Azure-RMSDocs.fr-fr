---
title: "Configurer et gérer des modèles pour Azure Information Protection"
description: "Configurer et gérer des modèles de gestion des droits à partir du portail Azure."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 671d1d5d706225fcd5c680ddc8687aa889b59b59
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuration et gestion des modèles pour Azure Information Protection

>*S’applique à : Azure Information Protection*

>[!NOTE]
>Cette fonctionnalité remplace la configuration des modèles personnalisés dans le portail Azure Classic. Le portail Classic étant désormais hors service, vous devez utiliser le portail Azure. Pour un mappage de procédure rapide, consultez [Tâches que vous réalisiez avec le portail Azure Classic](migrate-portal.md).


Les modèles Rights Management sont désormais intégrés à la stratégie Azure Information Protection. 

**Quand vous avez un abonnement qui inclut la classification, l’étiquetage et la protection (Azure Information Protection P1 ou P2) :**

- Les modèles Rights Management qui ne sont pas intégrés avec vos étiquettes pour votre client sont affichés dans la section **Modèles de protection**, après les étiquettes dans le panneau **Azure Information Protection - Stratégie globale**. Vous pouvez convertir ces modèles en étiquettes, ou les lier à des étiquettes lorsque vous configurez la protection de vos étiquettes. 

**Quand vous avez un abonnement qui n’inclut que la protection uniquement (un abonnement Office 365 qui inclut le service Azure Rights Management) :**

- Les modèles Rights Management pour votre client sont affichés dans le panneau **Azure Information Protection - Stratégie globale**, dans la section **Modèles de protection**. Aucune étiquette n’apparaît. Vous pouvez également voir les paramètres de configuration qui sont spécifiques à la classification et à l’étiquetage, mais ces paramètres n’ont aucun effet sur vos modèles ou ne peuvent pas être configurés. 

## <a name="default-templates"></a>Modèles par défaut

Lorsque vous obtenez votre abonnement pour Azure Information Protection ou un abonnement Office 365 qui inclut le service Azure Rights Management, deux modèles par défaut sont créés automatiquement pour votre client. Ces modèles restreignent l’accès aux utilisateurs autorisés de votre organisation. Lorsque ces modèles sont créés, ils ont les autorisations répertoriées dans la documentation [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md#rights-included-in-the-default-templates).

En outre, les modèles sont configurés pour autoriser l’accès hors connexion pendant sept jours et n’ont pas de date d’expiration.

>[!NOTE]
> Vous pouvez modifier ces paramètres, ainsi que les noms et descriptions des modèles par défaut. Cette possibilité n’était pas possible avec le portail Azure Classic et n’est toujours pas prise en charge pour PowerShell.

Ces modèles par défaut vous permettent, à vous et pour d’autres, de lancer immédiatement la protection des données sensibles de votre organisation. Ces modèles peuvent être utilisés avec les étiquettes d’Azure Information Protection, ou séparément avec des [applications et services](../understand-explore/applications-support.md) qui utilisent des modèles Rights Management.

Vous pouvez également créer vos propres modèles. Même si vous n’avez probablement besoin que de quelques modèles seulement, vous pouvez enregistrer jusqu’à un maximum de 500 modèles personnalisés dans Azure.

### <a name="default-template-names"></a>Noms des modèles par défaut

Si vous avez obtenu votre abonnement récemment, vos modèles par défaut sont créés avec les noms suivants :

- **Confidentiel \ Tous les employés** qui accorde des autorisations pour lire et modifier le contenu protégé.

- **Hautement confidentiel \ Tous les employés** qui accorde des autorisations en lecture seule pour le contenu protégé.

Si vous avez obtenu votre abonnement il y a quelque temps, vos modèles par défaut sont créés avec les noms suivants :

- **\<nom de l’organisation> - Confidentiel** qui accorde des autorisations pour lire et modifier le contenu protégé.

- **\<nom de l’organisation> - Affichage confidentiel uniquement** qui accorde des autorisations en lecture seule pour le contenu protégé. 

Vous pouvez renommer (et reconfigurer) ces modèles par défaut lorsque vous utilisez le portail Azure.

>[!NOTE]
>Si vous ne voyez pas vos modèles par défaut dans le panneau **Azure Information Protection - Stratégie globale**, c’est qu’ils sont convertis en étiquettes, ou liés à une étiquette. Ils existent toujours en tant que modèles, mais dans le portail Azure, vous les voyez dans le cadre d’une configuration d’étiquette qui inclut la protection Azure RMS. Vous pouvez toujours confirmer quels modèles votre client possède, en exécutant [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) à partir du [module AADRM PowerShell](administer-powershell.md).
>
>Vous pouvez convertir manuellement des modèles, comme expliqué dans la section ultérieure [Pour convertir des modèles en étiquettes](#to-convert-templates-to-labels), puis les renommer si vous le souhaitez. Ou bien ils sont convertis automatiquement pour vous si votre stratégie Azure Information Protection par défaut a été créée récemment et que le service Azure Rights Management pour votre client était activé à ce moment-là.

Les modèles archivés s’affichent comme étant indisponibles dans le panneau **Azure Information Protection - Stratégie globale**. Ces modèles ne peuvent pas être sélectionnés pour des étiquettes, mais ils peuvent être convertis en étiquettes.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Éléments à prendre en considération pour les modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes, assurez-vous que vous avez pris connaissance des éléments à prendre en considération et modifications suivantes. En raison de modifications d’implémentation, la liste suivante est particulièrement importante si vous gériez auparavant vos modèles dans le portail Azure Classic.

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) originaux. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels en utilisant le portail Azure. Ou, utilisez PowerShell avec les applets de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Autoriser les macros** (nom commun) est ajouté automatiquement. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.

- Les paramètres**Publié** et **Archivé** s’affichent comme étant **Activé** : **Oui** et **Activé** : **Non** respectivement sur le panneau **Étiquette**. Pour les modèles que vous souhaitez conserver, mais ne pas rendre visible aux utilisateurs ou services, définissez ces modèles sur **Activé** : **Non**.

- Vous ne pouvez pas copier ou supprimer un modèle dans le portail Azure. Lorsque le modèle est converti en étiquette, vous pouvez configurer l’étiquette pour qu’elle cesse d’utiliser le modèle en sélectionnant **Non configuré** pour l’option **Définir des autorisations pour les documents et e-mails contenant cette étiquette**. Ou, vous pouvez supprimer l’étiquette. Toutefois, dans les deux cas, le modèle n’est pas supprimé et demeure à l’état archivé.
    
    Vous pouvez maintenant supprimer le modèle à l’aide de l’applet de commande [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) de PowerShell. Vous pouvez également utiliser cette applet de commande PowerShell pour les modèles qui ne sont pas convertis en étiquettes. Toutefois, si vous supprimez un modèle qui a été utilisé pour protéger du contenu, ce contenu ne peut plus être ouvert. Ne supprimez des modèles que si vous êtes sûr qu’ils n’ont pas été utilisés pour protéger des documents ou des e-mails en production. Par précaution, vous devriez d’abord envisager d’exporter le modèle en tant que sauvegarde, à l’aide de l’applet de commande [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). 

- Les modèles de service (les modèles qui sont configurés pour une étendue) s’affichent dans la stratégie globale. Actuellement, si vous modifiez et enregistrez un modèle de service, cela supprime la configuration d’étendue. L’équivalent d’un modèle étendu dans la stratégie Azure Information Protection est une [stratégie étendue](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    En outre, vous ne pouvez pas actuellement définir le paramètre de compatibilité des applications pour un modèle de service. Si nécessaire, vous pouvez définir le paramètre de compatibilité des applications à l’aide de l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) et du paramètre *EnableInLegacyApps*.

- Quand vous convertissez ou liez un modèle à une étiquette, il ne peut plus être utilisé par d’autres étiquettes. En outre, ce modèle ne s’affiche plus dans la section **Modèles de protection**. 

- Ne créez pas de nouveau modèle à partir de la section **Modèles de protection**. Au lieu de cela, créez une étiquette qui possède le paramètre **Protéger**, et configurez les droits d’utilisation ainsi que les paramètres à partir du panneau **Protection**. Pour obtenir des instructions complètes, consultez [Créer un nouveau modèle](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Configurer les modèles dans la stratégie Azure Information Protection

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**.     
    
    Par exemple, dans le menu hub, cliquez sur **Autres services** et commencez à écrire **Informations** dans la zone de filtre. Sélectionnez **Azure Information Protection**.

2. Si le modèle que vous souhaitez configurer est pour tous les utilisateurs, restez sur le panneau **Azure Information Protection - Stratégie globale**.
    
    Si le modèle que vous souhaitez configurer se trouve dans une [stratégie étendue](configure-policy-scope.md), et afin qu’il s’applique uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez d’abord **Stratégies étendues**. Sélectionnez ensuite votre stratégie étendue à partir du panneau **Azure Information Protection - Stratégies étendues**.

3. Sur le panneau **Azure Information Protection - Stratégie globale**, ou sur le panneau **Stratégie:\<nom>**, cherchez le modèle que vous souhaitez configurer :
    
    - Quand vous avez un abonnement qui inclut la classification, l’étiquetage et la protection : étendez **Modèles de protection** après vos étiquettes.
    
    - Quand vous avez un abonnement qui n’inclut que la protection, les modèles s’affichent en tant qu’étiquettes.

4. Sélectionnez le modèle, puis, dans le panneau **Étiquette**, vous pouvez modifier le nom et la description du modèle si nécessaire, en modifiant les **Nom d’affichage de l’étiquette** et **Description**. Ensuite, sélectionnez **Protection** qui a une valeur **Azure (clé cloud)**, pour ouvrir le panneau **Protection**.

5. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu, ainsi que les paramètres d’accès hors connexion. Pour plus d’informations sur la configuration des paramètres de protection, consultez [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

6. Pour rendre vos modifications disponibles aux services et applications des utilisateurs, sur le panneau initial **Azure Information Protection**, cliquez sur **Publier**.

> [!NOTE]
> Vous pouvez également modifier un modèle à l’aide du bouton **Modifier le modèle** sur le panneau **Protection** si vous avez configuré une étiquette pour utiliser un modèle prédéfini. À condition qu’aucune autre étiquette n’utilise également le modèle sélectionné, ce bouton convertit le modèle en étiquette et vous amène à l’étape 5. Pour plus d’informations sur ce qui se passe lorsque des modèles sont convertis en étiquettes, consultez la section suivante.

## <a name="to-convert-templates-to-labels"></a>Pour convertir des modèles en étiquettes

Quand vous avez un abonnement qui inclut la classification, l’étiquetage et la protection, vous pouvez convertir un modèle en étiquette. Lorsque vous convertissez un modèle, le modèle d’origine est conservé, mais dans le portail Azure, il s’affiche désormais comme étant inclus dans une nouvelle étiquette.

Par exemple, si vous convertissez un modèle nommé **Marketing** qui accorde des droits d’utilisation au groupe marketing, dans le portail Azure il s’affiche désormais comme une étiquette nommée **Marketing** qui a les mêmes paramètres de protection. Si vous modifiez les paramètres de protection de cette nouvelle étiquette, vous les modifiez dans le modèle et n’importe quel utilisateur ou un service qui utilise ce modèle obtiendra les nouveaux paramètres de protection avec la prochaine actualisation de ce modèle. 

Il n’est pas nécessaire de convertir tous vos modèles en étiquettes, mais lorsque vous le faites, les paramètres de protection sont totalement intégrés à l’ensemble des fonctionnalités des étiquettes, afin que vous n’ayez pas à mettre à jour les paramètres séparément.

Pour convertir un modèle en étiquette, cliquez avec le bouton droit sur le modèle, puis sélectionnez **Convertir en étiquette**. Vous pouvez également utiliser le menu contextuel pour sélectionner cette option. 

Vous pouvez également convertir un modèle en étiquette lorsque vous configurez une étiquette pour la protection et un modèle prédéfini, à l’aide du bouton **Modifier le modèle**. 

Lorsque vous convertissez un modèle en étiquette :

- Le nom du modèle est converti en un nouveau nom d’étiquette, et la description du modèle est convertie en info-bulle de l’étiquette. 

- Si l’état du modèle a été publié, ce paramètre est mappé sur **Activé**: **Oui** pour l’étiquette, qui s’affiche à présent en tant que cette étiquette aux utilisateurs lorsque vous publiez ensuite la stratégie Azure Information Protection. Si l’état du modèle a été archivé, ce paramètre est mappé sur **Activé**: **Non** pour l’étiquette et ne s’affiche pas comme étant une étiquette disponible aux utilisateurs.

- Les paramètres de protection sont conservés, et vous pouvez les modifier si nécessaire, mais également ajouter d’autres paramètres d’étiquette tels que les marqueurs visuels et des conditions.

- Le modèle d’origine n’apparaît plus dans les **modèles de protection** et ne peut pas être sélectionné comme modèle prédéfini lorsque vous configurez la protection pour une étiquette. Pour modifier ce modèle dans le portail Azure, vous devez à présent modifier l’étiquette qui a été créée lors de la conversion du modèle. Le modèle reste disponible pour le service Azure Rights Management et peut toujours être géré à l’aide des [commandes PowerShell](administer-powershell.md).  

## <a name="to-create-a-new-template"></a>Créer un nouveau modèle

Lorsque vous créez une nouvelle étiquette avec le paramètre de protection de **Azure RMS** ou **Azure (clé cloud)**, cette action crée en arrière-plan un nouveau modèle personnalisé qui est ensuite accessible par les services et applications qui s’intègrent aux modèles Rights Management.

1. Si le nouveau modèle est pour tous les utilisateurs, restez sur le panneau **Azure Information Protection - Stratégie globale**.
    
     Si le nouveau modèle est un modèle de service, et afin qu’il s’applique uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez d’abord **Stratégies étendues**. Créez ou sélectionnez ensuite votre [stratégie étendue](configure-policy-scope.md) à partir du panneau **Azure Information Protection - Stratégies étendues**.

2. Sur le panneau **Azure Information Protection - Stratégie globale**, ou sur le panneau **Stratégie:\<nom>**, cliquez sur **Ajouter une nouvelle étiquette**.

3. Sur le panneau **Étiquette**, conservez la valeur par défaut sur **Activé**: **Oui** pour publier ce nouveau modèle, ou changez le paramètre sur **Non** pour créer le modèle en tant qu’archivé. Puis entrez un nom d’étiquette et une description pour le nom et la description du modèle.

4. Pour **Définir les autorisations pour les documents et e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis sélectionnez **Protection** :
    
     ![Configurer la protection pour une étiquette Azure Information Protection](../media/info-protect-protection-bar-configured.png)

5. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu, ainsi que les paramètres d’accès hors connexion. Pour plus d’informations sur la configuration de ces paramètres de protection, consultez [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md).
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

6. Pour rendre vos modèles disponibles aux services et applications des utilisateurs, sur le panneau initial **Azure Information Protection**, cliquez sur **Publier**.


## <a name="next-steps"></a>Étapes suivantes

Comme pour toutes les modifications apportées à la stratégie Azure Information Protection, un ordinateur qui exécute le client Azure Information Protection peut prendre jusqu’à 15 minutes pour terminer le téléchargement de ces modèles. Pour plus d’informations sur la manière dont les ordinateurs et les services téléchargent et actualisent les modèles, consultez [Actualisation des modèles pour les utilisateurs et les services](refresh-templates.md).

Tout ce que vous pouvez configurer dans le portail Azure pour créer et gérer vos modèles, vous pouvez le faire à l’aide de PowerShell. En outre, PowerShell fournit davantage d’options qui ne sont pas disponibles dans le portail. Pour plus d’informations, consultez [Référence PowerShell pour les modèles de protection](configure-templates-with-powershell.md). 

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
