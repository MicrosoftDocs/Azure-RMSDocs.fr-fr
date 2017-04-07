---
title: "Utiliser des applications et services Office avec Azure Information Protection"
description: "Comment les applications Office (telles que Word, Excel, PowerPoint et Outlook) et les services Office (tels qu’Exchange et SharePoint) pour utilisateurs finaux peuvent utiliser le service Azure Rights Management pour protéger les données de votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9fe4e6173f864711009479e77ff162c307c750e5
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="office-applications-and-services"></a>Applications et services Office

>*S’applique à : Azure Information Protection, Office 365*

Les applications Office (telles que Word, Excel, PowerPoint et Outlook) et les services Office (tels qu’Exchange et SharePoint) pour utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les données de votre organisation.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Applications Office : Word, Excel, PowerPoint, Outlook
Ces applications prennent en charge la Gestion des droits de manière native grâce au service de Gestion des droits relatifs à l’information (IRM), et permettent aux utilisateurs d’appliquer une protection à un document enregistré ou à un message électronique à envoyer. Les utilisateurs peuvent appliquer des modèles ou, pour Word, Excel et PowerPoint, choisir des paramètres personnalisés pour l’accès, les droits et les restrictions d’utilisation. 

Par exemple, ils peuvent configurer un document Word pour qu’il puisse être accessible uniquement par les personnes de votre organisation. Ils peuvent également déterminer si une feuille de calcul Excel peut être modifiée, si elle est disponible en lecture seule uniquement ou empêcher son impression. Pour les fichiers sensibles, ils peuvent configurer une date d’expiration (directement ou en appliquant un modèle) à laquelle le fichier ne sera plus accessible. Pour Outlook, les utilisateurs peuvent choisir l’option **Ne pas transférer** pour éviter toute fuite de données, en plus de choisir un modèle.

Outre la prise en charge native des droits IRM, ces applications prennent en charge la barre Azure Information Protection qui est installée avec le [client Azure Information Protection](../rms-client/aip-client.md ). Cette barre affiche des étiquettes permettant aux utilisateurs d’appliquer automatiquement et en toute simplicité la protection Rights Management à des documents et des e-mails qui contiennent des données sensibles.

## <a name="exchange-online-and-exchange-server"></a>Exchange Online et Exchange Server
Quand vous utilisez Exchange Online ou Exchange Server, vous pouvez utiliser l’intégration de la Gestion des droits relatifs à l’information (IRM), laquelle propose des solutions supplémentaires de protection des informations :

-   **Exchange ActiveSync IRM** pour que les appareils mobiles puissent protéger des messages électroniques et utiliser des messages électroniques protégés.

-   Prise en charge par RMS d’ **Outlook Web App**, implémenté de manière similaire au client Outlook, pour que les utilisateurs puissent protéger des messages électroniques par des modèles ou en spécifiant des options individuelles, et qu’ils puissent lire et utiliser les messages électroniques protégés qui leur sont envoyés.

