---
title: "Classifier et protéger un fichier ou un e-mail à l’aide d’Azure Information Protection| Azure Information Protection"
description: Instructions sur la classification et la protection de vos documents et e-mails.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e6d4cc50259b9d9bb73a75c648f9e6915562accf
ms.openlocfilehash: e1d61fbe1d74a4a57d9a1fdf518aeb0242d0f7ad


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Classifier et protéger un fichier ou un e-mail avec Azure Information Protection

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 avec SP1*

**[Cette version du client est une préversion susceptible d’être modifiée.]**

Le plus simple pour classifier et protéger vos documents et vos e-mails consiste à le faire quand vous les créez ou les modifiez à partir de vos applications bureautiques Office : **Word**, **Excel**, **PowerPoint**, **Outlook**. 

Toutefois, vous pouvez également classifier et protéger des fichiers à l’aide de l’**Explorateur de fichiers**, lequel prend en charge des types de fichiers supplémentaires et constitue un moyen pratique de classifier et protéger plusieurs fichiers à la fois.

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Utilisation des applications Office pour classifier et protéger vos documents et vos e-mails

Utilisez la barre Azure Information Protection et sélectionnez une des étiquettes qui a été configurée pour vous. Exemple :

![Exemple de barre Azure Information Protection](../media/info-protect-bar-not-set-callout.png)


## <a name="using-file-explorer-to-classify-and-protect-files"></a>Utilisation de l’Explorateur de fichiers pour classifier et protéger des fichiers

Avec l’Explorateur de fichiers, vous pouvez rapidement classifier et protéger un seul fichier, plusieurs fichiers ou un dossier. 

Quand vous sélectionnez un dossier, tous les fichiers et sous-dossiers qu’il contient sont automatiquement sélectionnés pour les options de classification et de protection que vous définissez. Toutefois, les nouveaux fichiers que vous créez dans ce dossier ou ses sous-dossiers ne sont pas automatiquement configurés avec ces options.

Quand vous utiliserez l’Explorateur de fichiers pour classifier et protéger vos fichiers, vous remarquerez que les étiquettes ne sont pas toujours disponibles. Cela se produit quand les fichiers que vous sélectionnez ne prennent pas en charge la classification. Pour ces fichiers, vous pouvez sélectionner une étiquette uniquement si votre administrateur l’a configurée pour appliquer une protection. Ou bien, vous pouvez spécifier vos propres paramètres de protection. 

Pour obtenir la liste des types de fichiers pris en charge dans l’Explorateur de fichiers, consultez la section [Types de fichiers pris en charge pour la classification et la protection](#file-types-supported-for-classification-and-protection) dans cette page.


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>Pour classer et protéger un fichier à l’aide de l’Explorateur de fichiers

1.  Dans l’Explorateur de fichiers, sélectionnez votre fichier, plusieurs fichiers ou un dossier. Cliquez avec le bouton droit, puis sélectionnez **Classifier et protéger (préversion)**. 

2. Dans la boîte de dialogue **Classifier et protéger - Azure Information Protection**, utilisez les étiquettes comme vous le feriez dans une application Office, qui définit la classification et la protection comme les a effectuées votre administrateur. Si une étiquette ne peut pas être sélectionnée (elle est indisponible), le fichier sélectionné ne prend pas en charge la classification, mais vous pouvez le protéger.

3. Pour protéger le fichier, choisissez entre les paramètres de protection que votre administrateur a définis pour votre étiquette sélectionnée (**Automatique, en fonction de l’étiquette de classification sélectionnée**), ou spécifiez vos propres paramètres (**Remplacer par des autorisations personnalisées**).
    
    L’option de remplacement n’utilise pas tous les paramètres de protection que votre administrateur peut avoir définis pour l’étiquette de votre choix. À la place, vous spécifiez vos propres paramètres de protection. 

4. Si vous avez sélectionné l’option de remplacement, spécifiez maintenant ce qui suit :

    - **Sélectionner des autorisations** : sélectionnez le niveau d’accès que vous voulez donner aux utilisateurs quand vous protégez les fichiers sélectionnés.
    
    - **Sélectionner des utilisateurs** : spécifiez les personnes qui doivent disposer des autorisations que vous avez sélectionnées pour vos fichiers. Vous pouvez utiliser le carnet d’adresses pour rechercher et sélectionner les personnes et groupes de votre organisation. Pour les personnes extérieures à votre organisation, vous devez spécifier une adresse e-mail complète. Assurez-vous d’utiliser une adresse e-mail professionnelle, car les adresses personnelles ne sont pas prises en charge pour le moment.
        
    - **Faire expirer l’accès** : sélectionnez cette option uniquement pour les fichiers urgents afin que les personnes que vous avez spécifiées ne puissent pas les ouvrir après une date que vous spécifiez. Vous pouvez toujours ouvrir le fichier d’origine mais, après minuit (dans votre fuseau horaire), le jour spécifié, les personnes que vous avez désignées ne peuvent plus l’ouvrir.

5. Cliquez sur **Appliquer**, puis sur **Fermer**.

Les fichiers sélectionnés sont maintenant classifiés et protégés, conformément à vos sélections. Dans certains cas (quand l’ajout d’une protection modifie l’extension du nom du fichier), le fichier d’origine dans l’Explorateur de fichiers est remplacé par un nouveau fichier associé à l’icône de verrou de Azure Information Protection. Exemple :

![Fichier protégé avec une icône de verrou pour Azure Information Protection](../media/Pfile.png)

Si vous changez d’avis sur la classification et la protection, ou avez besoin de modifier vos paramètres, répétez simplement ce processus avec vos nouveaux paramètres.

La classification et la protection que vous avez spécifiées restent avec le fichier, même si vous l’envoyez par e-mail ou l’enregistrez à un autre emplacement. Si vous avez protégé le fichier, vous pouvez suivre son utilisation et au besoin, révoquer son accès. Pour plus d’informations, consultez [Suivre et révoquer vos documents protégés quand vous utilisez Azure Information Protection](client-track-revoke.md). 

#### <a name="file-types-supported-for-classification-and-protection"></a>Types de fichiers pris en charge pour la classification et la protection

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


La protection à l’aide du service Rights Management est prise en charge pour les types de fichiers décrits dans la [configuration de l’API de fichier](../develop/file-api-configuration.md). Cette protection est automatiquement applicable quand vous sélectionnez une étiquette que votre administrateur a configurée, ou vous pouvez spécifier vos propres paramètres de protection à l’aide de [niveaux d’autorisation](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 


## <a name="other-instructions"></a>Autres instructions
Pour obtenir des instructions pratiques, consultez les sections suivantes du guide de l’utilisateur Azure Information Protection :

-   [Que voulez-vous faire ?](client-user-guide.md#what-do-you-want-to-do)




<!--HONumber=Dec16_HO1-->


