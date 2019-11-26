---
title: File types supported - Azure Information Protection unified labeling client
description: Technical details about supported file types, file name extensions, and levels of protection for admins who are are responsible for the Azure Information Protection unified labeling client for Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bf386685847f10ecead59ac59c44620f03372d6d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474257"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Admin Guide: File types supported by the Azure Information Protection unified labeling client

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*>
>
> *Instructions for: [Azure Information Protection unified labeling client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

The Azure Information Protection unified labeling client can apply the following to documents and emails:

- Classification uniquement

- Classification et protection

- Protection uniquement

The Azure Information Protection unified labeling client can also inspect the content of some file types using well-known sensitive information types or regular expressions that you define.

Use the following information to check which file types the Azure Information Protection unified labeling client supports, understand the different levels of protection and how to change the default protection level, and to identify which files are automatically excluded (skipped) from classification and protection.

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

- If the **General** sensitivity label applies classification and does not apply protection: You could apply the **General** label to a file named sales.pdf but you could not apply this label to a file named sales.txt. 

- If the **Confidential \ All Employees** sensitivity label applies classification and protection: You could apply this label to a file named sales.pdf and a file named sales.txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

The Azure Information Protection unified labeling client supports protection at two different levels, as described in the following table.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|Description|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour toutes les autres applications et tous les autres types de fichiers, la protection générique offre un niveau de protection qui comprend l'encapsulation de fichier avec le type de fichier .pfile, et l'authentification, pour vérifier si un utilisateur est autorisé à ouvrir le fichier.|
|Protection|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués.|
|Protection par défaut selon les types de fichiers|Voici le niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).|Il s’agit de la protection par défaut pour tous les autres types de fichiers (comme .vsdx, .rtf, etc.) qui ne sont pas pris en charge par la fonctionnalité de protection native.|

You cannot change the default protection level that the Azure Information Protection unified labeling client or the scanner applies. However, you can change which file types are protected. For more information, see [Change which file types to protect](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

The protection can be applied automatically when a user selects a sensitivity label that an administrator has configured, or users can specify their own custom protection settings by using [permission levels](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

There are maximum file sizes that the Azure Information Protection unified labeling client supports for protection.

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

The following table lists a subset of file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. 

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

The next table lists the remaining file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichiers pris en charge par Office|Types de fichiers pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Types de fichiers exclus de la classification et de la protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. If users try to classify or protect these files by using the Azure Information Protection unified labeling client, they see a message that they are excluded.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb, .jar
    
    > [!NOTE]
    > Unlike the classic client, .msg files are not excluded. Currently, there is a known issue with .msg files that are classified and protected as ".msg.pfile" and you cannot open these files. For these files, remove the label to open the file.

- **Dossiers exclus** : 
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData 
    - \AppData (pour tous les utilisateurs)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Types de fichiers exclus de la classification et de la protection par le scanneur Azure Information Protection

By default, the scanner also excludes the same file types as the Azure Information Protection unified labeling client with the following exceptions:

- .msg, .rtf, and .rar, are also excluded

Vous pouvez changer les types de fichiers inclus ou exclus pour l’inspection des fichiers par le scanneur :

- Configurez les **types de fichiers à analyser** dans le profil du scanneur, [à l’aide du portail Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).
    
    > [!NOTE]
    > Because of the known issue for .msg files detailed in the previous section, we recommend you keep .msg files as excluded.
    > 
    > Si vous incluez des fichiers .rtf pour l’analyse, surveillez attentivement le scanneur. Certains fichiers .rtf ne peuvent pas être inspectés par le scanneur. En effet, pour ces fichiers, l’inspection n’aboutit pas et le service doit être redémarré. 

Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). To change this behavior for the scanner, use the PowerShell advanced setting, **PFileSupportedExtensions**. For more information, see [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

### <a name="files-that-cannot-be-protected-by-default"></a>Fichiers qui ne peuvent pas être protégés par défaut

Any file that is password-protected cannot be natively protected by the Azure Information Protection unified labeling client unless the file is currently open in the application that applies the protection. Les fichiers PDF protégés par mot de passe sont très courants, mais d’autres applications, comme les applications Office, offrent aussi cette fonctionnalité.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitations pour les fichiers conteneurs, comme les fichiers .zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection.

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

## <a name="file-types-supported-for-inspection"></a>Types de fichiers pris en charge pour l’inspection

Without any additional configuration, the Azure Information Protection unified labeling client uses Windows IFilter to inspect the contents of documents. Windows IFilter est utilisé par Windows Search pour l’indexation. As a result, the following file types can be inspected when you use the [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command.

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|Word|.doc; docx; .docm; .dot; .dotm; .dotx|
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

2. For the scanner: After finding sensitive information, if the .zip file should be classified and protected with a label, specify the .zip file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.


Exemple de scénario après avoir effectué ces étapes : 

Un fichier nommé **accounts.zip** contient des feuilles de calcul Excel avec des numéros de carte de crédit. You have a sensitivity label named **Confidential \ Finance**, which is configured to discover credit card numbers and automatically apply the label with protection that restricts access to the Finance group. 

After inspecting the file, the unified labeling client from your PowerShell session classifies this file as **Confidential \ Finance**, applies generic protection to the file so that only members of the Finance groups can unzip it, and renames the file **accounts.zip.pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Pour inspecter des fichiers .tiff à l’aide de la reconnaissance optique de caractères

The [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command can use optical character recognition (OCR) to inspect TIFF images with a .tiff file name extension when you install the Windows TIFF IFilter feature, and then configure [Windows TIFF IFilter Settings](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) on the computer running the PowerShell session.

For the scanner: After finding sensitive information, if the .tiff file should be classified and protected with a label, specify this file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

## <a name="next-steps"></a>Étapes suivantes
Now that you've identified the file types supported by the Azure Information Protection unified labeling client, see the following resources for additional information that you might need to support this client:

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

