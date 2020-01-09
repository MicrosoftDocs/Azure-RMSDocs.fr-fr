---
title: Concepts-stockage de cache
description: Cet article vous aidera à comprendre les concepts relatifs au stockage du cache dans le kit de développement logiciel MIP.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: ed6407e99677bbed293959e15720c4c7d418aa54
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555821"
---
# <a name="microsoft-information-protection-sdk---cache-storage"></a>Kit de développement logiciel (SDK) Microsoft Information Protection-stockage cache

Le kit de développement logiciel MIP implémente une base de données SQLite3 pour gérer le stockage du cache du SDK. Avant la version 1,3 du kit de développement logiciel (SDK) Microsoft Information Protection, seuls deux types de stockage d’État du cache étaient pris en charge : sur disque et en mémoire. Ces deux types stockent certaines données, en particulier des licences pour le contenu protégé et des informations de stratégie, en texte en clair.

Pour améliorer la position de sécurité du kit de développement logiciel (SDK), nous avons ajouté la prise en charge d’un deuxième type de sur le cache disque qui utilise des API de chiffrement spécifiques à la plateforme pour protéger la base de données et son contenu.

L’application définit le type de cache lors du chargement du profil dans le cadre des objets `FileProfileSettings`, `PolicyProfileSettings`ou `ProtectionProfileSettings`. Le type de cache est statique pendant toute la durée de vie du profil. La modification d’un type de stockage de cache différent nécessite de détruire le profil existant et d’en créer un nouveau.

## <a name="cache-storage-types"></a>Types de stockage de cache

À compter de la version 1,3 du kit de développement logiciel MIP, les types de cache de stockage suivants sont disponibles.

| Tapez            | Fonction                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Mémoire        | Maintient le cache de stockage en mémoire dans l’application.                                                                       |
| OnDisk          | Stocke la base de données sur le disque dans le répertoire fourni dans l’objet Settings. La base de données est stockée en texte brut.              |
| OnDiskEncrypted | Stocke la base de données sur le disque dans le répertoire fourni dans l’objet Settings. La base de données est chiffrée à l’aide d’API propres au système d’exploitation. |

Chaque **moteur** généré par l’application génère une nouvelle clé de chiffrement.

Le stockage de cache est défini via l’un des objets de paramètres de profil, via l’énumération `mip::CacheStorageType`.

```cpp 
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted, // Define the storage type to use.
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());
```

## <a name="when-to-use-each-type"></a>Quand utiliser chaque type

Le stockage du cache est important pour conserver l’accès hors connexion aux informations précédemment déchiffrées, ainsi que pour garantir les performances des opérations de déchiffrement lorsque les données ont été précédemment consommées.

- **Dans le stockage en mémoire**: utilisez ce type de stockage pour les processus à long terme où la conservation des informations de la stratégie ou du cache de licence entre les redémarrages de service n’est pas nécessaire.
- **Sur disque**: utilisez ce type de stockage pour les applications où les processus peuvent s’arrêter et démarrer fréquemment, mais doivent tenir à jour la stratégie, la licence et le cache de découverte de service entre les redémarrages. Ce type de cache de stockage est en texte brut, ce qui est mieux adapté aux charges de travail de serveur où les utilisateurs n’ont pas accès au stockage d’État. Il peut s’agir, par exemple, d’un service Windows ou d’un démon Linux exécuté sur un serveur, ou d’une application SaaS dans laquelle seuls les administrateurs de service ont accès aux données d’État.
- **Sur disque et chiffré**: utilisez ce type de stockage pour les applications où les processus peuvent s’arrêter et démarrer fréquemment, mais doivent tenir à jour la stratégie, la licence et le cache de découverte de service entre les redémarrages. Ce cache de stockage étant chiffré, il est mieux adapté aux applications de station de travail où un utilisateur peut parcourir et découvrir la base de données d’État. Le chiffrement permet de s’assurer que les utilisateurs indiscrets n’ont pas accès à via le contenu de la stratégie ou le contenu de la licence de protection en texte brut. Il est important de noter que, dans tous les cas, les données sont chiffrées avec des clés auxquelles l’utilisateur peut accéder. Un adversaire compétent sera en mesure de déchiffrer le cache avec un minimum d’effort, mais cela empêche la falsification et la navigation.

