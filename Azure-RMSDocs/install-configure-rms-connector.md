---
title: Installer et configurer le connecteur Azure Rights Management - AIP
description: Informations vous permettant d’installer et de configurer le connecteur Azure Rights Management (RMS). Ces procédures couvrent les étapes 1 à 4 de Déploiement du connecteur Azure Rights Management.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b92dfe6128a8ba361ebf4d0a047bdee2a124df46
ms.sourcegitcommit: a26d033ccd557839b61736284456370393f3b52a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67156499"
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Installation et configuration du connecteur Azure Rights Management

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Utilisez les informations suivantes pour vous aider à installer et à configurer le connecteur Azure Rights Management (RMS). Ces procédures couvrent les étapes 1 à 4 de [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Avant de commencer, vérifiez les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) pour ce déploiement.


## <a name="installing-the-rms-connector"></a>Installation du connecteur RMS

1.  Identifiez les ordinateurs (au moins deux) pour exécuter le connecteur RMS. Ces ordinateurs doivent respecter les caractéristiques minimales listées dans les conditions préalables.

    > [!NOTE]
    > Vous installez un seul connecteur RMS (constitué de plusieurs serveurs pour une haute disponibilité) par locataire (locataire Office 365 ou Azure AD). puisque, contrairement à Active Directory RMS, il n'est pas nécessaire d'en installer un par forêt.

