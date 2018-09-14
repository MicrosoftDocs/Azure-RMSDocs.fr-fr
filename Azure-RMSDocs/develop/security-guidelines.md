---
title: Bonnes pratiques de sécurité | Microsoft Information Protection
description: Vous développez de meilleures applications compatibles RMS en suivant les bonnes pratiques Azure Information Protection.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 88c1ce2cc09bedb35bb91f9eb0af7b8a1f955ec4
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148016"
---
# <a name="security-best-practices-for-azure-information-protection"></a>Bonnes pratiques de sécurité pour Azure Information Protection

Le Kit SDK Azure Information Protection (AIP) fournit un système robuste pour la publication et l’utilisation de tous les types d’informations protégées. Pour rendre un système AIP aussi fort que possible, les applications compatibles AIP doivent être créées sur la base des bonnes pratiques AIP. Les applications compatibles AIP partagent la responsabilité de la maintenance de la sécurité de cet écosystème. L’identification des risques de sécurité et la limitation de ces risques introduits au cours du développement d’applications permet de réduire la probabilité d’une implémentation logicielle moins sécurisée.

Les bonnes pratiques d’implémentation d’applications à l’aide du Kit SDK Azure Information Protection incluent les catégories de suggestion suivantes :
- [Modèles de menace et prévention](https://msdn.microsoft.com/library/aa362751.aspx)
- [Attaques de sécurité](https://msdn.microsoft.com/library/aa362736.aspx)

Ces informations complètent l’accord juridique qui doit être signé afin d’obtenir les certificats numériques nécessaires pour implémenter des applications à l’aide du SDK AIP.

## <a name="subjects-not-covered-in-these-topics"></a>Sujets non traités dans ces rubriques
Ces rubriques décrivent brièvement les problèmes suivants, qui sont significatifs lorsque vous tentez de créer un environnement de développement et une application sécurisée :
- **Gestion de processus de développement logiciel** : inclut des informations sur la gestion de la configuration, la sécurisation du code source, la limitation des accès au code débogué et l’affectation de priorité aux bogues. Pour certains de vos clients, il est capital de disposer d’un processus de développement de logiciels plus sécurisé. Certains clients prescrivent même un processus de développement.
- **Erreurs de codage courantes** : inclut des informations sur la prévention des dépassements de mémoire tampon. Nous vous recommandons la version la plus récente de Writing Secure Code par Michael Howard et David LeBlanc (Microsoft Press, 2002) pour passer en revue ces menaces génériques et les solutions possibles.
- **Ingénierie sociale** : inclut des informations sur les dispositifs de protection procéduriers et structurels qui vous permettent de vous protéger contre l’exploitation du code par des développeurs ou d’autres personnes au sein de l’organisation du fabricant.
- **Sécurité physique** : inclut des informations sur le verrouillage de l’accès à votre base de code et la signature de certificats.
- **Déploiement ou distribution de logiciels en version préliminaire** : inclut des informations sur la distribution de votre logiciel bêta.
- **Gestion de réseau** : inclut des informations sur les systèmes de détection d’intrusion sur vos réseaux physiques.

## <a name="threat-models-and-mitigations"></a>Modèles de menace et prévention
Les propriétaires d’informations numériques doivent être en mesure d’évaluer les environnements dans lesquels leurs ressources seront déchiffrées. Une instruction de normes de sécurité minimales peut fournir aux propriétaires d’informations un cadre leur permettant de comprendre et évaluer le niveau de sécurité des applications auxquelles ils confient leurs informations.

Certains secteurs, tels que le gouvernement et les soins de santé, incluent des processus de certification et d’accréditation et des normes qui peuvent s’appliquer à votre produit. Répondre à ces recommandations de sécurité minimale ne constitue pas un substitut aux besoins d’accréditation uniques de vos clients. Toutefois, les normes de sécurité ont pour but de vous aider à répondre aux besoins actuels et futurs de vos clients, et aucun investissement effectué au début du cycle de développement ne profitera à votre application. Il s’agit de recommandations, et non d’un programme de certification Microsoft formel.

Il existe plusieurs catégories principales de vulnérabilités dans un système Rights Management Services, notamment :
- **Fuite** : des informations apparaissent dans des emplacements non autorisés.
- **Corruption** : un logiciel ou des données sont modifiés de façon non autorisée.
- **Déni** : une ressource informatique n’est pas disponible pour être utilisée.

Ces rubriques portent principalement sur les problèmes de fuites. L’intégrité d’un système API dépend de sa capacité, au fil du temps, à protéger les informations et à autoriser l’accès uniquement à des entités désignées. Ces rubriques abordent également les problèmes de corruption. Les problèmes de déni ne sont pas couverts.

Microsoft n’effectue pas de tests ou ne révise pas les résultats de tests liés au respect de la norme minimale. Il incombe entièrement au partenaire de garantir que les normes minimales sont respectées. Microsoft fournit deux niveaux supplémentaires de recommandations pour aider à limiter les menaces courantes. En règle générale, ces suggestions sont additionnelles. Par exemple, respecter les principales recommandations implique que vous respectez les normes minimales, le cas échéant, sauf indication contraire.

|Niveau de norme|    Description|
|---|---|
|Norme minimale|  Une application qui traite des informations protégées par AIP doit être déterminée pour répondre à la norme minimale avant que l’application ne puisse être signée avec le certificat de production reçu de Microsoft. Les partenaires utilisent généralement le certificat de hiérarchie de production uniquement au moment de la version finale du logiciel lorsque les propres tests internes du partenaire ont vérifié que l’application répond à cette norme minimale. Le respect de la norme minimale n’est pas et ne doit pas être considéré comme une garantie de sécurité par Microsoft. Microsoft n’effectue pas de tests ou ne révise pas les résultats de tests liés au respect de la norme minimale. Il incombe entièrement au partenaire de garantir que les minimums sont respectés.|
|Norme recommandée|  Les instructions recommandées permettent d’optimiser la sécurité des applications et d’indiquer de quelle manière AIP peut évoluer à mesure que des critères de sécurité supplémentaires sont implémentés. Les fournisseurs peuvent tenter de différencier leurs applications en développant ce niveau supérieur d’instructions de sécurité.|
|Norme préférée|    Il s’agit de la catégorie de sécurité la plus élevée actuellement définie. Les fournisseurs qui développent des applications commercialisées comme hautement sécurisées doivent respecter cette norme. Les applications conformes à cette norme sont susceptibles d’être moins vulnérables aux attaques.|




## <a name="malicious-software"></a>Logiciels malveillants
Microsoft a défini des normes minimales requises que votre application doit respecter pour protéger le contenu contre des logiciels malveillants.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importation de logiciels malveillants à l’aide de tables d’adresses
AIP ne prend pas en charge la modification de code en cours d’exécution ou la modification de la table d’adresses d’importation (IAT). Une table d’adresses d’importation est créée pour chaque DLL chargée dans votre espace de processus. Elle spécifie les adresses de toutes les fonctions importées par votre application. Une attaque courante consiste à modifier les entrées de la table IAT au sein d’une application, par exemple pour qu’elle pointe vers des logiciels malveillants. AIP arrête l’application lorsqu’il détecte ce type d’attaque.

### <a name="minimum-standard"></a>Norme minimale
- Vous ne pouvez pas modifier la table d’adresses d’importation dans le processus d’application pendant l’exécution. -Votre application spécifie la plupart des fonctions appelées au moment de l’exécution à l’aide de tables d’adresses, qui ne peuvent pas être modifiées pendant ou après l’exécution. Entre autres choses, cela signifie que vous ne pouvez pas effectuer le profilage de code dans une application signée à l’aide du certificat de production.
- Vous ne pouvez pas appeler la fonction **DebugBreak** à partir de n’importe quel fichier DLL spécifié dans le manifeste.
- Vous ne pouvez pas appeler **LoadLibrary** si l’indicateur **DONT_RESOLVE_DLL_REFERENCES** est défini. Cet indicateur signale au chargeur d’ignorer la liaison aux modules importés, modifiant ainsi la table d’adresses d’importation.
- Vous ne pouvez pas modifier le chargement différé en exécutant le commutateur d’éditeur de liens /DELAYLOAD ou en y apportant des modifications ultérieures.
- Vous ne pouvez pas modifier le chargement différé en fournissant votre propre version de la fonction d’assistance Delayimp.lib.
- Vous ne pouvez pas décharger des modules qui ont été chargés en différé par les modules authentifiés alors que l’environnement AIP existe.
- Vous ne pouvez pas utiliser le commutateur d’éditeur de liens **/DELAY:UNLOAD** pour activer le déchargement de modules différés.


## <a name="incorrectly-interpreting-license-rights"></a>Interprétation incorrecte des droits de licence

Si votre application n’interprète pas et n’applique pas correctement les droits spécifiés dans la licence d’émission AIP, vous pouvez rendre des informations disponibles de manières non prévues par le propriétaire. Par exemple, l’application peut permettre à un utilisateur d’enregistrer des informations non chiffrées sur un nouveau support alors que la licence d’émission confère uniquement le droit de les afficher.

Le système AIP organise les droits de plusieurs regroupements. Pour plus d’informations, consultez [Configuration des droits d’utilisation pour Azure Rights Management](../configure-usage-rights.md).

### <a name="azure-information-protection"></a>Azure Information Protection  
L’API autorise ou non un utilisateur à déchiffrer des informations . Les informations ne comprennent aucune protection inhérente. Si un utilisateur dispose de droits pour déchiffrer des informations, l’API l’y autorise, et l’application est responsable de la gestion ou de la protection de ces informations lorsqu’elles sont déchiffrées. Une application est responsable de la gestion de son environnement et de son interface pour empêcher une utilisation non autorisée d’informations, par exemple en désactivant les boutons **Imprimer** et **Copier** si une licence accorde uniquement un droit de LECTURE. La suite de tests doit vérifier que votre application fonctionne correctement avec tous les droits de licence qu’elle reconnaît.

### <a name="minimum-standard"></a>Norme minimale
- L’implémentation par le client de droits XrML v.1.2 doit être cohérente avec les définitions de ces droits, comme décrit dans les spécifications XrML disponibles sur le site web de XrML (http://www.xrml.org). Tout droit spécifique à votre application doit être défini pour toutes les entités qui présentent un intérêt dans votre application.
- Votre processus de suite de tests et de test doit vérifier que votre application s’exécute correctement en fonction des droits qu’elle prend en charge et qu’elle n’agit pas sur la base de droits non pris en charge.
- Si vous développez une application de publication, vous devez rendre des informations disponibles expliquant les droits intrinsèques et les droits non pris en charge par l’application de publication, ainsi que la manière dont ces droits doivent être interprétés. En outre, l’interface utilisateur doit indiquer clairement à l’utilisateur final les implications de chaque droit accordé ou refusé pour une information spécifique.

- Tout droit abstrait inclus dans de nouveaux droits implémentés par une application doit être mappé sur la nouvelle terminologie. Par exemple, un nouveau droit appelé GESTIONNAIRE peut inclure des droits de COPIE, d’IMPRESSION et de MODIFICATION comme droits abstraits.
Norme recommandée : aucune à l’heure actuelle.
Norme préférée: aucune à l’heure actuelle.
