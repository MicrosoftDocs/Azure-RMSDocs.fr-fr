---
title: Installer et configurer le connecteur Rights Management - AIP
description: "Il s’agit d’informations destinées à vous aider à installer et à configurer le connecteur Azure Rights Management (RMS). Ces procédures couvrent les étapes 1 à 4 de l’article Déployer le connecteur Azure Rights Management - AIP."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/03/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e4aabc3c571ca132327748935ab3aeafa002db0
ms.sourcegitcommit: e21fb3385de6f0e251167e5dc973e90f0e7f2bcf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Installation et configuration du connecteur Azure Rights Management

>*S’applique à : Azure Information Protection, Office 365*

Utilisez les informations suivantes pour installer et configurer le connecteur Azure Rights Management (RMS). Ces procédures couvrent les étapes 1 à 4 de l’article [Déployer le connecteur Azure Rights Management - AIP](deploy-rms-connector.md).

Avant de commencer, assurez-vous que vous avez consulté et vérifié les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) à ce déploiement.


## <a name="installing-the-rms-connector"></a>Installation du connecteur RMS

1.  Identifiez les ordinateurs qui exécuteront le connecteur RMS (deux au minimum). Ils doivent présenter les caractéristiques minimales listées dans les conditions préalables.

    > [!NOTE]
    > Vous installez un seul connecteur RMS (constitué de plusieurs serveurs pour une haute disponibilité) par locataire (locataire Office 365 ou Azure AD). Contrairement à Active Directory RMS, il est inutile d’installer un connecteur RMS dans chaque forêt.

2.  Téléchargez les fichiers sources du connecteur RMS à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

    Pour installer le connecteur RMS, téléchargez RMSConnectorSetup.exe.

    Informations supplémentaires :

    -   Si vous décidez de configurer le connecteur à partir d’un ordinateur 32 bits, téléchargez également RMSConnectorAdminToolSetup_x86.exe.

    -   Si vous souhaitez utiliser l’outil de configuration de serveur pour le connecteur RMS afin d’automatiser la configuration des paramètres de Registre sur vos serveurs locaux, téléchargez également GenConnectorConfig.ps1.

3.  Sur l’ordinateur sur lequel vous souhaitez installer le connecteur RMS, exécutez **RMSConnectorSetup.exe** avec des privilèges d’administrateur.

4.  Sur la page d’accueil de Microsoft Rights Management Connector Setup, sélectionnez **Install Microsoft Rights Management connector on the computer** (Installer le connecteur Microsoft Rights Management sur l’ordinateur), puis cliquez sur **Suivant**.

5.  Lisez et acceptez les termes du contrat de licence du connecteur RMS, puis cliquez sur **Suivant**.

Pour continuer, entrez un compte et un mot de passe pour configurer le connecteur RMS.

## <a name="entering-credentials"></a>Saisie des informations d’identification
Avant de pouvoir configurer le connecteur RMS, vous devez entrer les informations d’identification d’un compte dispose de privilèges suffisants pour configurer le connecteur RMS. Par exemple, vous pouvez taper **admin@contoso.com**, puis spécifier le mot de passe pour ce compte.

Ce compte ne doit pas recourir à l’authentification multifacteur (MFA), car l’outil d’administration Microsoft Rights Management ne prend pas en charge cette fonctionnalité pour ce compte. 

Le connecteur applique également des restrictions de caractères pour ce mot de passe. Vous ne pouvez pas utiliser de mot de passe comportant les caractères suivants : esperluette (**&**) ; crochet ouvrant (**[**) ; crochet fermant (**]**) ; guillemet droit (**"**) ; et apostrophe (**’**). Si votre mot de passe comporte l’un de ces caractères, l’authentification échoue pour le connecteur RMS et le message d’erreur **Cette combinaison de nom d’utilisateur et mot de passe n’est pas correcte.** s’affiche, même si vous pouvez vous connecter à l’aide de ce compte et du mot de passe pour d’autres scénarios. Si ce scénario s’applique à votre mot de passe, utilisez un autre compte avec un mot de passe qui ne contient aucun de ces caractères spéciaux, ou redéfinissez votre mot de passe de façon à ce qu’il ne comporte aucun de ces caractères spéciaux.

En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), assurez-vous que le compte que vous spécifiez est en mesure de protéger du contenu. Par exemple, si vous avez limité la possibilité de protéger du contenu pour le groupe « Département informatique », le compte spécifié ici doit être un membre de ce groupe. Si ce n’est pas le cas, le message d’erreur : **Échec de la tentative de détection de l’emplacement du service d’administration et de l’organisation., s’affiche. Assurez-vous que le service Microsoft Rights Management est activé pour votre organisation.**