-   **Règles de protection** pour les clients Outlook qu’un administrateur configure pour appliquer automatiquement des modèles Rights Management aux messages électroniques envoyés à des destinataires spécifiés. Par exemple, quand des messages électroniques internes sont envoyés à votre service juridique, ils peuvent uniquement être lus par les membres du service juridique et ne peuvent pas être transférés. Les utilisateurs voient la protection appliquée au message électronique avant de l’envoyer et, par défaut, ils peuvent la supprimer s’ils décident qu’elle est inutile. Les messages électroniques sont chiffrés avant d’être envoyés. Pour plus d’informations, consultez [Règles de protection Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) et [Créer une règle de protection d’Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

-   **Règles de transport** qu’un administrateur configure pour appliquer automatiquement des modèles Rights Management aux messages électroniques en fonction de propriétés telles que l’expéditeur, le destinataire, l’objet du message et son contenu. Ces règles sont similaires par leur concept aux règles de protection, mais elles ne permettent pas aux utilisateurs de supprimer la protection, elles sont applicables à Outlook Web Access et aux messages électroniques envoyés par des appareils mobiles et elles ne chiffrent pas les messages avant leur envoi depuis le client. Pour plus d’informations, consultez [Créer une règle de protection de transport](https://technet.microsoft.com/library/dd302432.aspx) dans la bibliothèque Exchange.

-   **Stratégies de protection contre la perte de données (DLP)** qui contiennent des ensembles de conditions permettant de filtrer des messages électroniques et de prendre des mesures de prévention contre la perte de données pour le contenu confidentiel ou sensible (par exemple, les informations personnelles ou de carte de crédit). Vous pouvez utiliser des conseils de stratégie quand des données sensibles sont détectées, pour alerter les utilisateurs de l’éventuel besoin d’appliquer une protection des informations, en fonction des informations contenues dans le message électronique. Pour plus d’informations, consultez [Protection contre la perte de données](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

-   **Chiffrement de messages Office 365** qui utilise des règles de transport pour envoyer des messages électroniques chiffrés aux personnes extérieures à votre entreprise. Ces messages sont lus dans un navigateur doté d’une interface similaire à celle d’Outlook Web App. Vous pouvez personnaliser le texte de la clause d’exclusion de responsabilité et le texte d’en-tête dans les messages électroniques chiffrés de votre entreprise, et même ajouter son logo. Pour plus d’informations, consultez [Chiffrement de messages Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) sur le site web Office.

Si vous utilisez Exchange Server, vous pouvez utiliser les fonctionnalités de protection des informations avec le service Azure Rights Management en déployant le connecteur RMS, qui fait office de relais entre vos serveurs locaux et le service Azure Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online et SharePoint Server
Quand vous utilisez SharePoint Online ou SharePoint Server, vous pouvez utiliser l’intégration de la Gestion des droits relatifs à l’information (IRM), qui permet aux administrateurs de protéger des listes ou bibliothèques pour que, quand un utilisateur extrait un document, le fichier soit protégé afin que seules les personnes autorisées puissent l’afficher et l’utiliser conformément aux stratégies de protection des informations que vous spécifiez. Par exemple, le fichier peut être en lecture seule, vous pouvez désactiver la copie du texte, vous pouvez empêcher l’enregistrement d’une copie locale et l’impression du fichier.

Pour les listes et les bibliothèques, la protection des informations est toujours appliquée par un administrateur, jamais un utilisateur final. Et elle est appliquée au niveau de la liste ou bibliothèque de tous les documents inclus dans le conteneur, plutôt qu’à des fichiers individuels.  Si vous utilisez SharePoint Online, les utilisateurs peuvent également appliquer l’IRM à leur bibliothèque OneDrive Entreprise.

Le service IRM doit d’abord être activé pour SharePoint. Ensuite, vous spécifiez la Gestion des droits relatifs à l’information pour une bibliothèque. Pour SharePoint Online et OneDrive Entreprise, les utilisateurs peuvent également spécifier la Gestion des droits relatifs à l’information pour leur bibliothèque OneDrive Entreprise. SharePoint n’utilise pas de modèle de stratégie de droits, même s’il existe des paramètres de configuration de SharePoint que vous pouvez sélectionner, qui correspondent étroitement aux paramètres que vous pouvez spécifier dans des modèles.

Si vous utilisez SharePoint Server, vous pouvez utiliser les fonctionnalités de protection des informations avec le service Azure Rights Management en déployant le connecteur RMS, qui fait office de relais entre vos serveurs locaux et le service cloud Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> La Gestion des droits relatifs à l’information avec SharePoint est actuellement soumise à certaines limitations :
> 
> - Vous ne pouvez pas utiliser les modèles personnalisés ou par défaut que vous gérez dans le portail Azure Classic.
> - Les fichiers comportant une extension .PPDF pour les fichiers PDF protégés ne sont pas pris en charge. Les fichiers comportant une extension .PDF et protégés par Rights Management en mode natif sont pris en charge lorsque vous utilisez un lecteur PDF qui prend en charge Rights Management en mode natif.


Azure Rights Management applique des restrictions d’utilisation et un chiffrement de données aux documents téléchargés à partir de SharePoint, mais pas aux documents créés dans SharePoint ou chargés sur la bibliothèque. Pour plus d’informations sur la façon dont les documents sont protégés avant leur téléchargement, voir [Chiffrement de données dans OneDrive Entreprise et SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) dans la documentation SharePoint.

Pour plus d’informations sur l’utilisation du service Azure Rights Management avec SharePoint, consultez la publication suivante sur le blog Office : [Nouveautés en matière de gestion des droits relatifs à l’information dans SharePoint et SharePoint Online](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/).

## <a name="next-steps"></a>Étapes suivantes

Pour voir comment d’autres applications et services prennent en charge le service Azure Rights Management d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]