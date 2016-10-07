---
title: "Procédure d’utilisation des paramètres de chiffrement | Azure RMS"
description: Orientation pour les packages de chiffrement Azure RMS et les captures de code pour leur utilisation.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: bf27067f832f12ef66f6df92f4008a0d21cdf2aa


---

# Comment : utiliser des paramètres de chiffrement

Cette rubrique vous oriente vers nos offres de chiffrement et présente quelques extraits de code pour illustrer leur utilisation.

## Prise en charge d’AES 256 (nouveau chiffrement par défaut)

*AES 256* est le nouveau chiffrement par défaut. Il ne nécessite donc aucun code supplémentaire, si tant est que vous utilisez la mise à jour du mois de mars 2015 ou version ultérieure de RMS SDK 2.1 pour créer vos applications. Nous vous encourageons fortement à mettre à jour vos applications avec cette version pour bénéficier des fonctionnalités de sécurité supplémentaires qu’offre le chiffrement *AES 256*.

> [!IMPORTANT]
> La consommation des fichiers protégés par le chiffrement *AES 256* est prise en charge depuis la [version d’octobre 2014](release-notes-rtm.md). Si vous exécutez des applications créées avec une version du SDK antérieure à octobre 2014, cette mise à jour interrompra vos applications. Vérifiez que les clients des applications que vous créez utilisent le SDK mis à jour ou acceptent de passer immédiatement à la version la plus récente de votre application.

 
## Prise en charge du chiffrement dans l’API

À compter de la [mise à jour de mars 2015](release-notes-rtm.md), nos API et les packages de chiffrement associés comprennent les trois indicateurs suivants :

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (aussi appelé « algorithmes déconseillés »)

Vous pouvez utiliser les indicateurs de package de chiffrement (voir [**Chiffrement préféré**](/information-protection/sdk/2.1/api/win/constants#msipc_preferred_encryption)) conjointement avec notre nouvel indicateur de propriété de licence **IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE**.

Voici quelques extraits de code simples qui montrent comment utiliser la nouvelle propriété de licence.

## Algorithmes déconseillés

L’indicateur **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** n’est plus exposé dans notre API. Cela signifie que les futures applications ne seront plus compilées si elles font référence à cet indicateur. Toutefois, les applications déjà créées continueront de fonctionner dans la mesure où nous respecterons de manière privée l’indicateur dans le code de l’API.

Il est encore possible de tirer parti de l’ancien indicateur obsolète des algorithmes de chiffrement en modifiant simplement un indicateur. Pour obtenir des exemples, consultez les extraits de code suivants.

## Protéger les fichiers avec AES 256 CBC4K

Toute modification du code est inutile, car *AES 256* CBC4K est le chiffrement par défaut.

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## Protéger les fichiers avec AES 128 CBC4K

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## Protéger les fichiers avec AES-128 ECB (algorithmes déconseillés)

Cet exemple montre également la nouvelle façon de prendre en charge des *algorithmes déconseillés*.

    C++
    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

 

 



<!--HONumber=Sep16_HO5-->


