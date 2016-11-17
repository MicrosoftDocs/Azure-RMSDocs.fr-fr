---
title: "Fonctionnement d’Azure RMS | Azure Information Protection"
description: "Découvrez en détail le fonctionnement d’Azure RMS, les contrôles de chiffrement qu’il utilise et le déroulement de ce processus à l’aide de diagrammes détaillés."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0e66bfa436bf811b34cf3cfe1b2d68a6a4e137c2
ms.openlocfilehash: dd6c9250102e104ba49b0c08f14d9959cd1228cb


---


# <a name="how-does-azure-rms-work-under-the-hood"></a>Fonctionnement d'Azure RMS Sous le capot

>*S’applique à : Azure Information Protection, Office 365*

Concernant le fonctionnement d'Azure RMS, il est important de comprendre que le service Rights Management et, plus généralement, Microsoft ne consultent ni ne stockent vos données dans le cadre du processus de protection des informations. Les informations que vous protégez ne sont jamais stockées dans Azure, sauf si vous indiquez expressément votre volonté de les y stocker, ou si vous utilisez un autre service cloud qui les stocke dans Azure. Azure RMS rend simplement les données d'un document illisibles pour toute personne autre que des utilisateurs et services autorisés :

-   Les données sont chiffrées au niveau de l'application, et incluent une stratégie qui définit l'utilisation autorisée du document.

-   Quand un document protégé est utilisé par un utilisateur légitime, ou traité par un service autorisé, ses données sont déchiffrées et les droits définis dans la stratégie appliqués.

À un niveau élevé, vous pouvez voir comment ce processus fonctionne dans l'image suivante. Un document contenant la formule secrète est protégé, puis ouvert correctement par un utilisateur ou un service autorisé. Le document est protégé par une clé de contenu (la clé verte sur cette image). Elle est unique pour chaque document et est placée dans l’en-tête du fichier où elle est protégée par votre clé racine de locataire Azure Information Protection (la clé rouge sur l’image). Microsoft peut générer et gérer votre clé de locataire. Vous pouvez également générer et gérer personnellement votre propre clé de locataire.

Durant le processus de protection, quand Azure RMS chiffre, déchiffre, autorise et applique des restrictions, la formule secrète n'est jamais envoyée à Azure.

![Comment Azure RMS protège un fichier](../media/AzRMS_SecretColaFormula_final.png)

