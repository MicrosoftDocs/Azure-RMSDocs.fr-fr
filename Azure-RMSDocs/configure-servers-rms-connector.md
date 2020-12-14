---
title: Configurer des serveurs pour le connecteur Azure Rights Management - AIP
description: Informations vous permettant de configurer les serveurs locaux destinés à utiliser le connecteur Azure Rights Management (RMS). Ces procédures couvrent l’étape 5 de Déploiement du connecteur Azure Rights Management.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/10/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4f1dd3d2c832cebfe8cb8a994570d81e7544d8cf
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383004"
---
# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>Configuration des serveurs pour le connecteur Azure Rights Management

>***S’applique à**: [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Utilisez les informations suivantes pour vous aider à configurer les serveurs locaux destinés à utiliser le connecteur Azure Rights Management (RMS). Ces procédures couvrent l’étape 5 du [déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

**Conditions préalables**: avant de commencer, assurez-vous que vous disposez des éléments suivants :
    - Le connecteur RMS est installé et configuré
    - Vérifiez les [conditions préalables](deploy-rms-connector.md#prerequisites-for-the-rms-connector) applicables aux serveurs qui utiliseront le connecteur.

## <a name="configuring-servers-to-use-the-rms-connector"></a>Configuration de serveurs afin d'utiliser le connecteur RMS
Une fois que vous avez installé et configuré le connecteur RMS, vous êtes prêt à configurer les serveurs locaux qui se connecteront au service Azure Rights Management et à utiliser cette technologie de protection à l’aide du connecteur. 

Cela suppose de configurer les serveurs suivants :

|Environnement  |Serveurs à configurer  |
|---------|---------|
|**Exchange 2016 et Exchange 2013**     |  Serveurs d'accès au client et serveurs de boîte aux lettres       |
|**Exchange 2019**     |   serveurs d'accès au client et serveurs de transport Hub      |
|**SharePoint**     |    serveurs web frontaux SharePoint, y compris ceux hébergeant le serveur d'administration centrale     |
|**Infrastructure de classification des fichiers**     |   ordinateurs Windows Server sur lesquels le Gestionnaire de ressources de fichiers est installé      |
| | |

Cette configuration nécessite des paramètres de Registre, avec les options suivantes :

- [Modifier les paramètres du Registre automatiquement](#edit-registry-settings-automatically---advantages-and-disadvantages)
- [Modifier manuellement les paramètres du Registre](#edit-registry-settings-manually---advantages-and-disadvantages)

> [!IMPORTANT]
> Dans les deux cas, vous devez installer manuellement les composants requis et configurer Exchange, SharePoint et l'infrastructure de classification des fichiers pour utiliser Rights Management.

> [!NOTE]
> Pour la plupart des organisations, une configuration automatique avec l'outil de configuration de serveur pour le connecteur Microsoft RMS constitue la meilleure option, car elle est plus efficace et fiable que la configuration manuelle.
> 

Après avoir apporté les modifications de configuration sur ces serveurs, vous devez les redémarrer s’ils exécutent Exchange ou SharePoint et ont été précédemment configurés pour utiliser AD RMS. Il est inutile de redémarrer ces serveurs si vous les configurez pour Rights Management pour la première fois. 

Vous devez toujours redémarrer le serveur de fichiers qui est configuré pour utiliser l'infrastructure de classification des fichiers après avoir apporté ces modifications à la configuration.
### <a name="edit-registry-settings-automatically---advantages-and-disadvantages"></a>Modifier les paramètres du Registre automatiquement-avantages et inconvénients

Modifiez vos paramètres de Registre automatiquement à l’aide de l’outil de configuration de serveur pour le connecteur Microsoft RMS.

Les **avantages sont** les suivants :

- Pas d'édition directe du registre. Cette opération est automatisée à l'aide d'un script.

- Inutile d'exécuter une applet de commande Windows PowerShell pour obtenir l'URL Microsoft RMS.

- Les prérequis sont automatiquement vérifiés (mais pas corrigés) en cas d'exécution en local.

Les **inconvénients sont** les suivants : quand vous exécutez l’outil, vous devez établir une connexion à un serveur qui exécute déjà le connecteur RMS.

Pour plus d’informations, consultez [comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).
### <a name="edit-registry-settings-manually---advantages-and-disadvantages"></a>Modifier manuellement les paramètres du Registre-avantages et inconvénients

Les **avantages sont** les suivants : aucune connexion à un serveur exécutant le connecteur RMS n’est requise.

Les **inconvénients sont** les suivants :

- Importante charge administrative susceptible d'engendrer des erreurs.

- L'obtention de l'URL Microsoft RMS requiert d'exécuter une commande Windows PowerShell.

- Les prérequis doivent être vérifiés manuellement.

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>Utilisation de l'outil de configuration de serveur pour le connecteur Microsoft RMS

1.  Si vous n’avez pas encore téléchargé le script de l’outil de configuration de serveur pour le connecteur Microsoft RMS **(GenConnectorConfig.ps1)**, téléchargez-le à partir du [Centre de téléchargement Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

2.  Enregistrez le fichier **GenConnectorConfig.ps1** sur l’ordinateur sur lequel vous allez exécuter l’outil. 

    Si vous prévoyez d'exécuter l'outil localement, il doit s'agir du serveur que vous souhaitez configurer afin de communiquer avec le connecteur RMS. Sinon, vous pouvez l'enregistrer sur n'importe quel ordinateur.

3.  Déterminez de quelle façon exécuter l'outil :
    
    |Méthode  |Description  |
    |---------|---------|
    |**Localement**     |  Exécutez l’outil de manière interactive, à partir du serveur à configurer pour communiquer avec le connecteur RMS. <br><br>**Conseil**: cette option est utile pour une configuration unique, telle qu’un environnement de test.       |
    |**Déploiement logiciel**     |  Exécutez l’outil pour générer des fichiers de registre que vous déployez ensuite sur un ou plusieurs serveurs appropriés. <br><br>Déployez les fichiers du Registre à l’aide d’une application de gestion de systèmes qui prend en charge le déploiement de logiciels, comme System Center Configuration Manager.       |
    |**Stratégie de groupe**     | Exécutez l’outil pour générer un script que vous donnez à un administrateur qui peut créer des objets stratégie de groupe pour les serveurs à configurer. <br><br>Ce script créé un objet de stratégie de groupe pour chaque type de serveur à configurer, auquel l'administrateur peut assigner les serveurs pertinents.        |
    | | |

    > [!NOTE]
    > Cet outil configure les serveurs qui sont appelés à communiquer avec le connecteur RMS et qui sont répertoriés au début de cette section. N'exécutez pas cet outil sur les serveurs qui exécutent le connecteur RMS.

4.  Démarrez Windows PowerShell avec l’option **exécuter en tant qu’administrateur** , puis utilisez la commande **obtenir-aide** pour lire les instructions relatives à l’utilisation de l’outil pour la méthode de configuration choisie :

    ```PowerShell
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Pour exécuter le script, vous devez entrer l’URL du connecteur RMS pour votre organisation. 

Saisissez le préfixe de protocole (HTTP:// ou HTTPS://) ainsi que le nom du connecteur, tel que défini dans le système DNS pour l'adresse d'équilibrage de charge. Par exemple, `https:\//connector.contoso.com`. 

L'outil utilise ensuite cette URL pour contacter les serveurs qui exécutent le connecteur RMS et obtenir d'autres paramètres servant à créer les configurations requises.

> [!IMPORTANT]
> Quand vous exécutez cet outil, veillez à spécifier le nom du connecteur RMS de votre organisation faisant l'objet d'un équilibrage de charge et non celui d'un serveur unique exécutant le service de connecteur RMS.

Consultez les sections suivantes pour obtenir des informations spécifiques pour chaque type de service :

-   [Configuration d’un serveur Exchange pour utiliser le connecteur](#configuring-an-exchange-server-to-use-the-connector)

-   [Configuration d’un serveur SharePoint afin d’utiliser le connecteur](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configuration d’un serveur de fichiers pour l’infrastructure de classification des fichiers afin d’utiliser le connecteur](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

**Quand installer des applications clientes sur des ordinateurs distincts qui ne sont pas configurés pour utiliser le connecteur**

Il est possible que les applications clientes installées en local sur les serveurs configurés pour utiliser le connecteur ne fonctionnent pas avec RMS, car elles tentent d'utiliser le connecteur plutôt que RMS directement, ce qui n'est pas pris en charge.

En outre, si Office 2010 est installé localement sur un serveur Exchange, les fonctionnalités IRM de l’application cliente peuvent fonctionner à partir de cet ordinateur une fois que le serveur est configuré pour utiliser le connecteur, mais cela n’est pas pris en charge.

Dans les deux cas, vous devez installer les applications clientes sur des ordinateurs distincts non configurés pour utiliser le connecteur. Elles utiliseront alors RMS correctement.

## <a name="configuring-an-exchange-server-to-use-the-connector"></a>Configuration d'un serveur Exchange afin d'utiliser le connecteur
Les rôles Exchange qui communiquent avec le connecteur RMS sont les suivants :

-   Pour Exchange 2016 et Exchange 2013 : serveur d’accès au client et serveur de boîte aux lettres

-   Pour Exchange 2019 : serveur d’accès au client et serveur de transport Hub

Pour utiliser le connecteur RMS, ces serveurs Exchange doivent exécuter l'une des versions logicielles suivantes :

-   Exchange Server 2016

-   Exchange Server 2013 avec mise à jour cumulative 3 Exchange 2013

-   Exchange Server 2019

Vous avez également besoin sur ces serveurs d’une version 1 du client RMS (également appelé MSDRM) qui prend en charge le mode de chiffrement RMS 2. Tous les systèmes d’exploitation Windows incluent le client MSDRM, mais les versions antérieures du client ne prenaient pas en charge le mode de chiffrement 2. Si vos serveurs Exchange exécutent au moins Windows Server 2012, aucune action supplémentaire n’est nécessaire car le client RMS installé avec ces systèmes d’exploitation prend en charge le mode de chiffrement 2 en mode natif. 


> [!IMPORTANT]
> Si ces versions ou des versions ultérieures d’Exchange et du client MSDRM ne sont pas installées, vous ne pouvez pas configurer Exchange pour utiliser le connecteur. Vérifiez que ces versions sont installées avant de continuer.

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>Configuration de serveurs Exchange afin d'utiliser le connecteur

1. Vérifiez que les serveurs Exchange sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Cette configuration est nécessaire pour qu’Exchange puisse utiliser le connecteur RMS.

2. Sur les rôles serveur Exchange qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

   -   **Exécutez l’outil de configuration de serveur pour le connecteur Microsoft RMS**. 

       Pour plus d’informations, consultez [comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur exécutant Exchange 2016 ou Exchange 2013 :

       ```PowerShell
       .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
       ```

    
   -   **Effectuez des modifications manuelles du Registre**. Pour plus d’informations, consultez [paramètres du Registre pour le connecteur RMS](rms-connector-registry-settings.md). 

3. Activez les fonctionnalités IRM pour Exchange à l’aide de l’applet de commande Exchange PowerShell [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration). Définissez `InternalLicensingEnabled $true` et `ClientAccessServerEnabled $true`.


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>Configuration d'un serveur SharePoint afin d'utiliser le connecteur

Les serveurs frontaux SharePoint, y compris ceux hébergeant le serveur d’administration centrale, communiquent avec le connecteur RMS.

Pour utiliser le connecteur RMS, ces serveurs SharePoint doivent exécuter l'une des versions logicielles suivantes :

-   SharePoint Server 2019

-   Serveur SharePoint 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

Un serveur exécutant SharePoint 2019, 2016 ou SharePoint 2013 doit également exécuter une version du client MSIPC 2,1 prise en charge avec le connecteur RMS. 

Pour vous assurer que vous disposez d’une version prise en charge, téléchargez la dernière version du client à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Étant donné qu’il existe plusieurs versions du client MSIPC 2.1, assurez-vous que vous avez la version 1.0.2004.0 ou une version ultérieure.
>
> Vous pouvez vérifier la version du client en consultant le numéro de version du fichier MSIPC.dll, situé sous **\Program Files\Active Directory Rights Management Services Client 2.1**. La boîte de dialogue Propriétés affiche le numéro de version du client MSIPC 2.1.

Les serveurs exécutant SharePoint 2010 doivent disposer d’une version du client MSDRM qui inclut la prise en charge du mode de chiffrement RMS 2. Notez que Windows Server 2012 et Windows Server 2012 R2 prennent nativement en charge le mode de chiffrement 2.

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>Configuration de serveurs SharePoint afin d'utiliser le connecteur

1. Vérifiez que les serveurs SharePoint sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Cette configuration est exigée pour que vos serveurs SharePoint puissent utiliser le connecteur RMS.

2.  Sur les serveurs SharePoint qui communiquent avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   **Exécuter l’outil de configuration de serveur pour le connecteur Microsoft RMS** 

        Pour plus d’informations, consultez [comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur exécutant SharePoint 2019, 2016 ou SharePoint 2013 :

        ```PowerShell
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   **Si vous utilisez sharepoint 2019, 2016 ou sharepoint 2013, apportez des modifications manuelles au registre** en utilisant les informations des [paramètres du Registre du connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres de Registre sur les serveurs. 

3.  Activez IRM dans SharePoint. Pour plus d'informations, voir [Configurer la gestion des droits relatifs à l’information (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/hh545607(v=office.14)) dans la bibliothèque SharePoint.

    Dans le cadre de ces instructions, vous devez configurer SharePoint pour utiliser le connecteur en spécifiant l'option **Utiliser ce serveur RMS**, puis entrer l'URL de connecteur d'équilibrage de charge configurée. 

    Saisissez le préfixe de protocole (HTTP:// ou HTTPS://) ainsi que le nom du connecteur, tel que défini dans le système DNS pour l'adresse d'équilibrage de charge. 

    Par exemple, si le nom de votre connecteur est `https:\//connector.contoso.com`, votre configuration ressemble à l'image suivante :

    ![Configuration de SharePoint Server pour le connecteur RMS](./media/AzRMS_SharePointConnector.png)

    Une fois les services RMS activés pour une ferme SharePoint, vous pouvez les activer pour des bibliothèques grâce à l'option **Services RMS** de la page **Paramètres de la bibliothèque** pour chacune des bibliothèques.

## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>Configuration d'un serveur de fichiers pour l'infrastructure de classification des fichiers afin d'utiliser le connecteur

Pour utiliser le connecteur RMS et l'infrastructure de classification des fichiers dans l'objectif de protéger des documents Office, le serveur de fichiers doit exécuter l'un des systèmes d'exploitation suivants :

- Windows Server 2016

- Windows Server 2012 R2

- Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>Configuration de serveurs de fichiers afin d'utiliser le connecteur

1. Vérifiez que les serveurs de fichiers sont autorisés à utiliser le connecteur RMS à l’aide de l’outil d’administration du connecteur RMS et des informations contenues dans la section [Définition des serveurs autorisés à utiliser le connecteur RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Cette configuration est exigée pour que vos serveurs de fichiers puissent utiliser le connecteur RMS.

2. Sur les serveurs de fichiers qui sont configurés pour l'infrastructure de classification des fichiers et appelés à communiquer avec le connecteur RMS, effectuez l'une des opérations suivantes :

    -   **Exécuter l’outil de configuration de serveur pour le connecteur Microsoft RMS** 
    
        Pour plus d’informations, consultez [comment utiliser l’outil de configuration de serveur pour le connecteur Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Par exemple, pour exécuter l’outil localement afin de configurer un serveur de fichiers exécutant ICF :

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - **Apportez des modifications manuelles au registre** en utilisant les informations des [paramètres du Registre du connecteur RMS](rms-connector-registry-settings.md) pour ajouter manuellement des paramètres de Registre sur les serveurs. 

3. Créez des règles de classification et des tâches de gestion de fichiers pour protéger les documents avec le chiffrement RMS, puis spécifiez un modèle RMS pour appliquer automatiquement des stratégies RMS. 

    Pour plus d'informations, voir [Vue d'ensemble du Gestionnaire de ressources du serveur de fichiers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11)) dans la bibliothèque de documentation Windows Server.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que le connecteur RMS est installé et configuré, et que vos serveurs sont configurés pour l’utiliser, les administrateurs informatiques et les utilisateurs peuvent protéger et utiliser les e-mails et les documents à l’aide du service Azure Rights Management. 

Pour faciliter la tâche des utilisateurs, déployez le client Azure Information Protection, qui installe un module complémentaire pour Office et ajoute de nouvelles options contextuelles à l’Explorateur de fichiers. 

Pour plus d’informations, consultez le [Guide de l’administrateur du client Azure Information Protection](./rms-client/client-admin-guide.md).

Notez, que si vous configurez des modèles de services que vous souhaitez utiliser avec des règles de transport Exchange ou Windows Server FCI, la configuration de l’étendue doit inclure l’option de compatibilité des applications de manière à ce que la case à cocher **Afficher ce modèle à tous les utilisateurs lorsque les applications ne prennent pas en charge l'identité de l'utilisateur** soit activée.

Vous pouvez utiliser la [Feuille de route pour le déploiement d’Azure Information Protection](deployment-roadmap-classify-label-protect.md) pour déterminer si d’autres étapes de configuration peuvent s’avérer nécessaires avant de mettre Azure Rights Management à la disposition des utilisateurs et des administrateurs.

Pour surveiller le connecteur RMS, consultez [Surveiller le connecteur Azure Rights Management](monitor-rms-connector.md).