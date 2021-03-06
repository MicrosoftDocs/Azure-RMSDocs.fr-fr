---
title: 'Fonctionnement d’Azure RMS : Azure Information Protection'
description: Description du fonctionnement d’Azure RMS, des contrôles de chiffrement qu’il utilise et des diagrammes étape par étape expliquant le fonctionnement du processus.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8adba522d85bec9d2d1062c510b10ae9b96368a3
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381746"
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>Fonctionnement d’Azure RMS Sous le capot

>***S’applique à**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>*Concerne : client **d'** [étiquetage unifié AIP et client Classic](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

En ce qui concerne le fonctionnement d’Azure RMS, il est important de comprendre que ce service de protection des données fourni par Azure Information Protection n’affiche pas et ne stocke pas vos données dans le cadre du processus de protection. Les informations que vous protégez ne sont jamais stockées dans Azure, sauf si vous indiquez expressément votre volonté de les y stocker, ou si vous utilisez un autre service cloud qui les stocke dans Azure. Azure RMS rend simplement les données d’un document illisibles pour toute personne qui ne fasse pas partie des utilisateurs et services autorisés :

- Les données sont chiffrées au niveau de l’application, et incluent une stratégie qui définit l’utilisation autorisée du document.

- Quand un document protégé est employé par un utilisateur légitime, ou traité par un service autorisé, ses données sont déchiffrées et les droits définis dans la stratégie sont appliqués.

Dans l’image suivante, vous pouvez voir comment ce processus fonctionne dans sa globalité. Un document contenant la formule secrète est protégé, puis ouvert correctement par un utilisateur ou un service autorisé. Le document est protégé par une clé de contenu (la clé verte sur cette image). Elle est unique pour chaque document et se trouve dans l’en-tête du fichier où elle est protégée par votre clé racine de tenant Azure Information Protection (la clé rouge sur l’image). Microsoft peut générer et gérer votre clé de tenant. Vous pouvez également générer et gérer personnellement votre propre clé de tenant.

Durant le processus de protection, quand Azure RMS chiffre, déchiffre, autorise et applique des restrictions, la formule secrète n’est jamais envoyée à Azure.

![Protection d’un fichier par Azure RMS](./media/AzRMS_SecretColaFormula_final.png)

Pour obtenir une description détaillée de ce qui se passe, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de cet article.

Pour obtenir des détails techniques sur les algorithmes et les longueurs de clé qu’Azure RMS utilise, consultez la section suivante.

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Contrôles de chiffrement utilisés par Azure RMS : algorithmes et longueurs de clé
Même si vous n’avez pas besoin de connaître en détail le fonctionnement de cette technologie, vous devrez peut-être fournir certaines informations sur les contrôles de chiffrement utilisés, par exemple pour confirmer que la protection de sécurité répond aux normes.


