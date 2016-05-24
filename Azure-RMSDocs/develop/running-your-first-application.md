---
# required metadata

title: Test de votre application avec gestion des droits | Azure RMS
description: Décrit les étapes que vous devez effectuer pour tester votre application RMS SDK 2.1 avec gestion des droits.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834B7242-31D3-4275-A892-CFE95A61E29E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Test de votre application avec gestion des droits

Cette rubrique décrit les étapes que vous devez effectuer pour tester votre application Rights Management Services SDK 2.1 avec gestion des droits.

Pour publier et consommer du contenu protégé, une application Rights Management Services (RMS) fait appel à plusieurs types de certificats et de licences différents, dont chacun se compose d’une chaîne de certificat qui renvoie finalement à une autorité de certification Microsoft. Microsoft propose les hiérarchies suivantes :

-   La hiérarchie de préproduction permet de développer et de tester des applications.
-   La hiérarchie de production doit être utilisée par les applications publiées

Nous vous recommandons d’utiliser la hiérarchie de préproduction lors du développement d’une application. Vous pourrez ainsi travailler sans avoir à signer de contrat de licence de production auprès de Microsoft.

> [!IMPORTANT]
> Nous vous recommandons de tester votre application RMS SDK 2.1 d’abord avec l’environnement de préproduction RMS sur un serveur RMS. Ensuite, si vous souhaitez que votre client puisse utiliser votre application avec le service Azure RMS, effectuez les tests avec cet environnement. Pour plus d’informations, consultez [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Permettre à votre application de service d’opérer avec le service RMS cloud).

 

### Conditions préalables

-   Une installation de l’environnement de développement RMS SDK 2.1. Pour plus d’informations, consultez [Setting up the pre-production development environment](how-to-set-up-the-pre-production-development-environment.md) (Installation de l’environnement de développement de préproduction).
-   Pour obtenir un exemple d’application, consultez [IPCHelloWorld - an example application](how-to-build-your-first-application.md) (Exemple d’application IPCHelloWorld).

Instructions

### Étape 1 :

Créer et générer une application avec gestion des droits. Consultez la section Conditions préalables ci-dessus pour connaître les options.

### Étape 2 : générer un manifeste d’application en utilisant la chaîne de certificats de préproduction

Vous devez générer un manifeste pour votre application avant de l’exécuter.

**Remarque**  Si votre application utilise le mode API serveur (**IPC\_API\_MODE\_SERVER**), il n’est pas nécessaire d’utiliser un manifeste d’application. Vous pouvez tester votre application sur un serveur AD RMS de production, vous n’êtes alors pas obligé d’obtenir une licence de production quand vous passez à l’environnement de production. Pour plus d’informations sur les applications en mode serveur, consultez [Application types](application-types.md) (Types d’applications).

 

C’est aussi ce que l’on appelle signer une application. Vous pouvez générer le manifeste en utilisant une chaîne de certificats de production ou la chaîne de certificats de préproduction qui est installée avec le SDK. Nous vous recommandons d’utiliser la chaîne de certificats de préproduction pendant le développement.

Pour plus d’informations sur les clés et les chaînes de certificats, consultez [Understanding certificate chains](understanding-certificate-chains.md) (Présentation des chaînes de certificats).

Pour plus d’informations sur la signature d’une application avec une chaîne de certificats de production, consultez [Switching to the production environment](switching-to-the-production-environment.md) (Passer à l’environnement de production).

Pour générer le manifeste d’application à l’aide de la chaîne de certificats de préproduction, effectuez ces étapes sur votre ordinateur de développement :

1.  Copiez les fichiers suivants de leurs répertoires d’installation vers le dossier correspondant de votre application.

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\NomApp.isv.mcf

2.  Dans le dossier de votre application, renommez le fichier de configuration de manifeste, NomApp.isv.mcf, en lui attribuant le nom de votre application et en lui ajoutant l’extension de nom de fichier .mcf. Par exemple, si votre application se nomme MonApp.exe, remplacez NomApp.isv.mcf par MonApp.exe.mcf.

3.  Utilisez un éditeur de texte pour ajouter votre application au fichier de configuration de manifeste. Pour ce faire, remplacez le texte de l’espace réservé &lt;NomApp&gt;.exe figurant dans la liste des modules de votre fichier .mcf par le nom de votre application ; par exemple, MonApp.exe.

    Le processus de signature génère une erreur si le fichier .mcf est utilisé sans avoir été modifié.

4.  Exécutez Genmanifest.exe pour générer le manifeste d’application. C’est aussi ce que l’on appelle signer une application. Cette opération doit donner lieu à la création d’un fichier .man. Par exemple, si votre application se nomme MonApp.exe et que votre fichier de configuration de manifeste se nomme MonApp.exe.mcf, exécutez la commande suivante :

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MonApp.exe.mcf MonApp.exe.man**

### Étape 3 : exécuter votre application

Vous pouvez exécuter votre application à partir de n’importe quel répertoire, mais le manifeste d’application (MonApp.exe.man) doit se trouver dans le même répertoire que l’exécutable (MonApp.exe).

-   **Utilisation de l’environnement RMS 1-Box**

    Si vous utilisez l’environnement RMS 1-box pour tester votre application, copiez l’exécutable de votre application et le manifeste d’application dans un répertoire de l’environnement 1-box, puis exécutez votre application.

    Pour plus d’informations sur l’environnement RMS 1-box, consultez [Set up the test environment](how-to-set-up-your-test-environment.md) (Installer l’environnement de test).

-   **Utilisation d’une configuration serveur de préproduction**

    Si vous testez votre application sur un serveur RMS configuré pour la préproduction, assurez-vous d’avoir configuré Active Directory Rights Management Services Client 2.1 sur l’ordinateur où l’application sera exécutée (par exemple, sur votre ordinateur de développement). Ensuite, vérifiez que l’exécutable de l’application et le manifeste d’application se trouvent bien dans le même répertoire de cet ordinateur, puis exécutez votre application.

    Pour obtenir des informations sur la configuration du client sur votre ordinateur, consultez [Configure the client](how-to-configure-the-ad-rms-client-2-0.md) (Configurer le client). Pour obtenir des informations sur l’installation d’un serveur RMS, consultez [Install and configure the server](how-to-install-and-configure-an-rms-server.md) (Installer et configurer le serveur).

## Rubriques connexes

* [How-to use (Utilisation de procédures)](how-to-use-msipc.md)
* [Configure the client (Configurer le client)](how-to-configure-the-ad-rms-client-2-0.md)
* [Install and configure the server (Installer et configurer le serveur)](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - an example application (Exemple d’application IPCHelloWorld)](how-to-build-your-first-application.md)
* [Setting up the pre-production development environment (Installation de l’environnement de développement de préproduction)](how-to-set-up-the-pre-production-development-environment.md)
* [Switching to the production environment (Passer à l’environnement de production)](switching-to-the-production-environment.md)
* [Set up the test environment (Installer l’environnement de test)](how-to-set-up-your-test-environment.md)
* [Understanding certificate chains (Présentation des chaînes de certificats)](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO4-->


