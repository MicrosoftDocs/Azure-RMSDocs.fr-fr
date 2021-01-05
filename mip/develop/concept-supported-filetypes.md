---
title: Types de fichiers pris en charge-SDK Microsoft Information Protection
description: Détails techniques sur les types de fichiers pris en charge, les extensions de nom de fichier et les niveaux de protection pour les administrateurs qui sont responsables du kit de développement logiciel (SDK) Microsoft Information Protection.
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/16/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: e247a31b364c40f270538d73815464491fca7647
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864853"
---
# <a name="file-types-supported-by-the-microsoft-information-protection-sdk"></a>Types de fichiers pris en charge par le kit de développement logiciel (SDK) Microsoft Information Protection

Le kit de développement logiciel (SDK) Microsoft Information Protection peut appliquer les éléments suivants aux documents et aux e-mails :

- Classification uniquement

- Classification et protection

- Protection uniquement

Le kit de développement logiciel (SDK) Microsoft Information Protection peut également inspecter le contenu de certains types de fichiers à l’aide de types d’informations sensibles connus ou d’expressions régulières que vous définissez.

Utilisez les informations suivantes pour vérifier les types de fichiers pris en charge par le kit de développement logiciel (SDK) Microsoft Information Protection, comprendre les différents niveaux de protection et modifier le niveau de protection par défaut, et pour identifier les fichiers qui sont automatiquement exclus (ignorés) de la classification et de la protection.

## <a name="file-types-supported-for-classification-only"></a>Types de fichiers pris en charge pour la classification uniquement

Vous pouvez classifier les types de fichiers suivants même s’ils ne sont pas protégés.

- **Adobe Portable Document Format** : .pdf

- **Microsoft Project** : .mpp, .mpt

- **Microsoft Publisher** : .pub

- **Microsoft XPS** : .xps .oxps

- **Images** : .jpg, .jpe, .jpeg, .jif, .jfif, .jfi, png, .tif, .tiff

- **Autodesk Design Review 2013** : .dwfx

- **Adobe Photoshop** : .psd

- **Digital Negative** : .dng

- **Microsoft Office**: types de fichiers dans le tableau suivant.

    Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

    | Type de fichier Office                                                                                                                                                                                                                                               | Type de fichier Office                                                                                                                                                                                                                                 |
    | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | .doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd | .vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx |

D’autres types de fichiers prennent en charge la classification quand ils sont aussi protégés. Pour ces types de fichiers, consultez la section [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).

Par exemple, si une étiquette **général**, applique la classification et n’applique pas la protection, vous pouvez appliquer l’étiquette **général** à un fichier nommé sales.pdf, mais vous n’avez pas pu appliquer cette étiquette à un fichier nommé sales.txt.

En outre, si une étiquette **confidentiel \ tous les employés** applique la classification et la protection, vous pouvez appliquer cette étiquette à un fichier nommé sales.pdf et un fichier nommé sales.txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le kit de développement logiciel (SDK) Microsoft Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

| Type de protection     | Natif                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Générique                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Description            | Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).                                                                                                                                                                                                                                                                                       | Pour toutes les autres applications et tous les autres types de fichiers, la protection générique offre un niveau de protection qui comprend l'encapsulation de fichier avec le type de fichier .pfile, et l'authentification, pour vérifier si un utilisateur est autorisé à ouvrir le fichier.                                                                                                                                                                                                                                                                                              |
| Protection             | La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge). | La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués. |
| Protection par défaut selon les types de fichiers | Voici le niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).                                                                                                                                                                              | Il s’agit de la protection par défaut pour tous les autres types de fichiers (comme .vsdx, .rtf, etc.) qui ne sont pas pris en charge par la fonctionnalité de protection native.                                                                                                                                                                                                                                                                                                                                                                                             |

Vous pouvez modifier le niveau de protection par défaut appliqué par le kit de développement logiciel (SDK) Microsoft Information Protection. Vous pouvez modifier le niveau par défaut natif en générique, de générique à natif, et même empêcher le kit de développement logiciel (SDK) Microsoft Information Protection d’appliquer la protection.

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

À compter de Microsoft Information Protection SDK 1,6, la taille maximale du fichier par défaut est de 6 Go. Ce paramètre peut être substitué si nécessaire. Les valeurs par défaut les plus petites pour les plateformes Office héritées s’appliquent toujours.


- **Pour les fichiers Office :**

  | Application Office                                                                                                          | Taille de fichier maximale prise en charge                                                                                                |
  | --------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
  | Word 2007 (pris en charge par AD RMS uniquement)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016                         | 32 bits : 512 Mo<br /><br />64 bits : 512 Mo                                                                                   |
  | Excel 2007 (pris en charge par AD RMS uniquement)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016                     | 32 bits : 2 Go<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles                                            |
  | PowerPoint 2007 (pris en charge par AD RMS uniquement)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles |

- **Pour tous les autres fichiers** :

    Pour protéger d’autres types de fichiers et supprimer la protection sur ces types de fichiers à l’aide du kit de développement logiciel (SDK) : la taille de fichier maximale est limitée uniquement par l’espace disque et la mémoire disponibles.

### <a name="supported-file-types-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

Le tableau suivant répertorie un sous-ensemble de types de fichiers qui prennent en charge la protection native par le kit de développement logiciel (SDK) Microsoft Information Protection et qui peuvent également être classés.

Ces types de fichiers sont identifiés séparément, car quand ils sont protégés en mode natif, l’extension de nom de fichier d’origine change et ces fichiers passent en lecture seule. Notez que quand des fichiers sont protégés de façon générique, l’extension de nom de fichier d’origine est toujours remplacée par .pfile.

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être reconfigurer ces appareils et logiciels réseau pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

| Extension de nom de fichier d'origine | Extension de nom d’un fichier protégé |
| ---------------------------- | ----------------------------- |
| .txt                         | .ptxt                         |
| .xml                         | .pxml                         |
| .jpg                         | .pjpg                         |
| .jpeg                        | .pjpeg                        |
| .pdf                         | .ppdf [[1]](#footnote-1)      |
| .png                         | .ppng                         |
| .tif                         | .ptif                         |
| .tiff                        | .ptiff                        |
| .bmp                         | .pbmp                         |
| .gif                         | .pgif                         |
| .jpe                         | .pjpe                         |
| .jfif                        | .pjfif                        |

###### <a name="footnote-1"></a>Note 1
Avec la dernière version du kit de développement logiciel (SDK) Microsoft Information Protection, l’extension de nom de fichier du document PDF protégé reste au format. pdf.

Le tableau suivant répertorie les types de fichiers restants qui prennent en charge la protection native par le kit de développement logiciel (SDK) Microsoft Information Protection et qui peuvent également être classés. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

| Types de fichiers pris en charge par Office                                                                                                                                                                                                                  | Types de fichiers pris en charge par Office                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm | .vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps |

### <a name="limitations-for-container-files-such-as-zip-msg-files"></a>Limitations pour les fichiers de conteneur, tels que les fichiers. zip et. MSG

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent des fichiers. rar,. 7z,. MSG,. rpmsg et PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur. De même, un fichier conteneur protégé peut être non protégé à l’aide du kit de développement logiciel (SDK), mais la protection (si elle est appliquée) aux fichiers à l’intérieur du conteneur n’est pas supprimée par l’opération de suppression de la protection sur le fichier conteneur de manière récursive. Les développeurs d’applications sont responsables de la récurrence et de la déprotection des fichiers dans les conteneurs.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection.
