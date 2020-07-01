---
title: Journaux d’audit générés par Azure Information Protection-AIP
description: En savoir plus sur les journaux d’audit générés par Azure Information Protection-AIP.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cfcbc67d67375e1513373c26d935a5acdc041911
ms.sourcegitcommit: b7c4a6c3c343b53775cc4ffdecb966c32766dd6a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716042"
---
# <a name="azure-information-protection-audit-log-reference-public-preview"></a>Informations de référence sur le journal d’audit Azure Information Protection (version préliminaire publique)

>*S’applique à : [Azure information protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft Azure Information Protection génère des journaux d’audit au niveau des événements d’activité suivants :

* [y accéder](#access-audit-logs)
* [Accès refusé](#access-denied-audit-logs)
* [Protection contre les modifications](#change-protection-audit-logs)
* [Découvrir](#discover-audit-logs)
* [Étiquette de rétrogradation](#downgrade-label-audit-logs)
* [Fichier supprimé](#file-removed-audit-logs)
* [Nouvelle étiquette](#new-label-audit-logs)
* [Nouvelle protection](#new-protection-audit-logs)
* [Supprimer l’étiquette](#remove-label-audit-logs)
* [Supprimer la protection](#remove-protection-audit-logs)
* [Étiquette de mise à niveau](#upgrade-label-audit-logs)

## <a name="access-audit-logs"></a>Accéder aux journaux d’audit

Les journaux d’audit d' **accès** sont générés pour les activités suivantes :

|Signalé par  |Plateforme  |Application  |Action/Description  |
|---------|---------|---------|---------|
|Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié     | Windows        | Office        |Généré pour la première fois dans chaque session qu’un fichier étiqueté ou protégé est enregistré.<br>Le journal comprend toutes les correspondances de type d’informations.  <!-- plan to be removed -->    |
|Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié     |Windows         |Office         |Généré chaque fois qu’un fichier étiqueté ou protégé est créé.<!-- plan to be removed -->       |
|Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié     | Windows, SharePoint, OneDrive        | Office        | Généré chaque fois qu’un fichier étiqueté ou protégé est ouvert. </br></br>**Remarque :** Pour les fichiers protégés, les journaux d’audit d’accès sont générés uniquement lorsque le fichier est ouvert et que le contenu est correctement déchiffré et exposé à l’utilisateur. </br>Pour les e-mails protégés dans Outlook, les journaux d’audit d’accès sont également générés chaque fois que l’utilisateur tente d’ouvrir un e-mail chiffré, même si le déchiffrement est bloqué en raison d’autorisations insuffisantes. <!--limitations-->         |
|SDK Microsoft Information Protection (MIP)     | Quelconque        | Applications tierces        | Généré chaque fois qu’un fichier nommé ou protégé est accédé par une application tierce qui le prend en charge.       |
|Service RMS     | Windows        | Office         |Généré chaque fois qu’un document nommé ou protégé est accédé.<!-- plan to be removed -->       |


## <a name="access-denied-audit-logs"></a>Journaux d’audit de refus d’accès

Les journaux d’audit de **refus d’accès** sont générés pour les activités suivantes :

|Signalé par  |Plateforme  |Application  |Action/Description   |
|---------|---------|---------|---------|
|Service RMS     | Windows        | Office         |Généré chaque fois qu’un utilisateur tente d’accéder à un document protégé pour lequel il n’a pas d’autorisations.

## <a name="change-protection-audit-logs"></a>Modifier les journaux d’audit de protection

Les journaux d’audit de la **protection des modifications** sont générés pour les activités suivantes :

|Signalé par  |Plateforme  |Application  |Action/Description   |
|---------|---------|---------|---------|
|Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié     | Windows, SharePoint, OneDrive        | Office        | Généré chaque fois que la protection d’un document sans étiquette est modifiée manuellement.         |
|SDK Microsoft Information Protection (MIP)     | Quelconque        | Applications tierces        | Généré chaque fois que la protection d’un document sans étiquette est modifiée manuellement.<br>Généré uniquement s’il est pris en charge par l’application tierce.       |

## <a name="discover-audit-logs"></a>Détecter les journaux d’audit

**Découvrez** les journaux d’audit générés pour les activités suivantes :

|Signalé par  |Plateforme  |Application  |Action/Description   |
|---------|---------|---------|---------|
|Azure Information Protection :</br>-Scanneur classique </br>-Scanneur d’étiquetage unifié     | Windows        | Office        |Généré chaque fois qu’un fichier est analysé par le scanneur AIP.<br>Le journal contient les informations suivantes :<br>-Types d’informations identiques<br>-Étiquettes |
|SDK Microsoft Information Protection (MIP) | Quelconque | Applications tierces | Généré chaque fois qu’un fichier est analysé par une application tierce qui le prend en charge. </br>Le journal contient les informations suivantes :</br>-Types d’informations identiques</br>-Étiquettes|

## <a name="downgrade-label-audit-logs"></a>Déclasser les journaux d’audit des étiquettes

Les journaux d’audit des **étiquettes de rétrogradation** sont générés pour les activités suivantes :

| Signalé par      | Plateforme                       | Application              | Action/Description      |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
|Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette moins sensible.|
| Microsoft Defender - PACM            | Windows                        | Système d''exploitation                       | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette moins sensible. |
| SDK Microsoft Information Protection (MIP)          | Quelconque                            | Applications tierces | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette moins sensible.<br>Généré uniquement s’il est pris en charge par l’application tierce. |

## <a name="file-removed-audit-logs"></a>Fichiers journaux d’audit supprimés

> [!NOTE]
> Les journaux d’audit de fichiers supprimés ne sont pris en charge que dans Azure Information Protection version d’analyse [2.7.96.0](rms-client/unifiedlabelingclient-version-release-history.md#version-27960) et versions ultérieures.

Les journaux d’audit des **fichiers supprimés** sont générés pour les activités suivantes :

| Signalé par                                                                              | Plateforme | Application                     | Action/Description                                                          |
| ---------------------------------------------------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Scanneur Azure Information Protection, client d’étiquetage unifié | Windows  | Office et types de fichiers pris en charge | Généré chaque fois que l’analyseur AIP détecte qu’un fichier précédemment analysé a été supprimé. |

## <a name="new-label-audit-logs"></a>Nouveaux journaux d’audit des étiquettes

De nouveaux journaux d’audit des **étiquettes** sont générés pour les activités suivantes :

| Signalé par                                                                      | Plateforme                       | Application              | Action/Description                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois qu’une nouvelle étiquette est appliquée.                                                                  |
| Microsoft Defender - PACM                                                                            | Windows                        | Système d''exploitation                       | Généré chaque fois qu’une nouvelle étiquette de document est appliquée.                                                                  |
| SDK Microsoft Information Protection (MIP)                                                                          | Quelconque                            | Applications tierces | Généré chaque fois qu’une nouvelle étiquette de document est appliquée.<br>Généré uniquement lorsqu’il est pris en charge par l’application tierce. |

## <a name="new-protection-audit-logs"></a>Nouveaux journaux d’audit de protection

De nouveaux journaux d’audit de **protection** sont générés pour les activités suivantes :

| Signalé par                                                                      | Plateforme                       | Application              | Action/Description                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois que la protection est ajoutée manuellement, sans étiquette.                                                                  |
| SDK Microsoft Information Protection (MIP)                                                                          | Quelconque                            | Applications tierces | Généré chaque fois que la protection est ajoutée manuellement, sans étiquette.<br>Généré uniquement lorsqu’il est pris en charge par l’application tierce. |

## <a name="remove-label-audit-logs"></a>Supprimer les journaux d’audit des étiquettes

**Supprimer** les journaux d’audit des étiquettes sont générés pour les activités suivantes :

| Signalé par                                                                      | Plateforme                       | Application              | Action/Description                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois qu’une étiquette est supprimée.                                                                  |
| Microsoft Defender - PACM                                                                            | Windows                        | Système d''exploitation                       | Généré chaque fois qu’une étiquette est supprimée.                                                                  |
| SDK Microsoft Information Protection (MIP)                                                                          | Quelconque                            | Applications tierces | Généré chaque fois qu’une étiquette est supprimée.<br>Généré uniquement lorsqu’il est pris en charge par l’application tierce. |

## <a name="remove-protection-audit-logs"></a>Supprimer les journaux d’audit de protection

**Supprimer** les journaux d’audit de protection sont générés pour les activités suivantes :

| Signalé par                                                                      | Plateforme                       | Application              | Action/Description                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois que la protection est supprimée manuellement, sans étiquette.                                                                  |
| SDK Microsoft Information Protection (MIP)                                                                          | Quelconque                            | Applications tierces | Généré chaque fois que la protection est supprimée manuellement, sans étiquette.<br>Généré uniquement lorsqu’il est pris en charge par l’application tierce. |

## <a name="upgrade-label-audit-logs"></a>Mettre à niveau les journaux d’audit

Les journaux d’audit des **étiquettes de mise à niveau** sont générés pour les activités suivantes :

| Signalé par                                                                      | Plateforme                       | Application              | Action/Description                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection :</br>-Client classique</br>-Client d’étiquetage unifié | Windows, SharePoint, un lecteur | Office                   | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette plus sensible.                                                                   |
| Microsoft Defender - PACM                                                                            | Windows                        | Système d''exploitation                       | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette plus sensible.                                                                   |
| SDK Microsoft Information Protection (MIP)                                                                          | Quelconque                            | Applications tierces | Généré chaque fois qu’une étiquette de document est mise à jour avec une étiquette plus sensible.<br>Généré uniquement lorsqu’il est pris en charge par l’application tierce. |
