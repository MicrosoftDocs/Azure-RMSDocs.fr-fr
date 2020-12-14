---
title: Log & analyser l’utilisation de la protection à partir de Azure Information Protection
description: Informations et instructions sur l’utilisation de la journalisation de l’utilisation pour le service de protection à partir de Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 06b32848bd1e2b0fa939474e74c174a674427eec
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384381"
---
# <a name="logging-and-analyzing-the-protection-usage-from-azure-information-protection"></a>Journalisation et analyse de l’utilisation de la protection à partir de Azure Information Protection

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Utilisez ces informations pour vous aider à comprendre comment utiliser la journalisation de l’utilisation pour le service de protection (Azure Rights Management) à partir de Azure Information Protection. Ce service de protection fournit la protection des données pour les documents et e-mails de votre organisation, et il peut journaliser chaque demande. Ces demandes incluent les cas où les utilisateurs protègent des documents et des e-mails, mais également consomment ce contenu, les actions effectuées par vos administrateurs pour ce service et les actions effectuées par des opérateurs Microsoft pour prendre en charge votre déploiement Azure Information Protection. 

Vous pouvez ensuite utiliser ces journaux d’utilisation de la protection pour prendre en charge les scénarios d’entreprise suivants :

-   **Analyse pour gagner en visibilité**

    Les journaux générés par le service de protection peuvent être importés dans un référentiel de votre choix (par exemple, une base de données, un système de traitement analytique en ligne (OLAP) ou un système Map-Reduce) pour analyser les informations et générer des rapports. Par exemple, vous pouvez identifier les personnes qui accèdent à vos données protégées, déterminer quelles sont les données protégées auxquelles accèdent les utilisateurs, à partir de quels appareils et à partir de quel emplacement, savoir si les utilisateurs parviennent à consulter du contenu protégé, ou encore identifier les personnes qui ont lu un document important qui était protégé.

-   **Surveillance des abus**

    Les informations de journalisation relatives à l’utilisation de la protection sont disponibles quasiment en temps réel, ce qui vous permet de surveiller en permanence l’utilisation du service de protection de votre entreprise. 99,9 % des journaux sont disponibles pour le service dans un délai de 15 minutes suivant le début d’une action initiée.

    Par exemple, vous pouvez souhaiter recevoir une alerte en cas d’augmentation soudaine du nombre de personnes qui consultent des données protégées en dehors des heures de travail, ce qui pourrait signifier qu’un utilisateur malveillant recueille des informations pour les revendre à des concurrents, ou si un même utilisateur accède visiblement à des données à partir d’adresses IP différentes dans un court laps de temps, cela peut indiquer qu’un compte d’utilisateur a été compromis.

-   **Audit légal**

    En cas de fuite d'informations, vous devrez très certainement fournir une liste des personnes qui ont accédé récemment à des documents spécifiques ainsi que le type d'informations auxquelles a pu accéder un individu suspecté. Vous pouvez répondre à ces types de questions lorsque vous utilisez cette journalisation, car les personnes qui utilisent du contenu protégé doivent toujours obtenir une licence Rights Management pour ouvrir des documents et des images protégés par Azure Information Protection, même si ces fichiers sont déplacés par courrier électronique ou copiés sur des lecteurs USB ou d’autres dispositifs de stockage. Cela signifie que vous pouvez utiliser ces journaux en tant que source d’informations définitive pour une analyse de l’investigation lorsque vous protégez vos données à l’aide de Azure Information Protection.

En plus de cette journalisation de l’utilisation, vous disposez également des options de journalisation suivantes :

