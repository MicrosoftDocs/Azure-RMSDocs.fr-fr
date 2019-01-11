---
title: Bonnes pratiques de sécurité pour Information Protection
description: Vous développez de meilleures applications compatibles RMS en suivant les bonnes pratiques pour Information Protection.
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 12/13/2018
ms.topic: conceptual
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 3b22a8723a232cd05349a19987686c25dc5f320f
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54070296"
---
# <a name="security-best-practices-for-information-protection"></a>Bonnes pratiques de sécurité pour Information Protection

Les kits SDK Information Protection fournissent un système robuste pour publier et utiliser tous les types d’informations protégées. Pour rendre un système aussi fort que possible, les applications compatibles avec Information Protection doivent être créées en respectant des bonnes pratiques. Les applications partagent la responsabilité de la gestion de la sécurité de cet écosystème. L’identification des risques de sécurité et la limitation de ces risques introduits au cours du développement d’applications permet de réduire la probabilité d’une implémentation logicielle moins sécurisée.

Ces informations complètent l’accord juridique qui doit être signé afin d’obtenir les certificats numériques pour les applications utilisant les kits SDK.

## <a name="subjects-not-covered"></a>Sujets non abordés

Bien que les sujets suivants constituent des points importants dans la création d’un environnement de développement et d’applications sécurisées, ils n’entrent pas dans le cadre de cet article :

- **Gestion de processus de développement logiciel** : gestion de la configuration, sécurisation du code source, limitation des accès au code débogué et affectation de priorités aux bogues. Pour certains clients, il est capital de disposer d’un processus de développement de logiciels plus sécurisé. Certains clients prescrivent même un processus de développement.
- **Erreurs de codage courantes** : informations sur la prévention des dépassements de mémoire tampon. Nous vous recommandons la version la plus récente de Writing Secure Code par Michael Howard et David LeBlanc (Microsoft Press, 2002) pour passer en revue ces menaces génériques et les solutions possibles.
- **Ingénierie sociale** : inclut des informations sur les dispositifs de protection procéduraux et structurels qui vous permettent de vous protéger contre l’exploitation du code par des développeurs ou d’autres personnes au sein de l’organisation du fabricant.
- **Sécurité physique** : inclut des informations sur le verrouillage de l’accès à votre base de code et la signature de certificats.
- **Déploiement ou distribution de logiciels en version préliminaire** : inclut des informations sur la distribution de votre logiciel bêta.
- **Gestion de réseau** : inclut des informations sur les systèmes de détection d’intrusion sur vos réseaux physiques.

## <a name="threat-models-and-mitigations"></a>Modèles de menace et prévention

Les propriétaires d’informations numériques doivent être en mesure d’évaluer les environnements dans lesquels leurs ressources seront déchiffrées. Une déclaration des normes de sécurité minimales fournit aux propriétaires d’informations un cadre leur permettant de comprendre et d’évaluer le niveau de sécurité des applications.

Certains secteurs, tels que le gouvernement et les soins de santé, incluent des processus de certification et d’accréditation et des normes qui peuvent s’appliquer à votre produit. Répondre à ces recommandations de sécurité minimales ne constitue pas un substitut aux besoins d’accréditation uniques de vos clients. Toutefois, les normes de sécurité ont pour but de vous aider à répondre aux besoins actuels et futurs de vos clients, et aucun investissement effectué au début du cycle de développement ne profitera à votre application. Ces directives sont des recommandations : elles ne constituent pas un programme de certification Microsoft formel.

Il existe plusieurs catégories principales de vulnérabilités dans un système Rights Management Services, notamment :

- **Fuite** : des informations apparaissent dans des emplacements non autorisés.
- **Corruption** : un logiciel ou des données sont modifiés de façon non autorisée.
- **Refus** : une ressource informatique n’est pas disponible pour être utilisée.

Ces rubriques portent principalement sur les problèmes de fuites. L’intégrité d’un système d’API dépend de sa capacité, au fil du temps, à protéger les informations et à autoriser l’accès seulement à des entités désignées. Ces rubriques abordent également les problèmes de corruption. Les problèmes de refus ne sont pas couverts.

Microsoft ne teste pas et ne passe pas en revue les résultats des tests liés au respect de la norme minimale. Le partenaire est responsable du respect des normes minimales. Microsoft fournit deux niveaux supplémentaires de recommandations pour aider à limiter les menaces courantes. En règle générale, ces suggestions sont cumulatives. Par exemple, le respect des recommandations préférées implique que vous respectez les normes minimales là où elles sont applicables, sauf indication contraire.

|Niveau de norme|Description|
|---|---|
|Norme minimale| Une application qui traite des informations protégées doit répondre à la norme minimale pour qu’elle puisse être signée avec le certificat de production reçu de Microsoft. Les partenaires utilisent généralement le certificat de hiérarchie de production, au moment de la publication finale du logiciel. Les tests internes propres à un partenaire sont utilisés pour vérifier si l’application répond à cette norme minimale. Le respect de la norme minimale n’est pas et ne doit pas être considéré comme une garantie de sécurité par Microsoft. Microsoft ne teste pas ni ne vérifie les résultats des tests liés au respect de la norme minimale. Le partenaire est responsable du respect de ce minimum.|
|Norme recommandée| Les instructions recommandées permettent d’optimiser la sécurité des applications et d’indiquer de quelle manière le SDK peut évoluer à mesure que des critères de sécurité supplémentaires sont implémentés. Les fournisseurs peuvent différencier leurs applications en développant selon ce niveau plus élevé des directives de sécurité.|
|Norme préférée| Cette norme est la catégorie de sécurité la plus élevée actuellement définie. Les fournisseurs qui développent des applications commercialisées comme hautement sécurisées doivent respecter cette norme. Les applications conformes à cette norme sont susceptibles d’être moins vulnérables aux attaques.|

