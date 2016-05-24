---
# required metadata

title: Configurer le client| Azure RMS
description: Instructions sur la configuration d’Active Directory Rights Management Services Client 2.1
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 74C342BF-0F79-486D-AED7-C53230DE5FA7
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurer le client

Cette rubrique contient des instructions sur la configuration d’Active Directory Rights Management Services Client 2.1

**Important** : Si vous testez votre application en l’exécutant dans l’environnement RMS ISV standard, vous n’avez pas besoin de configurer AD RMS Client 2.1. Pour plus d’informations, consultez [Test de votre application avec gestion des droits](running-your-first-application.md).

 

### Conditions préalables

-   AD RMS Client 2.1 doit être installé sur l’ordinateur sur lequel vous testez votre application.

    -   Si vous testez votre application sur votre ordinateur de développement, vous devez déjà avoir installé Rights Management Services SDK 2.1. AD RMS Client 2.1 est installé en mode silencieux lors de l’installation du Kit.

        Pour plus d’informations sur la façon d’installer Rights Management Services SDK 2.1, consultez [Installer le SDK](create-your-first-rights-aware-application.md).

    -   Si vous testez votre application sur un ordinateur autre que votre ordinateur de développement, vous pouvez installer AD RMS Client 2.1 sur cet ordinateur à partir de la [page de téléchargement d’AD RMS Client 2.1](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
        **Remarque** : Si votre application utilise le mode API serveur (**IPC\_API\_MODE\_SERVER**), il n’est pas nécessaire d’utiliser un manifeste d’application. Vous pouvez tester votre application sur un serveur RMS de production et vous n’êtes pas obligé d’obtenir une licence de production quand vous passez à l’environnement de production. Pour plus d’informations sur les applications en mode serveur, consultez [Types d’applications](application-types.md).

         

-   Un serveur RMS doit être installé et configuré pour pouvoir utiliser l’environnement de préproduction. Pour plus d’informations, consultez [Installer et configurer le serveur](how-to-install-and-configure-an-rms-server.md).

Instructions

### Étape 1 : Configurer RMS Client 2.1 pour la hiérarchie de certificats de préproduction

Les étapes suivantes expliquent comment installer le runtime développeur, configurer le client pour qu’il utilise la hiérarchie de certificats ISV (de préproduction) et configurer la découverte de service sur le client.

1.  Copiez le runtime développeur (Ipcsecproc\_isv.dll) de l’emplacement %MSIPCSDKDIR%\\bin\\x86 (pour les versions 32 bits de Windows) ou %MSIPCSDKDIR\\bin\\x64 (pour les versions 64 bits de Windows) vers C:\\Program Files\\Active Directory Rights Management Services Client 2.1.

    **Important** Si vous exécutez une application 32 bits sur une version 64 bits de Windows, vous devez copier Ipcsecproc\_isv.dll de l’emplacement %MSIPCSDKDIR%\\bin\\x86 vers l’emplacement \\Active C:\\Program Files (x86) Directory Rights Management Services Client 2.1.

     

2.  Configurez AD RMS Client 2.1 pour qu’il utilise la hiérarchie de certificats ISV (de préproduction) en définissant la valeur de clé du Registre **Hierarchy** sur 1.

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **Remarque** D’un point de vue fonctionnel, le fait de ne pas inclure la valeur **Hierarchy** dans le Registre revient à la définir sur 0 (zéro), ce qui signifie que RMS SDK 2.1 fonctionne en mode de production. Pour plus d’informations sur les clés et les chaînes de certificats, consultez [Présentation des chaînes de certificats](understanding-certificate-chains.md).

    **Important**  
    Si vous exécutez une application 32 bits sur une version 64 bits de Windows, vous devez définir la valeur **Hierarchy** dans l’emplacement de clé suivant :

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  Configurez la découverte côté serveur ou côté client pour que AD RMS Client 2.1 découvre et établisse une communication avec votre serveur RMS de préproduction.

    -   Pour la découverte côté serveur, l’administrateur inscrit un point de connexion de service pour le cluster racine RMS de préproduction auprès d’Active Directory. Ainsi, le client interroge Active Directory pour découvrir le point de connexion de service et établir une connexion avec le serveur.
    -   Pour la découverte côté client, vous configurez des paramètres de découverte de service RMS dans le Registre de l’ordinateur sur lequel s’exécute AD RMS Client 2.1. Ces paramètres indiquent à AD RMS Client 2.1 le serveur RMS à utiliser. Quand de tels paramètres sont définis, la découverte côté serveur n’est pas lancée.

    Pour configurer la découverte côté client, vous pouvez définir les clés de Registre suivantes pour qu’elles pointent vers votre serveur RMS de préproduction. Pour plus d’informations sur la configuration de la découverte côté serveur, consultez [RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx) (Notes sur le déploiement de RMS Client 2.0).

|Clé|Valeur|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(par défaut) :<br><br> [**http**&#124;**https**]**://** *Nom_cluster_RMS* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(par défaut) :<br><br> [**http**&#124;**https**]**://** *Nom_cluster_RMS* **/_wmcs/Licensing**|


**Remarque** Par défaut, ces clés ne sont pas présentes dans le Registre et doivent être créées.
     
**Important**  
    Si vous exécutez une application 32 bits sur une version 64 bits de Windows, vous devez définir ces clés dans l’emplacement de clé suivant :


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### Remarques

Les instructions de cette rubrique ne sont pas exhaustives. Pour plus d’informations sur la configuration d’AD RMS Client 2.1, consultez [RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx) (Notes sur le déploiement de RMS Client 2.0).

## Rubriques connexes


* [Utilisation des procédures](how-to-use-msipc.md)
* [Notes sur le déploiement de RMS Client 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [Installer le SDK](create-your-first-rights-aware-application.md)
* [Installer et configurer le serveur](how-to-install-and-configure-an-rms-server.md)
* [Test de votre application avec gestion des droits](running-your-first-application.md)
* [Présentation des chaînes de certificats](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO4-->