|Option de journalisation|Description|
|----------------|---------------|
|**Journal d’administration**|Journalise les tâches d’administration pour le service de protection. Par exemple, si le service est désactivé, lorsque la fonctionnalité de super utilisateur est activée et lorsque des utilisateurs délèguent des autorisations d’administrateur au service. <br /><br />Pour plus d’informations, consultez l’applet de commande PowerShell, [obtenir-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog).|
|**Suivi des documents**|Permet aux utilisateurs d’effectuer le suivi et de révoquer les documents dont ils ont effectué le suivi avec le client Azure Information Protection. Les administrateurs généraux peuvent également effectuer le suivi de ces documents au nom des utilisateurs. <br /><br />Pour plus d’informations, consultez [Configuration et utilisation du suivi des documents pour Azure Information Protection](./rms-client/client-admin-guide-document-tracking.md).|
|**Journaux des événements de client**|Activité d’utilisation pour le client Azure Information Protection, enregistrée dans le journal des événements **Applications et services** Windows local, **Azure Information Protection**. <br /><br />Pour plus d’informations, consultez [Journalisation de l’utilisation du client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-classic-client).|
|**Fichiers journaux du client**|Journaux de dépannage pour le client Azure Information Protection, qui se trouvent dans **%localappdata%\Microsoft\MSIP**. <br /><br />Ces fichiers sont destinés au Support Microsoft.|
| | |

En outre, les informations dans les journaux d’utilisation du client Azure Information Protection et le scanneur Azure Information Protection sont collectées et agrégées afin de créer des rapports dans le portail Azure. Pour plus d’informations, consultez [Création de rapports pour Azure Information Protection](reports-aip.md).

Utilisez les sections suivantes pour plus d’informations sur la journalisation de l’utilisation pour le service de protection. 

## <a name="how-to-enable-logging-for-protection-usage"></a>Comment activer la journalisation de l’utilisation de la protection
La journalisation de l’utilisation de la protection est activée par défaut pour tous les clients. 

Le stockage des journaux ou la fonctionnalité de journalisation n’entraînent pas de frais supplémentaires.

