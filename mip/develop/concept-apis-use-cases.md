---
title: Concepts – API dans le kit SDK MIP
description: Cet article vous aidera à comprendre 3 types d’API figurant dans le kit SDK MIP et les liens qu’ils partagent, et il présente des cas d’utilisation pour chacun d’eux.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a625df159a00a955d155850ff4e326d1e0d204e5
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453330"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux API

Le kit SDK MIP est composé de trois API :

- [API de protection](#protection-api)
- [API de stratégie](#policy-api)
- [API de fichier](#file-api)

## <a name="protection-api"></a>API de protection

L’API de protection permet aux développeurs de logiciels de convertir les flux de texte en clair en flux gérés par des droits et vice versa.

### <a name="protection-api-use-cases"></a>Cas d’utilisation de l’API de protection

- Votre organisation développe un logiciel d’impression 3D utilisant un format de fichier propriétaire. Vous souhaitez utiliser MIP pour protéger ce fichier, afin qu’il puisse être imprimé uniquement par des utilisateurs spécifiques. L’API de protection vous permet d’appliquer une protection au fichier afin que seuls des consommateurs autorisés soient en mesure de l’ouvrir et/ou de l’imprimer. 

- Votre organisation développe une solution eDiscovery qui traite les boîtes aux lettres Exchange et les fichiers PST. Votre application doit être en mesure de déchiffrer les messages afin de pleinement tirer parti d’eDiscovery. Vous pouvez utiliser un analyseur de message/RPMSG personnalisé et un compte disposant de privilèges suffisants pour exploiter l’API RMS afin de déchiffrer le fichier chiffré, d’analyser le contenu et d’ignorer ce dernier s’il n’est pas pertinent ou de créer un package s’il l’est.

## <a name="policy-api"></a>API de stratégie

L’API de stratégie, ou moteur de stratégie universel (UPE), permet aux développeurs de logiciels d’obtenir des stratégies d’étiquetage pour un utilisateur spécifique, puis de « calculer » les actions que ces étiquettes doivent prendre.

L’API de stratégie sera utilisée principalement par les applications clientes pour lesquelles le développeur contrôle l’interface et le format de fichier ou pour lesquelles la seule exigence consiste à obtenir une stratégie d’utilisateur et pas nécessairement à étiqueter les fichiers directement. 

### <a name="policy-api-use-cases"></a>Cas d’utilisation de l’API de stratégie

- Votre organisation développe un logiciel de conception 3D qui utilise un format de fichier propriétaire. Vos clients utilisent Microsoft Information Protection et veulent pouvoir appliquer des étiquettes en mode natif par le biais de votre application. En tant qu’ingénieur logiciel, vous utiliseriez l’API de stratégie et un contrôle personnalisé pour afficher les étiquettes disponibles pour l’utilisateur authentifié. Une fois que l’utilisateur a sélectionné une étiquette, vous appelleriez la méthode d’action de calcul de l’API pour savoir exactement ce qui doit être appliqué en ce qui concerne les métadonnées, le marquage de contenu et la protection.

- Votre organisation développe un service DLP qui permet à vos clients de configurer des stratégies DLP via un portail d’administration centrale. Vous avez des clients qui utilisent Microsoft Information Protection et souhaitent être en mesure de lire ou d’appliquer des étiquettes AIP dans le cadre des stratégies DLP. En tant qu’ingénieur logiciel, vous pouvez utiliser l’API de stratégie pour obtenir la liste des étiquettes pour l’organisation cliente, puis lire ces étiquettes dans le cadre d’une règle DLP ou appliquer les informations d’étiquette dans le cadre d’une action de règle.

## <a name="file-api"></a>API de fichier

L’API de fichier est une abstraction des deux API de protection et de stratégie. Elle fournit des interfaces faciles à utiliser pour la lecture des étiquettes à partir du service, l’application des étiquettes sur des types de fichiers définis, ainsi que la lecture d’étiquettes à partir de ces types de fichiers. L’API de fichier sera utilisée par un service ou une application quelconque si un type de fichier pris en charge est impliqué et si des étiquettes doivent être lues ou écrites, ou si du contenu doit être protégé ou déchiffré.

### <a name="file-api-use-cases"></a>Cas d’utilisation de l’API de fichier

- Vous êtes un ingénieur logiciel auprès d’un établissement de services financiers. Vous voulez être sûr que les données issues de vos applications métier, généralement exportées au format Excel, soient étiquetées lors de l’exportation en fonction de leur contenu. L’API de fichier peut être utilisée pour répertorier les étiquettes disponibles puis pour appliquer l’étiquette appropriée à un format de fichier pris en charge.

- Votre organisation développe un répartiteur de sécurité d’accès cloud (CASB). Vos clients demandent la possibilité d’appliquer des étiquettes MIP aux documents Microsoft Office et PDF. L’API de fichier vous permettrait d’afficher la liste des étiquettes configurées, puis d’autoriser vos clients à générer des règles qui appliqueraient l’étiquette souhaitée. L’API de fichier, acceptant l’ID d’étiquette, traiterait le reste pour les fichiers répondant aux critères du client.

- Votre organisation fournit une solution de protection contre la perte de données basée sur un service et/ou un CASB qui supervise les activités de fichier des applications SaaS. Pour réduire le risque de perte ou d’exposition des données quand les données sont protégées avec MIP, votre service doit être en mesure d’analyser le contenu des fichiers protégés. En utilisant l’API de fichier pour les formats pris en charge, lorsque le service est un utilisateur privilégié, vous pouvez supprimer la protection, analyser le contenu à la recherche d’un contenu limité ou sensible, ignorer le résultat en texte clair et appliquer une règle de service pour signaler ou gérer le risque éventuellement trouvé.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez une idée générale sur les API MIP disponibles et la manière dont elles sont utilisées, poursuivez avec les [concepts liés aux objets de profil et de moteur](concept-profile-engine-cpp.md). Ces concepts sont fondamentaux et s’appliquent à tous les ensembles d’API de MIP.