|Contrôles de chiffrement|Utilisation dans Azure RMS|
|-|-|
|Algorithme : AES<br /><br />Longueur de clé : 128 bits et 256 bits [[1]](#footnote-1)|Protection du contenu|
|Algorithme : RSA<br /><br />Longueur de clé : 2 048 bits [[2]](#footnote-2)|Protection de clé|
|SHA-256|Signature de certificat|
| | |

###### <a name="footnote-1"></a>Note 1 

Une clé de 256 bits est utilisée par le client Azure Information Protection dans les scénarios suivants :

- Protection générique (.pfile).

- Protection native pour les documents PDF quand le document a été protégé avec la norme ISO pour le chiffrement de PDF, ou quand le document protégé qui en résulte a une extension de nom de fichier .ppdf.

- Protection native pour les fichiers texte ou image (comme .ptxt ou .pjpg).

###### <a name="footnote-2"></a>Note 2

La longueur de la clé est de 2 048 bits quand le service Azure Rights Management est activé. Une longueur de 1 024 bits est prise en charge dans les scénarios optionnels suivants :

- Durant une migration à partir d’un site local, si le cluster AD RMS s’exécute en mode de chiffrement 1.

- Pour les clés archivées qui ont été créées localement avant la migration, afin que le contenu préalablement protégé par AD RMS puisse continuer à être ouvert par la post-migration du service Azure Rights Management.

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>Mode de stockage et de sécurisation des clés de chiffrement Azure RMS

Pour chaque document ou e-mail protégé par Azure RMS, Azure RMS crée une clé AES unique (la « clé de contenu ») qui est incorporée au document et persiste au fil de ses modifications successives. 

La clé de contenu est protégée à l’aide de la clé RSA de l’organisation (« clé de tenant Azure Information Protection ») dans le cadre de la stratégie définie dans le document. La stratégie est également signée par l’auteur du document. Cette clé de tenant est commune à tous les documents et e-mails protégés par le service Azure Rights Management pour l’organisation. Elle ne peut être modifiée par un administrateur Azure Information Protection que si l’organisation utilise une clé de tenant gérée par le client, également appelée BYOK (Bring Your Own Key). 

Cette clé de tenant est protégée dans les services en ligne de Microsoft, dans un environnement très contrôlé et sous étroite surveillance. Quand vous utilisez une clé de tenant gérée par le client (BYOK), cette sécurité est renforcée par l’utilisation d’une série de modules de sécurité matériels (HSM) haut de gamme dans chaque région Azure, sans possibilité d’extraire, d’exporter ou de partager les clés, quelles que soient les circonstances. Pour plus d’informations sur les options de clé de tenant et les clés BYOK, consultez [Planification et implémentation de votre clé de locataire Azure Information Protection](plan-implement-tenant-key.md).

Les licences et certificats envoyés à un appareil Windows sont protégés par la clé privée d’appareil du client, créée quand un utilisateur se sert d’Azure RMS sur l’appareil pour la première fois. Cette clé privée est à son tour protégée par DPAPI sur le client, ce qui a pour effet de protéger ces secrets à l’aide d’une clé dérivée du mot de passe de l’utilisateur. Sur les appareils mobiles, les clés ne sont utilisées qu’une seule fois. Ainsi, n’étant pas stockées sur les clients, elles ne nécessitent pas de protection sur l’appareil. 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu

Pour comprendre plus en détail le fonctionnement d’Azure RMS, examinons un flux classique tel qu’il se produit après l’[activation du service Azure Rights Management](activate-service.md), quand un utilisateur emploie le service Rights Management pour la première fois sur son ordinateur Windows (un processus parfois nommé **initialisation de l’environnement utilisateur** ou amorçage), **protège du contenu** (un document ou un e-mail), puis **consomme** (ouvre et utilise) du contenu protégé par quelqu’un d’autre.

Après l’initialisation de l’environnement utilisateur, l’utilisateur peut protéger des documents ou consommer des documents protégés sur cet ordinateur.

> [!NOTE]
> Si l’utilisateur se sert d’un autre ordinateur Windows, ou si un autre utilisateur se sert de ce même ordinateur, le processus d’initialisation est répété.

### <a name="initializing-the-user-environment"></a>Initialisation de l’environnement utilisateur
Pour qu’un utilisateur puisse protéger du contenu ou utiliser du contenu protégé sur un ordinateur Windows, l’environnement utilisateur doit être préparé sur l’appareil en question. Ce processus se produit une seule fois, sans intervention humaine, quand un utilisateur tente de protéger ou de consommer du contenu protégé :

![Flux d’activation du client RMS : étape 1, authentification du client](./media/AzRMS.png)

**Ce qui se passe à l’étape 1** : le client RMS sur l’ordinateur se connecte d’abord au service Azure Rights Management, puis authentifie l’utilisateur à l’aide de son compte Azure Active Directory.

Lorsque le compte de l’utilisateur est fédéré avec Azure Active Directory, cette authentification est automatique. L’utilisateur n’est donc pas invité à fournir d’informations d’identification.

![Activation du client RMS : étape 2, les certificats sont téléchargés sur le client](./media/AzRMS_useractivation2.png)

**Ce qui se passe à l’étape 2** : une fois l’utilisateur authentifié, la connexion est automatiquement redirigée vers le tenant Azure Information Protection de l’organisation, qui émet des certificats permettant à l’utilisateur de s’authentifier auprès du service Azure Rights Management, pour consommer du contenu protégé et protéger du contenu hors connexion.

Le certificat de compte de droits, ou certificat RAC, est l’un de ces certificats. Ce certificat authentifie l’utilisateur pour Azure Active Directory et est valide pendant 31 jours. Le certificat est renouvelé automatiquement par le client RMS, à condition que le compte d’utilisateur existe toujours dans Azure Active Directory et qu’il soit activé. Ce certificat n’est pas configurable par un administrateur. 

Une copie de ce certificat est stockée dans Azure pour permettre la création d’autres certificats avec les mêmes clés si l’utilisateur change d’appareil.

### <a name="content-protection"></a>Protection du contenu
Quand un utilisateur protège un document, le client RMS effectue les actions suivantes sur un document non protégé :

![Protection de document RMS : étape 1, le document est chiffré](./media/AzRMS_documentprotection1.png)

**Ce qui se passe à l’étape 1**: le client RMS crée une clé aléatoire (clé de contenu), puis chiffre le document en utilisant cette clé, avec l’algorithme de chiffrement symétrique AES.

![Protection de document RMS : étape 2, la stratégie est créée](./media/AzRMS_documentprotection2.png)

**Ce qui se passe à l’étape 2**: le client RMS crée ensuite un certificat incluant une stratégie pour le document, qui comprend les [droits d’utilisation](configure-usage-rights.md) pour les utilisateurs ou les groupes, ainsi que d’autres restrictions, comme une date d’expiration. Ces paramètres peuvent être définis dans un modèle qu’un administrateur a déjà configuré ou spécifié au moment de la protection du contenu (parfois appelé « stratégie ad hoc »).   

Le principal attribut Azure AD utilisé pour identifier les utilisateurs et groupes sélectionnés est l’attribut ProxyAddresses d’Azure AD, qui stocke toutes les adresses e-mail pour un utilisateur ou un groupe. Toutefois, si un compte d’utilisateur ne possède aucune valeur dans l’attribut ProxyAddresses d’AD, la valeur UserPrincipalName de l’utilisateur est employée à la place.

Le client RMS utilise ensuite la clé de l’organisation obtenue lors de l’initialisation de l’environnement utilisateur, en se servant de cette clé pour chiffrer la stratégie et la clé symétrique de contenu. Le client RMS signe également la stratégie avec le certificat de l’utilisateur obtenu lors de l’initialisation de l’environnement utilisateur.

![Protection de document RMS : étape 3, la stratégie est incorporée dans le document](./media/AzRMS_documentprotection3.png)

**Ce qui se passe à l’étape 3**: Enfin, le client RMS incorpore la stratégie dans un fichier avec le corps du document chiffré précédemment, qui, ensemble, comprend un document protégé.

Ce document peut être stocké partout, ou partagé à l’aide de n’importe quelle méthode, et la stratégie reste toujours associée au document chiffré.

### <a name="content-consumption"></a>Consommation du contenu
Quand un utilisateur veut consommer un document protégé, le client RMS commence par demander l’accès au service Azure Rights Management :

![Consommation de document RMS : étape 1, l’utilisateur est authentifié et obtient la liste des droits](./media/AzRMS_documentconsumption1.png)

**Ce qui se passe à l’étape 1**: l’utilisateur authentifié envoie la stratégie de document et les certificats de l’utilisateur au service Azure Rights Management. Le service déchiffre et évalue la stratégie, puis génère la liste des droits (éventuels) de l’utilisateur sur le document. Pour identifier l’utilisateur, l’attribut ProxyAddresses d’Azure AD est utilisé pour le compte de l’utilisateur et les groupes dont l’utilisateur est membre. Pour des raisons de performances, l’appartenance au groupe est [mise en cache](prepare.md#group-membership-caching-by-azure-information-protection). Si le compte d’utilisateur n’a aucune valeur pour l’attribut ProxyAddresses d’Azure AD, la valeur UserPrincipalName d’Azure AD est utilisée à la place.

![Consommation de document RMS : étape 2, la licence d’utilisation est retournée au client](./media/AzRMS_documentconsumption2.png)

**Ce qui se passe à l’étape 2**: le service extrait ensuite la clé de contenu AES de la stratégie déchiffrée. Cette clé est alors chiffrée avec la clé RSA publique de l’utilisateur obtenue avec la requête.

Après cela, la clé de contenu rechiffrée est incorporée dans une licence d’utilisation chiffrée avec la liste des droits de l’utilisateur, qui est renvoyée au client RMS.

![Consommation de document RMS : étape 3, le document est déchiffré et les droits sont appliqués](./media/AzRMS_documentconsumption3.png)

**Ce qui se passe à l’étape 3**: enfin, le client RMS prend la licence d’utilisation chiffrée et la déchiffre avec sa propre clé privée utilisateur. Cela permet au client RMS de déchiffrer le corps du document si nécessaire, et de l’afficher à l’écran.

Le client déchiffre également la liste des droits, et transmet ces derniers à l’application qui les applique dans son interface utilisateur.

> [!NOTE]
> Quand les utilisateurs externes à votre organisation consomment du contenu que vous avez protégé, le flux de consommation est le même. Ce qui change dans ce scénario, c’est le mode d’authentification de l’utilisateur. Pour plus d’informations, consultez [Lors du partage d’un document protégé avec une personne extérieure à mon organisation, comment cet utilisateur s’authentifie-t-il ?](./faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)


### <a name="variations"></a>Variantes
Les procédures pas à pas précédentes couvrent les scénarios standard, mais il existe des variantes :

- **Protection de la messagerie** : quand le chiffrement des messages Exchange Online et Office 365 avec de nouvelles fonctionnalités est utilisé pour protéger des messages e-mail, l’authentification demandée pour leur consommation peut également utiliser la fédération avec un fournisseur d’identité sociale ou un code secret à usage unique. Ensuite, les flux de traitement sont très similaires, excepté que la consommation du contenu se fait du côté service dans une session de navigateur web, sur une copie temporairement mise en cache des e-mails sortants.

- **Appareils mobiles** : quand des appareils mobiles protègent ou consomment des fichiers avec le service Azure Rights Management, les flux du processus sont beaucoup plus simples. Les appareils mobiles ne passent pas par le processus d’initialisation utilisateur, car chaque transaction (pour protéger ou consommer du contenu) est indépendante. Comme avec les ordinateurs Windows, les appareils mobiles se connectent au service Azure Rights Management et s’authentifient. Pour protéger du contenu, les appareils mobiles soumettent une stratégie, puis le service Azure Rights Management leur envoie une licence de publication et une clé symétrique pour protéger le document. Pour consommer du contenu, quand des appareils mobiles se connectent au service Azure Rights Management et s’authentifient, ils envoient la stratégie de document au service Azure Rights Management et demandent une licence d’utilisation pour consommer le document. En réponse, le service Azure Rights Management leur envoie les clés nécessaires et les restrictions. Les deux processus utilisent TLS pour protéger l’échange de clés et d’autres communications.

- **Connecteur RMS** : quand le service Azure Rights Management est utilisé avec le connecteur RMS, le flux du processus reste identique. La seule différence est que le connecteur fait office de relais entre les services locaux (comme Exchange Server et SharePoint Server) et le service Azure Rights Management. Le connecteur proprement dit n’effectue aucune opération telle qu’une initialisation de l’environnement utilisateur, un chiffrement ou un déchiffrement. Il relaie simplement la communication qui accède généralement à un serveur AD RMS, en gérant la traduction entre les protocoles utilisés de part et d’autre. Ce scénario vous permet d’utiliser le service Azure Rights Management avec des services locaux.

- **Protection générique (.pfile)** : quand le service Azure Rights Management protège un fichier de façon générique, le flux est fondamentalement le même pour la protection du contenu, sauf que le client RMS crée une stratégie qui accorde tous les droits. Lorsque le fichier est consommé, il est déchiffré avant d’être transmis à l’application cible. Ce scénario vous permet de protéger tous les fichiers, même s’ils ne prennent pas en charge RMS en mode natif.

- **Comptes Microsoft** : Azure Information Protection peut autoriser l’utilisation d’adresses e-mail si elles sont authentifiées avec un compte Microsoft. Toutefois, toutes les applications ne peuvent pas ouvrir du contenu protégé lorsqu’un compte Microsoft est utilisé pour l’authentification. [Plus d’informations](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur le service Azure Rights Management, reportez-vous aux autres articles de la section **Comprendre et explorer**, comme [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md), pour savoir comment intégrer vos applications existantes avec Azure Rights Management afin de bénéficier d’une solution de protection des informations. 

Consultez [Terminologie liée à Azure Information Protection](./terminology.md) pour vous familiariser avec les termes que vous allez rencontrer lors de la configuration et de l’utilisation du service Azure Rights Management, et n’oubliez pas de lire aussi [Configuration requise pour Azure Information Protection](requirements.md) avant d’entamer votre déploiement. Si vous souhaitez vous plonger directement et essayer par vous-même, utilisez le Guide de démarrage rapide et les didacticiels suivants :

- [Démarrage rapide : Déployer le client d’étiquetage unifié](quickstart-deploy-client.md)
- [Tutoriel : Installation du scanneur d’étiquetage unifié Azure Information Protection](tutorial-install-scanner.md)
- [Tutoriel : Recherche de votre contenu sensible avec le scanneur Azure Information Protection (AIP)](tutorial-scan-networks-and-content.md)
- [Tutoriel : Empêcher les partages inappropriés dans Outlook avec Azure Information Protection (AIP)](tutorial-preventing-oversharing.md)

Si vous êtes prêt à déployer la protection des données pour votre organisation, utilisez la feuille [de route de déploiement AIP pour la classification, l’étiquetage et la protection](deployment-roadmap-classify-label-protect.md) de vos étapes de déploiement, ainsi que des liens vers des instructions.

> [!TIP]
> Pour obtenir plus d’informations et de l’aide supplémentaire, utilisez les ressources et les liens dans [Informations et prise en charge pour Azure Information Protection](information-support.md).