## <a name="how-to-access-and-use-your-protection-usage-logs"></a>Comment accéder à vos journaux d’utilisation de la protection et les utiliser
Azure Information Protection écrit les journaux sous la forme d’une série d’objets BLOB dans un compte de stockage Azure qu’il crée automatiquement pour votre locataire. Chaque objet blob contient un ou plusieurs enregistrements journal au format W3C étendu. Les noms des objets blob sont des chiffres et sont classés dans leur ordre de création. La section [Comment interpréter vos journaux d’utilisation d’Azure Rights Management](#how-to-interpret-your-usage-logs) (plus loin dans ce document) contient des informations supplémentaires sur le contenu des journaux et leur création.

L’affichage des journaux dans votre compte de stockage peut prendre un certain temps après une action de protection. La plupart des journaux apparaissent dans un délai de 15 minutes. Nous vous conseillons de télécharger les journaux vers un espace de stockage local, tel qu’un dossier, une base de données ou un référentiel Map/Reduce.

Pour télécharger vos journaux d’utilisation, vous allez utiliser le module PowerShell AIPService pour Azure Information Protection. Pour obtenir des instructions d’installation, consultez [installation du module PowerShell AIPService](install-powershell.md).

### <a name="to-download-your-usage-logs-by-using-powershell"></a>Pour télécharger vos journaux d’utilisation à l’aide de PowerShell

1.  Démarrez Windows PowerShell avec l’option **exécuter en tant qu’administrateur** et utilisez l’applet de commande [Connect-AipService](/powershell/module/aipservice/connect-aipservice) pour vous connecter à Azure information protection :

    ```PowerShell
    Connect-AipService
    ```
    
2.  Pour télécharger les journaux correspondant à une date précise, exécutez la commande suivante : 

    ```PowerShell
    Get-AipServiceUserLog -Path <location> -fordate <date>
    ```

    Par exemple, après avoir créé un dossier nommé Logs sur votre lecteur E :
    
    * Pour télécharger les journaux correspondant à une date précise (par exemple le 1er février 2016), exécutez la commande suivante : `Get-AipServiceUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Pour télécharger les journaux correspondant à une plage de dates (par exemple du 1er au 14 février 2016), exécutez la commande suivante : `Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Si vous spécifiez uniquement le jour, comme dans nos exemples, l’heure est supposée être 00:00:00 dans votre heure locale, puis convertie en temps universel coordonné (UTC). Quand vous spécifiez une heure à l’aide des paramètres -fromdate ou -todate (par exemple, -fordate "2/1/2016 15:00:00"), ces date et heure sont converties au format UTC. La commande Get-AipServiceUserLog obtient ensuite les journaux pour cette période UTC.

Vous ne pouvez pas spécifier moins d’une journée entière à télécharger.

Par défaut, cette applet de commande utilise trois threads pour télécharger les journaux. Si vous disposez d’une bande passante suffisante et souhaitez réduire le temps nécessaire pour télécharger les journaux, utilisez le paramètre -NumberOfThreads qui prend en charge une valeur comprise entre 1 et 32. Par exemple, si vous exécutez la commande suivante, l’applet de commande génère 10 threads pour télécharger les journaux : `Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> Vous pouvez agréger l’ensemble de vos fichiers journaux téléchargés dans un fichier CSV en utilisant l’[Analyseur du journal de Microsoft](https://www.microsoft.com/download/details.aspx?id=24659). Il s’agit d’un outil permettant d’effectuer des conversions entre plusieurs formats de fichiers journaux connus. Vous pouvez également utiliser cet outil pour convertir des données dans le format SYSLOG, ou les importer dans une base de données. Après avoir installé l’outil, exécutez `LogParser.exe /?` pour obtenir de l’aide et des informations sur l’utilisation de cet outil. 
>
> Par exemple, vous pouvez exécuter la commande suivante pour importer toutes les informations dans un fichier au format .log : `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

## <a name="how-to-interpret-your-usage-logs"></a>Comment interpréter vos journaux d’utilisation
Utilisez les informations suivantes pour vous aider à interpréter les journaux d’utilisation de la protection.

### <a name="the-log-sequence"></a>Séquence du journal
Azure Information Protection écrit les journaux sous la forme d’une série d’objets BLOB.

Chaque entrée du journal a un horodatage UTC. Étant donné que le service de protection s’exécute sur plusieurs serveurs répartis dans plusieurs centres de données, les journaux peuvent parfois sembler hors séquence, même s’ils sont triés en fonction de leur horodateur. Toutefois, le décalage est mineur et souvent inférieur à une minute. Dans la plupart des cas, cela ne risque pas de poser de problème lors de l'analyse des journaux.

### <a name="the-blob-format"></a>Format des objets blob
Chaque objet blob est au format de journal W3C étendu. Il commence par les deux lignes suivantes :

**#Software : RMS**

**#Version : 1,1**

La première ligne indique qu’il s’agit de journaux de protection à partir de Azure Information Protection. La deuxième indique que le reste de l’objet blob suit les spécifications de la version 1.1. À titre de recommandation, les applications qui analysent ces journaux doivent vérifier ces deux lignes avant de continuer l’analyse du reste de l’objet blob.

La troisième ligne énumère une liste de noms de champs séparés par des tabulations :

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

Chacune des lignes suivantes est un enregistrement de journal. Les valeurs des champs sont dans le même ordre que celui de la ligne précédente et sont séparées par des tabulations. Utilisez le tableau suivant pour interpréter les champs.

| Nom du champ         | Type de données W3C | Description                                                                                                                                                                                                                                                                                          | Valeur d'exemple                                                                                                                       |
| ------------------ | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **date**           | Date          | Date UTC du traitement de la demande.<br /><br />La source est l’horloge locale du serveur qui a traité la demande.                                                                                                                                                                                | 25-06-2013                                                                                                                          |
| **time**           | Temps          | Heure UTC (au format 24 h) du traitement de la demande.<br /><br />La source est l’horloge locale du serveur qui a traité la demande.                                                                                                                                                              | 21:59:28                                                                                                                            |
| **ID de ligne**         | Texte          | GUID unique de cet enregistrement de journal. En l’absence de valeur, utilisez la valeur correlation-id pour identifier l’entrée.<br /><br />Cette valeur est utile lorsque vous agrégez des journaux ou lorsque vous copiez des journaux dans un autre format.                                                                                            | 1c3fe7a9-d9e0-4654-97b7-14fafa72ea63                                                                                                |
| **type de demande**  | Nom          | Nom de l’API RMS demandée.                                                                                                                                                                                                                                                              | AcquireLicense                                                                                                                      |
| **ID utilisateur**        | String        | Utilisateur ayant adressé la demande.<br /><br />La valeur est placée entre guillemets simples. Les appels à partir d’une clé de locataire gérée par vous (BYOK) ont la valeur **"**, qui s’applique également quand les types de demande sont anonymes.                                                                     | ‘joe@contoso.com’                                                                                                                   |
| **result**         | String        | « Success » si la demande a été traitée correctement.<br /><br />Type d’erreur (entre guillemets simples) si la demande échoue.                                                                                                                                                                           | « Succès »                                                                                                                           |
| **ID de corrélation** | Texte          | GUID commun au journal du client RMS et au journal du serveur pour une demande donnée.<br /><br />Cette valeur peut être utile pour résoudre les problèmes liés au client.                                                                                                                                        | cab52088-8925-4371-be34-4b71a3112356                                                                                                |
| **ID de contenu**     | Texte          | GUID (entre accolades) qui identifie le contenu protégé (par exemple, un document).<br /><br />Ce champ contient une valeur uniquement si le champ request-type est égal à AcquireLicense. Sinon, il reste vierge pour les autres types de demande.                                                                                   | {bb4af47b-cfed-4719-831d-71b98191a4f2}                                                                                              |
| **owner-email**    | String        | Adresse de messagerie du propriétaire du document.<br /><br /> Ce champ est vide si le type de demande est RevokeAccess.                                                                                                                                                                                     | alice@contoso.com                                                                                                                   |
| **Émetteur**         | String        | Adresse de messagerie de l’émetteur du document. <br /><br /> Ce champ est vide si le type de demande est RevokeAccess.                                                                                                                                                                                          | alice@contoso.com ou FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'                                             |
| **ID de modèle**   | String        | ID du modèle utilisé pour protéger le document. <br /><br /> Ce champ est vide si le type de demande est RevokeAccess.                                                                                                                                                                               | {6d9371a6-4e2d-4e97-9a38-202233fed26e}                                                                                              |
| **nom de fichier**      | String        | Nom de fichier d’un document protégé qui est suivi en utilisant le client Azure Information Protection pour Windows. <br /><br />Actuellement, certains fichiers (tels que les documents Office) sont affichés sous forme de GUID plutôt que noms de fichiers réels.<br /><br /> Ce champ est vide si le type de demande est RevokeAccess. | TopSecretDocument.docx                                                                                                              |
| **Date de publication** | Date          | Date à laquelle le document a été protégé.<br /><br /> Ce champ est vide si le type de demande est RevokeAccess.                                                                                                                                                                                           | 2015-10-15T21:37:00                                                                                                                 |
| **c-info**         | String        | Informations concernant la plateforme du client d’où émane la demande.<br /><br />La chaîne spécifique varie selon l'application (par exemple, le système d'exploitation ou le navigateur).                                                                                                            | ’MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64’ |
| **c-IP**           | Adresse       | Adresse IP du client d’où émane la demande.                                                                                                                                                                                                                                                     | 64.51.202.144                                                                                                                       |
| **admin-action**   | Bool          | Définit si un administrateur a eu accès au site de suivi des documents en mode administrateur.                                                                                                                                                                                                              | Vrai                                                                                                                                |
| **acting-as-user** | String        | Adresse e-mail de l’utilisateur pour lequel un administrateur accède au site de suivi des documents.                                                                                                                                                                                                     | 'joe@contoso.com'                                                                                                                   |
|                    |               |                                                                                                                                                                                                                                                                                                      |                                                                                                                                     |

