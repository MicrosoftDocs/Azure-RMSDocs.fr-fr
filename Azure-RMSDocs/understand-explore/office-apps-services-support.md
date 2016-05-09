---
# required metadata

title: Applications et services Office | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Applications et services Office
Les applications Office (telles que Word, Excel, PowerPoint et Outlook) et les services Office (tels qu’Exchange et SharePoint) pour utilisateurs finaux peuvent utiliser Microsoft Azure Rights Management pour protéger les données de votre organisation.

## Applications Office : Word, Excel, PowerPoint, Outlook
Ces applications prennent en charge la Gestion des droits de manière native grâce au service de Gestion des droits relatifs à l’information (IRM), et permettent aux utilisateurs d’appliquer une protection à un document enregistré ou à un message électronique à envoyer. Les utilisateurs peuvent appliquer des modèles ou choisir des paramètres personnalisés pour l’accès, les droits et les restrictions d’utilisation. 

Par exemple, ils peuvent configurer un fichier pour qu’il puisse être accessible uniquement par les personnes de votre organisation. Ils peuvent également déterminer si le fichier peut être modifié, s’il est disponible en lecture seule uniquement ou empêcher son impression. Pour les fichiers sensibles, ils peuvent configurer une date d’expiration (directement ou en appliquant un modèle) à laquelle le fichier ne sera plus accessible. Pour Outlook, les utilisateurs peuvent également choisir l’option **Ne pas transférer** pour éviter toute fuite de données.

## Exchange Online et Exchange Server
Quand vous utilisez Exchange Online ou Exchange Server, vous pouvez utiliser l’intégration de la Gestion des droits relatifs à l’information (IRM), laquelle propose des solutions supplémentaires de protection des informations :

-   **Exchange ActiveSync IRM** pour que les appareils mobiles puissent protéger des messages électroniques et utiliser des messages électroniques protégés.

-   Prise en charge par RMS d’ **Outlook Web App**, implémenté de manière similaire au client Outlook, pour que les utilisateurs puissent protéger des messages électroniques par des modèles ou en spécifiant des options individuelles, et qu’ils puissent lire et utiliser les messages électroniques protégés qui leur sont envoyés.