Vous pouvez utiliser un compte possédant l’un des privilèges suivants :

-   **Administrateur global pour votre locataire** : compte qui est administrateur global pour votre locataire Office 365 ou Azure AD.

-   **Administrateur global Azure Rights Management**: compte dans Azure Active Directory auquel a été attribué le rôle d’administrateur global Azure RMS.

-   **Administrateur du connecteur Azure Rights Management**: compte dans Azure Active Directory auquel des droits d’installation et d’administration du connecteur RMS ont été accordés pour votre organisation.

    > [!NOTE]
    > Le rôle d’administrateur global Azure Rights Management et le rôle d’administrateur du connecteur Azure Rights Management sont affectés aux comptes à l’aide de l’applet de commande [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) d’Azure RMS.
    > 
    > Pour exécuter le connecteur RMS avec des privilèges minimum, créez un compte dédié à cet effet, auquel vous attribuez ensuite le rôle d’administrateur du connecteur Azure RMS en procédant comme suit :
    >
    > 1.  Si ce n’est pas déjà fait, téléchargez et installez Windows PowerShell pour Rights Management. Pour plus d’informations, consultez [Installer Windows PowerShell pour Azure Rights Management](install-powershell.md).
    >
    >     Démarrez Windows PowerShell avec la commande **Exécuter en tant qu’administrateur** et connectez-vous au service Azure RMS à l’aide de la commande [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) :
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Puis exécutez la commande [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) en utilisant un seul des paramètres suivants :
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Par exemple, tapez : **Add-AadrmRoleBasedAdministrator - EmailAddress melisa@contoso.com -Role « ConnectorAdministrator »**
    >
    >     Bien que ces commandes attribuent le rôle d’administrateur du connecteur, vous pourriez également utiliser le rôle GlobalAdministrator ici.

Pendant le processus d’installation du connecteur RMS, tous les logiciels requis sont validés et installés, Internet Information Services (IIS) est installé si ce n’est pas déjà fait et le logiciel du connecteur est installé et configuré. En outre, vous préparez la configuration d’Azure RMS en créant les éléments suivants :

-   Une table vide de serveurs autorisés à utiliser le connecteur pour communiquer avec Azure RMS. Vous ajouterez ultérieurement des serveurs à cette table.

-   Un ensemble de jetons de sécurité pour le connecteur, qui autorisent des opérations avec Azure RMS. Ces jetons sont téléchargés à partir d’Azure RMS et installés sur l’ordinateur local dans le Registre. Ils sont protégés à l’aide de l’API de protection des données (DPAPI) et des informations d’identification du compte du système Local.

Dans la page finale de l’Assistant, procédez comme suit, puis cliquez sur **Terminer** :

-   S’il s’agit du premier connecteur installé, ne sélectionnez pas **Launch connector administrator console to authorize servers** (Lancer la console d’administrateur du connecteur pour autoriser les serveurs) pour l’instant. Vous sélectionnerez cette option après avoir installé le deuxième (ou dernier) connecteur RMS. Au lieu de cela, exécutez à nouveau l’Assistant sur au moins un autre ordinateur. Vous devez installer au moins deux connecteurs.

-   Si vous avez installé votre deuxième (ou dernier) connecteur, sélectionnez **Launch connector administrator console to authorize servers** (Lancer la console d’administrateur du connecteur pour autoriser les serveurs).

> [!TIP]
> À ce stade, un test de vérification peut être effectué pour tester si les services web pour le connecteur RMS sont opérationnels :
>
> -   À partir d’un navigateur web, connectez-vous à **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx**, en remplaçant  *&lt;connectoraddress&gt;*  par l’adresse ou le nom du serveur qui a installé le connecteur RMS. En cas de réussite de la connexion, une page **ServerCertificationWebService** s’affiche.

Si vous devez désinstaller le connecteur RMS, exécutez à nouveau l’Assistant et sélectionnez l’option de désinstallation.

Si vous rencontrez des problèmes lors de l’installation, vérifiez le journal d’installation : **%LocalAppData%\Temp\Microsoft Rights Management connector_\<date et time>.log** 

Par exemple, votre journal d’installation peut ressembler à C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352.log

