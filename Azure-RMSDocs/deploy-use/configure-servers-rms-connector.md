---
title: Configuration des serveurs pour le connecteur Azure Rights Management | Azure Information Protection
description: "Informations vous permettant de configurer les serveurs locaux destinés à utiliser le connecteur Azure Rights Management (RMS). Ces procédures couvrent l’étape 5 de Déploiement du connecteur Azure Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/29/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: f262d64a1903eb47bf5f54577fa68df9d43c7f2d


---

# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>Configuration des serveurs pour le connecteur Azure Rights Management

>*S’applique à : Azure Information Protection, Windows Server 2012, Windows Server 2012 R2*


Utilisez les informations suivantes pour vous aider à configurer les serveurs locaux destinés à utiliser le connecteur Azure Rights Management (RMS). Ces procédures couvrent l’étape 5 de [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Avant de commencer, vérifiez que le connecteur RMS est installé et configuré. Assurez-vous également que les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) applicables aux serveurs qui utiliseront le connecteur sont remplies.


## <a name="configuring-servers-to-use-the-rms-connector"></a>Configuration de serveurs afin d'utiliser le connecteur RMS
Une fois que vous avez installé et configuré le connecteur RMS, vous êtes en mesure de configurer les serveurs locaux destinés à se connecter au service Azure Rights Management et à utiliser cette technologie de protection par le biais du connecteur. Cela suppose de configurer les serveurs suivants :

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

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>Utilisation de l'outil de configuration de serveur pour le connecteur Microsoft RMS

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

