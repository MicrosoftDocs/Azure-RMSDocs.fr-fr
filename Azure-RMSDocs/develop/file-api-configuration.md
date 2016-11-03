---
title: "Configuration de l’API de fichier | Azure RMS"
description: "Le comportement de l’API de fichier peut être configuré via les paramètres du Registre."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 734ff9735adbf5aac5824b5c823a1fdcaf245d4e
ms.openlocfilehash: 92df5a261565b83e71a6bfd1a2d432072815bd27


---

# Configuration de l’API de fichier


Le comportement de l’API de fichier peut être configuré via les paramètres du Registre.

L’API de fichier fournit deux types de protection : une protection native et une protection PFile.

-   **Protection native** - Le fichier est protégé par un format de fichier AD RMS basé sur son type MIME (extension de nom de fichier).
-   **Protection PFile** - Le fichier est protégé par le format de fichier protégé (PFile) AD RMS.

Pour plus d’informations sur les formats de fichiers pris en charge, consultez **API de fichier - Détails de la prise en charge des fichiers** dans cette rubrique.

## Types et descriptions des clés/valeurs de clés

Les sections suivantes décrivent les clés et valeurs de clés qui contrôlent le chiffrement.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

**Type** : Clé

**Description** : Contient la configuration générale de l’API de fichier.

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;

**Type** : Clé

**Description** : Spécifie les informations de configuration d’une extension de fichier spécifique ; par exemple TXT, JPG, etc.

- Le caractère générique « * » est autorisé. Toutefois, le paramètre d’une extension spécifique est prioritaire sur le paramètre du caractère générique. Le caractère générique n’affecte pas les paramètres des fichiers Microsoft Office. Vous devez désactiver explicitement ces derniers à l’aide du type de fichier.
- Pour spécifier des fichiers qui n’ont pas d’extension, utilisez « . »
- N’indiquez pas le caractère « . » quand vous spécifiez la clé d’une extension de fichier particulière. Par exemple, utilisez `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` pour spécifier les paramètres des fichiers .txt. (N’utilisez pas `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`).

Définissez la valeur **Encryption** dans la clé pour spécifier le comportement de la protection. Si la valeur **Encryption** n’est pas définie, le comportement par défaut du type de fichier est observé.


### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;\Encryption*

**Type** : REG_SZ

**Description** : Contient l’une des trois valeurs suivantes :

- **Off** : Le chiffrement est désactivé.

> [!Note]
> Ce paramètre n’a aucune incidence sur le déchiffrement. Tout fichier chiffré, que ce soit via la protection Native ou la protection Pfile, peut être déchiffré du moment que l’utilisateur dispose du droit **EXTRACT**.

- **Native** : Le chiffrement natif est utilisé. Pour les fichiers Office, le fichier chiffré a la même extension que le fichier d’origine. Par exemple, un fichier avec l’extension de fichier .docx est chiffré en fichier avec l’extension .docx. Les autres fichiers auxquels une protection native peut être appliquée sont chiffrés en fichiers avec une extension au format p*zzz*, où *zzz* représente l’extension de fichier d’origine. Par exemple, les fichiers .txt sont chiffrés en fichiers avec l’extension .ptxt. Vous trouverez ci-après une liste d’extensions de fichiers pouvant bénéficier d’une protection native.

- **Pfile** : Le chiffrement PFile est utilisé. L’extension .pfile est ajoutée à l’extension d’origine du fichier chiffré. Par exemple, une fois le chiffrement effectué, un fichier .txt a l’extension .txt.pfile.


> [!Note]
> Ce paramètre n’a aucune incidence sur les formats de fichiers Office. Par exemple, si la valeur `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` est « Pfile », les fichiers .docx sont tout de même chiffrés à l’aide de la protection native. De plus, les fichiers chiffrés gardent l’extension de fichier .docx.

Si vous affectez une autre valeur, ou si vous n’affectez aucune valeur, le comportement par défaut s’applique.

## Comportement par défaut des différents formats de fichiers

-   **Fichiers Office** : Le chiffrement natif est activé.
-   **Fichiers txt, xml, jpg, jpeg, pdf, png, tiff, bmp, gif, giff, jpe, jfif, jif** : Le chiffrement natif est activé (xxx devient pxxx)
-   **Tous les autres fichiers** : Le chiffrement avec protection de fichier (pfile) est activé (xxx devient xxx.pfile)

Si vous tentez un chiffrement sur un type de fichier bloqué, une erreur [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx) se produit.

### API de fichier - Détails de la prise en charge des fichiers

Vous pouvez ajouter une prise en charge native pour tous les types de fichier (extension). Par exemple, pour toute extension &lt;ext&gt; (non-Office), \*.p&lt;ext&gt; est utilisé si la configuration d’administration pour cette extension est « NATIVE ».

**Fichiers Office**

-   Extensions de fichier : doc, dot, xla, xls, xlt, pps, ppt, docm, docx, dotm, dotx, xlam, xlsb, xlsm, xlsx, xltm, xltx, xps, potm, potx, ppsx, ppsm, pptm, pptx, thmx.
-   Type de protection = Native (par défaut) : sample.docx est chiffré en sample.docx
-   Type de protection = Pfile : pour les fichiers Office, le résultat est le même qu’avec la protection native.
-   Off : Désactive le chiffrement.

**Fichiers PDF**

-   Type de protection = Native : sample.pdf est chiffré et nommé sample.ppdf
-   Type de protection = Pfile : sample.pdf est chiffré et nommé sample.pdf.pfile.
-   Off : Désactive le chiffrement.

**Tous les autres formats de fichiers**

-   Type de protection = Pfile : sample.*zzz* est chiffré et nommé sample.*zzz*.pfile, où *zzz* représente l’extension de fichier d’origine.
-   Off : Désactive le chiffrement.

### Exemples

Les paramètres suivants activent le chiffrement PFile pour les fichiers txt. La protection native est appliquée aux fichiers Office (par défaut) tandis que la protection PFile est appliquée aux fichiers txt. Pour tous les autres fichiers, la protection est bloquée (par défaut).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

Les paramètres suivants activent le chiffrement PFile pour tous les fichiers non-Office, à l’exception des fichiers txt. La protection native est appliquée aux fichiers Office (par défaut) mais la protection est bloquée pour les fichiers txt. Pour tous les autres fichiers, la protection PFile est appliquée.

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

Les paramètres suivants désactivent le chiffrement natif pour les fichiers docx. Pour les fichiers Office, à l’exception des fichiers docx, la protection native est appliquée (par défaut). Pour tous les autres fichiers, la protection est bloquée (par défaut).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## Rubriques connexes

- [Notes pour le développeur](developer-notes.md)
- [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx)
 

 



<!--HONumber=Oct16_HO3-->