## <a name="supported-platforms-for-encryption"></a>Plateformes prises en charge pour le chiffrement

| Plate-forme          | Version                | Remarques                                                                                                                               |
| ----------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft Windows | Windows 8 et versions ultérieures    | Windows 7 prend en charge uniquement CacheStorageType :: OnDisk                                                                                    |
| macOS             | High Sierra et versions ultérieures  |                                                                                                                                     |
| Ubuntu Linux      | 16,04 et versions ultérieures        | Requiert [SecretService](https://developer.gnome.org/libsecret/unstable/SecretService.html) et `LinuxEncryptedCache` indicateur de fonctionnalité. |
| Android           | Android 7,0 ou version ultérieure   |                                                                                                                                     |
| iOS               | Toutes les versions prises en charge |                                                                                                                                     |

Si le kit de développement logiciel MIP prend en charge d’autres distributions Linux, nous n’avons pas testé le chiffrement du cache sur RedHat Enterprise Linux, CentOS ou Debian.

> [!NOTE]
> L’indicateur de fonctionnalité permettant d’activer le stockage du cache sur Linux est défini via `mip::MipContext::CreateWithCustomFeatureSettings()`

## <a name="cache-storage-database-tables"></a>Tables de base de données de stockage de cache

Le SDK MIP gère deux bases de données pour le cache. L’une concerne les API de protection et la conservation des détails de l’état de la protection. L’autre concerne les API de stratégie et conserve les informations de service et les détails de la stratégie. Les deux sont stockées dans le chemin d’accès défini dans l’objet Settings, sous **mip\mip.Policies.sqlite3** et **mip\mip.protection.sqlite3**.

### <a name="protection-database"></a>Base de données de protection

| Table         | Fonction                                                        | Chiffré |
| ------------- | -------------------------------------------------------------- | --------- |
| AuthInfoStore | Stocke les détails de la demande d’authentification.                       | Non        |
| ConsentStore  | Stocke les résultats de consentement pour chaque moteur.                        | Non        |
| DnsInfoStore  | Stocke les résultats de la recherche DNS pour les opérations de protection du SDK        | Non        |
| EngineStore   | Stocke les détails du moteur, les utilisateurs associés et les données client personnalisées | Non        |
| KeyStore      | Stocke des clés de chiffrement symétriques pour chaque moteur.              | Oui       |
| LicenseStore  | Les magasins utilisent les informations de licence pour les données précédemment déchiffrées.  | Oui       |
| SdInfoStore   | Stocke les résultats de la découverte du service.                              | Non        |

### <a name="policy-database"></a>Base de données de stratégie

| Table           | Fonction                                                          | Chiffré |
| --------------- | ---------------------------------------------------------------- | --------- |
| KeyStore        | Stocke des clés de chiffrement symétriques pour chaque moteur.                | Oui       |
| Stratégies        | Stocke les informations de stratégie d’étiquette pour chaque utilisateur.                   | Oui       |
| PoliciesUrl     | Stocke l’URL du service de stratégie backend pour un utilisateur spécifique.             | Non        |
| Sensibilité     | Stocke des règles de classification pour une stratégie d’utilisateur spécifique.          | Oui       |
| SensitivityUrls | Stocke l’URL du service de stratégie de sensibilité du backend pour un utilisateur spécifique. | Non        |

## <a name="database-size-considerations"></a>Considérations relatives à la taille des bases de données

La taille de la base de données dépend de deux facteurs : la quantité de moteurs ajoutés au cache et la quantité de licences de protection qui ont été mises en cache. À compter du kit de développement logiciel (SDK) MIP 1,3, il n’existe aucun mécanisme pour nettoyer le cache de licences lorsqu’il expire. Il doit y avoir un processus externe pour supprimer le cache s’il dépasse le nombre souhaité.

Le contributeur le plus significatif à la croissance de la base de données sera le cache des licences de protection. Si la mise en cache des licences n’est pas nécessaire, soit parce que les allers-retours de service n’ont pas d’impact sur les performances de votre application, soit le cache peut devenir trop volumineux, le cache de licences peut être désactivé. Pour ce faire, affectez la valeur false `CanCacheLicenses` sur l’objet `FileProfile::Settings`.

```cpp
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted,
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetCanCacheLicenses(false);
```
