---
title: Configurer et gérer des modèles pour Azure Information Protection – AIP
description: Configurez et gérez les modèles de protection, également appelés modèles de gestion des droits, à partir du Portail Azure.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 63c6857794730dc0b6532d39c6ae7b8a2d572671
ms.sourcegitcommit: b66b249ab5681d02ec3b5af0b820eda262d5976a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "78973297"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuration et gestion des modèles pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Instructions pour : [Azure information protection client pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Les modèles de protection, également appelés modèles Rights Management, sont un regroupement de paramètres de protection définis par l’administrateur pour Azure Information Protection. Ces paramètres incluent les [droits d’utilisation](configure-usage-rights.md) que vous avez choisis pour les utilisateurs autorisés et les contrôles d’accès pour l’accès hors connexion et après l’expiration. Ces modèles sont intégrés à la stratégie Azure Information Protection : 

**Si vous avez un abonnement qui inclut la classification, l’étiquetage et la protection (Azure Information Protection P1 or P2) :**

- Les modèles qui ne sont pas intégrés à vos étiquettes pour votre locataire sont affichés dans la section **modèles de protection** après vos étiquettes dans le volet **Azure information protection-étiquettes** . Pour accéder à ce volet, sélectionnez l’option de menu **classifications** > **étiquettes** . Vous pouvez convertir ces modèles en étiquettes ou créer un lien vers celles-ci quand vous configurez la protection pour vos étiquettes. 

**Lorsque vous avez un abonnement qui inclut uniquement la protection (un abonnement Office 365 qui inclut le service Azure Rights Management) :**

- Les modèles de votre locataire sont affichés dans la section **modèles de protection** dans le volet **Azure information protection-étiquettes** . Pour accéder à ce volet, sélectionnez l’option de menu **classifications** > **étiquettes** . Aucune étiquette n’est affichée. Vous voyez également les paramètres de configuration qui sont spécifiques à la classification et l’étiquetage, mais ces paramètres n’ont aucun effet sur vos modèles ou ne peuvent pas être configurés. 

>[!NOTE]
>Dans certains services et applications, vous pouvez voir [Ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails) et [Chiffrement seul](configure-usage-rights.md#encrypt-only-option-for-emails) (ou **Chiffrer**) affichés sous la forme d’un modèle. Ils ne s’agit pas de modèles que vous pouvez modifier ou supprimer, mais d’options fournies par défaut avec le service Exchange.

## <a name="default-templates"></a>Modèles par défaut

Quand vous obtenez votre abonnement pour Azure Information Protection ou pour un abonnement Office 365 qui inclut le service Azure Rights Management, deux modèles par défaut sont créés automatiquement pour votre locataire. Ces modèles limitent l’accès aux utilisateurs autorisés de votre organisation. Lorsque ces modèles sont créés, ils disposent des autorisations répertoriées dans la documentation [Configuration des droits d’utilisation pour Azure information protection](configure-usage-rights.md#rights-included-in-the-default-templates) .

Par ailleurs, les modèles sont configurés pour autoriser l’accès hors connexion pendant sept jours et n’ont pas de date d’expiration.

>[!NOTE]
> Vous pouvez changer ces paramètres ainsi que les noms et les descriptions des modèles par défaut. Cette possibilité n’existait pas dans le portail Azure Classic et n’est toujours pas prise en charge dans PowerShell.

Ces modèles par défaut permettent de commencer facilement à protéger les données sensibles de votre organisation. Ces modèles peuvent être utilisés avec des étiquettes d’Azure Information Protection, ou par eux-mêmes avec [des applications et des services](applications-support.md) qui peuvent utiliser des modèles Rights Management.

Vous pouvez également créer vos propres modèles personnalisés. Même si vous n’aurez probablement besoin que de quelques modèles, vous pouvez enregistrer au maximum 500 modèles personnalisés dans Azure.


### <a name="default-template-names"></a>Noms des modèles par défaut

Si vous avez obtenu votre abonnement récemment, vos modèles par défaut sont créés avec les noms suivants :

- **Confidentiel \ Tous les employés**

- **Hautement confidentiel \ Tous les employés**

Si vous avez obtenu votre abonnement il y a quelque temps, vos modèles par défaut peuvent être créés avec les noms suivants :

- **nom de l’organisation \<>-confidentiel**

- **\<nom de l’organisation> - Affichage confidentiel uniquement** 

Vous pouvez renommer (et reconfigurer) ces modèles par défaut quand vous utilisez le portail Azure.

>[!NOTE]
>Si vous ne voyez pas vos modèles par défaut dans le volet **Azure information protection-étiquettes** , ils sont convertis en étiquettes ou liés à une étiquette. Ils existent encore en tant que modèles, mais dans le portail Azure, ils apparaissent comme faisant partie d’une configuration d’étiquettes qui comprend les paramètres de protection d’une clé cloud. Vous pouvez toujours confirmer les modèles de votre locataire, en exécutant la [AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) à partir du [module PowerShell AIPService](administer-powershell.md).
>
>Vous pouvez convertir manuellement des modèles, comme expliqué dans une section ultérieure, [Pour convertir des modèles en étiquettes](#to-convert-templates-to-labels), puis les renommer si vous le voulez. Ils sont convertis automatiquement pour vous si votre stratégie Azure Information Protection par défaut a été créée récemment et que le service Azure Rights Management pour votre locataire a été activé à ce moment.

Les modèles archivés apparaissent comme étant indisponibles dans le volet **Azure information protection-étiquettes** . Ces modèles ne peuvent pas être sélectionnés pour les étiquettes, mais ils peuvent être convertis en étiquettes.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Considérations relatives aux modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes, tenez compte des changements et des considérations qui suivent. En raison des changements dans l’implémentation, la liste suivante est particulièrement importante si vous avez géré précédemment des modèles dans le portail Azure Classic.

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) d’origine. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels dans le portail Azure. Ou utilisez PowerShell avec les applets de commande [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) et [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) .
    
    - **Autoriser les macros** (nom commun) est automatiquement ajouté. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.

- Les paramètres **publiés** et **archivés** affichent **activé**: activé et **activé**: **désactivé** **respectivement dans le** volet **étiquette** . Pour les modèles que vous voulez conserver mais qui ne doivent pas être visibles par les utilisateurs ou les services, définissez-les sur **Activé** : **Désactivé**.

- Vous ne pouvez pas copier ou supprimer un modèle dans le portail Azure. Quand le modèle est converti en étiquette, vous pouvez configurer l’étiquette pour qu’elle cesse d’utiliser le modèle en sélectionnant **Non configuré** pour l’option **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**. Vous pouvez aussi supprimer l’étiquette. Dans les deux cas cependant, le modèle n’est pas supprimé et reste dans un état archivé.
    
    Vous pouvez maintenant supprimer le modèle à l’aide de l’applet de commande PowerShell [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) . Vous pouvez également utiliser cette applet de commande PowerShell pour les modèles qui ne sont pas convertis en étiquettes. Cependant, pour garantir que le contenu précédemment protégé puisse être ouvert et utilisé comme prévu, nous vous déconseillons généralement de supprimer des modèles. En guise de bonne pratique, supprimez uniquement des modèles si vous êtes sûr qu’ils n’ont pas été utilisés pour protéger des documents ou des e-mails en production. Par précaution, vous souhaiterez peut-être d’abord exporter le modèle en tant que sauvegarde, à l’aide de l’applet de commande [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate) . 

- Actuellement, si vous modifiez et enregistrez un modèle de service, il supprime la configuration d’étendue. L’équivalent d’un modèle délimité dans la stratégie Azure Information Protection est une [stratégie délimitée](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    De plus, vous ne pouvez pas définir le paramètre de compatibilité d’application d’un modèle de service en utilisant le portail Azure. Si nécessaire, vous pouvez définir ce paramètre de compatibilité des applications à l’aide de l’applet de commande [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) et du paramètre *du enableinlegacyapps* .

- Quand vous convertissez ou que vous liez un modèle à une étiquette, il ne peut plus être utilisé par d’autres étiquettes. Par ailleurs, ce modèle ne s’affiche plus dans la section **Modèles de protection**. 

- Vous ne créez pas de modèle à partir de la section **Modèles de protection**. Au lieu de cela, créez une étiquette qui a le paramètre **protéger** et configurez les droits d’utilisation et les paramètres à partir du volet **protection** . Pour obtenir des instructions, consultez [Pour créer un nouveau modèle](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Pour configurer les modèles dans la stratégie Azure Information Protection

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Ensuite, accédez au volet **Azure information protection-étiquettes** .
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. À partir de l’option de menu **classifications** > **étiquettes** : dans le volet **Azure information protection-étiquettes** , développez **modèles de protection**, puis recherchez le modèle que vous souhaitez configurer.
    
3. Sélectionnez le modèle, puis dans le volet **étiquette** , vous pouvez modifier le nom et la description du modèle, le cas échéant, en modifiant le **nom complet** et la **Description**de l’étiquette. Ensuite, sélectionnez **protection** qui a la valeur **Azure (clé Cloud)** pour ouvrir le volet **protection** .

4. Dans le volet **protection** , vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration des paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis dans le volet **étiquette** , cliquez sur **Enregistrer**.
    
> [!NOTE]
> Vous pouvez également modifier un modèle à l’aide du bouton **modifier le modèle** dans le volet **protection** si vous avez configuré une étiquette pour utiliser un modèle prédéfini. Si aucune autre étiquette utilise le modèle sélectionné, ce bouton convertit le modèle en étiquette et vous ramène à l’étape 5. Pour plus d’informations sur ce qui se passe quand les modèles sont convertis en étiquettes, consultez la section suivante.

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

Quand vous créez une étiquette avec le paramètre de protection **Azure (clé cloud)** , en arrière-plan, cette action crée un modèle personnalisé qui est ensuite accessible pour les services et applications qui sont intégrés aux modèles Rights Management.

1. À partir de l’option de menu **classifications** > **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez **Ajouter une nouvelle étiquette**.

2. Dans le volet **étiquette** , conservez la valeur par défaut **activé : activée**, puis entrez un nom d’étiquette et une description pour le nom et la description du modèle. **On**

3. Pour **Définir les autorisations pour les documents et les e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis **Protection** :
    
     ![Configurer la protection d’une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png)

4. Dans le volet **protection** , vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour en savoir plus sur la configuration de ces paramètres de protection, voir [Comment configurer une étiquette pour la protection offerte par Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis dans le volet **étiquette** , cliquez sur **Enregistrer**.
    
    Dans le volet **Azure information protection-étiquettes** , vous voyez maintenant votre nouvelle étiquette affichée avec la colonne **protection** pour indiquer qu’elle contient des paramètres de protection. Ces paramètres de protection s’affichent en tant que modèles pour les applications et services qui prennent en charge le service Azure Rights Management.
    
    Bien que l’étiquette soit activée, par défaut, le modèle est archivé. Afin que les applications et services puissent utiliser le modèle pour protéger des documents et des e-mails, exécutez la dernière étape pour publier le modèle.

5. À partir de l’option de menu **Classifications** > **Stratégies**, sélectionnez la stratégie qui doit contenir les nouveaux paramètres de protection. Puis, sélectionnez **Ajouter ou supprimer des étiquettes**. Dans le volet **stratégie : ajouter ou supprimer des étiquettes** , sélectionnez l’étiquette qui vient d’être créée et qui contient vos paramètres de protection, cliquez sur **OK**, puis sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Il peut prendre jusqu'à 15 minutes pour qu’un ordinateur exécutant le client Azure Information Protection obtienne ces paramètres modifiés. Pour plus d’informations sur la façon dont les ordinateurs et les services téléchargent et actualisent les modèles, consultez [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

Tout ce que vous pouvez configurer dans le portail Azure pour créer et gérer vos modèles, vous pouvez le faire en utilisant PowerShell. En outre, PowerShell offre des options supplémentaires qui ne sont pas disponibles dans le portail. Pour plus d’informations, consultez [Informations de référence sur PowerShell pour les modèles de protection](configure-templates-with-powershell.md). 

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