-   **Règles de protection** pour les clients Outlook qu’un administrateur configure pour appliquer automatiquement des modèles RMS aux messages électroniques envoyés à des destinataires spécifiés. Par exemple, quand des messages électroniques internes sont envoyés à votre service juridique, ils peuvent uniquement être lus par les membres du service juridique et ne peuvent pas être transférés. Les utilisateurs voient la protection appliquée au message électronique avant de l’envoyer et, par défaut, ils peuvent la supprimer s’ils décident qu’elle est inutile. Les messages électroniques sont chiffrés avant d’être envoyés. Pour plus d’informations, consultez [Règles de protection Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) et [Créer une règle de protection d’Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

-   **Règles de transport** qu’un administrateur configure pour appliquer automatiquement des modèles RMS aux messages électroniques en fonction de propriétés telles que l’expéditeur, le destinataire, l’objet du message et son contenu. Ces règles sont similaires par leur concept aux règles de protection, mais elles ne permettent pas aux utilisateurs de supprimer la protection, elles sont applicables à Outlook Web Access et aux messages électroniques envoyés par des appareils mobiles et elles ne chiffrent pas les messages avant leur envoi depuis le client. Pour plus d’informations, consultez [Créer une règle de protection de transport](https://technet.microsoft.com/library/dd302432.aspx) dans la bibliothèque Exchange.

-   **Stratégies de protection contre la perte de données (DLP)** qui contiennent des ensembles de conditions permettant de filtrer des messages électroniques et de prendre des mesures de prévention contre la perte de données pour le contenu confidentiel ou sensible (par exemple, les informations personnelles ou de carte de crédit). Vous pouvez utiliser des conseils de stratégie quand des données sensibles sont détectées, pour alerter les utilisateurs de l’éventuel besoin d’appliquer une protection des informations, en fonction des informations contenues dans le message électronique. Pour plus d’informations, consultez [Protection contre la perte de données](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

-   **Chiffrement de messages Office 365** qui utilise des règles de transport pour envoyer des messages électroniques chiffrés aux personnes extérieures à votre entreprise. Ces messages sont lus dans un navigateur doté d’une interface similaire à celle d’Outlook Web App. Vous pouvez personnaliser le texte de la clause d’exclusion de responsabilité et le texte d’en-tête dans les messages électroniques chiffrés de votre entreprise, et même ajouter son logo. Pour plus d’informations, consultez [Chiffrement de messages Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) sur le site web Office.

Si vous utilisez Exchange Server, vous pouvez utiliser les fonctionnalités de protection des informations avec [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] en déployant le connecteur RMS, qui joue le rôle de relais entre vos serveurs locaux et le service cloud RMS. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## SharePoint Online et SharePoint Server
Quand vous utilisez SharePoint Online ou SharePoint Server, vous pouvez utiliser l’intégration de la Gestion des droits relatifs à l’information (IRM), qui permet aux administrateurs de protéger des listes ou bibliothèques pour que, quand un utilisateur extrait un document, le fichier soit protégé afin que seules les personnes autorisées puissent l’afficher et l’utiliser conformément aux stratégies de protection des informations que vous spécifiez. Par exemple, le fichier peut être en lecture seule, vous pouvez désactiver la copie du texte, vous pouvez empêcher l’enregistrement d’une copie locale et l’impression du fichier.

Pour les listes et bibliothèques, la protection des informations est toujours appliquée par un administrateur, jamais un utilisateur final. Et elle est appliquée au niveau de la liste ou bibliothèque de tous les documents inclus dans le conteneur, plutôt qu’à des fichiers individuels.  Si vous utilisez SharePoint Online, les utilisateurs peuvent également appliquer l’IRM à leur bibliothèque OneDrive Entreprise.

Le service IRM doit d’abord être activé pour SharePoint. Ensuite, vous spécifiez la Gestion des droits relatifs à l’information pour une bibliothèque. Pour SharePoint Online et OneDrive Entreprise, les utilisateurs peuvent également spécifier la Gestion des droits relatifs à l’information pour leur bibliothèque OneDrive Entreprise. SharePoint n’utilise pas de modèle de stratégie de droits, même s’il existe des paramètres de configuration de SharePoint que vous pouvez sélectionner, qui correspondent étroitement aux paramètres que vous pouvez spécifier dans des modèles.

Si vous utilisez SharePoint Server, vous pouvez utiliser les fonctionnalités de protection des informations avec [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] en déployant le connecteur RMS, qui joue le rôle de relais entre vos serveurs locaux et le service cloud RMS. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> La Gestion des droits relatifs à l’information avec SharePoint est actuellement soumise à certaines limitations :
> 
> -   Vous ne pouvez pas utiliser les modèles personnalisés ou par défaut que vous gérez dans le portail Azure Classic.
> -   Les fichiers comportant une extension .PPDF pour les fichiers PDF protégés ne sont pas pris en charge. Les fichiers comportant une extension .PDF et protégés par RMS en mode natif sont pris en charge lorsque vous utilisez un lecteur PDF qui prend en charge RMS en mode natif.
> -   Office sur les appareils mobiles ne prenant pas encore en charge RMS, ces appareils doivent utiliser un navigateur pour afficher les fichiers protégés par RMS, qui sont en lecture seule.

Azure RMS applique des restrictions d’utilisation et un chiffrement de données aux documents téléchargés à partir de SharePoint, mais pas aux documents créés dans SharePoint ou chargés sur la bibliothèque. Pour plus d’informations sur la façon dont les documents sont protégés avant leur téléchargement, voir [Chiffrement de données dans OneDrive Entreprise et SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) dans la documentation SharePoint.

Pour plus d’informations sur l’utilisation d’Azure RMS avec SharePoint, voir la publication suivante sur le blog Office : [Nouveautés du service de Gestion des droits relatifs à l’information dans SharePoint et SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## Étapes suivantes

Pour voir comment d’autres applications et services prennent en charge Azure Rights Management, consultez [Comment les applications prennent en charge Azure Rights Management](applications-support.md).

<!--HONumber=Apr16_HO3-->


