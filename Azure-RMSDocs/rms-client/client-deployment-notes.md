---
title: Notes sur le déploiement du client RMS - Azure Information Protection
description: Informations à propos de l’installation, des systèmes d’exploitation pris en charge, des paramètres du Registre et de la découverte du service pour le client Rights Management Service (client RMS) version 2, également appelé client MSIPC.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 03cc8c6f-3b63-4794-8d92-a5df4cdf598f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0af65b69d28c97e547c0d0bce9e3024402b28dee
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259641"
---
# <a name="rms-client-deployment-notes"></a>Notes sur le déploiement du client RMS

>*S’applique à : Services AD RMS (Active Directory Rights Management Services), [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 7 avec SP1, Windows 8, Windows 8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016*

Le client service Rights Management (client RMS) version 2 est également appelé client MSIPC. Il s'agit d'un logiciel pour ordinateurs Windows, qui communique avec les services Microsoft Rights Management localement ou dans le cloud pour protéger l'accès aux informations et leur utilisation quand celles-ci transitent par des applications et appareils, à l'intérieur ou à l'extérieur des limites managées de votre organisation. 

Outre le fait qu’il est livré avec [le client Azure Information Protection pour Windows](aip-client.md), le client RMS est disponible [sous la forme d’un téléchargement facultatif](https://www.microsoft.com/download/details.aspx?id=38396) qui peut, après réception et acceptation de son contrat de licence, être distribué gratuitement avec des logiciels tiers, de sorte que les clients peuvent protéger et utiliser du contenu protégé par les services RMS.


## <a name="redistributing-the-rms-client"></a>Redistribution du client RMS
Le client RMS peut être librement redistribué et regroupé avec d'autres applications et solutions informatiques. Si vous êtes développeur d'applications ou fournisseur de solutions, et souhaitez redistribuer le client RMS, vous avez deux options :

- Recommandé : Incorporez le programme d’installation du client RMS dans votre installation d’application et exécutez-le en mode silencieux (commutateur **/quiet**, détaillé dans la section suivante).

- Faites du client RMS une condition préalable pour votre application. Avec cette option, vous devrez peut-être fournir aux utilisateurs des instructions supplémentaires pour obtenir, installer et mettre à jour leurs ordinateurs avec le client avant de pouvoir utiliser votre application.

## <a name="installing-the-rms-client"></a>Installation du client RMS
Le client RMS est contenu dans un fichier exécutable d’installation nommé **setup_msipc_*\<arch\>*.exe**, où *\<arch>* est **x86** (pour les ordinateurs clients 32 bits) ou **x64** (pour les ordinateurs clients 64 bits). Le package d'installation 64 bits (x64) installe un exécutable runtime 32 bits pour la compatibilité avec les applications 32 bits qui s'exécutent sur une installation de système d'exploitation 64 bits, ainsi qu'un exécutable runtime 64 bits pour la prise en charge des applications 64 bits natives. Le programme d’installation 32 bits (x86) ne s’exécute pas sur une installation de Windows 64 bits.

> [!NOTE]
> Pour installer le client RMS, vous avez besoin de privilèges élevés, comme ceux d’un membre du groupe Administrateurs sur l’ordinateur local.

Vous pouvez installer le client RMS à l'aide de l'une des méthodes d'installation suivantes :

- **Mode silencieux.** L’utilisation du commutateur **/quiet** parmi les options de ligne de commande permet d’installer le client RMS en mode silencieux sur des ordinateurs. L'exemple suivant illustre une installation en mode silencieux du client RMS sur un ordinateur client 64 bits :

    ```
    setup_msipc_x64.exe /quiet
    ```

- **Mode interactif.** Autrement, vous pouvez installer le client RMS en utilisant le programme d’installation basé sur l’interface graphique utilisateur fourni par l’Assistant Installation du client RMS. Pour une installation interactive, double-cliquez sur le package d’installation du client RMS (**setup_msipc_*\<arch\>*.exe**) dans le dossier dans lequel il a été copié ou téléchargé sur votre ordinateur local.

## <a name="questions-and-answers-about-the-rms-client"></a>Questions et réponses sur le client RMS
La section suivante contient des questions fréquemment posées sur le client RMS et les réponses à celles-ci.

### <a name="which-operating-systems-support-the-rms-client"></a>Quels systèmes d'exploitation prennent en charge le client RMS ?
Le client RMS est pris en charge par les systèmes d'exploitation suivants :

|Système d'exploitation Windows Server|Système d'exploitation Windows Client|
|-----------------------------------|-----------------------------------|
|Windows Server 2016|Windows 10|
|Windows Server 2012 R2|Windows 8.1|
|Windows Server 2012|Windows 8|
|Windows Server 2008 R2|Windows 7 avec au minimum SP1|


### <a name="which-processors-or-platforms-support-the--rms-client"></a>Quels processeurs ou plates-formes prennent en charge le client RMS ?
Le client RMS est pris en charge sur les plates-formes de calcul x86 et x64.

### <a name="where-is-the--rms-client-installed"></a>Où est installé le client RMS ?
Par défaut, le client RMS est installé dans %ProgramFiles%\Active Directory Rights Management Services Client 2.\<numéro de version mineure>.

### <a name="what-files--are-associated-with-the-rms-client-software"></a>Quels fichiers sont associés au logiciel du client RMS ?
Les fichiers installés en même temps que le logiciel du client RMS sont les suivants :

-   Msipc.dll

-   Ipcsecproc.dll

-   Ipcsecproc_ssp.dll

-   MSIPCEvents.man

Outre ces fichiers, le client RMS installe des fichiers de prise en charge d'interface utilisateur multilingue (MUI) dans 44 langues. Pour vérifier les langues prises en charge, exécutez l'installation du client RMS, puis, une fois l'installation terminée, examinez le contenu des dossiers de prise en charge multilingue sous le chemin d'accès par défaut.

### <a name="is-the-rms-client-included-by-default-when-i-install-a-supported-operating-system"></a>Le client RMS est-il inclus par défaut lors de l'installation d'un système d'exploitation pris en charge ?
Non. Cette version du client RMS est fournie en tant que téléchargement facultatif pouvant être installé séparément sur des ordinateurs exécutant les versions prises en charge du système d'exploitation Microsoft Windows.

### <a name="is-the-rms-client-automatically-updated-by-microsoft-update"></a>Le client RMS est-il automatiquement mis à jour par Microsoft Update ?
Si vous avez utilisé l’option d’installation silencieuse pour installer ce client RMS, celui-ci hérite des paramètres actuels de Microsoft Update. Si vous avez installé le client RMS à l’aide du programme d’installation basé sur l’interface utilisateur graphique, l’Assistant Installation du client RMS vous invite à activer Microsoft Update.

## <a name="rms-client-settings"></a>Paramètres du client RMS
La section suivante contient des informations de paramètres sur le client RMS. Ces informations peuvent être utiles si vous rencontrez des problèmes avec des applications ou services utilisant le client RMS.

> [!NOTE]
> Certains paramètres varient selon que l’application compatible avec RMS s’exécute en tant qu’application en mode client (par exemple, Microsoft Word et Outlook, ou le client Azure Information Protection avec l’Explorateur de fichiers Windows), ou en mode serveur (par exemple, SharePoint et Exchange). Dans les tableaux suivants, ces paramètres sont identifiés respectivement comme **Mode Client** et **Mode serveur**.

### <a name="where-the-rms-client-stores-licenses-on-client-computers"></a>Où le client RMS stocke-t-il les licences sur les ordinateurs clients ?
Le client RMS stocke les licences sur le disque local et met également en cache des informations dans le Registre Windows.

|Description|Chemins d'accès du mode client|Chemins d'accès du mode serveur|
|---------------|---------------------|---------------------|
|Emplacement du magasin de licences|%localappdata%\Microsoft\MSIPC|%allusersprofile%\Microsoft\MSIPC\Server\\*\<SID\>*|
|Emplacement du magasin de modèles|%localappdata%\Microsoft\MSIPC\Templates|%allusersprofile%\Microsoft\MSIPC\Server\\*\<SID\>*|
|Emplacement du Registre|HKEY_CURRENT_USER<br /> \Software<br /> \Classes<br /> \Local Settings<br /> \Software<br /> \Microsoft<br /> \MSIPC|HKEY_CURRENT_USER<br /> \Software<br /> \Microsoft<br /> \MSIPC<br /> \Server<br /> \\*\<SID*\>|

> [!NOTE]
> *\<SID*> est l’identificateur sécurisé du compte sous lequel s’exécute l’application serveur. Par exemple, si l'application s'exécute sous le compte de service réseau intégré, remplacez *\<SID\>* par la valeur du SID connu pour ce compte (S-1-5-20).

### <a name="windows-registry-settings-for-the-rms-client"></a>Paramètres du Registre Windows pour le client RMS
Vous pouvez utiliser des clés de Registre Windows pour définir ou modifier des configurations de client RMS. Par exemple, en tant qu’administrateur d’applications compatibles avec RMS qui communiquent avec des serveurs AD RMS, il se peut que vous souhaitiez mettre à jour l’emplacement du service d’entreprise (pour remplacer le serveur AD RMS actuellement sélectionné pour la publication) en fonction de l’emplacement actuel de l’ordinateur client dans votre topologie Active Directory. Vous pouvez également activer le suivi RMS sur l’ordinateur client pour faciliter la résolution d’un problème lié à une application compatible avec RMS. Utilisez le tableau suivant pour identifier les paramètres de Registre que vous pouvez modifier pour le client RMS.


|                                                                                                  Tâche                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Paramètres                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                  Si la version du client est la version 1.03102.0221 ou une version ultérieure :<br /><br />**Pour contrôler la collecte de données d’application**                                                  | **Important** : En tant qu’administrateur, afin de respecter la confidentialité de l’utilisateur, vous devez lui demander son consentement avant d’activer la collecte de données.<br /><br />Si vous activez la collecte de données, vous acceptez d’envoyer des données à Microsoft via Internet. Microsoft utilise ces données pour garantir et améliorer la qualité, la sécurité et l’intégrité des produits et services Microsoft. Par exemple, Microsoft analyse les performances et la fiabilité, comme les fonctionnalités que vous utilisez, la rapidité de réponse des fonctionnalités, les performances de l’appareil, les interactions de l’interface utilisateur et tous les problèmes que vous rencontrez avec le produit. Ces données incluent également des informations sur la configuration de vos logiciels, comme le logiciel en cours d’exécution et l’adresse IP.<br /><br />Pour la version 1.0.3356 ou ultérieure : <br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft\MSIPC<br />REG_DWORD: DiagnosticAvailability<br /><br />Pour les versions antérieures à 1.0.3356 : <br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft\MSIPC<br />REG_DWORD: DiagnosticState<br /><br />**Valeur :** 0 pour Défini par l’application (par défaut) à l’aide de la propriété d’environnement [IPC_EI_DATA_COLLECTION_ENABLED](https://msdn.microsoft.com/library/hh535247(v=vs.85).aspx), 1 pour Désactivé, 2 pour Activé<br /><br />**Remarque** : Si votre application MSIPC 32 bits s’exécute sur une version 64 bits de Windows, l’emplacement est HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC. |
|                                                       AD RMS uniquement :<br /><br />**Pour mettre à jour l’emplacement du service d’entreprise d’un ordinateur client**                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Modifiez la clé de Registre suivante :<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterpriseCertification<br />REG_SZ: default<br /><br />**Valeur:**\<http ou https>://*RMS_Cluster_Name*/_wmcs/Certification<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation\EnterprisePublishing<br />REG_SZ: default<br /><br />**Valeur :** \<http ou https>://*RMS_Cluster_Name*/_wmcs/Licensing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                    **Pour activer et désactiver le suivi**                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    Mettez à jour la clé de registre suivante :<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC<br />REG_DWORD: Trace<br /><br />**Valeur :** 1 pour activer le suivi, 0 pour désactiver le suivi (par défaut)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                        **Pour modifier la fréquence en jours d’actualisation des modèles**                                                                         |                                                                                                                                                                                                                                                                                Les valeurs suivantes du Registre spécifient la fréquence à laquelle les modèles sont actualisés sur l’ordinateur de l’utilisateur si la valeur TemplateUpdateFrequencyInSeconds n'est pas définie.  Si aucune de ces valeurs n'est définie, l'intervalle d'actualisation par défaut pour les applications utilisant le client RMS (version 1.0.1784.0) pour télécharger des modèles est de 1 jour. Les versions antérieures ont une valeur par défaut : tous les 7 jours.<br /><br />**Mode client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valeur :** Valeur entière spécifiant le nombre de jours (au minimum 1) entre les téléchargements.<br /><br />**Mode serveur:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\<SID\><br />REG_DWORD: TemplateUpdateFrequency<br /><br />**Valeur :** Valeur entière spécifiant le nombre de jours (au minimum 1) entre les téléchargements.                                                                                                                                                                                                                                                                                 |
| **Pour modifier la fréquence en secondes d’actualisation des modèles**<br /><br />Important : Si ce paramètre est spécifié, la valeur d’actualisation en jours des modèles est ignorée. Spécifiez une ou l'autre, pas les deux. |                                                                                                                                                                                                                                                                   Les valeurs de Registre suivantes spécifient la fréquence à laquelle les modèles sont actualisés sur l'ordinateur de l'utilisateur. Si cette valeur ou la valeur modifiant la fréquence en jours (TemplateUpdateFrequency) n’est pas définie, l’intervalle d’actualisation par défaut pour les applications utilisant le client RMS (version 1.0.1784.0) pour télécharger des modèles est d’une journée. Les versions antérieures ont une valeur par défaut : tous les 7 jours.<br /><br />**Mode client:**<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valeur :** Valeur entière spécifiant le nombre de secondes (au minimum 1) entre les téléchargements.<br /><br />**Mode serveur:**<br /><br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\Server\\<*SID*><br />REG_DWORD: TemplateUpdateFrequencyInSeconds<br /><br />**Valeur :** Valeur entière spécifiant le nombre de secondes (au minimum 1) entre les téléchargements.                                                                                                                                                                                                                                                                    |
|                                                      AD RMS uniquement :<br /><br />**Pour télécharger les modèles immédiatement à la prochaine demande de publication**                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                 Durant les tests et évaluations, il se peut que vous souhaitiez que le client RMS télécharge les modèles dès que possible. Pour cette configuration, supprimez la clé de Registre suivante. Ainsi, le client RMS télécharge les modèles immédiatement à la prochaine demande de publication au lieu d’attendre l’heure spécifiée par le paramètre de Registre TemplateUpdateFrequency :<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*Nom de serveur*>\Template <br /><br />**Remarque** : \<*Nom du serveur*> peut avoir des URL externes (corprights.contoso.com) et internes (corprights), et donc deux entrées différentes.                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                               AD RMS uniquement :<br /><br />**Pour activer la prise en charge de l’authentification fédérée**                                                                |                                                                                                                                                                                                                                                                             Si l'ordinateur client RMS se connecte à un cluster AD RMS en utilisant une approbation fédérée, vous devez configurer le domaine d'accueil de fédération.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_SZ: FederationHomeRealm<br /><br />**Valeur :** La valeur de cette entrée de Registre est l’URI (Uniform Resource Identifier) du service de fédération (par exemple « <http://TreyADFS.trey.net/adfs/services/trust> »).<br /><br /> **Remarque** : Il est important de spécifier http et non pas https pour cette valeur. De plus, si votre application MSIPC 32 bits s’exécute sur une version 64 bits de Windows, l’emplacement est HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Federation. Pour obtenir un exemple de configuration, consultez [Déploiement des services AD RMS (Active Directory Rights Management Services) avec les services ADFS (Active Directory Federation Services)](https://technet.microsoft.com/library/dn758110.aspx).                                                                                                                                                                                                                                                                             |
|                                        AD RMS uniquement :<br /><br />**Pour prendre en charge les serveurs de fédération de partenaires qui requièrent une authentification basée sur les formulaires pour l’entrée utilisateur**                                         |                                                                                                                                                                                                                                                                                                                                                             Par défaut, le client RMS fonctionne en mode silencieux et l’entrée utilisateur n’est pas nécessaire. Toutefois, les serveurs de fédération de partenaires peuvent être configurés pour exiger une entrée utilisateur, telle qu'une authentification basée sur les formulaires. Dans ce cas, vous devez configurer le client RMS pour ignorer le mode silencieux afin que le formulaire d’authentification fédérée s’affiche dans une fenêtre de navigateur et que l’utilisateur soit invité à s’authentifier.<br /><br />HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\Federation<br />REG_DWORD: EnableBrowser<br /><br />**Remarque** : Si le serveur de fédération est configuré pour utiliser l'authentification basée sur les formulaires, cette clé est obligatoire. Si le serveur de fédération est configuré pour utiliser l’authentification Windows intégrée, cette clé n’est pas nécessaire.                                                                                                                                                                                                                                                                                                                                                             |
|                                                                      AD RMS uniquement :<br /><br />**Pour bloquer la consommation de services ILS**                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                 Par défaut, le client RMS autorise la consommation de contenu protégé par le service ILS, mais vous pouvez configurer le client pour bloquer ce service en définissant la clé de Registre suivante. Si cette clé de Registre est définie pour bloquer le service ILS, toute tentative d’ouvrir et de consommer du contenu protégé par le service ILS retourne l’erreur suivante :<br />HRESULT_FROM_WIN32(ERROR_ACCESS_DISABLED_BY_POLICY)<br /><br />HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC<br />REG_DWORD: **DisablePassportCertification**<br /><br />**Valeur :** 1 pour bloquer la consommation ILS, 0 pour autoriser la consommation ILS (par défaut)                                                                                                                                                                                                                                                                                                                                                                                                                  |

### <a name="managing-template-distribution-for-the-rms-client"></a>Gestion de la distribution de modèles pour le client RMS
Avec les modèles, il est plus simple pour les utilisateurs et les administrateurs d’appliquer rapidement la protection de Rights Management, et le client RMS télécharge automatiquement des modèles à partir de ses serveurs RMS ou de son service. Si vous placez les modèles dans le dossier suivant, le client RMS ne télécharge pas les modèles à partir de son emplacement par défaut, mais télécharge plutôt les modèles que vous avez placés dans ce dossier. Il se peut que le client RMS continue à télécharger des modèles à partir d'autres serveurs RMS disponibles.

**Mode client:** %localappdata%\Microsoft\MSIPC\UnmanagedTemplates

**Mode serveur:**%allusersprofile%\Microsoft\MSIPC\Server\UnmanagedTemplates\\*\<SID\>*

Lorsque vous utilisez ce dossier, aucune convention d'affectation de noms particulière ne s'impose, sauf que les modèles doivent être émis par le serveur ou le service RMS, et doivent avoir l'extension de nom de fichier .xml. Par exemple, Contoso-Confidential.xml ou Contoso-ReadOnly.xml sont des noms valides.

## <a name="ad-rms-only-limiting-the-rms-client-to-use-trusted-ad-rms-servers"></a>AD RMS uniquement : Limitation du client RMS à l’utilisation de serveurs AD RMS approuvés
Vous pouvez limiter le client RMS à l'utilisation exclusive de serveurs AD RMS de confiance spécifiques en apportant les modifications suivantes au Registre Windows sur des ordinateurs locaux.

**Pour activer la limitation du client RMS à l’utilisation des seuls serveurs AD RMS approuvés**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\

    REG_DWORD:AllowTrustedServersOnly

    **Valeur :** Si une valeur différente de zéro est spécifiée, le client RMS approuve uniquement les serveurs spécifiés configurés dans la liste TrustedServers et le service Azure Rights Management.

**Pour ajouter des membres à la liste des serveurs AD RMS approuvés**

-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\TrustedServers\

    REG_SZ:*\<URL_ou_NomHôte>*

    **Valeur :** Les valeurs de chaîne de cet emplacement de clé de Registre peuvent être au format de nom de domaine DNS (par exemple **adrms.contoso.com**) ou des URL complètes de serveurs AD RMS approuvés (par exemple **https://adrms.contoso.com**). Si une URL spécifiée commence par **https://**, le client RMS utilise le protocole SSL ou TLS pour contacter le serveur AD RMS spécifié.

## <a name="rms-service-discovery"></a>Découverte du service RMS
La découverte du service RMS permet au client RMS de vérifier avec quel serveur ou service RMS communiquer avant de protéger le contenu. La découverte du service peut également se produire quand le client RMS consomme du contenu protégé. Ce type de découverte est cependant moins probable, car la stratégie attachée au contenu contient le serveur ou service RMS préféré. Le client exécute la découverte de service uniquement si ces sources sont infructueuses.

Pour réaliser la découverte du service, le client RMS vérifie les éléments suivants :

1. **Le Registre Windows sur l’ordinateur local** : si des paramètres de découverte du service sont configurés dans le Registre, ces paramètres sont essayés en premier. 

    Par défaut, ces paramètres ne sont pas configurés dans le Registre, mais un administrateur peut les configurer pour AD RMS, comme documenté dans une [section suivante](#enabling-client-side-service-discovery-by-using-the-windows-registry). Un administrateur configure généralement ces paramètres pour le service Azure Rights Management lors du [processus de migration](../migrate-from-ad-rms-phase2.md) d’AD RMS vers Azure Information Protection.

2. **Services de domaine Active Directory** : Un ordinateur appartenant à un domaine interroge Active Directory pour un point de connexion de service (SCP). 

    Si un point de connexion de service est inscrit comme documenté dans la [section suivante](#ad-rms-only-enabling-server-side-service-discovery-by-using-active-directory), l’URL du serveur AD RMS est retournée au client RMS qui va l’utiliser.

3. **Le service de découverte Azure Rights Management** : Le client RMS se connecte à **https://discover.aadrm.com**, qui invite l’utilisateur à s’authentifier.

    Quand l’authentification réussit, le nom d’utilisateur (et le domaine) de l’authentification est utilisé pour identifier le locataire Azure Information Protection à utiliser. L’URL d’Azure Information Protection à utiliser pour ce compte d’utilisateur est retournée au client RMS. L’URL a le format suivant : **https://**\<URL_de_votre_locataire\>**/_wmcs/licensing** 

    Par exemple :  5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

    *\<URL_de_votre_locataire\>* a le format suivant: **{GUID}.rms.[Région].aadrm.com**. Vous pouvez trouver cette valeur en identifiant la valeur de **RightsManagementServiceId** quand vous exécutez l’applet de commande [Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) pour Azure RMS.

> [!NOTE]
> Il existe quatre exceptions importantes pour ce flux de découverte de service :
> 
> - Les appareils mobiles sont mieux adaptés pour utiliser un service cloud : par défaut, ils utilisent donc la découverte de service pour le service Azure Rights Management (https://discover.aadrm.com). Pour remplacer cette option par défaut afin que les appareils mobiles utilisent AD RMS au lieu du service Azure Rights Management, spécifiez les enregistrements SRV dans DNS et installez l’extension d’appareils mobiles comme documenté dans [Extension d’appareils mobiles d’Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574\(v=ws.11\).aspx). 
>
> - Quand le service Rights Management est appelé par une étiquette Azure Information Protection, la découverte de service n’est pas réalisée. Au lieu de cela, l’URL est spécifiée directement dans la valeur de l’étiquette qui est configurée dans la stratégie Azure Information Protection. 
>  
> - Quand un utilisateur se connecte à une application Office, le nom d’utilisateur (et le domaine) de l’authentification est utilisé pour identifier le locataire Azure Information Protection à utiliser. Dans ce cas, les paramètres du Registre ne sont pas nécessaires et le point de connexion de service n’est pas vérifié.
> 
> - Quand vous avez configuré la [redirection DNS](../migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection) pour les applications de bureau Démarrer en un clic Office, le client RMS recherche le service Azure Rights Management en ayant l’accès refusé au cluster AD RMS qu’il avait trouvé. Cette action de refus pousse le client à rechercher l’enregistrement SRV, qui redirige le client vers le service Azure Rights Management pour votre locataire. Cet enregistrement SRV laisse aussi Exchange Online déchiffrer les e-mails qui ont été protégés par votre cluster AD RMS. 

### <a name="ad-rms-only-enabling-server-side-service-discovery-by-using-active-directory"></a>AD RMS uniquement : Activation de la découverte du service côté serveur avec Active Directory
Si votre compte dispose de privilèges suffisants (Administrateurs de l’entreprise et administrateur local pour le serveur AD RMS), vous pouvez inscrire automatiquement un point de connexion de service (SCP) lorsque vous installez le serveur de clusters racine AD RMS. S'il existe déjà un SCP dans la forêt, vous devez le supprimer avant de pouvoir en inscrire un nouveau.

Vous pouvez inscrire et supprimer un SCP une fois AD RMS installé à l'aide de la procédure suivante. Avant de commencer, assurez-vous que votre compte dispose des privilèges requis (Administrateurs de l’entreprise et administrateur local pour le serveur AD RMS).

#### <a name="to-enable-ad-rms-service-discovery-by-registering-an-scp-in-active-directory"></a>Pour activer la découverte du service AD RMS en inscrivant un SCP dans Active Directory

1.  Ouvrez la console Services AD RMS (Active Directory Rights Management Services) sur le serveur AD RMS :

    - Pour Windows Server 2012 R2 ou Windows Server 2012, dans Gestionnaire de serveur, sélectionnez **Outils** > **Services AD RMS (Active Directory Rights Management Services)**.

    - Pour Windows Server 2008 R2, sélectionnez **Démarrer** > **Outils d’administration** > **Services AD RMS (Active Directory Rights Management Services)**.

2.  Dans la console AD RMS, cliquez avec le bouton droit sur le cluster AD RMS, puis cliquez sur **Propriétés**.

3.  Cliquez sur l'onglet **SCP** .

4.  Activez la case à cocher **Modifier le point de connexion de service** .

5.  Sélectionnez l'option **Définir le point de connexion de service sur le cluster de certification actuel** , puis cliquez sur **OK**.

### <a name="enabling-client-side-service-discovery-by-using-the-windows-registry"></a>Activation de la découverte du service côté Client à l’aide du Registre Windows
Une alternative à l'utilisation d'un SCP, ou à défaut de SCP, vous pouvez configurer le Registre sur l'ordinateur client afin que le client RMS puisse localiser son serveur AD RMS.

#### <a name="to-enable-client-side-ad-rms-service-discovery-by-using-the-windows-registry"></a>Pour activer la découverte du service AD RMS côté client à l'aide du Registre Windows

1. Ouvrez l'Éditeur du Registre Windows, Regedit.exe :

    - Sur l’ordinateur client, dans la fenêtre Exécuter, tapez **regedit**, puis appuyez sur Entrée pour ouvrir l’Éditeur du Registre.

2. Dans l’Éditeur du Registre, accédez à **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC**.

    > [!NOTE]
    > Si vous exécutez une application 32 bits sur un ordinateur 64 bits,accédez à **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSIPC**

3. Pour créer la sous-clé ServiceLocation, cliquez avec le bouton droit sur **MSIPC**, pointez sur **Nouveau**, cliquez sur **Clé**, puis tapez **ServiceLocation**.

4. Pour créer la sous-clé EnterpriseCertification, cliquez avec le bouton droit sur **ServiceLocation**, pointez sur **Nouveau**, cliquez sur **Clé**, puis tapez **EnterpriseCertification**.

5. Pour définir l’URL de certification d’entreprise, double-cliquez sur la valeur **(Par défaut)** sous la sous-clé **EnterpriseCertification**. Quand la boîte de dialogue **Modifier la chaîne** s’affiche, pour **Données de valeur**, tapez `<http or https>://<AD RMS_cluster_name>/_wmcs/Certification` et cliquez sur **OK**.

6. Pour créer la sous-clé EnterprisePublishing, cliquez avec le bouton droit sur **ServiceLocation**, pointez sur **Nouveau**, cliquez sur **Clé**, puis tapez `EnterprisePublishing`.

7. Pour définir l’URL de publication d’entreprise, double-cliquez sur **(Par défaut)** sous la sous-clé **EnterprisePublishing**. Quand la boîte de dialogue **Modifier la chaîne** s’affiche, pour **Données de valeur**, tapez `<http or https>://<AD RMS_cluster_name>/_wmcs/Licensing` et cliquez sur **OK**.

8.  Fermez l'Éditeur du Registre.

Si le client RMS ne peut pas trouver de SCP en interrogeant Active Directory et si le SCP n’est pas spécifié dans le Registre, les appels de découverte du service pour AD RMS échouent.

### <a name="redirecting-licensing-server-traffic"></a>Redirection du trafic du serveur de licences
Dans certains cas, il se peut que vous deviez rediriger le trafic pendant la découverte du service, par exemple, lorsque deux organisations sont fusionnées, que l'ancien serveur de licences dans une organisation est retiré, et que les clients doivent être redirigés vers un nouveau serveur de licences. Vous pouvez également migrer d'AD RMS vers Azure RMS. Pour activer la redirection de licences, procédez comme suit.

#### <a name="to-enable-rms-licensing-redirection-by-using-the-windows-registry"></a>Pour activer la redirection de licences RMS à l'aide du Registre Windows

1.  Ouvrez l'Éditeur du Registre Windows, Regedit.exe.

2.  Dans l’Éditeur du Registre, accédez à l’un des éléments suivants :

    -   Pour la version 64 bits d'Office sur plateforme x64 : HKLM\SOFTWARE\Microsoft\MSIPC\Servicelocation

    -   Pour la version 32 bits d'Office sur une plateforme x64 : HKLM\SOFTWARE\Wow6432Node\Microsoft\MSIPC\Servicelocation

3.  Créez une sous-clé LicensingRedirection. Pour cela, cliquez avec le bouton droit sur **Servicelocation**, pointez sur **Nouveau**, cliquez sur **Clé**, puis tapez **LicensingRedirection**.

4.  Pour définir la redirection de licences, cliquez avec le bouton droit sur la sous-clé **LicensingRedirection**, sélectionnez **Nouveau**, puis sélectionnez **Valeur de chaîne**.  Pour **Nom**, spécifiez l'URL de licence de serveur précédente, et pour **Valeur** , spécifiez la nouvelle URL de licence de serveur.

    Par exemple, pour rediriger la gestion des licences d'un serveur de Contoso.com vers un serveur de Fabrikam.com, vous pouvez entrer les valeurs suivantes :

    **Nom :** `https://contoso.com/_wmcs/licensing`

    **Valeur :** `https://fabrikam.com/_wmcs/licensing`

    > [!NOTE]
    > Si l’ancien serveur de licences a une URL intranet et extranet spécifiées, un nouveau nom et un mappage de valeur doivent être définis pour ces deux URL sous la clé **LicensingRedirection**.

5.  Répétez l'étape précédente pour tous les serveurs à rediriger.

6.  Fermez l'Éditeur du Registre.

