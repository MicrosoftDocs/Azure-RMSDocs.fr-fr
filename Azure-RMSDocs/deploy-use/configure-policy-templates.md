---
title: "Configurer et gérer les modèles dans la stratégie Azure Information Protection"
description: "Actuellement en version préliminaire : vous pouvez désormais configurer et gérer des modèles de gestion des droits à partir de la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 1f41aad2d132e087e9122b2683be4b45185527de
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="configuring-and-managing-templates-in-the-azure-information-protection-policy"></a>Configuration et gestion des modèles dans la stratégie Azure Information Protection

>*S’applique à : Azure Information Protection*

>[!NOTE]
>Cette fonctionnalité est actuellement en version préliminaire et susceptible d’être modifiée fréquemment.
>
>Avant de tester cette fonctionnalité en version préliminaire avec des modèles personnalisés que vous avez créés dans le portail Azure Classic, déterminez si vous disposez d’une sauvegarde récente de vos modèles. Vous pouvez sauvegarder vos modèles personnalisés à l’aide de l’applet de commande PowerShell [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). Vous pouvez, si nécessaire, utiliser [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) pour les restaurer.
>
>En raison de différences dans l’implémentation, nous vous déconseillons de gérer les mêmes modèles à partir du portail Azure Classic et du portail Azure.


Les modèles de gestion des droits sont désormais intégrés à la stratégie Azure Information Protection. 

**Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection (Azure Information Protection P1 or P2) :**

- Les modèles de gestion des droits pour votre client sont affichés dans la nouvelle section **Modèles** après les étiquettes. Vous pouvez convertir ces modèles en étiquettes, ou vous pouvez continuer à les gérer en tant que modèles distincts et les lier lorsque vous configurez la protection pour vos étiquettes. 

**Lorsque vous avez un abonnement qui inclut uniquement la protection (un abonnement Office 365 qui inclut le service Azure Rights Management) :**

- Les modèles de gestion des droits pour votre client sont affichés en tant qu’étiquettes et, actuellement, les paramètres de configuration qui sont spécifiques à la classification et à l’étiquetage sont également disponibles. 


## <a name="considerations-for-templates-in-the-azure-portal"></a>Considérations relatives aux modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes dans le portail Azure, tenez compte des modifications suivantes dans l’implémentation de la gestion des modèles dans le portail Azure Classic. Certaines limitations devraient être traitées lors de la période préliminaire :

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) d’origine. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels à l’aide de PowerShell avec les applets de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Enregistrer sous, Exporter** (nom commun) est supprimé. Dans le portail Azure, vous ne pouvez pas spécifier manuellement ce droit d’utilisation, mais il est inclus avec le droit d’utilisation Contrôle total, que vous pouvez ajouter si nécessaire.
    
    - **Autoriser les macros** (nom commun) est automatiquement ajouté. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.
    
- Actuellement, les modèles par défaut sont affichés mais ne peuvent pas être modifiés ou convertis. 

- Impossible de copier ou supprimer un modèle. Pour supprimer un modèle, utilisez l’applet de commande PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate). 

- Actuellement, les modèles qui ont été configurés pour les langues à l’aide du portail Azure Classic ou de PowerShell n’affichent pas ces langues pour le nom et la description, mais ils sont conservés.

- Les paramètres **Publié** et **Archivé** sous la forme **Activé** : **Oui** et **Activé** : **Non** respectivement sur le panneau **Étiquette**.

