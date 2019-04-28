---
title: Types de fichier pris en charge par le client d’étiquetage unifié Azure Information Protection
description: Détails techniques sur les types de fichiers pris en charge, les extensions de nom de fichier et niveaux de protection pour les administrateurs sont responsables du client d’étiquetage unifiée d’Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: aca0fe5d3d9624676bc2bb12a772f5b753eb1a0d
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183753"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Guide de l’administrateur : Types de fichier pris en charge par le client d’étiquetage unifié Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*>
>
> *Instructions pour : [Azure Information Protection unifiée étiquetage client pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Le client d’étiquetage unifié Azure Information Protection peut appliquer les éléments suivants aux documents et e-mails :

- Classification uniquement

- Classification et protection

- Protection uniquement

Le client d’étiquetage unifié Azure Information Protection peut également inspecter le contenu de certains types de fichiers à l’aide des types d’informations sensibles connu ou des expressions régulières que vous définissez.

Utilisez les informations suivantes pour vérifier les types de fichiers prend en charge par le client étiquetage d’Azure Information Protection unifié, de comprendre les différents niveaux de protection et comment modifier le niveau de protection par défaut et pour identifier les fichiers qui sont automatiquement exclus (ignorés) de la classification et la protection.

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

- **Microsoft Office 365** : types de fichiers dans le tableau suivant.

    Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

    |Type de fichier Office|Type de fichier Office|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

D’autres types de fichiers prennent en charge la classification quand ils sont aussi protégés. Pour ces types de fichiers, consultez la section [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).

Exemples :

- Si le **général** étiquette de sensibilité applique la classification et n’applique pas de protection : Vous pouvez appliquer l’étiquette **Général** à un fichier nommé sales.pdf, mais vous ne pouvez pas l’appliquer à un fichier nommé sales.txt. 

- Si le **confidentiel \ tous les employés** étiquette de sensibilité s’applique la classification et la protection : Vous pouvez appliquer cette étiquette à un fichier nommé sales.pdf et à un fichier nommé sales.txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le client d’étiquetage unifié Azure Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|Description|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour toutes les autres applications et tous les autres types de fichier, la protection générique fournit un niveau de protection qui inclut à la fois l’encapsulation de fichier avec le type de fichier .pfile et l’authentification pour déterminer si un utilisateur est autorisé à ouvrir le fichier.|
|Protection|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués.|
|Valeur par défaut pour les types de fichier|Il s'agit du niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).|Il s’agit de la protection par défaut pour tous les autres types de fichiers (comme .vsdx, .rtf, etc.) qui ne sont pas pris en charge par la fonctionnalité de protection native.|

Vous pouvez modifier le niveau de protection par défaut que le client d’étiquetage unifié Azure Information Protection s’applique. Vous pouvez modifier le niveau par défaut du mode natif au mode générique, générique natif et même empêcher le client d’étiquetage unifié Azure Information Protection à partir de l’application de la protection. Pour plus d’informations, consultez la section [Modification du niveau de protection par défaut des fichiers](#changing-the-default-protection-level-of-files) dans cet article.

La protection peut être appliquée automatiquement lorsqu’un utilisateur sélectionne une étiquette de sensibilité un administrateur a configuré, ou les utilisateurs peuvent spécifier leurs propres paramètres de protection personnalisés à l’aide de [niveaux d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

Il existe des tailles de fichier maximale que le client d’étiquetage unifié Azure Information Protection prend en charge pour la protection.

- **Pour les fichiers Office :**


  |                                                     Application Office                                                      |                                                Taille de fichier maximale prise en charge                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bits : 512 Mo<br /><br />64 bits : 512 Mo                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bits : 2 Go<br /><br />64 bits : limité uniquement par l’espace disque et la mémoire disponibles                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bits : limité uniquement par l’espace disque et la mémoire disponibles<br /><br />64 bits : limité uniquement par l’espace disque et la mémoire disponibles |


- **Pour tous les autres fichiers** : 

  - Pour protéger d’autres types de fichiers et ouvrir ces types de fichiers dans la visionneuse Azure Information Protection : la taille de fichier maximale est limitée uniquement par l’espace disque et la mémoire disponibles.

  - Pour ôter la protection de fichiers à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) : la taille de fichier maximale prise en charge pour les fichiers .pst est de 5 Go. Les autres types de fichiers sont limités uniquement par l’espace disque et la mémoire disponibles

    Conseil : Si vous avez besoin de rechercher ou de récupérer des éléments protégés dans des fichiers .pst volumineux, consultez [Conseils d’utilisation d’Unprotect-RMSFile pour eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

Le tableau suivant répertorie un sous-ensemble de types de fichiers qui prennent en charge la protection native par le client d’étiquetage unifié d’Azure Information Protection et qui peut également être classée. 

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

Le tableau suivant répertorie les types de fichiers restants qui prennent en charge la protection native par le client d’étiquetage unifié d’Azure Information Protection et qui peut également être classée. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichier pris en charge par Office|Types de fichier pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modification du niveau de protection par défaut des fichiers
Vous pouvez modifier la façon dont le client d’étiquetage unifié Azure Information Protection protège les fichiers en modifiant le Registre. Par exemple, vous pouvez forcer les fichiers qui prennent en charge la protection native à être protégés par le client d’étiquetage unifié Azure Information Protection.

Raisons pour lesquelles vous pourriez vouloir procéder ainsi :

- Pour vous assurer que tous les utilisateurs peuvent ouvrir le fichier s'ils ne possèdent pas d'application prenant en charge la protection native.

- Pour tenir compte des systèmes de sécurité qui agissent sur les fichiers selon leur extension de nom de fichier et peuvent être reconfigurés pour prendre en charge l'extension de nom de fichier .pfile, mais ne peuvent pas être reconfigurés pour prendre en charge plusieurs extensions de nom de fichier pour la protection native.

De même, vous pouvez forcer le client étiquetage unifié d’Azure Information Protection pour appliquer une protection native aux fichiers qui auraient une protection générique par défaut. Cette action peut être appropriée si vous avez une application qui prend en charge les API RMS. Par exemple une application métier écrite par vos développeurs internes ou une application achetée auprès d'un éditeur de logiciels indépendant.

Vous pouvez également forcer le client étiquetage Azure Information Protection unifié pour bloquer la protection des fichiers (ne pas appliquer la protection native ou générique). Par exemple, cette action peut être nécessaire si vous avez une application ou un service automatisé qui doit être en mesure d'ouvrir un fichier spécifique pour traiter son contenu. Lorsque vous bloquez la protection pour un type de fichier, les utilisateurs ne pouvez pas utiliser le client d’étiquetage unifié Azure Information Protection pour protéger un fichier de ce type de fichier. Quand ils essaient de le faire, un message indiquant que l'administrateur a empêché la protection s'affiche, et ils doivent annuler leur action pour protéger le fichier.

Pour configurer le client étiquetage unifié d’Azure Information Protection pour appliquer une protection générique à tous les fichiers qui auraient une protection native par défaut, apportez les modifications suivantes au Registre. Si la clé FileProtection n’existe pas, vous devez la créer manuellement.

1. Créez une clé nommée * pour le chemin de Registre suivant. Cette clé désigne les fichiers avec n’importe quelle extension de nom de fichier :

    - Pour une version 32 bits de Windows : **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - Pour une version 64 bits de Windows : **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** et **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. Dans la clé nouvellement ajoutée (par exemple, HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*), créez une valeur de chaîne (REG_SZ) nommée **Encryption** avec la valeur de données **Pfile**.

    Avec ce paramètre, le client Azure Information Protection applique une protection générique.

Ces deux réglages entraînent dans le client unifié étiquetage Azure Information Protection qu’appliquent la protection générique à tous les fichiers ayant une extension de nom de fichier. Si c'est l'objectif que vous recherchez, aucune configuration supplémentaire n'est requise. Toutefois, vous pouvez définir des exceptions pour des types de fichier spécifiques, afin qu'ils soient protégés en mode natif. Pour cela, vous devez effectuer trois (pour Windows 32 bits) ou six (pour Windows 64 bits) modifications supplémentaires dans le Registre pour chaque type de fichier :

1. Pour **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** et **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (le cas échéant) : Ajoutez une nouvelle clé qui porte le nom de l’extension de nom de fichier (sans le point précédent).

    Par exemple, pour les fichiers qui ont une extension de nom de fichier .docx, créez une clé nommée **DOCX**.

2. Dans la clé nouvellement ajoutée (par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur DWORD nommée **AllowPFILEEncryption** avec la valeur **0**.

3. Dans la clé de type de fichier nouvellement ajoutée, par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur de chaîne nommée **Encryption** avec la valeur **Native**.

Suite à ces réglages, tous les fichiers sont protégés de façon générique, à l'exception des fichiers qui ont une extension de nom de fichier .docx. Ces fichiers sont protégés en mode natif par le client d’étiquetage unifié Azure Information Protection.

Répétez ces trois étapes pour d’autres types de fichier que vous souhaitez définir en tant qu’exceptions car ils prennent en charge la protection native et vous ne souhaitez pas qu’elles soient protégés par le client d’étiquetage unifié Azure Information Protection.

Vous pouvez apporter des modifications similaires au Registre pour d'autres scénarios en modifiant la valeur de la chaîne **Encryption** qui prend en charge les valeurs suivantes :

- **Pfile** : protection générique

- **Natif** : protection native

- **Désactivé** : Bloquer la protection

Il n’est pas nécessaire de redémarrer l’ordinateur après avoir apporté ces modifications au Registre. Toutefois, si vous utilisez des commandes PowerShell pour protéger des fichiers, vous devez démarrer une nouvelle session PowerShell pour que les modifications soient effectives.

Pour savoir comment modifier le Registre afin de changer le niveau de protection par défaut des fichiers, voir [Configuration de l’API des fichiers](../develop/file-api-configuration.md) dans l’aide aux développeurs. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ».

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Types de fichiers exclus de la classification et de la protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. Si les utilisateurs essaient de classifier ou de protéger ces fichiers à l’aide du client Azure Information Protection unifié étiquetage, elle voit un message qu’elles sont exclues.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msg, .msp, .msi, .pdb, .jar


- **Dossiers exclus** : 
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData 
    - \AppData (pour tous les utilisateurs)


### <a name="files-that-cannot-be-protected-by-default"></a>Fichiers qui ne peuvent pas être protégés par défaut

N’importe quel fichier qui est protégé par mot de passe ne peut pas être protégé en mode natif par le client d’étiquetage unifié Azure Information Protection, sauf si le fichier est actuellement ouvert dans l’application qui applique la protection. Les fichiers PDF protégés par mot de passe sont très courants, mais d’autres applications, comme les applications Office, offrent aussi cette fonctionnalité.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitations pour les fichiers conteneurs, comme les fichiers .zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection.

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié les types de fichiers pris en charge par le client d’étiquetage unifié Azure Information Protection, consultez les ressources suivantes pour plus d’informations que vous devrez peut-être prendre en charge de ce client :

- [Customizations](clientv2-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](clientv2-admin-guide-files-and-logging.md)

- [Commandes PowerShell](clientv2-admin-guide-powershell.md)