#### <a name="exceptions-for-the-user-id-field"></a>Exceptions pour le champ user-id.
Bien que le champ user-id indique généralement l'utilisateur qui effectue la demande, il existe deux exceptions pour lesquelles la valeur ne mappe pas à un utilisateur réel :

-   Valeur **'microsoftrmsonline@&lt;votreIDdeClient&gt;.rms.&lt;région&gt;.aadrm.com'**.

    Cela indique qu’un service Office 365, tel qu’Exchange Online ou Microsoft SharePoint, fait la demande. Dans la chaîne, *&lt; YourTenantID &gt;* est le GUID de votre locataire et *&lt; région &gt;* est la région dans laquelle votre locataire est inscrit. Par exemple, **na** correspond à l'Amérique du Nord, **eu** correspond à l'Europe et **ap** correspond à l'Asie.

-   Si vous utilisez le connecteur RMS :

    Les demandes émises par ce connecteur sont journalisées avec le nom de principal du service **Aadrm_S-1-7-0**, automatiquement généré à l’installation du connecteur RMS.

#### <a name="typical-request-types"></a>Types de demande standard
Il existe de nombreux types de demandes pour le service de protection, mais le tableau suivant identifie certains des types de demandes les plus utilisés.

|Type de demande|Description|
|----------------|---------------|
|**AcquireLicense**|Un client d’un ordinateur Windows demande une licence pour du contenu protégé.|
|**AcquirePreLicense**|Un client, pour le compte de l’utilisateur, demande une licence pour le contenu protégé.|
|**AcquireTemplates**|Un appel a été fait pour acquérir des modèles basés sur des ID de modèle.|
|**AcquireTemplateInformation**|Un appel a été fait pour obtenir les ID du modèle à partir du service.|
|**AddTemplate**|Un appel est fait à partir du portail Azure pour ajouter un modèle.|
|**AllDocsCsv**|Un appel est effectué à partir du site de suivi des documents pour télécharger le fichier CSV à partir de la page **Tous les documents**.|
|**BECreateEndUserLicenseV1**|Un appel est fait à partir d’un appareil mobile pour créer une licence utilisateur final.|
|**BEGetAllTemplatesV1**|Un appel est fait à partir d’un appareil mobile (principal) pour obtenir tous les modèles.|
|**Certify**|Le client certifie l’utilisateur pour la consommation et la création de contenu protégé.|
|**FECreateEndUserLicenseV1**|Similaire à la demande AcquireLicense, mais à partir d’un appareil mobile.|
|**FECreatePublishingLicenseV1**|Identique à Certify et GetClientLicensorCert combinés, mais à partir de clients mobiles.|
|**FEGetAllTemplates**|Un appel est fait à partir d’un appareil mobile (frontal) pour obtenir les modèles.|
|**FindServiceLocationsForUser**|Un appel est fait pour rechercher des URL utilisées pour appeler Certify ou AcquireLicense.|
|**GetClientLicensorCert**|Le client demande un certificat de publication (qui sera ensuite utilisé pour protéger du contenu) à partir d'un ordinateur Windows.|
|**GetConfiguration**|Une applet de commande Azure PowerShell est appelée pour obtenir la configuration du client Azure RMS.|
|**GetConnectorAuthorizations**|Un appel est fait via les connecteurs RMS pour obtenir leur configuration à partir du cloud.|
|**GetRecipients**|Un appel est effectué à partir du site de suivi des documents pour accéder à l’affichage de liste pour un seul document.|
|**GetTenantFunctionalState**|Le Portail Azure vérifie si le service de protection (Azure Rights Management) est activé.|
|**KeyVaultDecryptRequest**|Le client tente de déchiffrer le contenu protégé par RMS. Applicable uniquement pour une clé de locataire gérée par le client (BYOK) dans Azure Key Vault.|
|**KeyVaultGetKeyInfoRequest**|Un appel est effectué pour vérifier que la clé spécifiée pour être utilisée dans Azure Key Vault pour la clé de locataire Azure Information Protection est accessible et n’est pas déjà utilisée.|
|**KeyVaultSignDigest**|Un appel est effectué quand une clé gérée par le client (BYOK) dans Azure Key Vault est utilisée à des fins de signature. Cet appel est généralement fait une fois par demande AcquireLicense (ou FECreateEndUserLicenseV1), Certify et GetClientLicensorCert (ou FECreatePublishingLicenseV1).|
|**KMSPDecrypt**|Le client tente de déchiffrer le contenu protégé par RMS. Applicable uniquement pour une clé de locataire gérée par le client (BYOK) héritée.|
|**KMSPSignDigest**|Un appel est fait quand une clé gérée par le client (BYOK) héritée est utilisée à des fins de signature. Cet appel est généralement fait une fois par demande AcquireLicense (ou FECreateEndUserLicenseV1), Certify et GetClientLicensorCert (ou FECreatePublishingLicenseV1).|
|**ServerCertify**|Un appel est fait à partir d’un client RMS (par exemple, SharePoint) pour certifier le serveur.|
|**SetUsageLogFeatureState**|Un appel est fait pour activer la journalisation de l’utilisation.|
|**SetUsageLogStorageAccount**|Un appel est effectué pour spécifier l’emplacement des journaux du service Azure Rights Management.|
|**UpdateTemplate**|Un appel est fait à partir du portail Azure pour mettre à jour un modèle existant.|
| | | 

