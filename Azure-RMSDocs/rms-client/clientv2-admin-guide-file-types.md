---
title: Types de fichiers pris en charge-Azure Information Protection client d’étiquetage unifié
description: Détails techniques sur les types de fichiers pris en charge, les extensions de nom de fichier et les niveaux de protection pour les administrateurs qui sont responsables de l’Azure Information Protection client d’étiquetage unifié pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ce3325b507aaee3b5c4ab207e23875dfb42e395f
ms.sourcegitcommit: 3464f9224b34dc54ad6fc1b7bc4dc11ad1ab8d59
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984865"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows server 2008 R2*>
>
> *Instructions pour : [Azure information protection client d’étiquetage unifié pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Le client d’étiquetage unifié Azure Information Protection peut appliquer les éléments suivants aux documents et aux e-mails :

- Classification uniquement

- Classification et protection

- Protection uniquement

Le client d’étiquetage unifié Azure Information Protection peut également inspecter le contenu de certains types de fichiers à l’aide de types d’informations sensibles connus ou d’expressions régulières que vous définissez.

Utilisez les informations suivantes pour vérifier les types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection, comprendre les différents niveaux de protection et modifier le niveau de protection par défaut et identifier les fichiers qui sont automatiquement exclu (ignoré) de la classification et de la protection.

Pour les types de fichiers figurant dans la liste, les emplacements WebDAV ne sont pas pris en charge.

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

- **Microsoft Office** : types de fichiers dans le tableau suivant.

    Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

    |Type de fichier Office|Type de fichier Office|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

D’autres types de fichiers prennent en charge la classification quand ils sont aussi protégés. Pour ces types de fichiers, consultez la section [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).

Exemples :

- Si l’étiquette de sensibilité **générale** applique la classification et n’applique pas la protection : vous pouvez appliquer l’étiquette **générale** à un fichier nommé Sales. pdf, mais vous n’avez pas pu appliquer cette étiquette à un fichier nommé Sales. txt. 

- Si l’étiquette de sensibilité **confidentiel \ tous les employés** applique la classification et la protection : vous pouvez appliquer cette étiquette à un fichier nommé Sales. pdf et à un fichier nommé Sales. txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le client d’étiquetage unifié Azure Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|Description|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour toutes les autres applications et tous les autres types de fichiers, la protection générique offre un niveau de protection qui comprend l'encapsulation de fichier avec le type de fichier .pfile, et l'authentification, pour vérifier si un utilisateur est autorisé à ouvrir le fichier.|
|Protection|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués.|
|Protection par défaut selon les types de fichiers|Voici le niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).|Il s’agit de la protection par défaut pour tous les autres types de fichiers (comme .vsdx, .rtf, etc.) qui ne sont pas pris en charge par la fonctionnalité de protection native.|

