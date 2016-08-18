---
title: "Journalisation et analyse de l’utilisation d’Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5ab8d4ef132eec9991c0ff789f2b2dfa7bdf2cd8
ms.openlocfilehash: 845a47f526754f291c27a3c2bbd80af736b44992


---

# Journalisation et analyse de l’utilisation d’Azure Rights Management

*S’applique à : Azure Rights Management, Office 365*

Les informations de cette rubrique aident à comprendre comment utiliser la journalisation de l’utilisation avec Azure Rights Management (Azure RMS). Le service Azure Rights Management peut journaliser chaque demande effectuée pour votre organisation, notamment les demandes provenant d’utilisateurs, les actions effectuées par les administrateurs Rights Management au sein de votre organisation, ainsi que les actions effectuées par les opérateurs Microsoft pour prendre en charge votre déploiement du service Azure Rights Management.

Vous pouvez ensuite utiliser les journaux Azure Rights Management dans le cadre des scénarios d’entreprise suivants :

-   **Analyse pour gagner en visibilité**

    Vous pouvez importer les journaux générés par Azure Rights Management dans le référentiel de votre choix (par exemple, une base de données, un système de traitement analytique en ligne (OLAP) ou un système Map/Reduce) pour analyser les informations et générer des rapports. Par exemple, vous pourriez identifier les personnes qui accèdent à vos données protégées par RMS, déterminer quelles sont les données protégées par RMS auxquelles accèdent les utilisateurs, à partir de quels appareils et à partir de quel emplacement, savoir si les utilisateurs parviennent à consulter du contenu protégé, ou encore identifier les personnes qui ont lu un document important qui était protégé.

-   **Surveillance des abus**

    Les informations de journalisation d’Azure Rights Management mises à votre disposition quasiment en temps réel vous permettent de surveiller en continu l’utilisation de Rights Management au sein de votre entreprise. 99,9 % des journaux sont disponibles dans un délai de 15 minutes suivant le début d’une action initiée par RMS.

    Par exemple, vous souhaiteriez peut-être recevoir une alerte en cas d’augmentation soudaine du nombre de personnes qui consultent des données protégées par RMS en dehors des heures de travail, ce qui pourrait signifier qu’un utilisateur malveillant recueille des informations pour les revendre à des concurrents, ou si un même utilisateur accède visiblement à des données à partir d’adresses IP différentes dans un court laps de temps, cela peut indiquer qu’un compte d’utilisateur a été compromis.

-   **effectuer une analyse d’investigation ;**

    En cas de fuite d’informations, vous devrez très certainement fournir une liste des personnes qui ont accédé récemment à des documents spécifiques ainsi que le type d’informations auxquelles a pu accéder un individu suspecté. Vous pouvez répondre à ces types de questions quand vous utilisez Azure Rights Management et la journalisation, car les personnes qui consultent du contenu protégé doivent toujours obtenir une licence Rights Management pour ouvrir des documents et des images protégés par Azure Rights Management, même si ces fichiers sont déplacés par e-mail ou s’ils sont copiés sur des lecteurs USB ou d’autres dispositifs de stockage. Cela signifie que vous pouvez utiliser les journaux storage devices en tant que source d’informations fiable pour une analyse légale quand vous protégez vos données à l’aide d’Azure Rights Management.

> [!NOTE]
> Si vous vous intéressez uniquement à la journalisation des tâches d’administration pour Azure Rights Management et que vous ne souhaitez pas suivre la manière dont les utilisateurs utilisent Rights Management, vous pouvez utiliser l’applet de commande Windows PowerShell [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) pour Azure Rights Management.
> 
> Vous pouvez également utiliser le portail Azure Classic pour obtenir des rapports détaillés tels que **Résumé RMS**, **Utilisateurs RMS actifs**, **Plateformes des appareils RMS** et **Utilisation d’applications RMS**. Pour accéder à ces rapports à partir du portail Azure Classic, cliquez sur **Active Directory**, sélectionnez et ouvrez un annuaire, puis cliquez sur **RAPPORTS**.

