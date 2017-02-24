---
title: Types de fichiers pris en charge par le client Azure Information Protection | Azure Information Protection
description: "Détails techniques sur les types de fichiers pris en charge, les extensions de noms de fichiers et les niveaux de protection pour les administrateurs responsables du client Azure Information Protection pour Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f4503c7383f9ffd9dc7e5cd3c676ec929bdc2802
ms.openlocfilehash: c556769aa34282063ae10190202a746eee33abe6


---


# <a name="file-types-supported-by-the-azure-information-protection-client"></a>Types de fichiers pris en charge par le client Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

Le client Azure Information Protection peut appliquer les éléments suivants aux documents et e-mails :

- Classification uniquement

- Classification et protection

- Protection uniquement

Utilisez les informations suivantes pour vérifier les types de fichiers pris en charge, les différents niveaux de protection, la manière de modifier le niveau de protection par défaut, et les fichiers qui sont automatiquement exclus (ignorés) de la classification et de la protection.

## <a name="file-types-supported-for-classification-only"></a>Types de fichiers pris en charge pour la classification uniquement

Seule la classification est prise en charge pour les types de fichiers suivants. Les autres types de fichiers prennent en charge la classification quand ils sont aussi protégés.

- **Microsoft Visio** : .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst

- **Microsoft Project** : .mpp, .mpt

- **Microsoft Publisher** : .pub

- **Microsoft Office 97, Office 2010, Office 2003** : .xls, .xlt, .doc, .dot, .ppt, .pps, .pot

- **Microsoft XPS** : .xps .oxps

- **Images** : .jpg, .jpe, .jpeg, .jif, .jfif,. jfi.png, .tif, .tiff

- **SolidWorks** : .sldprt, .slddrw, .sldasm

- **Autodesk Design Review 2013** : .dwfx

- **Adobe Photoshop** : .psd

- **Digital Negative** : .dng

## <a name="file-types-supported-for-protection"></a>Types de fichiers pris en charge pour la protection

Le client Azure Information Protection prend en charge la protection à deux niveaux différents, comme décrit dans le tableau suivant.

|Type de protection|Natif|Générique|
|----------------------|----------|-----------|
|Description|Dans le cas de fichiers texte, image, Microsoft Office (Word, Excel, PowerPoint), .pdf et d’autres types de fichier d’application qui prennent en charge un service Rights Management, la protection native fournit un niveau de protection élevé, qui comprend le chiffrement et la mise en application de droits (autorisations).|Pour toutes les autres applications et tous les autres types de fichier, la protection générique fournit un niveau de protection qui inclut à la fois l’encapsulation de fichier avec le type de fichier .pfile et l’authentification pour déterminer si un utilisateur est autorisé à ouvrir le fichier.|
|Protection|Les fichiers sont entièrement chiffrés et la protection est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes qui reçoivent le fichier par e-mail ou qui y ont accès grâce aux autorisations de fichier ou de partage doivent être authentifiées.<br /><br />- De plus, la stratégie et les droits d’utilisation, définis par le propriétaire du contenu quand les fichiers sont protégés, sont entièrement appliqués quand le contenu est affiché dans la visionneuse Azure Information Protection (pour les fichiers texte et image protégés) ou dans l’application associée (pour tous les autres types de fichiers pris en charge).|La protection des fichiers est appliquée comme suit :<br /><br />- Pour afficher le contenu protégé, les personnes autorisées à ouvrir le fichier et qui y ont accès doivent être authentifiées. Si l'autorisation échoue, le fichier ne s'ouvre pas.<br /><br />- Les droits d’utilisation et la stratégie définis par le propriétaire du contenu sont affichés pour informer les utilisateurs autorisés de la stratégie d’utilisation prévue.<br /><br />- Un enregistrement d’audit des utilisateurs autorisés qui ouvrent les fichiers et qui y accèdent est réalisé, mais aucun droit d’utilisation n’est appliqué par les applications qui ne prennent pas cette fonctionnalité en charge.|
|Valeur par défaut pour les types de fichier|Il s'agit du niveau de protection par défaut pour les types de fichiers suivants :<br /><br />- Fichiers texte et image<br /><br />- Fichiers Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Fichiers PDF (Portable Document Format) (.pdf)<br /><br />Pour plus d’informations, consultez la section suivante, [Types de fichier pris en charge et extensions de nom de fichier](#supported-file-types-for-protection-and-their-file-name-extensions).|Il s’agit de la protection par défaut pour tous les autres types de fichier (comme .vsdx, .rtf, etc.), qui ne sont pas pris en charge par la fonctionnalité de protection complète.|

