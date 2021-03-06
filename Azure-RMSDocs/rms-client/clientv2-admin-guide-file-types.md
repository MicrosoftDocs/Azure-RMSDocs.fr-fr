---
title: Types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection (AIP)
description: En savoir plus sur les types de fichiers et les tailles prises en charge pour le client d’étiquetage unifié Azure Information Protection (AIP) pour Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 22a30abf5ea3bf63e5a352bb8b68ceb852036794
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446913"
---
# <a name="file-types-supported-by-the-azure-information-protection-aip-unified-labeling-client"></a>Types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection (AIP)

>***S’applique à** [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012*>
>
>*Si vous disposez de Windows 7 ou Office 2010, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Concerne**: [client d’étiquetage unifié AIP uniquement](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Pour le client Classic, consultez [types de fichiers client classiques](client-admin-guide-file-types.md)*

Cet article répertorie les types et les tailles de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection (AIP)

> [!NOTE]
> Pour les types de fichiers figurant dans la liste, les emplacements WebDAV ne sont pas pris en charge.
> 
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

    |Type de fichier Office|Type de fichier Office|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|
    | | |

Les autres types de fichiers prennent en charge la classification quand ils sont aussi protégés. Pour ces types de fichiers, consultez la section [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).

Exemples :

- Si l’étiquette de sensibilité **générale** applique la classification et n’applique pas la protection : vous pouvez appliquer l’étiquette **générale** à un fichier nommé sales.pdf mais vous n’avez pas pu appliquer cette étiquette à un fichier nommé sales.txt.

- Si l’étiquette de sensibilité **confidentiel \ tous les employés** applique la classification et la protection : vous pouvez appliquer cette étiquette à un fichier nommé sales.pdf et à un fichier nommé sales.txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le client d’étiquetage unifié Azure Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|**Description**|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour les autres types de fichiers pris en charge, la protection générique fournit un niveau de protection qui inclut à la fois l’encapsulation de fichier à l’aide du type de fichier. pfile et l’authentification pour vérifier si un utilisateur est autorisé à ouvrir le fichier.|
|**Protection**|La protection des fichiers est appliquée comme suit :<br /><br />-Avant que le contenu protégé soit affiché, une authentification réussie doit se produire pour les utilisateurs qui reçoivent le fichier par courrier électronique ou qui y ont accès via des autorisations de fichier ou de partage.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués.|
|**Protection par défaut selon les types de fichiers**|Niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).|Protection par défaut pour tous les autres types de fichiers (tels que. vsdx,. rtf, etc.) qui ne sont pas pris en charge par la protection native.|
| | |

Vous ne pouvez pas modifier le niveau de protection par défaut appliqué par le client d’étiquetage unifié Azure Information Protection ou le scanneur. Toutefois, vous pouvez modifier les types de fichiers protégés. Pour plus d’informations, consultez [modifier les types de fichiers à protéger](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

La protection peut être appliquée automatiquement lorsqu’un utilisateur sélectionne une étiquette de sensibilité qu’un administrateur a configurée, ou que les utilisateurs peuvent spécifier leurs propres paramètres de protection personnalisés à l’aide des [niveaux d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels).

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

La taille maximale des fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection est prise en charge pour la protection.

**Pour les fichiers Office**:

|                                                     Application Office                                                      |                                                Taille de fichier maximale prise en charge                                                 |
|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
|             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bits : 512 Mo<br /><br />64 bits : 512 Mo                                          |
|           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bits : 2 Go<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles                       |
| PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles |
| | |

> [!IMPORTANT]
> Le support étendu d’Office 2010 a pris fin le 13 octobre 2020. Pour plus d’informations, consultez [AIP et versions héritées de Windows et d’Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
>

**Pour tous les autres fichiers** :

- **Pour protéger d’autres types** de fichiers et ouvrir ces types de fichiers dans la visionneuse de Azure information protection : la taille de fichier maximale est limitée uniquement par l’espace disque et la mémoire disponibles.

- **Pour ôter la protection des fichiers** à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) : la taille de fichier maximale prise en charge pour les fichiers. pst est de 5 Go. Les autres types de fichiers sont limités uniquement par l’espace disque et la mémoire disponibles

> [!TIP]
> Pour rechercher ou récupérer des éléments protégés dans des fichiers. PST volumineux, consultez les [conseils pour l’utilisation de Unprotect-RMSFile pour eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).
> 
### <a name="supported-file-types-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

Le tableau suivant répertorie un sous-ensemble de types de fichiers qui prennent en charge la protection native par le client d’étiquetage unifié Azure Information Protection, et qui peuvent également être classés.

Ces types de fichiers sont identifiés séparément, car quand ils sont protégés en mode natif, l’extension de nom de fichier d’origine change et ces fichiers passent en lecture seule. Lorsque les fichiers sont protégés de manière générique, l’extension de nom de fichier d’origine est toujours remplacée par `.p<file-type>` .

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être reconfigurer ces appareils et logiciels réseau pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

|Extension de nom de fichier d'origine|Extension de nom d’un fichier protégé|
|--------------------------------|-------------------------------------|
|.bmp|.pbmp|
|.gif|.pgif|
|.jfif|.pjfif|
|.jpe|.pjpe|
|.jpeg|.pjpeg|
|.jpg|.pjpg|
|.jt|.pjt|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.txt|.ptxt|
|.xla |.pxla | 
|.xlam |.pxlam |
|.xml|.pxml|
| | |

**Types de fichiers pris en charge par Office**

La liste suivante répertorie les types de fichiers restants qui prennent en charge la protection native par le client d’étiquetage unifié Azure Information Protection, et qui peuvent également être classés. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier *reste la même* une fois que le fichier est protégé par un service Rights Management.

:::row:::
   :::column span="4":::
.doc

.docm

.docx

.dot

.dotm

.dotx

.potm

   :::column-end:::
   :::column span="":::

.potx

.pps

.ppsm

.ppsx

.ppt

.pptm

.pptx


   :::column-end:::
   :::column span="":::
.vsdm

.vsdx

.vssm

.vssx

.vstm

.vstx

.xls

   :::column-end:::
   :::column span="":::

.xlsb

.xlt

.xlsm

.xlsx

.xltm

.xltx

.xps
   :::column-end:::
:::row-end:::

## <a name="file-types-excluded-from-classification-and-protection"></a>Types de fichiers exclus de la classification et de la protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. Si les utilisateurs essaient de classer ou de protéger ces fichiers à l’aide du client d’étiquetage unifié Azure Information Protection, ils voient un message indiquant qu’ils sont exclus.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb, .jar

- **Dossiers exclus** :
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData
    - \AppData (pour tous les utilisateurs)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Types de fichiers exclus de la classification et de la protection par le scanneur Azure Information Protection

Par défaut, le scanneur exclut également les mêmes types de fichiers que le client d’étiquetage unifié Azure Information Protection. 

Pour le scanneur, les types de fichiers suivants sont également exclus :. MSG,. rtf et. rar

Pour modifier les types de fichiers inclus ou exclus pour l’inspection des fichiers par le scanneur, configurez les **types de fichiers à analyser** dans le [travail d’analyse du contenu](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).
    
> [!NOTE]
> Si vous incluez des fichiers. rtf pour l’analyse, nous vous recommandons de surveiller attentivement le scanneur. Certains fichiers .rtf ne peuvent pas être inspectés par le scanneur. En effet, pour ces fichiers, l’inspection n’aboutit pas et le service doit être redémarré.

Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Pour modifier ce comportement pour le scanneur, utilisez le paramètre avancé PowerShell **PFileSupportedExtensions**. Pour plus d’informations, consultez [Utiliser PowerShell pour modifier les types de fichiers protégés](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) contre les instructions de déploiement de l’analyseur.

### <a name="files-that-cannot-be-protected-by-default"></a>Fichiers qui ne peuvent pas être protégés par défaut

Tout fichier protégé par mot de passe ne peut pas être protégé en mode natif par le Azure Information Protection client d’étiquetage unifié, sauf si le fichier est actuellement ouvert dans l’application qui applique la protection. Les fichiers PDF protégés par mot de passe sont très courants, mais d’autres applications, comme les applications Office, offrent aussi cette fonctionnalité.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitations pour les fichiers conteneurs, comme les fichiers .zip

Pour plus d’informations, consultez la [Azure information protection problèmes connus](../known-issues.md#client-support-for-container-files-such-as-zip-files).

## <a name="file-types-supported-for-inspection"></a>Types de fichiers pris en charge pour l’inspection

Sans configuration supplémentaire, le Azure Information Protection client d’étiquetage unifié utilise Windows IFilter pour inspecter le contenu des documents. Windows IFilter est utilisé par Windows Search pour l’indexation. Par conséquent, les types de fichiers suivants peuvent être inspectés quand vous utilisez la commande PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) .

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|**Word**|champs docx ;. docm ;. dot ;. dotm ;. dotx|
|**Excel**|.xls ; .xlt ; .xlsx ; .xltx ; .xltm ; .xlsm ; .xlsb|
|**PowerPoint**|.ppt ; .pps ; .pot ; .pptx ; .ppsx ; .pptm ; .ppsm ; .potx ; .potm|
|**PDF** |.pdf|
|**Text**|.txt ; .xml ; .csv|
| | | |

Avec une configuration supplémentaire, d’autres types de fichiers peuvent également être inspectés. Par exemple, vous pouvez [inscrire une extension de nom de fichier personnalisée pour utiliser le gestionnaire de filtres Windows existant pour les fichiers texte](/windows/desktop/search/-search-ifilter-registering-filters)et vous pouvez installer d’autres filtres à partir de fournisseurs de logiciels.

Pour déterminer les filtres qui sont installés, consultez [Recherche d’un gestionnaire de filtre pour une extension de fichier donnée](/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension) dans le guide du développeur de Windows Search.

Les sections suivantes contiennent des instructions de configuration pour inspecter les fichiers .zip et .tiff.

### <a name="to-inspect-zip-files"></a>Pour inspecter les fichiers .zip

Le scanneur Azure Information Protection et la commande PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) permettent d’inspecter les fichiers .zip suivant ces instructions :

1. Pour l’ordinateur exécutant le scanneur ou la session PowerShell, installez [Office 2010 Filter Pack SP2](https://support.microsoft.com/help/2687447/description-of-office-2010-filter-pack-sp2).

2. Pour le scanneur : après avoir trouvé des informations sensibles, si le fichier. zip doit être classifié et protégé par une étiquette, spécifiez l’extension de nom de fichier. zip avec le paramètre PowerShell avancé, **PFileSupportedExtensions**, comme décrit dans [Utiliser PowerShell pour modifier les types de fichiers protégés](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) des instructions de déploiement de l’analyseur.

Exemple de scénario après avoir effectué ces étapes :

Un fichier nommé **accounts.zip** contient des feuilles de calcul Excel avec des numéros de carte de crédit. Vous avez une étiquette de sensibilité nommée **confidentiel \ finance**, qui est configurée pour découvrir les numéros de carte de crédit et appliquer automatiquement l’étiquette avec une protection qui limite l’accès au groupe finance.

Une fois le fichier inspecté, le client d’étiquetage unifié de votre session PowerShell classe ce fichier comme **confidentiel \ finance**, applique la protection générique au fichier afin que seuls les membres des groupes finance puissent le décompresser et renomme le fichier **accounts.zip. pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Pour inspecter des fichiers .tiff à l’aide de la reconnaissance optique de caractères

La commande PowerShell [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) peut utiliser la reconnaissance optique de caractères pour inspecter les images TIFF avec une extension de nom de fichier. TIFF lorsque vous installez la fonctionnalité Windows TIFF IFilter, puis configurer les [paramètres IFilter Windows TIFF](/previous-versions/windows/it-pro/windows-7/dd744701(v=ws.10)) sur l’ordinateur exécutant la session PowerShell.

Pour le scanneur : après avoir trouvé des informations sensibles, si le fichier. TIFF doit être classifié et protégé par une étiquette, spécifiez cette extension de nom de fichier avec le paramètre avancé PowerShell **PFileSupportedExtensions**, comme décrit dans [Utiliser PowerShell pour modifier les types de fichiers protégés](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) des instructions de déploiement de l’analyseur.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d'informations, consultez les pages suivantes :

- [Personnalisations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)