## <a name="authorizing-servers-to-use-the-rms-connector"></a>Autorisation des serveurs à utiliser le connecteur RMS
Une fois le connecteur RMS installé sur au moins deux ordinateurs, vous êtes prêt à autoriser les serveurs et les services voulus à utiliser le connecteur RMS. Par exemple, les serveurs exécutant Exchange Server 2013 ou SharePoint Server 2013.

Pour définir ces serveurs, exécutez l’outil d’administration du connecteur RMS et ajoutez des entrées à la liste des serveurs autorisés. Vous pouvez exécuter cet outil lorsque vous sélectionnez **Launch connector administrator console to authorize servers** (Lancer la console d’administrateur du connecteur pour autoriser les serveurs) à la fin de l’Assistant de configuration du connecteur Microsoft Rights Management, ou vous pouvez l’exécuter séparément à partir de l’Assistant.

Lorsque vous autorisez ces serveurs, tenez compte des considérations suivantes :

- Des privilèges spéciaux sont accordés aux serveurs que vous ajoutez. Tous les comptes que vous spécifiez pour le rôle Exchange Server dans la configuration du connecteur se voient attribuer le [rôle super utilisateur](configure-super-users.md) dans Azure RMS, qui leur donne accès à tout le contenu de ce locataire RMS. La fonctionnalité de super utilisateur est automatiquement activée à ce stade, si nécessaire. Pour éviter le risque de sécurité lié à l’élévation de privilèges, veillez à spécifier uniquement les comptes utilisés par les serveurs Exchange de votre organisation. Tous les serveurs configurés comme serveurs SharePoint ou serveurs de fichiers utilisant l’infrastructure de classification des fichiers se voient accorder des privilèges d’utilisateur standard.

- Vous pouvez ajouter plusieurs serveurs sous forme d’entrée unique en spécifiant un groupe de sécurité ou de distribution Active Directory ou un compte de service utilisé par plusieurs serveurs. Lorsque vous utilisez cette configuration, le groupe de serveurs partage les mêmes certificats RMS et sont tous considérés comme les propriétaires du contenu qu’ils ont protégé. Pour réduire les coûts d’administration, nous vous recommandons d’utiliser cette configuration d’un groupe unique plutôt que des serveurs individuels pour autoriser les serveurs Exchange de votre organisation ou une batterie de serveurs SharePoint.

Sur la page **Serveurs autorisés à utiliser le connecteur**, cliquez sur **Ajouter**.

> [!NOTE]
> La configuration dans Azure RMS qui consiste à autoriser des serveurs équivaut dans ADRMS à configurer manuellement l’application de droits NTFS à ServerCertification.asmx pour les comptes d’ordinateur du service ou du serveur et à accorder manuellement des droits de super utilisateur aux comptes Exchange. L’application de droits NTFS à ServerCertification.asmx n’est pas requise sur le connecteur.


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>Ajouter un serveur à la liste des serveurs autorisés
Sur la page **Autoriser un serveur à utiliser le connecteur**, entrez le nom de l’objet ou cliquez sur Parcourir pour identifier l’objet à autoriser.

Il est important d’autoriser l’objet adéquat. Pour qu’un serveur utilise le connecteur, le compte qui exécute le service local (par exemple, Exchange ou SharePoint) doit être sélectionné pour l’autorisation. Par exemple, si le service s’exécute comme un compte de service configuré, ajoutez le nom de ce compte de service à la liste. Si le service s’exécute en tant que système local, ajoutez le nom de l’objet ordinateur (par exemple, SERVERNAME$). Il est recommandé de créer un groupe qui contient ces comptes, puis de spécifier le groupe au lieu des noms de chaque serveur.

Pour plus d’informations sur les différents rôles de serveur consultez :

-   Pour les serveurs qui exécutent Exchange : vous devez spécifier un groupe de sécurité et vous pouvez utiliser le groupe par défaut (**serveurs Exchange**) qu’Exchange crée et gère parmi tous les serveurs Exchange de la forêt.

-   Pour les serveurs exécutant SharePoint :

    -   Si un serveur SharePoint 2010 est configuré pour s’exécuter en tant que système local (il n’utilise pas un compte de service), créez manuellement un groupe de sécurité dans Active Directory Domain Services et ajoutez l’objet de nom d’ordinateur pour le serveur dans cette configuration à ce groupe.

    -   Si un serveur SharePoint est configuré pour utiliser un compte de service (pratique recommandée pour SharePoint 2010 et seule option pour SharePoint 2016 et SharePoint 2013), procédez comme suit :

        1.  Ajoutez le compte de service qui exécute le service SharePoint Central Administration pour que SharePoint puisse être configuré à partir de sa console d’administrateur.

        2.  Ajoutez le compte qui est configuré pour le pool d’applications SharePoint.

        > [!TIP]
        > Si ces deux comptes sont différents, envisagez de créer un groupe unique contenant les deux comptes pour réduire les coûts d’administration.

