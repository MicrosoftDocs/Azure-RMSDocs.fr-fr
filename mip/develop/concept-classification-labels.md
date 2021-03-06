---
title: Concepts – Étiquettes de classification
description: Cet article vous aidera à comprendre comment les étiquettes sont utilisées pour la classification des données.
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: b2be24e1703d4831a95feaa51012cf7469a481b7
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556212"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux étiquettes de classification

Dans le cadre d’une stratégie complète de protection des données, les organisations doivent implémenter un système de classification des données qui précise les niveaux de sensibilité des données au sein de l’organisation, puis mapper les attributs des documents à ces classifications.

Les attributs liés à la classification impliquent généralement le **risque** encouru par l’organisation si un document ou des données sont perdus ou consultés par des personnes indésirables. Dans le système de classification usuel de l’État fédéral des États-Unis, il existe trois niveaux de classification. Chacun d’eux a une définition qui décrit quand cette classification doit être appliquée :

* **Top secrète** : s’applique aux informations dont la divulgation non autorisée pourrait raisonnablement causer un préjudice exceptionnellement grave à la sécurité nationale que l’autorité de classification d’origine est en mesure d’identifier ou de décrire.
* **Secrète** : s’applique aux informations dont la divulgation non autorisée pourrait raisonnablement nuire gravement à la sécurité nationale que l’autorité de classification d’origine est en mesure d’identifier ou de décrire.
* **Confidentielle** : s’applique aux informations dont la divulgation non autorisée pourrait raisonnablement nuire à la sécurité nationale que l’autorité de classification d’origine est en mesure d’identifier ou de décrire.
* **Non classifiée** : ce n’est pas réellement une classification, mais plutôt l’absence des trois classifications ci-dessus.

Dans une application du secteur commercial ou privé, nous pouvons définir une liste semblable à la liste par défaut du service Azure Information Protection, avec des valeurs monétaires jointes.

* **Hautement confidentielle** : s’applique aux informations, dont la divulgation non autorisée pourrait raisonnablement entraîner des dommages supérieurs à 1 M USD.
* **Confidentielle** : s’applique aux informations, dont la divulgation non autorisée pourrait raisonnablement entraîner des dommages supérieurs à 100 000 USD.
* **Générale** : s’applique aux informations, dont la divulgation non autorisée pourrait raisonnablement entraîner des dommages mesurables limités.
* **Publique** : s’applique aux informations destinées à une consommation externe publique. 
* **Non professionnelle** : s’applique aux informations qui ne sont pas liées, directement ni indirectement, à l’activité de l’entreprise.

Chaque classification décrit le risque encouru par l’entreprise en cas de divulgation non autorisée de ces informations. Après avoir identifié cette classification et ces conditions, il convient d’identifier les attributs qui aident les propriétaires de données à comprendre quelle classification appliquer.

## <a name="labeling"></a>Étiquetage

Le fait d’associer une classification de données à un ensemble d’informations est appelé **étiquetage**. Étant donné que le kit SDK MIP traite de l’application d’**étiquettes** de classification à des documents, nous ne nous référons pas à des classifications, mais plutôt à des étiquettes. Un utilisateur ou un processus a déjà **classifié** les données en fonction des informations connues : le kit SDK MIP **étiquètera** ensuite les informations.

## <a name="labels-in-the-mip-sdk"></a>Étiquettes dans le kit SDK MIP

Les étiquettes sont un composant fondamental du kit SDK MIP. Les étiquettes définissent l’étiquetage, la protection et le marquage du contenu de tous les documents traités par le kit SDK. Le kit SDK peut :

* Appliquer des étiquettes aux documents
* Lire les étiquettes existantes sur des documents
* Modifier une étiquette existante et exiger une justification si la stratégie le demande
* Supprimer une étiquette d’un document

L’étiquette applique une protection et un marquage du contenu en fonction de l’étiquette de configuration que les administrateurs ont définie dans le Centre de sécurité et conformité. 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label ou mip::ContentLabel

Il existe deux types d’étiquette dans le kit SDK MIP. Voir `Label` et `ContentLabel`.

* Label : étiquette qui peut être appliquée par un utilisateur ou un processus telle qu’elle est définie dans la politique de l’organisation.
* ContentLabel : étiquette qui existe déjà sur un document ou des informations. Elle peut être lue, mise à jour ou supprimée. 

En d’autres termes, l’étiquette `ContentLabel` est une étiquette `Label` qui a été appliquée à des informations.

## <a name="metadata"></a>Metadata

Le kit SDK prend également en charge l’ajout de métadonnées supplémentaires aux documents sous la forme de paires clé/valeur. Si votre organisation a des sous-classifications ou des balises qui décrivent les informations de manière plus spécifique, le kit SDK peut être utilisé pour appliquer ces métadonnées.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le système de classification de l’État fédéral des États-Unis, consultez https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm.
