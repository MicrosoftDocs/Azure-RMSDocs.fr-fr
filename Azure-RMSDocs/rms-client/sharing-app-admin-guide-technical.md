---
title: Vue d’ensemble technique de l’application de partage RMS - AIP
description: Détails techniques destinés aux administrateurs de réseaux d’entreprise en charge du déploiement de l’application de partage RMS pour Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/02/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8556bb8e2ba5df713b925cbb05628c73284b3df1
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393869"
---
# <a name="technical-overview-and-protection-details-for-the-microsoft-rights-management-sharing-application"></a>Présentation technique de l’application de partage Microsoft Rights Management et détails sur la protection

>*S’applique à : Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 avec SP1, Windows 8, Windows 8.1*


L'application de partage Microsoft Rights Management est une application téléchargeable facultative pour Microsoft Windows et d’autres plateformes. Elle offre les fonctionnalités suivantes :

-   Protection d’un seul fichier ou protection en bloc de plusieurs fichiers, ainsi que de tous les fichiers d’un dossier sélectionné

-   Prise en charge intégrale de la protection de tous les types de fichier et intégration d’une visionneuse pour les types de fichier texte et image couramment utilisés

-   Protection générique des fichiers qui ne prennent pas en charge la protection RMS.

-   Interopérabilité complète avec les fichiers protégés à l'aide de la Gestion des droits relatifs à l'information (IRM).

-   Interopérabilité complète avec les fichiers PDF protégés à l’aide de l’Infrastructure de classification des fichiers (ICF) et des outils de création de fichiers PDF pris en charge.