- Les modèles de service (les modèles qui sont configurés pour une étendue) s’affichent dans la stratégie globale. Actuellement, si vous modifiez et enregistrez un modèle de service, il supprime la configuration d’étendue. L’équivalent d’un modèle délimité dans la stratégie Azure Information Protection est une [stratégie délimitée](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    En outre, vous ne pouvez actuellement pas définir le paramètre de compatibilité d’application pour un modèle de service. Si nécessaire, vous pouvez définir cela à l’aide de PowerShell avec l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

- Vous ne créez pas un nouveau modèle à partir du conteneur **Modèles** ; au lieu de cela, créez une étiquette qui a le paramètre **Protéger** et configurez les droits d’utilisation et les paramètres à partir du panneau **Protection**. Pour obtenir des instructions, consultez [Pour créer un nouveau modèle](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Pour configurer les modèles dans la stratégie Azure Information Protection

1. Dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général.

2. Accédez au panneau **Azure Information Protection**: par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information Protection** dans la zone Filtrer. Dans les résultats, sélectionnez **Azure Information Protection**. 

2. Si le modèle à configurer s’applique à tous les utilisateurs, sélectionnez **Global** dans le panneau **Azure Information Protection**. Par contre, si le modèle à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, choisissez plutôt la stratégie délimitée en question.

3. Dans le panneau de la stratégie, recherchez le modèle que vous souhaitez configurer :
    
    - Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection : développez **Modèles** après vos étiquettes.
    
    - Lorsque vous avez un abonnement qui inclut uniquement la protection : les modèles s’affichent sous forme d’étiquettes.

4. Sélectionnez le modèle, puis, dans le panneau **Étiquette**, vous pouvez modifier le nom du modèle et la description si nécessaire, en modifiant **Nom d’étiquette** et **Description**. Ensuite, sélectionnez **Protection**, qui a la valeur **Azure RMS**, pour ouvrir le panneau **Protection**.

5. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration des paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

6. Pour que les utilisateurs puissent voir les modifications apportées aux applications et services, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="to-convert-templates-to-labels"></a>Pour convertir des modèles en étiquettes

Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection, vous pouvez convertir des modèles en étiquettes. Lorsque vous faites cela, le modèle d’origine est conservé, mais dans le portail Azure, il s’affiche désormais comme étant inclus dans une nouvelle étiquette.

Par exemple, si vous convertissez une étiquette nommée **Marketing** qui accorde des droits d’utilisation pour le groupe marketing dans le portail Azure il s’affiche maintenant comme une étiquette nommée **Marketing** qui a les mêmes paramètres de protection. Si vous modifiez les paramètres de protection de cette nouvelle étiquette, vous les changez dans le modèle et n’importe quel utilisateur ou service qui utilise ce modèle obtient les nouveaux paramètres de protection lors de la prochaine actualisation des modèles. 

Il n’est pas nécessaire de convertir tous vos modèles en étiquettes, mais lorsque vous le faites, les paramètres de protection sont totalement intégrés à l’ensemble des fonctionnalités des étiquettes afin que vous n’ayez pas à mettre à jour les paramètres séparément.

Pour convertir un modèle en étiquette, cliquez sur le modèle, puis sélectionnez **Convertir en étiquette**. Vous pouvez également utiliser le menu contextuel pour sélectionner cette option.

Lorsque vous convertissez un modèle en étiquette :

- Le nom du modèle est converti en un nouveau nom d’étiquette, et la description du modèle est convertie en info-bulle pour l’étiquette. 

- Si l’état du modèle a été publié, ce paramètre est mappé sur **Activé** : **Oui** pour l’étiquette, qui s’affiche désormais comme cette étiquette pour les utilisateurs lorsque vous publiez ensuite la stratégie Azure Information Protection. Si l’état du modèle a été archivé, ce paramètre est mappé sur **Activé** : **Non** pour l’étiquette et ne s’affiche pas comme une étiquette disponible pour les utilisateurs.

- Les paramètres de protection sont conservés, et vous pouvez les modifier si nécessaire, puis ajouter également d’autres paramètres à l’étiquette, comme des marqueurs visuels et des conditions.

- Le modèle d’origine n’est plus affiché sous **Modèles** et, pour le modifier dans le portail Azure, vous devez maintenant modifier l’étiquette qui a été créée. Le modèle reste disponible pour le service Azure Rights Management et peut toujours être géré à l’aide de [commandes PowerShell](administer-powershell.md).  

## <a name="to-create-a-new-template"></a>Pour créer un nouveau modèle

Lorsque vous créez une nouvelle étiquette avec le paramètre de protection de **Azure RMS**, en pratique, cela crée un nouveau modèle personnalisé qui est ensuite accessible pour les services et applications qui s’intègrent avec les modèles Rights Management.

1. Si le nouveau modèle à créer s’applique à tous les utilisateurs à partir du panneau **Stratégie : Globale**, cliquez sur **Ajouter une nouvelle étiquette**.
    
     Si le nouveau modèle à créer sera un modèle de service pour qu’il s’applique uniquement aux utilisateurs sélectionnés, commencez par sélectionner ou créer une stratégie délimitée à partir du panneau **Azure Information Protection** initial.

2. Dans le panneau **Étiquette**, conservez la valeur par défaut **Activé** : **Oui** pour publier ce nouveau modèle, ou modifiez ce paramètre sur **Non** pour créer le modèle comme étant archivé. Saisissez ensuite un nom d’étiquette et une description pour le nom du modèle et la description.

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis **Protection** :
    
     ![Configurer la protection d’une étiquette Azure Information Protection](../media/info-protect-protection-bar.png)

4. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration de ces paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.

5. Pour rendre ces modèles disponibles pour les applications et services de l’utilisateur, cliquez dans le panneau **Azure Information Protection** sur **Publier**.


## <a name="next-steps"></a>Étapes suivantes

Comme avec toutes les modifications apportées à la stratégie Azure Information Protection, il peut falloir jusqu'à 15 minutes pour qu’un ordinateur exécutant le client Azure Information Protection termine le téléchargement de ces modèles. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent les modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
