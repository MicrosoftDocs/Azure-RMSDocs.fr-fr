---
title: Concepts - métadonnées d’étiquette dans le SDK MIP
description: Cet article vous aidera à comprendre les métadonnées qui sont générée par le SDK Microsoft Information Protection.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 21148e9293c3be1162028a6cf7e26c30fb52a15f
ms.sourcegitcommit: 2d08bee51c26af3159bd52456e12e0166c8369c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65822174"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK - métadonnées

Le SDK Microsoft Information Protection génère le jeu de métadonnées doivent être appliqué à un fichier. Ces métadonnées sont une représentation de l’étiquette. Ce document décrit les métadonnées que le SDK génère pour appliquer à la messagerie, documents et autres enregistrements.

## <a name="labels"></a>Étiquettes

Étiquettes dans le SDK Microsoft Information Protection sont appliqués aux informations pour décrire la sensibilité de ces informations. Données de l’étiquette sont conservées dans le fichier ou un enregistrement dans un ensemble de paires clé-valeur qui décrivent l’étiquette. Le nom de métadonnées repose sur la structure suivante :

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Lorsqu’il est appliqué aux données étiquetées avec la Protection des informations de Microsoft, le résultat est :

`MSIP_Label_GUID_Enabled = true`

Le GUID est un identificateur unique pour chaque étiquette dans une organisation.

## <a name="microsoft-information-protection-sdk-metadata"></a>Métadonnées de kit de développement logiciel Microsoft Information Protection

Le SDK MIP s’applique à l’ensemble suivant de métadonnées.

| Attribut | Type ou valeur                 | Description                                                                                                                                                                                                                                        | Obligatoire |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Activé**   | True ou False                 | Cet attribut indique si la classification représentée par ce jeu de paires clé-valeur est activée pour l’élément de données. Les produits DLP validez généralement l’existence de cette clé pour identifier l’étiquette de classification. | Oui       |
| **SiteId**    | GUID                          | ID de locataire Azure Active Directory                                                                                                                                                                                                                   | Oui       |
| **ActionId**  | GUID                          | ActionID est modifié chaque fois qu’une étiquette est définie. Journaux d’audit inclura les ancien et nouveaux actionID pour autoriser le chaînage de l’étiquetage d’activité à l’élément de données.                                                                                 | Oui       |
| **Méthode**    | Standard ou privilégié        | Définir [mip::AssignmentMethod](reference/mip-enums-and-structs.md#assignmentmethod). Standard implique que l’étiquette est appliquée par défaut, ou automatiquement. Privilèges implique que l’étiquette a été sélectionné manuellement.                                                                                                                                                                                                                 | Non        |
| **SetDate**   | Format de Date étendues ISO 8601 | Horodateur de l’étiquette a été définie.                                                                                                                                                                                                              | Non        |
| **Nom**      | chaîne                        | Nom unique au sein du client. Il ne correspond pas nécessairement pour nom d’affichage.                                                                                                                                                              | Non      |
| **ContentBits** | entier | Masque de bits qui décrit les types de contenu de marquage qui doit être appliqué à un fichier. CONTENT_HEADER = 0 X 1, CONTENT_FOOTER = 0 X 2, FILIGRANE = 0 X 4, CHIFFRER = 0 X 8
 | Non |

Lorsqu’il est appliqué à un fichier, le résultat est similaire à la table ci-dessous.

| Touche                                                         | Value                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | Privilégié                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | Confidentiel                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>Extension des métadonnées avec des attributs personnalisés

Métadonnées personnalisées peuvent être ajoutées via l’API de stratégie et de fichier. Attributs personnalisés doivent conserver la base de `MSIP_Label_GUID` préfixe. 

Par exemple, une application écrite par Contoso Corporation doit appliquer les métadonnées indiquant quel système a généré un fichier étiqueté. L’application peut créer une nouvelle étiquette, le préfixe `MSIP_Label_GUID`. Le nom de fournisseur et un attribut personnalisé sont ajoutés au préfixe pour générer des métadonnées personnalisées.

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> Pour assurer la compatibilité entre applications courantes, la longueur maximale pour chaque une clé et une valeur est de 255 caractères.

## <a name="versioning"></a>Contrôle de version

Au fil du temps, les attributs seront être introduits, modifiés ou mis hors service. Il est probable que les applications de continuer à gérer ces anciennes ou attributs mis hors service, comme en remplaçant la valeur dans une entreprise peuvent prendre des années.

Lors du remplacement d’un attribut avec une version plus récente, un suffixe de version doit être ajouté à l’attribut :

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>E-mail

Métadonnées appliquées à la messagerie tient à jour une paire clé/valeur de format similaire à celle des documents. La principale différence est que tous les attributs sont sérialisés dans à un en-tête d’e-mail unique appelé **MSIP_Labels**. Les paires clé/valeur sont séparées par un point-virgule et un espace blanc et placés dans le nouvel en-tête.

À l’aide de l’exemple de métadonnées ci-dessus :

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
