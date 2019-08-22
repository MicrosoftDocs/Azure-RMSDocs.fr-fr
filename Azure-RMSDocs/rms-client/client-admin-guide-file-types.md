---
title: Types de fichiers pris en charge-client Azure Information Protection
description: Détails techniques sur les types de fichiers pris en charge, les extensions de noms de fichiers et les niveaux de protection pour les administrateurs responsables du client Azure Information Protection pour Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9d7ddd54feaef28c1d93a9ae041818007c6e965f
ms.sourcegitcommit: f0dee92d6668001681b507e82f8aea61f3bfa96e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69894449"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-client"></a>Guide de l’administrateur : Types de fichiers pris en charge par le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*
>
> *Instructions pour : [Client Azure Information Protection pour Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Le client Azure Information Protection peut appliquer les éléments suivants aux documents et e-mails :

- Classification uniquement

- Classification et protection

- Protection uniquement

Le client Azure Information Protection peut également inspecter le contenu de certains types de fichiers à l’aide de types d’informations sensibles bien connus ou d’expressions régulières que vous définissez.

Utilisez les informations suivantes pour vérifier les types de fichiers pris en charge par le client Azure Information Protection, pour comprendre les différents niveaux de protection et comment modifier le niveau de protection par défaut, et pour identifier les fichiers qui sont automatiquement exclus (ignorés) de la classification et de la protection.

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

Par exemple, dans la [stratégie par défaut](../configure-policy-default.md) actuelle, l’étiquette **Général** applique la classification et n’applique pas de protection. Vous pouvez appliquer l’étiquette **Général** à un fichier nommé sales.pdf, mais vous ne pouvez pas l’appliquer à un fichier nommé sales.txt. 

Par ailleurs, dans la stratégie par défaut actuelle, **Confidentiel \ Tous les emplyés** applique la classification et la protection. Vous pouvez appliquer cette étiquette à un fichier nommé sales.pdf et à un fichier nommé sales.txt. Vous pouvez également appliquer juste une protection à ces fichiers, sans classification.

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le client Azure Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|Description|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour toutes les autres applications et tous les autres types de fichier, la protection générique fournit un niveau de protection qui inclut à la fois l’encapsulation de fichier avec le type de fichier .pfile et l’authentification pour déterminer si un utilisateur est autorisé à ouvrir le fichier.|
|Protection|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation qui ont été définis par le propriétaire du contenu quand les fichiers ont été protégés sont appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- La journalisation de l’audit de l’ouverture et de l’accès aux fichiers par les utilisateurs autorisés est effectuée. Cependant, les droits d’utilisation ne sont pas appliqués.|
|Valeur par défaut pour les types de fichier|Il s'agit du niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichiers pris en charge pour la classification et la protection](#supported-file-types-for-classification-and-protection).|Il s’agit de la protection par défaut pour tous les autres types de fichiers (comme .vsdx, .rtf, etc.) qui ne sont pas pris en charge par la fonctionnalité de protection native.|

Vous pouvez modifier le niveau de protection par défaut que le client Azure Information Protection applique. Vous pouvez remplacer le niveau de protection native par défaut par une protection générique, et inversement, et même empêcher que le client Azure Information Protection n’applique la protection. Pour plus d’informations, consultez la section [Modification du niveau de protection par défaut des fichiers](#changing-the-default-protection-level-of-files) dans cet article.

La protection des données peut être automatiquement appliquée lorsqu’un utilisateur sélectionne une étiquette qu’un administrateur a configurée. Les utilisateurs peuvent également spécifier leurs propres paramètres de protection personnalisés à l’aide des [niveaux d’autorisation](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Tailles de fichiers prises en charge pour la protection

Il existe des tailles de fichier maximales que le client Azure Information Protection prend en charge pour la protection.

- **Pour les fichiers Office :**


  |                                                     Application Office                                                      |                                                Taille de fichier maximale prise en charge                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2007 (pris en charge par AD RMS uniquement)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bits: 512 Mo<br /><br />64 bits: 512 Mo                                          |
  |           Excel 2007 (pris en charge par AD RMS uniquement)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bits: 2 Go<br /><br />64 bits: limité uniquement par l’espace disque et la mémoire disponibles                       |
  | PowerPoint 2007 (pris en charge par AD RMS uniquement)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bits: limité uniquement par l’espace disque et la mémoire disponibles<br /><br />64 bits: limité uniquement par l’espace disque et la mémoire disponibles |


- **Pour tous les autres fichiers** : 

  - Pour protéger d’autres types de fichiers et ouvrir ces types de fichiers dans la visionneuse Azure Information Protection : la taille de fichier maximale est limitée uniquement par l’espace disque et la mémoire disponibles.

  - Pour ôter la protection de fichiers à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) : la taille de fichier maximale prise en charge pour les fichiers .pst est de 5 Go. Les autres types de fichiers sont limités uniquement par l’espace disque et la mémoire disponibles

    Conseil : Si vous avez besoin de rechercher ou de récupérer des éléments protégés dans des fichiers .pst volumineux, consultez [Conseils d’utilisation d’Unprotect-RMSFile pour eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

Le tableau suivant liste une partie des types de fichiers qui prennent en charge la protection native par le client Azure Information Protection et qui peuvent également être classés. 

Ces types de fichiers sont identifiés séparément, car quand ils sont protégés en mode natif, l’extension de nom de fichier d’origine change et ces fichiers passent en lecture seule. Notez que quand des fichiers sont protégés de façon générique, l’extension de nom de fichier d’origine est toujours remplacée par .pfile.

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être reconfigurer ces appareils et logiciels réseau pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

|Extension de nom de fichier d'origine|Extension de nom d’un fichier protégé|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.pdf|.ppdf [[1]](#footnote-1)|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

###### <a name="footnote-1"></a>Note 1
Avec la dernière version du client Azure Information Protection, [par défaut](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), l’extension de nom de fichier des documents PDF protégés reste au format .pdf.

Le tableau suivant liste les types de fichiers restants qui prennent en charge la protection native par le client Azure Information Protection et qui peuvent également être classés. Vous y trouvez les types de fichiers pour les applications Microsoft Office. Les formats de fichiers pris en charge pour ces types de fichiers sont les formats 97-2003 et les formats Office Open XML pour les programmes Office suivants : Word, Excel et PowerPoint.

Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichier pris en charge par Office|Types de fichier pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modification du niveau de protection par défaut des fichiers
Vous pouvez modifier la façon dont le client Azure Information Protection protège les fichiers en modifiant le Registre. Par exemple, vous pouvez forcer les fichiers qui prennent en charge la protection native à être protégés de manière générique par le client Azure Information Protection.

Raisons pour lesquelles vous pourriez vouloir procéder ainsi :

- Pour vous assurer que tous les utilisateurs peuvent ouvrir le fichier s'ils ne possèdent pas d'application prenant en charge la protection native.

- Pour tenir compte des systèmes de sécurité qui agissent sur les fichiers selon leur extension de nom de fichier et peuvent être reconfigurés pour prendre en charge l'extension de nom de fichier .pfile, mais ne peuvent pas être reconfigurés pour prendre en charge plusieurs extensions de nom de fichier pour la protection native.

De même, vous pouvez forcer le client Azure Information Protection à appliquer une protection native aux fichiers qui auraient une protection générique par défaut. Cette action peut être appropriée si vous avez une application qui prend en charge les API RMS. Par exemple une application métier écrite par vos développeurs internes ou une application achetée auprès d'un éditeur de logiciels indépendant.

Vous pouvez également forcer le client Azure Information Protection à bloquer la protection des fichiers (ne pas appliquer de protection native ou générique). Par exemple, cette action peut être nécessaire si vous avez une application ou un service automatisé qui doit être en mesure d'ouvrir un fichier spécifique pour traiter son contenu. Quand vous bloquez la protection pour un type de fichier particulier, les utilisateurs ne peuvent pas utiliser le client Azure Information Protection pour protéger les fichiers de ce type. Quand ils essaient de le faire, un message indiquant que l'administrateur a empêché la protection s'affiche, et ils doivent annuler leur action pour protéger le fichier.

Pour configurer le client Azure Information Protection afin qu’il applique une protection générique à tous les fichiers qui auraient par défaut une protection native, apportez les modifications suivantes au Registre. Si la clé FileProtection n’existe pas, vous devez la créer manuellement.

1. Créez une clé nommée * pour le chemin de Registre suivant. Cette clé désigne les fichiers avec n’importe quelle extension de nom de fichier :

    - Pour une version 32 bits de Windows : **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - Pour une version 64 bits de Windows : **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** et **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. Dans la clé nouvellement ajoutée (par exemple, HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*), créez une valeur de chaîne (REG_SZ) nommée **Encryption** avec la valeur de données **Pfile**.

    Avec ce paramètre, le client Azure Information Protection applique une protection générique.

Ces deux réglages entraînent l’application de la protection générique par le client Azure Information Protection à tous les fichiers ayant une extension de nom de fichier. Si c'est l'objectif que vous recherchez, aucune configuration supplémentaire n'est requise. Toutefois, vous pouvez définir des exceptions pour des types de fichier spécifiques, afin qu'ils soient protégés en mode natif. Pour cela, vous devez effectuer trois (pour Windows 32 bits) ou six (pour Windows 64 bits) modifications supplémentaires dans le Registre pour chaque type de fichier :

1. Pour **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** et **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (le cas échéant) : Ajoutez une nouvelle clé qui porte le nom de l’extension de nom de fichier (sans le point précédent).

    Par exemple, pour les fichiers qui ont une extension de nom de fichier .docx, créez une clé nommée **DOCX**.

2. Dans la clé nouvellement ajoutée (par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur DWORD nommée **AllowPFILEEncryption** avec la valeur **0**.

3. Dans la clé de type de fichier nouvellement ajoutée, par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur de chaîne nommée **Encryption** avec la valeur **Native**.

Suite à ces réglages, tous les fichiers sont protégés de façon générique, à l'exception des fichiers qui ont une extension de nom de fichier .docx. Ces fichiers sont protégés en mode natif par le client Azure Information Protection.

Répétez ces trois étapes pour les autres types de fichier que vous souhaitez définir en tant qu’exceptions car ils prennent en charge la protection native et vous ne souhaitez pas qu’ils soient protégés de manière générique par le client Azure Information Protection.

Vous pouvez apporter des modifications similaires au Registre pour d'autres scénarios en modifiant la valeur de la chaîne **Encryption** qui prend en charge les valeurs suivantes :

- **Pfile** : Protection générique

- **Natif** : Protection Native

- **Désactivé** : Protection contre les blocages

Il n’est pas nécessaire de redémarrer l’ordinateur après avoir apporté ces modifications au Registre. Toutefois, si vous utilisez des commandes PowerShell pour protéger des fichiers, vous devez démarrer une nouvelle session PowerShell pour que les modifications soient effectives.

Pour savoir comment modifier le Registre afin de changer le niveau de protection par défaut des fichiers, voir [Configuration de l’API des fichiers](../develop/file-api-configuration.md) dans l’aide aux développeurs. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ».

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Types de fichiers exclus de la classification et de la protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. Si les utilisateurs essaient de classifier ou de protéger ces fichiers avec le client Azure Information Protection, un message indiquant qu’ils sont exclus s’affiche.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msg, .msp, .msi, .pdb, .jar


- **Dossiers exclus** : 
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData 
    - \AppData (pour tous les utilisateurs)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Types de fichiers exclus de la classification et de la protection par le scanneur Azure Information Protection

Par défaut, le scanneur exclut également les mêmes types de fichier que le client Azure Information Protection, à cette exception près :

- .rtf et .rar sont également exclus

Vous pouvez changer les types de fichiers inclus ou exclus pour l’inspection des fichiers par le scanneur :

- Configurez les **types de fichiers à analyser** dans le profil du scanneur, [à l’aide du portail Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).

> [!NOTE]
> Si vous incluez des fichiers .rtf pour l’analyse, surveillez attentivement le scanneur. Certains fichiers .rtf ne peuvent pas être inspectés par le scanneur. En effet, pour ces fichiers, l’inspection n’aboutit pas et le service doit être redémarré. 

Par défaut, le scanneur protège uniquement les types de fichiers Office et PDF (si ces derniers sont protégés à l’aide de la norme ISO pour le chiffrement PDF). Pour modifier ce comportement du scanneur, modifiez le Registre et spécifiez les autres types de fichiers que vous souhaitez protéger. Pour obtenir des instructions, consultez [Modification du Registre du scanner](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner) dans les instructions de déploiement du scanner.

### <a name="files-that-cannot-be-protected-by-default"></a>Fichiers qui ne peuvent pas être protégés par défaut

Aucun fichier protégé par mot de passe ne peut être protégé en mode natif par le client Azure Information Protection, à moins que le fichier soit actuellement ouvert dans l’application qui applique la protection. Les fichiers PDF protégés par mot de passe sont très courants, mais d’autres applications, comme les applications Office, offrent aussi cette fonctionnalité.

Si vous modifiez le [comportement par défaut](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption) du client Azure Information Protection afin qu’il protège les fichiers PDF avec une extension de nom de fichier .ppdf, le client ne peut pas protéger ou déprotéger en mode natif des fichiers PDF dans les cas suivants :

- Un ficher PDF basé sur un formulaire.

- Un fichier PDF protégé qui a une extension de nom de fichier .pdf.

    Le client Azure Information Protection peut protéger un fichier PDF non protégé, et il peut déprotéger et reprotéger un fichier PDF protégé qui a une extension de nom de fichier .ppdf.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitations pour les fichiers conteneurs, comme les fichiers .zip

Les fichiers conteneurs sont des fichiers qui incluent d’autres fichiers, comme l’exemple classique des fichiers .zip qui contiennent des fichiers compressés. D’autres exemples incluent les fichiers .rar, .7z, .msg et les documents PDF qui incluent des pièces jointes.

Vous pouvez classifier et protéger ces fichiers conteneurs, mais la classification et la protection ne sont pas appliquées à chaque fichier situé à l’intérieur du conteneur.

Si vous avez un fichier conteneur qui inclut des fichiers classifiés et protégés, vous devez d’abord extraire ces fichiers pour modifier leurs paramètres de classification ou de protection. Toutefois, vous pouvez supprimer la protection pour tous les fichiers inclus dans des fichiers conteneurs pris en charge à l’aide de l’applet de commande [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

La visionneuse Azure Information Protection ne peut pas ouvrir les pièces jointes dans un document PDF protégé. Dans ce scénario, lorsque le document est ouvert dans la visionneuse, les pièces jointes ne sont pas visibles.

## <a name="file-types-supported-for-inspection"></a>Types de fichiers pris en charge pour l’inspection

Sans configuration supplémentaire, le client Azure Information Protection utilise Windows IFilter pour inspecter le contenu des documents. Windows IFilter est utilisé par Windows Search pour l’indexation. Les types de fichiers suivants peuvent donc être inspectés quand vous utilisez le [scanneur Azure Information Protection](../deploy-aip-scanner.md) ou la commande PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification).

|Type d'application|Type de fichier|
|--------------------------------|-------------------------------------|
|Word|champs docx;. docm;. dot;. dotm;. dotx|
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

2. Pour le scanneur : Après avoir trouvé des informations sensibles, si le fichier .zip doit être classifié et protégé avec une étiquette, ajoutez une entrée de Registre pour cette extension de nom de fichier afin de bénéficier d’une protection générique (pfile), comme décrit dans [Modification du Registre du scanneur](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner) dans les instructions de déploiement du scanneur.

Exemple de scénario après avoir effectué ces étapes : 

Un fichier nommé **accounts.zip** contient des feuilles de calcul Excel avec des numéros de carte de crédit. Votre stratégie Azure Information Protection dispose d’une étiquette nommée **Confidential \ Finance**, qui est configurée pour détecter les numéros de carte de crédit et appliquer automatiquement l’étiquette avec la protection qui limite l’accès au groupe Finance. 

Après avoir inspecté le fichier, le scanneur classifie ce fichier comme **Confidential \ Finance**, applique une protection générique au fichier afin que seuls les membres des groupes Finance puissent le décompresser et renomme le fichier **accounts.zip.pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Pour inspecter des fichiers .tiff à l’aide de la reconnaissance optique de caractères

Le scanneur Azure Information Protection et la commande PowerShell [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) peuvent utiliser la reconnaissance optique de caractères (OCR) pour inspecter les images TIFF avec une extension de nom de fichier .tiff quand vous installez la fonctionnalité Windows TIFF IFilter et configurez les [paramètres TIFF Windows IFilter](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) sur l’ordinateur qui exécute le scanneur ou la session PowerShell.

Pour le scanneur : Après avoir trouvé des informations sensibles, si le fichier .tiff doit être classifié et protégé avec une étiquette, ajoutez une entrée de Registre pour cette extension de nom de fichier afin de bénéficier d’une protection native, comme décrit dans [Modification du Registre du scanneur](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner) dans les instructions de déploiement du scanneur.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié les types de fichiers pris en charge par le client Azure Information Protection, consultez les ressources suivantes pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Customizations](client-admin-guide-customizations.md)

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

