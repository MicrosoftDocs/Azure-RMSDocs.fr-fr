---
title: Procédure d’installation, de configuration et de test d’un serveur RMS | Azure RMS
description: Installez et configurez un serveur RMS pour tester votre application avec gestion des droits.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 59aa02318a0c6d7ee5e9857bead4c79248546320
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2019
ms.locfileid: "68794107"
---
# <a name="how-to-install-configure-and-test-with-an-rms-server"></a>Comment : installer, configurer et tester avec un serveur RMS

Cette rubrique décrit les étapes de connexion à un serveur RMS ou à Azure RMS à des fins de test de votre application avec gestion des droits.
 
## <a name="instructions"></a>Instructions

### <a name="step-1-setup-your-rms-server"></a>Étape 1 : Configurer votre serveur RMS

La procédure suivante vous guide dans la configuration de votre serveur RMS et comprend les sections suivantes :

-   Installer le serveur
-   Inscrire le serveur

1. **Installer le serveur**

   Active Directory Rights Management Services (AD RMS) est constitué d’un composant client et d’un composant serveur. Le composant serveur est implémenté comme un ensemble de services web permettant de gérer une infrastructure RMS, d’émettre des licences pour les utilisateurs et les éditeurs de contenu, ainsi que d’émettre des certificats pour des utilisateurs et des ordinateurs.

   À partir de Windows Server 2008, les composants client et serveur sont compris dans le système d’exploitation. Vous pouvez télécharger les composants serveur des systèmes d’exploitation antérieurs à l’emplacement suivant.

   -   [Serveur RMS v1.0 SP2](https://go.microsoft.com/fwlink/p/?linkid=73722)

   Pour configurer le composant serveur sur Windows Server 2008, vous devez installer le rôle AD RMS. Si vous développez des applications sur une version antérieure d’un système d’exploitation serveur, configurez le Registre après l’installation du serveur RMS v1.0 SP2, mais avant l’approvisionnement du service RMS.

2. **Inscrire le serveur**

   Vous devez inscrire un serveur Rights Management Services (RMS) afin de l’identifier dans la hiérarchie de préproduction ou de production. Le processus d’inscription crée un certificat de licence serveur sur l’ordinateur serveur. Ce certificat est chaîné à une racine Microsoft de confiance. Le processus d’inscription du serveur dépend de la version RMS que vous utilisez.

   -   **Inscription automatique**

       Windows Server 2008 et versions ultérieures vous permettent d’inscrire un serveur RMS dans la hiérarchie appropriée sans envoyer d’informations à Microsoft. Quand vous installez le rôle RMS, un certificat d’inscription automatique et une clé privée sont également installés. Ceux-ci sont utilisés pour créer automatiquement le certificat de licence serveur. Aucune information n’est échangée avec Microsoft.

   -   **Inscription en ligne**

       Si vous utilisez AD RMS v1.0 SP 2, vous pouvez inscrire le serveur en ligne. L’inscription s’effectue en arrière-plan pendant le processus d’approvisionnement, mais vous devez disposer d’une connexion Internet.

       **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **Tester avec le serveur RMS**

    Pour un test avec un serveur RMS, configurez la découverte côté serveur ou côté client pour activer le client Rights Management Services 2.1 afin de découvrir et d’établir la communication avec votre serveur RMS.

    > [!Note]
    > Le test avec Azure RMS ne nécessite pas de configuration de la découverte.

   - Pour la découverte côté serveur, l’administrateur inscrit un point de connexion de service pour le cluster racine RMS auprès d’Active Directory. Ainsi, le client interroge Active Directory pour découvrir le point de connexion de service et établir une connexion avec le serveur.
   - Pour la découverte côté client, vous configurez des paramètres de découverte de service RMS dans le Registre de l’ordinateur sur lequel s’exécute le client RMS 2.1. Ces paramètres indiquent au client RMS 2.1 le serveur RMS à utiliser. Quand de tels paramètres sont définis, la découverte côté serveur n’est pas lancée.

   Pour configurer la découverte côté client, vous pouvez définir les clés de Registre suivantes pour qu’elles pointent vers votre serveur RMS. Pour plus d’informations sur la configuration de la découverte côté serveur, consultez les [notes sur le déploiement du client RMS 2.0](https://technet.microsoft.com/library/jj159267(WS.10).aspx).

4. **EnterpriseCertification**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterpriseCertification

   **Valeur** : (Par défaut) : [**http|https**]://RMSClusterName/**_wmcs/Certification**

5. **EnterprisePublishing**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterprisePublishing
                  
   **Valeur** : (Par défaut) :[**http|https**]://RMSClusterName/**_wmcs/Licensing**

> [!NOTE]
> Par défaut, ces clés n’existent pas dans le Registre et doivent être créées.
> 
> [!IMPORTANT]
> Si vous exécutez une application 32 bits sur une version 64 bits de Windows, vous devez définir ces clés dans l’emplacement de clé suivant :<p>
>   ```    
>   HKEY_LOCAL_MACHINE
>     SOFTWARE
>       Wow6432Node
>         Microsoft
>           MSIPC
>             ```
