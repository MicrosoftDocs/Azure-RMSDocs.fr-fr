---
title: "Configurer les marquages visuels d’une étiquette Azure Information Protection"
description: "Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/17/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: 99aba6560f9dcdbd564f317e8d9e0ce89845f4a9
ms.sourcegitcommit: f78f5209f0e19c6edfd1815d76e0e9750b4ce71d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2017
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Comment configurer des marquages visuels d’une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page.

Informations supplémentaires sur ces marqueurs visuels :

- Les en-têtes et pieds de page s’appliquent à Word, Excel, PowerPoint et Outlook.

- Les filigranes s’appliquent à Word, Excel et PowerPoint :

    - Excel : les filigranes avec Excel sont visibles uniquement en mode Mise en page et Aperçu avant impression, ainsi que lors de l’impression.
    
    - PowerPoint : les filigranes sont appliqués au masque des diapositives comme image d’arrière-plan.
    
    - Plusieurs lignes de texte sont prises en charge.

- Vous pouvez spécifier simplement une chaîne de texte ou utiliser des [variables](#using-variables-in-the-text-string) pour créer dynamiquement la chaîne de texte quand l’en-tête, le pied de page ou le filigrane est appliqué.

- Les marquages visuels prennent en charge une seule langue.

## <a name="when-visual-markings-are-applied"></a>Application des marquages visuels

Pour les e-mails, les marquages visuels sont appliqués lorsqu’un e-mail est envoyé depuis Outlook.

Pour les documents, les marquages visuels sont appliqués comme suit :

- Dans une application Office, les marquages visuels d’une étiquette sont appliqués lorsque l’étiquette est appliquée. Les marquages visuels sont également appliqués lors de l’ouverture d’un document étiqueté et lors du premier enregistrement document.  

- Lorsqu’un document est étiqueté à l’aide de l’Explorateur de fichiers ou de PowerShell, les marquages visuels ne sont pas appliqués immédiatement, mais lorsque ce document est ouvert dans une application Office et lors du premier enregistrement du document.

## <a name="to-configure-visual-markings-for-a-label"></a>Pour configurer les marquages visuels pour une étiquette

Utilisez les instructions suivantes pour configurer les marquages visuels d’une étiquette.

1. Si vous ne l’avez pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général. Accédez ensuite au panneau **Azure Information Protection**. 
    
    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer s’applique à tous les utilisateurs, restez dans le panneau **Azure Information Protection - Stratégie globale**.
    
    Si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour s’appliquer uniquement aux utilisateurs sélectionnés, dans la sélection de menu **STRATÉGIES**, sélectionnez **Stratégies délimitées**. Sélectionnez ensuite votre stratégie délimitée dans le panneau **Azure Information Protection - Stratégies délimitées**.

3. Dans le panneau **Étiquette**, dans la section **Définir un marquage visuel (par exemple, un en-tête ou un pied de page)**, configurez les paramètres pour les marquages visuels que vous souhaitez, puis cliquez sur **Enregistrer** :
    
    - Pour configurer un en-tête : pour **Les documents avec cette étiquette ont un en-tête**, sélectionnez **Activé** si vous souhaitez un en-tête, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement de l’en-tête.
    
    - Pour configurer un pied de page : pour **Les documents avec cette étiquette ont un pied de page**, sélectionnez **Activé** si vous souhaitez un pied de page, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement du pied de page.
    
    - Pour configurer un filigrane : pour **Les documents avec cette étiquette ont un filigrane**, sélectionnez **Activé** si vous souhaitez un filigrane, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement du filigrane.

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## <a name="using-variables-in-the-text-string"></a>Utilisation de variables dans la chaîne de texte

Vous pouvez utiliser les variables suivantes dans la chaîne de texte pour l’en-tête, le pied de page ou le filigrane :

- `${Item.Label}` pour l’étiquette sélectionnée. Par exemple : interne

- `${Item.Name}` pour le nom de fichier ou l’objet de l’e-mail. Par exemple : JulySales.docx

- `${Item.Location}` pour le chemin et le nom de fichier des documents, et pour l’objet des e-mails. Par exemple : \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` pour le propriétaire du document ou de l’e-mail, par le nom d’utilisateur connecté à Windows. Par exemple : rsimone

- `${User.PrincipalName}` pour le propriétaire du document ou de l’e-mail, par l’adresse e-mail du client Azure Information Protection connecté (UPN). Par exemple : rsimone@vanarsdelltd.com

- `${Event.DateTime}` pour la date et l’heure de la définition de l’étiquette sélectionnée. Par exemple : 16/08/2016 13:30

Exemple : Si vous spécifiez la chaîne `Document: ${item.name}  Classification: ${item.label}` pour le pied de page de l’étiquette **Général**, le texte du pied de page appliqué à un document nommé project.docx est **Document : project.docx Classification : Général**.

### <a name="setting-the-font-name"></a>Définition du nom de la police

Ce paramètre est actuellement en préversion.

Calibri est la police par défaut pour le texte des en-têtes, pieds de page et filigranes. Si vous spécifiez une autre police, vérifiez qu’elle est disponible sur les appareils clients qui appliqueront les marqueurs visuels. Sinon, la police utilisée sera non déterministe. 

Si vous utilisez la préversion du client Azure Information Protection et que la police spécifiée n’est pas disponible, le client revient à l’utilisation de la police Calibri.

### <a name="setting-the-font-color"></a>Définition de la couleur de la police

Vous pouvez choisir une couleur dans la liste des couleurs disponibles ou spécifier une couleur personnalisée en entrant un code (triplet hexadécimal) représentant les composants RVB (rouge, vert, bleu) de la couleur. Par exemple, **#DAA520**. 

Si vous avez besoin d’informations de référence pour ces codes, l’article [Couleurs par nom](https://msdn.microsoft.com/library/aa358802\(v=vs.85\).aspx) de la documentation MSDN constitue un bon point de départ. Ces codes sont utilisés dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
