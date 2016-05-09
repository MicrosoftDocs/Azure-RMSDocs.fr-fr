---
# required metadata

title: [TITRE DE L’ARTICLE | NOM DU SERVICE]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Métadonnées et modèle Markdown

Ce modèle docs.ms contient des exemples de syntaxe Markdown, ainsi que des conseils sur la définition des métadonnées. Il est disponible dans le répertoire racine de chaque référentiel EM Pilot (par exemple, ~/Azure-RMSDocs-pr
/ template.md) et doit être lu comme un fichier Markdown. Vous pouvez également consulter [la version publiée](https://stage.docs.microsoft.com/en-us/rights-management/template) pour découvrir le rendu des exemples de fichiers Markdown.

Quand vous créez un fichier Markdown, vous devez copier le modèle dans un nouveau fichier, remplir les métadonnées comme indiqué ci-dessous, définir le titre H1 ci-dessus comme titre de l’article et supprimer le contenu. 


## Métadonnées 

Le bloc de métadonnées complet se situe au-dessus, divisé en champs obligatoires et facultatifs. Consultez la [Fiche récapitulative des métadonnées OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) pour plus de détails. Remarques importantes :

- Vous **devez** ajouter un espace entre le signe deux-points (:) et la valeur d’un élément de métadonnées.
- Si un élément de métadonnées facultatif n’a pas de valeur, commentez l’élément avec le signe # (ne le laissez pas vide et n’utilisez pas « n/a »). Si vous ajoutez une valeur à un élément commenté, assurez-vous de supprimer le signe #.
- Le signe deux-points dans une valeur (par exemple, un titre) arrête l’analyseur de métadonnées. À la place, utilisez l’encodage HTML &#58; (par exemple, « title: Azure Rights Management &#58; les principes de base | Azure RMS »).
- **title** : Ce titre s’affiche dans les résultats des moteurs de recherche. Il doit se terminer par une barre verticale (|) suivie du nom du service (voir ci-dessus). Il ne doit pas être identique à votre titre H1. Il doit contenir environ 65 caractères (y compris | NOM DU SERVICE)
- **author**, **manager**, **reviewer** : Le champ author doit contenir le **nom d’utilisateur Github** de l’auteur, pas son alias.  En revanche, les champs « manager » et « reviewer » doivent contenir des alias. ms.reviewer spécifie le nom du PM associé à l’article ou au service.
- **ms.assetid** : Il s’agit du GUID de l’article en majuscules. Quand vous créez un fichier Markdown, obtenez un GUID à partir de [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm** : Des valeurs possibles pour ces éléments se trouvent [ici](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## Formats GFM et Markdown de base

Tous les formats Markdown et Github-flavored Markdown de base sont pris en charge. Pour plus d’informations sur ce sujet, consultez :

- [Syntaxe Markdown de référence](https://daringfireball.net/projects/markdown/syntax)
- [Documentation GFM (Github-Flavored Markdown)](https://guides.github.com/features/mastering-markdown)

## Titres

Des exemples de titres de premier et de deuxième niveau sont présentés ci-dessus. 

Vous ne **pouvez avoir** qu’un seul titre de premier niveau dans votre rubrique, qui sera affiché comme titre sur la page.  

Les titres de deuxième niveau génèrent la table des matières sur la page qui s’affiche dans la section « Dans cet article », en dessous du titre sur la page.

### Titre de troisième niveau
#### Titre de quatrième niveau
##### Titre de cinquième niveau
###### Titre de sixième niveau

## Style du texte

*Italique* 

**Gras** 

~~Barré~~



## Links

Pour créer un lien vers un fichier Markdown dans le même référentiel, utilisez des [liens relatifs](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Exemple : [En quoi consiste Azure Rights Management](./understand-explore/what-is-azure-rms.md)

Pour créer un lien vers un en-tête dans le même fichier Markdown, affichez la source de l’article publié, recherchez l’ID de la tête (par exemple, `id="blockquote"`, et liez-le avec # + ID (par exemple, `#blockquote`).

- Exemple : [Blockquotes](#blockquote)

Pour créer un lien vers un en-tête dans un fichier Markdown dans le même référentiel, utilisez des liaisons relatives + les liaisons par balise de hachage.

- Exemple : [Présentation technique de la procédure d’inscription](./understand-explore/rms-for-individuals-user-sign-up.md#technical-overview-of-the-sign-up-process)

Pour créer un lien vers un fichier externe, utilisez l’URL complète comme lien.

- Exemple : [Github](http://www.github.com)

Si une URL apparaît dans un fichier Markdown, elle est transformée en lien actif.

- Exemple : http://www.github.com

## Listes

### Listes triées

1. Cela 
1. Est
1. Une
1. Liste
1. Triée  


#### Liste triée avec une liste intégrée

1. Voici
1. ici
1. une
1. liste
    1. Mademoiselle Rose
    1. Monsieur Violet
1. intégrée
1. triée


### Listes non triées

- Cela
- est
- une
- liste
- à puces


##### Liste non triée avec une liste intégrée

- Cette 
- liste 
- à puces
    - Madame Pervenche
    - Monsieur Olive
- contient  
- d’autres
    1. listes
    1. Madame Leblanc
- Colonel Moutarde


## Règle horizontale

---

## Tables

| Les tables        | Sont           | Chouettes  |
| ------------- |:-------------:| -----:|
| col 3 est      | alignée à droite | $1600 |
| col 2 est      | centrée      |   $12 |
| col 1 est par défaut | alignée à gauche     |    $1 |


## Code

### CodeBlock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Code en ligne

Il s’agit d’un exemple de `in-line code`.

## Blockquotes

> La sécheresse durait désormais depuis dix millions d’années et le règne des horribles lézards s’était terminé depuis longtemps. Ici au niveau de l’Équateur, sur le continent qui serait un jour connu sous le nom d’Afrique, la lutte pour la vie avait atteint un nouveau paroxysme de férocité et la victoire n’était pas encore en vue. Sur cette terre désertique et desséchée, seul le petit, le rapide ou le féroce pouvait prospérer, ou même espérer survivre.

## Images

### Image statique

![il s’agit du texte de remplacement](./media/AzRMS_elements.png)

### Image liée

[![ail s’agit du texte pour l’image liée](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### GIF animé

![GIF animé](./media/hololens.gif)

## Alertes

### Remarque

> [!NOTE]
> Il s’agit d’une REMARQUE

### Avertissement

> [!WARNING]
> Il s’agit d’un AVERTISSEMENT

### Conseil

> [!TIP]
> Il s’agit d’un CONSEIL

### Important

> [!IMPORTANT]
> Cela est IMPORTANT

## Vidéos

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## extensions docs.ms

### Bouton

> [!div class="button"]
[liens de boutons](/rights-management)

### Sélectionneur

> [!div class="op_single_selector"]
- [aide](/rights-management/template.md)
- [barre](/rights-management/scratch.md)

### Procédure pas à pas

>[!div class="step-by-step"]
[Préc.](https://www.example.com)
[Suivant](https://www.example.com)

<!--HONumber=Apr16_HO3-->


