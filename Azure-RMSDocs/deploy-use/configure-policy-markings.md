---
title: "Configurer les marquages visuels d’une étiquette Azure Information Protection"
description: "Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.openlocfilehash: efc60ee6126a6a0b2798f66c46c2242942878829
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Comment configurer des marquages visuels d’une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection*

Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page :

Les marquages visuels sont appliqués à des documents Word, Excel et PowerPoint au moment de l’application de l’étiquette et lorsque la documentation est enregistrée dans ces applications Office. Pour les e-mails, les marquages visuels sont appliqués lorsqu’un e-mail est envoyé depuis Outlook.

Aucun marquage visuel n’est appliqué aux documents dont l’application de l’étiquette intervient à l’aide de l’Explorateur de fichiers et d’un clic droit, ou lorsqu’un document est classé à l’aide de PowerShell.

Informations supplémentaires sur ces marqueurs visuels :

- Les en-têtes et pieds de page s’appliquent à Word, Excel, PowerPoint et Outlook.

- Les filigranes s’appliquent à Word, Excel et PowerPoint :

    - Excel : les filigranes avec Excel sont visibles uniquement en mode Mise en page et Aperçu avant impression, ainsi que lors de l’impression.

    - PowerPoint : les filigranes sont appliqués au masque des diapositives comme image d’arrière-plan.

- Vous pouvez spécifier simplement une chaîne de texte ou utiliser des [variables](#using-variables-in-the-text-string) pour créer dynamiquement la chaîne de texte quand l’en-tête, le pied de page ou le filigrane est appliqué.

Utilisez les instructions suivantes pour configurer les marquages visuels d’une étiquette.

1. Si vous ne l’avez pas déjà fait, dans une nouvelle fenêtre de navigateur, connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur de la sécurité ou administrateur général, puis accédez au panneau **Azure Information Protection**.

    Par exemple, dans le menu du hub, cliquez sur **Autres services** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Si l’étiquette à configurer pour les marquages visuels s’applique à tous les utilisateurs, sélectionnez l’étiquette à changer dans le panneau **Stratégie : Globale**.

     Si l’étiquette à configurer se trouve dans une [stratégie délimitée](configure-policy-scope.md) pour qu’elle s’applique uniquement aux utilisateurs sélectionnés, commencez par sélectionner cette stratégie à partir du panneau **Azure Information Protection** initial.

3. Dans le panneau **Étiquette**, dans la section **Définir un marquage visuel (par exemple, un en-tête ou un pied de page)**, configurez les paramètres pour les marquages visuels que vous souhaitez, puis cliquez sur **Enregistrer** :

    - Pour configurer un en-tête : pour **Les documents avec cette étiquette ont un en-tête**, sélectionnez **Activé** si vous souhaitez un en-tête, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et l’alignement de l’en-tête.

    - Pour configurer un pied de page : pour **Les documents avec cette étiquette ont un pied de page**, sélectionnez **Activé** si vous souhaitez un pied de page, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et l’alignement du pied de page.

    - Pour configurer un filigrane : pour **Les documents avec cette étiquette ont un filigrane**, sélectionnez **Activé** si vous souhaitez un filigrane, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et la mise en page du filigrane.

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

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
