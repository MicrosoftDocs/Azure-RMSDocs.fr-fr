---
title: Configurer et gérer des modèles pour Azure Information Protection
description: Configurer et gérer des modèles Rights Management à partir du portail Azure.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9f3dc55f8443b4280cd5e108f1b5c5e3093748d4
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39490062"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuration et gestion des modèles pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

>[!NOTE]
>Cette fonctionnalité remplace la configuration de modèles personnalisés dans le portail Azure Classic. Le portail classique est maintenant hors service, vous devez utiliser le portail Azure. Pour trouver rapidement les fonctionnalités de remplacement, consultez [Tâches que vous aviez l’habitude d’effectuer avec le portail Azure Classic](migrate-portal.md).


Les modèles Rights Management sont désormais intégrés à la stratégie Azure Information Protection. 

**Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection (Azure Information Protection P1 or P2) :**

- Les modèles Rights Management qui ne sont pas intégrés aux étiquettes de votre locataire sont affichés à la section **Modèles de protection**, après vos étiquettes dans le panneau **Azure Information Protection - Étiquettes**. Pour accéder à ce panneau, sélectionnez l’option de menu **CLASSIFICATIONS** > **Étiquettes**. Vous pouvez convertir ces modèles en étiquettes ou créer un lien vers celles-ci quand vous configurez la protection pour vos étiquettes. 

**Lorsque vous avez un abonnement qui inclut uniquement la protection (un abonnement Office 365 qui inclut le service Azure Rights Management) :**

- Les modèles Rights Management de votre locataire sont affichés à la section **Modèles de protection** dans le panneau **Azure Information Protection - Étiquettes**. Pour accéder à ce panneau, sélectionnez l’option de menu **CLASSIFICATIONS** > **Étiquettes**. Aucune étiquette n’est affichée. Vous voyez également les paramètres de configuration qui sont spécifiques à la classification et l’étiquetage, mais ces paramètres n’ont aucun effet sur vos modèles ou ne peuvent pas être configurés. 

## <a name="default-templates"></a>Modèles par défaut

Quand vous obtenez votre abonnement pour Azure Information Protection ou pour un abonnement Office 365 qui inclut le service Azure Rights Management, deux modèles par défaut sont créés automatiquement pour votre locataire. Ces modèles limitent l’accès aux utilisateurs autorisés de votre organisation. Quand ces modèles sont créés, ils ont les autorisations listées dans la documentation [Configuration des droits d’utilisation pour Azure Rights Management](configure-usage-rights.md#rights-included-in-the-default-templates).

Par ailleurs, les modèles sont configurés pour autoriser l’accès hors connexion pendant sept jours et n’ont pas de date d’expiration.

>[!NOTE]
> Vous pouvez changer ces paramètres ainsi que les noms et les descriptions des modèles par défaut. Cette possibilité n’existait pas dans le portail Azure Classic et n’est toujours pas prise en charge dans PowerShell.

Ces modèles par défaut permettent de commencer facilement à protéger les données sensibles de votre organisation. Ces modèles peuvent être utilisés avec des étiquettes d’Azure Information Protection, ou par eux-mêmes avec [des applications et des services](applications-support.md) qui peuvent utiliser des modèles Rights Management.

Vous pouvez également créer vos propres modèles personnalisés. Même si vous n’aurez probablement besoin que de quelques modèles, vous pouvez enregistrer au maximum 500 modèles personnalisés dans Azure.

### <a name="default-template-names"></a>Noms des modèles par défaut

Si vous avez obtenu votre abonnement récemment, vos modèles par défaut sont créés avec les noms suivants :

- **Confidentiel \ Tous les employés**, qui accorde des autorisations de lecture ou de modification du contenu protégé.

- **Hautement confidentiel \ Tous les employés**, qui accorde des autorisations d’accès en lecture seule au contenu protégé.

Si vous avez obtenu votre abonnement il y a quelque temps, vos modèles par défaut sont créés avec les noms suivants :

- **\<nom organisation> - Confidentiel** : accorde des autorisations de lecture ou de modification du contenu protégé.

- **\<nom organisation> - Affichage confidentiel uniquement** : accorde des autorisations d’accès en lecture seule au contenu protégé. 

Vous pouvez renommer (et reconfigurer) ces modèles par défaut quand vous utilisez le portail Azure.

>[!NOTE]
>Si vous ne voyez pas vos modèles par défaut dans le panneau **Azure Information Protection - Étiquettes**, c’est qu’ils sont convertis en étiquettes ou liés à une étiquette. Ils existent encore en tant que modèles, mais dans le portail Azure, ils apparaissent comme faisant partie d’une configuration d’étiquettes qui comprend les paramètres de protection d’une clé cloud. Vous pouvez toujours vérifier les modèles dont dispose votre locataire en exécutant l’applet de commande [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) à partir du [module PowerShell AADRM](administer-powershell.md).
>
>Vous pouvez convertir manuellement des modèles, comme expliqué dans une section ultérieure, [Pour convertir des modèles en étiquettes](#to-convert-templates-to-labels), puis les renommer si vous le voulez. Ils sont convertis automatiquement pour vous si votre stratégie Azure Information Protection par défaut a été créée récemment et que le service Azure Rights Management pour votre locataire a été activé à ce moment.

Les modèles archivés apparaissent comme étant indisponibles dans le panneau **Azure Information Protection - Étiquettes**. Ces modèles ne peuvent pas être sélectionnés pour les étiquettes, mais ils peuvent être convertis en étiquettes.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Considérations relatives aux modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes, tenez compte des changements et des considérations qui suivent. En raison des changements dans l’implémentation, la liste suivante est particulièrement importante si vous avez géré précédemment des modèles dans le portail Azure Classic.

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) d’origine. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels dans le portail Azure. Sinon, utilisez PowerShell avec les applets de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).
    
    - **Autoriser les macros** (nom commun) est automatiquement ajouté. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.

