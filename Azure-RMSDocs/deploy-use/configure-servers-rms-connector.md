---
# required metadata

title: Configuration des serveurs pour le connecteur Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuration des serveurs pour le connecteur Azure Rights Management

Utilisez les informations suivantes pour vous aider à configurer les serveurs locaux destinés à utiliser le connecteur Azure Rights Management (RMS). Ces procédures couvrent l’étape 5 de [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Avant de commencer, vérifiez que le connecteur RMS est installé et configuré. Assurez-vous également que les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) applicables aux serveurs qui utiliseront le connecteur sont remplies.


## Configuration de serveurs afin d'utiliser le connecteur RMS
Une fois que vous avez installé et configuré le connecteur RMS, vous êtes en mesure de configurer les serveurs locaux destinés à utiliser Rights Management et à se connecter à Azure RMS à l’aide du connecteur. Cela suppose de configurer les serveurs suivants :

-   **Pour Exchange 2016 et Exchange 2013** : serveurs d’accès au client et serveurs de boîte aux lettres

-   **Pour Exchange 2010** : serveurs d’accès au client et serveurs de transport Hub

-   **Pour SharePoint** : serveurs web frontaux SharePoint, notamment ceux hébergeant le serveur d’administration centrale

-   **Pour l’infrastructure de classification des fichiers** : ordinateurs Windows Server sur lesquels le Gestionnaire de ressources de fichiers est installé

Cette configuration nécessite des paramètres de registre. Pour ce faire, deux options de configuration s’offrent à vous : automatique (en utilisant l’outil de configuration de serveur pour le connecteur Microsoft RMS) ou manuelle (en modifiant le Registre).

---

**Configuration automatique à l’aide de l’outil de configuration de serveur pour le connecteur Microsoft RMS :**

- Avantages :

    - Pas d'édition directe du registre. Cette opération est automatisée à l'aide d'un script.

    - Inutile d'exécuter une applet de commande Windows PowerShell pour obtenir l'URL Microsoft RMS.

    - Les prérequis sont automatiquement vérifiés (mais pas corrigés) en cas d'exécution en local.

Inconvénients :

- L'utilisation de cet outil requiert d'établir une connexion à un serveur exécutant déjà le connecteur RMS.

---

**Configuration manuelle nécessitant la modification du Registre :**

- Avantages :

    - Inutile d'établir une connexion à un serveur exécutant le connecteur RMS.

- Inconvénients :

    - Importante charge administrative susceptible d'engendrer des erreurs.

    - L'obtention de l'URL Microsoft RMS requiert d'exécuter une commande Windows PowerShell.

    - Les prérequis doivent être vérifiés manuellement.


---

> [!IMPORTANT]
> Dans les deux cas, vous devez installer manuellement les composants requis et configurer Exchange, SharePoint et l'infrastructure de classification des fichiers pour utiliser Rights Management.

Pour la plupart des organisations, une configuration automatique avec l'outil de configuration de serveur pour le connecteur Microsoft RMS constitue la meilleure option, car elle est plus efficace et fiable que la configuration manuelle.

Après avoir modifié la configuration de ces serveurs, vous devez les redémarrer s'ils exécutent Exchange ou SharePoint et s'ils ont été précédemment configurés pour utiliser les services AD RMS. Il est inutile de redémarrer ces serveurs si vous les configurez pour Rights Management pour la première fois. Vous devez toujours redémarrer le serveur de fichiers qui est configuré pour utiliser l'infrastructure de classification des fichiers après avoir apporté ces modifications à la configuration.

### Utilisation de l'outil de configuration de serveur pour le connecteur Microsoft RMS

1.  Si vous ne l'avez pas encore fait, téléchargez le script de l'outil de configuration de serveur pour le connecteur Microsoft RMS (GenConnectorConfig.ps1) à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Enregistrez le fichier GenConnectorConfig.ps1 sur l'ordinateur que vous utiliserez pour exécuter l'outil. Si vous prévoyez d'exécuter l'outil localement, il doit s'agir du serveur que vous souhaitez configurer afin de communiquer avec le connecteur RMS. Sinon, vous pouvez l'enregistrer sur n'importe quel ordinateur.

3.  Déterminez de quelle façon exécuter l'outil :

    -   **En local**: vous pouvez exécuter l'outil de manière interactive à partir du serveur à configurer pour communiquer avec le connecteur RMS. Cette option est adaptée aux configurations uniques, comme un environnement de test.

    -   **Déploiement logiciel**: vous pouvez exécuter l'outil pour générer des fichiers de registre que vous déployez ensuite sur un ou plusieurs serveurs pertinents à l'aide d'une application de gestion des systèmes prenant en charge le déploiement logiciel, telle que System Center Configuration Manager.

    -   **Stratégie de groupe**: vous pouvez exécuter l'outil pour générer un script, que vous pouvez ensuite transmettre à un administrateur capable de créer des objets de stratégie de groupe pour les serveurs à configurer. Ce script créé un objet de stratégie de groupe pour chaque type de serveur à configurer, auquel l'administrateur peut assigner les serveurs pertinents.

    > [!NOTE]
    > Cet outil configure les serveurs qui sont appelés à communiquer avec le connecteur RMS et qui sont répertoriés au début de cette section. N'exécutez pas cet outil sur les serveurs qui exécutent le connecteur RMS.