## <a name="malicious-software"></a>Logiciel malveillant

Microsoft a défini des normes minimales requises que votre application doit respecter pour protéger le contenu contre des logiciels malveillants.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importation de logiciels malveillants avec des tables d’adresses

Le SDK Information Protection ne prend pas en charge la modification de code à l’exécution ni la modification de la table d’adresses d’importation (IAT). Une table d’adresses d’importation est créée pour chaque DLL chargée dans votre espace de processus. Elle spécifie les adresses de toutes les fonctions importées par votre application. Une attaque courante consiste à modifier les entrées de la table IAT au sein d’une application, par exemple pour qu’elle pointe vers des logiciels malveillants. Le SDK arrête l’application quand il détecte ce type d’attaque.

### <a name="minimum-standard"></a>Norme minimale

- Vous ne pouvez pas modifier la table d’adresses d’importation dans le processus de l’application pendant l’exécution. Votre application spécifie la plupart des fonctions appelées au moment de l’exécution à l’aide de tables d’adresses. Ces tables ne peuvent pas être modifiées pendant ou après l’exécution. Entre autres choses, cette restriction signifie que vous ne pouvez pas effectuer le profilage de code dans une application signée à l’aide du certificat de production.
- Vous ne pouvez pas appeler la fonction **DebugBreak** à partir des DLL spécifiées dans le manifeste.
- Vous ne pouvez pas appeler **LoadLibrary** si l’indicateur **DONT_RESOLVE_DLL_REFERENCES** est défini. Cet indicateur signale au chargeur d’ignorer la liaison aux modules importés, modifiant ainsi la table d’adresses d’importation.
- Vous ne pouvez pas modifier le chargement différé en apportant des modifications au commutateur d’éditeur de liens /DELAYLOAD à l’exécution ou après celle-ci.
- Vous ne pouvez pas modifier le chargement différé en fournissant votre propre version de la fonction helper Delayimp.lib.
- Vous ne pouvez pas décharger des modules qui ont été chargés en différé par des modules authentifiés alors que l’environnement du SDK Information Protection existe.
- Vous ne pouvez pas utiliser le commutateur d’éditeur de liens **`/DELAY:UNLOAD`** pour activer le déchargement de modules différés.

## <a name="incorrectly-interpreting-license-rights"></a>Interprétation incorrecte des droits de licence

Si votre application n’interprète pas et n’applique pas correctement les droits spécifiés dans la licence d’émission du SDK, vous pouvez rendre des informations disponibles de différentes façons non prévues par le propriétaire. Par exemple, quand l’application permet à un utilisateur d’enregistrer des informations non chiffrées sur un nouveau support, alors que la licence d’émission confère uniquement le droit de les afficher.

### <a name="azure-information-protection-aip"></a>Azure Information Protection (AIP)

Le système de protection des informations organise les droits selon plusieurs regroupements. Pour plus d’informations, consultez [Configuration des droits d’utilisation pour Azure Rights Management](../configure-usage-rights.md).

Azure Information Protection permet à un utilisateur de déchiffrer ou non des informations. Les informations n’ont en soi aucune protection. Si un utilisateur dispose du droit de déchiffrer, l’API l’y autorise. L’application est responsable de la gestion ou de la protection de ces informations une fois que celles-ci sont en texte clair. Une application est responsable de la gestion de son environnement et de son interface pour empêcher l’utilisation non autorisée d’informations. Par exemple, la désactivation des boutons **Imprimer** et **Copier** si une licence accorde uniquement le droit VIEW (AFFICHER). La suite de tests doit vérifier que votre application fonctionne correctement avec tous les droits de licence qu’elle reconnaît.

### <a name="minimum-standard"></a>Norme minimale

- L’implémentation par le client de droits XrML v.1.2 doit être cohérente avec les définitions de ces droits, comme décrit dans les spécifications XrML disponibles sur le site web de XrML (http://www.xrml.org). Tout droit spécifique à votre application doit être défini pour toutes les entités qui présentent un intérêt dans votre application.
- Votre suite de tests et votre processus de test doit vérifier que votre application s’exécute correctement en fonction des droits qu’elle prend en charge. Elle doit également vérifier qu’elle **n’agit pas** en utilisant des droits non pris en charge.
- Si vous créez une application de publication, vous devez rendre disponible des informations expliquant les droits intrinsèques utilisés. Il s’agit des droits qui sont et de ceux qui ne sont pas pris en charge par l’application de publication, et de la façon dont ces droits doivent être interprétés. En outre, l’interface utilisateur doit indiquer clairement à l’utilisateur final les implications de chaque droit accordé ou refusé pour une information spécifique.
- Les droits abstraits inclus dans de nouveaux droits implémentés par une application doivent être mappés à la nouvelle terminologie. Par exemple, un nouveau droit appelé GESTIONNAIRE peut inclure des droits de COPIE, d’IMPRESSION et de MODIFICATION comme droits abstraits.

### <a name="recommended-standard"></a>Norme recommandée

Néant à l'heure actuelle.

### <a name="preferred-standard"></a>Norme préférée

Néant à l'heure actuelle.

## <a name="next-steps"></a>Étapes suivantes

Les bonnes pratiques pour implémenter des applications à l’aide du SDK Azure Information Protection incluent les articles suivants :

- [Modèles de menace et prévention](https://msdn.microsoft.com/library/aa362751.aspx)
- [Attaques de sécurité](https://msdn.microsoft.com/library/aa362736.aspx)
