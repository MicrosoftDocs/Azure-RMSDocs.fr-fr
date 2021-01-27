---
title: Configurer et gérer des modèles pour Azure Information Protection – AIP
description: Configurez et gérez les modèles de protection, également appelés modèles de gestion des droits, à partir du Portail Azure.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8301aabb-047d-4892-935c-7574f6af8813
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 761927f4815460b5b83b17e7f7481e1ff3a0cf9e
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809719"
---
# <a name="configuring-and-managing-templates-for-azure-information-protection"></a>Configuration et gestion des modèles pour Azure Information Protection

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne :** [Azure information protection client classique pour Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client d’étiquetage unifié, consultez [en savoir plus sur les étiquettes de sensibilité](/microsoft-365/compliance/sensitivity-labels) et [restreindre l’accès au contenu à l’aide du chiffrement dans les étiquettes de sensibilité](/microsoft-365/compliance/encryption-sensitivity-labels) de la documentation de Microsoft 365. *

> [!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.
>

Les modèles de protection, également appelés modèles Rights Management, sont un regroupement de paramètres de protection définis par l’administrateur pour Azure Information Protection. Ces paramètres incluent les [droits d’utilisation](configure-usage-rights.md) que vous avez choisis pour les utilisateurs autorisés et les contrôles d’accès pour l’accès hors connexion et après l’expiration. Ces modèles sont intégrés à la stratégie Azure Information Protection : 

**Si vous avez un abonnement qui comprend la classification, l’étiquetage et la protection (Azure information protection P1 ou P2)**:

- Les modèles qui ne sont pas intégrés à vos étiquettes pour votre locataire sont affichés dans la section **modèles de protection** après vos étiquettes dans le volet **Azure information protection-étiquettes** . Pour accéder à ce volet, sélectionnez l’option de menu **classifications**  >  **étiquettes** . Vous pouvez convertir ces modèles en étiquettes, ou les lier à des étiquettes lorsque vous configurez la protection de vos étiquettes. 

**Si vous avez un abonnement qui comprend uniquement la protection (un abonnement Microsoft 365 qui comprend le service Azure Rights Management)**:

- Les modèles de votre locataire sont affichés dans la section **modèles de protection** dans le volet **Azure information protection-étiquettes** . Pour accéder à ce volet, sélectionnez l’option de menu **classifications**  >  **étiquettes** . Aucune étiquette n’apparaît. Vous pouvez également voir les paramètres de configuration qui sont spécifiques à la classification et à l’étiquetage, mais ces paramètres n’ont aucun effet sur vos modèles ou ne peuvent pas être configurés. 

>[!NOTE]
>Dans certains services et applications, vous pouvez voir [ne pas transférer](configure-usage-rights.md#do-not-forward-option-for-emails) et [chiffrer uniquement](configure-usage-rights.md#encrypt-only-option-for-emails) (**chiffrer**) affiché en tant que modèle. Ils ne s’agit pas de modèles que vous pouvez modifier ou supprimer, mais d’options fournies par défaut avec le service Exchange.

## <a name="default-templates"></a>Modèles par défaut

Lorsque vous obtenez votre abonnement pour Azure Information Protection ou pour un abonnement Microsoft 365 qui comprend le service de Rights Management Azure, deux modèles par défaut sont créés automatiquement pour votre locataire. Ces modèles restreignent l’accès aux utilisateurs autorisés de votre organisation. Lorsque ces modèles sont créés, ils disposent des autorisations répertoriées dans la documentation [Configuration des droits d’utilisation pour Azure information protection](configure-usage-rights.md#rights-included-in-the-default-templates) .

En outre, les modèles sont configurés pour autoriser l’accès hors connexion pendant sept jours et n’ont pas de date d’expiration.

>[!NOTE]
> Vous pouvez modifier ces paramètres, ainsi que les noms et descriptions des modèles par défaut. Cette possibilité n’était pas possible avec le portail Azure Classic et n’est toujours pas prise en charge pour PowerShell.

Ces modèles par défaut vous permettent, à vous et pour d’autres, de lancer immédiatement la protection des données sensibles de votre organisation. Ces modèles peuvent être utilisés avec les étiquettes d’Azure Information Protection, ou séparément avec des [applications et services](applications-support.md) qui utilisent des modèles Rights Management.

Vous pouvez également créer vos propres modèles. Même si vous n’avez probablement besoin que de quelques modèles seulement, vous pouvez enregistrer jusqu’à un maximum de 500 modèles personnalisés dans Azure.


### <a name="default-template-names"></a>Noms des modèles par défaut

Si vous avez obtenu votre abonnement récemment, vos modèles par défaut sont créés avec les noms suivants :

- **Confidentiel \ Tous les employés**

- **Hautement confidentiel \ Tous les employés**

Si vous avez obtenu votre abonnement il y a quelque temps, vos modèles par défaut peuvent être créés avec les noms suivants :

- **\<organization name> -Confidentiel**

- **\<organization name> -Affichage confidentiel uniquement** 

Vous pouvez renommer (et reconfigurer) ces modèles par défaut lorsque vous utilisez le portail Azure.

>[!NOTE]
>Si vous ne voyez pas vos modèles par défaut dans le volet **Azure information protection-étiquettes** , ils sont convertis en étiquettes ou liés à une étiquette. Ils existent encore en tant que modèles, mais dans le portail Azure, ils apparaissent comme faisant partie d’une configuration d’étiquettes qui comprend les paramètres de protection d’une clé cloud. Vous pouvez toujours confirmer les modèles de votre locataire, en exécutant la [AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate) à partir du [module PowerShell AIPService](administer-powershell.md).
>
>Vous pouvez convertir manuellement des modèles, comme expliqué dans la section ultérieure [Pour convertir des modèles en étiquettes](#to-convert-templates-to-labels), puis les renommer si vous le souhaitez. Ou bien ils sont convertis automatiquement pour vous si votre stratégie Azure Information Protection par défaut a été créée récemment et que le service Azure Rights Management pour votre client était activé à ce moment-là.

Les modèles archivés apparaissent comme étant indisponibles dans le volet **Azure information protection-étiquettes** . Ces modèles ne peuvent pas être sélectionnés pour des étiquettes, mais ils peuvent être convertis en étiquettes.

## <a name="considerations-for-templates-in-the-azure-portal"></a>Éléments à prendre en considération pour les modèles dans le portail Azure

Avant de modifier ces modèles ou de les convertir en étiquettes, assurez-vous que vous avez pris connaissance des éléments à prendre en considération et modifications suivantes. En raison de modifications d’implémentation, la liste suivante est particulièrement importante si vous gériez auparavant vos modèles dans le portail Azure Classic.

- Une fois que vous modifiez ou convertissez un modèle et enregistrez la stratégie Azure Information Protection, les modifications suivantes sont apportées aux [droits d’utilisation](configure-usage-rights.md) originaux. Si nécessaire, vous pouvez ajouter ou supprimer des droits d’utilisation individuels en utilisant le portail Azure. Ou utilisez PowerShell avec les applets de commande [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) et [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) .
    
    - **Autoriser les macros** (nom commun) est ajouté automatiquement. Ce droit d’utilisation est requis pour la barre Azure Information Protection dans les applications Office.

- Les paramètres **publiés** et **archivés** affichent **activé**: activé et **activé**: **désactivé** **respectivement dans le** volet **étiquette** . Pour les modèles que vous souhaitez conserver, mais ne pas rendre visible aux utilisateurs ou services, définissez ces modèles sur **Activé** : **Non**.

- Vous ne pouvez pas copier ou supprimer un modèle dans le portail Azure. Lorsque le modèle est converti en étiquette, vous pouvez configurer l’étiquette pour qu’elle cesse d’utiliser le modèle en sélectionnant **Non configuré** pour l’option **Définir des autorisations pour les documents et e-mails contenant cette étiquette**. Ou, vous pouvez supprimer l’étiquette. Toutefois, dans les deux cas, le modèle n’est pas supprimé et demeure à l’état archivé.
    
    La suppression de modèles à l’aide de l’applet de commande PowerShell [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate) est **définitive**. Vous pouvez également utiliser cette applet de commande PowerShell pour les modèles qui ne sont pas convertis en étiquettes. Cependant, pour garantir que le contenu précédemment protégé puisse être ouvert et utilisé comme prévu, nous vous déconseillons généralement de supprimer des modèles. En guise de bonne pratique, supprimez uniquement des modèles si vous êtes sûr qu’ils n’ont pas été utilisés pour protéger des documents ou des e-mails en production. Par précaution avant de supprimer définitivement un modèle à l’aide de PowerShell, envisagez d’exporter le modèle en tant que sauvegarde à l’aide de l’applet de commande [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate) . 

- Actuellement, si vous modifiez et enregistrez un modèle de service, cela supprime la configuration d’étendue. L’équivalent d’un modèle étendu dans la stratégie Azure Information Protection est une [stratégie étendue](configure-policy-scope.md). Si vous convertissez le modèle en étiquette, vous pouvez sélectionner une étendue existante.
    
    De plus, vous ne pouvez pas définir le paramètre de compatibilité d’application d’un modèle de service en utilisant le portail Azure. Si nécessaire, vous pouvez définir ce paramètre de compatibilité des applications à l’aide de l’applet de commande [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) et du paramètre *du enableinlegacyapps* .

- Quand vous convertissez ou liez un modèle à une étiquette, il ne peut plus être utilisé par d’autres étiquettes. En outre, ce modèle ne s’affiche plus dans la section **Modèles de protection**. 

- Ne créez pas de nouveau modèle à partir de la section **Modèles de protection**. Au lieu de cela, créez une étiquette qui a le paramètre **protéger** et configurez les droits d’utilisation et les paramètres à partir du volet **protection** . Pour obtenir des instructions complètes, consultez [Créer un nouveau modèle](#to-create-a-new-template).

## <a name="to-configure-the-templates-in-the-azure-information-protection-policy"></a>Configurer les modèles dans la stratégie Azure Information Protection

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Ensuite, accédez au volet **Azure information protection-étiquettes** .
    
    Par exemple, dans la zone de recherche de ressources, services et documents : Commencez à taper **Information** et sélectionnez **Azure Information Protection**.

2. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , développez **modèles de protection**, puis recherchez le modèle que vous souhaitez configurer.
    
3. Sélectionnez le modèle, puis dans le volet **étiquette** , vous pouvez modifier le nom et la description du modèle, le cas échéant, en modifiant le **nom complet** et la **Description** de l’étiquette. Ensuite, sélectionnez **protection** qui a la valeur **Azure (clé Cloud)** pour ouvrir le volet **protection** .

4. Dans le volet **protection** , vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour plus d’informations sur la configuration des paramètres de protection, consultez [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md)
    
    Cliquez sur **OK** pour conserver vos modifications, puis dans le volet **étiquette** , cliquez sur **Enregistrer**.
    
> [!NOTE]
> Vous pouvez également modifier un modèle à l’aide du bouton **modifier le modèle** dans le volet **protection** si vous avez configuré une étiquette pour utiliser un modèle prédéfini. À condition qu’aucune autre étiquette n’utilise également le modèle sélectionné, ce bouton convertit le modèle en étiquette et vous amène à l’étape 5. Pour plus d’informations sur ce qui se passe lorsque des modèles sont convertis en étiquettes, consultez la section suivante.

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

Vous pouvez créer des modèles à l’aide du portail ou de PowerShell. 

### <a name="template-creation-using-powershell"></a>Création de modèle à l’aide de PowerShell

Pour créer un modèle de protection à l’aide de PowerShell avec le nom, la description, la stratégie et le paramètre d’état souhaité spécifiés, utilisez l’applet de commande [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate) . 


### <a name="template-creation-using-the-portal"></a>Création de modèle à l’aide du portail

Lorsque vous créez une étiquette à l’aide du portail avec le paramètre de protection **Azure (clé Cloud)**, cette action crée un nouveau modèle personnalisé qui est ensuite accessible par les services et applications qui s’intègrent à Rights Management modèles.

1. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez **Ajouter une nouvelle étiquette**.

2. Dans le volet **étiquette** , conservez la valeur par défaut **activé : activée**, puis entrez un nom d’étiquette et une description pour le nom et la description du modèle. 

3. Pour **Définir les autorisations pour les documents et e-mails contenant cette étiquette**, sélectionnez **Protéger**, puis sélectionnez **Protection** :
    
     ![Configurer la protection pour une étiquette Azure Information Protection](./media/info-protect-protection-bar-configured.png)

4. Dans le volet **protection** , vous pouvez modifier les autorisations, l’expiration du contenu et les paramètres d’accès hors connexion. Pour plus d’informations sur la configuration de ces paramètres de protection, consultez [Comment configurer une étiquette pour la protection de Rights Management](configure-policy-protection.md).
    
    Cliquez sur **OK** pour conserver vos modifications, puis dans le volet **étiquette** , cliquez sur **Enregistrer**.
    
    Dans le volet **Azure information protection-étiquettes** , vous voyez maintenant votre nouvelle étiquette affichée avec la colonne **protection** pour indiquer qu’elle contient des paramètres de protection. Ces paramètres de protection s’affichent en tant que modèles pour les applications et services qui prennent en charge le service Azure Rights Management.
    
    Bien que l’étiquette soit activée, par défaut, le modèle est archivé. Afin que les applications et services puissent utiliser le modèle pour protéger des documents et des e-mails, exécutez la dernière étape pour publier le modèle.

5. Dans l’option de menu **classifications**  >  **stratégies** , sélectionnez la stratégie qui doit contenir les nouveaux paramètres de protection. Puis, sélectionnez **Ajouter ou supprimer des étiquettes**. Dans le volet **stratégie : ajouter ou supprimer des étiquettes** , sélectionnez l’étiquette qui vient d’être créée et qui contient vos paramètres de protection, cliquez sur **OK**, puis sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

Il peut prendre jusqu'à 15 minutes pour qu’un ordinateur exécutant le client Azure Information Protection obtienne ces paramètres modifiés. Pour plus d’informations sur la manière dont les ordinateurs et les services téléchargent et actualisent les modèles, consultez l’article [Actualisation des modèles pour les utilisateurs et services](refresh-templates.md).

Tout ce que vous pouvez configurer dans le portail Azure pour créer et gérer vos modèles, vous pouvez le faire à l’aide de PowerShell. En outre, PowerShell fournit davantage d’options qui ne sont pas disponibles dans le portail. Pour plus d’informations, consultez [Référence PowerShell pour les modèles de protection](configure-templates-with-powershell.md). 

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).