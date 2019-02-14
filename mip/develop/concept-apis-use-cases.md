---
title: Concepts – API dans le kit SDK MIP
description: Cet article vous aidera à comprendre 3 types d’API figurant dans le kit SDK MIP et les liens qu’ils partagent, et il présente des cas d’utilisation pour chacun d’eux.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 10/16/2018
ms.author: bryanla
ms.openlocfilehash: 1dddb9834a0cc7b365a2294bbad3611e4d01870a
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252399"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Kit SDK Microsoft Information Protection – Concepts liés aux API

Le SDK Microsoft Information Protection (MIP) se compose de trois API, comme illustré dans le diagramme suivant :

[![Diagramme des API du SDK MIP](media/concept-apis-use-cases/mip-sdk-components.png)](media/concept-apis-use-cases/mip-sdk-components.png#lightbox)

En fonction des besoins de votre application, vous souhaiterez peut-être intervenir au niveau de la couche de l’API de fichier ou utiliser directement les couches des API de stratégie ou de protection.

## <a name="file-api"></a>API de fichier

L’API de fichier est une abstraction des deux API de protection et de stratégie. Elle fournit des interfaces faciles à utiliser pour la lecture des étiquettes du service, l’application d’étiquettes à des types de fichiers définis et la lecture des étiquettes de ces types de fichiers. L’API de fichier est utilisée par tout service ou toute application où :

- un type de fichier pris en charge est impliqué
- des étiquettes doivent être lues ou écrites
- le contenu doit être protégé ou déchiffré

### <a name="file-api-use-cases"></a>Cas d’utilisation de l’API de fichier

- Vous êtes un ingénieur logiciel auprès d’un établissement de services financiers. Vous voulez être sûr que les données issues de vos applications métier, généralement exportées au format Excel, soient étiquetées lors de l’exportation en fonction de leur contenu. Vous pouvez utiliser l’API de fichier pour lister les étiquettes disponibles et pour appliquer l’étiquette appropriée à un format de fichier pris en charge.

- Votre organisation développe un répartiteur de sécurité d’accès cloud (CASB). Vos clients demandent la possibilité d’appliquer des étiquettes MIP aux documents Microsoft Office et PDF. L’API de fichier vous permet d’afficher la liste des étiquettes configurées, puis d’autoriser vos clients à créer des règles qui appliquent une étiquette spécifique. L’API de fichier, acceptant l’ID d’étiquette, traite le reste des fichiers répondant aux critères du client.

- Votre organisation fournit une solution de protection contre la perte de données basée sur un service ou un CASB qui supervise les activités des fichiers des applications SaaS. Pour réduire le risque de perte ou d’exposition des données quand celles-ci sont protégées avec MIP, votre service doit analyser le contenu des fichiers protégés. À l’aide de l’API de fichier pour les formats pris en charge, quand le service est un utilisateur privilégié, il peut :

  1. supprimer la protection
  2. analyser le contenu à la recherche d’éléments restreints ou sensibles
  3. ignorer le résultat en texte clair
  4. appliquer une règle de service pour signaler ou atténuer un risque, le cas échéant

## <a name="policy-api"></a>API de stratégie

L’API de stratégie, ou moteur de stratégie universel (UPE), permet aux développeurs de logiciels de récupérer des stratégies d’étiquetage pour un utilisateur spécifique. Elle peut ensuite « calculer » les actions que ces étiquettes doivent entreprendre.

L’API de stratégie est principalement utilisée par les applications clientes, où le développeur contrôle l’interface et le format de fichier. Elle est également utilisée quand vous devez juste récupérer la stratégie utilisateur, et pas étiqueter les fichiers directement. 

### <a name="policy-api-use-cases"></a>Cas d’utilisation de l’API de stratégie

- Votre organisation développe un logiciel de conception 3D qui utilise un format de fichier propriétaire. Vos clients utilisent MIP et veulent appliquer des étiquettes en mode natif par le biais de votre application. En tant qu’ingénieur logiciel, vous utilisez l’API de stratégie et un contrôle personnalisé pour afficher les étiquettes disponibles pour l’utilisateur authentifié. Une fois que l’utilisateur sélectionne une étiquette, vous appelez la méthode d’action de calcul de l’API. L’API vous indique exactement ce qui doit être appliqué en matière de métadonnées, de marquage de contenu et de protection.

- Votre organisation développe un service DLP (Data Loss Prevention) qui permet à vos clients de configurer des stratégies DLP via un portail d’administration centrale. Vous avez des clients qui utilisent MIP et avez besoin de lire ou d’appliquer des étiquettes AIP dans le cadre des stratégies DLP. En tant qu’ingénieur logiciel, vous pouvez utiliser l’API de stratégie pour obtenir une liste d’étiquettes pour l’organisation du client. Vous pouvez ensuite lire ces étiquettes comme partie d’une règle DLP, ou appliquer les informations d’étiquette comme action de règle.

## <a name="protection-api"></a>API de protection

L’API de protection permet aux développeurs de logiciels de convertir les flux de texte en clair en flux gérés par des droits et vice versa.

### <a name="protection-api-use-cases"></a>Cas d’utilisation de l’API de protection

- Votre organisation développe un logiciel d’impression 3D utilisant un format de fichier propriétaire. Vous souhaitez utiliser MIP pour protéger ce fichier, afin qu’il puisse être imprimé uniquement par des utilisateurs spécifiques. L’API de protection vous permet d’appliquer une protection au fichier afin que seuls les consommateurs autorisés puissent l’ouvrir et l’imprimer. 

- Votre organisation développe une solution eDiscovery qui traite les boîtes aux lettres Exchange et les fichiers .PST. Votre application doit autoriser les utilisateurs à déchiffrer les messages pour effectuer des opérations e-Discovery. À l’aide d’un analyseur de message/RPMSG personnalisé et d’un compte disposant des privilèges suffisants, vous pouvez utiliser l’API RMS pour :
  - déchiffrer le fichier chiffré
  - analyser le contenu
  - ignorer si hors de portée ou empaqueter si dans la portée

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez une idée générale sur les API MIP disponibles et la manière dont elles sont utilisées, poursuivez avec les [concepts liés aux objets de profil et de moteur](concept-profile-engine-cpp.md). Ces concepts sont fondamentaux et s’appliquent à tous les ensembles d’API de MIP.