Vous ne pouvez pas modifier le niveau de protection par défaut appliqué par le client d’étiquetage unifié Azure Information Protection ou le scanneur. Toutefois, vous pouvez modifier les types de fichiers protégés. Pour plus d’informations, consultez [modifier les types de fichiers à protéger](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

La protection peut être appliquée automatiquement lorsqu’un utilisateur sélectionne une étiquette de sensibilité qu’un administrateur a configurée, ou que les utilisateurs peuvent spécifier leurs propres paramètres de protection personnalisés à l’aide des [niveaux d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

La taille maximale des fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection est prise en charge pour la protection.

- **Pour les fichiers Office :**


  |                                                     Application Office                                                      |                                                Taille de fichier maximale prise en charge                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bits : 512 Mo<br /><br />64 bits : 512 Mo                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bits : 2 Go<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles<br /><br />64 bits : limité uniquement par l’espace disque disponible et la mémoire disponibles |


- **Pour tous les autres fichiers** : 

  - Pour protéger d’autres types de fichiers et ouvrir ces types de fichiers dans la visionneuse Azure Information Protection : la taille de fichier maximale est limitée uniquement par l’espace disque et la mémoire disponibles.

  - Pour ôter la protection de fichiers à l’aide de la cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) : la taille de fichier maximale prise en charge pour les fichiers .pst est de 5 Go. Les autres types de fichiers sont limités uniquement par l’espace disque et la mémoire disponibles

    Conseil : Si vous avez besoin de rechercher ou de récupérer des éléments protégés dans des fichiers .pst volumineux, consultez [Conseils d’utilisation d’Unprotect-RMSFile pour eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

Le tableau suivant répertorie un sous-ensemble de types de fichiers qui prennent en charge la protection native par le client d’étiquetage unifié Azure Information Protection, et qui peuvent également être classés. 

Ces types de fichiers sont identifiés séparément, car quand ils sont protégés en mode natif, l’extension de nom de fichier d’origine change et ces fichiers passent en lecture seule. Notez que quand des fichiers sont protégés de façon générique, l’extension de nom de fichier d’origine est toujours remplacée par .pfile.

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être reconfigurer ces appareils et logiciels réseau pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

|Extension de nom de fichier d'origine|Extension de nom d’un fichier protégé|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

Le tableau suivant répertorie les types de fichiers restants qui prennent en charge la protection native par le client d’étiquetage unifié Azure Information Protection, et qui peuvent également être classés. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichiers pris en charge par Office|Types de fichiers pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Types de fichiers exclus de la classification et de la protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. Si les utilisateurs essaient de classer ou de protéger ces fichiers à l’aide du client d’étiquetage unifié Azure Information Protection, ils voient un message indiquant qu’ils sont exclus.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msg, .msp, .msi, .pdb, .jar


- **Dossiers exclus** : 
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData 
    - \AppData (pour tous les utilisateurs)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Types de fichiers exclus de la classification et de la protection par le scanneur Azure Information Protection

Par défaut, le scanneur exclut également les mêmes types de fichiers que le client d’étiquetage unifié Azure Information Protection, avec les exceptions suivantes :

- .rtf et .rar sont également exclus

Vous pouvez changer les types de fichiers inclus ou exclus pour l’inspection des fichiers par le scanneur :

- Configurez les **types de fichiers à analyser** dans le profil du scanneur, [à l’aide du portail Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).

> [!NOTE]
> Si vous incluez des fichiers .rtf pour l’analyse, surveillez attentivement le scanneur. Certains fichiers .rtf ne peuvent pas être inspectés par le scanneur. En effet, pour ces fichiers, l’inspection n’aboutit pas et le service doit être redémarré. 

Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Pour modifier ce comportement pour le scanneur, utilisez le paramètre avancé PowerShell **PFileSupportedExtensions**. Pour plus d’informations, consultez [configuration PowerShell pour modifier les types de fichiers protégés](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) contre les instructions de déploiement de l’analyseur.

### <a name="files-that-cannot-be-protected-by-default"></a>Fichiers qui ne peuvent pas être protégés par défaut

Tout fichier protégé par mot de passe ne peut pas être protégé en mode natif par le Azure Information Protection client d’étiquetage unifié, sauf si le fichier est actuellement ouvert dans l’application qui applique la protection. Les fichiers PDF protégés par mot de passe sont très courants, mais d’autres applications, comme les applications Office, offrent aussi cette fonctionnalité.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitations pour les fichiers conteneurs, comme les fichiers .zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection.

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

## <a name="file-types-supported-for-inspection"></a>Types de fichiers pris en charge pour l’inspection

Sans configuration supplémentaire, le Azure Information Protection client d’étiquetage unifié utilise Windows IFilter pour inspecter le contenu des documents. Windows IFilter est utilisé par Windows Search pour l’indexation. Par conséquent, les types de fichiers suivants peuvent être inspectés quand vous utilisez la commande PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) .

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|Word|champs docx ;. docm ;. dot ;. dotm ;. dotx|
|Excel|.xls ; .xlt ; .xlsx ; .xltx ; .xltm ; .xlsm ; .xlsb|
|PowerPoint|.ppt ; .pps ; .pot ; .pptx ; .ppsx ; .pptm ; .ppsm ; .potx ; .potm|
|PDF |.pdf|
|Text|.txt ; .xml ; .csv|

Avec une configuration supplémentaire, d’autres types de fichiers peuvent également être inspectés. Par exemple, vous pouvez [inscrire une extension de nom de fichier personnalisée pour utiliser le gestionnaire de filtre Windows existant pour les fichiers texte](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters). Vous pouvez également installer des filtres supplémentaires provenant d’éditeurs de logiciels.

Pour déterminer les filtres qui sont installés, consultez [Recherche d’un gestionnaire de filtre pour une extension de fichier donnée](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension) dans le guide du développeur de Windows Search.

Les sections suivantes contiennent des instructions de configuration pour inspecter les fichiers .zip et .tiff.

### <a name="to-inspect-zip-files"></a>Pour inspecter les fichiers .zip

Le scanneur Azure Information Protection et la commande PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) permettent d’inspecter les fichiers .zip suivant ces instructions :

1. Pour l’ordinateur exécutant le scanneur ou la session PowerShell, installez [Office 2010 Filter Pack SP2](https://support.microsoft.com/en-us/help/2687447/description-of-office-2010-filter-pack-sp2).

2. Pour le scanneur : après avoir trouvé des informations sensibles, si le fichier. zip doit être classifié et protégé par une étiquette, spécifiez l’extension de nom de fichier. zip avec le paramètre avancé PowerShell **PFileSupportedExtensions**, comme décrit dans [ Configuration PowerShell pour modifier les types de fichiers protégés](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) contre les instructions de déploiement de l’analyseur.


Exemple de scénario après avoir effectué ces étapes : 

Un fichier nommé **accounts.zip** contient des feuilles de calcul Excel avec des numéros de carte de crédit. Vous avez une étiquette de sensibilité nommée **confidentiel \ finance**, qui est configurée pour découvrir les numéros de carte de crédit et appliquer automatiquement l’étiquette avec une protection qui limite l’accès au groupe finance. 

Une fois le fichier inspecté, le client d’étiquetage unifié de votre session PowerShell classe ce fichier comme **confidentiel \ finance**, applique la protection générique au fichier afin que seuls les membres des groupes finance puissent le décompresser et renomme le fichier **. comptes. zip. pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Pour inspecter des fichiers .tiff à l’aide de la reconnaissance optique de caractères

La commande PowerShell [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) peut utiliser la reconnaissance optique de caractères (OCR) pour inspecter les images TIFF avec une extension de nom de fichier. TIFF lorsque vous installez la fonctionnalité Windows TIFF IFilter, puis configurer [Windows TIFF IFilter Paramètres](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) sur l’ordinateur exécutant la session PowerShell.

Pour le scanneur : après avoir trouvé des informations sensibles, si le fichier. TIFF doit être classifié et protégé par une étiquette, spécifiez cette extension de nom de fichier avec le paramètre avancé PowerShell **PFileSupportedExtensions**, comme décrit dans [PowerShell configuration pour modifier les types de fichiers protégés](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) contre les instructions de déploiement de l’analyseur.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié les types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection, consultez les ressources suivantes pour obtenir des informations supplémentaires dont vous pouvez avoir besoin pour prendre en charge ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

