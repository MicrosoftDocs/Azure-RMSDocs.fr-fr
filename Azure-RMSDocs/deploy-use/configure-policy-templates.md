---
title: "Configurer et gérer les modèles dans la stratégie Azure Information Protection"
description: "Actuellement en version préliminaire : vous pouvez désormais configurer et gérer des modèles de gestion des droits à partir de la stratégie Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: dc39a52ca09ec7818b70a5bac320024bdc4de657
ms.sourcegitcommit: 4186c8fadea7bcd32cce7d468916374a9cdf151b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2017
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuration et gestion des modèles pour Azure Information Protection

>*S’applique à : Azure Information Protection*

>[!NOTE]
>Cette fonctionnalité remplace la configuration de modèles personnalisés dans le portail Azure Classic.
>
>Même si vous pouvez toujours créer et gérer les modèles dans le portail Azure Classic, nous vous déconseillons de gérer les mêmes modèles à partir du portail Azure Classic et du portail Azure. L’implémentation de la configuration des modèles dans ces différents portails a changé : configurer le même modèle dans des portails différents peut aboutir à une configuration non fiable.


Les modèles Rights Management sont désormais intégrés à la stratégie Azure Information Protection. 

**Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection (Azure Information Protection P1 or P2) :**

- Les modèles Rights Management qui ne sont pas intégrés aux étiquettes pour votre locataire sont affichés dans la section **Modèles** après les étiquettes du panneau **Azure Information Protection - Stratégie globale**. Vous pouvez convertir ces modèles en étiquettes ou créer un lien vers celles-ci quand vous configurez la protection pour vos étiquettes. 

**Lorsque vous avez un abonnement qui inclut uniquement la protection (un abonnement Office 365 qui inclut le service Azure Rights Management) :**

- Les modèles Rights Management pour votre locataire sont affichés dans le panneau **Azure Information Protection - Stratégie globale**, dans la section **Modèles**. Aucune étiquette n’est affichée. Vous voyez également les paramètres de configuration qui sont spécifiques à la classification et l’étiquetage, mais ceux-ci n’ont aucun effet sur vos modèles ou ne peuvent pas être configurés. 

## <a name="default-templates"></a>Modèles par défaut

Quand vous obtenez votre abonnement pour Azure Information Protection ou pour un abonnement Office 365 qui inclut le service Azure Rights Management, deux modèles par défaut sont créés automatiquement pour votre locataire, qui limitent l’accès aux utilisateurs autorisés de votre organisation. Ces deux modèles ont les restrictions suivantes : 

- Autorisations de lecture ou de modification du contenu protégé
    
    - Autorisations spécifiques : Afficher le contenu, Enregistrer le fichier, Modifier le contenu, Afficher les droits affectés, Autoriser les macros, Transférer, Répondre, Répondre à tous

- Affichage en lecture seule du contenu protégé
    
    - Autorisation spécifique : Afficher le contenu

Ces modèles permettent à vous-même et d’autres personnes de commencer facilement à protéger les données sensibles de votre organisation. Ces modèles peuvent être utilisés avec des étiquettes d’Azure Information Protection, ou par eux-mêmes avec [des applications et des services](../understand-explore/applications-support.md) qui peuvent utiliser des modèles Rights Management.

Vous pouvez également créer vos propres modèles personnalisés. Même si vous n’aurez probablement besoin que de quelques modèles, vous pouvez enregistrer au maximum 500 modèles personnalisés dans Azure.

### <a name="default-template-names"></a>Noms des modèles par défaut

Si vous avez obtenu récemment un abonnement pour Azure Information Protection, les noms de vos modèles par défaut sont les suivants :

- **Confidentiel \ Tous les employés** pour les autorisations de lecture ou de modification du contenu protégé.

- **Hautement confidentiel \ Tous les employés** pour les autorisations d’affichage en lecture seule du contenu protégé.

Si vous avez obtenu votre abonnement Azure Information Protection il y a quelque temps, ou si vous n’avez pas d’abonnement Azure Information Protection mais que vous avez un abonnement Office 365 incluant Azure Rights Management, les noms de vos modèles par défaut sont les suivants :

- **\<nom organisation> - Confidentiel** pour les autorisations de lecture ou de modification du contenu protégé.

- **\<nom organisation> - Affichage confidentiel uniquement** pour l’affichage en lecture seule du contenu protégé. 