-   [Configuration d’un serveur Exchange afin d’utiliser le connecteur](#configuring-an-exchange-server-to-use-the-connector)

-   [Configuration d’un serveur SharePoint afin d’utiliser le connecteur](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configuration d’un serveur de fichiers pour l’infrastructure de classification des fichiers afin d’utiliser le connecteur](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> Il est possible que les applications clientes installées en local sur les serveurs configurés pour utiliser le connecteur ne fonctionnent pas avec RMS, car elles tentent d'utiliser le connecteur plutôt que RMS directement, ce qui n'est pas pris en charge.
>
> En outre, si Office 2010 est installé en local sur un serveur Exchange, les fonctionnalités de gestion des droits relatifs à l'information d'une application cliente peuvent fonctionner sur cet ordinateur une fois le serveur configuré pour utiliser le connecteur, ce qui n'est pas non plus pris en charge.
>
> Dans les deux cas, vous devez installer les applications clientes sur des ordinateurs distincts non configurés pour utiliser le connecteur. Elles utiliseront alors RMS correctement.

## <a name="configuring-an-exchange-server-to-use-the-connector"></a>Configuration d'un serveur Exchange afin d'utiliser le connecteur
Les rôles Exchange qui communiquent avec le connecteur RMS sont les suivants :

-   Pour Exchange 2016 et Exchange 2013 : serveur d’accès au client et serveur de boîte aux lettres

-   Pour Exchange 2010 : serveur d'accès au client et serveur de transport Hub

Pour utiliser le connecteur RMS, ces serveurs Exchange doivent exécuter l'une des versions logicielles suivantes :

-   Exchange Server 2016

-   Exchange Server 2013 avec mise à jour cumulative 3 Exchange 2013

-   Exchange Server 2010 avec mise à jour cumulative 6 Exchange 2010 Service Pack 3

Vous avez également besoin sur ces serveurs d’une version 1 du client RMS (également appelé MSDRM) qui prend en charge le mode de chiffrement RMS 2. Tous les systèmes d’exploitation Windows incluent le client MSDRM, mais les versions antérieures du client ne prenaient pas en charge le mode de chiffrement 2. Si vos serveurs Exchange exécutent au moins Windows Server 2012, aucune action supplémentaire n’est nécessaire car le client RMS installé avec ces systèmes d’exploitation prend en charge le mode de chiffrement 2 en mode natif. 

Si vos serveurs Exchange exécutent une version antérieure du système d’exploitation, vérifiez que la version installée du client RMS prend en charge le mode de chiffrement 2. Pour cela, comparez le numéro de version du fichier Windows\System32\Msdrm.dll installé aux numéros de version répertoriés dans les articles suivants de la Base de connaissances. Si le numéro de version du fichier installé est égal ou supérieur aux numéros de version répertoriés, aucune action supplémentaire n’est nécessaire. Si le numéro de version du fichier installé est inférieur, téléchargez le correctif indiqué dans l’article et installez-le.

- Windows Server 2008 : [https://support.microsoft.com/kb/2627272](https://support.microsoft.com/kb/2627272) 

- Windows Server 2008 R2 : [https://support.microsoft.com/kb/2627273](https://support.microsoft.com/kb/2627273)

> [!IMPORTANT]
> Si ces versions ou des versions ultérieures d’Exchange et du client MSDRM ne sont pas installées, vous ne pouvez pas configurer Exchange pour utiliser le connecteur. Vérifiez que ces versions sont installées avant de continuer.

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>Configuration de serveurs Exchange afin d'utiliser le connecteur

1. Vérifiez que les serveurs Exchange sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les rôles serveur Exchange qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur exécutant Exchange 2016 ou Exchange 2013 :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   Modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Activez les fonctionnalités Information Rights Management dans Exchange. Pour plus d’informations, consultez [Procédures de gestion des droits relatifs à l’information](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

    > [!NOTE]
    > Par défaut, après l’exécution de **Set-IRMConfiguration - InternalLicensingEnabled $true**, IRM est activé automatiquement pour Outlook Web App et les appareils mobiles, ainsi que pour les boîtes aux lettres. Toutefois, les administrateurs peuvent désactiver IRM à différents niveaux, par exemple pour un serveur d’accès au client, pour le répertoire virtuel ou la stratégie de boîte aux lettres Outlook Web App, et pour une stratégie de boîte aux lettres d’appareil mobile. Si les utilisateurs ne voient aucune modèle Azure RMS dans Outlook Web App (après avoir attendu une journée) ou sur les appareils mobiles alors qu’ils peuvent les voir dans le client Outlook, vérifiez les paramètres appropriés pour vous assurer qu’IRM n’est pas désactivé. Pour plus d’informations, consultez [Activer ou désactiver la gestion des droits relatifs à l’information (IRM) sur les serveurs d’accès au client](https://technet.microsoft.com/library/dd876938(v=exchg.150).aspx) dans la documentation d’Exchange. 


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>Configuration d'un serveur SharePoint afin d'utiliser le connecteur
Les rôles SharePoint qui communiquent avec le connecteur RMS sont les suivants :

-   serveurs web frontaux SharePoint, y compris ceux hébergeant le serveur d'administration centrale

Pour utiliser le connecteur RMS, ces serveurs SharePoint doivent exécuter l'une des versions logicielles suivantes :

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

Un serveur SharePoint 2016 ou SharePoint 2013 doit également exécuter une version du client MSIPC 2.1 prise en charge avec le connecteur RMS. Pour vérifier que vous disposez d’une version prise en charge, téléchargez la dernière version du client à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Étant donné qu’il existe plusieurs versions du client MSIPC 2.1, assurez-vous que vous avez la version 1.0.2004.0 ou une version ultérieure.
>
> Vous pouvez vérifier la version du client en consultant le numéro de version du fichier MSIPC.dll, situé sous **\Program Files\Active Directory Rights Management Services Client 2.1**. La boîte de dialogue Propriétés affiche le numéro de version du client MSIPC 2.1.

Les serveurs exécutant SharePoint 2010 doivent disposer d’une version du client MSDRM qui inclut la prise en charge du mode de chiffrement RMS 2. La version minimale prise en charge dans Windows Server 2008 est incluse dans le correctif logiciel que vous pouvez télécharger depuis la page [Longueur de clé RSA augmentée à 2 048 bits pour AD RMS dans Windows Server 2008 R2 et Windows Server 2008](http://support.microsoft.com/kb/2627272), et la version minimale pour Windows Server 2008 R2 est téléchargeable à partir de la page [Longueur de clé RSA augmentée à 2 048 bits pour AD RMS dans Windows 7 ou Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Notez que Windows Server 2012 et Windows Server 2012 R2 prennent nativement en charge le mode de chiffrement 2.

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>Configuration de serveurs SharePoint afin d'utiliser le connecteur

1. Vérifiez que les serveurs SharePoint sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les serveurs SharePoint qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement pour configurer un serveur exécutant SharePoint 2016 ou SharePoint 2013 :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   Si vous utilisez SharePoint 2016 ou SharePoint 2013, modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Activez IRM dans SharePoint. Pour plus d’informations, consultez [Configurer la gestion des droits relatifs à l’information (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) dans la bibliothèque SharePoint.

    Dans le cadre de ces instructions, vous devez configurer SharePoint pour utiliser le connecteur en spécifiant l’option **Utiliser ce serveur RMS**, puis entrer l’URL de connecteur d’équilibrage de charge que vous avez configurée. Saisissez le préfixe de protocole (HTTP:// ou HTTPS://) ainsi que le nom du connecteur, tel que défini dans le système DNS pour l'adresse d'équilibrage de charge. Par exemple, si le nom de votre connecteur est https://connector.contoso.com, votre configuration ressemble à l'image suivante :

    ![Configuration de SharePoint Server pour le connecteur RMS](../media/AzRMS_SharePointConnector.png)

    Une fois les services RMS activés pour une ferme SharePoint, vous pouvez les activer pour des bibliothèques grâce à l'option **Services RMS** de la page **Paramètres de la bibliothèque** pour chacune des bibliothèques.


## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>Configuration d'un serveur de fichiers pour l'infrastructure de classification des fichiers afin d'utiliser le connecteur
Pour utiliser le connecteur RMS et l'infrastructure de classification des fichiers dans l'objectif de protéger des documents Office, le serveur de fichiers doit exécuter l'un des systèmes d'exploitation suivants :

-   Windows Server 2012 R2

-   Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>Configuration de serveurs de fichiers afin d'utiliser le connecteur

1.  Vérifiez que les serveurs de fichiers sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2.  Sur les serveurs de fichiers qui sont configurés pour l'infrastructure de classification des fichiers et appelés à communiquer avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   Exécutez l'outil de configuration de serveur pour le connecteur Microsoft RMS. Pour plus d’informations, consultez [Comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) dans cet article.

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur de fichiers exécutant ICF :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Modifiez manuellement le Registre à l’aide des informations contenues dans [Paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres du Registre sur les serveurs. 

3.  Créez des règles de classification et des tâches de gestion de fichiers pour protéger les documents avec le chiffrement RMS, puis spécifiez un modèle RMS pour appliquer automatiquement des stratégies RMS. Pour plus d'informations, voir [Vue d'ensemble du Gestionnaire de ressources du serveur de fichiers](http://technet.microsoft.com/library/hh831701.aspx) dans la bibliothèque de documentation Windows Server.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que le connecteur RMS est installé et configuré, et que vos serveurs sont configurés pour l’utiliser, les administrateurs informatiques et les utilisateurs peuvent protéger et utiliser les e-mails et les documents à l’aide du service Azure Rights Management. Pour faciliter la tâche des utilisateurs, déployez l'application de partage RMS, qui installe un module complémentaire pour Office et ajoute de nouvelles options contextuelles à l'Explorateur de fichiers. Pour plus d’informations, consultez le [guide d’administration de l’application de partage Rights Management](../rms-client/sharing-app-admin-guide.md).

Notez, que si vous configurez des modèles de services que vous souhaitez utiliser avec des règles de transport Exchange ou Windows Server FCI, la configuration de l’étendue doit inclure l’option de compatibilité des applications de manière à ce que la case à cocher **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l'identité de l'utilisateur** soit activée.

Vous pouvez utiliser la [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] à la disposition des utilisateurs et des administrateurs.

Pour surveiller le connecteur RMS, consultez [Surveiller le connecteur Azure Rights Management](monitor-rms-connector.md). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


