---
title: Concepts-nommer les métadonnées dans le kit de développement logiciel MIP
description: Cet article vous aidera à comprendre les métadonnées générées par le kit de développement logiciel (SDK) Microsoft Information Protection.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 3ae27b1bf0b4f709e9621f00b1b3a16c2ba1882c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886133"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>SDK Microsoft Information Protection-métadonnées

Le kit de développement logiciel (SDK) Microsoft Information Protection génère l’ensemble des métadonnées à appliquer à un fichier. Ces métadonnées sont une représentation de l’étiquette. Ce document décrit les métadonnées générées par le kit de développement logiciel (SDK) pour s’appliquer aux courriers électroniques, documents et autres enregistrements.

## <a name="labels"></a>Étiquettes

Les étiquettes dans le kit de développement logiciel (SDK) Microsoft Information Protection sont appliquées aux informations pour décrire la sensibilité de ces informations. Les données d’étiquette sont conservées dans un fichier ou un enregistrement dans un jeu de paires clé-valeur qui décrivent l’étiquette. Le nom des métadonnées repose sur la structure suivante :

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

En cas d’application aux données étiquetées avec Microsoft Information Protection, le résultat est le suivant :

`MSIP_Label_GUID_Enabled = true`

Le GUID est un identificateur unique pour chaque étiquette d’une organisation.

## <a name="microsoft-information-protection-sdk-metadata"></a>Métadonnées du SDK Microsoft Information Protection

Le kit de développement logiciel MIP applique l’ensemble de métadonnées suivant.

| Attribut | Type ou valeur                 | Description                                                                                                                                                                                                                                        | Obligatoire |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Enabled**   | Vrai ou faux                 | Cet attribut indique si la classification représentée par cet ensemble de paires clé-valeur est activée pour l’élément de données. Les produits DLP valident généralement l’existence de cette clé pour identifier l’étiquette de classification. | Oui       |
| **SiteId**    | GUID                          | ID de locataire Azure Active Directory                                                                                                                                                                                                                   | Oui       |
| **ActionId**  | GUID                          | ActionID est modifié chaque fois qu’une étiquette est définie. Les journaux d’audit incluent l’ancien et le nouvel actionID pour permettre le chaînage de l’activité d’étiquetage à l’élément de données.                                                                                 | Oui       |
| **Méthode**    | Standard ou privilégié        | Défini via [MIP :: assignation](reference/mip-enums-and-structs.md#assignmentmethod-enum). Standard signifie que l’étiquette est appliquée par défaut ou automatiquement. Privileged signifie que l’étiquette a été sélectionnée manuellement.                                                                                                                                                                                                                 | Non        |
| **SetDate**   | Format de date ISO 8601 étendu | Horodatage lorsque l’étiquette a été définie.                                                                                                                                                                                                              | Non        |
| **Nom**      | string                        | Nom unique de l’étiquette dans le locataire. Il ne correspond pas nécessairement au nom complet.                                                                                                                                                              | Non      |
| **ContentBits** | integer | Masque de données qui décrit les types de marquage de contenu qui doivent être appliqués à un fichier. CONTENT_HEADER = 0X1, CONTENT_FOOTER = 0X2, filigrane = 0X4, CHIFFREr = 0x8
 | Non |

Lorsqu’il est appliqué à un fichier, le résultat est semblable au tableau ci-dessous.

| Clé                                                         | Value                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_Method      | Privilégié                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | Confidentiel                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-B329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>Extension des métadonnées avec des attributs personnalisés

Les métadonnées personnalisées peuvent être ajoutées par le biais de l’API de fichier et de stratégie. Les attributs personnalisés doivent conserver le préfixe de base `MSIP_Label_GUID`. 

Par exemple, une application écrite par Contoso Corporation doit appliquer des métadonnées indiquant le système qui a généré un fichier étiqueté. L’application peut créer une nouvelle étiquette, précédée de `MSIP_Label_GUID`. Le nom de l’éditeur du logiciel et l’attribut personnalisé sont ajoutés au préfixe pour générer les métadonnées personnalisées.

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> Pour assurer la compatibilité entre les applications courantes, la longueur maximale pour chaque clé et une valeur est de 255 caractères.

## <a name="versioning"></a>Contrôle de version

Au fil du temps, les attributs seront introduits, modifiés ou mis hors service. Il est prévu que les applications continuent à gérer ces attributs anciens ou retirés, car le remplacement de la valeur dans une entreprise peut prendre des années.

Lors du remplacement d’un attribut par une version plus récente, un suffixe de version doit être ajouté à l’attribut :

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>Adresse de messagerie

Les métadonnées appliquées à la messagerie électronique gèrent un format de paire clé/valeur semblable à celui des documents. La principale différence réside dans le fait que tous les attributs sont sérialisés dans un en-tête de message électronique appelé **MSIP_Labels**. Les paires clé/valeur sont délimitées par un point-virgule et un espace blanc, puis placées dans le nouvel en-tête.

Utilisation des exemples de métadonnées ci-dessus :

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