-   Pour les serveurs de fichiers qui utilisent l’infrastructure de classification des fichiers, les services associés s’exécutent en tant que compte du système local, vous devez autoriser le compte d’ordinateur pour les serveurs de fichiers (par exemple, SERVERNAME$) ou un groupe qui contient ces comptes d’ordinateur.

Une fois les serveurs ajoutés à la liste, cliquez sur **Fermer**.

Si ce n’est pas déjà fait, vous devez maintenant configurer l’équilibrage de charge pour les serveurs qui ont installé le connecteur RMS et envisager d’utiliser le protocole HTTPS pour les connexions entre ces serveurs et les serveurs que vous venez d’autoriser.

## <a name="configuring-load-balancing-and-high-availability"></a>Configuration de l’équilibrage de charge et de la haute disponibilité
Après avoir installé la deuxième instance ou l’instance finale du connecteur RMS, définissez le nom de serveur d’URL du connecteur et configurez un système d’équilibrage de charge.

Le nom de serveur URL du connecteur peut être n’importe quel nom figurant sous un espace de noms que vous contrôlez. Par exemple, vous pouvez créer une entrée dans votre système DNS pour **rmsconnector.contoso.com** et la configurer de manière à utiliser une adresse IP dans votre système d’équilibrage de charge. Il n’existe aucune exigence particulière pour ce nom, et il ne doit pas être configuré sur les serveurs de connecteur eux-mêmes. Sauf si vos serveurs Exchange et SharePoint sont amenés à communiquer avec le connecteur via Internet, ce nom ne doit pas être résolu sur Internet.

> [!IMPORTANT]
> Nous recommandons de ne pas modifier ce nom après avoir configuré les serveurs Exchange ou SharePoint de manière à utiliser le connecteur, sans quoi vous devriez alors supprimer ces serveurs de toutes les configurations IRM et ensuite les reconfigurer.

