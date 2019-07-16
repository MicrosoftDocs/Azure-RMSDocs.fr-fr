---
title: Terminologie liée à Azure Information Protection
description: Vous ne comprenez pas un mot, une expression ou un acronyme lié à Microsoft Azure Information Protection ? Recherchez ici la définition de termes et d’abréviations propres à Azure Information Protection, ou qui ont un sens particulier dans le contexte de ce service.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: 731870990e5fd852cbc0ac03a988710d1cf52fbf
ms.sourcegitcommit: e730f897452fcb0ca1003c6b86f6e65678d0ec57
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67885596"
---
# <a name="terminology-for-azure-information-protection"></a>Terminologie liée à Azure Information Protection

>*S’applique à : [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Vous ne comprenez pas un mot, une expression ou un acronyme lié à Microsoft Azure Information Protection ? Recherchez ici la définition de termes et d’abréviations propres à Azure Information Protection, ou qui ont un sens particulier dans le contexte de ce service.

|Terme|Définition|
|--------|--------------|
|AADRM|Nom du premier module PowerShell pour le service de protection (Azure Rights Management), dérivé de l’abréviation non officielle d’Azure Rights Management lorsqu’il a été nommé précédemment (Windows) Azure Active Directory Rights Management. Ce module PowerShell est maintenant remplacé par le module AIPService.|
|activer|Pour activer le service de protection (Azure Rights Management) afin qu’une organisation puisse protéger ses documents et ses e-mails. Cette action active également les fonctionnalités IRM dans Exchange Online et SharePoint Online.|
|Active Directory Rights Management Services|Souvent abrégé *AD RMS*.<br /><br />Rôle Windows Server qui assure une protection par gestion des droits en utilisant le chiffrement et des stratégies pour mieux sécuriser les documents, les fichiers et les e-mails.|
|AD RMS|Voir *Services Active Directory Rights Management*.|
|AIPService|Nom actuel du module PowerShell pour le service de protection, qui remplace par l’ancien module AADRM.|
AzureInformationProtection|Nom du module PowerShell pour le client Azure Information Protection (Classic) et le client d’étiquetage unifié Azure Information Protection.
|Azure Information Protection|Service cloud qui utilise des étiquettes pour classifier et protéger les documents et e-mails. Azure Rights Management offre une protection à l’aide de stratégies de chiffrement, d’identité et d’autorisation.|
Client Azure Information Protection (classique)|Parfois abrégé en *client classique*.<br /><br />Le côté client d’origine de Azure Information Protection qui permet aux utilisateurs, aux administrateurs et aux services d’utiliser les étiquettes et les paramètres de votre stratégie de Azure Information Protection. Désormais remplacé par le client d’étiquetage unifié Azure Information Protection.|
|Étiquette Azure Information Protection|Élément qui applique toujours une valeur de classification aux documents et aux e-mails, et qui peut aussi les protéger. Quand une étiquette est appliquée, les informations de l’étiquette sont stockées dans les métadonnées pour que les applications et les services puissent les lire, et éventuellement agir sur celles-ci.|
|Stratégie Azure Information Protection|Configuration définie par l’administrateur pour les clients et services qui utilisent les paramètres de stratégie et les étiquettes Azure Information Protection.|
|Scanneur Azure Information Protection|Service qui s’exécute sur Windows Server et vous permet de découvrir, classifier et protéger des documents sur les dossiers locaux, les partages réseau et les bibliothèques et sites SharePoint Server.|
|Client d’étiquetage unifié Azure Information Protection|Parfois abrégé en *client d’étiquetage unifié*.<br /><br />client des ordinateurs Windows permettant aux utilisateurs, aux administrateurs et aux services d’utiliser les étiquettes de confidentialité et les paramètres de stratégie provenant du Centre de sécurité et conformité Office 365, du Centre de sécurité Microsoft 365 et du Centre de conformité Microsoft 365. Remplace le client Azure Information Protection (classique).|
|Azure RMS|Voir *Azure Rights Management*.|
|Visionneuse Azure Information Protection|Application qui s’exécute sur des ordinateurs Windows et des appareils mobiles pour afficher les fichiers protégés.|
|Gestion des droits Azure|Souvent abrégé *Azure RMS*.<br /><br />Service Azure utilisé par Azure Information Protection qui recourt au chiffrement et à des stratégies, à des fins de sécurisation des documents, des fichiers et des e-mails.  Également appelé *service Rights Management Azure*. Les noms précédents étaient les suivants :<br /><br />- *Windows Azure Active Directory Rights Management* : Souvent abrégé en service Windows Azure AD Rights Management.<br /><br />- *RMS Online* : Nom proposé à l’origine, que vous pouvez parfois voir apparaître dans les messages d’erreur et les entrées du fichier journal.|
|modèle par défaut|Modèle de protection qui est automatiquement créé pour vous lorsque vous obtenez un abonnement pour Azure Information Protection, afin que vous puissiez immédiatement commencer à protéger les documents et e-mails qui contiennent des informations sensibles.|
|BYOK|Voir *Bring your own key*.|
|Bring your own key|Souvent abrégé *BYOK*.<br /><br />Option de configuration et de topologie choisie par une organisation pour générer et gérer sa propre clé de locataire pour Azure Information Protection.|
|clé de contenu|Clé unique créée par des applications compatibles RMS pour chaque document ou e-mail protégé avec Rights Management et qui aide à limiter le risque de divulgation des informations.|
|consommer|Dans le contexte de la protection uniquement : Pour ouvrir un document ou un e-mail afin de le lire ou de l’utiliser si ce contenu a été protégé par un service de gestion des droits. Pour un document, la consommation inclut le fait de modifier et d’ajouter un nouveau contenu à un document protégé. Pour un e-mail, la consommation inclut le fait de répondre à un message protégé.<br /><br />Dans le contexte de l’étiquetage (avec ou sans protection) : Pour lire et potentiellement agir sur les informations des étiquettes stockées dans les métadonnées des fichiers et des e-mails.|
|désactiver|Permet de désactiver le service Rights Management pour que l’organisation ne puisse plus utiliser Azure Information Protection.|
|modèle de service|Modèle de protection que vous créez et que vous configurez pour être visible pour les utilisateurs sélectionnés, et non par tous les utilisateurs de votre organisation. Également appelé *modèle délimité*.|
|applications compatibles|Applications qui prennent nativement en charge Rights Management, telles que les applications Office, comme Word et Excel. Les éditeurs de logiciels indépendants et les développeurs peuvent également créer des applications qui prennent nativement en charge Rights Management.|
|gestion des droits d'entreprise|Terme générique standard couramment utilisé pour décrire les produits et solutions permettant aux organisations de protéger leurs informations sensibles ou précieuses par le biais d'une association d'outils de chiffrement et de stratégies d'autorisation. Azure Information Protection est un exemple de solution de gestion des droits d’entreprise (ERM).|
|ERM (Enterprise Rights Management)|Voir *Gestion des droits d’entreprise*.|
|protection générique|Niveau de protection permettant de chiffrer tout type de données et d'empêcher les personnes non autorisées d'accéder aux fichiers. Une fois le fichier ouvert, il est déchiffré et utilisable dans une application qui ne prend pas nativement en charge Rights Management.|
|HYOK|Voir *conservez votre propre clé*.|
|conservez votre propre clé|Souvent abrégé *HYOK*.<br /><br />Option de configuration et de topologie d’une organisation qui souhaite générer et stocker sa propre clé au niveau local, en général pour des raisons de conformité et de respect de la réglementation.|
|objet clé|Dans le contexte de la clé de locataire, entité qui contient les métadonnées exigées par le service Azure Rights Management pour les opérations de chiffrement.|
|label|Consultez *Étiquette Azure Information Protection*.|
|protection des informations|Souvent abrégé *IP*.<br /><br />Terme générique standard qui fait référence à la protection des données et des fichiers par le biais d'un accès limité, même après que les données et les fichiers ont quitté les frontières de l'organisation par courrier électronique ou via le partage de documents. Microsoft Azure Information Protection est un exemple de solution de protection des informations.|
|Gestion des droits relatifs à l'information|Souvent abrégé *IRM*.<br /><br />Terme utilisé avec les services Office, comme Exchange Server, Word et SharePoint Online, pour décrire la capacité à prendre en charge les services Microsoft Rights Management.|
|RMS|Voir *Gestion des droits relatifs à l’information*.|
|Chiffrement des messages Office|Souvent abrégé *OME*.<br /><br />Les nouvelles fonctionnalités de chiffrement de messages Office 365 ont une intégration native avec le service Azure Rights Management pour fournir la même protection des e-mails des utilisateurs internes et externes, actualiser automatiquement les modèles et prendre en charge le scénario BYOK (Bring your own key). La précédente implémentation d’OME était seulement conçue pour les destinataires externes, nécessitait une règle de flux de courrier et ne prenait pas en charge BYOK.|
|MSDRM|Vu parfois comme référence au client RMS 1.0, qui est remplacé par le nouveau client, MSIPC. Cet ancien client prend en charge les applications développées avec le kit de développement logiciel (SDK) RMS 1.0, ainsi qu'Office 2010 et Office 2007, Exchange 2010 et Exchange 2013, SharePoint 2010 et SharePoint 2007.|
|MSIPC|Vu parfois comme référence au client RMS 2.0, qui remplace l'ancien client RMS, MSDRM. Ce nouveau client prend en charge les applications développées avec RMS SDK 2.0, ainsi qu’Office 365 ProPlus, Office 2019, Office 2016, Office 2013, SharePoint 2013 et le client Azure Information Protection.|
|protection native|Niveau de protection disponible dans toutes les applications compatibles, qui empêche l'accès aux fichiers aux personnes non autorisées et qui permet également d'appliquer des stratégies restrictives, comme la lecture seule et l'interdiction d'impression. Il s'agit d'une protection permanente, même en cas de transfert des fichiers ou de sauvegarde dans un lieu public accessible à d'autres personnes.|
|.pfile|Extension de nom de fichier annexée à tous les fichiers protégés via un service de gestion des droits.|
|niveau d’autorisation|Regroupement logique des droits d’utilisation qui permet aux utilisateurs finals et aux administrateurs de choisir plus facilement les options de configuration basées sur des rôles. Par exemple, Réviseur et Coauteur.|
|protéger|Appliquer des contrôles de gestion des droits à des fichiers ou à des e-mails via des stratégies de chiffrement, d’identité et de contrôle d’accès afin de sécuriser vos données.|
|modèle de protection|Également appelé *modèle de stratégie de droits*, *modèle Rights Management* et *modèle RMS*.<br /><br />Groupe de paramètres de protection gérés par un administrateur et qui incluent les droits d’utilisation définis pour les utilisateurs autorisés et les contrôles d’accès hors connexion et d’expiration. |
|publish|Protection des fichiers en vue d'empêcher tout accès et utilisation non autorisés. Également utilisé en tant que terme conjointement avec les modèles de protection et la stratégie Azure Information Protection, pour rendre ces éléments disponibles pour une utilisation par les clients et services.|
|connecteur Rights Management|Relais de proxy sortant que vous pouvez déployer pour des services locaux, comme Exchange Server et SharePoint, afin de protéger les données à l’aide du service Azure Rights Management.|
|Émetteur Rights Management|Compte qui a protégé un document ou un e-mail.|
|Propriétaire Rights Management|Compte qui conserve le contrôle total sur un document ou un e-mail protégé quand il se voit automatiquement octroyé le droit d’utilisation Contrôle total de la gestion des droits et exempté de toute date d’expiration ou de paramètre hors connexion.|
|services Rights Management|Terme générique qui s’applique à la version cloud de Rights Management (Azure Rights Management) et à la version locale de Rights Management (AD RMS).|
|application de partage Rights Management|Maintenant remplacée par le client Azure Information Protection.|
|RMS|Voir *Services Rights Management*.|
|connecteur RMS|Voir *Connecteur Rights Management*.|
|RMS for individuals|Abonnement gratuit permettant à l’utilisateur d’utiliser Rights Management quand son organisation n’a pas d’abonnement Office 365 ou Azure Active Directory.|
|Application de partage RMS|Voir *Application de partage Rights Management*.|
|Modèle RMS|Voir *modèle de protection*.|
|mode Protection uniquement|Mode de fonctionnement du client Azure Information Protection lorsqu’il n’existe aucune stratégie Azure Information Protection à appliquer aux étiquettes. Dans ce mode, les étiquettes de classification ne s’affichent pas, mais les utilisateurs peuvent continuer à appliquer la protection Rights Management.|
|scanneur|Voir *Scanneur Azure Information Protection*.|
|super utilisateur|Groupe d’administrateurs de confiance possédant un droit d’accès et de déchiffrement sur les fichiers protégés par l’organisation à l’aide d’un service de gestion des droits. Ce niveau d'accès est généralement requis pour le processus eDiscovery légal et les audits.|
|clé de locataire|Ou clé de certificat de licence serveur (SLC).<br /><br />Clé propre à l’organisation, qui sécurise de façon optimale toutes les fonctions de chiffrement de Rights Management qui lui sont associées.|
|ôter la protection|Supprimer des contrôles de protection de fichiers ou d’e-mails, qui utilisent des stratégies de chiffrement, d’identité, de droits d’utilisation et de contrôle d’accès afin de sécuriser vos données.|
|licence d'utilisation|Certificat associé à un document, qui est accordé à un utilisateur qui ouvre un fichier ou un e-mail protégé par un service de gestion des droits. Ce certificat contient les droits d'utilisateur du fichier ou de l'e-mail, la clé de chiffrement qui est utilisée pour chiffrer le contenu, ainsi que les restrictions d'accès supplémentaires définies dans la stratégie du document.|