- Les paramètres **Publié** et **Archivé** sous la forme **Activé** : **Oui** et **Activé** : **Non** respectivement sur le panneau **Étiquette**. Pour les modèles que vous voulez conserver mais qui ne doivent pas être visibles par les utilisateurs ou les services, définissez-les sur **Activé** : **Désactivé**.

- Vous ne pouvez pas copier ou supprimer un modèle dans le portail Azure. Quand le modèle est converti en étiquette, vous pouvez configurer l’étiquette pour qu’elle cesse d’utiliser le modèle en sélectionnant **Non configuré** pour l’option **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**. Vous pouvez aussi supprimer l’étiquette. Dans les deux cas cependant, le modèle n’est pas supprimé et reste dans un état archivé.
    
    Vous pouvez maintenant supprimer le modèle en utilisant l’applet de commande PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate). Vous pouvez également utiliser cette applet de commande PowerShell pour les modèles qui ne sont pas convertis en étiquettes. Cependant, si vous supprimez un modèle qui a été utilisé pour protéger du contenu, ce contenu ne peut plus être ouvert. Supprimez des modèles seulement si vous êtes sûr qu’ils n’ont pas été utilisés pour protéger des documents ou des e-mails en production. À titre de précaution, vous pouvez d’abord exporter le modèle en tant que sauvegarde, en utilisant l’applet de commande [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). 

- Actuellement, si vous modifiez et enregistrez un modèle de service, il supprime la configuration d’étendue. L’équivalent d’un modèle délimité dans la stratégie Azure Information Protection est une [stratégie délimitée](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    De plus, vous ne pouvez pas définir le paramètre de compatibilité d’application d’un modèle de service en utilisant le portail Azure. Si nécessaire, vous pouvez définir ce paramètre de compatibilité d’application à l’aide de l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) et du paramètre *EnableInLegacyApps*.

- Quand vous convertissez ou que vous liez un modèle à une étiquette, il ne peut plus être utilisé par d’autres étiquettes. Par ailleurs, ce modèle ne s’affiche plus dans la section **Modèles de protection**. 

