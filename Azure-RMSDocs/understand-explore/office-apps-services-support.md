---
title: "Prise en charge d’Azure RMS d’Azure Information Protection par les programmes et services Office"
description: "Voici comment les programmes Office (comme Word et Outlook) et les services Office (Exchange et SharePoint) pour les utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les données de votre organisation."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5e4d753c6c58394c257466269c5a4f50df6c6fc4
ms.sourcegitcommit: 869e42f35a851c412164a71b1f657621af07b2f5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/02/2017
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Prise en charge d’Azure Rights Management par les programmes et services Office 

>*S’applique à : Azure Information Protection, Office 365*

Les programmes Office et les services Office pour utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les données de votre organisation. Ces programmes Office sont Word, Excel, PowerPoint et Outlook. Les services Office sont Exchange et SharePoint. Les configurations Office prenant en charge le service Azure Rights Management utilisent souvent le terme **gestion des droits relatifs à l’information (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Programmes Office : Word, Excel, PowerPoint, Outlook
Ces programmes prennent en charge la Gestion des droits de façon native et permettent aux utilisateurs d’appliquer la protection à un document enregistré ou à un e-mail à envoyer. Les utilisateurs peuvent utiliser des modèles pour appliquer la protection. Autre possibilité pour Word, Excel et PowerPoint : les utilisateurs appliquent des paramètres personnalisés pour l’accès, les droits et les restrictions d’utilisation. 

Par exemple, les utilisateurs peuvent configurer un document Word pour qu’il soit accessible seulement par des personnes de votre organisation. Vous pouvez contrôler si une feuille de calcul Excel peut être modifiée ou limitée à la lecture seule, ou l’empêcher d’être imprimée. Pour les fichiers ayant des contraintes de temps, un délai d’expiration peut être configuré, au terme duquel le fichier ne sera plus accessible. Cette configuration peut être faite directement par les utilisateurs ou en appliquant un modèle. Pour Outlook, les utilisateurs peuvent également choisir l’option **Ne pas transférer** pour éviter toute fuite de données.

En plus de la prise en charge native par Office d’Azure Rights Management, ces programmes prennent en charge la barre Azure Information Protection qui est installée avec le [client Azure Information Protection](../rms-client/aip-client.md). Cette barre affiche des étiquettes permettant aux utilisateurs d’appliquer automatiquement une protection à des documents et des e-mails qui contiennent des données sensibles.

Si vous êtes prêt à configurer des programmes Office et le client Azure Information Protection :

- Pour configurer des programmes Office, consultez [Applications Office : configuration pour les clients](../deploy-use/configure-office-apps.md).

- Pour installer et configurer le client Azure Information Protection, consultez [Client Azure Information Protection : installation et configuration pour les clients](../deploy-use/configure-client.md).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online et Exchange Server
Quand vous utilisez Exchange Online ou Exchange Server, vous pouvez configurer des options de gestion des droits relatifs à l’information qui prennent en charge Azure Rights Management. Cette configuration permet à Exchange d’offrir les solutions de protection suivantes :

-   **Exchange ActiveSync IRM** pour que les appareils mobiles puissent protéger les e-mails et utiliser des e-mails protégés.

-   Prise en charge de la protection des e-mails pour **Outlook sur le web**, qui est implémentée de façon similaire à celle du client Outlook. Cette configuration permet aux utilisateurs de protéger des e-mails à l’aide de modèles ou en spécifiant des options individuelles. Les utilisateurs peuvent lire et utiliser les e-mails protégés qui leur sont envoyés.

-   **Règles de protection** pour les clients Outlook qu’un administrateur configure afin d’appliquer automatiquement des modèles de protection aux e-mails envoyés à des destinataires spécifiés. Par exemple, quand des e-mails internes sont envoyés à votre service juridique, ils peuvent uniquement être lus par les membres du service juridique et ne peuvent pas être transférés. Les utilisateurs voient la protection appliquée à l’e-mail avant de l’envoyer. Ils peuvent aussi, par défaut, supprimer cette protection s’ils décident qu’elle est inutile. Les e-mails sont chiffrés avant d’être envoyés. Pour plus d’informations, consultez [Règles de protection Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) et [Créer une règle de protection d’Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) dans la bibliothèque Exchange.

-   **Règles de transport** qu’un administrateur configure pour appliquer automatiquement des modèles de protection aux e-mails. Ces règles sont basées sur des propriétés, comme l’expéditeur, le destinataire, l’objet du message et le contenu. Ces règles sont similaires par leur concept aux règles de protection, mais elles ne permettent pas aux utilisateurs de supprimer la protection. Les règles peuvent être appliquées à Outlook sur le web et aux e-mails envoyés par des appareils mobiles. De plus, ces règles ne chiffrent pas les e-mails avant leur envoi à partir du client. Pour plus d’informations, consultez [Créer une règle de protection de transport](https://technet.microsoft.com/library/dd302432.aspx) dans la bibliothèque Exchange.

-   **Stratégies de protection contre la perte de données (DLP)** qui contiennent des ensembles de conditions permettant de filtrer des e-mails et de prendre des mesures de prévention contre la perte de données pour le contenu confidentiel ou sensible. Les informations de carte de crédit ou des informations personnelles sont des exemples de contenu confidentiel ou sensible. Vous pouvez utiliser des conseils de stratégie quand des données sensibles sont détectées, pour alerter les utilisateurs qu’il peut être nécessaire d’appliquer une protection. Pour plus d’informations, consultez [Protection contre la perte de données](https://technet.microsoft.com/library/jj150527(v=exchg.160).aspx) dans la bibliothèque Exchange.

-   **Chiffrement de messages Office 365** qui utilise des règles de transport pour envoyer des e-mails chiffrés aux personnes extérieures à votre entreprise. Ces messages sont lus dans un navigateur doté d’une interface similaire à celle d’Outlook sur le web. Vous pouvez personnaliser le texte de la clause d’exclusion de responsabilité et le texte d’en-tête dans les e-mails chiffrés de votre entreprise, et même ajouter son logo. Pour plus d’informations, consultez [Chiffrement de messages Office 365](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx) sur le site web Office.

Si vous utilisez Exchange local, vous pouvez utiliser les fonctionnalités IRM avec le service Azure Rights Management en déployant le connecteur Azure Rights Management. Ce connecteur fait office de relais entre vos serveurs locaux et le service Azure Rights Management.

Si vous êtes prêt à configurer Exchange pour l’IRM :

- Pour Exchange Online, consultez [Exchange Online : configuration de la Gestion des droits relatifs à l’information (IRM)](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Pour Exchange sur site, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online et SharePoint Server

Si vous utilisez SharePoint Online ou SharePoint Server, vous pouvez protéger vos documents à l’aide de la fonctionnalité Gestion des droits relatifs à l’information (IRM) de SharePoint. Cette fonctionnalité permet aux administrateurs de protéger des listes ou des bibliothèques pour que le fichier qui est téléchargé quand un utilisateur extrait un document soit protégé. Cela signifie que seules les personnes autorisées peuvent afficher et utiliser ce fichier conformément aux stratégies de protection des informations que vous spécifiez. Par exemple, le fichier peut être en lecture seule, vous pouvez désactiver la copie du texte, vous pouvez empêcher l’enregistrement d’une copie locale et l’impression du fichier.

Les documents Word, PowerPoint, Excel et PDF prennent en charge cette protection IRM de SharePoint. Par défaut, la protection est limitée à la personne qui télécharge le document. Vous pouvez changer ce comportement par défaut avec une option de configuration qui étend la protection à tous les utilisateurs qui ont accès au document sur SharePoint, ou à un groupe que vous spécifiez.

Pour les listes et les bibliothèques SharePoint, cette protection est toujours configurée par un administrateur, jamais par un utilisateur final. Vous définissez les autorisations au niveau du site, puis ces autorisations sont, par défaut, héritées par les listes ou les bibliothèques de ce site. Si vous utilisez SharePoint Online, les utilisateurs peuvent également configurer leur bibliothèque OneDrive Entreprise avec la protection IRM.

Pour effectuer un contrôle affiné, vous pouvez configurer une liste ou une bibliothèque du site pour qu’elle n’hérite plus des autorisations de son parent. Vous pouvez ensuite configurer des autorisations IRM au niveau de la liste ou de la bibliothèque. Ces autorisations sont alors désignées comme « autorisations uniques ». Notez toutefois que les autorisations sont toujours définies au niveau du conteneur. Vous ne pouvez donc pas les définir pour les fichiers de façon individuelle. 

Le service IRM doit d’abord être activé pour SharePoint. Ensuite, vous spécifiez les autorisations IRM pour une bibliothèque. Pour SharePoint Online et OneDrive Entreprise, les utilisateurs peuvent également spécifier des autorisations IRM pour leur bibliothèque OneDrive Entreprise. SharePoint n’utilise pas de modèle de stratégie de droits, même s’il existe des paramètres de configuration de SharePoint que vous pouvez sélectionner, qui correspondent à certains paramètres que vous pouvez spécifier dans les modèles.

Si vous utilisez SharePoint Server, vous pouvez utiliser cette protection IRM en déployant le connecteur Azure Rights Management. Ce connecteur fait office de relais entre vos serveurs locaux et le service cloud Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Quand vous utilisez la protection IRM de SharePoint, certaines limitations s’appliquent :
> 
> - Vous ne pouvez pas utiliser les modèles personnalisés ou par défaut que vous gérez dans le portail Azure. 
> 
> - Les fichiers qui ont une extension .ppdf (pour « fichiers PDF protégés ») ne sont pas pris en charge. Les fichiers qui ont une extension .PDF et qui ont été protégés par Rights Management de façon native sont pris en charge quand vous utilisez un lecteur PDF qui prend en charge Rights Management de façon native.
> 
> - Si vous protégez un fichier que vous chargez ensuite dans une bibliothèque SharePoint ou OneDrive, les fonctionnalités suivantes ne sont pas opérationnelles avec ce fichier : co-édition, Office Online, recherche, aperçu du document, miniature et eDiscovery.

Quand vous utilisez la protection IRM SharePoint, le service Azure Rights Management applique des restrictions d’utilisation et un chiffrement de données aux documents téléchargés à partir de SharePoint, mais pas aux documents créés initialement dans SharePoint ou chargés dans la bibliothèque. Pour plus d’informations sur la façon dont les documents sont protégés avant leur téléchargement, voir [Chiffrement de données dans OneDrive Entreprise et SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) dans la documentation SharePoint.

Le billet de blog Office [Nouveautés en matière de gestion des droits relatifs à l’information dans SharePoint et SharePoint Online](https://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) n’est pas nouveau, mais il contient des informations complémentaires qui peuvent vous être utiles.

Si vous êtes prêt à configurer SharePoint pour l’IRM :

- Pour SharePoint Online, consultez [SharePoint Online et OneDrive Entreprise : configuration de la Gestion des droits relatifs à l’information (IRM)](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration).

- Pour SharePoint Server, consultez [Déploiement du connecteur Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="next-steps"></a>Étapes suivantes

Si vous avez Office 365, consultez [Solutions de protection des fichiers dans Office 365](https://technet.microsoft.com/library/dn919927.aspx#BKMK_O365fileprotect), qui fournit des fonctionnalités recommandées pour la protection des fichiers dans Office 365.

Pour voir comment d’autres applications et services prennent en charge le service Azure Rights Management d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

Si vous êtes prêt à commencer le déploiement, qui comprend la configuration de ces applications et services, consultez [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]