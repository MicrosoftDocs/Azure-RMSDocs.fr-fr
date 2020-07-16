---
title: Comment traiter des messages électroniques à l’aide du kit de développement logiciel MIP
description: Cet article vous aidera à comprendre le scénario d’utilisation de l’API de fichier du kit de développement logiciel MIP pour traiter les fichiers. MSG et. rpmsg.
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 074a0f6868796c68cf02a5a6cf4e105f9afeff19
ms.sourcegitcommit: 36413b0451ae28045193c04cbe2d3fb2270e9773
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86405213"
---
# <a name="file-api-email-message-file-processing"></a>Traitement du fichier de message électronique de l’API de fichier

Le SDK MIP prend en charge le déchiffrement et le chiffrement pour les messages électroniques. Les fichiers. MSG, générés par Outlook ou Exchange, ainsi que les fichiers. rpmsg sont pris en charge par le kit de développement logiciel (SDK), bien qu’ils soient légèrement différents de ceux que nous aborderons dans ce scénario.

Voici quelques-uns des cas d’utilisation populaires pour ce scénario :

- Déchiffrer les messages pour eDiscovery
- Déchiffrer le courrier et les pièces jointes pour l’inspection DLP
- Publier des messages protégés directement à partir d’applications métier
- Déchiffrer, modifier et reprotéger des messages en transit

## <a name="file-api-operations-for-msg-files"></a>Opérations de l’API de fichier pour les fichiers. MSG

L’API de fichier prend en charge les opérations de protection pour les fichiers. MSG et de manière identique à tout autre type de fichier, sauf que le kit de développement logiciel (SDK) a besoin de l’application pour activer l’indicateur de fonctionnalité MSG. 

> [!IMPORTANT]
> Les opérations d’étiquetage pour les fichiers. msg ne sont pas prises en charge actuellement.

Comme nous l’avons vu précédemment, l’instanciation de `mip::FileEngine` nécessite un objet de paramètre : `mip::FileEngineSettings`. `mip::FileEngineSettings`peut être utilisé pour passer des paramètres pour les paramètres personnalisés que l’application doit définir pour une instance particulière. La propriété CustomSettings de FileEngineSettings est utilisée pour définir l’indicateur pour `enable_msg_file_type` activer le traitement des fichiers. msg.

Le pseudo-code des opérations de protection du fichier. MSG peut se présenter comme suit :

- Définissez `enable_msg_file_type` l’indicateur dans `mip::FileEngineSettings` et ajoutez `mip::FileEngine` à `mip::FileProfile` .
- Utilisez l’API de protection pour répertorier les modèles de protection disponibles pour l’utilisateur.
- Construit `mip::FileHandler` qui pointe vers le fichier à protéger.
- Sélectionnez un modèle pour protéger et définir la protection du fichier à l’aide `mip::FileHandler` de la `SetProtection` méthode de.

Guide de démarrage rapide de l’API refer protection [: liste des modèles](quick-protection-list-templates-cpp.md) pour plus d’informations sur la façon de répertorier les modèles de protection.

## <a name="file-api-operations-for-rpmsg-files"></a>Opérations de l’API de fichier pour les fichiers. rpmsg

Le kit de développement logiciel MIP ne prend pas en charge les messages compatibles MIME (généralement EML). Au lieu de cela, le kit de développement logiciel (SDK) expose une fonction d’inspection permettant de déchiffrer le fichier **message. rpmsg** incorporé et de présenter un ensemble de flux d’octets comme sortie. C’est à l’utilisateur du kit de développement logiciel (SDK) d’extraire le fichier message. rpmsg et de le passer à l’API. Des variantes de ce nom de fichier existent pour les scénarios de chiffrement de messages Office et l’API accepte également les fichiers message_v2, v3 ou v4.

En règle générale, les services de passerelle de messagerie et de protection contre la perte de données traitent les messages MIME alors que la messagerie électronique est en transit. Lorsque le courrier est protégé, le contenu du message est stocké dans une pièce jointe, *message. rpmsg*. Ces pièces jointes contiennent le corps de l’e-mail chiffré et les pièces jointes qui faisaient partie du message d’origine. Le fichier *rpmsg* est l’attachement à un message électronique de wrappers en texte clair, puis envoyé au service de messagerie. Une fois que ce message quitte la limite Exchange ou Exchange Online, il est dans le format compatible MIME afin qu’il puisse être envoyé à sa destination.

Dans la plupart des cas, le partenaire DLP doit être en mesure d’obtenir les pièces jointes et les octets en texte clair du message à inspecter et à évaluer par rapport aux stratégies DLP. L’API d’inspection prend le message. rpmsg comme entrée et retourne des flux d’octets en tant que sortie. Ces flux d’octets contiennent les octets de texte en clair du message, ainsi que les pièces jointes. C’est au développeur de l’application de gérer ces flux et de faire des choses utiles avec eux (inspecter, déchiffrer de manière récursive, etc.).

L' `Inspect` API est implémentée par le biais d’une classe `mip::FileInspector` qui expose des opérations pour inspecter les types de fichiers pris en charge. `mip::MsgInspector`qui étend `mip::FileInspector` , expose les opérations de déchiffrement spécifiques au format de fichier rpmsg. Le kit de développement logiciel MIP ne prend pas en charge les scénarios de publication des fichiers *message. rpmsg* .

`mip::MsgInspector`la classe expose les membres suivants :

```cpp
public const std::vector<uint8_t>& GetBody()
public BodyType GetBodyType() const
public BodyType GetBodyType() const
public InspectorType GetInspectorType() const
public std::shared_ptr<Stream> GetFileStream() const
```

Pour plus d’informations, consultez [référence des API](./reference/mip-sdk-reference.md).

## <a name="next-steps"></a>Étapes suivantes

- Passez en revue le [fichier API-traiter les fichiers d’e-mail. MSG (C++) démarrage rapide](quick-email-msg-cpp.md)
- Passez en revue le [fichier API-traiter les fichiers d’e-mail. MSG (C#) démarrage rapide](quick-email-msg-csharp.md)