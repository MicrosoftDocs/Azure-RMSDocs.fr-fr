---
title: Prise en charge d’Azure RMS d’Azure Information Protection par les programmes et services Office
description: Voici comment les programmes Office (comme Word et Outlook) et les services Office (Exchange et SharePoint) pour les utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les données de votre organisation.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/31/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 758fb47d41a4ca15e202fb5f18e3b94706bbb493
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164604"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Prise en charge d’Azure Rights Management par les programmes et services Office 

>***S’applique à** : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Concerne** : [Client d’étiquetage unifié AIP et client classique](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients).*

>[!NOTE] 
> Pour fournir une expérience client unifiée et homogène, le **client classique Azure Information Protection** et la **gestion des étiquettes** dans le portail Azure seront **dépréciés** à compter du **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Les programmes Office et les services Office pour utilisateurs finaux peuvent utiliser le service Azure Rights Management d’Azure Information Protection pour protéger les données de votre organisation. Ces programmes Office sont Word, Excel, PowerPoint et Outlook. Les services Office sont Exchange et Microsoft SharePoint. Les configurations Office prenant en charge le service Azure Rights Management utilisent souvent le terme **gestion des droits relatifs à l’information (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Applications Office : Word, Excel, PowerPoint, Outlook
Ces applications prennent en charge Azure Rights Management intégrées et permettent aux utilisateurs d’appliquer la protection à un document enregistré ou à un message électronique à envoyer. Les utilisateurs peuvent utiliser des modèles pour appliquer la protection. Autre possibilité pour Word, Excel et PowerPoint : les utilisateurs appliquent des paramètres personnalisés pour l’accès, les droits et les restrictions d’utilisation.

Par exemple, les utilisateurs peuvent configurer un document Word pour qu’il soit accessible seulement par des personnes de votre organisation. Vous pouvez contrôler si une feuille de calcul Excel peut être modifiée ou limitée à la lecture seule, ou l’empêcher d’être imprimée. Pour les fichiers ayant des contraintes de temps, un délai d’expiration peut être configuré, au terme duquel le fichier ne sera plus accessible. Cette configuration peut être faite directement par les utilisateurs ou en appliquant un modèle de protection. Pour Outlook, les utilisateurs peuvent également choisir l’option **Ne pas transférer** pour éviter toute fuite de données.

Si vous êtes prêt à configurer des applications Office, consultez [applications Office : configuration pour les clients](configure-office-apps.md).

Pour les problèmes connus pertinents, consultez [problèmes connus liés aux AIP dans les applications Office](known-issues.md#aip-known-issues-in-office-applications).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online et Exchange Server
Quand vous utilisez Exchange Online ou Exchange Server, vous pouvez configurer des options pour Azure Information Protection. Cette configuration permet à Exchange d’offrir les solutions de protection suivantes :

-   **Exchange ActiveSync IRM** pour que les appareils mobiles puissent protéger des messages électroniques et utiliser des messages électroniques protégés.

-   Prise en charge de la protection des e-mails pour **Outlook sur le web**, qui est implémentée de façon similaire à celle du client Outlook. Cette configuration permet aux utilisateurs de protéger des e-mails à l’aide de modèles de protection ou en spécifiant des options. Les utilisateurs peuvent lire et utiliser les e-mails protégés qui leur sont envoyés.

-   **Règles de protection** pour les clients Outlook qu’un administrateur configure afin d’appliquer automatiquement des modèles de protection et des options aux e-mails envoyés à des destinataires spécifiés. Par exemple, quand des messages électroniques internes sont envoyés à votre service juridique, ils peuvent uniquement être lus par les membres du service juridique et ne peuvent pas être transférés. Les utilisateurs voient la protection appliquée à l’e-mail avant de l’envoyer. Ils peuvent aussi, par défaut, supprimer cette protection s’ils décident qu’elle est inutile. Les messages électroniques sont chiffrés avant d’être envoyés. Pour plus d’informations, voir [Règles de protection Outlook](/exchange/outlook-protection-rules-exchange-2013-help) et [Créer une règle de protection d’Outlook](/exchange/create-an-outlook-protection-rule-exchange-2013-help) dans la bibliothèque Exchange.

-   **Règles de flux de courrier** qu’un administrateur configure pour appliquer automatiquement des modèles de protection ou des options aux e-mails. Ces règles sont basées sur des propriétés, comme l’expéditeur, le destinataire, l’objet du message et le contenu. Ces règles sont similaires par leur concept aux règles de protection, mais elles ne permettent pas aux utilisateurs de supprimer la protection, car celle-ci est définie par le service Exchange plutôt que par le client. Étant donné que la protection est définie par le service, peu importe l’appareil ou le système d’exploitation dont disposent les utilisateurs. Pour plus d’informations, consultez [Règles de flux de courrier (règles de transport) dans Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) et [Créer une règle de protection de transport](/exchange/create-a-transport-protection-rule-exchange-2013-help) pour Exchange sur site.

-   **Stratégies de protection contre la perte de données (DLP)** qui contiennent des ensembles de conditions permettant de filtrer des e-mails et de prendre des mesures de prévention contre la perte de données pour le contenu confidentiel ou sensible. L’une des actions que vous pouvez spécifier consiste à appliquer le chiffrement comme protection, en spécifiant l’une des options ou l’un des modèles de protection. Vous pouvez utiliser des conseils de stratégie quand des données sensibles sont détectées, pour alerter les utilisateurs qu’il peut être nécessaire d’appliquer une protection. Pour plus d’informations, consultez [Protection contre la perte de données](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) dans la documentation Exchange Online.

-   **Chiffrement de message** qui prend en charge l’envoi d’un message électronique protégé et de documents Office protégés en tant que pièces jointes à une adresse de messagerie sur n’importe quel appareil. Pour les comptes d’utilisateur sans Azure AD, une expérience web prend en charge les fournisseurs d’identité sociale ou un code secret à usage unique. Pour plus d’informations, consultez [configurer de nouvelles fonctionnalités de chiffrement de Message Microsoft 365 basées sur Azure information protection](/microsoft-365/compliance/set-up-new-message-encryption-capabilities) à partir de la documentation de Microsoft 365. Pour vous aider à trouver des informations supplémentaires relatives à cette configuration, consultez [Microsoft 365 le chiffrement des messages](/microsoft-365/compliance/ome).

Si vous utilisez Exchange local, vous pouvez utiliser les fonctionnalités IRM avec le service Azure Rights Management en déployant le connecteur Azure Rights Management. Ce connecteur fait office de relais entre vos serveurs locaux et le service Azure Rights Management.

Pour plus d’informations sur les options de messagerie que vous pouvez utiliser pour protéger les e-mails, consultez [option ne pas transférer pour](configure-usage-rights.md#do-not-forward-option-for-emails) les e-mails et [option chiffrer uniquement pour les e-mails](configure-usage-rights.md#encrypt-only-option-for-emails).

Si vous êtes prêt à configurer Exchange pour protéger les e-mails :

- Pour Exchange Online, consultez [Exchange Online : configuration de la Gestion des droits relatifs à l’information (IRM)](configure-office365.md#exchangeonline-irm-configuration).

- Pour Exchange sur site, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

Pour plus d'informations, consultez les pages suivantes :

- **Client d’étiquetage unifié**. Configurez les étiquettes de sensibilité et les stratégies d’étiquetage dans le centre d’administration d’étiquetage, y compris le centre de sécurité Microsoft 365, le centre de conformité des Microsoft 365, ou le centre de conformité Microsoft 365 Security &. Pour plus d’informations, consultez la [documentation Microsoft 365](/microsoft-365/compliance/sensitivity-labels).

- **Client classique**. Configurez les modèles de protection dans le Portail Azure. Pour plus d’informations, consultez [Configuration et gestion des modèles pour Azure Information Protection](configure-policy-templates.md).


## <a name="sharepoint-in-microsoft-365-and-sharepoint-server"></a>SharePoint dans Microsoft 365 et SharePoint Server

Lorsque vous utilisez SharePoint dans Microsoft 365 ou SharePoint Server, vous pouvez protéger des documents à l’aide de la fonctionnalité de gestion des droits relatifs à l’information (IRM) de SharePoint. Cette fonctionnalité permet aux administrateurs de protéger des listes ou des bibliothèques pour que le fichier qui est téléchargé quand un utilisateur extrait un document soit protégé. Cela signifie que seules les personnes autorisées peuvent afficher et utiliser ce fichier conformément aux stratégies de protection des informations que vous spécifiez. Par exemple, le fichier peut être en lecture seule, vous pouvez désactiver la copie du texte, vous pouvez empêcher l'enregistrement d'une copie locale et l'impression du fichier.

Les documents Word, PowerPoint, Excel et PDF prennent en charge cette protection IRM de SharePoint. Par défaut, la protection est limitée à la personne qui télécharge le document. Vous pouvez modifier cette valeur par défaut avec une option de configuration nommée **Autoriser la protection de groupe**, qui étend la protection à un groupe que vous spécifiez. Vous pouvez, par exemple, spécifier un groupe qui a l’autorisation de modifier des documents dans la bibliothèque, afin que le même groupe d’utilisateurs puisse modifier le document en dehors de SharePoint, quel que soit l’utilisateur qui a téléchargé le document. Ou, vous pouvez spécifier un groupe qui ne dispose pas d’autorisations dans SharePoint, mais dont les utilisateurs ont besoin d’accéder au document en dehors de SharePoint. Pour les listes et les bibliothèques SharePoint, cette protection est toujours configurée par un administrateur, jamais par un utilisateur final. Vous définissez les autorisations au niveau du site, puis ces autorisations sont, par défaut, héritées par les listes ou les bibliothèques de ce site. Si vous utilisez SharePoint dans Microsoft 365, les utilisateurs peuvent également configurer leur bibliothèque Microsoft OneDrive pour la protection IRM.

Pour effectuer un contrôle affiné, vous pouvez configurer une liste ou une bibliothèque du site pour qu’elle n’hérite plus des autorisations de son parent. Vous pouvez ensuite configurer des autorisations IRM au niveau de la liste ou de la bibliothèque. Ces autorisations sont alors désignées comme « autorisations uniques ». Notez toutefois que les autorisations sont toujours définies au niveau du conteneur. Vous ne pouvez donc pas les définir pour les fichiers de façon individuelle. 

Le service IRM doit d'abord être activé pour SharePoint. Ensuite, vous spécifiez les autorisations IRM pour une bibliothèque. Pour SharePoint et OneDrive, les utilisateurs peuvent également spécifier des autorisations IRM pour leur bibliothèque OneDrive. SharePoint n’utilise pas de modèle de stratégie de droits, même s’il existe des paramètres de configuration de SharePoint que vous pouvez sélectionner, qui correspondent à certains paramètres que vous pouvez spécifier dans les modèles.

Si vous utilisez SharePoint Server, vous pouvez utiliser cette protection IRM en déployant le connecteur Azure Rights Management. Ce connecteur fait office de relais entre vos serveurs locaux et le service cloud Rights Management. Pour plus d’informations, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).

> [!NOTE]
> Il existe certaines limitations lorsque vous utilisez l’IRM de SharePoint :
> 
> - Vous ne pouvez pas utiliser les modèles de protection personnalisés ou par défaut que vous gérez dans le portail Azure. 
> 
> - Les fichiers qui ont une extension .ppdf (pour « fichiers PDF protégés ») ne sont pas pris en charge. Pour plus d’informations sur l’affichage des documents PDF protégés, consultez [Lecteurs PDF protégés pour Microsoft Information Protection](./rms-client/protected-pdf-readers.md).
> 
> - La co-création, c’est-à-dire quand plusieurs personnes modifient un document simultanément, n’est pas prise en charge. Pour modifier un document dans une bibliothèque protégée par IRM, vous devez tout d’abord extraire le document et le télécharger, puis le modifier dans votre application Office. Par conséquent, une seule personne peut modifier le document à la fois.

Pour les bibliothèques qui ne sont pas protégées par IRM, si vous appliquez la protection uniquement à un fichier que vous chargez ensuite sur SharePoint ou OneDrive, les éléments suivants ne fonctionnent pas avec ce fichier : co-création, Office pour le Web, recherche, aperçu du document, miniature, eDiscovery et protection contre la perte de données (DLP).

> [!IMPORTANT]
> Vous pouvez utiliser SharePoint IRM conjointement avec les étiquettes de sensibilité qui appliquent la protection. Lorsque vous utilisez les deux fonctionnalités ensemble, le comportement change pour les fichiers protégés. Pour plus d’informations, consultez [activer les étiquettes de sensibilité pour les fichiers Office dans SharePoint et OneDrive](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

Quand vous utilisez la protection IRM SharePoint, le service Azure Rights Management applique des restrictions d’utilisation et un chiffrement de données aux documents téléchargés à partir de SharePoint, mais pas aux documents créés initialement dans SharePoint ou chargés dans la bibliothèque. Pour plus d’informations sur la façon dont les documents sont protégés avant leur téléchargement, consultez [chiffrement des données dans OneDrive et SharePoint](/microsoft-365/compliance/data-encryption-in-odb-and-spo?redirectSourcePath=%252fen-us%252farticle%252f6501b5ef-6bf7-43df-b60d-f65781847d6c) dans la documentation SharePoint.

Bien qu’il ne soit plus nouveau, le billet suivant du blog Microsoft 365 contient des informations supplémentaires que vous pouvez trouver utiles : [nouveautés avec les informations Rights Management dans SharePoint](https://www.microsoft.com/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

Pour obtenir les modifications à venir, consultez [mises à jour de la sécurité, de l’administration et de la migration SharePoint](https://techcommunity.microsoft.com/t5/Microsoft-SharePoint-Blog/Updates-to-SharePoint-security-administration-and-migration/ba-p/549585).

Si vous êtes prêt à configurer SharePoint pour l’IRM :

- Pour SharePoint dans Microsoft 365, consultez [SharePoint dans Microsoft 365 et OneDrive : configuration d’IRM](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration).

- Pour SharePoint Server, consultez [Déploiement du connecteur Azure Rights Management](deploy-rms-connector.md).


## <a name="next-steps"></a>Étapes suivantes

Si vous avez Microsoft 365, vous souhaiterez peut-être examiner les [solutions de protection de fichiers dans Microsoft 365](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect), qui fournit des fonctionnalités recommandées pour la protection des fichiers dans Microsoft 365.

Pour voir comment d’autres applications et services prennent en charge le service Azure Rights Management d’Azure Information Protection, consultez [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md).

Si vous êtes prêt à démarrer le déploiement, ce qui comprend la configuration de ces applications et services, consultez la feuille [de route pour le déploiement d’AIP pour la classification, l’étiquetage et la protection](deployment-roadmap-classify-label-protect.md).