Pour plus d’informations sur la journalisation de l’utilisation d’Azure Rights Management, consultez les sections suivantes.

## Comment activer la journalisation de l’utilisation d’Azure Rights Management
Depuis février 2016, la journalisation de l’utilisation d’Azure Rights Management est activée par défaut pour tous les clients. Cela s’applique aux clients qui ont activé leur service Azure RMS avant février 2016 et à ceux qui l’activent après février 2016. 

> [!NOTE]
> Le stockage des journaux ou la fonctionnalité de journalisation n’entraînent pas de frais supplémentaires.
> 
> Si vous utilisiez la journalisation de l’utilisation pour Azure RMS avant février 2016, vous aviez besoin d’un abonnement à Azure et d’une capacité de stockage suffisante sur Azure, ce qui n’est plus le cas.



## Comment accéder aux journaux d’utilisation Azure Rights Management et les utiliser
Azure Rights Management écrit des journaux enregistrés dans votre compte de stockage Azure sous la forme d’une série d’objets blob. Chaque objet blob contient un ou plusieurs enregistrements journal au format W3C étendu. Les noms des objets blob sont des chiffres et sont classés dans leur ordre de création. La section [Comment interpréter vos journaux d’utilisation d’Azure Rights Management](#how-to-interpret-your-azure-rights-management-usage-logs) (plus loin dans ce document) contient des informations supplémentaires sur le contenu des journaux et leur création.

Les journaux peuvent mettre un certain temps à apparaître dans votre compte de stockage après une action Azure Rights Management. La plupart des journaux apparaissent dans un délai de 15 minutes. Nous vous conseillons de télécharger les journaux vers un espace de stockage local, tel qu’un dossier, une base de données ou un référentiel Map/Reduce.

Pour télécharger vos journaux d’utilisation, vous allez utiliser le module d’administration RMS Azure pour Windows PowerShell. Pour obtenir des instructions d’installation, consultez [Installation de Windows PowerShell pour Azure Rights Management](install-powershell.md). Si vous avez déjà téléchargé ce module Windows PowerShell, exécutez la commande suivante pour vérifier que le numéro de votre version est au minimum **2.4.0.0** : `(Get-Module aadrm -ListAvailable).Version` 

### Pour télécharger vos journaux d’utilisation à l’aide de PowerShell

1.  Démarrez Windows PowerShell avec l’option **Exécuter en tant qu’administrateur**, puis utilisez l’applet de commande [Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) pour vous connecter au service Azure Rights Management :

    ```
    Connect-AadrmService
    ```
    
2.  Pour télécharger les journaux correspondant à une date précise, exécutez la commande suivante : 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    Par exemple, après avoir créé un dossier nommé Logs sur votre lecteur E :
    
    * Pour télécharger les journaux correspondant à une date précise (par exemple, le 1er février 2016), exécutez la commande suivante : `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Pour télécharger les journaux correspondant à une plage de dates (par exemple, du 1er au 14 février 2016), exécutez la commande suivante : `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Si vous spécifiez uniquement le jour, comme dans nos exemples, l’heure est supposée être 00:00:00 dans votre heure locale, puis convertie en temps universel coordonné (UTC). Quand vous spécifiez une heure à l’aide des paramètres -fromdate ou -todate (par exemple, -fordate "2/1/2016 15:00:00"), ces date et heure sont converties au format UTC. La commande Get-AadrmUserLog obtient alors les journaux correspondant à cette période UTC.

Vous ne pouvez pas spécifier moins d’une journée entière à télécharger.

Par défaut, cette applet de commande utilise trois threads pour télécharger les journaux. Si vous disposez d’une bande passante suffisante et souhaitez réduire le temps nécessaire pour télécharger les journaux, utilisez le paramètre -NumberOfThreads qui prend en charge une valeur comprise entre 1 et 32. Par exemple, si vous exécutez la commande suivante, l’applet de commande génère 10 threads pour télécharger les journaux : `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Vous pouvez agréger l’ensemble de vos fichiers journaux téléchargés dans un fichier CSV en utilisant l’[Analyseur du journal de Microsoft](https://www.microsoft.com/download/details.aspx?id=24659). Il s’agit d’un outil permettant d’effectuer des conversions entre plusieurs formats de fichiers journaux connus. Vous pouvez également utiliser cet outil pour convertir des données dans le format SYSLOG, ou les importer dans une base de données. Après avoir installé l’outil, exécutez `LogParser.exe /?` pour obtenir de l’aide et des informations sur l’utilisation de cet outil. 
>
> Par exemple, vous pouvez exécuter la commande suivante pour importer toutes les informations dans un fichier au format .log : `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Si vous avez activé manuellement la journalisation de l’utilisation d’Azure RMS avant le changement de journalisation du 22 février 2016


Si vous utilisiez la journalisation de l’utilisation avant le changement de journalisation, vous aurez des journaux d’utilisation dans votre compte de stockage Azure. Dans le cadre de ce changement de journalisation, Microsoft ne copie pas ces journaux de votre compte de stockage vers le nouveau compte de stockage géré Azure RMS. Vous êtes responsable de la gestion du cycle de vie des journaux générés précédemment, et vous pouvez utiliser l’applet de commande [Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) pour télécharger vos anciens journaux. Exemple :

- Pour télécharger tous les journaux disponibles dans votre dossier E:\logs : `Get-AadrmUsageLog -Path "E:\Logs"`
    
- Pour télécharger une plage d'objets blob spécifique : `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

Notez que vous n’avez pas à télécharger de journaux à l’aide de l’applet de commande Get-AadrmUsageLog dans les cas suivants :

-  Vous activé Azure Rights Management avant le 22 février 2016, mais n’avez pas activé la fonctionnalité de journalisation de l’utilisation.

- Vous activé Azure Rights Management après le 22 février 2016.

## Comment interpréter vos journaux d’utilisation d’Azure Rights Management
Pour interpréter les journaux d’utilisation d’Azure Rights Management, utilisez les informations suivantes.

### Séquence du journal
Azure Rights Management écrit les journaux sous forme de série d’objets blob. 

Chaque entrée du journal a un horodatage UTC. Étant donné qu’Azure Rights Management s’exécute sur plusieurs serveurs répartis dans plusieurs centres de données, les journaux peuvent parfois sembler hors séquence, même s’ils sont triés en fonction de leur horodatage. Toutefois, le décalage est mineur et souvent inférieur à une minute. Dans la plupart des cas, cela ne risque pas de poser de problème lors de l’analyse des journaux.

### Format des objets blob
Chaque objet blob est au format de journal W3C étendu. Il commence par les deux lignes suivantes :

**#Logiciel : RMS**

**#Version : 1.1**

La première ligne indique qu’il s’agit de journaux Azure Rights Management. La deuxième indique que le reste de l’objet blob suit les spécifications de la version 1.1. À titre de recommandation, les applications qui analysent ces journaux doivent vérifier ces deux lignes avant de continuer l’analyse du reste de l’objet blob.

La troisième ligne énumère une liste de noms de champs séparés par des tabulations :

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

Chacune des lignes suivantes est un enregistrement de journal. Les valeurs des champs sont dans le même ordre que celui de la ligne précédente et sont séparées par des tabulations. Utilisez le tableau suivant pour interpréter les champs.

|Nom du champ|Type de données W3C|Description|Exemple de valeur|
|--------------|-----------------|---------------|-----------------|
|date|Date|Date UTC du traitement de la demande.<br /><br />La source est l’horloge locale du serveur qui a traité la demande.|25-06-2013|
|heure|Heure|Heure UTC (au format 24 h) du traitement de la demande.<br /><br />La source est l’horloge locale du serveur qui a traité la demande.|21:59:28|
|row-id|Text|GUID unique de cet enregistrement de journal. En l’absence de valeur, utilisez la valeur correlation-id pour identifier l’entrée.<br /><br />Cette valeur est utile lorsque vous agrégez des journaux ou lorsque vous copiez des journaux dans un autre format.|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|Nom|Nom de l’API RMS demandée.|AcquireLicense|
|user-id|Chaîne|Utilisateur ayant adressé la demande.<br /><br />La valeur est placée entre guillemets simples. Les appels à partir d’une clé de locataire gérée par vous (BYOK) ont la valeur **"**, qui s’applique également quand les types de demande sont anonymes.|« joe@contoso.com »|
|result|Chaîne|« Success » si la demande a été traitée correctement.<br /><br />Type d’erreur (entre guillemets simples) si la demande échoue.|« Success »|
|correlation-id|Text|GUID commun au journal du client RMS et au journal du serveur pour une demande donnée.<br /><br />Cette valeur peut être utile pour résoudre les problèmes liés au client.|cab52088-8925-4371-be34-4b71a3112356|
|content-id|Text|GUID (entre accolades) qui identifie le contenu protégé (par exemple, un document).<br /><br />Ce champ contient une valeur uniquement si le champ request-type est égal à AcquireLicense. Sinon, il reste vierge pour les autres types de demande.|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|Chaîne|Adresse de messagerie du propriétaire du document.|alice@contoso.com|
|issuer|Chaîne|Adresse de messagerie de l’émetteur du document.|alice@contoso.com (ou) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com’|
|template-id|Chaîne|ID du modèle utilisé pour protéger le document.|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|file-name|Chaîne|Nom de fichier du document qui a été protégé. <br /><br />Actuellement, certains fichiers (tels que les documents Office) sont affichés sous forme de GUID plutôt que noms de fichiers réels.|TopSecretDocument.docx|
|date-published|Date|Date à laquelle le document a été protégé.|2015-10-15T21:37:00|
|c-info|Chaîne|Informations concernant la plateforme du client d’où émane la demande.<br /><br />La chaîne spécifique varie selon l’application (par exemple, le système d’exploitation ou le navigateur).|’MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64’|
|c-ip|Adresse|Adresse IP du client d’où émane la demande.|64.51.202.144|

#### Exceptions pour le champ user-id.
Bien que le champ user-id indique généralement l’utilisateur qui effectue la demande, il existe deux exceptions pour lesquelles la valeur ne mappe pas à un utilisateur réel :

-   Valeur **'microsoftrmsonline@&lt;votreIDdeClient&gt;.rms.&lt;région&gt;.aadrm.com'**.

    Cette valeur indique qu’un service Office 365, tel qu’Exchange Online ou SharePoint Online, est à l’origine de la demande. Dans la chaîne, *&lt;votreIDdeClient&gt;* correspond au GUID de votre client, et *&lt;région&gt;* à la région dans laquelle votre client est inscrit. Par exemple, **AN** représente l’Amérique du Nord, **UE** correspond à l’Europe et **AP** correspond à l’Asie.

-   Si vous utilisez le connecteur RMS :

    Les demandes émises par ce connecteur sont journalisées avec le nom de principal du service **Aadrm_S-1-7-0**, automatiquement généré à l’installation du connecteur RMS.

#### Types de demande standard
Il existe de nombreux types de demande dans Azure Rights Management. Le tableau suivant répertorie quelques-uns des types de demandes les plus utilisés.

|Type de demande|Description|
|----------------|---------------|
|AcquireLicense|Un client sur une machine Windows demande une licence pour du contenu protégé par RMS.|
|AcquirePreLicense|Un client demande, au nom de l’utilisateur, une licence pour du contenu protégé par RMS.|
|AcquireTemplates|Un appel a été fait pour acquérir des modèles basés sur des ID de modèle.|
|AcquireTemplateInformation|Un appel a été fait pour obtenir les ID du modèle à partir du service.|
|AddTemplate|Un appel est fait à partir du portail Azure Classic pour ajouter un modèle.|
|BECreateEndUserLicenseV1|Un appel est fait à partir d’un appareil mobile pour créer une licence utilisateur final.|
|BEGetAllTemplatesV1|Un appel est fait à partir d’un appareil mobile (principal) pour obtenir tous les modèles.|
|Certify|Le client certifie le contenu pour la protection.|
|KMSPDecrypt|Le client tente de déchiffrer le contenu protégé par RMS. Applicable uniquement pour une clé de locataire gérée par le client (BYOK).|
|DeleteTemplateById|Un appel est fait à partir du portail Azure Classic pour supprimer un modèle sur la base de son ID.|
|ExportTemplateById|Un appel est fait à partir du portail Azure Classic pour exporter un modèle sur la base de son ID.|
|FECreateEndUserLicenseV1|Similaire à la demande AcquireLicense, mais à partir d’un appareil mobile.|
|FECreatePublishingLicenseV1|Identique à Certify et GetClientLicensorCert combinés, mais à partir de clients mobiles.|
|FEGetAllTemplates|Un appel est fait à partir d’un appareil mobile (frontal) pour obtenir les modèles.|
|GetAllTemplates|Un appel est fait à partir du portail Azure Classic pour obtenir tous les modèles.|
|GetClientLicensorCert|Le client demande un certificat de publication (qui sera ensuite utilisé pour protéger du contenu) à partir d’un ordinateur Windows.|
|GetConfiguration|Une applet de commande Azure PowerShell est appelée pour obtenir la configuration du client Azure RMS.|
|GetConnectorAuthorizations|Un appel est fait via les connecteurs RMS pour obtenir leur configuration à partir du cloud.|
|GetTenantFunctionalState|Le portail Azure Classic vérifie si Azure RMS est activé.|
|GetTemplateById|Un appel est fait à partir du portail Azure Classic pour obtenir un modèle sur la base de son ID.|
|ExportTemplateById|Un appel est fait à partir du portail Azure Classic pour exporter un modèle sur la base de son ID.|
|FindServiceLocationsForUser|Un appel est fait pour rechercher des URL utilisées pour appeler Certify ou AcquireLicense.|
|ImportTemplate|Un appel est fait à partir du portail Azure Classic pour importer un modèle.|
|ServerCertify|Un appel est fait à partir d’un client RMS (par exemple, SharePoint) pour certifier le serveur.|
|SetUsageLogFeatureState|Un appel est fait pour activer la journalisation de l’utilisation.|
|SetUsageLogStorageAccount|Un appel est fait pour spécifier l’emplacement des journaux Azure RMS.|
|KMSPSignDigest|Un appel est fait quand une clé gérée par le client (BYOK) est utilisée à des fins de signature. Cet appel est généralement fait une fois par demande AcquireLicense (ou FECreateEndUserLicenseV1), Certify et GetClientLicensorCert (ou FECreatePublishingLicenseV1).|
|UpdateTemplate|Un appel est fait à partir du portail Azure Classic pour mettre à jour un modèle existant.|

## Référence Windows PowerShell
À partir de février 2016, la seule applet de commande Windows PowerShell dont vous avez besoin pour la journalisation de l’utilisation d’Azure RMS est [Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx). 

Avant ce changement, les applets de commande (désormais déconseillées) nécessaires pour les journaux d’utilisation d’Azure RMS étaient les suivantes :  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Si vous avez dans votre propre stockage Azure des journaux antérieurs au changement de journalisation d’Azure RMS, vous pouvez les télécharger à l’aide de ces applets de commande plus anciennes, en utilisant Get-AadrmUsageLog et Get-AadrmUsageLogLastCounterValue comme précédemment. En revanche, tous les nouveaux journaux d’utilisation sont consignés dans le nouveau stockage Azure RMS, et doivent être téléchargés à l’aide de l’applet de commande Get-AadrmUserLog.

Pour plus d’informations sur l’utilisation de Windows PowerShell pour Azure Rights Management, consultez [Administration d’Azure Rights Management à l’aide de Windows PowerShell](administer-powershell.md).






<!--HONumber=Jul16_HO3-->