Vous pouvez modifier le niveau de protection par défaut que le client Azure Information Protection applique. Vous pouvez remplacer le niveau de protection native par défaut par une protection générique, et inversement, et même empêcher que le client Azure Information Protection n’applique la protection. Pour plus d’informations, consultez la section [Modification du niveau de protection par défaut des fichiers](#changing-the-default-protection-level-of-files) dans cet article.

La protection des données peut être automatiquement appliquée lorsqu’un utilisateur sélectionne une étiquette qu’un administrateur a configurée. Les utilisateurs peuvent également spécifier leurs propres paramètres de protection personnalisés à l’aide des [niveaux d’autorisation](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="supported-file-types-for-protection-and-their-file-name-extensions"></a>Types de fichiers pris en charge pour la protection et les extensions de noms de fichiers
Le tableau suivant répertorie les types de fichiers pris en charge en mode natif par le client Azure Information Protection. Pour ces types de fichier, l'extension de nom de fichier d'origine est modifiée lorsque la protection native est appliquée, et ces fichiers sont alors en lecture seule.

Pour les fichiers protégés de manière générique, l'extension de nom de fichier d'origine est toujours remplacée par .pfile.

> [!WARNING]
> Si vous disposez de pare-feu, proxys web ou logiciels de sécurité qui contrôlent et prennent des mesures en fonction des extensions de nom de fichier, vous devrez peut-être les reconfigurer pour qu'ils prennent en charge ces nouvelles extensions de nom de fichier.

|Extension de nom de fichier d'origine|Extension de nom d’un fichier protégé|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|


Le tableau suivant répertorie les types de fichiers que le client Azure Information Protection prend en charge en mode natif pour les applications Microsoft Office. Pour ces fichiers, l’extension de nom de fichier reste la même une fois que le fichier est protégé par un service Rights Management.

|Types de fichier pris en charge par Office|Types de fichier pris en charge par Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modification du niveau de protection par défaut des fichiers
Vous pouvez modifier la façon dont le client Azure Information Protection protège les fichiers en modifiant le Registre. Par exemple, vous pouvez forcer les fichiers qui prennent en charge la protection native à être protégés de manière générique par le client Azure Information Protection.

Raisons pour lesquelles vous pourriez vouloir procéder ainsi :

-   Pour vous assurer que tous les utilisateurs peuvent ouvrir le fichier s'ils ne possèdent pas d'application prenant en charge la protection native.

-   Pour tenir compte des systèmes de sécurité qui agissent sur les fichiers selon leur extension de nom de fichier et peuvent être reconfigurés pour prendre en charge l'extension de nom de fichier .pfile, mais ne peuvent pas être reconfigurés pour prendre en charge plusieurs extensions de nom de fichier pour la protection native.

De même, vous pouvez forcer le client Azure Information Protection à appliquer une protection native aux fichiers qui auraient une protection générique par défaut. Cela peut être approprié si vous avez une application qui prend en charge les API RMS, par exemple une application métier écrite par vos développeurs internes ou une application achetée auprès d'un éditeur de logiciels indépendant.

Vous pouvez également forcer le client Azure Information Protection à bloquer la protection des fichiers (ne pas appliquer de protection native ou générique). Par exemple, cela peut être nécessaire si vous avez une application automatisée ou un service qui doit être en mesure d'ouvrir un fichier spécifique pour traiter son contenu. Quand vous bloquez la protection pour un type de fichier particulier, les utilisateurs ne peuvent pas utiliser le client Azure Information Protection pour protéger les fichiers de ce type. Quand ils essaient de le faire, un message indiquant que l'administrateur a empêché la protection s'affiche, et ils doivent annuler leur action pour protéger le fichier.

Pour configurer le client Azure Information Protection afin qu’il applique une protection générique à tous les fichiers qui auraient par défaut une protection native, apportez les modifications suivantes au Registre. Si la clé FileProtection n’existe pas, vous devez la créer manuellement.

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** : créez une clé nommée *.

    Ce réglage désigne les fichiers avec une extension de nom de fichier quelconque.

2.  Dans la clé nouvellement ajoutée HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*, créez une valeur de chaîne (REG_SZ) nommée **Encryption** avec la valeur de données **Pfile**.

    Avec ce paramètre, le client Azure Information Protection applique une protection générique.

Ces deux réglages entraînent l’application de la protection générique par le client Azure Information Protection à tous les fichiers ayant une extension de nom de fichier. Si c'est l'objectif que vous recherchez, aucune configuration supplémentaire n'est requise. Toutefois, vous pouvez définir des exceptions pour des types de fichier spécifiques, afin qu'ils soient protégés en mode natif. Pour cela, vous devez effectuer trois modifications supplémentaires dans le Registre pour chaque type de fichier :

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** : ajoutez une nouvelle clé dont le nom correspond à l’extension de nom de fichier (sans le point en préfixe).

    Par exemple, pour les fichiers qui ont une extension de nom de fichier .docx, créez une clé nommée **DOCX**.

2.  Dans la clé nouvellement ajoutée (par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur DWORD nommée **AllowPFILEEncryption** avec la valeur **0**.

3.  Dans la clé de type de fichier nouvellement ajoutée, par exemple **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), créez une valeur de chaîne nommée **Encryption** avec la valeur **Native**.

Suite à ces réglages, tous les fichiers sont protégés de façon générique, à l’exception des fichiers qui ont une extension de nom de fichier .docx, qui sont protégés en mode natif par le client Azure Information Protection.

Répétez ces trois étapes pour les autres types de fichier que vous souhaitez définir en tant qu’exceptions car ils prennent en charge la protection native et vous ne souhaitez pas qu’ils soient protégés de manière générique par le client Azure Information Protection.

Vous pouvez apporter des modifications similaires au Registre pour d'autres scénarios en modifiant la valeur de la chaîne **Encryption** qui prend en charge les valeurs suivantes :

-   **Pfile**: protection générique

-   **Native**: protection native

-   **Off**: bloquer la protection

Pour plus d’informations, consultez [Configuration des API de fichier](../develop/file-api-configuration.md) dans le Guide du développeur. Dans cette documentation pour les développeurs, la protection générique est appelée « PFile ». 

## <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client"></a>Types de fichiers exclus de la classification et de la protection par le client Azure Information Protection

Pour empêcher les utilisateurs de modifier des fichiers essentiels au fonctionnement de l’ordinateur, certains types de fichiers et de dossiers sont automatiquement exclus de classification et de la protection. Si les utilisateurs essaient de classifier ou de protéger ces fichiers, un message indiquant qu’ils sont exclus s’affiche.

- **Types de fichiers exclus** : .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb, .jar

- **Dossiers exclus** : 
    - Windows
    - Program Files (\Program Files et \Program Files (x86))
    - \ProgramData 
    - \AppData (pour tous les utilisateurs)




## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez identifié les types de fichiers pris en charge par le client Azure Information Protection, consultez les éléments suivants pour des informations supplémentaires nécessaires à la prise en charge de ce client :

- [Fichiers du client et journalisation de l’utilisation](client-admin-guide-files-and-logging.md)

- [Suivi des documents](client-admin-guide-document-tracking.md)

- [Commandes PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