**Client classique uniquement**

Les types de demandes suivants sont pertinents pour les utilisateurs avec le client classique AIP uniquement :

|Type de demande|Description|
|----------------|---------------|
|**DeleteTemplateById**|Un appel est fait à partir du portail Azure pour supprimer un modèle sur la base de son ID.|
|**DocumentEventsCsv**|Un appel est effectué à partir du site de suivi des documents pour télécharger le fichier CSV pour un seul document.|
|**ExportTemplateById**|Un appel est fait à partir du portail Azure pour exporter un modèle sur la base de son ID.|
|**FEGetAllTemplates**|Un appel est fait à partir d’un appareil mobile (frontal) pour obtenir les modèles.|
|**GetAllDocs**|Un appel est effectué à partir du site de suivi des documents pour charger la page **tous les documents** pour un utilisateur ou rechercher tous les documents pour le client. Utilisez cette valeur avec les champs admin-action et acting-as-admin :<br /><br />- admin-action est vide : un utilisateur affiche la page **tous les documents** page pour ses propres documents.<br /><br />- admin-action a la valeur true et acting-as-user est vide : un administrateur affiche tous les documents pour son client.<br /><br />- admin-action a la valeur true et acting-as-user n’est pas vide : un administrateur affiche la page **tous les documents** pour un utilisateur.|
|**GetAllTemplates**|Un appel est fait à partir du portail Azure pour obtenir tous les modèles.|
|**GetConnectorAuthorizations**|Un appel est fait via les connecteurs RMS pour obtenir leur configuration à partir du cloud.|
|**GetSingle**|Un appel est effectué à partir du site de suivi des documents pour accéder à une page **un seul document**.|
|**GetTemplateById**|Un appel est fait à partir du portail Azure pour obtenir un modèle en spécifiant son ID.|
|**LoadEventsForMap**|Un appel est effectué à partir du site de suivi des documents pour accéder à l’affichage du mappage pour un seul document.|
|**LoadEventsForSummary**|Un appel est effectué à partir du site de suivi des documents pour accéder à l’affichage de la chronologie pour un seul document.|
|**LoadEventsForTimeline**|Un appel est effectué à partir du site de suivi des documents pour accéder à l’affichage du mappage pour un seul document.|
|**ImportTemplate**|Un appel est fait à partir du portail Azure pour importer un modèle.|
|**RevokeAccess**|Un appel est effectué à partir du site de suivi des documents pour révoquer un document.|
|**SearchUsers** |Un appel est effectué à partir du site de suivi des documents pour rechercher tous les utilisateurs dans un client.|
|**UpdateNotificationSettings**|Un appel est effectué à partir du site de suivi des documents pour modifier les paramètres de notification pour un seul document.|
|**UpdateTemplate**|Un appel est fait à partir du portail Azure pour mettre à jour un modèle existant.|
| | | 



## <a name="powershell-reference"></a>Informations de référence sur PowerShell

La seule applet de commande PowerShell dont vous avez besoin pour accéder à la journalisation de l’utilisation de la protection est [AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog). 

Pour plus d’informations sur l’utilisation de PowerShell pour Azure Information Protection, consultez [administration de la protection à partir de Azure information protection à l’aide de PowerShell](administer-powershell.md).
