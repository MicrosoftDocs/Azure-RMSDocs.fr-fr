---
# required metadata

title: Installer et configurer le serveur | Azure RMS
description: Installez et configurez un serveur RMS pour tester votre application avec gestion des droits.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installer et configurer le serveur

Cette rubrique décrit les étapes d’installation et de configuration d’un serveur RMS pour tester votre application avec gestion des droits.

**Important** : Si vous testez votre application en l’exécutant sur l’environnement RMS ISV standard, il est inutile d’installer un serveur RMS, car celui-ci est déjà installé et configuré dans l’environnement standard.
Pour plus d’informations sur l’environnement AD RMS ISV standard, consultez [Configurer l’environnement de test](how-to-set-up-your-test-environment.md).

 

## Instructions

### Étape 1 : Configurer votre serveur RMS

La procédure suivante vous guide dans la configuration de votre serveur RMS et comprend les sections suivantes :

-   Configurer le Registre
-   Installer le serveur
-   Inscrire le serveur

1.  **Configurer le Registre**

    Pour spécifier que vous utilisez la hiérarchie des certificats de préproduction, définissez les valeurs de Registre suivantes.

    **Remarque** : Si vous utilisez Windows Server 2008 R2 ou Windows Server 2008, définissez les valeurs de Registre avant d’installer le service AD RMS.

    Si vous utilisez AD RMS sur Windows Server 2008 R2, vous devez définir la valeur **REG\_DWORD**. Définissez cette valeur sur 0 (zéro) pour basculer vers la hiérarchie de production.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    Si vous utilisez AD RMS sur Windows Server 2008 R2 et qu’un autre service AD RMS est déjà déployé dans Active Directory comme service de préproduction, ajoutez la valeur de chaîne vide suivante dans le Registre.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    Si vous utilisez AD RMS sur Windows Server 2008, vous devez définir la valeur **REG\_DWORD**. Définissez cette valeur sur 0 (zéro) pour basculer vers la hiérarchie de production.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    Si vous utilisez AD RMS sur Windows Server 2008 et qu’un autre service AD RMS est déjà déployé dans Active Directory comme service de préproduction, ajoutez la valeur de chaîne vide suivante dans le Registre.

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **Installer le serveur**

    Active Directory Rights Management Services (AD RMS) est constitué d’un composant client et d’un composant serveur. Le composant serveur est implémenté comme un ensemble de services web permettant de gérer une infrastructure RMS, d’émettre des licences pour les utilisateurs et les éditeurs de contenu, ainsi que d’émettre des certificats pour des utilisateurs et des ordinateurs.

    À partir de Windows Server 2008, les composants client et serveur sont compris dans le système d’exploitation. Vous pouvez télécharger les composants serveur des systèmes d’exploitation antérieurs à l’emplacement suivant.

    -   [Serveur RMS v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Pour configurer le composant serveur sur Windows Server 2008, vous devez installer le rôle AD RMS. Toutefois, vous devez d’abord configurer le Registre pour spécifier que vous allez utiliser la hiérarchie de certificats de préproduction plutôt que la hiérarchie de production. Si vous développez des applications sur une version antérieure d’un système d’exploitation serveur, configurez le Registre après l’installation du serveur RMS v1.0 SP2, mais avant l’approvisionnement du service RMS.

    Pour plus d’informations, consultez l’étape 1, « Configurer le Registre », ci-dessus.

3.  **Inscrire le serveur**

    Vous devez inscrire un serveur Rights Management Services (RMS) afin de l’identifier dans la hiérarchie de préproduction ou de production. Le processus d’inscription crée un certificat de licence serveur sur l’ordinateur serveur. Ce certificat est chaîné à une racine Microsoft de confiance. Le processus d’inscription du serveur dépend de la version RMS que vous utilisez.

    -   **Inscription automatique**

        Windows Server 2008 et versions ultérieures vous permettent d’inscrire un serveur RMS dans la hiérarchie appropriée sans envoyer d’informations à Microsoft. Quand vous installez le rôle RMS, un certificat d’inscription automatique et une clé privée sont également installés. Ceux-ci sont utilisés pour créer automatiquement le certificat de licence serveur. Aucune information n’est échangée avec Microsoft.

    -   **Inscription en ligne** Si vous utilisez AD RMS 1.0 Service Pack 2, vous pouvez inscrire le serveur en ligne. L’inscription s’effectue en arrière-plan pendant le processus de configuration. Pour cela, vous devez disposer d’une connexion Internet et spécifier la valeur de Registre appropriée pour identifier la hiérarchie dans laquelle vous inscrivez le serveur. Pour inscrire le serveur dans la hiérarchie de préproduction, ajoutez la valeur **REG\_SZ**, puis approvisionnez le serveur. Pour inscrire le serveur dans la hiérarchie de production, effacez la valeur, puis approvisionnez le serveur.

        Pour plus d’informations, consultez l’étape 1, « Configurer le Registre », ci-dessus.

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## Rubriques connexes

* [Utilisation de procédures](how-to-use-msipc.md)
 

 





<!--HONumber=Apr16_HO4-->