Une fois le nom créé dans le système DNS et configuré pour une adresse IP, configurez l’équilibrage de charge pour cette adresse qui dirige le trafic vers les serveurs du connecteur. Pour ce faire, vous pouvez utiliser n’importe quel équilibreur de charge basé sur l’IP, qui inclut la fonctionnalité d’équilibrage de charge réseau (NLB) dans Windows Server. Pour plus d’informations, consultez le [Guide de déploiement de l’équilibrage de charge](http://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Utilisez les paramètres suivants pour configurer le cluster d’équilibrage de charge réseau :

-   Ports : 80 (pour HTTP) ou 443 (pour HTTPS)

    Pour en savoir plus sur le choix du protocole HTTP ou HTTPS, consultez la section suivante.

-   Affinité : Aucune

-   Méthode de distribution : Égale

Ce nom que vous définissez pour le système à équilibrage de charge (pour les serveurs exécutant le service du connecteur RMS) est le nom du connecteur RMS de votre organisation que vous utilisez ultérieurement, lorsque vous configurez les serveurs locaux de manière à utiliser Azure RMS.

## <a name="configuring-the-rms-connector-to-use-https"></a>Configuration du connecteur RMS de manière à utiliser HTTPS
> [!NOTE]
> Cette étape de configuration est facultative mais recommandée pour renforcer la sécurité.

Bien que l’utilisation de SSL ou TLS soit facultative pour le connecteur RMS, nous vous la recommandons pour tous les services sécurisés sensibles basés sur HTTP. Cette configuration permet d’authentifier les serveurs exécutant le connecteur sur vos serveurs Exchange et SharePoint utilisant le connecteur. De plus, toutes les données envoyées depuis ces serveurs au connecteur sont chiffrées.

Pour permettre au connecteur RMS d’utiliser TLS, sur chaque serveur qui exécute le connecteur RMS, installez un certificat d’authentification de serveur qui contient le nom que vous utilisez pour le connecteur. Par exemple, si le nom de votre connecteur RMS défini dans DNS est **rmsconnector.contoso.com**, déployez un certificat d’authentification de serveur qui contient **rmsconnector.contoso.com** dans l’objet du certificat comme nom commun. Ou bien, indiquez **rmsconnector.contoso.com** dans l’autre nom du certificat comme valeur DNS. Il n’est pas nécessaire d’inclure le nom du serveur dans le certificat. Ensuite, dans IIS, reliez ce certificat au site web par défaut.

Si vous utilisez l’option HTTPS, assurez-vous que tous les serveurs qui exécutent le connecteur disposent d’un certificat d’authentification de serveur valide lié à une autorité de certification racine à laquelle vos serveurs Exchange et SharePoint peuvent faire confiance. De plus, si l’autorité de certification (CA) qui a émis les certificats pour les serveurs du connecteur publie une liste de révocation de certificats (CRL), les serveurs Exchange et SharePoint doivent être en mesure de la télécharger.

> [!TIP]
> Vous pouvez utiliser les informations et les ressources suivantes pour vous aider à demander et installer un certificat d’authentification de serveur et lier ce certificat au site web par défaut dans IIS :
>
> -   Si vous utilisez une autorité de certification d’entreprise (CA) et Active Directory Certificate Services (AD CS) pour déployer ces certificats d’authentification de serveur, vous pouvez dupliquer et ensuite utiliser le modèle de certificat de serveur web. Ce modèle de certificat utilise **Fourni dans la demande** comme nom d’objet du certificat, ce qui signifie que vous pouvez fournir le nom de domaine complet du nom du connecteur RMS pour le nom d’objet du certificat ou l’autre nom d’objet lorsque vous demandez le certificat.
> -   Si vous utilisez une autorité de certification autonome ou achetez ce certificat auprès d’une autre société, consultez [Configuring Internet Server Certificates (IIS 7)](http://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) (Configurer des certificats de serveurs IIS 7) dans la bibliothèque de documents relatifs au [Serveur web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) sur TechNet.
> -   Pour configurer IIS de manière à utiliser le certificat, consultez [Add a Binding to a Site (IIS 7)](http://technet.microsoft.com/library/cc731692.aspx) (Ajouter une liaison à un site IIS 7) dans la bibliothèque de documents relatifs au [Serveur web (IIS)](http://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) sur TechNet.

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Configuration du connecteur RMS pour un serveur proxy web
Si les serveurs de votre connecteur sont installés dans un réseau ne disposant pas de connectivité Internet directe et ne nécessitant pas la configuration manuelle d’un serveur proxy web pour l’accès Internet sortant, vous devez configurer le Registre sur ces serveurs pour le connecteur RMS.

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Pour configurer le connecteur RMS de manière à utiliser un serveur proxy web

1.  Sur chaque serveur exécutant le connecteur RMS, ouvrez un éditeur de Registre, tel que Regedit.

2.  Accédez à **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**.

3.  Ajoutez la valeur de chaîne **ProxyAddress** , puis définissez les données de cette valeur sur **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    Par exemple : **http://proxyserver.contoso.com: 8080**

4.  Fermez l’éditeur de Registre, puis redémarrez le serveur ou exécutez une commande IISReset pour redémarrer IIS.

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>Installation de l’outil d’administration de connecteur RMS sur les ordinateurs d’administration
Vous pouvez exécuter l’outil d’administration de connecteur RMS à partir d’un ordinateur sur lequel le connecteur RMS n’est pas installé, si cet ordinateur satisfait aux exigences suivantes :

-   Ordinateur physique ou virtuel exécutant Windows Server 2012 ou Windows Server 2012 R2 (toutes éditions), Windows Server 2008 R2 ou Windows Server 2008 R2 Service Pack 1 (toutes éditions), Windows 8.1, Windows 8 ou Windows 7.

-   Au moins 1 Go de RAM.

-   Au moins 64 Go d’espace disque.

-   Au moins une interface réseau.

-   Accès à Internet via un pare-feu (ou un proxy web).

Pour installer l’outil d’administration de connecteur RMS, exécutez les fichiers suivants :

-   Pour un ordinateur 32 bits : RMSConnectorAdminToolSetup_x86.exe

-   Pour un ordinateur 64 bits : RMSConnectorSetup.exe

Si vous n’avez pas encore téléchargé ces fichiers, vous pouvez le faire à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que le connecteur RMS est installé et configuré, vous êtes en mesure de configurer vos serveurs locaux de manière à l’utiliser. Accédez à [Configuration des serveurs pour le connecteur Azure Rights Management](configure-servers-rms-connector.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
