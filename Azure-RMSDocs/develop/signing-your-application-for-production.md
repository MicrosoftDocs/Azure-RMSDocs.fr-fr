---
# required metadata

title: Signature de votre application pour la production | Azure RMS
description: Cette rubrique vous guide tout au long du processus de signature de votre application pour le mode de production.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 09BA148C-7D1E-43C8-92EA-24BBB6EFDB19
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Signature de votre application pour la production

Cette rubrique vous guide tout au long du processus de signature de votre application pour le mode de production.

## Signer votre application avec gestion des droits

Ces étapes supposent que vous avez déjà signé votre application pour une hiérarchie de préproduction. Si vous ne l’avez pas déjà fait, parcourez le processus décrit dans [Test de votre application avec gestion des droits](running-your-first-application.md).

Une fois que vous avez reçu le certificat de production de Microsoft, vous disposez des fichiers suivants :

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

Placez-les dans le même répertoire que *GenManifest.exe* et le fichier binaire de votre application (.exe).

-   Le processus ci-dessous vous guide dans la création d’un fichier MCF avec un certificat de production :

    -   Créez un répertoire et placez-y les fichiers. Utilisez Notepad.exe pour créer un fichier MCF pour votre application. Le fichier doit contenir ce qui suit.

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   Exécutez la commande suivante pour signer votre application :

        **genmanifest.exe -chain ProductionCertificate.xml** *Nom_de_votre_application***.mcf** *Nom_de_votre_application***.exe.man**

        Si Genmanifest s’exécute correctement, seul le texte suivant s’affiche :

        Si Genmanifest échoue, un message d’erreur s’affiche.

    -   Votre fichier *Nom_de_votre_application*.exe.man doit toujours se trouver dans le même répertoire que *Nom_de_votre_application*.exe.

## Rubriques connexes

* [Procédures](how-to-use-msipc.md)
* [Test de votre application avec gestion des droits](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