2.  Téléchargez les fichiers sources du connecteur RMS sur le [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

    Pour installer le connecteur RMS, téléchargez le fichier RMSConnectorSetup.exe.

    De plus :

    -   Si vous souhaitez configurer ultérieurement le connecteur à partir d'un ordinateur 32 bits, téléchargez également le fichier RMSConnectorAdminToolSetup_x86.exe.

    -   Si vous voulez utiliser l'outil de configuration de serveur pour le connecteur RMS, afin d'automatiser la configuration des paramètres de registre sur vos serveurs locaux, téléchargez également le fichier GenConnectorConfig.ps1.

3.  Sur l'ordinateur sur lequel vous souhaitez installer le connecteur RMS, exécutez le fichier **RMSConnectorSetup.exe** avec des privilèges d'administrateur.

4.  Dans la page d'accueil de Microsoft Rights Management Connector Setup, sélectionnez **Installer le connecteur Microsoft Rights Management sur l'ordinateur**, puis cliquez sur **Suivant**.

5.  Lisez et acceptez les termes du contrat de licence du connecteur RMS, puis cliquez sur **Suivant**.

Pour continuer, saisissez un compte et un mot de passe pour configurer le connecteur RMS.

## <a name="entering-credentials"></a>Saisie des informations d'identification
Pour pouvoir configurer le connecteur RMS, vous devez saisir les identifiants d'un compte disposant des droits suffisants. Par exemple, vous pouvez taper <strong>admin@contoso.com</strong>, puis spécifier le mot de passe pour ce compte.

Ce compte ne doit pas requérir l’authentification multifacteur (MFA), car l’outil d’administration Microsoft Rights Management ne prend pas en charge l’authentification multifacteur pour ce compte. 

Le connecteur applique également des restrictions de caractères à ce mot de passe. Vous ne pouvez pas utiliser un mot de passe qui comporte les caractères suivants : Esperluette ( **&** ), crochet gauche ( **[** ), crochet droite ( **]** ), guillemets droits ( **"** ) et apostrophe ( **’** ). Si votre mot de passe contient l’un de ces caractères, l’authentification échoue pour le connecteur RMS, et vous voyez le message d’erreur **Cette combinaison de nom d’utilisateur et mot de passe n’est pas correcte**, même si vous pouvez vous connecter à l’aide de ce compte et de ce mot de passe pour d’autres scénarios. Si ce scénario s’applique à votre mot de passe, utilisez un autre compte dont le mot de passe ne contient aucun de ces caractères spéciaux ou redéfinissez votre mot de passe de façon à ce qu’il n’en contienne pas.

En outre, si vous avez implémenté des [contrôles d’intégration](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), vérifiez que le compte spécifié peut protéger le contenu. Par exemple, si vous avez limité la possibilité de protéger du contenu pour le groupe « Département informatique », le compte que vous spécifiez ici doit être un membre de ce groupe. Sinon, le message d’erreur suivant s’affiche : **Échec de la tentative de détection de l’emplacement du service d’administration et de l’organisation. Vérifiez que le service Microsoft Rights Management est activé pour votre organisation.**

Vous pouvez utiliser un compte possédant l'un des privilèges suivants :

- **Administrateur général pour votre locataire** : Compte d’administrateur général pour votre locataire Office 365 ou votre locataire Azure AD.

- **Administrateur général Azure Rights Management** : Compte dans Azure Active Directory auquel a été affecté le rôle d’administrateur général Azure RMS.

- **Administrateur du connecteur Azure Rights Management** : Un compte dans Azure Active Directory qui ont été accordés des droits à installer et administrer le connecteur RMS pour votre organisation.

  > [!NOTE]
  > Le rôle d’administrateur général Azure Rights Management et le rôle d’administrateur du connecteur Azure Rights Management sont affectés aux comptes à l’aide de l’applet de commande Azure RMS [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).
  > 
  > Pour exécuter le connecteur RMS avec des privilèges minimum, créez un compte dédié à cet effet, auquel vous affectez ensuite le rôle d’administrateur du connecteur Azure RMS en procédant comme suit :
  > 
  > 1. Si ce n’est déjà fait, téléchargez et installez Windows PowerShell pour Rights Management. Pour plus d’informations, voir [Installation du module PowerShell AADMR](install-powershell.md).
  > 
  >    Démarrez Windows PowerShell avec la commande **Exécuter en tant qu'administrateur**, et connectez-vous au service Azure RMS à l'aide de la commande [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice):
  > 
  >    ```
  >    Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
  >    ```
  > 2. Puis exécutez la commande [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator), en utilisant un seul des paramètres suivants :
  > 
  >    ```
  >    Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
  >    ```
  > 
  >    ```
  >    Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
  >    ```
  > 
  >    ```
  >    Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
  >    ```
  >    Par exemple, entrez : **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
  > 
  >    Même si ces commandes affectent le rôle d’administrateur du connecteur, vous pouvez également utiliser le rôle GlobalAdministrator ici aussi.

Au cours du processus d'installation du connecteur RMS, tous les logiciels requis sont validés et installés, les services Internet (IIS) sont installés s'ils ne l'étaient pas déjà et le logiciel du connecteur est installé et configuré. De plus, Azure RMS est préparé pour la configuration via la création des éléments suivants :

-   Table vide des pour les serveurs autorisés à utiliser le connecteur pour communiquer avec Azure RMS. Vous ajoutez des serveurs à cette table par la suite.

-   Ensemble de jetons de sécurité pour le connecteur, qui autorisent des opérations avec Azure RMS. Ces jetons sont téléchargés à partir d'Azure RMS et installés dans le Registre de l'ordinateur local. Ils sont protégés à l'aide de l'API de protection de données (DPAPI) et des informations d'identification du compte système Local.

Exécutez les actions suivantes sur la dernière page de l'Assistant, puis cliquez sur **Terminer** :

-   S'il s'agit du premier connecteur installé, ne sélectionnez pas l'option **Lancer la console Administrateur du connecteur pour autoriser des serveurs** à ce stade. Vous sélectionnerez cette option une fois que vous aurez installé la deuxième (ou dernière) instance du connecteur RMS. ‎À la place, exécutez à nouveau l'Assistant sur au moins un autre ordinateur. Notez que vous devez procéder à deux installations minimum.

-   S'il s'agit de la deuxième (ou dernière) instance du connecteur, sélectionnez **Lancer la console Administrateur du connecteur pour autoriser des serveurs**.

> [!TIP]
> À ce stade, vous pouvez réaliser un test de vérification pour vous assurer que les services Web du connecteur RMS sont opérationnels :
>
> -   Dans un navigateur web, accédez à l’URL **http://&lt;adresse_connecteur&gt;/_wmcs/certification/servercertification.asmx**, en remplaçant *&lt;adresse_connecteur&gt;* par l’adresse ou le nom du serveur sur lequel le connecteur RMS est installé. Si la connexion fonctionne, la page **ServerCertificationWebService** apparaît.

Si vous avez besoin de désinstaller le connecteur RMS, exécutez à nouveau l'Assistant et sélectionnez l'option Désinstaller.

Si vous rencontrez des problèmes lors de l’installation, vérifiez le journal d’installation : **%LocalAppData%\Temp\Microsoft Rights Management connector_\<date et heure>.log** 

Par exemple, le nom de votre journal d’installation peut être similaire à C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352.log

## <a name="authorizing-servers-to-use-the-rms-connector"></a>Définition des serveurs autorisés à utiliser le connecteur RMS
Dès lors que le connecteur RMS est installé sur au moins deux ordinateurs, vous êtes en mesure d'autoriser les serveurs et les services souhaités à utiliser le connecteur RMS. Par exemple, les serveurs exécutant Exchange Server 2013 ou SharePoint Server 2013.

Pour définir ces serveurs, exécutez l'outil d'administration du connecteur RMS, puis ajoutez des entrées à la liste des serveurs autorisés. Vous pouvez exécuter cet outil lors de la sélection de l'option **Lancer la console Administrateur du connecteur pour autoriser des serveurs** à la fin de l'Assistant de configuration du connecteur Microsoft Rights Management, mais vous pouvez également l'exécuter séparément de l'Assistant.

Prenez en compte les considérations suivantes lors de la définition des serveurs :

- Les serveurs ajoutés reçoivent des privilèges particuliers. Tous les comptes que vous spécifiez pour le rôle serveur Exchange dans la configuration du connecteur reçoivent le [rôle super utilisateur](configure-super-users.md) dans Azure RMS, ce qui leur donne accès à tout le contenu de ce locataire RMS. La fonctionnalité de super utilisateur est automatiquement activée à ce stade, si nécessaire. Pour éviter le risque de sécurité lié à l'élévation de privilèges, veillez à spécifier uniquement les comptes utilisés par les serveurs Exchange de votre organisation. Tous les serveurs configurés comme serveurs SharePoint ou serveurs de fichiers utilisant l'infrastructure de classification des fichiers (ICF) reçoivent des privilèges d’utilisateur standard.

- Vous pouvez ajouter plusieurs serveurs sous la forme d'une entrée unique en spécifiant un groupe de distribution ou de sécurité Active Directory ou un compte de service utilisé par plus d'un serveur. Quand vous utilisez cette configuration, le groupe de serveurs partage les mêmes certificats RMS et ils sont tous considérés comme étant propriétaires de l’ensemble du contenu protégé par un des serveurs. Pour minimiser la charge administrative, nous vous conseillons d'adopter cette configuration de groupe unique plutôt que de serveurs multiples pour autoriser les serveurs Exchange ou la batterie de serveurs SharePoint de votre organisation.

Sur la page **Serveurs autorisés à utiliser le connecteur**, cliquez sur **Ajouter**.

> [!NOTE]
> Autoriser des serveurs dans Azure RMS équivaut à la configuration AD RMS qui consiste à appliquer manuellement des droits NTFS à ServerCertification.asmx pour les comptes d’ordinateur de service ou de serveur et à accorder manuellement des droits de super utilisateur aux comptes Exchange. L’application de droits NTFS à ServerCertification.asmx n’est pas nécessaire sur le connecteur.


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>Ajout d'un serveur à la liste des serveurs autorisés
Sur la page **Autoriser un serveur à utiliser le connecteur**, saisissez le nom de l'objet ou recherchez l'objet à autoriser.

Il est important d'autoriser l'objet adéquat. Pour qu'un serveur utilise le connecteur, le compte qui exécute le service local (par exemple, Exchange ou SharePoint) doit être sélectionné pour autorisation. Par exemple, si le service est exécuté en tant que compte de service configuré, ajoutez le nom de ce compte de service à la liste. Si le service est exécuté en tant que système local, ajoutez le nom de l'objet d'ordinateur (par exemple, NOMSERVEUR$). Il est préférable de créer un groupe contenant ces comptes afin de spécifier ce groupe plutôt que des noms de serveurs individuels.

Voici quelques informations relatives aux différents rôles de serveur :

-   Pour les serveurs qui exécutent Exchange : Vous devez spécifier un groupe de sécurité. Notez que vous pouvez utiliser le groupe par défaut (**Serveurs Exchange**) créé et mis à jour automatiquement par Exchange, regroupant tous les serveurs Exchange de la forêt.

-   Pour les serveurs exécutant SharePoint :

    -   Si un serveur SharePoint 2010 est configuré pour s'exécuter en tant que système Local (il n'utilise pas de compte de service), créez manuellement un groupe de sécurité dans les services de domaine Active Directory, puis ajoutez l'objet de nom d'ordinateur pour le serveur dans cette configuration à ce groupe.

    -   Si un serveur SharePoint est configuré pour utiliser un compte de service (pratique recommandée pour SharePoint 2010 et seule option pour SharePoint 2016 et SharePoint 2013), procédez comme suit :

        1.  Ajoutez le compte de service exécutant le service Administration centrale de SharePoint pour que SharePoint soit configuré à partir de sa console Administrateur.

        2.  Ajoutez le compte configuré pour le pool d'applications SharePoint.

        > [!TIP]
        > S'il s'agit de deux comptes différents, pensez à créer un groupe unique les réunissant, afin de minimiser la charge administrative.

-   Pour les serveurs de fichiers utilisant l'infrastructure de classification des fichiers, les services associés s'exécutent en tant que compte de système local. Vous devez donc autoriser les comptes d'ordinateur des serveurs de fichiers (par exemple, NOMSERVEUR$) ou un groupe réunissant ces comptes d'ordinateur.

Une fois que tous les serveurs sont ajoutés, cliquez sur **Fermer**.

Si vous ne l'avez pas déjà fait, vous devez à présent configurer l'équilibrage de charge pour les serveurs disposant du connecteur RMS installé, et déterminer si vous souhaitez utiliser le protocole HTTPS pour les connexions entre ces serveurs et les serveurs que vous venez d'autoriser.

## <a name="configuring-load-balancing-and-high-availability"></a>Configuration de l'équilibrage de charge et de la haute disponibilité
Une fois que vous avez installé l’instance de deuxième ou final du connecteur RMS, définir un nom de serveur de connecteur URL et configurer un système d’équilibrage de charge.

Le nom de serveur URL du connecteur peut être n'importe quel nom défini dans un espace de noms que vous contrôlez. Par exemple, vous pouvez créer une entrée dans votre système DNS pour **rmsconnector.contoso.com** et configurer cette entrée pour utiliser une adresse IP dans votre système d’équilibrage de charge. Il n'y a pas de conditions requises particulières pour ce nom, et il n'est pas nécessaire de le configurer sur les serveurs de connecteur eux-mêmes. Il n'est pas non plus nécessaire que ce nom apparaisse sur Internet, sauf si vos serveurs Exchange et SharePoint sont amenés à communiquer avec le connecteur via Internet.

> [!IMPORTANT]
> Nous vous conseillons de ne pas modifier ce nom une fois les serveurs Exchange ou SharePoint configurés pour utiliser le connecteur, car vous devriez alors supprimer ces serveurs de l'ensemble des configurations de gestion des droits relatifs à l'information pour ensuite les reconfigurer.

Une fois le nom créé dans le système DNS et associé à une adresse IP, configurez l'équilibrage de charge pour cette adresse, afin de rediriger le trafic vers les serveurs du connecteur. Vous pouvez utiliser n'importe quel programme d'équilibrage de charge basé sur une adresse IP, notamment la fonctionnalité Équilibrage de la charge réseau (NLB) de Windows Server. Pour plus d’informations, consultez le [guide de déploiement de l’équilibrage de charge](https://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Utilisez les paramètres suivants pour configurer le cluster NLB :

-   Ports : 80 (pour HTTP) ou 443 (HTTPS)

    Pour plus d'informations sur le choix du protocole HTTP ou du protocole HTTPS, consultez la section suivante.

-   Affinité : Aucune

-   Méthode de distribution : égal

Ce nom que vous définissez pour le système d'équilibrage de charge (pour les serveurs exécutant le service de connecteur RMS) est le nom du connecteur RMS de votre organisation que vous utilisez par la suite afin de configurer les serveurs locaux pour qu’ils utilisent Azure RMS.

## <a name="configuring-the-rms-connector-to-use-https"></a>Configuration du connecteur RMS pour le protocole HTTPS
> [!NOTE]
> Cette étape de configuration est facultative, mais recommandée pour plus de sécurité.

Bien que l'utilisation de TLS ou de SSL soit facultative pour le connecteur RMS, nous la conseillons pour tout service lié à la sécurité basé sur le protocole HTTP. Cette configuration authentifie les serveurs exécutant le connecteur sur vos serveurs Exchange et SharePoint qui utilisent le connecteur. De plus, toutes les données envoyées depuis ces serveurs au connecteur sont chiffrées.

Pour que le connecteur RMS utilise TLS, installez un certificat d'authentification de serveur contenant le nom utilisé pour le connecteur RMS sur chacun des serveurs qui l'exécutent. Par exemple, si le nom de connecteur RMS défini dans votre système DNS est **rmsconnector.contoso.com**, déployez un certificat d’authentification de serveur incluant le nom commun **rmsconnector.contoso.com** dans le sujet du certificat. Vous pouvez aussi spécifier **rmsconnector.contoso.com** dans le nom alternatif du certificat comme valeur DNS. Le certificat n'a pas besoin d'inclure le nom du serveur. Dans IIS, reliez ensuite ce certificat au site Web par défaut.

Si vous utilisez l'option HTTPS, assurez-vous que tous les serveurs exécutant le connecteur disposent d'un certificat d'authentification de serveur valide lié à l'autorité de certification racine reconnue par vos serveurs Exchange et SharePoint. Par ailleurs, si l'autorité de certification qui a établi les certificats pour les serveurs du connecteur publie une liste de révocation de certificats, les serveurs Exchange et SharePoint doivent pouvoir la télécharger.

> [!TIP]
> Vous pouvez utiliser les informations et ressources suivantes pour vous aider à demander et à installer un certificat d'authentification de serveur, puis à relier ce certificat au site Web par défaut dans IIS :
>
> - Si vous utilisez les services de certificat Active Directory (AD CS) et une autorité de certification d'entreprise pour déployer ces certificats d'authentification de serveur, vous pouvez dupliquer puis utiliser le modèle de certificat de serveur Web. Ce modèle utilise l'option **Fourni dans la demande** pour le nom du sujet du certificat, ce qui signifie que vous pouvez fournir le nom de domaine complet du nom du connecteur RMS pour le nom du sujet du certificat ou le nom alternatif du sujet pour votre demande de certificat.
> -   Si vous utilisez une autorité de certification autonome ou si vous achetez ce certificat auprès d’une autre société, consultez la rubrique [Configuration des certificats de serveur Internet (IIS 7)](https://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) dans la bibliothèque de documentation [Serveur web (IIS)](https://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) sur TechNet.
> - Pour configurer IIS afin d’utiliser le certificat, consultez [Ajouter une liaison à un site (IIS 7)](https://technet.microsoft.com/library/cc731692.aspx) dans la bibliothèque de documentation [Serveur web (IIS)](https://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) sur TechNet.

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Configuration du connecteur RMS pour un serveur proxy web
Si vos serveurs de connecteur sont installés au sein d'un réseau qui ne possède pas de connectivité Internet directe et qui nécessite la configuration manuelle d'un serveur proxy web pour obtenir un accès Internet sortant, vous devez configurer le registre de ces serveurs pour le connecteur RMS.

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Configuration du connecteur RMS afin d'utiliser un serveur proxy web

1.  Sur chaque serveur exécutant le connecteur RMS, ouvrez un éditeur de registre, tel que Regedit.

2.  Accédez à l’emplacement **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**.

3.  Ajoutez la valeur de chaîne **Adresse proxy**, puis configurez les données de cette valeur sur **http://&lt;MonDomainProxyOuAdresseIP&gt;:&lt;MonPortProxy&gt;**

    Par exemple : **http://proxyserver.contoso.com:8080**

4.  Fermez l'éditeur de registre, puis redémarrez le serveur ou exécutez une commande IISReset pour redémarrer IIS.

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>Installation de l'outil d'administration du connecteur RMS sur les ordinateurs d'administration
Vous pouvez exécuter l'outil d'administration du connecteur RMS à partir d'un ordinateur sur lequel le connecteur RMS n'est pas installé, dans la mesure où cet ordinateur est conforme à la configuration suivante :

-   Un ordinateur physique ou virtuel exécutant Windows Server 2012 ou Windows Server 2012 R2 (toutes éditions), Windows Server 2008 R2 ou Windows Server 2008 R2 Service Pack 1 (toutes éditions), Windows 8.1, Windows 8 ou Windows 7.

-   1 Go de RAM minimum.

-   64 Go d'espace disque minimum.

-   Au moins une interface réseau.

-   Un accès à Internet via un pare-feu (ou un proxy web).

Exécutez les fichiers suivants pour installer l'outil d'administration du connecteur RMS :

-   Pour un ordinateur 32 bits : RMSConnectorAdminToolSetup_x86.exe

-   Pour un ordinateur 64 bits : RMSConnectorSetup.exe

Si ce n'est déjà fait, vous pouvez télécharger ces fichiers à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).


## <a name="next-steps"></a>Étapes suivantes
Maintenant que le connecteur RMS est installé et configuré, vous êtes prêt à configurer vos serveurs locaux pour qu’ils l’utilisent. Accédez à [Configuration des serveurs pour le connecteur Azure Rights Management](configure-servers-rms-connector.md).