- Vous ne créez pas de modèle à partir de la section **Modèles de protection**. Au lieu de cela, créez une étiquette qui a le paramètre **Protéger** et configurez les droits d’utilisation et les paramètres à partir du panneau **Protection**. Pour obtenir des instructions, consultez [Pour créer un nouveau modèle](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Pour configurer les modèles dans la stratégie Azure Information Protection

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au panneau **Azure Information Protection - Étiquettes**.
    
    Par exemple, dans le menu hub, cliquez sur **Tous les services** et tapez **Informations** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, développez **Modèles de protection**, puis recherchez le modèle que vous souhaitez configurer.
    
3. Sélectionnez le modèle, puis, dans le panneau **Étiquette**, vous pouvez changer le nom du modèle et la description si nécessaire en modifiant le **Nom d’étiquette** et la **Description**. Ensuite, sélectionnez **Protection**, qui a la valeur **Azure (clé du cloud)**, pour ouvrir le panneau **Protection**.

4. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration des paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.
    
> [!NOTE]
> Vous pouvez également modifier un modèle à l’aide du bouton **Modifier le modèle** du panneau **Protection**, si vous avez configuré une étiquette pour utiliser un modèle prédéfini. Si aucune autre étiquette utilise le modèle sélectionné, ce bouton convertit le modèle en étiquette et vous ramène à l’étape 5. Pour plus d’informations sur ce qui se passe quand les modèles sont convertis en étiquettes, consultez la section suivante.

## <a name="to-convert-templates-to-labels"></a>Pour convertir des modèles en étiquettes

Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection, vous pouvez convertir des modèles en étiquettes. Lorsque vous convertissez un modèle, le modèle d’origine est conservé, mais dans le portail Azure, il s’affiche désormais comme étant inclus dans une nouvelle étiquette.

Par exemple, si vous convertissez une étiquette nommée **Marketing** qui accorde des droits d’utilisation pour le groupe marketing dans le portail Azure il s’affiche maintenant comme une étiquette nommée **Marketing** qui a les mêmes paramètres de protection. Si vous modifiez les paramètres de protection de cette nouvelle étiquette, vous les changez dans le modèle et n’importe quel utilisateur ou service qui utilise ce modèle obtient les nouveaux paramètres de protection lors de la prochaine actualisation des modèles. 

Il n’est pas nécessaire de convertir tous vos modèles en étiquettes, mais lorsque vous le faites, les paramètres de protection sont totalement intégrés à l’ensemble des fonctionnalités des étiquettes afin que vous n’ayez pas à mettre à jour les paramètres séparément.

Pour convertir un modèle en étiquette, cliquez sur le modèle, puis sélectionnez **Convertir en étiquette**. Vous pouvez également utiliser le menu contextuel pour sélectionner cette option. 

Vous pouvez également convertir un modèle en étiquette quand vous configurez une étiquette pour la protection et un modèle prédéfini, à l’aide du bouton **Modifier le modèle**. 

Lorsque vous convertissez un modèle en étiquette :

- Le nom du modèle est converti en un nouveau nom d’étiquette, et la description du modèle est convertie en info-bulle pour l’étiquette. 

- Si l’état du modèle a été publié, ce paramètre est mappé sur **Activé** : **Oui** pour l’étiquette, qui s’affiche désormais comme cette étiquette pour les utilisateurs lorsque vous publiez ensuite la stratégie Azure Information Protection. Si l’état du modèle a été archivé, ce paramètre est mappé à **Activé** : **Non** pour l’étiquette et ne s’affiche pas comme une étiquette disponible pour les utilisateurs.

- Les paramètres de protection sont conservés, et vous pouvez les modifier si nécessaire, puis ajouter également d’autres paramètres à l’étiquette, comme des marqueurs visuels et des conditions.

- Le modèle d’origine n’est plus affiché dans **Modèles de protection** et ne peut pas être sélectionné comme modèle prédéfini quand vous configurez la protection d’une étiquette. Pour modifier ce modèle dans le portail Azure, vous modifiez maintenant l’étiquette qui a été créée quand vous avez converti le modèle. Le modèle reste disponible pour le service Azure Rights Management et peut toujours être géré à l’aide de [commandes PowerShell](administer-powershell.md).  

## <a name="to-create-a-new-template"></a>Pour créer un nouveau modèle

Quand vous créez une étiquette avec le paramètre de protection **Azure (clé cloud)**, en arrière-plan, cette action crée un modèle personnalisé qui est ensuite accessible pour les services et applications qui sont intégrés aux modèles Rights Management.

1. À partir de l’option de menu **CLASSIFICATIONS** > **Étiquettes** : dans le panneau **Azure Information Protection - Étiquettes**, sélectionnez **Ajouter une nouvelle étiquette**.

2. Dans le panneau **Étiquette**, conservez la valeur par défaut **Activé** : **On**, puis entrez un nom d’étiquette et une description pour le nom du modèle et la description.

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis **Protection** :
    
     ![Configurer la protection d’une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png)

4. Sur le panneau **Protection**, vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration de ces paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis, dans le panneau **Étiquette**, cliquez sur **Enregistrer**.
    
    Dans le panneau **Azure Information Protection - Étiquettes**, vous voyez maintenant votre nouvelle étiquette, accompagnée de la colonne **PROTECTION** indiquant qu’elle contient des paramètres de protection. Ces paramètres de protection s’affichent en tant que modèles pour les applications et services qui prennent en charge le service Azure Rights Management.
    
    Bien que l’étiquette soit activée, par défaut, le modèle est archivé. Afin que les applications et services puissent utiliser le modèle pour protéger des documents et des e-mails, exécutez la dernière étape pour publier le modèle.

5. À partir de l’option de menu **CLASSIFICATIONS** > **Stratégies**, sélectionnez la stratégie qui doit contenir les nouveaux paramètres de protection. Puis, sélectionnez **Ajouter ou supprimer des étiquettes**. Dans le panneau **Stratégie : ajouter ou supprimer des étiquettes**, sélectionnez l’étiquette créée qui contient vos paramètres de protection, cliquez sur **OK**, puis sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Il peut prendre jusqu'à 15 minutes pour qu’un ordinateur exécutant le client Azure Information Protection obtienne ces paramètres modifiés. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent les modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

Tout ce que vous pouvez configurer dans le portail Azure pour créer et gérer vos modèles, vous pouvez le faire en utilisant PowerShell. En outre, PowerShell offre des options supplémentaires qui ne sont pas disponibles dans le portail. Pour plus d’informations, consultez [Informations de référence sur PowerShell pour les modèles de protection](configure-templates-with-powershell.md). 

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  