Pour obtenir une description détaillée de ce qui se passe, consultez la section [Procédure pas à pas décrivant le fonctionnement d’Azure RMS : première utilisation, protection du contenu, consommation du contenu](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de cet article.

Pour obtenir des détails techniques sur les algorithmes et les longueurs de clé qu'Azure RMS utilise, consultez la section suivante.

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Contrôles de chiffrement utilisés par Azure RMS : Algorithmes et longueurs de clé
Même si vous n'avez pas besoin de connaître le détail du fonctionnement de RMS, il se peut que l'on vous interroge sur les contrôles de chiffrement utilisés, pour s'assurer que la protection de sécurité est conforme aux normes.


|Contrôles de chiffrement|Utilisation dans Azure RMS|
|-|-|
|Algorithme : AES<br /><br />Longueur de clé : 128 bits et 256 bits [[1]](#footnote-1)|Protection de documentation|
|Algorithme : RSA<br /><br />Longueur de clé : 2 048 bits|Protection de clé|
|SHA-256|Signature de certificat|

###### <a name="footnote-1"></a>Note 1 

La longueur de 256 bits est utilisée par l'application de partage Rights Management pour la protection en modes générique et natif quand le fichier a une extension de nom de fichier .ppdf, ou est un fichier image ou texte protégé (tel que .ptxt ou .pjpg).

Mode de stockage et de sécurisation des clés de chiffrement :

- Pour chaque document ou e-mail protégé par Azure RMS, Azure RMS crée une clé AES unique (la « clé de contenu »), qui est incorporée au document et qui persiste au fil de ses modifications successives. 

- La clé de contenu est protégée à l’aide de la clé RSA de l’organisation (la « clé de locataire Azure Information Protection ») dans le cadre de la stratégie définie dans le document. La stratégie est également signée par l’auteur du document. Cette clé de locataire est commune à tous les documents et e-mails protégés par Azure RMS pour l’organisation ; elle ne peut être modifiée par un administrateur Azure Information Protection que si l’organisation utilise une clé de locataire gérée par le client, également appelée BYOK (Bring Your Own Key). 

    Cette clé de locataire est protégée dans les services en ligne de Microsoft, dans un environnement très contrôlé et sous étroite surveillance. Lorsque vous utilisez une clé de locataire gérée par le client (BYOK), cette sécurité est renforcée par l’utilisation d’une série de modules de sécurité matériels (HSM) haut de gamme dans chaque région Azure, ne laissant aucune possibilité d’extraire, exporter ou partager les clés, quelles que soient les circonstances. Pour plus d’informations sur les options de clé de locataire et les clés BYOK, consultez [Planification et implémentation de votre clé de locataire Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

- Les licences et certificats envoyés à un appareil Windows sont protégés par la clé privée d’appareil du client, créée quand un utilisateur utilise Azure RMS sur l’appareil pour la première fois. Cette clé privée est à son tour protégée par DPAPI sur le client, ce qui a pour effet de protéger ces clés secrètes à l’aide d’une clé dérivée du mot de passe de l’utilisateur. Sur les appareils mobiles, les clés ne sont utilisées qu’une seule fois. Ainsi, n’étant pas stockées sur les clients, elles ne nécessitent pas de protection sur l’appareil. 



## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Procédure pas à pas décrivant le fonctionnement d'Azure RMS : première utilisation, protection du contenu, consommation du contenu
Pour comprendre plus en détails le fonctionnement d’Azure RMS, examinons un flux classique tel qu’il se produit après l’[activation du service Azure Rights Management](../deploy-use/activate-service.md), quand un utilisateur utilise le service Rights Management pour la première fois sur son ordinateur Windows (un processus parfois nommé **initialisation de l’environnement utilisateur** ou amorçage), **protège du contenu** (un document ou un e-mail), puis **consomme** (ouvre et utilise) du contenu protégé par quelqu’un d’autre.

Après l'initialisation de l'environnement utilisateur, l'utilisateur peut protéger des documents ou consommer des documents protégés sur cet ordinateur.

> [!NOTE]
> Si l'utilisateur utilise un autre ordinateur Windows, ou si un autre utilisateur utilise ce même ordinateur, le processus d'initialisation est répété.

### <a name="initializing-the-user-environment"></a>Initialisation de l'environnement utilisateur
Pour qu'un utilisateur puisse protéger du contenu ou utiliser du contenu protégé sur un ordinateur Windows, l'environnement utilisateur doit être préparé sur l'appareil en question. Ce processus se produit une seule fois, sans intervention humaine, quand un utilisateur tente de protéger ou de consommer du contenu protégé :

![Activation du client RMS : étape 1](../media/AzRMS.png)

**Ce qui se passe à l’étape 1** : le client RMS sur l’ordinateur se connecte d’abord au service à Azure Rights Management, puis authentifie l’utilisateur à l’aide de son compte Azure Active Directory.

Lorsque le compte de l'utilisateur est fédéré avec Azure Active Directory, cette authentification est automatique. L'utilisateur n'est donc pas invité à fournir d'informations d'identification.

![Activation du client RMS : étape 2](../media/AzRMS_useractivation2.png)

**Ce qui se passe à l’étape 2** : une fois l’utilisateur authentifié, la connexion est automatiquement redirigée vers le locataire Azure Information Protection de l’organisation, qui émet des certificats permettant à l’utilisateur de s’authentifier auprès du service Azure Rights Management, pour consommer du contenu protégé et protéger du contenu hors connexion.

Une copie du certificat de l’utilisateur est stockée dans Azure afin que, si l’utilisateur utilise un autre appareil, les certificats soient créés en utilisant les mêmes clés.

### <a name="content-protection"></a>Protection du contenu
Quand un utilisateur protège un document, le client RMS effectue les actions suivantes sur un document non protégé :

![Protection de document RMS : étape 1](../media/AzRMS_documentprotection1.png)

**Ce qui se passe à l’étape 1** : le client RMS crée une clé aléatoire (la clé de contenu), puis chiffre le document en utilisant cette clé, avec l’algorithme de chiffrement symétrique AES.

![Protection de document RMS : étape 2](../media/AzRMS_documentprotection2.png)

**Ce qui se passe à l’étape 2** : le client RMS crée ensuite un certificat incluant une stratégie pour le document, soit en se basant sur un modèle, soit en spécifiant des droits spécifiques pour le document. Cette stratégie inclut les droits de différents utilisateurs ou groupes, ainsi que d'autres restrictions telles qu'une date d'expiration.

Le client RMS utilise ensuite la clé de l'organisation obtenue lors de l'initialisation de l'environnement utilisateur, en se servant de cette clé pour chiffrer la stratégie et la clé symétrique de contenu. Le client RMS signe également la stratégie avec le certificat de l'utilisateur obtenu lors de l'initialisation de l'environnement utilisateur.

![Protection de document RMS : étape 3](../media/AzRMS_documentprotection3.png)

**Ce qui se passe à l’étape 3 **: enfin, le client RMS incorpore la stratégie dans un fichier avec le corps du document précédemment chiffré, pour constituer un document protégé.

Ce document peut être stocké partout, ou partagé à l'aide de n'importe quelle méthode, et la stratégie reste toujours associée au document chiffré.

### <a name="content-consumption"></a>Consommation du contenu
Quand un utilisateur veut consommer un document protégé, le client RMS commence par demander l’accès au service Azure Rights Management :

![Consommation de document RMS : étape 1](../media/AzRMS_documentconsumption1.png)

**Ce qui se passe à l’étape 1 **: l’utilisateur authentifié envoie la stratégie de document et les certificats de l’utilisateur au service Azure Rights Management. Le service déchiffre et évalue la stratégie, puis génère la liste des droits (éventuels) de l'utilisateur sur le document.

![Consommation de document RMS : étape 2](../media/AzRMS_documentconsumption2.png)

**Ce qui se passe à l’étape 2** : le service extrait ensuite la clé de contenu AES de la stratégie déchiffrée. Cette clé est alors chiffrée avec la clé RSA publique de l'utilisateur obtenue avec la demande.

Après cela, la clé de contenu re-chiffrée est incorporée dans une licence d'utilisation chiffrée avec la liste des droits de l'utilisateur, qui est renvoyée au client RMS.

![Consommation de document RMS : étape 3](../media/AzRMS_documentconsumption3.png)

**Ce qui se passe à l’étape 3** : enfin, le client RMS prend la licence d’utilisation chiffrée et la déchiffre avec sa propre clé privée utilisateur. Cela permet au client RMS de déchiffrer le corps du document si nécessaire, et de l'afficher à l'écran.

Le client déchiffre également la liste des droits, et transmet ceux-ci à l'application qui les applique dans son interface utilisateur.

### <a name="variations"></a>Variantes
Les procédures pas à pas précédentes couvrent les scénarios standard, mais il existe des variantes :

-   **Appareils mobiles** : quand des appareils mobiles protègent ou consomment des fichiers avec le service Azure Rights Management, les flux du processus sont beaucoup plus simples. Les appareils mobiles ne passent pas par le processus d'initialisation utilisateur, car chaque transaction (pour protéger ou consommer du contenu) est indépendante. Comme avec les ordinateurs Windows, les appareils mobiles se connectent au service Azure Rights Management et s’authentifient. Pour protéger du contenu, les appareils mobiles soumettent une stratégie, puis le service Azure Rights Management leur envoie une licence de publication et une clé symétrique pour protéger le document. Pour consommer du contenu, quand des appareils mobiles se connectent au service Azure Rights Management et s’authentifient, ils envoient la stratégie de document au service Azure Rights Management et demandent une licence d’utilisation pour consommer le document. En réponse, le service Azure Rights Management leur envoie les clés nécessaires et les restrictions. Les deux processus utilisent TLS pour protéger l'échange de clés et d'autres communications.

-   **Connecteur RMS** : quand le service Azure Rights Management est utilisé avec le connecteur RMS, le flux du processus reste identique. La seule différence est que le connecteur fait office de relais entre les services locaux (comme Exchange Server et SharePoint Server) et le service Azure Rights Management. Le connecteur proprement dit n'effectue aucune opération telle qu'une initialisation de l'environnement utilisateur, un chiffrement ou un déchiffrement. Il relaie simplement la communication qui accède généralement à un serveur AD RMS, en gérant la traduction entre les protocoles utilisés de part et d'autre. Ce scénario vous permet d’utiliser le service Azure Rights Management avec des services locaux.

-   **Protection générique (.pfile)** : quand le service Azure Rights Management protège un fichier de façon générique, le flux est fondamentalement le même pour la protection du contenu, sauf que le client RMS crée une stratégie qui accorde tous les droits. Lorsque le fichier est consommé, il est déchiffré avant d'être transmis à l'application cible. Ce scénario vous permet de protéger tous les fichiers, même s'ils ne prennent pas en charge RMS en mode natif.

-   **PDF protégé (.ppdf)** : quand le service Azure Rights Management protège un fichier Office en mode natif, il en crée également une copie qu’il protège de la même façon. La seule différence est que la copie est un fichier au format PPDF, que l'application de partage RMS peut ouvrir en mode affichage. Ce scénario vous permet d'envoyer des pièces jointes protégées par courrier électronique, en sachant que le destinataire sur un appareil mobile sera toujours en mesure de les lire, même si son appareil n'a pas d'application prenant en charge en mode natif des fichiers Office protégés.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur le service Azure Rights Management, reportez-vous aux autres articles de la section **Comprendre et explorer**, comme [Comment les applications prennent en charge le service Azure Rights Management](applications-support.md), pour savoir comment intégrer vos applications existantes avec Azure Rights Management afin de bénéficier d’une solution de protection des informations. 

Consultez [Terminologie liée à Azure Information Protection](../get-started/terminology.md) pour vous familiariser avec les termes que vous allez rencontrer lors de la configuration et de l’utilisation du service Azure Rights Management, et n’oubliez pas de lire aussi [Requirements for Azure Information Protection](../get-started/requirements-azure-rms.md) avant d’entamer votre déploiement. Si vous voulez vous y plonger directement et essayer par vous-même, utilisez le [Didacticiel de démarrage rapide pour Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Si vous êtes prêt à déployer la protection des données pour votre organisation, utilisez la [Feuille de route pour le déploiement d’Azure Information Protection](../plan-design/deployment-roadmap.md) pour connaître les étapes de déploiement et accéder à des liens vers des instructions.

> [!TIP]
> Pour obtenir plus d’informations et de l’aide supplémentaire, utilisez les ressources et les liens dans [Informations et support pour Azure Information Protection](../get-started/information-support.md).



<!--HONumber=Nov16_HO1-->