4.  Démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur** et utilisez la commande Get-help pour obtenir des instructions d’utilisation de l’outil pour la méthode de configuration choisie :

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Pour exécuter le script, vous devez entrer l’URL du connecteur RMS pour votre organisation. Saisissez le préfixe de protocole (HTTP:// ou HTTPS://) ainsi que le nom du connecteur, tel que défini dans le système DNS pour l'adresse d'équilibrage de charge. Par exemple, https://connector.contoso.com. L'outil utilise ensuite cette URL pour contacter les serveurs qui exécutent le connecteur RMS et obtenir d'autres paramètres servant à créer les configurations requises.

> [!IMPORTANT]
> Quand vous exécutez cet outil, veillez à spécifier le nom du connecteur RMS de votre organisation faisant l'objet d'un équilibrage de charge et non celui d'un serveur unique exécutant le service de connecteur RMS.

Consultez les sections suivantes pour obtenir des informations spécifiques pour chaque type de service :

-   [Configuration d'un serveur Exchange afin d'utiliser le connecteur](#configuring-an-exchange-server-to-use-the-connector)

-   [Configuration d'un serveur SharePoint afin d'utiliser le connecteur](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configuration d'un serveur de fichiers pour l'infrastructure de classification des fichiers afin d'utiliser le connecteur](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> Il est possible que les applications clientes installées en local sur les serveurs configurés pour utiliser le connecteur ne fonctionnent pas avec RMS, car elles tentent d'utiliser le connecteur plutôt que RMS directement, ce qui n'est pas pris en charge.
>
> En outre, si Office 2010 est installé en local sur un serveur Exchange, les fonctionnalités de gestion des droits relatifs à l'information d'une application cliente peuvent fonctionner sur cet ordinateur une fois le serveur configuré pour utiliser le connecteur, ce qui n'est pas non plus pris en charge.
>
> Dans les deux cas, vous devez installer les applications clientes sur des ordinateurs distincts non configurés pour utiliser le connecteur. Elles utiliseront alors RMS correctement.

## Configuration d'un serveur Exchange afin d'utiliser le connecteur
Les rôles Exchange qui communiquent avec le connecteur RMS sont les suivants :

-   Pour Exchange 2016 et Exchange 2013 : serveur d’accès au client et serveur de boîte aux lettres

-   Pour Exchange 2010 : serveur d'accès au client et serveur de transport Hub

Pour utiliser le connecteur RMS, ces serveurs Exchange doivent exécuter l'une des versions logicielles suivantes :

-   Exchange Server 2016

-   Exchange Server 2013 avec mise à jour cumulative 3 Exchange 2013

-   Exchange Server 2010 avec mise à jour cumulative 6 Exchange 2010 Service Pack 3

Vous devez également installer sur ces serveurs une version du client RMS qui prend en charge le mode de chiffrement RMS 2. La version minimale prise en charge par Windows Server 2008 est incluse dans le correctif décrit dans [Longueur de clé RSA augmentée à 2 048 bits pour AD RMS dans Windows Server 2008 R2 et Windows Server 2008](http://support.microsoft.com/kb/2627272). La version minimum pour Windows Server 2008 R2 peut quant à elle être téléchargée via la rubrique [La longueur de clé RSA est augmentée à 2 048 bits pour AD RMS dans Windows 7 ou Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Notez que Windows Server 2012 et Windows Server 2012 R2 prennent nativement en charge le mode de chiffrement 2.

> [!IMPORTANT]
> Si ces versions ou des versions ultérieures d'Exchange et du client RMS ne sont pas installées, vous ne pourrez pas configurer Exchange pour utiliser le connecteur. Vérifiez que ces versions sont installées avant de continuer.

### Configuration de serveurs Exchange afin d'utiliser le connecteur

1. Vérifiez que les serveurs Exchange sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les rôles serveur Exchange qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur exécutant Exchange 2016 ou Exchange 2013 :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   Modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Activez les fonctionnalités Information Rights Management dans Exchange. Pour plus d’informations, consultez [Procédures de gestion des droits relatifs à l’information](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

## Configuration d'un serveur SharePoint afin d'utiliser le connecteur
Les rôles SharePoint qui communiquent avec le connecteur RMS sont les suivants :

-   serveurs web frontaux SharePoint, y compris ceux hébergeant le serveur d'administration centrale

Pour utiliser le connecteur RMS, ces serveurs SharePoint doivent exécuter l'une des versions logicielles suivantes :

-   SharePoint Server 2013

-   SharePoint Server 2010

Un serveur SharePoint 2013 doit également exécuter une version du client MSIPC 2.1 prise en charge avec le connecteur RMS. Pour vérifier que vous disposez d’une version prise en charge, téléchargez la dernière version du client à partir du [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Étant donné qu’il existe plusieurs versions du client MSIPC 2.1, assurez-vous que vous avez la version 1.0.2004.0 ou une version ultérieure.
>
> Vous pouvez vérifier la version du client en consultant le numéro de version du fichier MSIPC.dll, situé sous **\Program Files\Active Directory Rights Management Services Client 2.1**. La boîte de dialogue Propriétés affiche le numéro de version du client MSIPC 2.1.

Ces serveurs exécutant SharePoint 2010 doivent disposer d'une version du client MSDRM qui inclut la prise en charge du mode de chiffrement RMS 2. La version minimale prise en charge dans Windows Server 2008 est incluse dans le correctif logiciel que vous pouvez télécharger depuis la page [Longueur de clé RSA augmentée à 2 048 bits pour AD RMS dans Windows Server 2008 R2 et Windows Server 2008](http://support.microsoft.com/kb/2627272), et la version minimale pour Windows Server 2008 R2 est téléchargeable à partir de la page [Longueur de clé RSA augmentée à 2 048 bits pour AD RMS dans Windows 7 ou Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Notez que Windows Server 2012 et Windows Server 2012 R2 prennent nativement en charge le mode de chiffrement 2.

### Configuration de serveurs SharePoint afin d'utiliser le connecteur

1. Vérifiez que les serveurs SharePoint sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les serveurs SharePoint qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur exécutant SharePoint 2013 :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   Si vous utilisez SharePoint 2013, modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Activez IRM dans SharePoint. Pour plus d’informations, consultez [Configurer la gestion des droits relatifs à l’information (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) dans la bibliothèque SharePoint.

    Dans le cadre de ces instructions, vous devez configurer SharePoint pour utiliser le connecteur en spécifiant l’option **Utiliser ce serveur RMS**, puis entrer l’URL de connecteur d’équilibrage de charge que vous avez configurée. Saisissez le préfixe de protocole (HTTP:// ou HTTPS://) ainsi que le nom du connecteur, tel que défini dans le système DNS pour l'adresse d'équilibrage de charge. Par exemple, si le nom de votre connecteur est https://connector.contoso.com, votre configuration ressemble à l'image suivante :

    ![](../media/AzRMS_SharePointConnector.png)

    Une fois les services RMS activés pour une ferme SharePoint, vous pouvez les activer pour des bibliothèques grâce à l'option **Services RMS** de la page **Paramètres de la bibliothèque** pour chacune des bibliothèques.


## Configuration d'un serveur de fichiers pour l'infrastructure de classification des fichiers afin d'utiliser le connecteur
Pour utiliser le connecteur RMS et l'infrastructure de classification des fichiers dans l'objectif de protéger des documents Office, le serveur de fichiers doit exécuter l'un des systèmes d'exploitation suivants :

-   Windows Server 2012 R2

-   Windows Server 2012

### Configuration de serveurs de fichiers afin d'utiliser le connecteur

1.  Vérifiez que les serveurs de fichiers sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les serveurs de fichiers qui sont configurés pour l'infrastructure de classification des fichiers et appelés à communiquer avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur de fichiers exécutant ICF :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Créez des règles de classification et des tâches de gestion de fichiers pour protéger les documents avec le chiffrement RMS, puis spécifiez un modèle RMS pour appliquer automatiquement des stratégies RMS. Pour plus d'informations, voir [Vue d'ensemble du Gestionnaire de ressources du serveur de fichiers](http://technet.microsoft.com/library/hh831701.aspx) dans la bibliothèque de documentation Windows Server.

## Étapes suivantes
Maintenant que le connecteur RMS est installé et configuré et que vos serveurs sont configurés pour l'utiliser, les administrateurs informatiques et les utilisateurs peuvent protéger et utiliser la messagerie électronique et les documents à l'aide d'Azure RMS. Pour faciliter la tâche des utilisateurs, déployez l'application de partage RMS, qui installe un module complémentaire pour Office et ajoute de nouvelles options contextuelles à l'Explorateur de fichiers. Pour plus d’informations, consultez le [Guide de l’administrateur de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

Vous pouvez également consulter les éléments suivants qui vous aideront à gérer le connecteur RMS et l’utilisation d’Azure RMS par votre organisation :

-   Compteurs de performances intégrés au **connecteur Microsoft Rights Management**

-   [Outil Analyseur RMS](https://www.microsoft.com/en-us/download/details.aspx?id=46437), notamment l’option de connecteur RMS pour vous aider à surveiller l’intégrité du connecteur et à identifier les problèmes de configuration

-   [Journalisation et analyse de l’utilisation d’Azure Rights Management](log-analyze-usage.md)

Utilisez la [Feuille de route pour le déploiement d’Azure Rights Management](../plan-design/deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] à la disposition des utilisateurs et des administrateurs. 


<!--HONumber=Apr16_HO3-->

