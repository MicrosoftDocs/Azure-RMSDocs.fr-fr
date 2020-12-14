---
title: Terminologie relative à la Azure Information Protection (AIP)
description: Vous avez perdu un mot, une expression ou un acronyme lié à Microsoft Azure Information Protection (AIP) ? Recherchez ici la définition des termes et abréviations spécifiques à AIP ou qui ont une signification spécifique lorsqu’ils sont utilisés dans le contexte de ce service.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: af5c035a19847eca18a9686cc32895c363c0a926
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384554"
---
# <a name="terminology-for-azure-information-protection"></a>Terminologie liée à Azure Information Protection

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Pour fournir une expérience client unifiée et rationalisée, Azure Information Protection la **gestion des étiquettes** et des **clients classiques** dans le portail Azure sont **dépréciées** depuis le **31 mars 2021**. Ce laps de temps permet à tous les clients Azure Information Protection actuels de passer à notre solution d’étiquetage unifiée à l’aide de la plateforme d’étiquetage unifiée de Microsoft Information Protection. En savoir plus en consultant la [notice de dépréciation](https://aka.ms/aipclassicsunset) officielle.

Vous ne comprenez pas un mot, une expression ou un acronyme lié à Microsoft Azure Information Protection ? Recherchez ici la définition de termes et d’abréviations propres à Azure Information Protection, ou qui ont un sens particulier dans le contexte de ce service.

## <a name="word-phrase-or-acronym"></a>Mot, expression ou acronyme

[Un](#a)  |  [B](#b)  |  [C](#c)  |  [D](#d)  |  [E](#e)  |  [G](#g)  |  [H](#h)  |  [Je](#i)  |  [K](#k)  |  [L](#l)  |  [M](#m) [N](#n)  |  [O](#o)  |  [P](#p)  |  [R](#r)  |  [](#s)  |  [T](#t)  |  [U](#u)

### <a name="a"></a>Un
|Terme|Définition|
|--------|--------------|
|**AADRM**|Nom du premier module PowerShell pour le service de protection (Azure Rights Management), dérivé de l’abréviation non officielle d’Azure Rights Management lorsqu’il a été nommé précédemment (Windows) Azure Active Directory Rights Management. </br></br>Ce module PowerShell est maintenant remplacé par le module AIPService.|
|**déclencher**|Activez le service de protection Azure Rights Management pour qu’une organisation puisse protéger ses documents et ses e-mails. </br></br>Cette action active également les fonctionnalités IRM dans Exchange Online et Microsoft SharePoint.|
|**Services AD RMS (Active Directory Rights Management Services)**|Souvent abrégé *AD RMS*.<br /><br />Rôle Windows Server qui assure une protection par gestion des droits en utilisant le chiffrement et des stratégies pour mieux sécuriser les documents, les fichiers et les e-mails.|
|**AD RMS**|Voir *Services Active Directory Rights Management*.|
|**AIP** |Consultez *Azure information protection*.|
|**AIPService**|Nom actuel du module PowerShell pour le service de protection, qui remplace par l’ancien module AADRM.|
|**AzureInformationProtection**|Nom du module PowerShell pour l’Azure Information Protection client d’étiquetage classique ou unifié.|
|**Azure Information Protection**|Service cloud qui utilise des étiquettes pour classifier et protéger les documents et e-mails. </br></br> Azure Rights Management offre une protection à l’aide de stratégies de chiffrement, d’identité et d’autorisation.|
|**Client Azure Information Protection Classic**|Parfois abrégé en *client classique*.<br /><br />Le côté client d’origine de Azure Information Protection qui permet aux utilisateurs, aux administrateurs et aux services d’utiliser les étiquettes et les paramètres de votre stratégie de Azure Information Protection. </br></br> Désormais remplacé par le client d’étiquetage unifié Azure Information Protection.|
|**Étiquette Azure Information Protection**|Élément qui applique toujours une valeur de classification aux documents et aux e-mails, et qui peut aussi les protéger. </br></br>Quand une étiquette est appliquée, les informations de l’étiquette sont stockées dans les métadonnées pour que les applications et les services puissent les lire, et éventuellement agir sur celles-ci.|
|**Stratégie Azure Information Protection**|Configuration définie par l’administrateur pour les clients et services qui utilisent les paramètres de stratégie et les étiquettes Azure Information Protection.|
|**Scanneur Azure Information Protection**|Service qui s’exécute sur Windows Server et vous permet de découvrir, classifier et protéger des documents sur des partages réseau, ainsi que des sites et des bibliothèques SharePoint Server.|
|**Client d’étiquetage unifié Azure Information Protection**|Parfois abrégé en *client d’étiquetage unifié*.<br /><br />Le client pour les ordinateurs Windows qui permet aux utilisateurs, aux administrateurs et aux services d’utiliser les étiquettes de sensibilité et les paramètres de stratégie d’étiquette du centre de conformité d’Office 365 Security &, le centre de sécurité Microsoft 365 et le centre de conformité des Microsoft 365. </br></br>Remplace le client Azure Information Protection Classic.|
|**Azure RMS**|Voir *Azure Rights Management*.|
|**Visionneuse Azure Information Protection**|Application qui s’exécute sur des ordinateurs Windows et des appareils mobiles pour afficher les fichiers protégés.|
|**Azure Rights Management**|Également connu sous le nom de *service Azure Rights Management*, souvent abrégé en *Azure RMS*.<br /><br />Service Azure utilisé par Azure Information Protection qui recourt au chiffrement et à des stratégies, à des fins de sécurisation des documents, des fichiers et des e-mails. </br></br>Les noms précédents étaient les suivants :<br /><br />- *Windows Azure Active Directory Rights Management*: souvent abrégé en service Rights Management Windows Azure ad.<br /><br />- *RMS Online*: nom proposé à l’origine, que vous pouvez parfois voir apparaître dans les messages d’erreur et les entrées du fichier journal.|
| | |

### <a name="b"></a>B

|Terme|Définition|
|--------|--------------|
|**apporter votre propre clé**|Souvent abrégé *BYOK*.<br /><br />Option de configuration et de topologie choisie par une organisation pour générer et gérer sa propre clé de locataire pour Azure Information Protection.|
|**étiquetage intégré**|Une Microsoft 365 une application ou une fonctionnalité de service pour prendre en charge les étiquettes de sensibilité sans nécessiter l’installation d’un client d’étiquetage supplémentaire. Également appelée *étiquetage natif*.|
|**BYOK**|Voir *Bring your own key*.|
| | |

### <a name="c"></a>C

|Terme|Définition|
|--------|--------------|
|**occuper**|**Dans le contexte de la protection uniquement**: </br>Pour ouvrir un document ou un e-mail afin de le lire ou de l’utiliser si ce contenu a été protégé par un service de gestion des droits. </br>Pour un document, la consommation inclut le fait de modifier et d’ajouter un nouveau contenu à un document protégé. Pour un e-mail, la consommation inclut le fait de répondre à un message protégé.<br /><br/>**Dans le contexte de l’étiquetage (avec ou sans protection)**: </br>Pour lire et potentiellement agir sur les informations des étiquettes stockées dans les métadonnées des fichiers et des e-mails.|
|**clé de contenu**|Clé unique créée par des applications compatibles RMS pour chaque document ou e-mail protégé avec Rights Management et qui aide à limiter le risque de divulgation des informations.|
| | |

### <a name="d"></a>D

|Terme|Définition|
|--------|--------------|
|**désactiver**|Permet de désactiver le service Rights Management pour que l’organisation ne puisse plus utiliser Azure Information Protection.|
|**modèle par défaut**|Modèle de protection qui est automatiquement créé pour vous lorsque vous obtenez un abonnement pour Azure Information Protection, afin que vous puissiez immédiatement commencer à protéger les documents et e-mails qui contiennent des informations sensibles.|
|**modèle de service**|Modèle de protection que vous créez et que vous configurez pour être visible pour les utilisateurs sélectionnés, et non par tous les utilisateurs de votre organisation. Également appelé *modèle délimité*.|
|**Chiffrement à clé double** |Également connu sous le nom de *DKE*, méthode de sécurisation du contenu qui utilise deux clés : une qui est conservée dans Azure et une autre détenue par le webhdfs. </br></br>DKE est uniquement pris en charge par le client unifié AIP et est configuré dans Microsoft 365. |
| | |

### <a name="e"></a>E

|Terme|Définition|
|--------|--------------|
|**applications compatibles**|Applications qui prennent nativement en charge Rights Management, telles que les applications Office, comme Word et Excel. </br></br>Les éditeurs de logiciels indépendants et les développeurs peuvent également créer des applications qui prennent nativement en charge Rights Management.|
|**gestion des droits d'entreprise**|Terme générique standard couramment utilisé pour décrire les produits et solutions permettant aux organisations de protéger leurs informations sensibles ou précieuses par le biais d'une association d'outils de chiffrement et de stratégies d'autorisation. </br></br>Azure Information Protection est un exemple de solution de gestion des droits d’entreprise (ERM).|
|**ERM (Enterprise Rights Management)**|Voir *gestion des droits d'entreprise*.|
| | |

### <a name="g"></a>G

|Terme|Définition|
|--------|--------------|
|**protection générique**|Niveau de protection permettant de chiffrer tout type de données et d'empêcher les personnes non autorisées d'accéder aux fichiers. </br></br>Une fois le fichier ouvert, il est déchiffré et utilisable dans une application qui ne prend pas nativement en charge Rights Management.|
| | |

### <a name="h"></a>H

|Terme|Définition|
|--------|--------------|
|**conserver votre propre clé**|Souvent abrégé *HYOK*.<br /><br />Option de configuration et de topologie d’une organisation qui souhaite générer et stocker sa propre clé au niveau local, en général pour des raisons de conformité et de respect de la réglementation. </br></br>HYOK est pris en charge par le client standard AIP uniquement.|
|**HYOK**|Voir *conservez votre propre clé*.|
| | |

### <a name="i"></a>I

|Terme|Définition|
|--------|--------------|
|**protection des informations**|Souvent abrégé *PI*.<br /><br />Terme générique standard qui fait référence à la protection des données et des fichiers par le biais d'un accès limité, même après que les données et les fichiers ont quitté les frontières de l'organisation par courrier électronique ou via le partage de documents. </br></br>Microsoft Azure Information Protection est un exemple de solution de protection des informations.|
|**Informations Rights Management**|Souvent abrégé *IRM*.<br /><br />Terme utilisé conjointement avec les services Office, tels qu’Exchange Server, Word et SharePoint, pour décrire la capacité à prendre en charge les services Microsoft Rights Management.|
|**RMS**|Voir *services RMS*.|
| | |


### <a name="k"></a>K

|Terme|Définition|
|--------|--------------|
|**Key, objet**|Dans le contexte de la clé de locataire, entité qui contient les métadonnées exigées par le service Azure Rights Management pour les opérations de chiffrement.|
| | |

### <a name="l"></a>L

|Terme|Définition|
|--------|--------------|
|**label**|Consultez *Étiquette Azure Information Protection*.|
| | |

### <a name="m"></a>M

|Terme|Définition|
|--------|--------------|
|**Microsoft Information Protection**| Parfois abrégé en *MIP*.<br /><br /> Une infrastructure pour les produits et les fonctionnalités intégrées qui utilisent le même magasin d’étiquetage (« étiquettes unifiées ») et vous aident à protéger les informations sensibles de votre organisation.|
|**MIP**| Consultez *Microsoft information protection*|
|**MSDRM**|Vu parfois comme référence au client RMS 1.0, qui est remplacé par le nouveau client, MSIPC. </br></br>Cet ancien client prend en charge les applications développées avec RMS SDK 1.0, ainsi qu'Office 2010 et Office 2007, Exchange 2010 et Exchange 2013, SharePoint 2010 et SharePoint 2007.|
|**MSIPC**|Vu parfois comme référence au client RMS 2.0, qui remplace l'ancien client RMS, MSDRM. </br></br>Ce nouveau client prend en charge les applications développées avec RMS SDK 2.0, ainsi qu’Office 365 ProPlus, Office 2019, Office 2016, Office 2013, SharePoint 2013 et le client Azure Information Protection.|
| | |

### <a name="n"></a>N

|Terme|Définition|
|--------|--------------|
|**protection native**|Niveau de protection disponible dans toutes les applications compatibles, qui empêche l'accès aux fichiers aux personnes non autorisées et qui permet également d'appliquer des stratégies restrictives, comme la lecture seule et l'interdiction d'impression. </br></br>Il s'agit d'une protection permanente, même en cas de transfert des fichiers ou de sauvegarde dans un lieu public accessible à d'autres personnes.|
| | |

### <a name="o"></a>O

|Terme|Définition|
|--------|--------------|
|**Chiffrement des messages Office**|Souvent abrégé *OME*.<br /><br />Les nouvelles fonctionnalités de chiffrement de messages Office 365 intègrent le service Azure Rights Management pour offrir la même protection de messagerie pour les utilisateurs internes et externes, l’actualisation automatique des modèles et la prise en charge du scénario BYOK. </br></br>La précédente implémentation d’OME était seulement conçue pour les destinataires externes, nécessitait une règle de flux de courrier et ne prenait pas en charge BYOK.|
| | |

### <a name="p"></a>P

|Terme|Définition|
|--------|--------------|
|**. pfile**|Extension de nom de fichier annexée à tous les fichiers protégés via un service de gestion des droits.|
|**niveau d’autorisation**|Regroupement logique des droits d’utilisation qui permet aux utilisateurs finals et aux administrateurs de choisir plus facilement les options de configuration basées sur des rôles. Par exemple, Réviseur et Coauteur.|
|**protéger**|Appliquer des contrôles de gestion des droits à des fichiers ou à des e-mails via des stratégies de chiffrement, d’identité et de contrôle d’accès afin de sécuriser vos données.|
|**mode protection uniquement**|Mode de fonctionnement du client Azure Information Protection lorsqu’il n’existe aucune stratégie Azure Information Protection à appliquer aux étiquettes. </br></br>Dans ce mode, les étiquettes de classification ne s’affichent pas, mais les utilisateurs peuvent continuer à appliquer la protection Rights Management.|
|**modèle de protection**|Également appelé *modèle de stratégie de droits*, *modèle Rights Management* et *modèle RMS*.<br /><br />Groupe de paramètres de protection gérés par un administrateur et qui incluent les droits d’utilisation définis pour les utilisateurs autorisés et les contrôles d’accès hors connexion et d’expiration. |
|**édition**|Protection des fichiers en vue d'empêcher tout accès et utilisation non autorisés. </br></br>Également utilisé en tant que terme conjointement avec les modèles de protection et la stratégie Azure Information Protection, pour rendre ces éléments disponibles pour une utilisation par les clients et services.|
| | |

### <a name="r"></a>R

|Terme|Définition|
|--------|--------------|
|**connecteur Rights Management**|Relais de proxy sortant que vous pouvez déployer pour des services locaux, comme Exchange Server et SharePoint, afin de protéger les données à l’aide du service Azure Rights Management.|
|**Émetteur Rights Management**|Compte qui a protégé un document ou un e-mail.|
|**Propriétaire Rights Management**|Compte qui conserve le contrôle total sur un document ou un e-mail protégé quand il se voit automatiquement octroyé le droit d’utilisation Contrôle total de la gestion des droits et exempté de toute date d’expiration ou de paramètre hors connexion.|
|**Services Rights Management**|Terme générique qui s’applique à la version cloud de Rights Management (Azure Rights Management) et à la version locale de Rights Management (AD RMS).|
|**application de partage Rights Management**|Maintenant remplacée par le client Azure Information Protection.|
|**RMS**|Voir *services Rights Management*.|
|**Connecteur RMS**|Voir *Connecteur Rights Management*.|
|**RMS pour les particuliers**|Abonnement gratuit permettant à l’utilisateur d’employer Rights Management quand son organisation n’a pas d’abonnement Office 365 ou Azure Active Directory.|
|**Application de partage RMS**|Voir *application de partage Rights Management*.|
|**Modèle RMS**|Voir *modèle de protection*.|

### <a name="s"></a>S

|Terme|Définition|
|--------|--------------|
|**logiciels**|Voir *Scanneur Azure Information Protection*.|
|**super utilisateur**|Groupe d’administrateurs de confiance possédant un droit d’accès et de déchiffrement sur les fichiers protégés par l’organisation à l’aide d’un service de gestion des droits. </br></br>Ce niveau d'accès est généralement requis pour le processus eDiscovery légal et les audits.|

### <a name="t"></a>T

|Terme|Définition|
|--------|--------------|
|**clé de locataire**|Également appelée clé de *certificat de licence serveur*.<br /><br />Clé propre à l’organisation, qui sécurise de façon optimale toutes les fonctions de chiffrement de Rights Management qui lui sont associées.|

### <a name="u"></a>U

|Terme|Définition|
|--------|--------------|
|**étiquette unifiée**| Également appelée *étiquette de sensibilité unifiée*.<br /><br /> Étiquette qui peut être appliquée par les applications, les clients et les services qui prennent en charge Microsoft Information Protection Framework, pour appliquer la classification et éventuellement la protection. </br></br>Dans les applications et services Office, les étiquettes unifiées sont implémentées en tant qu’étiquettes de sensibilité.|
|**ôter la protection**|Supprimer des contrôles de protection de fichiers ou d’e-mails, qui utilisent des stratégies de chiffrement, d’identité, de droits d’utilisation et de contrôle d’accès afin de sécuriser vos données.|
|**licence d'utilisation**|Certificat associé à un document, qui est accordé à un utilisateur qui ouvre un fichier ou un e-mail protégé par un service de gestion des droits. </br></br>Ce certificat contient les droits d'utilisateur du fichier ou de l'e-mail, la clé de chiffrement qui est utilisée pour chiffrer le contenu, ainsi que les restrictions d'accès supplémentaires définies dans la stratégie du document.|

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les noms AIP, consultez [Azure information protection, également appelé...](aka.md).