---
# required metadata

title: Configurer l’environnement de test | Azure RMS
description: Vous pouvez tester votre application avec gestion des droits à l’aide de plusieurs options du serveur.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurer l’environnement de test

Vous pouvez tester votre application avec gestion des droits à l’aide de plusieurs options du serveur.

**Important**  Nous vous recommandons de tester votre application Rights Management Services SDK 2.1 d’abord avec l’environnement de préproduction AD RMS sur un serveur AD RMS. Ensuite, si vous souhaitez que votre client puisse utiliser votre application avec le service Azure RMS, passez aux tests avec cet environnement. Pour plus d’informations, consultez [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Permettre à votre application de service d’opérer avec le service RMS cloud).

 

### Conditions préalables

-   [Installer le SDK](create-your-first-rights-aware-application.md)

Instructions

### Étape 1 : Configurer votre environnement de test

Pour tester votre application avec gestion des droits, vous devez l’exécuter sur un serveur RMS configuré pour la préproduction. Un serveur RMS de préproduction utilise la hiérarchie des certificats ISV/préproduction pour chiffrer et déchiffrer les fichiers.

Pour plus d’informations sur la hiérarchie des certificats AD RMS, consultez [Présentation des chaînes de certificats](understanding-certificate-chains.md).

Deux options sont disponibles pour tester votre application sur un serveur RMS :

-   **Vous pouvez exécuter votre application sur l’environnement AD RMS ISV 1-box**. Si vous exécutez Windows Server 2012, Windows Server 2008 R2 ou Windows Server 2008 et que Hyper-V est installé, vous pouvez déployer l’environnement AD RMS ISV 1-box en créant une machine virtuelle à l’aide du VHD AD RMS 1-box. L’environnement AD RMS ISV 1-box fournit un serveur RMS configuré pour la préproduction et sur lequel Active Directory Rights Management Services Client 2.1 est installé. Les paramètres du Registre pour le serveur et le client RMS sont déjà configurés. Pour tester votre application, exécutez-la sur la machine virtuelle sur laquelle l’environnement 1-box est déployé.
-   **Vous pouvez exécuter votre application sur un serveur RMS configuré pour la préproduction et déployé sur votre réseau**. Dans ce cas, vous devez également installer et configurer AD RMS Client 2.1 sur l’ordinateur où votre application s’exécutera. Pour plus d’informations sur la procédure à suivre, consultez [Configurer le client](how-to-configure-the-ad-rms-client-2-0.md). Pour plus d’informations sur la façon de déployer un serveur RMS et de le configurer pour la préproduction, consultez [Installer et configurer le serveur](how-to-install-and-configure-an-rms-server.md).

## Rubriques connexes

* [Procédures](how-to-use-msipc.md)
* [Page de téléchargement des éléments associés au webinaire AD RMS SDK](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [Configurer le client](how-to-configure-the-ad-rms-client-2-0.md)
* [Installer le SDK](create-your-first-rights-aware-application.md)
* [Installer et configurer le serveur](how-to-install-and-configure-an-rms-server.md)
* [Présentation des chaînes de certificats](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO4-->


