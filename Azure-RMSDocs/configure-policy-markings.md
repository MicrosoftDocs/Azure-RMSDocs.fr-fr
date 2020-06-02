---
title: Configurer les marquages visuels d’une étiquette Azure Information Protection – AIP
description: Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: a0a0f5e712c0313b281fc2bafa64719ed61d2e03
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84249859"
---
# <a name="how-to-configure-a-label-for-visual-markings-for-azure-information-protection"></a>Comment configurer des marquages visuels d’une étiquette pour Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>[!NOTE]
> Pour fournir une expérience client unifiée et rationalisée, **Azure Information Protection client (Classic)** et **Gestion des étiquettes** dans le Portail Azure sont **dépréciées** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Lorsque vous affectez une étiquette à un document ou un e-mail, vous pouvez sélectionner plusieurs options pour que la classification choisie soit facilement visible. Ces marquages visuels sont un filigrane, un en-tête et un pied de page.

Informations supplémentaires sur ces marquages visuels :

- Les en-têtes et pieds de page s’appliquent à Word, Excel, PowerPoint et Outlook.

- Les filigranes s’appliquent à Word, Excel et PowerPoint :

    - Excel : les filigranes avec Excel sont visibles uniquement en mode Mise en page et Aperçu avant impression, ainsi que lors de l’impression.

    - PowerPoint : les filigranes sont appliqués au masque des diapositives comme image d’arrière-plan. Sur l’onglet **Affichage**, **Masque des diapositives**, vérifiez que la case à cocher **Masquer les graphiques en arrière-plan** n’est pas sélectionnée.