L’application de partage Microsoft Rights Management utilise le [runtime du client AD RMS 2.1](https://www.microsoft.com/download/details.aspx?id=38396). Grâce aux fonctionnalités d'AD RMS 2.1, l'application de partage Microsoft Rights Management fournit aux utilisateurs finaux une expérience simple de protection et de consommation.

Avec la version d’octobre 2013 de RMS, vous pouvez protéger des documents en mode natif à l’aide d’Office 2010 et les envoyer à des personnes d’une autre entreprise, celles-ci pouvant alors utiliser le service Azure Rights Management d’Azure Information Protection. En outre, avec cette version, si vous utilisez AD RMS en mode de chiffrement 2, vous pouvez utiliser RMS for Individuals et utiliser du contenu provenant de personnes d’une autre entreprise utilisant le service Azure Rights Management. Pour plus d’informations sur le mode de chiffrement 2, voir [Modes de chiffrement AD RMS](https://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

Pour obtenir des informations sur le déploiement, consultez [Déploiement automatique de l’application de partage Microsoft Rights Management](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application).

## <a name="levels-of-protection--native-and-generic"></a>Niveaux de protection : natif et générique
L’application de partage Microsoft Rights Management prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.


|   Type de protection   |                                                                                                                                                                                                                                                                             Natif                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                            Générique                                                                                                                                                                                                                                                                             |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Description       |                                                                                                                                    Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).                                                                                                                                     |                                                                                                                                                              Pour toutes les autres applications et tous les autres types de fichier, la protection générique fournit un niveau de protection qui inclut à la fois l’encapsulation de fichier avec le type de fichier .pfile et l’authentification pour déterminer si un utilisateur est autorisé à ouvrir le fichier.                                                                                                                                                              |
|       Protection       | Les fichiers sont entièrement chiffrés et la protection est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation, définis par le propriétaire du contenu quand les fichiers sont protégés, sont entièrement appliqués quand le contenu est affiché dans IP Viewer (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge). | La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- Un enregistrement d’audit des utilisateurs autorisés qui ouvrent les fichiers et qui y accèdent est réalisé, mais aucun droit d’utilisation n’est appliqué par les applications qui ne prennent pas cette fonctionnalité en charge. |
| Valeur par défaut pour les types de fichier |                                                                                         Il s'agit du niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichier pris en charge et extensions de nom de fichier](#supported-file-types-and-file-name-extensions).                                                                                         |                                                                                                                                                                                                              Il s’agit de la protection par défaut pour tous les autres types de fichier (comme .vsdx, .rtf, etc.), qui ne sont pas pris en charge par la fonctionnalité de protection complète.                                                                                                                                                                                                               |

Vous pouvez modifier le niveau de protection par défaut appliqué par l'application de partage RMS. Vous pouvez remplacer le niveau de protection native par défaut par une protection générique, et inversement, et même empêcher que l'application de partage RMS n'applique la protection. Pour plus d’informations, consultez la section [Modification du niveau de protection par défaut des fichiers](#changing-the-default-protection-level-of-files) dans cet article.

## <a name="supported-file-types-and-file-name-extensions"></a>Types de fichier pris en charge et extensions de nom de fichier
Le tableau suivant répertorie les types de fichier pris en charge en mode natif par l'application de partage Microsoft Rights Management. Pour ces types de fichier, l'extension de nom de fichier d'origine est modifiée lorsque la protection native est appliquée, et ces fichiers sont alors en lecture seule.

En outre, quand l'application de partage RMS protège en mode natif un fichier Word, Excel ou PowerPoint que les utilisateurs protègent par le partage, cette action crée automatiquement un deuxième fichier, qui est une copie du fichier d'origine avec le même nom, mais avec une extension de nom de fichier **.ppdf** ¹. Cette version du fichier permet de garantir que les destinataires qui installent l'application de partage RMS peuvent toujours ouvrir le fichier auquel une protection native est appliquée.

Pour les fichiers protégés de manière générique, l'extension de nom de fichier d'origine est toujours remplacée par .pfile.

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être les reconfigurer pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

| Extension de nom de fichier d'origine | Extension de nom d'un fichier protégé par RMS |
|------------------------------|-----------------------------------|
|             .txt             |               .ptxt               |
|             .xml             |               .pxml               |
|             .jpg             |               .pjpg               |
|            .jpeg             |               .pjeg               |
|             .pdf             |               .ppdf               |
|             .png             |               .ppng               |
|             .tif             |               .ptif               |
|            .tiff             |              .ptiff               |
|             .bmp             |               .pbmp               |
|             .gif             |               .pgif               |
|             .jpe             |               .pjpe               |
|            .jfif             |              .pjfif               |
|             .jt              |               .pjt                |

¹ Rendu PDF avec Foxit. Copyright © 2003-2014 Foxit Corporation.

Le tableau suivant répertorie les types de fichier pris en charge en mode natif par l’application de partage Microsoft Rights Management dans Microsoft Office 2016, Office 2013 et Office 2010. Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichier pris en charge par Office|Types de fichier pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modification du niveau de protection par défaut des fichiers
Vous pouvez modifier la façon dont l'application de partage RMS protège les fichiers en modifiant le Registre. Par exemple, vous pouvez forcer les fichiers qui prennent en charge la protection native à être protégés de manière générique par l'application de partage RMS.

Raisons pour lesquelles vous pourriez vouloir procéder ainsi :

-   Pour vous assurer que tous les utilisateurs peuvent ouvrir le fichier à partir de leurs appareils mobiles.

-   Pour vous assurer que tous les utilisateurs peuvent ouvrir le fichier s'ils ne possèdent pas d'application prenant en charge la protection native.

-   Pour tenir compte des systèmes de sécurité qui agissent sur les fichiers selon leur extension de nom de fichier et peuvent être reconfigurés pour prendre en charge l'extension de nom de fichier .pfile, mais ne peuvent pas être reconfigurés pour prendre en charge plusieurs extensions de nom de fichier pour la protection native.

De même, vous pouvez forcer l'application de partage RMS à appliquer une protection native aux fichiers qui auraient une protection générique par défaut. Cela peut être approprié si vous avez une application qui prend en charge les API RMS, par exemple une application métier écrite par vos développeurs internes ou une application achetée auprès d'un éditeur de logiciels indépendant.

Vous pouvez également forcer l'application de partage RMS à bloquer la protection des fichiers (ne pas appliquer de protection native ou générique). Par exemple, cela peut être nécessaire si vous avez une application automatisée ou un service qui doit être en mesure d'ouvrir un fichier spécifique pour traiter son contenu. Quand vous bloquez la protection pour un type de fichier particulier, les utilisateurs ne peuvent pas utiliser l'application de partage RMS pour protéger les fichiers de ce type. Quand ils essaient de le faire, un message indiquant que l'administrateur a empêché la protection s'affiche, et ils doivent annuler leur action pour protéger le fichier.

Pour configurer l'application de partage RMS afin qu'elle applique une protection générique à tous les fichiers qui auraient par défaut une protection native, apportez les modifications suivantes au Registre. Notez que, si les clés RmsSharingApp ou FileProtection n’existent pas, vous devez les créer manuellement.

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection** : Créez une clé nommée *.

    Ce réglage désigne les fichiers avec une extension de nom de fichier quelconque.

2.  Dans la clé nouvellement ajoutée HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\\\*, créez une valeur de chaîne (REG_SZ) nommée **Encryption** avec la valeur de données **Pfile**.

    Ce réglage entraîne l'application de la protection générique par l'application de partage RMS.

Ces deux réglages entraînent l'application de la protection générique par l'application de partage RMS à tous les fichiers ayant une extension de nom de fichier. Si c'est l'objectif que vous recherchez, aucune configuration supplémentaire n'est requise. Toutefois, vous pouvez définir des exceptions pour des types de fichier spécifiques, afin qu'ils soient protégés en mode natif. Pour cela, vous devez effectuer trois modifications supplémentaires dans le Registre pour chaque type de fichier :

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection** : Ajoutez une nouvelle clé qui porte le nom de l'extension de nom de fichier (sans le point qui précède).

    Par exemple, pour les fichiers qui ont une extension de nom de fichier .docx, créez une clé nommée **DOCX**.

2.  Dans la clé nouvellement ajoutée (par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**), créez une valeur DWORD nommée **AllowPFILEEncryption** avec la valeur **0**.

3.  Dans la clé de type de fichier nouvellement ajoutée, par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**, créez une valeur de chaîne nommée **Encryption** avec la valeur **Native**.

Suite à ces réglages, tous les fichiers sont protégés de façon générique, à l'exception des fichiers qui ont une extension de nom de fichier .docx, qui sont protégés en mode natif par l'application de partage RMS.

Répétez ces trois étapes pour les autres types de fichier que vous souhaitez définir en tant qu'exceptions car ils prennent en charge la protection native et vous ne souhaitez pas qu'ils soient protégés de manière générique par l'application de partage RMS.

Vous pouvez apporter des modifications similaires au Registre pour d'autres scénarios en modifiant la valeur de la chaîne **Encryption** qui prend en charge les valeurs suivantes :

-   **Pfile** : Protection générique

-   **Natif** : Protection native

-   **Désactivé** : Bloquer la protection

## <a name="see-also"></a>Voir aussi
[Guide d’utilisation de l’application de partage Rights Management](sharing-app-user-guide.md)