>[!NOTE]
>Si vous ne voyez pas vos modèles par défaut dans le panneau **Azure Information Protection - Stratégie globale**, c’est qu’ils sont convertis en étiquettes ou liés à une étiquette. Ils existent encore en tant que modèles, mais dans le portail Azure, ils apparaissent comme faisant partie d’une configuration d’étiquettes qui inclut la protection Azure RMS. Vous pouvez toujours vérifier les modèles dont dispose votre locataire en exécutant l’applet de commande [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate) à partir du [module PowerShell AADRM](administer-powershell.md).
>
>Vous pouvez convertir manuellement des modèles, comme expliqué dans une section ultérieure, [Pour convertir des modèles en étiquettes](#to-convert-templates-to-labels), puis les renommer si vous le voulez. Ils seront convertis automatiquement pour vous si votre stratégie Azure Information Protection par défaut a été créée récemment et que le service Azure Rights Management pour votre locataire a été activé à ce moment.

Les modèles archivés apparaissent comme étant indisponibles dans le panneau **Azure Information Protection - Stratégie globale**. Ces modèles ne peuvent pas être sélectionnés pour les étiquettes, mais ils peuvent être convertis en étiquettes.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Considérations relatives aux modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes, tenez compte des changements et des considérations qui suivent. En raison des changements dans l’implémentation, la liste suivante est particulièrement importante si vous avez géré précédemment des modèles dans le portail Azure Classic.

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) d’origine. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels à l’aide de PowerShell avec les applets de commande [New-AadrmRightsDefinition](/powershell/module/aadrm/set-aadrmtemplateproperty) et [Set-AadrmTemplateProperty](/powershell/module/aadrm/new-aadrmrightsdefinition).
    
    - **Enregistrer sous, Exporter** (nom commun) est supprimé. Dans le portail Azure, vous ne pouvez pas spécifier manuellement ce droit d’utilisation, mais il est inclus avec le droit d’utilisation Contrôle total, que vous pouvez ajouter si nécessaire.
    
    - **Autoriser les macros** (nom commun) est automatiquement ajouté. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.
    

- Les paramètres **Publié** et **Archivé** sous la forme **Activé** : **Oui** et **Activé** : **Non** respectivement sur le panneau **Étiquette**. Pour les modèles que vous voulez conserver mais qui ne doivent pas être visibles par les utilisateurs ou les services, définissez pour ceux-ci **Activé** : **Désactivé**.

- Vous ne pouvez pas copier ou supprimer un modèle dans le portail Azure. Quand le modèle est converti en étiquette, vous pouvez configurer l’étiquette pour qu’elle cesse d’utiliser le modèle en sélectionnant **Non configuré** pour l’option **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**. Vous pouvez aussi supprimer l’étiquette. Dans les deux cas cependant, le modèle n’est pas supprimé et reste dans un état archivé.
    
    Vous pouvez maintenant supprimer le modèle en utilisant l’applet de commande PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate). Vous pouvez également utiliser cette applet de commande PowerShell pour les modèles qui ne sont pas convertis en étiquettes. Cependant, si vous supprimez un modèle qui a été utilisé pour protéger du contenu, ce contenu ne peut plus être ouvert. Supprimez des modèles seulement si vous êtes sûr qu’ils n’ont pas été utilisés pour protéger des documents ou des e-mails en production. À titre de précaution, vous pouvez d’abord exporter le modèle en tant que sauvegarde, en utilisant l’applet de commande [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate). 

- Les modèles de service (les modèles qui sont configurés pour une étendue) s’affichent dans la stratégie globale. Actuellement, si vous modifiez et enregistrez un modèle de service, il supprime la configuration d’étendue. L’équivalent d’un modèle délimité dans la stratégie Azure Information Protection est une [stratégie délimitée](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    En outre, vous ne pouvez actuellement pas définir le paramètre de compatibilité d’application pour un modèle de service. Si nécessaire, vous pouvez définir cela à l’aide de PowerShell avec l’applet de commande [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

- Actuellement, les modèles que vous avez configurés pour plusieurs langues à l’aide du portail Azure Classic ou de PowerShell n’affichent pas ces langues pour le nom et les descriptions, mais elles sont conservées.

- Quand vous convertissez ou que vous liez un modèle à une étiquette, il ne peut plus être utilisé par d’autres étiquettes.

- Vous ne créez pas un nouveau modèle à partir du conteneur **Modèles**. Au lieu de cela, créez une étiquette qui a le paramètre **Protéger** et configurez les droits d’utilisation et les paramètres à partir du panneau **Protection**. Pour obtenir des instructions, consultez [Pour créer un nouveau modèle](#to-create-a-new-template).

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

- Le modèle d’origine n’est plus affiché sous **Modèles** et il ne peut pas être sélectionné comme modèle prédéfini quand vous configurez la protection pour une étiquette. Pour modifier ce modèle dans le portail Azure, vous modifiez maintenant l’étiquette qui a été créée quand vous avez converti le modèle. Le modèle reste disponible pour le service Azure Rights Management et peut toujours être géré à l’aide de [commandes PowerShell](administer-powershell.md).  

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

Tout ce que vous pouvez configurer dans le portail Azure pour créer et gérer vos modèles, vous pouvez le faire en utilisant PowerShell. En outre, PowerShell offre des options supplémentaires qui ne sont pas disponibles dans le portail. Pour plus d’informations, consultez [Informations de référence sur PowerShell pour les modèles de protection](configure-templates-with-powershell.md). 

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