- Il est possible d’ajouter plusieurs lignes dans les filigranes, ainsi que dans les en-têtes et les pieds de page dans Word, Excel et PowerPoint. Si plusieurs lignes sont spécifiées dans l’en-tête ou le pied de page appliqué à Outlook d’une étiquette, les lignes sont concaténées. Dans ce cas de figure, vous pouvez utiliser la configuration permettant de [définir des marquages visuels différents pour Word, Excel, PowerPoint et Outlook](#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook).

- Longueurs de chaînes maximales :

    - La longueur de chaîne maximale que vous pouvez entrer pour les en-têtes et pieds de page est de 1 024 caractères. Toutefois, Excel a une limite totale de 255 caractères pour les en-têtes et pieds de page. Cette limite inclut des caractères qui ne sont pas visibles dans Excel, comme les codes de mise en forme. Si cette limite est atteinte, la chaîne que vous entrez n’est pas affichée dans Excel.

    - La longueur de chaîne maximale pour les filigranes que vous pouvez entrer est de 255 caractères.

- Vous pouvez spécifier simplement une chaîne de texte ou utiliser des [variables](#using-variables-in-the-text-string) pour créer dynamiquement la chaîne de texte quand l’en-tête, le pied de page ou le filigrane est appliqué.

- Word, PowerPoint, Outlook et maintenant Excel prennent en charge les marquages visuels de différentes couleurs.

- Les marquages visuels prennent en charge une seule langue.

## <a name="when-visual-markings-are-applied"></a>Application des marquages visuels

Pour les e-mails, les marquages visuels sont appliqués lorsqu’un e-mail est envoyé depuis Outlook. Si cet e-mail fait l’objet d’un transfert ou d’une réponse avec une modification d’étiquette, les marquages visuels d’origine sont conservés.

Pour les documents, les marquages visuels sont appliqués comme suit :

- Dans une application Office, les marquages visuels d’une étiquette sont appliqués lorsque l’étiquette est appliquée. Les marquages visuels sont également appliqués lors de l’ouverture d’un document étiqueté et lors du premier enregistrement document.  

- Lorsqu’un document est étiqueté à l’aide de l’Explorateur de fichiers, de PowerShell ou du scanneur Azure Information Protection, les marquages visuels ne sont pas appliqués immédiatement, mais le sont par le client Azure Information Protection lorsque ce document est ouvert dans une application Office et lors du premier enregistrement du document.

    La seule exception est quand vous utilisez l' [enregistrement automatique](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) avec les applications Office pour les fichiers qui sont enregistrés dans Microsoft SharePoint, onedrive entreprise ou scolaire, ou onedrive à la page : lorsque l’enregistrement automatique est activé, les marquages visuels ne sont pas appliqués, sauf si vous configurez le [paramètre client avancé](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) pour activer la classification en continu en arrière-plan. 

## <a name="to-configure-visual-markings-for-a-label"></a>Pour configurer les marquages visuels pour une étiquette

Utilisez les instructions suivantes pour configurer les marquages visuels d’une étiquette.

1. Si ce n’est pas déjà fait, ouvrez une nouvelle fenêtre de navigateur et [connectez-vous au Portail Azure](configure-policy.md#signing-in-to-the-azure-portal). Accédez ensuite au volet **Azure Information Protection**. 
    
    Par exemple, dans la zone de recherche pour ressources, services et docs : commencez à taper les **informations** et sélectionnez **Azure information protection**.

2. À partir de l’option de menu **classifications**  >  **étiquettes** : dans le volet **Azure information protection-étiquettes** , sélectionnez l’étiquette qui contient les marquages visuels que vous souhaitez ajouter ou modifier.

3. Dans le volet **étiquette** , dans la section **définir le marquage visuel (par exemple, un en-tête ou un pied de page)** , configurez les paramètres des marquages visuels que vous souhaitez, puis cliquez sur **Enregistrer**:
    
    - Pour configurer un en-tête : pour **Les documents avec cette étiquette ont un en-tête**, sélectionnez **Activé** si vous souhaitez un en-tête, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement de l’en-tête.
    
    - Pour configurer un pied de page : pour **Les documents avec cette étiquette ont un pied de page**, sélectionnez **Activé** si vous souhaitez un pied de page, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement du pied de page.
    
    - Pour configurer un filigrane : pour **Les documents avec cette étiquette ont un filigrane**, sélectionnez **Activé** si vous souhaitez un filigrane, et **Désactivé** si ce n’est pas le cas. Si vous sélectionnez **Activé**, spécifiez ensuite le texte, la taille, la [police](#setting-the-font-name), la [couleur](#setting-the-font-color) et l’alignement du filigrane.
    
Quand vous cliquez sur **Enregistrer**, vos modifications sont automatiquement disponibles pour les utilisateurs et les services. Il n’y a plus d’option de publication distincte.


## <a name="using-variables-in-the-text-string"></a>Utilisation de variables dans la chaîne de texte

Les variables suivantes sont généralement disponibles lors de l’utilisation de Azure Information Protection client classique et sont en version préliminaire publique lors de l’utilisation du client d’étiquetage unifié Azure Information Protection.  

Vous pouvez utiliser les variables suivantes dans la chaîne de texte pour l’en-tête, le pied de page ou le filigrane :

- `${Item.Label}` pour l’étiquette sélectionnée. Par exemple : Général

- `${Item.Name}` pour le nom de fichier ou l’objet de l’e-mail. Par exemple : JulySales.docx

- `${Item.Location}` pour le chemin et le nom de fichier des documents, et pour l’objet des e-mails. Par exemple : \\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` pour le propriétaire du document ou de l’e-mail, par le nom d’utilisateur connecté à Windows. Par exemple : rsimone 

- `${User.PrincipalName}` pour le propriétaire du document ou de l’e-mail, par l’adresse e-mail du client Azure Information Protection connecté (UPN). Par exemple : rsimone@vanarsdelltd.com

- `${Event.DateTime}` pour la date et l’heure de la définition de l’étiquette sélectionnée. Par exemple : 16/08/2016 13:30

> [!NOTE]
>Cette syntaxe respecte la casse. Par exemple, si vous spécifiez la chaîne `Document: ${Item.Name}  Classification: ${Item.Label}` pour le pied de page de l’étiquette **générale** , le texte du pied de page appliqué à un document nommé Project. docx sera **document : Project. docx classification : général**.

<!-- REMOVED w JUNE 2020 RELEASE> [!NOTE]
> Use of either the `${User.Name}` and/or `${User.PrincipalName}` variable are currently not supported by the Azure Information Protection unified labeling client. 
-->
>[!TIP]
> Vous pouvez également utiliser un [Code de champ pour insérer le nom de l’étiquette](faqs-infoprotect.md#can-i-create-a-document-template-that-automatically-includes-the-classification) dans un document ou un modèle.

## <a name="setting-different-visual-markings-for-word-excel-powerpoint-and-outlook"></a>Définition de marquages visuels différents pour Word, Excel, PowerPoint et Outlook

Par défaut, les marquages visuels que vous spécifiez sont appliqués dans Word, Excel, PowerPoint et Outlook. Toutefois, vous pouvez spécifier des marquages visuels par type d’application Office lorsque vous utilisez une instruction de variable « If.App » dans la chaîne de texte et identifier le type d’application en utilisant les valeurs **Word**, **Excel**, **PowerPoint**, ou **Outlook**. Vous pouvez également abréger ces valeurs, ce qui est nécessaire si vous souhaitez en spécifier plusieurs dans la même instruction If.App.

Utilisez la syntaxe suivante :

    ${If.App.<application type>}<your visual markings text> ${If.End}

> [!NOTE]
>La syntaxe de cette instruction respecte la casse.

Exemples :

- **Définir un texte d’en-tête pour les documents Word uniquement :**
    
    `${If.App.Word}This Word document is sensitive ${If.End}`
    
    Dans les en-têtes de document Word uniquement, l’étiquette applique le texte d’en-tête « Ce document Word respecte la casse ». Aucun texte d’en-tête n’est appliqué à d’autres applications Office.

- **Définir un texte de pied de page pour Word, Excel et Outlook et un texte de pied de page différent pour PowerPoint :**
    
    `${If.App.WXO}This content is confidential. ${If.End}${If.App.PowerPoint}This presentation is confidential. ${If.End}`
    
    Dans Word, Excel et Outlook, l’étiquette applique le texte de pied de page « Ce contenu est confidentiel. » Dans PowerPoint, l’étiquette applique le texte de pied de page « Cette présentation est confidentielle ».

- **Définir un texte en filigrane spécifique pour Word et PowerPoint et un texte en filigrane pour Word, Excel et PowerPoint :**
    
    `${If.App.WP}This content is ${If.End}Confidential`
    
    Dans Word et PowerPoint, l’étiquette applique le texte en filigrane « Ce contenu est confidentiel ». Dans Excel, l’étiquette applique le texte en filigrane « Confidentiel ». Dans Outlook, l’étiquette n’applique pas de texte en filigrane, car les filigranes comme les marquages visuels ne sont pas pris en charge pour Outlook.

> [!NOTE]
> Lorsque vous utilisez le client d’étiquetage unifié Azure Information Protection, la définition des valeurs pour le nom de la **police** est possible uniquement à l’aide du portail Azure information protection. Lorsque vous définissez des valeurs pour la **couleur de police** au-delà de l’une des cinq valeurs par défaut, est également possible uniquement à l’aide du portail Azure information protection.

### <a name="setting-the-font-name"></a>Définition du nom de la police

Calibri est la police par défaut pour le texte des en-têtes, pieds de page et filigranes. Si vous spécifiez une autre police, vérifiez qu’elle est disponible sur les appareils clients qui appliqueront les marquages visuels. 

Si la police spécifiée n’est pas disponible, le client utilise la police Calibri.

### <a name="setting-the-font-color"></a>Définition de la couleur de la police

Vous pouvez choisir une couleur dans la liste des couleurs disponibles ou spécifier une couleur personnalisée en entrant un code (triplet hexadécimal) représentant les composants RVB (rouge, vert, bleu) de la couleur. Par exemple, **#40e0d0** est la valeur hexadécimale RVB pour turquoise. 

Si vous avez besoin d’une référence pour ces codes, vous trouverez une table utile à partir de la [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) page des documents Web MSDN. Vous trouverez également ces codes dans de nombreuses applications qui vous permettent de modifier des images. Par exemple, Microsoft Paint vous permet de choisir une couleur personnalisée dans une palette et de copier les valeurs RVB qui sont automatiquement affichées.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la configuration de votre stratégie Azure Information Protection, utilisez les liens dans la section [Configuration de la stratégie de votre organisation](configure-policy.md#configuring-your-organizations-policy).  

