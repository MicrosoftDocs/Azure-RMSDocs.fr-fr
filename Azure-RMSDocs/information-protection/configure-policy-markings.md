---
title: "Comment configurer des marquages visuels d’une étiquette pour Azure Information Protection | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 78b68c7a502776c6492437e9b8a5c3f1ebf27f95


---

# Comment configurer des marquages visuels d’une étiquette pour Azure Information Protection

>*S’applique à : Azure Information Protection (préversion)*

**[ Cette information est préliminaire et susceptible d'être modifiée. ]**

Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page :

Les marquages visuels sont appliqués à des documents Word, Excel et PowerPoint lorsque l’étiquette est appliquée, et lorsque la documentation est enregistrée. Pour les e-mails, les marquages visuels sont appliqués lorsqu’un e-mail est envoyé.

Informations supplémentaires sur ces marqueurs visuels :

- Les en-têtes et pieds de page s’appliquent à Word, Excel, PowerPoint et Outlook.

- Les filigranes s’appliquent à Word, Excel et PowerPoint :

    - Excel : les filigranes avec Excel sont visibles uniquement en mode Mise en page et Aperçu avant impression, ainsi que lors de l’impression.

    - PowerPoint : les filigranes sont appliqués au masque des diapositives comme image d’arrière-plan.

- Vous pouvez spécifier simplement une chaîne de texte ou utiliser des [variables](#using-variables-in-the-text-string) pour créer dynamiquement la chaîne de texte quand l’en-tête, le pied de page ou le filigrane est appliqué. 

Utilisez les instructions suivantes pour configurer les marquages visuels d’une étiquette.

1. Si vous ne l’avez pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez au panneau **Azure Information Protection**. 
    
    Par exemple, cliquez sur **Parcourir** et commencez à taper **Information** dans la zone Filtrer. Sélectionnez **Azure Information Protection**.

2. Dans le panneau **Azure Information Protection**, sélectionnez l’étiquette que vous souhaitez configurer pour les marquages visuels.

3. Dans le panneau **Étiquette**, dans la section **Définir un marquage visuel (par exemple, un en-tête ou un pied de page)**, configurez les paramètres pour les marquages visuels que vous souhaitez, puis cliquez sur **Enregistrer** :

    - Pour configurer un en-tête : pour **Les documents avec cette étiquette ont un en-tête**, sélectionnez **Activé** si vous souhaitez un en-tête, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et l’alignement de l’en-tête.
    
    - Pour configurer un pied de page : pour **Les documents avec cette étiquette ont un pied de page**, sélectionnez **Activé** si vous souhaitez un pied de page, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et l’alignement du pied de page.
    
    - Pour configurer un filigrane : pour **Les documents avec cette étiquette ont un filigrane**, sélectionnez **Activé** si vous souhaitez un filigrane, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la couleur et la mise en page du filigrane. 

4. Pour que les utilisateurs puissent voir ces modifications, cliquez dans le panneau **Azure Information Protection** sur **Publier**.

## Utilisation de variables dans la chaîne de texte

Vous pouvez utiliser les variables suivantes dans la chaîne de texte pour l’en-tête, le pied de page ou le filigrane :

- `${Item.Label}` pour l’étiquette sélectionnée

- `${Item.Name}` pour le nom de fichier ou l’objet de l’e-mail

- `${Item.Location}` pour le chemin du fichier

- `${User.Name}` pour le propriétaire du document ou de l’e-mail

- `${Event.DateTime}` pour la date et l’heure de la définition de l’étiquette sélectionnée 
    
Exemple : Si vous spécifiez la chaîne `Document: ${item.name} Sensitivity: ${item.label}` pour le pied de page de l’étiquette Secret, le texte du pied de page appliqué à un document nommé project.docx est **Document: project.docx Sensitivity: Secret**.

## Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens figurant dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organization-s-policy).  





<!--HONumber=Aug16_HO2-->


